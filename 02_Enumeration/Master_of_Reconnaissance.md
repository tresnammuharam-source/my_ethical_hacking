# RECONNAISSANCE

Dalam fase ofensif, istilah yang lebih tepat digunakan adalah **Reconnaissance** (pengintaian). Ini adalah langkah awal untuk mengumpulkan informasi sebanyak mungkin tentang target sebelum melakukan penetrasi.

Berikut adalah alat dan metode yang umum digunakan:

### 1. Passive Reconnaissance

Mengumpulkan data tanpa berinteraksi langsung dengan sistem target agar tidak terdeteksi.

* **Google Dorking:** Menggunakan operator pencarian khusus untuk menemukan file sensitif atau direktori terbuka.
* **Whois & DNS Lookup:** Mencari informasi kepemilikan domain dan catatan IP.
* **Shodan:** Mencari perangkat yang terhubung ke internet (IoT, server, kamera).
* **TheHarvester:** Mengumpulkan email, sub-domain, dan nama karyawan dari sumber publik.

### 2. Active Reconnaissance

Berinteraksi langsung dengan target untuk memetakan infrastruktur.

* **Nmap:** Alat utama untuk **network scanning**, mengetahui port yang terbuka, dan sistem operasi yang digunakan.
* **Burp Suite:** Digunakan untuk memetakan struktur aplikasi web dan mencari celah keamanan.
* **Gobuster/Dirbuster:** Melakukan *brute-force* untuk menemukan direktori atau sub-domain tersembunyi.
* **Netcat:** Digunakan untuk *banner grabbing* guna mengetahui versi layanan yang berjalan pada suatu port.

### Alur Kerja (Workflow)

1. **Footprinting:** Menentukan ruang lingkup (IP range, domain).
2. **Scanning:** Mengidentifikasi host yang aktif dan port terbuka.
3. **Enumeration:** Mencari informasi mendalam seperti nama *user*, *shares*, dan versi layanan spesifik untuk mencari kerentanan.

---

Untuk menjadi ahli dalam tahap pengintaian (**Reconnaissance**), fokus utama Anda adalah menguasai teknik pengumpulan data secara otomatis dan mendalam. Anda perlu menggabungkan teknik **OSINT** (Open Source Intelligence) dengan alat pemindaian infrastruktur.

### Langkah Strategis

1. **Kuasai Automasi Scripting:** Pelajari Python atau Bash. Seorang ahli tidak menjalankan alat satu per satu secara manual, melainkan membuat *pipeline* agar alat-alat tersebut bekerja secara beruntun.
2. **Pahami Arsitektur Jaringan & Cloud:** Pelajari cara kerja DNS, pemetaan ASN (*Autonomous System Number*), dan bagaimana data tersimpan di *bucket* cloud yang tidak terproteksi (S3 Buckets).
3. **Pelajari Pengolahan Data:** Fokus pada teknik memilah ribuan data mentah menjadi informasi yang berguna (*actionable intelligence*).

### Alat untuk Mengumpulkan Data Massal

| Kategori | Alat / Tool | Kegunaan Utama |
| --- | --- | --- |
| **All-in-One Framework** | **Recon-ng** | Framework modular mirip Metasploit khusus untuk pengintaian. |
| **Subdomain Discovery** | **Subfinder** & **Amass** | Mencari ribuan sub-domain menggunakan berbagai sumber API. |
| **Asset Mapping** | **Maltego** | Visualisasi hubungan antara orang, grup, domain, dan infrastruktur. |
| **Web Crawling** | **Katana** | *Crawler* generasi baru untuk menemukan setiap sudut dan parameter di situs web. |
| **Vulnerability Recon** | **Nuclei** | Memindai target secara massal untuk mencari celah spesifik berdasarkan *template*. |

### Cara Kerja Pengumpulan Data Masif

* **Horizontal Recon:** Mencari seluruh aset yang dimiliki organisasi (IP, Domain, ASN).
* **Vertical Recon:** Masuk lebih dalam ke satu aset untuk menemukan direktori tersembunyi, parameter API, dan bocoran kredensial di GitHub menggunakan alat seperti **TruffleHog**.

---

## tahapan-tahapan untuk bisa langsung melakukannya

Untuk menjadi ahli, fokuslah pada membangun **Recon Pipeline** otomatis agar Anda bisa mengolah data dalam jumlah besar tanpa input manual yang berulang.

Berikut adalah tahapan praktis untuk langsung memulainya di Kali Linux:

### 1. Persiapan API Keys

Banyak alat hebat bersifat mandul tanpa data. Segera daftar dan masukkan API keys dari layanan seperti **BinaryEdge**, **Censys**, **Shodan**, dan **SecurityTrails** ke dalam konfigurasi alat Anda (terutama pada `Amass`).

