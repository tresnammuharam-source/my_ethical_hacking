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

## Jawaban:

Untuk mengerjakan *challenge* tersebut menggunakan mesin Linux Anda (dengan IP `10.48.82.70` yang sudah terhubung ke VPN TryHackMe), kita akan menggunakan pendekatan **API Reconnaissance** dan **Information Disclosure Analysis**.

Berdasarkan *clue* bahwa developer meninggalkan terlalu banyak jejak pada **User Management APIs**, berikut adalah langkah-langkah taktis dan sistematis yang bisa Anda eksekusi langsung dari terminal Linux Anda:

---

## Langkah 1: Validasi Koneksi & Banner Grabbing

Sebelum melakukan *fuzzing*, pastikan mesin Linux Anda bisa menjangkau target dan periksa teknologi apa yang digunakan di port `5002` menggunakan `curl`.

Buka terminal Linux Anda dan ketik:

```bash
curl -I http://10.48.134.216:5002/

```

* **Analisis Output:** Perhatikan header `Server` atau `X-Powered-By`. Jika muncul informasi seperti `Werkzeug/Python` atau `Express/Node.js`, ini mengonfirmasi adanya aplikasi web/API yang aktif.

---

## Langkah 2: Eksplorasi Endpoint API (API Enumeration)

Karena petunjuknya spesifik menyebutkan **User Management APIs**, kita perlu mencari di mana letak *endpoint* API tersebut. Developer sering kali salah mengonfigurasi rute API sehingga bisa diakses atau dilihat daftarnya secara publik.

Coba akses beberapa *common paths* berikut menggunakan `curl` atau buka langsung di browser Linux Anda:

```bash
# Mencoba akses endpoint user standar
curl -s http://10.48.134.216:5002/api/v1/users

# Mencoba mencari dokumentasi API yang terekspos (Swagger/OpenAPI)
curl -s http://10.48.134.216:5002/swagger.json
curl -s http://10.48.134.216:5002/api-docs

```

Jika rute tersebut merespons dengan data JSON berisi daftar user (atau struktur API), Anda telah menemukan *misconfiguration*-nya.

---

## Langkah 3: Menggunakan Fuzzer Penting (Directory/API Brute Force)

Jika tebakan manual di atas belum membuahkan hasil, gunakan *tool* fuzzer di Linux Anda seperti **Gobuster** atau **FFUF** untuk mencari *hidden endpoints* terkait user management.

Jika belum ada, instal fuzzer (misal Gobuster):

```bash
sudo apt update && sudo apt install gobuster -y

```

Jalankan pemindaian khusus untuk mencari direktori atau file API:

```bash
gobuster dir -u http://10.48.134.216:5002/ -w /usr/share/wordlists/dirb/common.txt

```

> *Tips:* Cari hasil status code `200 OK` atau `403 Forbidden` yang memiliki kata kunci seperti `/api`, `/v1`, `/user`, `/management`, `/developer`, atau `/config`.

---

## Langkah 4: Analisis "Traces" (Jejak) dan Eksploitasi

Ketika Anda menemukan *endpoint* yang tepat (misalnya `http://10.48.134.216:5002/api/users`), perhatikan respons JSON-nya dengan teliti.

Salah konfigurasi keamanan (Security Misconfiguration) pada API sering kali membocorkan hal-hal berikut dalam respons mentahnya:

1. **Kredensial yang di-hardcode:** Password admin, API key, atau token rahasia tertulis di dalam komentar kode atau objek JSON.
2. **Verbose Error / Stack Trace:** Coba kirim request yang salah (misal mengakses `/api/users/abc` menggunakan karakter string padahal meminta ID angka). Jika muncul error internal yang sangat detail, periksa apakah ada *flag* atau *path* sensitif yang bocor di sana.

Untuk membaca respons JSON dengan rapi di terminal Linux, Anda bisa menyalurkannya ke *tool* `jq`:

```bash
curl -s http://10.48.134.216:5002/api/users | jq

```

---

## Ringkasan Alur Kerja Anda:

