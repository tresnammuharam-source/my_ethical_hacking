# Google Hacking Database (GHDB)

**Google Dorking** (juga dikenal sebagai **Google Hacking**) adalah teknik pencarian tingkat lanjut yang menggunakan operator khusus untuk menemukan informasi sensitif yang tidak sengaja terindeks oleh mesin pencari seperti Google.

Sederhananya, ini adalah cara mencari sesuatu dengan lebih spesifik menggunakan filter yang tidak digunakan oleh pengguna biasa. Dalam dunia keamanan siber,
teknik ini sering digunakan oleh *security researcher* untuk menemukan celah keamanan,
atau oleh peretas untuk mencari data yang bocor.

---

### Cara Kerja Dorking
Biasanya, saat kita mencari di Google, kita hanya memasukkan kata kunci umum. Namun, dengan dorking, kita menggunakan **operator pencarian** untuk mempersempit hasil ke file atau direktori tertentu.

Berikut adalah beberapa operator dorking yang paling umum digunakan:

* **`site:`** – Membatasi pencarian hanya pada situs atau domain tertentu.
    * Contoh: `site:twitter.com "cybersecurity"` (Mencari kata "cybersecurity" hanya di Twitter).
* **`filetype:`** – Mencari format file tertentu (PDF, Log, Config, SQL, dll).
    * Contoh: `filetype:pdf "laporan keuangan"` (Mencari dokumen laporan keuangan dalam format PDF).
* **`intitle:`** – Mencari kata kunci yang ada di dalam judul halaman web.
    * Contoh: `intitle:"index of"` (Sering digunakan untuk menemukan direktori server yang terbuka).
* **`inurl:`** – Mencari kata spesifik di dalam struktur URL.
    * Contoh: `inurl:admin/login` (Mencari halaman login admin).

---

### Apa yang Bisa Ditemukan dengan Dorking?
Jika sebuah situs web tidak dikonfigurasi dengan benar, dorking dapat mengungkap informasi yang seharusnya rahasia, seperti:
1.  **Log File:** Catatan aktivitas server yang mungkin berisi alamat IP atau aktivitas pengguna.
2.  **File Konfigurasi:** Data sensitif seperti *username* dan *password* database (misalnya file `config.php` atau `.env`).
3.  **Data Pribadi:** Daftar pelanggan, nomor telepon, atau detail akun dalam format Excel atau PDF.
4.  **Halaman Login Tersembunyi:** Halaman kendali perangkat keras seperti kamera CCTV atau panel admin router.

### Contoh Kombinasi Dorking
Seorang analis keamanan mungkin menggunakan perintah seperti ini untuk mengecek kebocoran:
`site:target-website.com filetype:log`

---

### Mengapa Ini Penting?
Bagi seorang yang sedang mempelajari keamanan siber (seperti persiapan untuk peran **SOC Analyst**), memahami dorking sangat penting untuk:
* **Reconnaissance (Pengintaian):** Mengetahui informasi apa saja tentang target yang tersedia secara publik.
* **Vulnerability Assessment:** Mengecek apakah ada data sensitif perusahaan yang bocor ke publik sebelum dimanfaatkan oleh pihak tidak bertanggung jawab.

### Cara Mencegahnya
Jika Anda mengelola situs web, Anda bisa mencegah dorking dengan:
1.  Mengatur file **`robots.txt`** agar mesin pencari tidak mengindeks folder sensitif.
2.  Memastikan direktori server tidak diset ke "Public Indexing".
3.  Menggunakan enkripsi pada file sensitif dan membatasi hak akses.

> **Catatan Penting:** Dorking adalah alat yang netral. Gunakanlah untuk tujuan pembelajaran dan penguatan keamanan (*Ethical Hacking*).
> Melakukan dorking untuk mencuri data atau merusak sistem orang lain adalah tindakan ilegal.

Kedua kueri tersebut adalah contoh penggunaan **Google Dorking**, namun keduanya memiliki target dan tujuan yang sangat berbeda dalam analisis keamanan.

