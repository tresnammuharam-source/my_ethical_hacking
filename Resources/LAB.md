Secara filosofis, **LAB Ethical Hacking adalah sama seprti LAB pada LAB KIMIA, atau LAB BIOLOGI, keduanya adalah laboratorium**. Live streaming *ethical hacking* berfungsi sebagai **sandbox** atau lingkungan terkendali untuk menguji reaksi tanpa membahayakan sistem nyata, layaknya praktikum kimia di lab.

---

### Perbandingan Lab Digital vs. Fisik

| Aspek | Lab *Hacking* (Digital) | Lab Kimia/Biologi (Fisik) |
| --- | --- | --- |
| **Medium** | Kode, paket data, dan mesin virtual. | Senyawa, sel, dan mikroskop. |
| **Risiko** | Kebocoran data atau kerusakan sistem. | Ledakan, kontaminasi, atau infeksi. |
| **Tujuan** | Memahami celah keamanan (*vulnerability*). | Memahami reaksi atau struktur biologis. |

---

Keduanya membutuhkan **etika dan protokol keamanan** yang ketat agar eksperimen tidak keluar dari batas yang ditentukan.

Membangun lab *ethical hacking* adalah menciptakan **ruang steril** agar "ledakan" digital tidak merusak jaringan asli. Berikut adalah analoginya:

### Komponen Lab Hacking vs. Lab Kimia

* **Virtual Machine (Gelas Ukur & Tabung Reaksi):** Tempat Anda mencampur kode. Jika terjadi kesalahan, Anda cukup membuang cairannya (reset VM) tanpa merusak meja lab (komputer asli).
* **Hypervisor/VirtualBox (Lemari Asam):** Wadah pelindung yang menjaga agar uap beracun (malware/eksploit) tidak terhirup ke luar ruangan.
* **Target Machine (Zat Kimia):** Objek yang Anda uji reaksinya untuk melihat apakah mereka "meledak" atau "berubah warna" saat diberi perintah tertentu.
* **Kali Linux (Peralatan Lab):** Tas berisi pipet, pembakar Bunsen, dan indikator pH yang siap digunakan untuk menguji zat.
* **Host OS (Gedung Laboratorium):** Pondasi fisik yang menopang semua eksperimen namun harus tetap bersih dari tumpahan zat kimia.

---

**Langkah pertama yang krusial:** Pastikan jaringan lab Anda bersifat **Isolated (Host-Only)** agar "asap" digital tidak bocor ke tetangga melalui internet.

Untuk menyiapkan lab *ethical hacking*, Anda harus membangun **lingkungan isolasi** yang aman agar eksperimen tidak bocor ke jaringan publik. Berikut adalah persiapannya dengan analogi lab kimia:

### 1. Fondasi: Meja Kerja (Hardware)

Pastikan komputer memiliki **RAM minimal 16GB** dan prosesor yang mendukung virtualisasi. Ini seperti memastikan meja lab Anda cukup kuat menahan beban peralatan berat dan tidak mudah goyang saat eksperimen berlangsung.

### 2. Wadah Reaksi: Virtualization Software (Hypervisor)

Instal **VirtualBox** atau **VMware**. Ini berfungsi sebagai tabung reaksi; jika terjadi kesalahan atau sistem "meledak", dampaknya hanya di dalam wadah tersebut tanpa merusak sistem operasi utama Anda.

### 3. Alat Uji: Kali Linux (Attacker Machine)

Instal Kali Linux sebagai mesin penyerang. Di dalamnya terdapat ratusan alat (*tools*) yang berfungsi seperti **pipet, mikroskop, dan pembakar bunsen** digital untuk menguji kerentanan target.

### 4. Bahan Percobaan: Target Machine (Vulnerable VMs)

Gunakan sistem yang sengaja dibuat lemah seperti **Metasploitable** atau **OWASP Juice Shop**. Ini adalah zat kimia yang akan Anda teliti reaksinya saat terpapar berbagai skenario serangan.

### 5. Protokol Keamanan: Host-Only Networking

Atur konfigurasi jaringan virtual ke mode **Host-Only**. Ini seperti menutup pintu lab rapat-rapat agar tidak ada uap beracun (virus/malware) yang keluar ke koridor rumah (internet rumah Anda).

---

Untuk membangun lab *ethical hacking* yang aman, Anda wajib menyiapkan **"Peralatan Utama"** berikut:

