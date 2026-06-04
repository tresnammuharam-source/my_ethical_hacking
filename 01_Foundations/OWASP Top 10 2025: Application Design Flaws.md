# OWASP Top 10 2025: Application Design Flaws

Teks ini merupakan deskripsi pengantar (*intro*) untuk **room TryHackMe yang berbeda**, yang berfokus pada pilar **Architecture & System Design (AS)** dalam daftar OWASP Top 10 2025.

Sebagai *cybersecurity specialist*, jika room sebelumnya (IAAA) berfokus pada kesalahan penanganan identitas dan akses, room yang ini berfokus pada **salah urus konfigurasi, cacat cetak biru (blueprint) aplikasi, dan kelemahan komponen pihak ketiga**.

Berikut adalah pembedahan teknis mengenai maksud dari tulisan tersebut:

### 1. Fokus Utama: Kegagalan Arsitektur & Desain Sistem

Kalimat awal menegaskan bahwa room ini membedah 4 kategori risiko yang lahir dari keputusan arsitektur yang buruk sejak awal sistem dirancang, bukan sekadar kesalahan pengetikan kode oleh developer.

Berikut adalah 4 kategori yang dicakup:

* **AS02: Security Misconfigurations (Salah Konfigurasi Keamanan)**
* *Maksudnya:* Sistem dideploy menggunakan pengaturan *default* (bawaan pabrik), mengaktifkan fitur/fitur *debugging* yang tidak diperlukan di server produksi, atau membiarkan kredensial standar (seperti `admin:admin`) tetap aktif.

* **AS03: Software Supply Chain Failures (Kegagalan Rantai Pasok Perangkat Lunak)**
* *Maksudnya:* Aplikasi menggunakan *library*, *framework*, atau modul pihak ketiga yang sudah usang atau mengandung celah keamanan (*vulnerable dependency*). Penyerang mengeksploitasi kode milik pihak ketiga tersebut untuk masuk ke sistem utama Anda.

* **AS04: Cryptographic Failures (Kegagalan Kriptografi)**
* *Maksudnya:* Penggunaan algoritma enkripsi yang sudah usang/lemah (seperti MD5 atau SHA1), pengiriman data sensitif melalui protokol tidak aman (HTTP biasa), atau penyimpanan kunci enkripsi (*key management*) yang ceroboh di dalam kode (*hardcoded keys*).

* **AS06: Insecure Design (Desain Tidak Aman)**
* *Maksudnya:* Aplikasi sejak awal dirancang tanpa memikirkan aspek keamanan (*security by design*). Contohnya: Alur bisnis yang cacat logikanya sehingga bisa diakali, atau tidak adanya mekanisme *fail-safe* ketika sistem mengalami error.

---

### 2. Instruksi Teknis Memulai Lab (Deploy Practical)

Bagian kedua adalah panduan operasional wajib sebelum Anda bisa mengerjakan tantangan praktisnya:

* **Jalankan VM Target:** Anda diinstruksikan untuk menekan tombol hijau bertuliskan **"Start Lab Machine"** di bagian atas task untuk menyalakan mesin virtual target (server yang sengaja dibuat rentan untuk dieksploitasi).
* **Metode Koneksi:** Teks ini mengingatkan bahwa Anda tidak bisa mengakses server target begitu saja dari internet publik. Anda wajib menggunakan salah satu dari dua jalur akses ini:
1. **AttackBox:** Menggunakan mesin penyerang berbasis browser yang sudah disediakan langsung oleh TryHackMe.
2. **Mesin Sendiri via VPN:** Menggunakan OS hacking Anda sendiri (seperti Kali Linux) yang sudah terhubung dengan jaringan internal TryHackMe menggunakan file konfigurasi **OpenVPN**.

