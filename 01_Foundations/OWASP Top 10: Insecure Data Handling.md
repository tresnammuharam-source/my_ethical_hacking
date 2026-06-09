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

### 3. Alur Praktis & Instruksi Lab (Deploy Practical)

Sama seperti room sebelumnya, Anda tidak hanya belajar teori tetapi akan melakukan simulasi serangan (*practice exploiting*).

* **Persiapan:** Anda wajib menekan tombol hijau **"Start Lab Machine"** untuk menyalakan komputer target di server TryHackMe.
* **Akses:** Anda harus menggunakan **AttackBox** (kali linux berbasis browser milik THM) atau **mesin hacking sendiri** (seperti Kali Linux di VirtualBox) yang sudah tersambung ke jaringan internal menggunakan **OpenVPN TryHackMe**. Tanpa ini, Anda tidak akan bisa mengakses alamat IP laboratorium praktisnya nanti.