1. **Buka Browser / Terminal** -> Akses `10.48.134.216:5002`.
2. **Inspect Element / View Source** -> Lihat apakah ada skrip JavaScript yang memanggil fungsi API tertentu (misal: `fetch('/api/v1/...')`).
3. **Gunakan Gobuster** -> Jika tidak ada tanda-tanda di halaman utama, paksa temukan folder API-nya.
4. **Tangkap Flag** -> Analisis data JSON yang keluar. *Flag* TryHackMe biasanya berformat `THM{...}`. Temukan string tersebut di dalam baris kode atau respons API yang terekspos.

---

# Software Supply Chain Failures

Teks ini membahas salah satu ancaman paling kompleks dalam keamanan modern: **AS03: Software Supply Chain Failures (Kegagalan Rantai Pasok Perangkat Lunak)**.

Di dunia nyata, celah ini sangat ditakuti karena penyerang tidak meretas sistem Anda secara langsung, melainkan meretas pihak ketiga yang produk atau kodenya Anda gunakan.

Berikut adalah pembedahan teknis mendalam mengenai maksud dari teks tersebut:

### 1. Definisi & Risiko Utama (What It Is & Why It Matters)

* **Bukan Salah Kode Anda:** Sama seperti kasus arsitektur sebelumnya, kode yang Anda tulis sendiri bisa jadi 100% aman. Namun, aplikasi modern tidak dibuat dari nol; developer menggunakan *library*, paket (seperti npm, pip, nuget), API, atau bahkan model AI milik orang lain.
* **Efek Domino:** Jika salah satu *dependency* (komponen luar) tersebut disusupi oleh hacker (*compromised*), maka otomatis aplikasi Anda yang mengimpor komponen tersebut akan ikut terinfeksi. Penyerang mendapatkan akses instan ke sistem Anda tanpa perlu menembus *firewall* atau sistem pertahanan depan Anda.

---

### 2. Studi Kasus Nyata: SolarWinds (2021) & Tren AI

* **SolarWinds Orion:** Ini adalah salah satu serangan siber terbesar dalam sejarah. Penyerang berhasil menyusup ke dalam **sistem build/update** milik SolarWinds (perusahaan software manajemen jaringan). Hacker menyuntikkan *malicious code* ke dalam file pembaruan resmi. Ketika ribuan perusahaan dan instansi pemerintah mengunduh update resmi tersebut, mereka otomatis terinfeksi.
* **Ancaman pada AI/ML:** Teks ini juga memperingatkan tren baru di tahun 2025/2026. Jika Anda menggunakan model AI *open-source* atau *dataset* pihak ketiga yang belum diverifikasi, penyerang bisa saja menanamkan *backdoor* (pintu belakang) atau bias tersembunyi di dalam model tersebut yang dapat membocorkan data saat aplikasi dijalankan.

---

### 3. Pola Celah Klasik (Common Patterns)

Ada beberapa kecerobohan yang membuat rantai pasok software menjadi rapuh:

* **Blind Trust (Kepercayaan Buta):** Menginstal *library* dari internet secara acak tanpa memeriksa reputasi atau kodenya.
* **Auto-Update Tanpa Verifikasi:** Mengonfigurasi sistem untuk otomatis menarik pembaruan komponen terluar tanpa melewati tahap pengujian (*staging*) dan verifikasi *checksum/digital signature*.
* **CI/CD Pipeline yang Lemah:** Server otomatisasi (seperti Jenkins, GitHub Actions) yang tidak diamankan, sehingga penyerang bisa memanipulasi skrip saat proses *compile* sedang berjalan.

---

### 4. Strategi Pertahanan (How To Protect)

Untuk mengamankan rantai pasok, tim keamanan menerapkan pendekatan berikut:

* **Software Bill of Materials (SBOM):** Membuat daftar inventarisasi berkala mengenai semua komponen pihak ketiga yang digunakan.
* **Dependency Scanning & Patching:** Menggunakan *tools* otomatis (seperti Snyk, OWASP Dependency-Check, atau GitHub Dependabot) untuk mendeteksi jika ada komponen yang sudah usang atau memiliki kerentanan (CVE).
* **Pipeline Hardening:** Mengunci akses ke CI/CD dan memastikan setiap paket yang diunduh diverifikasi keasliannya (*signed & audited*).

