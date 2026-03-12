# Walkthrough Arena

istilah Walkthrough dalam dunia Menmbak / Shooting Sport, adalah kejadian untuk menelusuri jalannya target pada arena oleh Atlet yang akan melakukan shoorting dalam kompetisi Tembak Reaksi.
dalam cyber security, sebelum kita meretas atau pun menjaga jaringan harus tau dulu medan yang saat ini kita berada ada apa aja, untuk bisa kira kenali, dan membedakan itu orang kita atau orang lain yang masuk tanpa izin.

## Untuk mengetahui informasi jaringan pribadi Anda di Kali Linux, gunakan dua perintah utama berikut:

### 1. Cek IP Lokal Komputer Anda

Ketik `ip a` atau `ifconfig` di terminal. Cari bagian `wlan0` (untuk Wi-Fi) atau `eth0` (untuk kabel). Alamat IP Anda ada di sebelah kata **inet** (contoh: `192.168.1.15`).

### 2. Cek Perangkat yang Terhubung ke Wi-Fi

Gunakan alat bernama **Netdiscover** untuk memindai seluruh perangkat dalam jaringan yang sama:

* Jalankan: `sudo netdiscover -r [Range_IP/Subnet]`
* Contoh jika IP Anda 192.168.1.15: `sudo netdiscover -r 192.168.1.0/24`

### 3. Alternatif Menggunakan Nmap (Lebih Detail)

Anda juga bisa menggunakan Nmap untuk memindai siapa saja yang sedang "hidup" (*up*):

* `sudo nmap -sn 192.168.1.0/24`
* Perintah ini akan menampilkan daftar IP dan nama perangkat (jika tersedia) yang sedang tersambung ke router Anda.

**Kiat:** Perhatikan **MAC Address** yang muncul; biasanya vendor perangkat (seperti Samsung, Apple, atau TP-Link) akan terdeteksi sehingga Anda tahu jenis perangkat apa itu.

## Mengetahui siapa saja yang masuk atau menyusup pada jariangn router kita

Anda dapat menerapkan teknik yang sama untuk setiap IP yang terdeteksi di jaringan Anda. Gunakan **Nmap** untuk memeriksa pintu masuk (port) dan layanan yang aktif pada perangkat tersebut guna memahami identitasnya secara lebih mendalam.

Jalankan perintah ini di terminal Kali Linux:
`sudo nmap -sV -O [IP_Target]`

### Penjelasan Perintah:

* **`-sV`**: Mendeteksi **versi layanan** (misal: apakah itu printer, CCTV, atau ponsel Android).
* **`-O`**: Mencoba menebak **Sistem Operasi** (OS) yang digunakan perangkat tersebut.

Ini adalah cara terbaik untuk membedakan mana perangkat milik Anda dan mana yang mungkin penyusup.

## cara melihat "nama asli" (hostname) perangkat tersebut agar lebih mudah dikenali

Untuk melihat nama asli atau **hostname** perangkat, gunakan perintah `nmblookup -A [IP_Target]` atau `nslookup [IP_Target]`.

### Cara Cepat:

* **`nmblookup -A`**: Sangat efektif untuk perangkat Windows atau Android di jaringan lokal.
* **`nslookup`**: Mengecek nama perangkat melalui *database* DNS router Anda.
* **`sudo nmap -sL [IP_Range]`**: Melakukan "List Scan" untuk menarik semua nama perangkat dalam satu jaringan sekaligus tanpa mengirim paket serangan.

Dengan mengetahui hostname (seperti "Laptop-Andi" atau "CCTV-Teras"), Anda bisa langsung memastikan apakah IP tersebut milik keluarga atau penyusup.

## Cara membuka port di IP penyusup

Jika Anda menemukan IP asing, Anda dapat melakukan **Port Scanning** secara mendalam untuk melihat layanan apa yang mereka jalankan, yang mungkin menjadi celah untuk berkomunikasi atau mengidentifikasi perangkat tersebut.

Gunakan perintah agresif ini di Kali Linux:
`sudo nmap -p- -sV -A [IP_Penyusup]`

### Apa yang dilakukan perintah ini?

* **`-p-`**: Memeriksa **seluruh 65.535 port**, bukan hanya port populer. Penyusup sering menyembunyikan layanan di port yang tidak umum.
* **`-sV`**: Menentukan versi perangkat lunak yang berjalan. Ini krusial untuk mencari *exploit* yang spesifik.
* **`-A`**: Mengaktifkan deteksi OS, *script scanning*, dan *traceroute* secara bersamaan.

### Langkah Selanjutnya Jika Port Terbuka:

1. **Port 80/443**: Coba buka IP tersebut di browser; mungkin itu interface CCTV atau router yang tidak terenkripsi.
2. **Port 21/22/23**: Menandakan adanya layanan transfer file atau remote akses (FTP/SSH/Telnet).
3. **Port 445**: Menandakan berbagi file Windows (SMB) yang sering memiliki celah keamanan lama.

## Cara memutus perangkat asing yang masuk pada jaringan kita

Anda bisa menggunakan teknik **ARP Spoofing** untuk memutus koneksi perangkat asing dengan alat bernama `arpspoof` atau `bettercap`. Cara ini bekerja dengan memberi tahu perangkat target bahwa komputer Anda adalah router, lalu membuang paket datanya agar mereka kehilangan akses internet.

### Cara Memutus Koneksi dengan Bettercap:

1. **Instalasi**: `sudo apt install bettercap`
2. **Jalankan**: `sudo bettercap -iface wlan0` (ganti `wlan0` dengan interface Wi-Fi Anda).
3. **Eksekusi Perintah**:
* `net.probe on` (mencari semua perangkat).
* `set arp.spoof.targets [IP_TARGET]` (masukkan IP penyusup).
* `arp.spoof on` (mulai memutus koneksi).

**Catatan Penting:** Gunakan ini hanya di jaringan pribadi Anda untuk tujuan belajar. Memutus koneksi di jaringan publik tanpa izin adalah tindakan ilegal.

