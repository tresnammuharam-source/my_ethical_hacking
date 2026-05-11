# MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge)

## Mengenal MITRE ATT&CK

**MITRE ATT&CK** (Adversarial Tactics, Techniques, and Common Knowledge) adalah sebuah basis pengetahuan (knowledge base) yang mendokumentasikan perilaku penyerang siber berdasarkan observasi di dunia nyata. Jika dianalogikan dalam dunia kepolisian, ini adalah kumpulan "Modus Operandi" para kriminal digital yang disusun secara sistematis.

Framework ini menjadi standar industri bagi tim keamanan (Blue Team) untuk memahami cara kerja penyerang dan bagi penguji keamanan (Red Team) untuk mensimulasikan ancaman yang nyata.

---

### 1. Struktur Utama: Taktik, Teknik, dan Prosedur (TTP)

Untuk memahami ATT&CK, kita harus melihat tiga komponen utamanya yang sering disebut sebagai **TTP**:

* **Tactics (Taktik):** Merupakan tujuan strategis penyerang (the "Why"). Mengapa penyerang melakukan tindakan tersebut? Contohnya: *Initial Access* (mendapatkan akses masuk) atau *Exfiltration* (mencuri data).
* **Techniques (Teknik):** Merupakan cara spesifik penyerang mencapai tujuan taktis tersebut (the "How"). Contohnya: Untuk mencapai taktik *Initial Access*, penyerang mungkin menggunakan teknik *Phishing*.
* **Procedures (Prosedur):** Merupakan implementasi spesifik atau langkah demi langkah yang digunakan oleh kelompok penyerang tertentu (APT). Contohnya: "Grup APT28 mengirim email phishing dengan lampiran dokumen Word berbahaya yang mengeksploitasi celah CVE-2017-0199."

---

### 2. Matriks ATT&CK

MITRE membagi basis pengetahuan ini ke dalam beberapa matriks berdasarkan lingkungan target:

1. **Enterprise:** Mencakup sistem operasi tradisional (Windows, macOS, Linux) serta infrastruktur Cloud (AWS, Azure, GCP, Office 365) dan Network.
2. **Mobile:** Berfokus pada ancaman terhadap perangkat Android dan iOS.
3. **ICS (Industrial Control Systems):** Berfokus pada infrastruktur kritis seperti pembangkit listrik atau pabrik.

Di dalam matriks Enterprise, terdapat **14 Taktik** utama yang mengikuti alur serangan dari awal hingga akhir (sering disebut sebagai *Kill Chain*):

| Taktik | Penjelasan Singkat |
| --- | --- |
| **Reconnaissance** | Mengumpulkan informasi untuk merencanakan serangan. |
| **Resource Development** | Menyiapkan infrastruktur (misal: membeli domain, menyewa VPS). |
| **Initial Access** | Mencoba masuk ke dalam jaringan target. |
| **Execution** | Menjalankan kode berbahaya di sistem. |
| **Persistence** | Menjaga akses agar tetap ada meskipun sistem di-reboot. |
| **Privilege Escalation** | Berusaha mendapatkan hak akses yang lebih tinggi (Admin/Root). |
| **Defense Evasion** | Menghindari deteksi oleh antivirus atau EDR. |
| **Credential Access** | Mencuri username dan password. |
| **Discovery** | Menjelajahi lingkungan internal untuk mencari tahu konfigurasi sistem. |
| **Lateral Movement** | Berpindah dari satu komputer ke komputer lain di dalam jaringan. |
| **Collection** | Mengumpulkan data yang menjadi target utama. |
| **Command and Control** | Berkomunikasi dengan sistem yang telah terinfeksi dari jarak jauh. |
| **Exfiltration** | Memindahkan data curian keluar dari jaringan. |
| **Impact** | Merusak, memanipulasi, atau mengganggu operasional sistem. |

---

### 3. Cara Menggunakan MITRE ATT&CK

Ada beberapa alat dan metode yang biasa digunakan untuk berinteraksi dengan framework ini:

* **ATT&CK Navigator:** Alat berbasis web yang memungkinkan kita memvisualisasikan matriks, memberi warna pada teknik tertentu, dan memetakan pertahanan yang kita miliki terhadap teknik penyerang.
* **Groups & Software:** MITRE menyediakan daftar kelompok penyerang (misal: APT41, Lazarus Group) dan perangkat lunak/malware yang mereka gunakan. Ini membantu tim keamanan melakukan *Threat Profiling*.
* **Mitigations & Detection:** Setiap teknik di MITRE disertai dengan saran cara mencegahnya (*Mitigation*) dan cara mendeteksinya (*Detection data sources*).