---

### 5. Panduan Menjawab Challenge Lab (Misi Anda)

Bagian akhir teks adalah instruksi praktis untuk menyelesaikan tantangan di TryHackMe:

* **Target IP:** `http://10.49.138.151:5003` (Akses melalui browser di AttackBox atau VPN Anda).
* **Petunjuk Serangan (Clue):** Teks menyebutkan bahwa aplikasi web tersebut menggunakan kode usang dan mengimpor komponen lama bernama `lib/vulnerable_utils.py`. Anda diminta untuk melakukan "debugging" (menganalisis/memperbaiki).
* **Taktik Eksekusi Anda:**
1. Buka alamat web tersebut. Biasanya di halaman utama atau halaman error akan ditampilkan baris kode atau informasi mengenai kegagalan fungsi.
2. Fokus pada file `vulnerable_utils.py`. Cari tahu fungsi apa yang dijalankan oleh skrip tersebut (bisa berupa fungsi enkripsi yang lemah, fungsi eksekusi perintah, atau fungsi pemrosesan input).
3. Manfaatkan kerentanan yang ada pada komponen usang tersebut. Karena namanya sudah terang-terangan mengandung kata *vulnerable*, periksa apakah ada parameter input yang dikirim ke fungsi tersebut yang bisa Anda manipulasi untuk memicu *Remote Code Execution* (RCE) atau *Information Disclosure* guna mendapatkan *flag*.

## Jawaban:
Untuk menyelesaikan *challenge* **AS03: Software Supply Chain Failures** pada IP `10.49.138.151:5003`, kita harus memanfaatkan kerentanan yang ada di dalam *library* pihak ketiga yang diimpor oleh aplikasi tersebut, yaitu `lib/vulnerable_utils.py`.

Berikut adalah panduan detail dan sistematis untuk menganalisis hingga mengeksploitasi celah tersebut dari mesin Linux Anda:

---

## Langkah 1: Reconnaissance (Analisis Awal)

1. **Buka Web Target:**
Buka browser di mesin Linux Anda (yang sudah terhubung VPN THM) dan akses:
`http://10.49.138.151:5003`
2. **Amati Interface & Fitur:**
Perhatikan input apa saja yang disediakan oleh aplikasi web tersebut. Biasanya, tantangan jenis ini menyediakan sebuah form input (misalnya: form untuk kalkulasi, form untuk konversi teks, atau form ping/sistem utilitas).
3. **Memicu Error (Verbosity):**
Coba masukkan input acak atau karakter spesial (seperti `'`, `"`, `;`, atau `|`) pada form yang tersedia untuk melihat apakah aplikasi memuntahkan *error message* (Stack Trace).
* Jika error muncul, periksa apakah ada informasi mengenai cara kerja `vulnerable_utils.py` atau fungsi Python apa yang dipanggil di belakangnya (misalnya fungsi `eval()`, `pickle.loads()`, atau `subprocess.Popen()`).



---

## Langkah 2: Mengintip/Menebak Isi `vulnerable_utils.py`

Karena ini adalah simulasi *Supply Chain*, celah berada di dalam *dependency* tersebut. Berdasarkan pola lab TryHackMe, fungsi di dalam `vulnerable_utils.py` biasanya menggunakan salah satu dari dua fungsi berbahaya di Python ini:

* **Skenario A: Fungsi `eval()` atau `exec()**`
Fungsi ini mengeksekusi string input langsung sebagai kode Python.
* **Skenario B: Fungsi `pickle.loads()` (Insecure Deserialization)**
Fungsi ini digunakan untuk membaca data serial, yang jika tidak difilter, bisa mengeksekusi perintah sistem (*Remote Code Execution*).

---

## Langkah 3: Eksekusi Serangan (Exploitation)

Mari kita asumsikan form tersebut menerima input untuk dieksekusi oleh `vulnerable_utils.py`. Kita akan mencoba menyuntikkan perintah Linux (*Command Injection* atau *Python Code Injection*).