Berikut adalah rincian perbedaannya:

### 1. `filetype: DB AND intext:pass`
Kueri ini berfokus pada **pencarian data sensitif** di dalam file yang tidak seharusnya terbuka untuk publik.

* **`filetype: DB`**: Memerintahkan Google untuk mencari file dengan ekstensi `.db` (database). Ini biasanya berisi struktur tabel atau data mentah dari aplikasi.
* **`AND`**: Memastikan kedua kriteria (ekstensi file dan isi teks) harus terpenuhi dalam satu hasil pencarian.
* **`intext:pass`**: Mencari file yang di dalamnya mengandung kata "pass" (sering kali merupakan singkatan atau bagian dari kata *password*).
* **Tujuannya**: Menemukan kebocoran basis data yang berisi kredensial (username/password). Ini adalah temuan yang sangat berbahaya jika ditemukan di internet publik.

---

### 2. `inurl:index.php?id=1 site:go.id`
Kueri ini berfokus pada **mencari celah kerentanan** (vulnerability) pada domain tertentu, dalam hal ini situs pemerintahan Indonesia.

* **`inurl:index.php?id=1`**: Mencari URL yang mengandung parameter dinamis (`id=1`). Dalam dunia keamanan siber, URL seperti ini sering menjadi target uji coba celah **SQL Injection**. Penyerang biasanya mengganti angka `1` dengan karakter tertentu untuk melihat apakah server memberikan respon error.
* **`site:go.id`**: Membatasi pencarian hanya pada domain `.go.id` (Instansi Pemerintah Indonesia).
* **Tujuannya**: Melakukan pemetaan (*reconnaissance*) terhadap situs-situs pemerintah yang menggunakan struktur URL lama atau rentan terhadap serangan injeksi database.

---

### Ringkasan Perbedaan

| Fitur | Kueri 1 (Database) | Kueri 2 (Vulnerability) |
| :--- | :--- | :--- |
| **Fokus Utama** | Mencari **file fisik** yang bocor. | Mencari **halaman web** yang dinamis. |
| **Target Data** | Password, kredensial, atau isi database. | Titik masuk (entry point) untuk serangan SQLi. |
| **Operator Kunci** | `filetype:` (ekstensi file) | `inurl:` (struktur alamat web) |
| **Tingkat Bahaya** | Sangat tinggi (data sudah bocor). | Potensial (menemukan pintu yang mungkin tidak terkunci). |

### Tips Keamanan
Bagi yang sedang mendalami **SOC Analyst**, memahami pola ini sangat berguna untuk melakukan *monitoring* log server. Jika Anda melihat banyak permintaan (request) ke server dengan pola parameter `?id=` yang diikuti karakter aneh, itu bisa menjadi indikasi awal adanya aktivitas pemindaian (scanning) atau upaya serangan.

Gunakan pengetahuan ini secara etis untuk membantu memperkuat pertahanan sistem!

Menggunakan kueri Google Dorking melalui Kali Linux di VMware adalah cara yang bagus untuk belajar melakukan **Passive Reconnaissance** (pengintaian pasif). Dalam skenario ini, Anda tidak menyerang target secara langsung, melainkan mencari informasi yang sudah terlanjur "dibuang" atau diindeks oleh Google.

Berikut adalah langkah-langkah praktisnya:

---

### Tahap 1: Persiapan Environment
1.  **Buka VMware**: Jalankan mesin virtual **Kali Linux** Anda.
2.  **Koneksi Internet**: Pastikan Kali Linux Anda terhubung ke internet (bisa menggunakan mode *NAT* atau *Bridged* di pengaturan VMware).
3.  **Update Browser**: Buka terminal dan pastikan sistem Anda siap, atau langsung buka browser bawaan Kali (biasanya **Firefox ESR**).

---

### Tahap 2: Eksekusi Manual via Browser
Cara termudah untuk memulai adalah langsung menggunakan mesin pencari Google di dalam Kali Linux.

