# OWASP Top 10 2025: IAAA Failures

## Summary

Room TryHackMe **"OWASP Top 10 2025: IAAA Failures"** adalah bagian dari modul terbaru yang membahas kegagalan dalam pilar dasar keamanan informasi, yaitu **IAAA (Identity, Authentication, Authorisation, dan Accountability)**. Room ini memetakan model IAAA tersebut ke dalam 3 kategori kerentanan utama yang ada pada daftar OWASP Top 10 terbaru.

Berikut adalah penjelasan detail, urutan task, serta konsep simulasi praktis yang ada di dalam room tersebut.

---

## Konsep Dasar: Apa itu IAAA?

Sebelum masuk ke taks praktis, room ini meletakkan fondasi tentang apa itu **IAAA**:

1. **Identity (Identitas):** Siapa Anda? (Contoh: Username atau Email).
2. **Authentication (Autentikasi):** Membuktikan bahwa Anda benar-benar pemilik identitas tersebut (Contoh: Password, OTP, Passkey).
3. **Authorisation (Otorisasi):** Apa saja yang boleh Anda lakukan atau akses setelah masuk? (Contoh: User biasa vs Admin).
4. **Accountability (Akuntabilitas):** Pencatatan jejak digital untuk membuktikan siapa melakukan apa dan kapan (Contoh: Log audit/SIEM).

Jika salah satu komponen di atas gagal diterapkan dengan baik oleh developer, maka terjadilah **IAAA Failures**.

---

## Urutan Task dan Simulasi di Room TryHackMe

Berdasarkan struktur roomnya, berikut adalah detail pembahasan tiap task beserta gambaran simulasinya:

### Task 1 & 2: Introduction & What is IAAA?

* **Fokus:** Penjelasan teoritis mengenai model IAAA dan bagaimana model ini menjadi pondasi keamanan aplikasi web.
* **Inti Materi:** Mengenalkan bahwa kegagalan mengelola 4 aspek ini akan membuka celah bagi penyerang untuk menyamar, memanipulasi hak akses, atau menghapus jejak serangan.

---

### Task 3: Broken Access Control (A01) – Kegagalan Authorisation

Kategori ini menempati peringkat pertama karena dampaknya yang masif. Celah ini terjadi ketika aplikasi tidak melakukan pengecekan hak akses di sisi server (*server-side checks*).

* **Bentuk Celah Populer:** **IDOR (Insecure Direct Object References)**.
* **Konsep Simulasi pada Lab:**
* Anda masuk sebagai user biasa (misal: `user_id = 102`).
* Di halaman profil, Anda melihat URL atau parameter API seperti: `https://target-app.com/api/v1/profile?id=102`.
* **Eksploitasi:** Anda secara manual mengubah parameter `id=102` menjadi `id=101` atau `id=1` (yang biasanya milik Admin). Karena server tidak memverifikasi apakah `user_id 102` berhak melihat data `id 1`, server langsung mengembalikan data sensitif milik Admin.


* **Mitigasi:** Menerapkan kontrol akses yang ketat di setiap request sisi server (jangan percaya input/parameter dari *client*).

---

### Task 4: Authentication Failures (A07) – Kegagalan Authentication & Identity

Task ini membahas kegagalan sistem dalam memvalidasi identitas pengguna dengan benar.

* **Bentuk Celah Populer:** *Username Enumeration*, password yang lemah karena tidak ada *rate limiting* (pembatasan login gagar), dan *logic flaws* pada fitur reset password.
* **Konsep Simulasi pada Lab:**
* **Tahap 1 (Enumeration):** Mengetahui apakah username tersedia. Saat mencoba login dengan user acak, aplikasinya merespons *"User tidak ditemukan"*. Namun saat mengetik `admin`, responsnya berubah menjadi *"Password salah"*. Dari sini, penyerang tahu bahwa user `admin` itu ada.
* **Tahap 2 (Brute Force):** Karena aplikasi tidak memiliki *rate limit* atau sistem *account lockout*, Anda bisa melakukan *brute force* (mencoba ribuan password) ke akun `admin` tersebut menggunakan *wordlist* sampai berhasil masuk.