### Pengujian dengan Python Injection (`eval` / `exec`)

Jika form tersebut adalah input teks biasa yang memproses data, coba masukkan kode Python untuk membaca file di dalam server.

Coba masukkan input ini ke dalam form di web:

```python
__import__('os').popen('id').read()

```

* **Jika web merespons** dengan menampilkan teks seperti `uid=0(root) gid=0(root)...`, artinya Anda berhasil melakukan **Remote Code Execution (RCE)**.

### Pengujian dengan Command Injection Biasa

Jika fungsi di dalam `vulnerable_utils.py` memanggil perintah sistem (seperti melakukan ping atau ekstraksi file), coba gunakan *separator* perintah Linux (seperti `;` atau `&&`).

Coba masukkan input ini ke dalam form:

```bash
; id
# atau
; cat flag.txt

```

---

## Langkah 4: Mengambil Flag

Setelah Anda memastikan bahwa input Anda bisa mengeksekusi perintah Linux, saatnya mencari di mana letak *flag* TryHackMe berada.

1. **List Direktori:**
Gunakan perintah `ls` untuk melihat file di direktori aktif aplikasi.
*Input pada form:*
```python
__import__('os').popen('ls -la').read()

```


*(Atau gunakan `; ls -la` jika itu Command Injection biasa).*
2. **Cari File Flag:**
Perhatikan apakah ada file bernama `flag.txt`, `secret.txt`, atau sejenisnya. Jika tidak ada di direktori saat ini, coba cek direktori utama user atau direktori root:
```python
__import__('os').popen('ls /').read()

```


3. **Membaca Isi Flag:**
Setelah menemukan file flag (misalnya bernama `flag.txt`), baca isinya menggunakan perintah `cat`:
*Input pada form:*
```python
__import__('os').popen('cat flag.txt').read()

```


*(Atau sesuaikan dengan *path* tempat file itu berada, misal: `cat /app/flag.txt`).*
4. **Salin Jawaban:**
Format flag yang Anda cari akan keluar di layar browser Anda dengan format **`THM{kantong_kunci_jawaban}`**. Salin string tersebut dan masukkan ke kolom jawaban di TryHackMe.

---

#
Teks ini membahas kategori **AS04: Cryptographic Failures (Kegagalan Kriptografi)**. Di dalam OWASP Top 10 terbaru, kategori ini berfokus pada bagaimana data sensitif terekspos karena enkripsi tidak digunakan, atau digunakan dengan cara yang salah/lemah.

Sebagai *cybersecurity professional*, celah ini sering kali menjadi penentu apakah *attacker* bisa melakukan eskalasi dari sekadar masuk ke jaringan hingga bisa membaca seluruh database sensitif perusahaan.

Berikut adalah pembedahan teknis mendalam mengenai maksud dari teks tersebut beserta panduan taktis untuk menyelesaikan tantangan labnya:

---

## 1. Definisi & Dampak (What It Is & Why It Matters)

* **Salah Implementasi, Bukan Salah Kriptografinya:** Masalah utamanya hampir tidak pernah terletak pada matematika di balik enkripsi, melainkan pada **keteledoran implementasi oleh manusia**. Contohnya seperti menyimpan kunci enkripsi di tempat yang salah atau menggunakan mode enkripsi yang cacat.
* **Vektor Serangan:** Jika data dikirim tanpa enkripsi (plain HTTP), penyerang bisa melakukan **Man-in-the-Middle (MitM)** untuk mengintip data di tengah jalan. Jika data dienkripsi dengan algoritma usang, penyerang bisa melakukan *brute-force* atau memanfaatkan cacat matematis untuk membongkarnya tanpa tahu kunci aslinya.

---

## 2. Pola Celah yang Sering Ditemui (Common Patterns)

Di lapangan, tim audit keamanan paling sering menemukan poin-poin kecerobohan ini:

