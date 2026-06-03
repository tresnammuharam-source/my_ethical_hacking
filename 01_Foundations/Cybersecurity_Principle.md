# PRINSIP-PRINSIP CYBERSECURITY

---

# 2 PRINSIP CYBERSECURITY

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

# IMPACT of Cybersecurity Training

Dibagian ini kita akan membahas tentang **pentingnya pelatihan (*training*) dan simulasi laboratorium dalam dunia keamanan siber (*cybersecurity*)**, baik dari sudut pandang individu (Anda sebagai pembelajar) maupun dari sudut pandang organisasi/perusahaan.

Maksud utama dari teks ini adalah menjelaskan **mengapa platform seperti TryHackMe sangat krusial** dan mengapa belajar *cybersecurity* tidak bisa hanya dengan membaca teori, melainkan harus dipraktikkan di lingkungan yang aman.

Berikut adalah penjelasan detail mengenai poin-poin penting dari teks tersebut:

---

## 1. Belajar *Cybersecurity* Butuh Tempat Praktik yang Aman

> *“...practising what you learn in cyber security has certain requirements. Example: it usually involves setting up a computer lab environment...”*

**Maksudnya:** Untuk menguasai keahlian *hacking* atau pertahanan jaringan, Anda harus mempraktikkannya. Namun, Anda tidak boleh sembarangan mempraktikkan ilmu *hacking* di internet publik atau di jaringan kantor/sekolah karena bisa merusak sistem nyata (produksi) dan berurusan dengan hukum.

Oleh karena itu, Anda butuh **Platform Pelatihan (seperti TryHackMe)**. Platform ini menyediakan laboratorium virtual (lab komputer tiruan) yang terisolasi. Anda bisa bebas mencoba mengeksploitasi celah keamanan atau bertahan tanpa takut merusak apa pun.

---

## 2. Lebih Baik Gagal di Lab daripada Gagal saat Diserang Sungguhan

> *“An ounce of prevention is worth a pound of cure... it is better to learn in a training environment than during a live incident.”*

**Maksudnya:** Pepatah tersebut berarti *"Mencegah lebih baik daripada mengobati"*.
Dalam dunia nyata, sangat berbahaya jika tim IT baru belajar cara menangani *malware* atau serangan *hacker* **di tengah-tengah peristiwa serangan asli** yang sedang melanda perusahaan. Hal itu akan memicu kepanikan dan kerugian besar. Melalui lab pelatihan, tim bisa melakukan kesalahan, belajar dari kesalahan tersebut, dan siap ketika serangan asli benar-benar terjadi.

---

## 3. Manfaat bagi Perusahaan (Efisiensi & Rekrutmen)

Teks tersebut menjelaskan keuntungan besar bagi perusahaan yang menyediakan pelatihan terpusat bagi karyawannya:

* **Meningkatkan Kapasitas Tanpa Menambah Karyawan:** Karyawan yang terlatih akan bekerja lebih cepat dan efisien. Mereka tahu alat (*tools*) apa yang harus digunakan, sehingga perusahaan tidak perlu merekrut orang baru hanya untuk menyelesaikan satu masalah.
* **Mempermudah Perekrutan Tenaga Junior:** Perusahaan tidak perlu selalu mencari tenaga senior yang mahal. Mereka bisa merekrut orang baru (*junior*), lalu memanfaatkan platform pelatihan untuk mendidik mereka dengan cepat (*ramp up*). Ini juga menghemat waktu staf senior agar tidak perlu mengajarkan hal dasar yang sama berulang-ulang.

---

## 4. Standarisasi Kemampuan Karyawan (Common Baseline)

> *“Instead of vague terms like “junior” or “senior,” employees’ skills can be described more specifically.”*

**Maksudnya:** Di banyak perusahaan, istilah "Junior" atau "Senior" itu sangat abu-abu (vague). Orang yang dianggap senior di perusahaan A belum tentu senior di perusahaan B.

Dengan adanya platform pelatihan yang terpusat, perusahaan memiliki **tolok ukur (baseline) yang jelas**. Contohnya: *"Karyawan A sudah menyelesaikan modul Pentesting Web di TryHackMe, sedangkan Karyawan B baru menyelesaikan modul Dasar Jaringan."* Dengan data spesifik ini, manajer bisa lebih tepat membagikan tugas sesuai keahlian nyata karyawannya.