* **Mitigasi:** Gunakan pesan error yang generik (misal: *"Username atau password salah"*), terapkan *rate limiting*, dan paksa kebijakan password yang kuat.

---

### Task 5: Logging & Alerting Failures (A09) – Kegagalan Accountability

Jika sistem berhasil diserang tetapi tidak ada catatan (log) yang terekam, maka tim *defense* (seperti SOC Analyst) akan buta terhadap insiden tersebut.

* **Bentuk Celah Populer:** Aplikasi tidak mencatat aktivitas krusial (seperti kegagalan login berturut-turut atau perubahan *role* menjadi admin), atau log disimpan di tempat lokal yang mudah dimanipulasi penyerang.
* **Konsep Simulasi pada Lab:**
* Anda akan berperan melihat dasbor log aplikasi (atau lingkungan lab SIEM sederhana) setelah serangan terjadi.
* **Analisis:** Anda diminta memeriksa log untuk mencari anomali, seperti lonjakan *status code 401 (Unauthorized)* yang mengindikasikan adanya serangan brute force, atau aktivitas mencurigakan dari IP asing yang melakukan eskalasi hak akses.
* Jika log tidak terpusat (*centralised off-host*) atau formatnya tidak jelas, Anda akan merasakan sulitnya melakukan investigasi forensik.


* **Mitigasi:** Catat semua siklus autentikasi (sukses/gagal, perubahan role), amankan penyimpanan log agar *read-only* bagi penyerang, dan buat *alerting* otomatis jika ada aktivitas mencurigakan.

---

## Alur Singkat Eksekusi di Lab (Cheat Sheet Alur)

Jika Anda sedang menyalakan *AttackBox* atau VPN dan membuka target IP di room ini, alur belajarnya didesain seperti ini:

1. **Akses Aplikasi:** Buka IP web lab yang diberikan.
2. **Uji Celah Auth (A07):** Lakukan enumerasi username, temukan user yang valid, lalu temukan celah *logic* atau *weak password* untuk masuk ke sistem.
3. **Uji Celah Akses (A01):** Setelah masuk dengan akun yang didapat, manipulasi URL parameter atau parameter request untuk membaca data user lain (IDOR) atau naik tingkat menjadi admin.
4. **Investigasi Log (A09):** Periksa dasbor monitoring untuk melihat bagaimana jejak serangan Anda terekam (atau tidak terekam) di sistem.

---

# apa itu IAAA?

Sebagai seorang profesional di bidang cybersecurity, saya melihat room ini sebagai fundamental wajib. Teks tersebut menjelaskan sebuah lab praktis yang berfokus pada runtuhnya **Trust Boundary (Batas Kepercayaan)** pada sebuah aplikasi web.

Dalam arsitektur keamanan, **IAAA** adalah rantai pasok keamanan dari hulu ke hilir. Jika satu mata rantai putus, seluruh sistem dipastikan kompromi. Room ini memetakan kegagalan IAAA tersebut ke dalam 3 risiko terbesar versi OWASP Top 10 terbaru:

### 1. A01: Broken Access Control (Kegagalan Authorisation)

Ini adalah celah paling kritikal saat ini. Bayangkan sebuah aplikasi berhasil mengidentifikasi dan mengautentikasi pengguna dengan benar (Anda adalah User A), tetapi sistem **gagal melakukan otorisasi**. Akibatnya, User A bisa melihat data User B atau bahkan mengeksekusi fungsi milik Administrator hanya dengan memanipulasi parameter seperti URL atau ID di request API (sering disebut IDOR atau BOLA). Dari sudut pandang *attacker*, ini adalah jalan tol untuk *data exfiltration*.

### 2. A07: Authentication Failures (Kegagalan Identity & Authentication)

Di sini, gerbang depannya yang bermasalah. Aplikasi web gagal memvalidasi apakah entitas yang mencoba masuk benar-benar pemilik akun tersebut. Masalah klasiknya adalah tidak adanya *rate limiting*, mekanisme reset password yang cacat secara logika, atau membiarkan *username enumeration*. Efeknya, *attacker* bisa dengan mudah melancarkan serangan *brute force* atau *credential stuffing* secara masif tanpa hambatan.