---

### 4. Contoh Kasus (Scenario)

Bayangkan sebuah insiden di mana seorang karyawan menerima email palsu dan mengklik link yang mengunduh file `.exe`.

1. **Taktik:** *Initial Access* -> **Teknik:** *Phishing* (Spearphishing Link).
2. **Taktik:** *Execution* -> **Teknik:** *User Execution* (Karyawan menjalankan file tersebut).
3. **Taktik:** *Persistence* -> **Teknik:** *Registry Run Keys* (Malware mendaftarkan diri di registry agar otomatis jalan saat PC menyala).

Dengan memetakan insiden ke dalam MITRE ATT&CK, tim SOC (Security Operations Center) dapat dengan mudah mengomunikasikan celah mana yang perlu diperbaiki dan log apa yang perlu dipantau di masa depan.

---

# Materi MITRE ATT&CK di TryHackMe

Untuk memberikan penjelasan yang benar-benar menyerupai struktur *room* di **TryHackMe**, saya akan membaginya berdasarkan **Tasks** utama yang biasanya dipelajari di sana. Materi ini disusun agar kamu bisa memahami konsepnya secara sistematis, mirip dengan alur belajar di platform tersebut.

---

### Task 1: Introduction to MITRE ATT&CK

Pada tahap ini, kamu diperkenalkan pada fundamental framework.

* **Apa itu?** Sebuah basis pengetahuan global yang mendokumentasikan perilaku penyerang (adversary) berdasarkan kejadian nyata.
* **Tujuan:** Memberikan bahasa yang sama bagi praktisi keamanan di seluruh dunia untuk mendiskusikan ancaman.
* **Poin Penting:** ATT&CK bukan sekadar daftar malware, melainkan daftar **tindakan** yang diambil penyerang untuk mencapai tujuan mereka.

### Task 2: Tactics, Techniques, and Sub-Techniques

Ini adalah inti dari matriks MITRE.

* **Tactics (Taktik):** Tujuan jangka pendek penyerang (Contoh: *Initial Access*). Ada 14 taktik dalam matriks Enterprise.
* **Techniques (Teknik):** Cara spesifik untuk mencapai taktik (Contoh: Di bawah *Initial Access*, ada teknik *Phishing*).
* **Sub-Techniques:** Memberikan detail yang lebih spesifik lagi.
* *Contoh:* **T1566** adalah *Phishing*, sedangkan **T1566.001** adalah *Spearphishing Attachment*.
* *Tips THM:* Perhatikan format ID teknik yang selalu diawali huruf **T** diikuti 4 angka.



### Task 3: MITRE ATT&CK Matrix

Di sini kamu belajar cara membaca tabel besar yang sering kamu lihat di situs MITRE.

* Matriks ini dibaca dari **kiri ke kanan** sesuai alur serangan (*Adversary Lifecycle*).
* Kolom paling atas adalah **Taktik**, dan di bawahnya terdapat daftar **Teknik** yang relevan.
* **Key Concept:** Penyerang tidak perlu menggunakan semua taktik. Mereka mungkin meloncat dari satu taktik ke taktik lain sesuai kebutuhan di lapangan.

### Task 4: Groups and Software

MITRE tidak hanya mendokumentasikan "cara kerja" tapi juga "siapa" dan "alat apa".

* **Groups:** Profil dari kelompok APT (*Advanced Persistent Threat*) atau kelompok kriminal siber. Contoh: **APT28** atau **Lazarus Group**. Kamu bisa melihat teknik apa saja yang *biasanya* mereka gunakan.
* **Software:** Daftar alat (tool), malware, atau script yang digunakan oleh penyerang. Contoh: **Empire**, **Cobalt Strike**, atau bahkan perintah bawaan OS seperti **Net.exe**.

### Task 5: ATT&CK Navigator

Ini adalah alat visualisasi utama yang sering muncul di soal-soal TryHackMe.

* **Fungsi:** Membuat "layer" atau peta serangan.
* **Kegunaan:**
* Memetakan kapabilitas deteksi internal.
* Membandingkan dua kelompok penyerang yang berbeda (misalnya membandingkan teknik APT1 vs APT29).
* Merencanakan simulasi serangan (Red Teaming).

### Task 6: Mitigations and Detection

Bagaimana cara melawan teknik-teknik tersebut?

