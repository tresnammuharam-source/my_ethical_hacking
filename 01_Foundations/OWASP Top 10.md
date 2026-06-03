# OWASP Top 10

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