### 3. A09: Logging & Alerting Failures (Kegagalan Accountability)

Ini adalah mimpi buruk bagi tim Incident Response dan SOC (Security Operations Center). Celah ini terjadi bukan pada fungsionalitas web, melainkan pada aspek visibilitas. Ketika *attacker* membobol A07 dan mengacak-acak A01, aplikasi sama sekali tidak mencatat aktivitas tersebut ke dalam log, atau log-nya tidak memicu alarm (*alert*). Akibatnya, terjadi *zero visibility*—serangan berlangsung berbulan-bulan tanpa pernah terdeteksi sampai akhirnya data perusahaan bocor di forum gelap.

---

### Mengapa Room ini Dirancang untuk "Beginner"?

Sebagai senior, saya sering melihat pemula terjebak langsung belajar *exploit tools* canggih tanpa paham konsep dasar. Room ini membalik cara pandang itu. Anda akan dibawa untuk memahami bagaimana sebuah kode yang buruk (bad code) di sisi *back-end* berimplikasi langsung pada lahirnya celah keamanan. Memahami IAAA secara praktis sejak awal akan membentuk *mindset* yang benar, baik sebagai *pentester* (Blue Team) maupun *developer* (Secure Coding).

---

# kerentanan paling mematikan di dunia web security

Teks tersebut membahas salah satu kerentanan paling mematikan di dunia web security: **Broken Access Control**, yang dimanifestasikan dalam bentuk **IDOR (Insecure Direct Object Reference)**.

Sebagai *cybersecurity specialist*, berikut adalah breakdown teknis mengenai apa yang terjadi di balik layar dari teks tersebut:

### 1. Masalah Utama: Eksploitasi IDOR

Kalimat pertama menyoroti akar masalahnya: **Server terlalu percaya pada input dari client (user)** dan tidak melakukan validasi ulang di setiap *request*.

Ketika aplikasi menggunakan pengenal mentah (seperti angka berurutan `?id=7`) untuk merepresentasikan data pengguna, *attacker* hanya perlu melakukan teknik bernama **Parameter Tampering** (mengubah nilai parameter).

Jika Anda mengubah `id=7` menjadi `id=6` dan server langsung menyajikan data milik user 6 tanpa memeriksa apakah Anda *berhak* melihatnya, maka sistem kontrol akses aplikasi tersebut dinyatakan hancur (*broken*).

### 2. Dampak Serangan: Horizontal vs Vertical Escalation

Teks tersebut membagi dampak eksploitasi ini menjadi dua skenario:

* **Horizontal Privilege Escalation:** Anda berada di level hak akses yang sama (sama-sama user biasa), tetapi Anda bisa mengintip atau memodifikasi data milik user lain. Contoh: Mengubah ID di URL untuk melihat isi rekening orang lain.
* **Vertical Privilege Escalation:** Anda naik kasta dari user biasa menjadi administrator. Contoh: Mengubah parameter atau URL menuju fungsi sensitif seperti `/admin/delete-user` yang seharusnya terisolasi di sisi server.

### 3. Instruksi Lab Praktis (Misi Anda)

Bagian tengah teks adalah instruksi taktis untuk menyelesaikan tantangan di TryHackMe:

1. **Nyalakan Target:** Klik tombol untuk memulai *static site* (aplikasi web simulasi) yang menempel pada task tersebut.
2. **Manipulasi Parameter:** Amati URL pada web tersebut, cari parameter bernama `accountID`.
3. **Temukan Target:** Lakukan *fuzzing* manual (mengubah angka `accountID` satu per satu, misalnya dari 1, 2, 3, dst.) untuk memeriksa saldo akun dari masing-masing ID tersebut.
4. **Goal:** Temukan ID milik pengguna yang memiliki saldo di atas **$1.000.000**. Di akun itulah bendera (*flag*) atau jawaban untuk menyelesaikan task ini berada.

### 4. Rekomendasi Lanjutan

Di akhir paragraf, penulis room mengingatkan bahwa di dunia nyata, IDOR tidak selalu sejelas `?id=7`. Developer sering kali menyembunyikan ID menggunakan *encoding* (seperti Base64) atau *hashing* (MD5/SHA256).

