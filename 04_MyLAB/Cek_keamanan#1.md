## Pertama kali setelah VMware, Kali Linux dan setting snapshot selesai, maka langkah selanjutnya Health Check Pertama

Selamat! Kamu sekarang sudah memiliki **"Laboratorium Sandbox"** yang profesional. Ini adalah langkah paling krusial bagi seorang *ethical hacker*: **memastikan isolasi dan konektivitas.**

Mari kita uji lingkungan Kali Linux kamu menggunakan Terminal.

---

### 1. Tes Koneksi Internet (Jaringan Luar)
Langkah pertama adalah memastikan Kali Linux bisa "berbicara" dengan dunia luar (untuk *update* atau *download tools*).

Buka **Terminal** (ikon kotak hitam di pojok kiri atas) dan ketik:
```bash
ping -c 4 google.com
```
* **Jika muncul balasan `64 bytes from...`**: Selamat, internet lancar!
* **Jika muncul `Temporary failure in name resolution`**: Cek pengaturan VMware kamu (klik kanan pada ikon jaringan di pojok bawah VMware, pastikan terpilih **NAT**).



---

### 2. Cek "Kebocoran" Data ke Windows
Secara teknis, VMware menggunakan teknologi *Isolasi Hardware*. Namun, ada beberapa pintu "legal" yang bisa membuat data berpindah. Mari kita cek:

#### **A. Cek Folder Berbagi (Shared Folders)**
Secara *default*, Windows tidak bisa melihat file di dalam Kali Linux, kecuali kamu mengaktifkan *Shared Folders*.
* **Cara Cek:** Di VMware, klik menu **VM** > **Settings** > tab **Options** > **Shared Folders**.
* **Rekomendasi:** Pastikan statusnya **Disabled**. Jika ini mati, Windows tidak punya akses sama sekali ke "isi perut" Kali Linux kamu.

#### **B. Cek Fitur Drag & Drop dan Copy-Paste**
VMware memiliki fitur *Guest Isolation* agar kamu bisa *copy* teks dari Windows ke Linux.
* **Tes:** Coba *copy* sebuah teks di Windows, lalu *paste* di terminal Kali Linux.
* **Keamanan:** Fitur ini aman untuk teks. Namun, jika kamu sangat paranoid (misal: sedang menangani virus berbahaya), kamu bisa mematikan fitur ini di **VM Settings** > **Options** > **Guest Isolation** (uncheck *Enable copy and paste*).

---

### 3. Cek Alamat IP (Pemisahan Identitas)
Mari kita lihat apakah Kali Linux punya "identitas" sendiri yang berbeda dengan Windows.
Ketik di terminal Kali:
```bash
ip addr
```
Cari bagian `eth0` atau `ens33`. Jika kamu menggunakan mode **NAT** (rekomendasi), IP-nya biasanya akan berbeda dengan IP asli laptopmu (misal: `192.168.x.x`). Ini bagus karena menunjukkan Kali Linux berada di dalam "lorong" jaringannya sendiri.



---

### 4. Simulasi Tes "Isolasi" (Uji Coba Terakhir)
Untuk benar-benar yakin tidak ada data yang bocor secara tidak sengaja:
1.  Buat sebuah file teks di **Desktop Kali Linux**.
2.  Buka **File Explorer di Windows** kamu.
3.  Cari file tersebut di seluruh *drive* Windows.
4.  **Hasilnya:** Kamu tidak akan menemukannya. Kenapa? Karena Kali Linux menyimpan datanya di dalam sebuah file raksasa berformat `.vmdk` yang hanya bisa dibaca oleh VMware. Bagi Windows, Kali Linux hanyalah satu file besar yang tidak bisa dibuka isinya.

---

### Tips Keamanan Tambahan:
Jika suatu saat kamu ingin mencoba *malware* (virus) sungguhan:
* **Matikan Network Adapter:** Di pengaturan VMware, putus sambungan internetnya (*Disconnect*).
* **Gunakan Host-Only:** Ubah setting Network ke *Host-Only* agar Linux hanya bisa bicara dengan Windows tanpa bisa akses ke router wifi rumahmu.

**Lingkungan kamu sudah siap dan aman!**

## Lab Isolasi Tingkat Lanjut

