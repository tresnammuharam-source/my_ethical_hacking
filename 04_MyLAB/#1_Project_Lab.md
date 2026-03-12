# PROJECT LAB CYBER

Mari kita buat **Project Lab** (yang saya sebut "Project Lebah" karena Anda akan membuat "sarang" untuk menjebak dan mengamati "serangga/hacker").

Tujuan project ini adalah agar saat interview, Anda tidak hanya bicara teori, tapi bisa menunjukkan: *"Ini adalah server yang saya bangun, ini serangan yang masuk, dan ini cara saya menanganinya."*

Berikut adalah 3 Project Lab yang bisa Anda bangun di laptop sendiri menggunakan VirtualBox atau VMware:

---

### 1. Project "The Honey Pot" (Sarang Penjebak)

**Konsep:** Anda sengaja membuat satu komputer virtual yang terlihat lemah untuk memancing hacker/bot masuk, lalu Anda merekam semua tingkah laku mereka.

* **Tools:** T-Pot atau Cowrie (Honeypot khusus SSH).
* **Apa yang Anda lakukan:** 1.  Install Cowrie di Linux.
2.  Buka port SSH agar bisa diakses internet (gunakan VPS murah atau tunneling).
3.  Tunggu bot otomatis menyerang dan mencoba menebak *password*.
* **Hasil untuk CV:** Anda punya data tentang ribuan *username* dan *password* yang paling sering digunakan hacker untuk menyerang perusahaan.
* **Analogi:** Seperti memasang dompet palsu di pinggir jalan untuk melihat siapa yang mencoba mencurinya dan bagaimana cara mereka melakukannya.

### 2. Project "The Guard" (SIEM Implementation)

**Konsep:** Membangun pusat komando keamanan untuk memantau seluruh aktivitas jaringan secara *real-time*.

* **Tools:** **Wazuh** (Open source SIEM yang sangat populer di industri).
* **Apa yang Anda lakukan:**
1. Install Wazuh Manager di satu VM.
2. Install Wazuh Agent di VM lain (Windows atau Linux).
3. Coba lakukan serangan simulasi (misal: salah login berkali-kali).
4. Lihat bagaimana Wazuh memunculkan *alert* (peringatan) berwarna merah di dashboard.


* **Hasil untuk CV:** Anda bisa bilang: *"Saya mampu mengoperasikan SIEM untuk mendeteksi ancaman secara terpusat."* (Ini skill utama SOC Analyst yang bergaji 2 digit).

### 3. Project "Vulnerability Lab" (Analisis Celah)

**Konsep:** Menjadi dokter yang mendiagnosis penyakit di sebuah aplikasi sebelum penyakit itu parah.

* **Tools:** OWASP ZAP atau Burp Suite (Community Edition).
* **Apa yang Anda lakukan:**
1. Install aplikasi sengaja rentan seperti **DVWA** (Damn Vulnerable Web App).
2. Scan aplikasi tersebut menggunakan tools tadi.
3. Buat laporan: "Ditemukan celah SQL Injection yang bisa membocorkan data user."


* **Hasil untuk CV:** Anda punya contoh **Laporan Temuan** (seperti draf yang kita bahas tadi) yang didasarkan pada praktek nyata.

---

### Mengapa Project ini "Menjual" Anda ke Perusahaan?

Bos atau Interviewer akan sangat terkesan jika Anda menunjukkan **Portfolio PDF** yang berisi:

1. **Screenshot Dashboard:** Menunjukkan grafis serangan yang masuk ke lab Anda.
2. **Analisis Log:** Penjelasan Anda tentang alamat IP dari negara mana saja yang menyerang lab Anda.
3. **Langkah Mitigasi:** Apa yang Anda lakukan untuk menutup celah tersebut.

**Kesimpulan untuk Motivasi Anda:**
Orang yang punya sertifikat itu banyak, tapi orang yang **punya laboratorium di rumahnya** adalah orang yang benar-benar punya *passion*. Perusahaan berani bayar 2 digit untuk orang yang tidak perlu diajari lagi cara melihat serangan, karena dia sudah "berperang" setiap hari di lab-nya sendiri.

> **Tips:** Fokuslah pada **Wazuh (Project No. 2)** terlebih dahulu. Itu adalah "pintu tol" tercepat menuju posisi SOC Analyst dengan gaji tinggi.