* **Hard-coded Secrets:** Ini adalah dosa terbesar developer. Mereka menaruh *kunci enkripsi*, *API key*, atau *password database* langsung di dalam baris kode (misal: `key = "SuperSecretKey123"`). Ketika kode ini diunggah ke GitHub atau aplikasinya di-decompile, tamat sudah.
* **Weak Algorithms / ECB Mode:** Menggunakan fungsi *hashing* yang sudah rusak seperti MD5 atau SHA-1 (yang rentan terhadap *collision attack*). Atau menggunakan mode **AES-ECB** (Electronic Codebook), di mana blok data yang sama akan selalu menghasilkan enkripsi yang sama, sehingga pola data asli tetap terlihat (terkenal dengan analogi "ECB Penguin").
* **AI/ML Secret Handling:** Risiko modern di mana parameter model AI atau *prompt* yang berisi data sensitif dikirim ke pihak ketiga tanpa dienkripsi terlebih dahulu.

---

## 3. Strategi Pertahanan (How To Prevent It)

* **Gunakan Standar Modern:** Selalu gunakan algoritma standar industri seperti **AES-GCM** atau **ChaCha20-Poly1305** untuk data, serta paksa penggunaan **TLS 1.3** untuk jalur komunikasi.
* **Gunakan KMS (Key Management Service):** Jangan pernah menyimpan kunci di dalam kode atau server aplikasi yang sama. Gunakan solusi eksternal yang aman seperti **HashiCorp Vault**, **AWS KMS**, atau **Azure Key Vault**.
* **Key Rotation:** Terapkan kebijakan di mana kunci enkripsi otomatis diganti (dirotasi) secara berkala untuk membatasi dampak jika suatu saat kunci tersebut bocor.

---

---

## 4. Panduan Detail Menjawab Challenge Lab (Misi Anda)

**Target IP:** `http://10.49.138.151:5004`

**Tujuan:** Menemukan kunci (*key*) untuk mendekripsi sebuah file yang terkunci di server tersebut.

Berdasarkan teori *Cryptographic Failures* di atas, trik yang digunakan di lab TryHackMe biasanya berkisar pada **Hard-coded Key** atau **Information Disclosure**. Berikut alur kerja taktis dari mesin Linux Anda:

### Langkah 1: Eksplorasi Web (Reconnaissance)

1. Buka browser di Linux Anda dan akses `http://10.49.138.151:5004`.
2. Amati apa yang ada di halaman tersebut. Biasanya Anda akan melihat tombol untuk mengunduh file yang terenkripsi, atau form untuk memasukkan kunci dekripsi.

### Langkah 2: Berburu Kunci yang Tersembunyi (Source Code Audit)

Karena ini adalah tantangan "salah konfigurasi kriptografi", kemungkinan besar kuncinya disembunyikan di tempat yang bisa diakses publik secara tidak sengaja oleh developer.

1. **View Source Code:** Klik kanan pada halaman web -> **View Page Source** (atau tekan `Ctrl + U`).
2. Periksa apakah ada komentar HTML (seperti ``) atau skrip JavaScript yang berisi string aneh yang dicurigai sebagai kunci enkripsi.
3. **Periksa File JavaScript Eksternal:** Jika ada file `.js` yang di-load (misal `script.js` atau `app.js`), klik dan buka file tersebut. Developer sering kali melakukan *hard-code* kunci enkripsi langsung di dalam logika JavaScript di sisi *client*.

### Langkah 3: Periksa Backup atau Direktori Terbuka

Jika tidak ada di source code halaman utama, gunakan `curl` atau browser untuk menebak file sensitif yang ditinggalkan:

* Coba akses `http://10.49.138.151:5004/key.txt`
* Coba akses `http://10.49.138.151:5004/config.json`
* Coba akses direktori `.git` (jika developer lupa menghapusnya): `http://10.49.138.151:5004/.git/`

### Langkah 4: Eksekusi Dekripsi / Input Flag

Setelah Anda menemukan string panjang yang mencurigakan (bisa berupa teks biasa, Hex, atau Base64):

1. Masukkan string kunci tersebut ke dalam form input dekripsi yang disediakan di web target.
2. Jika kuncinya benar, sistem akan mendekripsi file dan memuntahkan flag TryHackMe Anda (**`THM{...}`**).

---