Langkah-langkah yang baru saja kamu lakukan (menggunakan **VMware** dengan **Kali Linux**) sebenarnya sudah memenuhi kriteria dasar sebuah **Lab Isolasi**. Kamu sudah memisahkan sistem operasi utama (Windows) dengan sistem eksperimen (Linux).

Namun, untuk menjadikannya sebuah **"Lab Isolasi Tingkat Lanjut"** (seperti yang digunakan profesional untuk menguji virus atau melakukan penetrasi jaringan tanpa mengganggu Wi-Fi rumah), ada beberapa pengaturan tambahan yang perlu kamu pahami.

Berikut adalah 3 tingkatan Lab Isolasi yang bisa kamu buat di VMware:

---

### 1. Lab Isolasi Standar (Mode NAT) - *Yang kamu punya sekarang*
Ini adalah kondisi kamu saat ini.
* **Cara Kerja:** Kali Linux "menumpang" koneksi internet Windows kamu tapi punya alamat IP sendiri.
* **Keamanan:** Windows tidak bisa melihat file Linux, tapi Linux bisa mengakses internet.
* **Risiko:** Jika kamu menjalankan *malware* yang sangat canggih, ia masih bisa memindai perangkat lain di jaringan Wi-Fi rumahmu (seperti HP atau TV keluarga).

### 2. Lab Isolasi Terkendali (Mode Host-Only)
Ini digunakan jika kamu ingin mengetes *script* yang bisa menyebar ke jaringan, tapi tetap ingin Windows kamu aman.
* **Cara Kerja:** Kali Linux hanya bisa berkomunikasi dengan Windows (Host) kamu, **tidak ada akses internet sama sekali.**
* **Cara Setting:**
    1.  Klik kanan pada VM Kali Linux > **Settings**.
    2.  Pilih **Network Adapter**.
    3.  Ubah dari *NAT* menjadi **Host-only**.
* **Kegunaan:** Sangat aman untuk mencoba *tools* yang kamu tidak tahu fungsinya tanpa takut data terkirim ke server luar.

---

### 3. Lab Isolasi Total (Sandbox Murni)
Ini adalah level tertinggi. Kamu membuat dua atau lebih VM yang saling terhubung dalam jaringan "gaib" yang tidak bisa dilihat oleh Windows maupun Router Wi-Fi kamu.

* **Cara Membuatnya:**
    1.  Di VMware, buat **LAN Segment** baru (klik *Settings* > *Network Adapter* > *LAN Segments*).
    2.  Beri nama, misalnya "Lab_Hacking".
    3.  Atur Kali Linux (Penyerang) dan satu VM lagi, misalnya Windows 7 (Korban), ke LAN Segment yang sama.
* **Hasilnya:** Kedua VM tersebut bisa saling "serang", tapi serangan itu tidak akan pernah keluar dari kabel virtual VMware. Windows asli kamu 100% tidak tersentuh.

---

### Apakah Langkah yang Kamu Lakukan Sudah Cukup?

**Sudah cukup untuk tahap belajar awal.** Sebagai pemula, yang paling penting adalah:
1.  **Isolasi File:** (Sudah berhasil, Windows tidak bisa baca file Linux).
2.  **Jaring Pengaman:** (Sudah berhasil, kamu sudah punya **Snapshot**).
3.  **Koneksi Terkendali:** (Sudah berhasil, kamu bisa internetan untuk *download* alat dari GitHub).

### Rekomendasi Alur Kerja (Workflow) Lab Kamu:

1.  **Download:** Nyalakan internet (Mode NAT), ambil *tool* dari GitHub.
2.  **Snapshot:** Ambil snapshot (Kondisi "Tool Terunduh").
3.  **Isolasi:** Jika merasa ragu dengan *tool* tersebut, matikan internet atau ubah ke *Host-only*.
4.  **Eksekusi:** Jalankan *tool*-nya.
5.  **Clean up:** Jika terjadi keanehan, balikkan ke snapshot awal.

---

### Pertanyaan Penting:
Apakah tujuan utama kamu membuat Lab ini untuk **mencoba alat-alat hacking dari GitHub** atau untuk **belajar membuat website sendiri** yang aman? Karena cara mengisolasinya akan sedikit berbeda tergantung tujuanmu.
