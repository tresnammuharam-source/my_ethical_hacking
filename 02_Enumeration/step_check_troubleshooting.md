# Troubleshooting

Sebagai praktisi cybersecurity, ketika ada perbedaan signifikan antara alokasi *bandwidth* (200 Mbps) dan hasil *realized speed* (40–50 Mbps), kita tidak langsung menyalahkan ISP. Kita lakukan **sistematik troubleshooting** dari *layer physical* (kabel & perangkat) hingga *layer software/network* untuk menemukan *bottleneck*-nya.

Kecepatan tertahan di kisaran 40–50 Mbps biasanya menandakan adanya **port LAN/adaptor Wi-Fi yang berjalan di mode 100 Mbps (Fast Ethernet)**, koneksi Wi-Fi di frekuensi 2.4 GHz, atau pembatasan pada sisi router/sistem.

---

### Phase 1: Isolasi Fisik & Hardware (Physical & Datalink Layer)

1. **Cek Frekuensi Wi-Fi (2.4 GHz vs 5 GHz):** Prasyarat Utama.
Wi-Fi frekuensi 2.4 GHz memiliki batas nyata sekitar 40–60 Mbps karena interfrensi sinyal dan lebar pita yang sempit.

* Pastikan PC terhubung ke SSID Wi-Fi pita **5 GHz** (biasanya bernama `NamaWi-Fi_5G`).
* *Verification:* Buka **Settings > Network & internet > Wi-Fi > Properties**, pastikan **Network band** tertulis **5 GHz**.


2. **Verifikasi Link Speed pada Adaptor Jaringan:** Windows 11 Settings.
Jika terhubung lewat kabel LAN atau Wi-Fi 5 GHz, periksa kapasitas batas fisik (*Link Speed*) yang dibaca oleh Windows.

1. Tekan `Win + R`, ketik `ncpa.cpl`, lalu tekan **Enter**.
2. Klik ganda pada adaptor yang aktif (**Ethernet** atau **Wi-Fi**).
3. Cek pada baris **Speed**.

* *Verification:* Nilai **Speed** harus menunjukkan **1.0 Gbps (1000 Mbps)** atau minimal di atas **300 Mbps**. Jika tertulis **100.0 Mbps**, maka batas fisik jaringan Anda terkunci di 100 Mbps (sehingga speedtest maksimal hanya ~40-50 Mbps).


3. **Periksa Spesifikasi Router & Kabel LAN:** Hardware Audit.
1. **Router/Modem ISP:** Pastikan port LAN pada router Bnetfit mendukung **Gigabit Ethernet (10/100/1000 Mbps)**, bukan Fast Ethernet (10/100 Mbps).
2. **Kabel LAN:** Jika menggunakan kabel, pastikan kabel minimal kategori **Cat5e** atau **Cat6**.

* *Verification:* Periksa cetakan tulisan di sepanjang kabel LAN, pastikan tertera `CAT5E` atau `CAT6`.


---

### Phase 2: Analisis & Konfigurasi Sistem Windows 11

1. **Matikan Bandwidth Throttling / QOS di Windows:** Registry Adjustment.
Windows 11 memiliki fitur *Network Throttling Index* dan *Delivery Optimization* yang kadang membatasi kecepatan unduh.

1. Tekan `Win + R`, ketik `regedit`, tekan **Enter**.
2. Buka path: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile`
3. Klik ganda pada `NetworkThrottlingIndex`, ubah nilainya menjadi `ffffffff` (Hexadecimal) untuk mematikan throttling.

* *Verification:* Nilai `NetworkThrottlingIndex` berubah menjadi `0xffffffff`.


2. **Reset TCP/IP Stack & Flush DNS:** Command Prompt (Admin).
Tumpukan protokol jaringan yang korup dapat membatasi *throughput* paket data.

1. Buka CMD sebagai **Administrator** (`Win + X` > **Terminal (Admin)**).
2. Jalankan perintah berikut secara berurutan:

```cmd
netsh int ip reset
netsh winsock reset
ipconfig /flushdns

```

3. Restart PC Anda.

* *Verification:* Terminal menampilkan pesan sukses untuk reset Winsock dan IP.


3. **Update / Rollback Driver Network Adapter:** Device Manager.
Driver adaptor jaringan yang usang sering kali gagal melakukan negosiasi kecepatan (*auto-negotiation*) ke tingkat Gigabit.

1. Tekan `Win + X`, pilih **Device Manager**.
2. Perluas **Network adapters**, klik kanan pada kartu Wi-Fi / Ethernet Anda, lalu pilih **Properties**.
3. Masuk ke tab **Advanced**, cari properti **Speed & Duplex** (untuk Ethernet) dan ubah dari *Auto Negotiation* ke **1.0 Gbps Full Duplex**.

* *Verification:* Adaptor tetap terhubung tanpa terputus dan menunjukkan negosiasi Gigabit.


---

### Phase 3: Validasi Akhir & Poin Kontak ISP

Setelah melakukan langkah-langkah di atas, lakukan pengujian ulang:

1. **Jalankan iPerf3 / Speedtest Multi-Server:** Gunakan Speedtest CLI atau aplikasi native Speedtest (bukan browser) untuk menghindari limitasi *browser rendering*.
2. **Uji Perangkat Lain:** Gunakan smartphone flagship/laptop lain yang mendukung Wi-Fi 5GHz/Gigabit LAN tepat di samping router.
* **Jika perangkat lain berhasil mendapat ~200 Mbps:** Masalah murni berada pada konfigurasi/hardware PC Windows 11 Anda.
* **Jika semua perangkat tetap tertahan di 40–50 Mbps:** Masalah berada pada **profil paket di sisi ISP (Bnetfit)** yang belum diperbarui di OLT/Server mereka, atau router dari ISP belum diganti ke tipe Gigabit.