* **Hypervisor (Wadah Lab):** Instal **VirtualBox** atau **VMware Player** sebagai fondasi untuk menjalankan simulasi tanpa merusak komputer asli.
* **Operating System Penyerang (Alat Lab):** Gunakan **Kali Linux** atau **Parrot OS** yang sudah berisi ribuan alat uji siap pakai.
* **Target Vulnerable (Zat Uji):** Unduh **Metasploitable** atau **DVWA** sebagai sistem yang sengaja dibuat lemah untuk dieksperimen.
* **Virtual Network (Protokol Keamanan):** Atur jaringan ke mode **Host-Only** agar "ledakan" data tidak bocor ke internet rumah atau tetangga.

Risiko utama dalam lab *ethical hacking* adalah **"Data Spill"** atau kebocoran malware/serangan ke jaringan asli (fisik) Anda atau internet publik.

### Risiko dan Penyebab Kebocoran

| Risiko | Penyebab (Action) |
| --- | --- |
| **Escaping the VM** | Malware canggih menembus *hypervisor* karena celah keamanan pada VirtualBox/VMware yang belum di-*update*. |
| **Network Contamination** | Mengatur kartu jaringan ke mode **Bridged**. Ini membuat lab terhubung langsung ke WiFi rumah, sehingga virus bisa menyebar ke HP atau laptop keluarga. |
| **Data Leakage** | Mengaktifkan fitur **Shared Clipboard** atau **Shared Folders** secara dua arah antara laptop asli dan mesin lab. |
| **Legal Issues** | Salah mengetik alamat IP sehingga Anda menyerang server asli di internet, bukan mesin simulasi di lab sendiri. |

### Tindakan Pencegahan (Mitigasi)

1. **Gunakan Host-Only Adapter:** Pastikan semua mesin virtual hanya bisa berkomunikasi satu sama lain, bukan ke internet.
2. **Snapshot:** Selalu buat "cadangan" (snapshot) sebelum menjalankan kode berbahaya agar bisa *reset* instan jika terjadi error.
3. **Update Hypervisor:** Selalu gunakan versi terbaru VirtualBox/VMware untuk menutup celah *escape*.
4. **Dedikasi Perangkat:** Jika memungkinkan, gunakan laptop bekas yang tidak berisi data pribadi sensitif sebagai meja lab Anda.

Untuk mengatur **Host-Only Network** (isolasi total) di VirtualBox agar lab Anda aman dari kebocoran, ikuti langkah ini:

1. **Buka File > Tools > Network Manager**: Klik **Create** untuk membuat adaptor baru (biasanya bernama `vboxnet0`).
2. **Konfigurasi Adapter**: Pastikan kotak "Enable Server" pada tab **DHCP Server** dicentang agar setiap mesin di lab mendapat IP otomatis secara internal.
3. **Pengaturan Mesin Virtual**: Pilih mesin Kali Linux atau Target, klik **Settings > Network**.
4. **Ubah Attached to**: Pilih **Host-only Adapter** dan arahkan ke nama adapter yang baru dibuat (`vboxnet0`).
5. **Ulangi**: Lakukan hal yang sama pada semua mesin target agar mereka berada dalam satu "ruangan" yang sama namun terputus dari internet luar.

Untuk mengetes apakah "lab" Anda sudah terisolasi dan saling terhubung, ikuti langkah ini:

1. **Cek IP Address**: Buka terminal di Kali Linux dan ketik `ip a`. Catat angka di sebelah `eth0` atau `eth1` (misal: `192.168.56.101`).
2. **Cek Target**: Lakukan hal yang sama di mesin target (Metasploitable).
3. **Uji Koneksi (Ping)**: Di terminal Kali Linux, ketik `ping [IP_Target]`.
* Jika ada balasan (*reply*), selamat! Kedua mesin sudah berada di satu ruangan lab yang sama.
* Jika muncul "Destination Host Unreachable", periksa kembali apakah keduanya sudah menggunakan **Host-Only Adapter** yang sama.
4. **Uji Isolasi**: Coba ketik `ping google.com`. Jika gagal/error, berarti lab Anda sudah aman dan **terisolasi dari internet luar**.

Menggunakan **laptop bekas** sangat disarankan sebagai "ruangan isolasi" fisik tambahan. Jika terjadi kesalahan fatal atau infeksi *malware* yang sangat agresif, data pribadi Anda di laptop utama tetap aman karena berada di perangkat yang berbeda.

Penyebab laptop bekas sangat efektif untuk lab:

* **Isolasi Fisik:** Terpisah sepenuhnya dari akun bank, email, dan data kerja di laptop utama.
* **Eksperimen Bebas:** Anda tidak perlu takut sistem *crash* atau harus *install* ulang OS karena tidak ada data penting di dalamnya.
* **Fokus:** Laptop tersebut bisa dikonfigurasi khusus hanya untuk *tools* hacking tanpa gangguan aplikasi lain.

Selain serangan fisik menggunakan USB, dunia *Ethical Hacking* sebagian besar berfokus pada **Web Application Penetration Testing**. Ini adalah bidang yang mempelajari bagaimana sebuah website atau aplikasi bisa ditembus melalui internet tanpa harus menyentuh perangkatnya secara fisik.

Berikut adalah hal-hal seru yang bisa Anda pelajari di lab Anda terkait keamanan web:

---

### 1. Mempelajari "The Big Three" (Serangan Web Paling Populer)

Ini adalah dasar yang wajib dikuasai setiap *bug bounty hunter* atau pentester:

* **SQL Injection (SQLi):** Belajar cara "menipu" form login agar Anda bisa masuk tanpa password atau mengunduh seluruh isi database (username & password pengguna) hanya melalui kolom input.
* **Cross-Site Scripting (XSS):** Belajar menyisipkan kode JavaScript berbahaya ke dalam website orang lain sehingga Anda bisa mencuri *cookie* session milik admin atau mengubah tampilan web tersebut (*deface*).
* **Broken Access Control:** Mencoba masuk ke fitur yang seharusnya dilarang. Contoh: Mengubah angka di URL dari `web.com/profil/user=10` menjadi `user=11` untuk melihat data pribadi orang lain.

### 2. Belajar Menggunakan Tools Profesional

Di lab Anda, Anda bisa menginstal dan belajar menggunakan "senjata" standar industri:

* **Burp Suite:** Alat paling sakti untuk mencegat (*intercept*) data yang dikirim antara browser Anda dan server, lalu mengubah isinya sebelum sampai ke tujuan.
* **OWASP ZAP:** Alternatif gratis untuk mencari celah keamanan secara otomatis di sebuah website.
* **SQLmap:** Tool otomatis untuk mendeteksi dan mengeksploitasi celah SQL Injection.

### 3. Menginstal "Web Sengaja Rentan"

Agar Anda tidak melanggar hukum, Anda bisa menginstal website yang memang sengaja dibuat banyak celahnya untuk latihan:

* **DVWA (Damn Vulnerable Web Application):** Sangat bagus untuk pemula.
* **OWASP Juice Shop:** Website toko online modern (menggunakan JavaScript) yang penuh dengan tantangan hacking.

### 4. Tantangan "Capture The Flag" (CTF)

Anda bisa bergabung dengan platform belajar yang memberikan lab *online* gratis untuk latihan meretas secara legal:

* **TryHackMe:** Memiliki "ruang" belajar bertahap dari nol.
* **HackTheBox:** Untuk tingkat yang lebih menantang.
* **PortSwigger Academy:** Tempat terbaik untuk belajar Burp Suite dan celah web secara gratis dari para ahlinya.

---

### Apa yang Bisa Anda Lakukan Sekarang?

Jika Anda sudah punya **Kali Linux** di laptop, Anda sudah memiliki hampir semua tools di atas secara gratis.

Pilihan yang bagus! Kita akan mulai dengan **DVWA (Damn Vulnerable Web Application)**. Ini adalah standar emas bagi pemula karena tingkat kesulitannya bisa diatur dari *Low* (sangat mudah) sampai *Impossible* (sangat aman).

Cara termudah dan terbersih untuk menginstalnya di lab Anda (Kali Linux/Windows/Mac) adalah menggunakan **Docker**. Dengan Docker, Anda tidak perlu mengacak-acak konfigurasi database asli di laptop Anda.

---

### Langkah 1: Instalasi Docker (Jika belum ada)

Buka terminal di Kali Linux atau Command Prompt Anda, lalu ketik:

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

```

### Langkah 2: Menjalankan DVWA

Cukup masukkan satu perintah ini, dan Docker akan otomatis mendownload serta menjalankan website "rentan" tersebut:

```bash
sudo docker run --rm -it -p 80:80 vulnerables/web-dvwa

