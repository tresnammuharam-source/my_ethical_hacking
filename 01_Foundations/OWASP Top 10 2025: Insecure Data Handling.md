# OWASP Top 10 2025: Insecure Data Handling

Teks ini merupakan pengantar (*intro*) untuk room ketiga, yaitu **OWASP Top 10 2025: Insecure Data Handling**.

Jika modul-modul sebelumnya berfokus pada Identitas (IAAA) dan Arsitektur (System Design), room kali ini berfokus pada **bagaimana aplikasi memproses, menerima, dan mengelola data serta input dari pengguna**. Kesalahan di area ini sering kali berujung pada eksploitasi yang sangat destruktif.

Berikut adalah pembedahan teknis dari sudut pandang *cybersecurity*:

### 1. Inti Pembelajaran: Perilaku Aplikasi & Input Pengguna

Teks tersebut menyatakan bahwa Anda akan mempelajari elemen yang berkaitan dengan *application behaviour* (bagaimana aplikasi merespons data) dan *user input* (input yang dimasukkan oleh pengguna).

Di dunia nyata, aturan nomor satu dalam *secure coding* adalah: **"Never trust user input"** (Jangan pernah percaya input dari user). Jika aplikasi menerima input mentah dari pengguna tanpa melakukan validasi, sanitasi, atau filtrasi yang ketat, aplikasi tersebut dipastikan rentan.

---

### 2. Tiga Kategori Kerentanan yang Dicakup

Room ini akan membedah 3 risiko keamanan spesifik:

* **A04: Cryptographic Failures (Kegagalan Kriptografi)**
* *Konteks di room ini:* Bagaimana data sensitif yang diinput atau disimpan oleh pengguna tidak dilindungi dengan enkripsi yang kuat, sehingga bisa diintip atau dimodifikasi dalam proses penanganan data (*data handling*).


* **A05: Injection (Injeksi)**
* *Maksudnya:* Salah satu celah paling klasik dan mematikan (seperti SQL Injection, Command Injection, atau Cross-Site Scripting/XSS). Terjadi ketika input berbahaya yang dimasukkan oleh *attacker* justru dianggap sebagai perintah/kode oleh interpreter server, sehingga server mengeksekusi perintah ilegal tersebut.


* **A08: Software or Data Integrity Failures (Kegagalan Integritas Perangkat Lunak atau Data)**
* *Maksudnya:* Aplikasi menerima data atau objek (seperti file update, data serial, atau *cookies*) tanpa memverifikasi integritasnya (apakah data tersebut asli atau sudah diubah di tengah jalan oleh penyerang). Contoh populersnya adalah *Insecure Deserialization*.


---

# A04: Cryptographic Failures (Kegagalan Kriptografi)

### 3. Alur Praktis & Instruksi Lab (Deploy Practical)

Sama seperti room sebelumnya, Anda tidak hanya belajar teori tetapi akan melakukan simulasi serangan (*practice exploiting*).

* **Persiapan:** Anda wajib menekan tombol hijau **"Start Lab Machine"** untuk menyalakan komputer target di server TryHackMe.
* **Akses:** Anda harus menggunakan **AttackBox** (kali linux berbasis browser milik THM) atau **mesin hacking sendiri** (seperti Kali Linux di VirtualBox) yang sudah tersambung ke jaringan internal menggunakan **OpenVPN TryHackMe**. Tanpa ini, Anda tidak akan bisa mengakses alamat IP laboratorium praktisnya nanti.

---

Teks ini membahas pengulangan materi **A04: Cryptographic Failures**, namun kali ini dengan fokus yang sangat spesifik pada **kesalahan penanganan data pengguna (Insecure Data Handling)** dan kesalahan fatal akibat membuat algoritma enkripsi sendiri.

Berikut adalah pembedahan teknis dari sudut pandang *cybersecurity*:

### 1. Inti Masalah: Kesalahan Fatal "Rolling Your Own Crypto"

Teks tersebut menyoroti sebuah fenomena yang sering menjadi lelucon sekaligus mimpi buruk di dunia siber: **Aplikasi yang mencoba membuat algoritma enkripsi mereka sendiri** (*rolling their own cryptography*).

Kriptografi adalah ilmu matematika tingkat tinggi yang membutuhkan audit bertahun-tahun oleh komunitas global sebelum dinyatakan aman. Ketika seorang developer mencoba membuat logika acakan teks sendiri (misal dengan memanipulasi string atau XOR sederhana), *attacker* berpengalaman bisa dengan mudah memetakan pola matematisnya (*pattern recognition*) dan membalikkan enkripsi tersebut untuk membaca data asli tanpa perlu tahu kuncinya.

Selain itu, teks kembali mengingatkan bahaya laten dari:

* Menyimpan password tanpa di-*hash* (teks polos).
* Menggunakan algoritma purba yang sudah pecah seperti **MD5**, **SHA1**, atau **DES**.

---

### 2. Solusi Defensif yang Direkomendasikan

Untuk mencegah kebocoran data, teks memberikan panduan standar industri:

* **Password Hashing:** Untuk data kredensial seperti password, jangan gunakan enkripsi biasa (yang bisa dibolak-balik), melainkan gunakan fungsi *hashing* yang sengaja dirancang lambat (*slow hashing functions*) seperti **bcrypt**, **scrypt**, atau **Argon2**. Ini bertujuan agar jika database bocor, *attacker* akan membutuhkan waktu puluhan tahun untuk melakukan *brute-force*.
* **Gunakan Library Standar:** Selalu gunakan pustaka resmi yang sudah tersertifikasi (seperti OpenSSL atau library bawaan bahasa pemrograman yang aman).
* **Environment Variables:** Jangan pernah menaruh *secret key* di dalam file `config` yang masuk ke Git. Gunakan *environment variables* atau *Secret Manager*.

---

### 3. Panduan Mengerjakan Lab Praktis (Misi Anda)

* **Target URL:** `http://[MACHINE_IP]:8001` (Ganti `[MACHINE_IP]` dengan IP dari VM yang Anda nyalakan dengan tombol hijau).
* **Skenario Lab:** Aplikasi web ini adalah penyedia layanan berbagi catatan (*note sharing service*).
* **Celah Keamanan (The Flaw):** Aplikasi ini menggunakan kunci enkripsi yang lemah dan **kuncinya diturunkan dari nilai yang dipakai bersama-sama (*shared derivative key*)**. Artinya, kunci untuk mengunci catatan User A dan User B memiliki pola pembentuk yang sama atau saling berkaitan.

#### Taktik Eksekusi Anda di Lab:

1. Buka alamat web tersebut di browser Linux Anda.
2. Ikuti petunjuk atau langkah-langkah yang tertera di halaman web utama. Biasanya Anda akan diminta melihat satu catatan yang terbuka, lalu menganalisis bagaimana parameter atau struktur kuncinya dibuat.
3. Karena kuncinya bersifat derivatif/turunan yang lemah, Anda kemungkinan besar bisa menebak atau memanipulasi token/kunci tersebut untuk membuka catatan-catatan rahasia milik user lain.
4. Buka semua catatan yang ada hingga Anda menemukan catatan tersembunyi yang berisi flag TryHackMe (**`THM{...}`**).