Oleh karena itu, Anda disarankan untuk menyelesaikan dua room spesifik setelah ini: **Broken Access Control** dan **Insecure Direct Object References**, untuk mempelajari variasi IDOR yang lebih kompleks yang biasa ditemukan saat melakukan *penetration testing* sesungguhnya.

---

## Authentication Failures

Teks ini membahas tentang **Authentication Failures**, yaitu kegagalan aplikasi dalam memvalidasi dan mengikat (*binding*) identitas pengguna dengan benar. Di sini Anda diajak memahami bagaimana celah pada proses login dan registrasi bisa dimanfaatkan untuk membobol akun.

Berikut adalah *breakdown* teknis dari sudut pandang *security engineer*:

### 1. Akar Masalah: Celah Sisi Autentikasi

Teks tersebut menyebutkan 4 kelemahan klasik yang sering dieksploitasi:

* **Username Enumeration:** Aplikasi memberikan respons berbeda untuk *user* yang terdaftar dan yang tidak (misal: "User tidak ditemukan" vs "Password salah"). Ini membocorkan informasi *username* valid ke penyerang.
* **Weak Passwords & No Rate Limits:** Aplikasi membiarkan pengguna memakai password lemah (seperti `password123`) tanpa ada pembatasan jumlah percobaan login (*rate limiting*) atau pemblokiran akun otomatis (*account lockout*). Ini adalah lampu hijau untuk serangan *brute force*.
* **Logic Flaws:** Cacat logika pada alur registrasi atau reset password yang bisa dilewati dengan trik tertentu.
* **Insecure Session/Cookie Handling:** Kegagalan mengamankan token sesi (seperti JWT atau Cookie), sehingga penyerang bisa mencuri atau memanipulasi *session* orang lain.

---

### 2. Trik Eksploitasi pada Lab: Case Sensitivity Flaw (Cacat Logika Registrasi)

Bagian tengah teks memberikan instruksi langsung untuk menyelesaikan tantangan di lab. Menariknya, teknik yang digunakan di sini adalah **Authentication Bypass melalui Logic Flaw saat registrasi**, memanfaatkan bagaimana database atau aplikasi menangani huruf besar/kecil (*case sensitivity*).

* **Skenario:** Anda tahu ada akun target dengan username `admin`.
* **Triknya:** Anda diminta mendaftarkan akun baru dengan nama `aDmiN` (mengubah variasi huruf besar-kecil).
* **Mengapa ini bisa merusak sistem?**
Pada aplikasi yang cacat logikanya, saat registrasi, aplikasi mengecek secara *case-sensitive* ("admin" tidak sama dengan "aDmiN"), sehingga pendaftaran Anda **diterima**. Namun, saat data disimpan ke database atau saat proses login, sistem melakukan query secara *case-insensitive* (menganggap "admin" dan "aDmiN" adalah entitas yang sama).
Akibatnya, password baru yang Anda buat untuk `aDmiN` justru menimpa (*overwrite*) atau mengizinkan Anda masuk ke sesi milik `admin` asli.

---

### 3. Langkah Taktis Eksekusi di Lab

1. **Jalankan Target:** Klik tombol untuk memulai *static site* pada task tersebut.
2. **Registrasi Akun Baru:** Pergi ke halaman *Register*, lalu daftar menggunakan username `aDmiN` dan buat password acak yang Anda tentukan sendiri.
3. **Login:** Gunakan akun `aDmiN` tersebut untuk login.
4. **Ambil Flag:** Jika berhasil masuk, aplikasi akan mengarahkan Anda ke dasbor milik `admin` asli, dan Anda akan mendapatkan *flag* (kode jawaban) di sana.

---

### 4. Rekomendasi Modul Lanjutan

Penulis mengingatkan bahwa ini hanyalah satu variasi kecil dari kegagalan autentikasi. Untuk menguasai teknik yang lebih kompleks seperti manipulasi JSON Web Tokens (JWT), *OAuth bypass*, serangan *brute force* yang matang, hingga membobol Multi-Factor Authentication (MFA), Anda disarankan menyelesaikan tiga room lanjutan: **Authentication Bypass**, **Multi-Factor Authentication**, dan **Authentication Module**.