### 2. Tahapan Eksekusi (Workflow)

* **Fase 1: Asset Discovery (Horizontal)**
Gunakan **Amass** atau **Subfinder** untuk memetakan seluruh domain dan IP yang berkaitan dengan target.
`subfinder -d target.com -o subdomains.txt`
* **Fase 2: Filtering & Probing (Vertical)**
Gunakan **httpx** untuk memeriksa subdomain mana yang benar-benar aktif dan merespons pada port 80/443.
`cat subdomains.txt | httpx -title -status-code -o alive.txt`
* **Fase 3: Content Enumeration**
Jalankan **Katana** untuk melakukan *crawling* masif guna menemukan endpoint API, file tersembunyi, dan parameter sensitif.
`katana -u alive.txt -o endpoints.txt`
* **Fase 4: Vulnerability Scanning**
Gunakan **Nuclei** dengan template komunitas untuk mencari celah keamanan (misconfig, CVE lama) secara otomatis pada semua endpoint yang ditemukan.
`nuclei -l alive.txt`

### 3. Otomasi dengan Bash Scripting

Jangan jalankan satu per satu; buat script sederhana yang menggabungkan semua perintah di atas sehingga Anda cukup memasukkan satu domain dan membiarkan Kali Linux bekerja mengumpulkan data selama Anda tidur.

**Peringatan:** Lakukan ini hanya pada sistem yang Anda miliki izin tertulisnya (seperti program *Bug Bounty*) untuk menghindari masalah hukum.

---

## memahami lebih dalam tahapan reconnasainnce

Untuk memahami secara mendalam, Anda harus mempelajari **mekanisme di balik alat** tersebut. Jangan sekadar menghafal perintah, tetapi pahami bagaimana protokol komunikasi bekerja.

### Langkah untuk Pemahaman Mendalam

* **Analisis Paket:** Gunakan **Wireshark** saat menjalankan *tools* pengintaian. Lihat bagaimana paket `SYN`, `ACK`, atau permintaan `HTTP` dikirim dan diterima. Ini mengajarkan Anda apa yang sebenarnya dideteksi oleh *firewall* target.
* **Bangun Lab Sendiri:** Instal sistem yang sengaja dibuat rentan seperti **Metasploitable** atau **OWASP Juice Shop**. Praktikkan *reconnaissance* di sana dan lihat log di sisi server untuk memahami "jejak" yang Anda tinggalkan.
* **Baca Dokumentasi Manual:** Pelajari *flag* pada perintah (misal: arti `-sV` atau `-Pn` pada Nmap). Memahami logika di balik opsi ini akan membantu Anda menyesuaikan serangan pada situasi yang berbeda.
* **Pelajari Coding:** Pelajari **Python**. Cobalah membuat alat *port scanner* sederhana sendiri. Dengan membangunnya dari nol, Anda akan paham mengapa suatu alat bisa gagal atau berhasil mengambil data.

**Kuncinya adalah: Lihat apa yang terjadi di kabel (jaringan) dan apa yang tercatat di log.**

Memulai perjalanan di bidang pengintaian (*reconnaissance*) berarti Anda sedang belajar cara menjadi **detektif digital**. Kunci utamanya bukan pada kecanggihan alat,
melainkan pada kemampuan Anda menghubungkan titik-titik data yang tersebar menjadi sebuah peta serangan yang utuh.

Berikut adalah tiga pilar yang harus Anda pegang agar tidak sekadar menjadi pengguna alat:

* **Pahami Footprinting:** Pelajari bagaimana setiap interaksi (seperti DNS *query*) meninggalkan jejak. Jika Anda tahu jejak apa yang ditinggalkan, Anda bisa belajar cara menyembunyikannya atau memalsukannya.
* **Logika Eksploitasi:** Selalu tanyakan, *"Mengapa data ini penting?"*. Mengetahui sebuah port terbuka tidak berguna jika Anda tidak tahu layanan apa yang berjalan di sana dan celah apa yang biasanya ada pada versi tersebut.
* **Metodologi OSINT:** Latihlah insting Anda untuk mencari informasi di tempat yang tidak terlihat, seperti komentar di kode sumber (*source code*) publik, dokumen lama di server yang terlupakan, atau profil media sosial karyawan perusahaan target.

Sebagai latihan awal, cobalah lakukan **Self-Recon**: gunakan alat-alat yang sudah disebutkan sebelumnya terhadap domain atau IP milik Anda sendiri,
lalu periksa log di server Anda untuk melihat seberapa "berisik" atau terdeteksinya aktivitas tersebut.

