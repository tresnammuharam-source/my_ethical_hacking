# **Operating System Security** 
di room ini kamu belajar **bagaimana OS diamankan dan bagaimana cara mengaksesnya dengan aman menggunakan SSH**.

---

# 1️⃣ Apa Maksud “Operating System Security”?

**Operating System Security** adalah cara melindungi sistem operasi agar:

* Tidak diakses oleh orang yang tidak berhak
* Tidak dimanipulasi oleh attacker
* Tidak dicuri datanya
* Tidak dijadikan pintu masuk ke jaringan

Karena **OS adalah pusat kontrol komputer**.

Jika hacker berhasil menguasai OS →
mereka bisa:

* membaca semua file
* menjalankan malware
* mencuri password
* menggunakan komputer sebagai botnet

---

# 2️⃣ Pilar Keamanan Sistem Operasi

Dalam keamanan sistem operasi biasanya ada beberapa kontrol utama:

### 🔐 1. Authentication (Autentikasi)

Membuktikan **siapa kamu**.

Contoh:

* username + password
* SSH key
* biometrik

---

### 👮 2. Authorization (Otorisasi)

Menentukan **apa yang boleh kamu lakukan**.

Contoh:

| User       | Akses           |
| ---------- | --------------- |
| user biasa | baca file       |
| admin      | install program |
| root       | kontrol penuh   |

---

### 🧾 3. Accounting / Auditing

Mencatat aktivitas pengguna.

Contoh log:

```
user tresna login via SSH
user root menjalankan sudo
```

Ini penting untuk **incident investigation**.

---

# 3️⃣ User Accounts di Linux

Linux memiliki beberapa jenis user:

### 👤 Normal User

Digunakan untuk aktivitas sehari-hari.

Contoh:

```
tresna
student
```

---

### 👑 Root User

Superuser dengan **akses penuh**.

Root bisa:

* membaca semua file
* mematikan sistem
* mengubah konfigurasi

Contoh login:

```
root@server
```

---

### ⚙️ System Users

Digunakan oleh service.

Contoh:

```
www-data
mysql
daemon
```

---

# 4️⃣ Konsep Permission Linux

Setiap file memiliki permission seperti:

```
-rwxr-xr--
```

Artinya:

| Symbol | Meaning |
| ------ | ------- |
| r      | read    |
| w      | write   |
| x      | execute |

Permission dibagi menjadi:

```
Owner
Group
Others
```

Contoh:

```
chmod 755 file.sh
```

Ini sangat penting karena **kesalahan permission bisa jadi celah security**.

---

# 5️⃣ Apa Itu SSH?

SSH adalah singkatan dari:

**Secure Shell**

Ini adalah protokol yang memungkinkan kita **mengakses komputer lain secara remote dengan aman**.

Biasanya digunakan untuk:

* login ke server
* mengelola cloud server
* remote administration
* pentesting

---

# 6️⃣ Kenapa SSH Penting di Cybersecurity?

Karena hampir semua server Linux di dunia diakses menggunakan SSH.

Contoh server:

* cloud server
* web server
* database server

Semua dikelola lewat SSH.

Contoh koneksi:

```
ssh user@192.168.1.10
```

---

# 7️⃣ Bagaimana SSH Bekerja?

Saat kamu menjalankan:

```
ssh user@server
```

Terjadi proses berikut:

### 1. Client menghubungi server

Komputer kamu → server target.

---

### 2. Enkripsi dibuat

SSH membuat koneksi yang **terenkripsi**.

Ini melindungi dari:

* packet sniffing
* man-in-the-middle attack

---

### 3. Authentication

Server meminta bukti identitas:

* password
  atau
* SSH key

---

### 4. Shell diberikan

Jika berhasil login:

kamu mendapatkan **remote terminal**.

Contoh:

```
user@server:~$
```

---

# 8️⃣ SSH Authentication Methods

Ada dua metode utama.

---

## 1. Password Authentication

Login menggunakan password.

Contoh:

```
ssh tresna@192.168.1.20
```

Lalu masukkan password.

---

### Kekurangan

Rentan terhadap:

* brute force attack
* password guessing

---

## 2. SSH Key Authentication

Metode yang lebih aman.

Menggunakan **cryptographic key pair**.

Terdiri dari:

* Private key
* Public key

---

### Cara Kerja

1️⃣ Kamu membuat key pair

```
ssh-keygen
```

2️⃣ Public key disimpan di server

```
~/.ssh/authorized_keys
```

3️⃣ Saat login

server memverifikasi private key.

---

### Keuntungan

* jauh lebih aman
* tidak perlu password
* sulit dibobol brute force

---

# 9️⃣ Struktur Folder SSH

Biasanya berada di:

```
~/.ssh
```

Contoh isi:

```
id_rsa
id_rsa.pub
authorized_keys
known_hosts
```

Penjelasan:

| File            | Fungsi                              |
| --------------- | ----------------------------------- |
| id_rsa          | private key                         |
| id_rsa.pub      | public key                          |
| authorized_keys | daftar key yang boleh login         |
| known_hosts     | daftar server yang pernah dihubungi |

