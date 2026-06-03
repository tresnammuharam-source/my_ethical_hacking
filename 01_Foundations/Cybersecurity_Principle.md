# PRINSIP-PRINSIP CYBER SECURITY

---

# 2 PRINSIP CYBER SECURITY

Kita akan membahas salah satu fondasi paling krusial dalam dunia keamanan siber (*cybersecurity*), yaitu **bagaimana kita mengelola rasa percaya (trust) terhadap pengguna, perangkat, dan sistem di dalam sebuah organisasi.**

Berikut adalah penjelasan lengkap, maksud, serta contoh nyata dari isi tulisan tersebut agar Anda mudah memahaminya.

---

## 1. Maksud Utama Tulisan (The Big Picture)

Secara garis besar, tulisan ini ingin menyampaikan bahwa **dalam dunia bisnis dan teknologi, kita tidak bisa hidup tanpa rasa percaya, tetapi rasa percaya yang berlebihan adalah sebuah celah keamanan (vulnerability).**

Jika kita terlalu curiga (misalnya takut pabrik laptop menanam *spyware*), kita tidak akan pernah mulai bekerja karena sibuk membongkar sistem. Namun sebaliknya, jika kita terlalu percaya, jaringan kita akan sangat mudah dibobol. Oleh karena itu, dunia *cybersecurity* melahirkan dua prinsip utama untuk menyeimbangkan hal ini: **Trust but Verify** (Percaya tapi Verifikasi) dan **Zero Trust** (Tanpa Rasa Percaya).

---

## 2. Bedah Prinsip 1: Trust but Verify (Percaya tapi Verifikasi)

### Arti & Maksud:

Prinsip ini adalah model keamanan tradisional. Di sini, organisasi **memberikan kepercayaan di awal** kepada entitas (user atau perangkat) yang berada di dalam jaringan internal mereka (misalnya karyawan yang bekerja di kantor). Namun, segala aktivitas mereka tetap **diawasi dan dicatat (logging)** untuk memastikan tidak ada hal aneh yang terjadi.

Tulisan tersebut juga menyebutkan bahwa manusia tidak akan sanggup memeriksa miliaran log aktivitas secara manual (misalnya memeriksa satu per satu riwayat *browsing* ratusan karyawan). Oleh karena itu, diperlukan alat otomatis seperti *Proxy*, IDS (*Intrusion Detection System*), dan IPS (*Intrusion Prevention System*).

### Contoh Nyata:

> **Skenario Kantor Tradisional:**
> Anda adalah seorang karyawan yang bekerja di dalam gedung kantor dan laptop Anda terhubung ke Wi-Fi resmi kantor. Karena Anda berada "di dalam", sistem langsung mempercayai Anda untuk mengakses file server perusahaan tanpa berkali-kali meminta password.
> Namun, tim IT tetap memasang sistem filter (Proxy) di latar belakang. Jika tiba-tiba laptop Anda mencoba mengakses situs judi atau *malware*, sistem otomatis (IDS/IPS) akan memblokirnya dan mencatatnya sebagai laporan kecurigaan.

---

## 3. Bedah Prinsip 2: Zero Trust (Jangan Pernah Percaya, Selalu Verifikasi)

### Arti & Maksud:

Prinsip ini lahir karena model *Trust but Verify* memiliki kelemahan fatal: **Ancaman dari Dalam (Insider Threats)**. Jika peretas berhasil mencuri akun satu karyawan di dalam kantor, peretas tersebut bisa bebas bergerak karena sistem terlanjur "percaya" pada jaringan internal.

Zero Trust menganggap **rasa percaya sebagai kelemahan**. Semboyannya adalah *"Never Trust, Always Verify"* (Jangan pernah percaya, selalu verifikasi). Zero Trust tidak peduli apakah Anda bos besar, menggunakan laptop inventaris kantor, atau sedang duduk di dalam kubikel kantor—sistem akan menganggap Anda sebagai ancaman (musuh) sampai Anda bisa membuktikan sebaliknya melalui proses **Autentikasi (Siapa Anda?)** dan **Autorisasi (Apa hak Anda?)** setiap kali ingin mengakses sesuatu.