* **Mitigations:** Langkah pencegahan untuk menghalangi teknik agar tidak berhasil (Contoh: Menggunakan *Antivirus* atau *User Account Control*).
* **Detection:** Menjelaskan data apa yang perlu dikumpulkan (Log, Network Traffic, Process Monitoring) untuk mendeteksi jika suatu teknik sedang digunakan.

### Task 7: Real-World Scenario (Practical Application)

Biasanya di Task terakhir, kamu diminta melakukan analisis terhadap laporan intelijen ancaman (*Cyber Threat Intelligence*).

* **Langkah Analisis:**
1. Baca laporan serangan.
2. Identifikasi tindakan penyerang (misal: "Penyerang mengirim email dengan dokumen makro").
3. Cari di situs MITRE teknik yang sesuai (misal: *Phishing: Spearphishing Attachment*).
4. Catat ID Tekniknya (**T1566.001**).

---

> **Pro Tip untuk Lab:** Jika kamu sedang mengerjakan lab di TryHackMe, sering-kali jawaban dari pertanyaan "What is the technique ID..." bisa ditemukan dengan mencari kata kunci di kotak pencarian (search bar) pada situs resmi **attack.mitre.org**.

Apakah ada Task spesifik atau bagian dari matriks ini yang ingin kamu bedah lebih dalam untuk persiapan sertifikasi atau portofolio kamu?

---

# Cara melakukan Analisa Laporan Intelejen Ancaman (Cyber Threat Intelligence)

Untuk melakukan analisis terhadap laporan intelijen ancaman (*Cyber Threat Intelligence*), alat utama yang paling sering digunakan dan muncul di materi TryHackMe adalah **MITRE ATT&CK Navigator**.

Berikut adalah panduan langkah demi langkah untuk mengakses, menggunakan, dan mengunduh data dari sana:

---

### 1. Akses ke Web Utama

Ada dua alamat penting yang perlu kamu ketahui:

* **Knowledge Base (Utama):** [attack.mitre.org](https://attack.mitre.org/) – Tempat mencari detail teknik, grup APT, dan software.
* **Analisis Tool (Navigator):** [mitre-attack.github.io/attack-navigator/](https://mitre-attack.github.io/attack-navigator/) – Tempat untuk memetakan laporan ancaman secara visual.

---

### 2. Panduan Analisis Laporan (Mapping)

Jika kamu memiliki laporan intelijen (misalnya artikel blog tentang serangan malware baru), ikuti langkah ini:

#### **A. Persiapan di Navigator**

1. Buka [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/).
2. Pilih **"Create New Layer"** dan klik **"Enterprise"** (untuk serangan berbasis Windows/Linux/Cloud).
3. Berikan nama pada layer kamu (misal: "Analisis Malware X") melalui ikon *Selection Controls* di atas.

#### **B. Mencari dan Menandai Teknik**

1. Baca laporan intelijen kamu. Temukan kata kunci perilaku penyerang (contoh: "Penyerang menghapus shadow copies untuk mencegah recovery").
2. Di Navigator, klik ikon **Kaca Pembesar (Search)**.
3. Ketik kata kunci atau ID teknik (misal: `T1490` untuk *Inhibit System Recovery*).
4. Klik teknik yang muncul, lalu gunakan ikon **Cat (Background Color)** untuk memberi warna pada kotak tersebut di matriks. Ini menandakan bahwa teknik tersebut ditemukan dalam laporan.

---

### 3. Mengunduh dan Menyimpan Hasil Analisis

Setelah selesai memetakan semua teknik dari laporan, kamu bisa mengunduhnya untuk keperluan portofolio atau laporan tim:

* **Download sebagai JSON:** Klik ikon **Download (Render layer to JSON)**. File ini bisa kamu simpan dan buka kembali di Navigator kapan saja.
* **Download sebagai Gambar (SVG):** Klik ikon **Kamera (Export to SVG)** jika ingin memasukkan visualisasi matriks ke dalam dokumen Word atau presentasi.
* **Download sebagai Excel:** Klik ikon **Excel (Export to Excel)**. Ini sangat berguna jika kamu ingin membuat daftar teknik secara tabular untuk diolah dengan Power Query atau SQL (seperti yang biasa kamu lakukan di pekerjaan).

---

### 4. Alat Bantu Otomasi: TRAM (Threat Report ATT&CK Mapper)

Jika laporan kamu berbentuk teks panjang dan kamu ingin bantuan AI untuk memetakannya:

* MITRE memiliki proyek bernama **TRAM** (tersedia di [GitHub MITRE](https://github.com/center-for-threat-informed-defense/tram)).
* TRAM menggunakan *Natural Language Processing* (NLP) untuk membaca teks laporan dan memberikan sugesti teknik ATT&CK mana yang paling relevan.

**Tips Tambahan:**
Karena kamu sedang membangun portofolio di GitHub, hasil analisis dari Navigator (file SVG dan JSON) sangat bagus untuk diunggah sebagai bukti kemampuan kamu dalam melakukan *Threat Mapping*.

Apakah ada laporan atau teknik tertentu yang saat ini sedang kamu coba petakan?

---

# Contoh Laporan Injelejen Ancaman yang kamu harus mencobanya

Sebagai pemula yang sedang meniti karier menuju SOC Analyst atau Penetration Tester, cara terbaik untuk belajar adalah dengan menganalisis laporan yang mendokumentasikan serangan nyata secara runtut.

Berikut adalah rekomendasi laporan dan teknik yang sangat ideal untuk dianalisis karena strukturnya yang jelas dan relevansinya yang tinggi di dunia kerja:

---

### 1. Laporan Utama: The DFIR Report

**The DFIR Report** adalah sumber terbaik karena mereka menyajikan laporan kasus nyata (case studies) lengkap dengan pemetaan teknik MITRE ATT&CK di setiap tahapannya.

* **Rekomendasi Laporan:** Cari laporan tentang **"Bumblebee Malware"** atau **"IcedID to Quantum Ransomware"**.
* **Kenapa ini bagus?** Mereka menjelaskan alur dari *Initial Access* hingga *Impact* (Ransomware) disertai dengan log perintah (command line) yang digunakan penyerang. Ini sangat berguna untuk latihan analisis Linux CLI atau Windows PowerShell.
* **Dimana membacanya?** Kunjungi [thedfirreport.com](https://thedfirreport.com/).

### 2. Teknik Dasar yang Wajib Dianalisis

Sebagai pemula, jangan mencoba menganalisis teknik yang terlalu kompleks. Fokuslah pada teknik "Low-Hanging Fruit" yang paling sering digunakan:

* **T1566.001 (Phishing: Spearphishing Attachment):** Pelajari bagaimana penyerang menyisipkan file LNK, ISO, atau dokumen macro untuk masuk ke sistem.
* **T1059.001 (Command and Scripting Interpreter: PowerShell):** Analisis bagaimana perintah PowerShell digunakan untuk mengunduh malware tambahan (*stager*).
* **T1003.001 (OS Credential Dumping: LSASS Memory):** Teknik klasik untuk mencuri password dari memori komputer yang terinfeksi.
* **T1021.001 (Remote Services: Remote Desktop Protocol):** Pelajari bagaimana penyerang berpindah antar komputer (*Lateral Movement*) menggunakan RDP.

### 3. Red Canary: Threat Detection Report

Red Canary menerbitkan laporan tahunan yang merangkum teknik apa saja yang paling banyak digunakan oleh penyerang di seluruh dunia.

* **Rekomendasi:** Baca **"Top 10 Techniques"** dari laporan terbaru mereka.
* **Kenapa ini bagus?** Setiap teknik dijelaskan secara mendalam: mengapa penyerang menyukainya, cara mendeteksinya, dan cara mengujinya.
* **Dimana membacanya?** Kunjungi [redcanary.com/threat-detection-report/](https://redcanary.com/threat-detection-report/).

### 4. Analisis Kelompok APT (Advanced Persistent Threat)

Memahami profil kelompok tertentu akan membantu kamu berpikir seperti "Hunter".

* **Rekomendasi Kelompok:** **APT29 (Cozy Bear)** atau **Lazarus Group**.
* **Dimana membacanya?** Langsung di situs MITRE ATT&CK: [attack.mitre.org/groups/](https://attack.mitre.org/groups/). Cari "APT29", lalu scroll ke bawah ke bagian **"Techniques Used"**.

---

### Langkah Praktis untuk Kamu:

1. **Unduh satu laporan** dari *The DFIR Report*.
2. **Buka MITRE ATT&CK Navigator** di tab sebelah.
3. **Lakukan "Mapping" secara manual**: Setiap kali laporan menyebutkan tindakan penyerang (misal: "Penyerang menjalankan `whoami` untuk melihat user"), cari tekniknya di MITRE (T1033 - *System Owner/User Discovery*) dan beri warna di Navigator.
4. **Simpan hasilnya sebagai JSON/SVG** dan masukkan ke dalam portofolio GitHub kamu sebagai bukti latihan *Threat Mapping*.

Langkah ini akan sangat membantu memperkuat profil kamu saat melamar posisi SOC Analyst nanti. Ingin saya bantu membedah satu teknik spesifik dari daftar di atas?

---

# Tools untuk melakukan Review Laporan Intelejen Ancaman

Untuk melakukan review laporan intelijen ancaman secara profesional—seperti yang dilakukan analis SOC—kamu membutuhkan metode untuk mengekstrak informasi penting sebelum memasukkannya ke MITRE ATT&CK Navigator.

Berikut adalah alat dan prosedur yang bisa kamu gunakan:

### 1. Alat untuk Melakukan Review Laporan

Ada tiga tingkat alat yang bisa kamu gunakan, tergantung pada preferensi kerjamu:

* **Tingkat Dasar: Browser Extension (Hypothesis)**
* Alat seperti **Hypothesis** atau **Memex** memungkinkan kamu menandai (highlight) teks langsung di website laporan dan memberikan catatan di pinggir halaman.


* **Tingkat Menengah: Obsidian atau Notion (Zettelkasten Method)**
* Sangat disarankan untuk kamu yang sedang membangun portofolio. Kamu menyalin isi laporan ke Obsidian, lalu menggunakan Markdown untuk menandai bagian penting. Obsidian memiliki plugin MITRE ATT&CK yang bisa menghubungkan teks langsung ke database MITRE.


* **Tingkat Profesional: TRAM (Threat Report ATT&CK Mapper)**
* Ini adalah alat bantu berbasis AI/ML dari MITRE. Kamu memasukkan teks laporan, dan TRAM akan secara otomatis menyoroti kalimat yang terdeteksi sebagai teknik ATT&CK.



---

### 2. Cara Melakukan Penandaan (Metode Analisis)

Gunakan teknik **"Color Coding"** saat membaca laporan untuk membedakan elemen-elemen penting:

| Warna / Tanda | Kategori Informasi | Contoh dari Laporan |
| --- | --- | --- |
| **Merah / Bold** | **Technique (TTPs)** | "Penyerang menggunakan *Schtasks* untuk jadwal rutin." |
| **Biru / Underline** | **Indicators (IoC)** | Alamat IP `192.168.1.50` atau hash file `a5f1...` |
| **Hijau** | **Tools / Software** | "Menggunakan *Mimikatz* untuk mencuri password." |
| **Kuning** | **Infrastructure** | "Koneksi menuju server *C2* di domain `update-windows.com`." |

---

### 3. Langkah-Langkah (Workflow) Analisis

Jika kamu ingin mempraktekkannya sekarang, ikuti alur kerja ini:

#### **Langkah 1: Ekstraksi Teks**

Copy teks dari laporan (misal dari *The DFIR Report*) ke aplikasi catatan (Notion/Obsidian) atau cetak ke PDF.

#### **Langkah 2: Pencarian Kata Kerja (Action-Oriented)**

Fokus pada **kata kerja**. MITRE ATT&CK adalah tentang perilaku.

* *Laporan:* "The adversary **executed** a base64 encoded **PowerShell** script."
* *Analisa:* Kata "Executed PowerShell" langsung mengarah ke teknik **T1059.001**.

#### **Langkah 3: Mapping ke Navigator**

1. Buka **ATT&CK Navigator**.
2. Setiap kali kamu menemukan satu teknik di laporan, cari ID-nya di web [attack.mitre.org](https://attack.mitre.org).
3. Di Navigator, pilih kotak teknik tersebut.
4. Gunakan fitur **"Score"** atau **"Color"**:
* Klik ikon cat (Background Color).
* Berikan warna (misal: Merah untuk teknik yang berhasil dilakukan penyerang).


5. Tambahkan **Comment**: Klik kanan pada kotak di Navigator -> *Edit Comment*. Masukkan potongan kalimat dari laporan sebagai bukti.

#### **Langkah 4: Dokumentasi Portofolio**

Setelah matriks di Navigator penuh dengan warna hasil analisismu:

1. Ekspor sebagai **SVG** (gambar).
2. Screenshot laporan yang sudah kamu tandai (highlight).
3. Tulis penjelasan singkat di GitHub: *"Saya menganalisis laporan insiden X, mengidentifikasi 5 teknik utama, dan memetakannya ke dalam matriks MITRE untuk memahami alur serangan."*

### Tips Tambahan:

Jika kamu ingin mencoba alat otomatis, kamu bisa mencari **"ATT&CK Powered Search"** (extension Chrome). Saat kamu membaca laporan di web, kamu bisa blok teksnya, dan extension ini akan langsung mencarikan teknik MITRE yang relevan.

Apakah kamu ingin mencoba membedah satu paragraf contoh laporan bersama saya sekarang?