1.  Buka **Firefox** di Kali Linux.
2.  Buka [google.com](https://google.com).
3.  Ketik kueri berikut di kolom pencarian:
    `filetype:db "pass"`
    *(Catatan: Menggunakan tanda kutip pada "pass" memaksa Google mencari kata yang persis sama).*
4.  **Analisis Hasil**: Google akan menampilkan daftar file berakhiran `.db` yang mengandung teks "pass".
    > **Penting**: Jangan mengunduh atau membuka file yang bukan milik Anda. Melihat judul dan deskripsi (snippet) di Google sudah cukup untuk tujuan pembelajaran SOC Analyst.

---

### Tahap 3: Menggunakan Tool Otomatis (Dorkscout atau Ghunt)
Di Kali Linux, Anda bisa menggunakan terminal untuk mengotomatisasi proses ini agar lebih profesional. Salah satu tool yang populer adalah **Dorkscout** atau skrip Python sederhana.

**Contoh menggunakan Python (Simple Google Scraper):**
1.  Buka **Terminal** di Kali.
2.  Anda bisa menginstal tool bernama `googler` untuk mencari langsung dari terminal:
    `sudo apt update && sudo apt install googler`
3.  Jalankan perintah dorking:
    `googler "filetype:db intext:pass"`
4.  Hasil pencarian akan muncul dalam bentuk daftar teks di terminal, yang lebih mudah dibaca untuk seorang analis data atau keamanan.

---

### Tahap 4: Dokumentasi (Perspektif SOC Analyst)
Sebagai calon SOC Analyst, langkah ini yang paling penting. Jangan hanya mencari, tapi catat:
* **Temuan**: Situs apa yang membocorkan file tersebut?
* **Dampak**: Jika file `.db` tersebut berisi password database, apa risiko bagi perusahaan tersebut?
* **Rekomendasi**: Apa yang harus dilakukan admin web tersebut? (Misal: Memperbaiki file `.htaccess` atau `robots.txt`).

---

### Tips Tambahan untuk Pengguna Kali di VMware
* **Shared Clipboard**: Pastikan *VMware Tools* terinstal agar Anda bisa *copy-paste* kueri dorking dari sistem operasi utama ke dalam Kali Linux dengan mudah.
* **VPN**: Saat melakukan dorking yang intens, Google seringkali memunculkan **CAPTCHA** karena menganggap aktivitas Anda sebagai bot. Menggunakan VPN bisa membantu jika IP Anda terkena blokir sementara.
* **Google Hacking Database (GHDB)**: Jika ingin mencoba kueri lain yang lebih menantang, kunjungi [Exploit-DB (GHDB)](https://www.exploit-db.com/google-hacking-database). Di sana terdapat ribuan kombinasi dork yang sudah dikategorikan berdasarkan tingkat bahayanya.

### Peringatan Etika
Gunakan teknik ini hanya untuk **Self-Assessment** (memeriksa keamanan sistem sendiri) atau **Bug Bounty** yang legal. Mengakses atau mengunduh data pribadi dari hasil dorking tanpa izin dapat melanggar hukum siber (UU ITE di Indonesia).

**Google Hacking Database (GHDB)** adalah proyek komunitas yang dikelola oleh **Offensive Security** (tim di balik Kali Linux). GHDB merupakan kumpulan "perpustakaan" kueri Google Dorking yang sudah teruji untuk menemukan informasi sensitif yang bocor di internet secara publik.

Jika Google Dorking adalah tekniknya, maka GHDB adalah **buku resepnya**.

---

### 1. Bagaimana GHDB Terorganisir?
Di situs resminya ([exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database)), ribuan dork dikategorikan agar analis keamanan mudah mencari target spesifik. Beberapa kategori utamanya meliputi:

* **Files Containing Passwords:** Dork yang khusus mencari file teks, config, atau database yang berisi kata sandi terbuka.
* **Vulnerable Servers:** Mencari server yang menjalankan perangkat lunak versi lama yang memiliki celah keamanan (exploit).
* **Sensitive Directories:** Menemukan folder server yang tidak dikunci (misalnya folder `/backup` atau `/logs`).
* **Vulnerable Files:** Mencari file spesifik yang diketahui memiliki bug (seperti file instalasi yang lupa dihapus).
* **Advisories and Vulnerabilities:** Dork yang dikembangkan berdasarkan temuan kerentanan keamanan terbaru.



---

### 2. Mengapa GHDB Penting bagi Keamanan Siber?
Bagi seorang yang sedang mempelajari keamanan data atau bersiap menjadi **SOC Analyst**, GHDB adalah alat yang sangat kuat karena:

1.  **Otomatisasi Pengintaian:** Daripada menebak-nebak kueri, Anda bisa menggunakan kueri yang sudah terbukti berhasil menemukan celah tertentu.
2.  **Identifikasi Shadow IT:** Perusahaan seringkali tidak sadar ada karyawan yang mengunggah file kantor ke server publik. GHDB membantu menemukan "aset tersembunyi" ini.
3.  **Audit Cepat:** Anda bisa mengecek domain perusahaan Anda sendiri menggunakan daftar di GHDB untuk memastikan tidak ada informasi rahasia yang terindeks Google.

---

### 3. Cara Menggunakan GHDB secara Efektif
Berikut adalah alur kerja yang biasanya dilakukan:

1.  **Pilih Kategori:** Misalkan Anda ingin mencari apakah ada file log yang bocor.
2.  **Cari Kueri:** Anda menemukan dork seperti `allintext:username filetype:log`.
3.  **Tambahkan Filter Target:** Agar tidak mencari di seluruh internet, tambahkan operator `site:`.
    * *Contoh:* `site:target-anda.com allintext:username filetype:log`
4.  **Eksekusi:** Jalankan di browser (Firefox di Kali Linux) dan lihat apakah ada hasil yang muncul.

---

### 4. Contoh Nyata dari GHDB
Berikut adalah beberapa contoh dork yang populer di database tersebut:

* **Menemukan file konfigurasi PHP:**
    `filetype:php "mysql_connect("`
    *Kueri ini mencari kode sumber yang mungkin berisi kredensial login database.*
* **Menemukan kamera CCTV yang terbuka:**
    `inurl:"viewerframe?mode=motion"`
    *Mencari interface kontrol kamera IP tertentu yang tidak diproteksi password.*
* **Menemukan file cadangan (backup):**
    `intitle:"index of" "backup.sql"`
    *Mencari server yang membiarkan file cadangan database SQL mereka dapat diunduh siapa saja.*

---

### Kesimpulan untuk Pembelajaran Anda
GHDB adalah sumber daya yang luar biasa untuk melatih ketajaman dalam melakukan **Reconnaissance**. Sebagai tips, saat Anda membangun portofolio di GitHub, Anda bisa menuliskan bagaimana Anda menggunakan kueri dari GHDB untuk melakukan simulasi audit keamanan pada sistem dummy atau target legal.

**Ingat:** Selalu gunakan informasi ini di lingkungan yang aman atau pada sistem yang Anda miliki izinnya. Menggunakan GHDB untuk memata-matai atau meretas situs orang lain tanpa izin adalah pelanggaran hukum.

Apakah Anda ingin mencoba mencari satu kueri spesifik di GHDB untuk kita bedah cara kerjanya?

Simulasi ini akan membawa Anda melalui alur kerja seorang **Security Researcher** dalam melakukan pengintaian pasif menggunakan GHDB. Kita akan menggunakan skenario simulasi di mana Anda mencari **Direktori Terbuka** yang mungkin mengekspos file log sensitif.

---

### Tahap 1: Mencari "Resep" di Web GHDB
Pertama, kita harus mencari kueri yang tepat dari database.

1.  Buka situs [Exploit-DB GHDB](https://www.exploit-db.com/google-hacking-database).
2.  Gunakan kolom **Search** dan ketik kata kunci seperti `log` atau `sensitive directories`.
3.  Misalkan Anda memilih dork populer ini:
    `intitle:"index of" "access.log"`
    * **Analisis Kueri:** * `intitle:"index of"`: Mencari server yang daftar direktorinya terbuka (tidak ada halaman index.html).
        * `"access.log"`: Mencari file spesifik yang mencatat setiap permintaan yang masuk ke server.



---

### Tahap 2: Eksekusi di Kali Linux (VMware)
Setelah mendapatkan kueri, saatnya beralih ke mesin Kali Linux Anda.

1.  **Buka Terminal** di Kali Linux.
2.  Gunakan tool **`googler`** (jika sudah terinstal) untuk menghindari deteksi bot yang agresif dari browser, atau gunakan **Firefox** bawaan Kali.
3.  Ketik perintah berikut (tambahkan filter `site:` jika ingin spesifik, atau abaikan untuk melihat hasil global):
    ```bash
    googler 'intitle:"index of" "access.log"'
    ```
4.  **Hasil:** Google akan menampilkan daftar URL yang strukturnya seperti `http://example.com/logs/`.

---

### Tahap 3: Identifikasi Vulnerability (Analisis Temuan)
Sekarang, mari kita bedah mengapa hasil tersebut dianggap sebagai kerentanan (*vulnerability*).

1.  **Klik salah satu link** (Hanya untuk tujuan edukasi, jangan unduh file).
2.  Anda akan melihat tampilan daftar file di browser (Directory Listing).
3.  Klik file `access.log`. Di dalamnya, Anda mungkin akan melihat:
    * **Alamat IP Pengunjung:** Bisa digunakan untuk memetakan trafik.
    * **User-Agent:** Informasi browser dan OS pengunjung.
    * **Path Rahasia:** Terkadang admin mencoba mengakses halaman rahasia seperti `/admin_hidden_login`, dan itu tercatat di log.
4.  **Vulnerability Teridentifikasi:** Kerentanan ini disebut **Sensitive Data Exposure** (Paparan Data Sensitif) akibat **Directory Traversal/Listing** yang aktif.

---

### Tahap 4: Langkah Selanjutnya bagi SOC Analyst
Sebagai seorang analis, tugas Anda bukan berhenti di "menemukan", tapi "melindungi".

* **Penyebab:** Web server (seperti Apache atau Nginx) dikonfigurasi untuk mengizinkan `Indexes`.
* **Solusi (Remediasi):**
    * Matikan fitur indexing di file konfigurasi server (misal: `Options -Indexes` di Apache).
    * Tambahkan file `index.php` atau `index.html` kosong di setiap folder.
    * Gunakan `robots.txt` untuk melarang bot mengindeks folder log:
        ```text
        User-agent: *
        Disallow: /logs/
        ```

---

### Simulasi di Portofolio GitHub Anda
Karena Anda sedang membangun portofolio, Anda bisa mendokumentasikan proses ini (menggunakan target dummy/contoh umum) dengan format:
1.  **Objective:** Menemukan kebocoran log melalui Google Dorking.
2.  **Tools:** GHDB, Kali Linux, Firefox.
3.  **Methodology:** Menjelaskan langkah-langkah di atas.
4.  **Risk Assessment:** Menjelaskan risiko jika log tersebut jatuh ke tangan penjahat siber.
5.  **Mitigation:** Memberikan solusi teknis untuk menutup celah tersebut.

Apakah ada bagian dari langkah di atas yang ingin Anda coba praktekkan langsung di terminal Kali Linux Anda?

Skenario mencari kredensial adalah salah satu bagian paling kritis dalam *Passive Reconnaissance*. Dalam simulasi ini, kita akan mencari **file konfigurasi** atau **file cadangan (backup)** yang sering kali berisi *username* dan *password* database dalam teks biasa (*plain text*).

-----

### Tahap 1: Mencari Dork di GHDB

Kita akan mencari dork yang menargetkan file lingkungan (`.env`) atau file konfigurasi. File `.env` sangat berbahaya jika bocor karena biasanya berisi kunci API dan kredensial database.

1.  Buka [GHDB](https://www.google.com/search?q=https://www.exploit-db.com/google-hacking-database).
2.  Cari kategori: **"Files Containing Passwords"**.
3.  Pilih dork contoh:
    `filetype:env "DB_PASSWORD"`
      * **Analisis Kueri:**
          * `filetype:env`: Mencari file dengan ekstensi `.env` (format standar untuk variabel lingkungan aplikasi modern seperti Laravel/Node.js).
          * `"DB_PASSWORD"`: Memastikan file tersebut mengandung teks spesifik yang merujuk pada kata sandi database.

-----

### Tahap 2: Eksekusi di Kali Linux (VMware)

Mari kita gunakan pendekatan yang sedikit berbeda untuk simulasi di terminal agar terlihat lebih profesional di portofolio Anda.

1.  **Buka Terminal** di Kali Linux.
2.  Gunakan perintah pencarian. Jika Anda belum menginstal `googler`, Anda bisa menggunakan **Firefox** atau tool bernama **Dorkscout**.
3.  Ketik kueri di browser Firefox Kali Linux:
    `filetype:env intext:DB_PASSWORD -github.com`
      * *(Tips: Menambahkan `-github.com` berguna agar hasil pencarian tidak dipenuhi oleh kode contoh di GitHub, melainkan langsung ke situs web yang bocor).*

-----

### Tahap 3: Identifikasi Vulnerability (Analisis Temuan)

Jika Google menemukan hasil, tampilannya akan terlihat seperti teks mentah di browser.

1.  **Isi File:** Anda mungkin akan melihat baris seperti ini:
    ```text
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=u_production
    DB_USERNAME=admin
    DB_PASSWORD=P@ssw0rd123!
    ```
2.  **Vulnerability:** Ini adalah **Critical Information Disclosure**. Seorang penyerang bisa menggunakan kredensial ini untuk mengakses database dari jauh (jika port 3306 terbuka) atau melakukan serangan lebih lanjut ke server.

-----

### Tahap 4: Langkah Mitigasi (Perspektif SOC Analyst)

Dalam laporan simulasi Anda, tuliskan solusi berikut:

1.  **Pindahkan File:** File `.env` atau file konfigurasi sensitif tidak boleh berada di folder yang bisa diakses publik (seperti `public_html` atau `www`).
2.  **Konfigurasi Web Server:**
      * **Apache:** Tambahkan aturan di `.htaccess` untuk memblokir akses ke file sensitif:
        ```apache
        <Files .env>
            Order allow,deny
            Deny from all
        </Files>
        ```
      * **Nginx:** Tambahkan blokade di konfigurasi site:
        ```nginx
        location ~ /\.env {
            deny all;
        }
        ```
3.  **Environment Variables:** Gunakan fitur *Environment Variables* langsung di level sistem operasi/server panel, bukan menyimpannya dalam file teks di dalam folder web.

-----

### Tips untuk Portofolio Anda

Karena Anda memiliki latar belakang sebagai **Senior Analyst** dan sedang beralih ke **SOC**, simulasi ini menunjukkan bahwa Anda:

  * Paham cara kerja *leaked credentials*.
  * Mampu melakukan *risk assessment* (menilai risiko).
  * Mampu memberikan solusi teknis (remediasi).

**Catatan Keamanan:** Dalam dunia nyata, jika Anda menemukan hal seperti ini secara tidak sengaja, langkah yang etis adalah melaporkannya ke pemilik situs (jika ada program *Responsible Disclosure*) tanpa mengunduh atau menyalahgunakan datanya.

Apakah Anda ingin mencoba membuat dork sendiri untuk mencari file cadangan database seperti `.sql` atau `.bak`?