---

# 🔟 Kenapa Penting untuk Ethical Hacking?

Dalam pentesting, SSH sering digunakan untuk:

### 🔍 Enumeration

Melihat konfigurasi SSH.

---

### 🔓 Brute Force

Contoh tool:

* Hydra
* Medusa

---

### 🔑 Credential Reuse

Jika password bocor → login via SSH.

---

### 🐚 Reverse Shell

Attacker bisa mendapatkan **remote shell**.

---

# 1️⃣1️⃣ Risiko Keamanan SSH

Beberapa kesalahan konfigurasi:

### ❌ Root login diaktifkan

```
PermitRootLogin yes
```

Ini sangat berbahaya.

---

### ❌ Password authentication aktif

```
PasswordAuthentication yes
```

Rentan brute force.

---

### ❌ Port default 22

Sering diserang bot.

---

# 1️⃣2️⃣ Best Practice Security

Administrator biasanya melakukan:

* Disable root login
* Gunakan SSH key
* Ganti port SSH
* Batasi IP login
* Gunakan firewall

---

# 🎯 Kesimpulan Materi Room Ini

Room **Operating System Security** ingin kamu memahami:

1️⃣ OS harus dilindungi dari akses ilegal
2️⃣ Linux menggunakan sistem **user dan permission**
3️⃣ Remote access biasanya menggunakan **SSH**
4️⃣ SSH menggunakan **encryption dan authentication**
5️⃣ SSH key lebih aman daripada password

Ini adalah **dasar keamanan server Linux**.

---

# **CIA Triad**

CIA adalah tiga prinsip utama yang digunakan untuk menjaga keamanan sistem dan data.

---

# 🔐 CIA Triad

CIA terdiri dari:

| Huruf | Arti            | Tujuan                        |
| ----- | --------------- | ----------------------------- |
| C     | Confidentiality | Menjaga kerahasiaan data      |
| I     | Integrity       | Menjaga keutuhan data         |
| A     | Availability    | Menjamin data selalu tersedia |

---

# 1️⃣ Confidentiality (Kerahasiaan)

Artinya **data hanya boleh diakses oleh orang yang berhak**.

### Contoh

* password
* data bank
* data pasien rumah sakit
* database perusahaan

Jika hacker bisa membaca data tersebut → **Confidentiality gagal**.

---

### Cara Melindungi Confidentiality

Beberapa cara yang digunakan:

* **Encryption**
* **Authentication**
* **Access Control**
* **VPN**
* **SSH**

Contoh:

```bash
ssh user@server
```

SSH mengenkripsi koneksi agar data tidak bisa disadap.

---

# 2️⃣ Integrity (Keutuhan Data)

Integrity berarti **data tidak boleh diubah secara ilegal atau tanpa izin**.

Contoh:

Database bank:

```text
Saldo awal: 1.000.000
```

Jika hacker mengubah menjadi:

```text
Saldo: 100.000.000
```

Maka **integrity rusak**.

---

### Cara Melindungi Integrity

Teknik yang digunakan:

* Hashing
* Digital signature
* File permission
* Version control
* Checksums

Contoh hashing:

```bash
sha256sum file.txt
```

Jika file berubah → hash berubah.

---

# 3️⃣ Availability (Ketersediaan)

Availability berarti **sistem dan data harus tetap bisa diakses saat dibutuhkan**.

Contoh:

* website bank
* server perusahaan
* aplikasi pembayaran

Jika server tidak bisa diakses → availability gagal.

---

### Ancaman terhadap Availability

Serangan yang sering terjadi:

* **DDoS attack**
* server crash
* hardware failure
* ransomware

---

### Cara Melindungi Availability

Biasanya menggunakan:

* Backup
* Redundancy
* Load balancing
* Cloud scaling
* Monitoring

Contoh di cloud:

Server otomatis bertambah saat traffic naik.

---

# 🧠 Analogi Sederhana

Bayangkan **brankas bank**.

### Confidentiality

Hanya orang tertentu yang tahu **kode brankas**.

### Integrity

Isi uang di dalam **tidak boleh diubah atau dicuri**.

### Availability

Brankas harus **bisa dibuka saat bank membutuhkannya**.

---

# 🎯 Hubungan CIA dengan Cyber Attack

| Jenis Serangan    | CIA yang Diserang |
| ----------------- | ----------------- |
| Data breach       | Confidentiality   |
| Data manipulation | Integrity         |
| DDoS attack       | Availability      |

---

# 🧩 Kenapa CIA Penting?

Semua sistem keamanan dirancang untuk menjaga **tiga hal ini**.

Contoh:

| Teknologi     | Melindungi      |
| ------------- | --------------- |
| Firewall      | Confidentiality |
| Hash          | Integrity       |
| Load Balancer | Availability    |

---

# 📌 Ringkasan

CIA Triad adalah **fondasi keamanan informasi**:

```
Confidentiality → Data harus rahasia
Integrity → Data tidak boleh diubah
Availability → Sistem harus selalu tersedia
```

Semua konsep cybersecurity akan selalu kembali ke **CIA Triad**.

---