---

## 5. Membangun Kerja Sama Tim Lewat CTF (Capture The Flag)

> *“...the experience of being part of a team playing a CTF (Capture the Flag) challenge builds incredible friendships...”*

**Maksudnya:** Pelatihan *cybersecurity* tidak harus selalu membosankan. Salah satu metodenya adalah dengan kompetisi **CTF (Capture The Flag)**, yaitu permainan simulasi di mana tim Anda harus berlomba mencari celah keamanan untuk mendapatkan "bendera" (kode rahasia). Kompetisi seperti ini melatih kerja sama tim, komunikasi, dan membangun ikatan pertemanan yang kuat. Hubungan baik ini akan sangat membantu saat mereka harus bahu-membahu mengatasi insiden keamanan yang penuh tekanan di dunia nyata.

---

## Kesimpulan / Rangkuman:

Tujuan dari teks ini di dalam room TryHackMe adalah untuk **memotivasi Anda**. Teks ini meyakinkan Anda bahwa tidak ada orang yang langsung lahir sebagai ahli *cybersecurity*. Kuncinya adalah latihan yang tekun di lingkungan lab yang tepat, dan investasi waktu Anda untuk belajar di platform ini akan sangat dihargai tinggi oleh industri dan perusahaan di masa depan.

---
## on company scale

**bagaimana perusahaan dengan skala yang berbeda memilih dan mengintegrasikan platform pelatihan *cybersecurity* (seperti TryHackMe)** agar sesuai dengan kebutuhan operasional mereka.

Teks ini membagi solusinya ke dalam dua fokus utama: **Kustomisasi Materi** (berdasarkan ukuran tim) dan **Integrasi Sistem** (untuk perusahaan skala besar/korporasi).

Berikut adalah penjelasan detail mengenai maksud dan tujuan dari masing-masing poin tersebut:

---

## 1. Pemilihan Pelatihan Berdasarkan Ukuran Tim

Teks ini memberikan panduan logis bagi perusahaan dalam memilih metode pelatihan:

* **Tim Kecil (Di bawah 20 orang):** Disarankan menggunakan **"Off-the-shelf training"** (pelatihan siap pakai). Maksudnya adalah materi, modul, dan *room* standar yang sudah disediakan langsung oleh TryHackMe tanpa perlu diubah-ubah. Ini lebih hemat waktu dan biaya untuk tim berskala kecil.
* **Tim Besar (Di atas 20 orang atau Kebutuhan Khusus):** Disarankan untuk melakukan **Kustomisasi (Penyesuaian)**. Mengapa? Karena setiap perusahaan memiliki infrastruktur teknologi dan ancaman yang berbeda.

### Solusi TryHackMe: "Content Studio"

Untuk memfasilitasi tim besar tersebut, TryHackMe menyediakan fitur bernama **Content Studio**.

* **Maksudnya:** Fitur ini memungkinkan tim internal perusahaan (misalnya manajer IT atau Security Lead) untuk mengubah *room* yang sudah ada atau bahkan **membuat modul/soal simulasi sendiri dari nol** yang mirip dengan sistem asli perusahaan mereka.
* **Tujuannya:** Meningkatkan efektivitas (*efficacy*) pelatihan. Karyawan tidak lagi belajar teori umum, melainkan langsung berlatih menghadapi simulasi sistem yang benar-benar akan mereka pegang di tempat kerja.

---

## 2. Kebutuhan Integrasi Teknologi untuk Korporasi Besar (Large Corporations)

Bagi perusahaan raksasa (Korporasi), membeli lisensi pelatihan saja tidak cukup. Mereka tidak ingin platform pelatihan tersebut berdiri sendiri (*standalone*) dan merepotkan tim IT dalam mengelolanya. Mereka butuh dua teknologi utama:

### A. Dukungan SSO (Single Sign-On)

* **Maksudnya:** SSO adalah teknologi yang memungkinkan karyawan masuk ke banyak aplikasi hanya dengan **satu akun dan satu password** (misalnya menggunakan akun Google Workspace Perusahaan, Microsoft Azure AD, atau Okta).
* **Tujuannya:** Karyawan tidak perlu membuat akun dan menghafal password baru lagi khusus untuk TryHackMe. Ketika mereka *login* menggunakan email kantor, mereka langsung otomatis masuk ke platform pelatihan. Ini sangat mempermudah manajemen akun bagi tim IT.

