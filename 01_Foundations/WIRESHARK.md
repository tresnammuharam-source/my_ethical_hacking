# WIRESHARK

Wire Shark adalah alat untuk memantau pergerakan packet yang ada pada lalu lintas jaringan.
dengan melihat packet yang melintas kita bisa melakukan analisa apakah packet tersebut mencurigakan atau tidak.

## Memantau Pergerakan Packet di wire shark pada proses pengintaian (reconnasainnce)

Melakukan pengintaian (*reconnaissance*) sambil memantau log aktivitas sendiri adalah cara terbaik untuk memahami bagaimana sistem keamanan (seperti IDS/IPS) mendeteksi jejak digital Anda.

Berikut adalah panduan instalasi dan penggunaan Wireshark di Kali Linux.

---

## 1. Cara Instalasi Wireshark di Kali Linux

Kali Linux biasanya sudah menyertakan Wireshark secara *default*. Namun, jika belum ada atau Anda ingin memastikan versinya yang terbaru, ikuti langkah berikut:

1. **Update Repository:**
Buka terminal dan jalankan perintah:
`sudo apt update`
2. **Instalasi Wireshark:**
Jalankan perintah:
`sudo apt install wireshark -y`
3. **Konfigurasi Hak Akses (Penting):**
Agar Anda bisa menjalankan Wireshark tanpa terus-menerus menggunakan `sudo`, jalankan perintah:
`sudo dpkg-reconfigure wireshark-common`
Pilih **Yes** pada jendela yang muncul.
4. **Tambahkan User ke Group:**
Masukkan user Anda ke grup Wireshark agar bisa menangkap paket:
`sudo usermod -aG wireshark $USER`
5. **Restart VM:**
Lakukan *reboot* pada Kali Linux Anda agar perubahan grup tersebut aktif.

---

## 2. Tutorial Singkat Penggunaan Wireshark

Setelah instalasi selesai, Anda bisa mulai memantau trafik yang keluar dari VM Anda.

### A. Memilih Interface

Buka Wireshark melalui menu aplikasi atau ketik `wireshark` di terminal. Di halaman utama, Anda akan melihat daftar *interface* jaringan (seperti `eth0` atau `wlan0`). Pilih interface yang memiliki grafik aktivitas (menandakan ada trafik) dan klik ikon **Sirip Hiu Biru** di pojok kiri atas untuk mulai menangkap paket.

### B. Membaca Panel Wireshark

Wireshark membagi tampilannya menjadi tiga bagian utama:

* **Packet List (Atas):** Daftar semua paket yang tertangkap (waktu, sumber IP, tujuan IP, protokol).
* **Packet Details (Tengah):** Rincian mendalam dari protokol paket yang dipilih (Layer 2 hingga Layer 7).
* **Packet Bytes (Bawah):** Data mentah dalam bentuk heksadesimal.

### C. Menggunakan Filter

Saat melakukan *recon*, trafik akan sangat padat. Gunakan kolom filter di bagian atas untuk menyaring data:

* **Filter IP Tujuan:** `ip.dst == [IP_Target]`
* **Filter Protokol:** `tcp`, `udp`, `http`, atau `icmp`.
* **Filter Port:** `tcp.port == 80` atau `udp.port == 53`.

---

## 3. Contoh Skenario: Memantau Log Reconnaissance

Jika Anda mencoba melakukan *scanning* dengan Nmap ke target luar jaringan, berikut cara melihat "jejak" Anda:

1. Jalankan Wireshark dan mulai *Capture*.
2. Buka terminal baru, lakukan scan sederhana: `nmap -sS [IP_Target]`.
3. Kembali ke Wireshark, ketik `tcp.flags.syn == 1 && tcp.flags.ack == 0` di kolom filter.
4. **Apa yang Anda lihat?** Anda akan melihat rentetan paket **TCP SYN** yang dikirimkan Kali Linux Anda ke berbagai port target dalam waktu singkat. Inilah log yang biasanya memicu alarm pada *firewall* target.

### Tips Tambahan untuk VM:

Pastikan pengaturan jaringan di VMware Anda menggunakan mode **Bridged** jika ingin berinteraksi langsung dengan perangkat di jaringan fisik, atau **NAT** jika hanya ingin keluar ke internet melalui IP host. Jika Anda menggunakan mode **Host-Only**, Anda tidak akan bisa melakukan *recon* ke luar jaringan.

Ada protokol atau jenis serangan tertentu yang ingin Anda pelajari cara deteksinya di Wireshark?