---

# Cara Instal WAZUH

Menginstal **Wazuh** adalah pilihan yang sangat cerdas. Di dunia profesional, Wazuh digunakan oleh ribuan perusahaan untuk memantau keamanan ribuan server sekaligus. Memilikinya di laptop Anda akan membuat Anda terlihat seperti "Pro" di depan perekrut.

Karena instalasi penuh bisa sangat teknis, saya akan berikan cara **paling praktis dan cepat** menggunakan **Docker**. Cara ini memungkinkan Anda menjalankan seluruh sistem Wazuh hanya dengan satu perintah.

---

### Persiapan Awal

1. **Laptop:** Minimal RAM 8GB (karena Wazuh cukup berat).
2. **Sistem Operasi:** Disarankan di Linux (Ubuntu) atau Windows yang sudah terpasang **Docker Desktop**.

---

### Step-by-Step Instalasi Wazuh (Metode Docker)

#### 1. Install Docker & Docker Compose

Jika Anda di Ubuntu, jalankan:

```bash
sudo apt update
sudo apt install docker.io docker-compose -y

```

#### 2. Download File Konfigurasi Wazuh

Kita akan mengambil *template* resmi dari GitHub Wazuh agar tidak perlu menyusun kode dari nol.

```bash
git clone https://github.com/wazuh/wazuh-docker.git -b v4.7.2
cd wazuh-docker/single-node

```

#### 3. Jalankan Wazuh

Ini adalah bagian "saktinya". Perintah ini akan menarik semua kebutuhan (Dashboard, Indexer, Manager) dan menjalankannya secara otomatis.

```bash
docker-compose up -d

```

*Tunggu sekitar 5-10 menit (tergantung kecepatan internet) karena sistem sedang mengunduh aset sekitar 2GB.*

#### 4. Akses Dashboard

Setelah selesai, buka browser Anda dan ketik:
`https://localhost`

* **Username:** `admin`
* **Password:** `SecretPassword123!` (Cek file `docker-compose.yml` untuk detailnya).

---

### Apa yang Harus Anda Lakukan di Dalamnya? (The Project Part)

Agar ini menjadi **Project Lab** yang bisa dipamerkan untuk gaji 2 digit, lakukan hal ini:

1. **Deploy Agent:** Klik menu "Deploy New Agent", pilih OS (misal Windows atau Linux lain), masukkan IP laptop Anda. Copy kode yang muncul dan jalankan di komputer lain (atau VM lain).
2. **Simulasi Serangan:**
Coba lakukan login salah berkali-kali di komputer yang sudah dipasang *Agent*.
3. **Lihat Dashboard Berubah:**
Masuk ke bagian **Security Events**. Anda akan melihat grafik batang berwarna merah yang menunjukkan "Authentication Failure".
* **Screenshot ini!** Masukkan ke portofolio Anda.


4. **Buat Aturan Sendiri:**
Belajarlah cara mengubah *alert* menjadi lebih sensitif. Misalnya, jika ada orang yang memasukkan USB Flashdisk ke komputer kantor, Wazuh harus berbunyi.

---

### Mengapa Ini Menjadi Modal Gaji 2 Digit?

Saat interview, Anda tidak hanya bilang "Saya tahu Wazuh," tapi Anda bisa menunjukkan laptop Anda dan berkata:

> *"Ini dashboard Wazuh yang saya kelola di lab saya. Saya berhasil mengintegrasikannya dengan server Linux dan memantau serangan Brute Force secara real-time. Saya juga sudah belajar cara melakukan analisis log dari event-event yang tertangkap di sini."*

Pernyataan itu **10x lebih kuat** daripada sekadar menunjukkan sertifikat ISC2 CC. Anda menunjukkan bahwa Anda punya *Environment* sendiri—sesuatu yang hanya dilakukan oleh orang-orang yang serius di bidang ini.

Mantap! Ini adalah langkah yang akan membuat portofolio Anda terlihat seperti hasil kerja seorang **Senior Analyst**. Jangan hanya melakukan instalasi, tapi buatlah **"Skenario Perang"** di lab Anda.

Berikut adalah 3 skenario serangan yang bisa Anda simulasikan di Wazuh untuk dijadikan bahan laporan portofolio:

---