---

# Logging & Alerting Failures (Pencatatan)

Teks ini membahas tentang **Logging & Alerting Failures**, yaitu kebutaan sistem akibat tidak adanya catatan aktivitas keamanan yang memadai. Dari sudut pandang **Blue Team** atau **SOC (Security Operations Center) Analyst**, celah ini adalah salah satu kendala terbesar dalam mendeteksi dan merespons insiden siber.

Berikut adalah pembedahan teknis mengenai apa yang dimaksud oleh teks tersebut:

### 1. Fondasi Utama: Akuntabilitas (Accountability)

Kalimat pertama menegaskan bahwa fungsi utama dari *logging* (pencatatan) yang baik adalah untuk mendukung **Akuntabilitas**. Artinya, ketika insiden terjadi, tim kemaanan harus bisa membuktikan secara forensik:

* **Who:** Siapa aktor di balik serangan tersebut? (User ID, Username).
* **What:** Apa saja yang mereka lakukan atau modifikasi? (Eksekusi perintah, unduh data).
* **When:** Kapan serangan itu terjadi? (Timestamp yang akurat).
* **Where:** Dari mana asal serangan tersebut? (IP Address, User-Agent).

Tanpa ini, sistem tidak memiliki visibilitas, dan *attacker* bisa menyusup tanpa terdeteksi.

---

### 2. Bentuk-Bentuk Kegagalan di Lapangan

Teks tersebut merinci beberapa kesalahan fatal yang sering dilakukan oleh pengembang atau administrator sistem:

* **Missing Authentication Events:** Tidak mencatat kapan seseorang berhasil login, atau yang lebih parah, gagal login.
* **Vague Error Logs:** Log yang terlalu abstrak (misal hanya mencatat `Error 500`) tanpa menyertakan detail *stack trace* atau *payload* yang memicu error tersebut.
* **No Alerting:** Log mencatat adanya serangan *brute-force* (ribuan kali gagal login dalam 1 menit), tetapi sistem tidak memiliki mekanisme alarm (*alerting*) untuk menembak notifikasi ke tim keamanan.
* **Short Retention:** Masa penyimpanan log yang terlalu singkat (misal hanya disimpan selama 3 hari). Padahal, rata-rata serangan baru terdeteksi setelah berminggu-minggu atau berbulan-bulan.
* **Tamper-able Logs:** Log disimpan secara lokal di server yang sama dengan aplikasi. Jika server tersebut berhasil di-*compromise*, *attacker* tinggal menghapus file log (`rm -rf /var/log/*`) untuk menghilangkan jejak mereka.

---

### 3. Panduan Lab Praktis (Misi Investigasi Anda)

Pada bagian ini, Anda diminta bertindak sebagai seorang **Digital Forensics / Incident Responder**:

1. **Mulai Simulasi:** Klik tombol untuk menyalakan *static site* yang berisi dasbor log atau catatan aktivitas dari sebuah aplikasi yang baru saja diserang.
2. **Lakukan Analisis:** Anda harus membaca baris demi baris log tersebut untuk merekonstruksi kronologi serangan. Cari pola anomali seperti:
* Alamat IP asing yang melakukan request tidak wajar.
* Rentetan kode status HTTP `401 Unauthorized` atau `403 Forbidden` yang menandakan percobaan paksa masuk.
* Upaya pengubahan hak akses secara tiba-tiba.


3. **Jawab Pertanyaan:** Gunakan temuan dari analisis log tersebut untuk menjawab pertanyaan-pertanyaan yang ada di bawah task TryHackMe.

### 4. Introspeksi Defensif

Di akhir instruksi, Anda diajak merenungkan sebuah pertanyaan krusial: *Seberapa sulit investigasi ini jika beberapa bagian penting dari log tersebut sengaja dihapus atau memang tidak pernah dicatat oleh sistem?*

Ini adalah latihan mental untuk menyadari bahwa secanggih apa pun *tools* pertahanan yang dimiliki, tim keamanan akan lumpuh tanpa adanya data log yang utuh, terpusat (*centralized off-host logging*), dan dilindungi dari manipulasi.

---