Dampaknya, jika terjadi kebocoran data (*data breach*), kerusakannya bisa dilokalisir (dikurung) dan tidak menyebar ke seluruh jaringan perusahaan.

### Contoh Nyata:

> **Skenario Akses Cloud Modern:**
> Meskipun Anda duduk di meja kantor menggunakan laptop perusahaan, saat Anda ingin membuka folder keuangan di Google Drive perusahaan, sistem akan:
> 1. Meminta password Anda.
> 2. Meminta kode MFA (*Multi-Factor Authentication*) dari HP Anda.
> 3. Memeriksa apakah sistem operasi laptop Anda sudah di-update atau belum.
> 
> 
> Jika Anda ingin pindah membuka folder HRD dua menit kemudian, sistem akan melakukan verifikasi ulang. Jaringan luar dan jaringan dalam kantor diperlakukan sama: **sama-sama tidak dipercaya sebelum lolos verifikasi.**

---

## 4. Apa itu Microsegmentation (Mikrosegmentasi)?

### Arti & Maksud:

Tulisan tersebut menyebutkan *Microsegmentation* sebagai salah satu cara menerapkan Zero Trust. Di jaringan model lama, jika peretas berhasil menjebol satu komputer di divisi Marketing, dia bisa melompat ke komputer divisi Finance karena seluruh kantor berada di satu jaringan besar yang sama.

Dengan *Microsegmentation*, jaringan dipecah menjadi bagian-bagian yang sangat kecil (bahkan bisa sekecil satu komputer saja). Antar komputer/bagian ini dipisahkan oleh dinding pembatas digital (Firewall/Access Control List). Untuk bisa berkomunikasi antar komputer, harus ada izin dan autentikasi ketat.

### Contoh Analogi:

> **Analogi Kapal Selam:**
> Bayangkan sebuah kapal selam. Jika seluruh isi kapal adalah satu ruangan besar tanpa sekat, begitu lambung kapal bocor sedikit saja, seluruh kapal akan tenggelam (ini model jaringan lama).
> *Microsegmentation* membuat kapal selam tersebut memiliki banyak **pintu kedap air**. Jika ruangan A bocor (teretas), pintu baja akan menutup otomatis. Ruangan B, C, dan D tetap aman dan kering. Peretas terkunci di ruangan A dan tidak bisa bergerak ke mana-mana.

---

## 5. Kesimpulan Paragraf Terakhir (Batasan Bisnis)

> *“There is a limit to how much we can apply zero trust without negatively impacting a business...”*

Maksudnya adalah, keamanan siber yang terlalu ketat bisa membuat proses bisnis menjadi lambat dan membuat karyawan frustrasi (misalnya jika setiap klik harus memasukkan kode OTP/MFA). Oleh karena itu, praktisi keamanan harus pandai menyeimbangkannya: **Terapkan Zero Trust seketat mungkin, selama hal itu masih masuk akal (feasible) dan tidak membuat roda bisnis perusahaan berhenti berputar.**

---

# 3 PILAR DASAR MANAJEMEN KEAMANAN DIGITAL

Ada tiga pilar paling mendasar dalam manajemen risiko keamanan informasi, yaitu **Vulnerability (Kerentanan)**, **Threat (Ancaman)**, dan **Risk (Risiko)**.

Maksud dan tujuan utama dari teks ini adalah **agar Anda tidak tertukar atau salah memahami ketiga istilah ini**, karena di dunia nyata (termasuk saat Anda menganalisis sistem atau membangun portofolio cybersecurity), ketiga kata ini sering dianggap sama, padahal artinya sangat berbeda namun saling berkaitan.

Berikut adalah penjelasan detail, maksud, tujuan, serta pembedahan contoh dari teks tersebut:

---

## 1. Maksud dari 3 Istilah Utama

Teks tersebut memecah ketiga istilah dengan formula hubungan seperti ini:

> **Risk (Risiko) terjadi jika ada Threat (Ancaman) yang berhasil memanfaatkan Vulnerability (Kerentanan).**

Berikut adalah rinciannya:

* **Vulnerability (Kerentanan / Kelemahan):** Ini adalah cacat, celah, atau kelemahan murni yang ada pada sistem, kode, prosedur, atau fisik. Kerentanan ini sifatnya pasif (belum diapa-apain).
* **Threat (Ancaman):** Ini adalah bahaya potensial yang bisa mengeksploitasi kelemahan tersebut. Ancaman bisa berupa manusia (hacker, kompetitor), alam (gempa bumi), atau program (malware). Sifatnya aktif atau berpotensi aktif.
* **Risk (Risiko):** Ini adalah kalkulasi atau dampak nyata terhadap bisnis. Risiko menghitung **seberapa besar kemungkinan (likelihood)** ancaman itu terjadi dan **seberapa parah dampak kerugiannya (impact)** bagi organisasi jika celah tersebut benar-benar dijebol.

---

## 2. Pembedahan Contoh 1: Showroom Mobil (Skenario Fisik)

Teks memberikan contoh non-teknis agar Anda mudah membayangkan logikanya:

* **Vulnerability:** Showroom mobil menggunakan pintu dan jendela dari **kaca biasa (standar)**. Sifat kaca biasa adalah rapuh dan mudah pecah. Ini adalah kelemahannya.
* **Threat:** Ada ancaman bahwa **kaca tersebut bisa dilempar batu atau dipalu oleh pencuri** hingga hancur.
* **Risk:** Pemilik showroom harus menghitung risikonya.
* *Likelihood (Kemungkinan):* Apakah showroom berada di area rawan kejahatan? Jika ya, kemungkinannya tinggi.
* *Impact (Dampak):* Jika kaca pecah, pencuri bisa masuk dan mobil mewah di dalamnya bisa hilang. Dampak finansialnya sangat besar.

---

## 3. Pembedahan Contoh 2: Database Rumah Sakit (Skenario IT / Cyber)

Ini adalah contoh yang sangat relevan dengan pekerjaan seorang analis keamanan:

* **Vulnerability:** Rumah sakit menggunakan sistem database tertentu untuk menyimpan rekam medis pasien. Suatu hari ditemukan bahwa **database tersebut memiliki celah keamanan (bug pada kode)**.
* **Threat:** Ancaman menjadi sangat nyata ketika di internet dirilis sebuah **Proof-of-Concept (PoC) exploit code** (skrip siap pakai untuk menjebol celah tersebut). Artinya, semua hacker di luar sana sekarang tahu cara memanfaatkan celah itu.
* **Risk:** Sebagai tim IT/Security rumah sakit, Anda harus menghitung risikonya untuk mengambil keputusan:
* *Likelihood:* Karena kodenya sudah disebar di publik, kemungkinan rumah sakit Anda dipindai dan diserang oleh hacker menjadi **sangat tinggi**.
* *Impact:* Jika database dijebol, data rekam medis pasien bisa bocor, rumah sakit bisa dituntut hukum, didenda miliaran, dan reputasinya hancur.

---

## 4. Tujuan dari Memahami Konsep Ini

Tujuan akhir dari memahami tiga istilah ini di dalam room TryHackMe (dan di dunia profesional) adalah untuk **Prioritisasi dan Pengambilan Keputusan (Risk-Based Decision Making)**.

Sebagai seorang profesional, Anda tidak bisa memperbaiki semua *vulnerability* dalam satu malam karena keterbatasan waktu dan biaya. Dengan memahami konsep ini, Anda bisa menghitung skala prioritas:

* Jika ada **Vulnerability** (celah), tapi tidak ada **Threat** (belum ada yang tahu cara eksploitasinya), maka **Risk**-nya **Rendah/Sedang**. Anda bisa memperbaikinya nanti saat jadwal maintenance bulanan.
* Jika ada **Vulnerability**, lalu muncul **Threat** nyata (seperti contoh database rumah sakit di atas di mana kode exploit-nya sudah tersebar luas), maka **Risk**-nya melompat menjadi **Critical/High**. Anda harus melakukan *patching* atau mitigasi darurat **detik itu juga** sebelum sistem Anda dieksploitasi oleh hacker.

---