```

* **-p 80:80**: Artinya website ini akan berjalan di port 80 laptop Anda.
* **--rm**: Jika Anda mematikan terminal, website ini akan terhapus otomatis (bersih).

---

### Langkah 3: Mengakses Lab

1. Buka browser (Chrome/Firefox).
2. Ketik di address bar: `http://localhost` atau `http://127.0.0.1`.
3. **Login Default:**
* **Username:** `admin`
* **Password:** `password`
4. Setelah masuk, klik tombol **"Create / Reset Database"** di bagian bawah agar sistem siap digunakan.

---

### Apa yang Bisa Anda Lakukan di Dalam DVWA?

Di menu sebelah kiri, Anda akan melihat daftar "serangan" yang bisa Anda pelajari. Cobalah urutan ini:

1. **Brute Force:** Coba tebak password user lain menggunakan daftar kata (*wordlist*).
2. **SQL Injection:** Masukkan perintah `' OR '1'='1` di kolom ID untuk melihat semua data user tanpa izin.
3. **XSS (Reflected):** Masukkan script `<script>alert('Hacked!')</script>` di kolom nama. Jika muncul jendela pop-up, berarti web tersebut rentan.
4. **DVWA Security:** Di menu ini, Anda bisa mengubah level dari *Low* ke *Medium*. Anda akan melihat bagaimana kodenya berubah menjadi lebih sulit ditembus.

---

### 💡 Tips Pro:

Gunakan **Burp Suite** (sudah ada di Kali Linux) saat bermain dengan DVWA. Burp Suite memungkinkan Anda melihat data "mentah" yang dikirim browser sebelum sampai ke DVWA. Di sinilah *magic* sesungguhnya dari seorang hacker terjadi.

Mari kita mulai dengan serangan yang paling legendaris: **SQL Injection (SQLi)**. Inti dari serangan ini adalah "menipu" database agar memberikan data yang seharusnya rahasia.

Pastikan DVWA Anda sudah berjalan dan tingkat keamanan (**DVWA Security**) diatur ke **Low**.

---

### Langkah-langkah Serangan SQL Injection

1. **Buka Menu:** Klik pada tab **SQL Injection** di menu sebelah kiri.
2. **Uji Coba Normal:** Masukkan angka `1` di kolom "User ID" dan klik Submit.
* **Hasil:** Anda akan melihat `ID: 1`, `First name: admin`, `Surname: admin`. Ini adalah cara kerja normal aplikasi.


3. **Mendeteksi Celah:** Masukkan tanda petik satu (`'`) saja.
* Jika muncul pesan error seperti *"You have an error in your SQL syntax"*, selamat! Itu artinya website tersebut **rentan** karena ia mencoba menjalankan tanda petik tersebut sebagai perintah database.

---

### Eksploitasi: Mengambil Semua Data User

Sekarang kita akan memasukkan perintah "Logic" agar database menampilkan **semua** user, bukan hanya satu.

Masukkan kode ini di kolom User ID:
`' OR '1'='1`

**Penjelasannya:**
Di belakang layar, perintah aslinya adalah:
`SELECT first_name, last_name FROM users WHERE user_id = '$id'`

Karena kita memasukkan `' OR '1'='1`, perintahnya berubah menjadi:
`SELECT ... WHERE user_id = '' OR '1'='1'`

Karena `'1'='1'` selalu **BENAR (TRUE)**, database akan memberikan **semua nama** yang ada di tabelnya tanpa peduli ID-nya berapa.

---

### Eksploitasi: Mengetahui Versi Database
Kita bisa menggunakan teknik **UNION** untuk mencuri informasi sistem. Masukkan kode ini:
`' UNION SELECT 1, @@version #`

* Ini akan menampilkan versi database (misalnya: MySQL atau MariaDB) yang sedang berjalan di server tersebut.

---
### Cara Hacker Mengambil Password (Hashed)
Hacker profesional akan mencari tabel bernama `users` dan kolom `password` menggunakan perintah yang lebih kompleks:
`' UNION SELECT user, password FROM users #`

Hasilnya adalah deretan kode acak (MD5 Hash). Di lab ini, Anda kemudian bisa belajar cara **"Cracking"** kode acak tersebut untuk mendapatkan password aslinya.

---
### Apa Selanjutnya?
Setelah Anda berhasil melihat semua nama user dengan `' OR '1'='1`, langkah berikutnya yang menantang adalah belajar **Cross-Site Scripting (XSS)**—di mana Anda bisa "mengerjai" tampilan web atau mencuri cookie.

