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

---

# Security Misconfigurations

Teks ini membahas salah satu risiko paling sering dieksploitasi di dunia nyata: **AS02: Security Misconfigurations (Salah Konfigurasi Keamanan)**.

Sebagai *cybersecurity professional*, saya melihat celah ini sebagai "kelalaian operasional". Ini bukan masalah kodenya yang salah tulis oleh developer, melainkan masalah **kecerobohan saat melakukan deployment dan pengaturan (setup) infrastruktur**.

Berikut adalah pembedahan teknis dari setiap poin teks tersebut:

### 1. Definisi & Dampak (What It Is & Why It Matters)

* **Bukan Bug Kode:** Teks menegaskan bahwa ini bukan kesalahan logika pemrograman (*code bugs*). Aplikasi bisa saja ditulis dengan sangat aman, tetapi jika dijalankan di atas server yang konfigurasinya berantakan, sistem tetap akan jebol.
* **Luasnya Attack Surface:** Aplikasi modern sangat kompleks karena melibatkan server, *cloud storage*, API pihak ketiga, hingga *container* (seperti Docker). Satu saja pintu kecil terbuka—misalnya panel admin yang bisa diakses publik—maka seluruh arsitektur sistem di belakangnya bisa ikut runtuh (*compromised*).

### 2. Studi Kasus Nyata: Uber (2017)

Teks tersebut membawa contoh riil yang sangat terkenal. Uber mengalami kebocoran data masif karena mereka melakukan kesalahan fatal: **membiarkan AWS S3 Bucket (penyimpanan cloud) mereka terekspos secara publik ke internet**.

* *Attacker* tidak perlu melakukan teknik *hacking* yang rumit seperti SQL Injection atau membobol password. Mereka hanya perlu menemukan URL bucket tersebut dan mengunduh seluruh data sensitif driver dan penumpang langsung dari sana.

---

### 3. Pola Celah yang Sering Ditemui (Common Patterns)

Di lapangan, tim *infosec* paling sering menemukan 7 pola kecerobohan ini:

* **Default Credentials:** Membiarkan *password* bawaan pabrik aktif (seperti `admin:admin`, `root:root`).
* **Exposed Unnecessary Services:** Membuka *port* atau layanan yang tidak diperlukan ke internet publik (misalnya membuka port database `3306` atau port *remote* `22` tanpa proteksi IP).
* **Misconfigured Cloud Storage:** Kasus seperti Uber di atas (S3 Bucket bocor).
* **Verbose Error Messages:** Ketika web mengalami error, web tersebut menampilkan *Stack Trace* (detail baris kode, versi framework, hingga struktur database) ke pengguna umum. Ini adalah informasi emas untuk *attacker* melakukan *reconnaissance*.
* **Exposed AI/ML Endpoints:** Tren baru di tahun 2025/2026, di mana pengembang membuka API untuk model AI/Machine Learning mereka tanpa adanya proteksi autentikasi di depannya.

---

### 4. Cara Pencegahan (How To Prevent It)

Untuk mengamankan sistem, pendekatan yang harus diambil adalah **System Hardening** dan **Principle of Least Privilege**:

* Matikan semua fitur, port, dan layanan yang tidak digunakan.
* Ubah semua kredensial bawaan sebelum server menyentuh lingkungan produksi (*production*).
* Sembunyikan pesan error yang terlalu detail dari publik; alihkan log error tersebut ke server log internal.
* **DevSecOps:** Integrasikan *automated configuration audit tools* ke dalam *CI/CD pipeline*, sehingga jika ada konfigurasi yang bocor/salah sebelum *deployment*, sistem akan otomatis menolaknya.

---

### 5. Panduan Menjawab Challenge Lab

Bagian akhir teks adalah misi praktis Anda di TryHackMe:

* **Target IP:** Buka browser di *AttackBox* atau mesin lokal Anda yang sudah terhubung VPN, lalu akses alamat: `[http://10.48.134.216:5002](http://10.48.134.216:5002)`.
* **Petunjuk Serangan (Clue):** Teks menyebutkan *"the developers left too many traces in their User Management APIs"* (developer meninggalkan terlalu banyak jejak/informasi pada API Manajemen Pengguna mereka).
* **Taktik Taktis Anda:**
1. Saat membuka web tersebut, lakukan inspeksi pada fitur login atau manajemen user.
2. Periksa dokumentasi API yang mungkin terekspos (seperti `/api`, `/swagger.json`, atau `/v1/users`).
3. Sengaja buat *request* yang error (misal memasukkan input asal pada form login) untuk melihat apakah sistem menampilkan *verbose error/stack trace* yang membocorkan informasi kredensial atau *endpoint* rahasia.
4. Cari informasi sensitif yang bocor dari respons API tersebut untuk mendapatkan *flag* berikutnya.