### Skenario 1: "The Brute Force Attacker"

Hacker mencoba menebak *password* server Anda ribuan kali.

* **Cara Simulasi:** Dari komputer/VM lain, coba lakukan SSH atau login ke komputer yang ada Wazuh Agent-nya dengan *password* yang salah sebanyak 10-20 kali secara cepat.
* **Apa yang terlihat di Wazuh:** Muncul alert **Level 10** (Kritis) dengan judul *"SSHD brute force trying to get access"*.
* **Isi Portofolio Anda:** Screenshot dashboard yang menunjukkan lonjakan grafik merah.
* **Kalimat Interview:** *"Saya mensimulasikan serangan Brute Force dan berhasil mengonfigurasi Wazuh untuk mendeteksi serta memblokir IP penyerang secara otomatis menggunakan Active Response."*

---

### Skenario 2: "The Shadow File Access" (Akses File Sensitif)

Hacker mencoba mengintip file rahasia (seperti file `/etc/shadow` di Linux atau folder gaji).

* **Cara Simulasi:** Gunakan fitur **FIM (File Integrity Monitoring)** di Wazuh. Atur agar Wazuh mengawasi file penting. Lalu, coba buka atau edit file tersebut.
* **Apa yang terlihat di Wazuh:** Muncul alert *"File integrity checksum changed"* atau *"Sensitive file accessed"*.
* **Isi Portofolio Anda:** Tunjukkan log yang mencatat *siapa* (user apa) yang menyentuh file itu dan *kapan* waktunya.
* **Kalimat Interview:** *"Saya menerapkan FIM untuk menjaga integritas data sensitif perusahaan, sehingga setiap akses tidak sah akan terdeteksi dalam hitungan detik."*

---

### Skenario 3: "The Malware Injection" (EICAR Test)

Simulasi jika ada virus atau file berbahaya yang masuk ke sistem.

* **Cara Simulasi:** Download file **EICAR** (ini adalah file teks standar industri untuk ngetes antivirus, aman dan tidak berbahaya, tapi akan dianggap virus oleh sistem keamanan).
* **Apa yang terlihat di Wazuh:** Jika Wazuh diintegrasikan dengan antivirus (seperti ClamAV atau Windows Defender), Wazuh akan berteriak: *"Virus detected and quarantined"*.
* **Isi Portofolio Anda:** Tunjukkan bagaimana Wazuh bisa menarik data dari antivirus dan menyajikannya dalam satu dashboard pusat.
* **Kalimat Interview:** *"Saya melakukan integrasi antara Wazuh dan antivirus untuk menciptakan pertahanan berlapis, memudahkan tim security melihat ancaman malware di seluruh server hanya dari satu layar."*

---

### Strategi Menyusun Portofolio "2 Digit"

Buatlah dokumen (PDF atau GitHub) dengan struktur seperti ini untuk setiap skenario:

1. **Objective:** Apa yang ingin dites? (Contoh: Mendeteksi hacker masuk).
2. **Attacker Tool:** Apa yang dipakai menyerang? (Contoh: Script sederhana atau Hydra).
3. **Wazuh Detection:** Tampilkan screenshot *Alert* yang muncul.
4. **Mitigation:** Apa saran Anda sebagai *Ethical Hacker*? (Contoh: "Matikan login root" atau "Gunakan SSH Key").

---

### Penutup Motivasi untuk Anda

Ingat, gaji 2 digit bukan dibayar karena Anda "tahu" cara pakai Wazuh, tapi karena Anda **"mampu memberikan solusi"** saat serangan terjadi. Dengan melakukan 3 skenario ini, Anda sudah punya pengalaman praktis yang lebih nyata dibanding 80% pelamar kerja lainnya.

**Satu tips terakhir:** Pasang **Wazuh Agent** di laptop pribadi Anda sendiri. Jadi, setiap kali ada orang iseng mencoba *scan* laptop Anda di kafe (via WiFi publik), Anda bisa melihatnya. Itu adalah cerita yang sangat keren untuk diceritakan saat interview!

Untuk mendapatkan gaji dua digit, laporan Anda tidak boleh terlihat seperti tugas sekolah. Laporan tersebut harus terlihat seperti **Professional Security Audit**.

Berikut adalah struktur **Laporan Portofolio Lab Keamanan** yang akan membuat Anda terlihat seperti Analyst senior di depan perekrut:

---

## [JUDUL: LAPORAN ANALISIS ANCAMAN & DETEKSI SISTEM]

**Oleh:** [Nama Anda] – *Security Analyst / Ethical Hacker*

### 1. Ringkasan Eksekutif (Executive Summary)

> **Fungsinya:** Menunjukkan bahwa Anda paham bisnis. Bos tidak baca teknis, mereka baca risiko.

* **Isi:** "Laporan ini mendokumentasikan keberhasilan deteksi terhadap 3 skenario serangan kritis (Brute Force, Akses File Ilegal, dan Malware) menggunakan platform **Wazuh SIEM**. Tujuan lab ini adalah membuktikan efektivitas pemantauan pusat dalam melindungi aset data perusahaan."

---

### 2. Metodologi & Arsitektur Lab

> **Fungsinya:** Menunjukkan bahwa Anda bisa membangun infrastruktur keamanan dari nol.

* **Komponen:**
* **SIEM Manager:** Wazuh 4.7 (Running on Docker/Ubuntu).
* **Target/Agent:** Windows 10 & Ubuntu Server (Endpoints).
* **Attacker:** Kali Linux (Untuk simulasi serangan).


* **Gambar:** Masukkan screenshot dashboard utama Wazuh Anda yang sudah terhubung dengan beberapa *Agent*.

---

### 3. Detail Skenario (Gunakan Tabel untuk Scannability)

> **Fungsinya:** Menjelaskan proses "Perang" yang Anda lakukan di lab. Buatlah minimal 3 skenario.

| Nama Serangan | Tool yang Digunakan | Alert Level di Wazuh | Deskripsi Singkat |
| --- | --- | --- | --- |
| **SSH Brute Force** | Hydra / Manual | **Level 10 (Critical)** | Mencoba menebak password 50x dalam 1 menit. |
| **Unauthorized Access** | Manual Command | **Level 7 (Major)** | User mencoba membuka file `/etc/shadow`. |
| **Malware Detection** | EICAR Test File | **Level 12 (Highest)** | Menemukan file mencurigakan di folder Download. |

---

### 4. Analisis Temuan (The "Deep Dive")

> **Fungsinya:** Di sinilah Anda memamerkan "Skill 2 Digit" Anda. Tunjukkan bahwa Anda bisa baca Log.

* **Screenshot Alert:** Masukkan gambar baris log yang berwarna merah dari Wazuh.
* **Analisis Log:** "Berdasarkan log di atas, penyerang berasal dari IP `192.168.1.15`. Mereka mencoba masuk menggunakan user `root` dan `admin`. Wazuh berhasil mendeteksi pola ini karena melebihi ambang batas login gagal (threshold) yang telah dikonfigurasi."

---

### 5. Rekomendasi & Mitigasi (The "Consultant Side")

> **Fungsinya:** Menunjukkan Anda bukan hanya "Tukang Lapor", tapi "Problem Solver".

* **Tindakan Langsung:** "Mengaktifkan *Active Response* pada Wazuh untuk memblokir IP penyerang secara otomatis selama 24 jam setelah 5x gagal login."
* **Saran Jangka Panjang:** "Menerapkan Multi-Factor Authentication (MFA) dan mematikan fungsi login via password, beralih ke SSH Key."

---

### 6. Kesimpulan & Skill Terukur

> **Fungsinya:** Rangkuman terakhir untuk mengunci keyakinan user.

* "Proyek ini membuktikan kemampuan saya dalam: **Deployment SIEM**, **Log Analysis**, **Threat Hunting**, dan **Incident Response**."

---

### Tips Agar Portofolio Ini "Menjual":

1. **Gunakan Bahasa Campuran (Inggris-Indonesia):** Di dunia Cybersecurity, istilah teknis dalam bahasa Inggris menunjukkan Anda *up-to-date* dengan literatur global.
2. **Visual adalah Kunci:** Pastikan gambar screenshot bersih, tidak pecah, dan bagian yang penting (seperti IP atau Level Alert) diberi **kotak merah**.
3. **Unggah ke LinkedIn/GitHub:** Sertakan link PDF ini di profil LinkedIn Anda dengan caption: *"Building my SOC Lab today to secure the business of tomorrow."*