### B. Dokumentasi API (Application Programming Interface) yang Baik

* **Maksudnya:** API adalah "jembatan" yang menghubungkan dua aplikasi berbeda agar bisa saling mengobrol dan bertukar data secara otomatis.
* **Tujuannya:** Dengan API, tim HRD atau Direktur Keamanan bisa menarik data nilai, progres latihan, dan sertifikat karyawan dari TryHackMe secara otomatis untuk dimasukkan ke dalam dasbor internal perusahaan atau sistem penilaian kinerja karyawan (LMS - *Learning Management System*).

---

## Kesimpulan / Rangkuman:

Maksud dari tulisan ini adalah menunjukkan bahwa **TryHackMe tidak hanya dirancang untuk individu yang belajar mandiri, tetapi juga memiliki fitur tingkat tinggi (Enterprise)**.

Platform ini bisa fleksibel: menjadi tempat belajar siap pakai yang instan untuk tim kecil, menjadi wadah pembuat modul kustom (*Content Studio*) untuk tim besar, dan bisa menyatu secara otomatis dengan sistem keamanan IT perusahaan melalui SSO dan API.

---

# CARA MENGHITUNG KEUNTUNGAN DARI PELATIHAN

Tulisan yang Anda bagikan membahas tentang **bagaimana cara menghitung dampak finansial dari pelatihan karyawan (Return on Investment - ROI)** agar Anda bisa meyakinkan manajemen atau perusahaan tempat Anda bekerja untuk memberikan anggaran (*budget*) pelatihan.

Perusahaan yang pintar akan melihat karyawan sebagai aset. Namun, untuk meminta anggaran pelatihan kepada atasan, Anda tidak bisa hanya bilang *"Pelatihan ini bagus"*. Anda harus berbicara menggunakan angka (data finansial) agar mereka tertarik.

Berikut adalah penjelasan logika perhitungan dari teks tersebut, diikuti dengan jawaban langsung untuk soal skenario di bagian bawah:

---

## 1. Memahami Logika Perhitungan Rumus

Teks tersebut memberikan contoh matematika sederhana untuk menghitung **Penghematan/Keuntungan (Savings/Gains)** yang didapat perusahaan dari peningkatan produktivitas kerja setelah karyawan dilatih.

* **Rumus Keuntungan Produktivitas:**

$$\text{Jumlah Karyawan} \times \text{Persentase Peningkatan Produktivitas} \times \text{Gaji Tahunan per Karyawan}$$


* **Return on Investment (ROI):**

$$\frac{\text{Total Keuntungan}}{\text{Total Biaya Pelatihan}} \times 100\%$$



Di contoh pertama teks tersebut:

* 10 karyawan $\times$ 4% produktivitas $\times$ $\$80.000$ gaji = **$\$32.000$ keuntungan perusahaan**.
* Biaya pelatihan cuma $\$5.000$.
* Maka ROI-nya sangat tinggi yaitu **640%**. Angka inilah yang dipakai untuk meyakinkan bos.

---

## 2. Jawaban untuk Pertanyaan Skenario di Akhir Teks

Mari kita hitung pertanyaan di bagian bawah sesuai dengan data skenario baru yang diberikan:

* **Jumlah Karyawan (Employees):** 20 orang
* **Gaji Tahunan per Karyawan (Cost):** $\$50.000$
* **Peningkatan Produktivitas (Assumption):** 4% (atau 0,04 dalam desimal)

### Jalur Perhitungannya:

1. Hitung total biaya gaji seluruh tim dalam setahun:
$$20 \times \$50.000 = \$1.000.000$$


2. Hitung nilai penghematan dari peningkatan produktivitas 4% tersebut:
$$\$1.000.000 \times 4\% = \$40.000$$



Atau menggunakan rumus langsung:


$$\text{Savings} = 20 \times 0.04 \times \$50.000 = \$40.000$$

---

### Jawaban untuk diinput ke kolom TryHackMe:

**40000** (atau jika meminta format mata uang: **$40,000**)

---

