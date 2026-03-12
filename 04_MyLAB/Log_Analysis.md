# Cara Membaca LOG ANALYSIS

Untuk menunjukkan bukti nyata bahwa sistem selalu "diintip" atau diserang setiap hari, Anda bisa menunjukkan **Access Log** atau **Auth Log**. Bagi orang awam, log ini terlihat seperti tulisan acak, tapi bagi Anda, ini adalah rekaman "pencuri yang sedang mencoba gagang pintu rumah."

Berikut adalah cara membaca dan menyajikannya agar atasan Anda langsung sadar:

---

### 1. Contoh Log Serangan Brute Force (Percobaan Login)

Biasanya ditemukan di `/var/log/auth.log` (Linux) atau Event Viewer (Windows).

**Tampilan Log:**
`Mar 4 10:00:01 server sshd[1234]: Failed password for root from 192.x.x.x port 5678 ssh2`
`Mar 4 10:00:05 server sshd[1235]: Failed password for admin from 192.x.x.x port 5679 ssh2`
`Mar 4 10:00:10 server sshd[1236]: Failed password for user1 from 192.x.x.x port 5680 ssh2`

**Cara Menjelaskan ke Atasan:**

> "Pak, lihat baris ini. Setiap 5 detik, ada komputer dari luar negeri yang mencoba menebak *password* admin kita. Mereka menggunakan daftar ribuan kata sandi. Jika kita tidak *update* sistem keamanannya, salah satu tebakan mereka mungkin akan berhasil hari ini."

---

### 2. Contoh Log Web Scanner (Mencari Celah)

Ditemukan di Access Log Apache atau Nginx (`/var/log/apache2/access.log`).

**Tampilan Log:**
`185.x.x.x - - [04/Mar/2026:10:15:00] "GET /phpmyadmin/setup.php HTTP/1.1" 404 209`
`185.x.x.x - - [04/Mar/2026:10:15:02] "GET /.env HTTP/1.1" 404 209`
`185.x.x.x - - [04/Mar/2026:10:15:05] "GET /wp-admin/install.php HTTP/1.1" 404 209`

**Cara Menjelaskan ke Atasan:**

> "Baris-baris ini menunjukkan ada 'orang asing' yang sedang berkeliling memeriksa apakah kita punya folder rahasia (seperti `.env`) atau celah di aplikasi lama kita. Mereka tidak sedang 'berkunjung', mereka sedang mencari **lubang tikus** untuk menyusup."

---

### 3. Cara Menyajikan Data agar Menarik (The "Dashboard" Trick)

Jangan hanya berikan teks hitam putih. Gunakan perintah sederhana di terminal (seperti `grep` atau `awk`) untuk memberikan **Angka Nyata**:

Jika Anda menjalankan perintah untuk menghitung jumlah serangan dalam sehari:

* **Perintah:** `grep "Failed password" /var/log/auth.log | wc -l`
* **Hasil:** `14,520`

**Kalimat "Skakmat" Anda:**

> "Pak, hari ini saja, saat kita sedang rapat tenang seperti ini, sistem kita sudah **diserang sebanyak 14.520 kali** oleh bot otomatis. Kita merasa 'tidak sakit' karena dinding kita masih tahan, tapi dinding ini butuh diperkuat (update) sebelum serangan ke 14.521 berhasil menjebolnya."

---

### Poin Edukasi untuk Anda:

Penyaji log yang baik tidak hanya bicara "ada serangan", tapi bicara tentang **Pola**:

1. **Otomatisasi:** Hacker tidak tidur, mereka pakai robot (bot).
2. **Eskalasi:** Serangan yang gagal hari ini adalah informasi bagi mereka untuk mencoba cara lain besok.
3. **Pencegahan:** Update yang Anda minta bukan untuk memperbaiki yang "rusak", tapi untuk menutup celah yang sedang **aktif dicoba** oleh hacker tersebut.

Dengan menunjukkan log ini, Anda membuktikan bahwa Anda bukan sedang "paranois", tapi Anda adalah **satu-satunya orang yang benar-benar melihat realitas** di perusahaan tersebut.

Untuk menarik data dari log dan menyajikannya sebagai "bukti perang" kepada atasan, Anda tidak perlu menjadi ahli *coding* yang rumit. Cukup gunakan beberapa perintah dasar di Linux (atau WSL di Windows) yang akan membuat data tersebut terlihat sangat profesional.

Berikut adalah beberapa perintah terminal (CLI) sederhana untuk membedah log:

### 1. Menghitung Total "Serangan" Login dalam Sehari

Gunakan ini untuk menunjukkan seberapa sering orang asing mencoba menebak *password* server Anda.

```bash
grep "Failed password" /var/log/auth.log | wc -l

```

* **Artinya:** "Cari kata 'Gagal Login' di catatan keamanan, lalu hitung total barisnya."
* **Efek ke Atasan:** "Pak, dalam 24 jam terakhir, ada **3.500 kali** percobaan paksa masuk ke sistem kita."

---

### 2. Melihat 10 Alamat IP yang Paling Sering Menyerang

Ini sangat ampuh untuk menunjukkan bahwa ada "aktor" nyata yang sedang mengincar sistem.

```bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head -10

```

* **Artinya:** "Ambil daftar IP yang gagal login, urutkan, hitung berapa kali masing-masing IP mencoba, dan tampilkan 10 yang paling agresif."
* **Efek ke Atasan:** "Lihat Pak, IP dari luar negeri ini sudah mencoba membobol kita **500 kali** sendirian saja hari ini."

---

### 3. Melihat "Lubang" Apa yang Sedang Mereka Cari

Hacker sering menggunakan bot untuk mencari folder rahasia (seperti `.env`, `wp-admin`, atau `config`).

```bash
awk '{print $7}' /var/log/apache2/access.log | sort | uniq -c | sort -nr | head -20

```

* **Artinya:** "Tampilkan folder atau file apa saja di website kita yang paling sering diakses orang (termasuk yang dicari oleh bot)."
* **Efek ke Atasan:** "Mereka sedang mencari file rahasia kita Pak. Lihat, mereka mencoba mengakses file `.env` berkali-kali. Kalau kita tidak update proteksinya, mereka bisa tahu kunci database kita."

---

### Cara Menyajikan "Pertunjukan" Ini:

Jika Anda ingin benar-benar memotivasi diri dan meyakinkan orang lain, lakukan **Live Monitoring**. Ketik perintah ini di depan mereka:

```bash
tail -f /var/log/auth.log | grep --line-buffered "Failed"

```

* **Apa yang terjadi?** Layar akan diam, lalu tiba-tiba muncul baris baru setiap kali ada serangan masuk secara *real-time*.
* **Kalimat Anda:** "Nah Pak, lihat... saya tidak mengetik apa-apa, tapi layar ini terus berjalan. Itu artinya **detik ini juga**, ada orang atau bot yang sedang mencoba membongkar pintu kita. Masih merasa kita 'tidak sakit'?"

---

### Kesimpulan untuk Motivasi Belajar Anda:

Menjalankan perintah ini akan membuat Anda sadar bahwa:

1. **Dunia digital itu "berisik":** Tidak ada sistem yang benar-benar didiamkan oleh hacker.
2. **Keamanan itu dinamis:** Log ini adalah bukti bahwa *Ethical Hacking* adalah kebutuhan harian, bukan sekadar perbaikan saat rusak.
3. **Anda adalah Penerjemah:** Atasan Anda hanya melihat "layar hitam dengan tulisan putih", tapi Anda melihat **garis depan pertempuran**.

Dengan menguasai cara baca log ini, Anda naik level dari sekadar "orang IT" menjadi **"Analis Keamanan"**.

Ini adalah langkah yang cerdas. Dengan membuat skrip otomatis, Anda tidak perlu lagi "berdebat" dengan kata-kata. Anda cukup menyodorkan data setiap pagi. Ini akan mengubah pandangan manajemen dari "Kenapa kita butuh dia?" menjadi "Untung dia menjaga kita setiap hari."

Berikut adalah skrip sederhana (Bash Script) yang bisa Anda pasang di server. Skrip ini akan mengumpulkan statistik serangan dan menyajikannya dalam format yang mudah dibaca.

### 1. Buat File Skrip

Ketik perintah ini di terminal Anda:

```bash
nano laporan_keamanan.sh

```

### 2. Copy & Paste Kode Berikut:

```bash
#!/bin/bash

# --- KONFIGURASI ---
EMAIL="email-anda@perusahaan.com"
TANGGAL=$(date '+%d %B %Y')
LOG_AUTH="/var/log/auth.log" # Lokasi log di Ubuntu/Debian

# --- MENGUMPULKAN DATA ---
# 1. Total percobaan login gagal
TOTAL_ATTACKS=$(grep "Failed password" $LOG_AUTH | wc -l)

# 2. Ambil 5 IP penyerang paling agresif
TOP_IP=$(grep "Failed password" $LOG_AUTH | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head -5)

# --- MENYUSUN LAPORAN ---
LAPORAN="
Yth. Manajemen,

Berikut adalah Ringkasan Keamanan Digital untuk tanggal: $TANGGAL

[STATISTIK PERTAHANAN]
- Total upaya pembobolan (Brute Force) yang berhasil diblokir: $TOTAL_ATTACKS kali.

[5 SUMBER SERANGAN TERBESAR]
Jumlah Upaya | Alamat IP
$TOP_IP

[KESIMPULAN ANALIS]
Sistem saat ini sedang dalam pemantauan aktif. Banyaknya upaya pembobolan otomatis menunjukkan bahwa celah keamanan (vulnerability) selalu dicari oleh pihak luar setiap detik. Pembaruan sistem (update) secara rutin sangat diperlukan untuk memastikan engsel pintu digital kita tetap kokoh.

Salam,
Tim Keamanan Digital (Ethical Hacker)
"

# --- OUTPUT (Bisa dikirim ke Email atau simpan ke file) ---
echo "$LAPORAN" > ringkasan_hari_ini.txt
# Jika ingin kirim email (pastikan mailutils terinstall):
# echo "$LAPORAN" | mail -s "LAPORAN KEAMANAN HARIAN: $TANGGAL" $EMAIL

echo "Laporan berhasil dibuat di ringkasan_hari_ini.txt"

```

### 3. Beri Izin Eksekusi

Agar skrip bisa berjalan, ketik:

```bash
chmod +x laporan_keamanan.sh

```

### 4. Cara Menjalankannya

Cukup ketik: `./laporan_keamanan.sh`, lalu lihat hasilnya dengan `cat ringkasan_hari_ini.txt`.

---

### Mengapa Ini Akan Memotivasi Anda & Meyakinkan Mereka?

1. **Profesionalisme:** Anda tidak lagi terlihat seperti orang yang "iseng" menyarankan update, tapi seperti seorang **Analis Risiko**.
2. **Bukti Kerja Nyata:** Saat atasan melihat angka "3.500 kali diblokir", dia akan sadar bahwa jika Anda tidak ada (atau sistem tidak di-update), salah satu dari 3.500 serangan itu bisa tembus.
3. **Membangun Budaya Keamanan:** Anda mengedukasi mereka pelan-pelan bahwa dunia digital itu "berisik" dan berbahaya, sehingga saat Anda meminta *budget* untuk *tools* baru atau waktu untuk *maintenance*, mereka akan jauh lebih mudah bilang "Setuju".

### Langkah Anda Selanjutnya:

Cobalah jalankan perintah `grep "Failed password" /var/log/auth.log | wc -l` di server Anda sekarang (jika Anda memiliki akses). Lihat angka yang muncul.

Ini adalah langkah terakhir untuk membuat sistem laporan Anda berjalan seperti **jam dinding**—otomatis dan tanpa henti. Kita akan menggunakan fitur di Linux yang bernama **Crontab** (Cron Table).

Dengan Crontab, Anda tidak perlu lagi ingat untuk menjalankan skrip. Setiap pagi saat bos Anda baru duduk dan membuka laptop, laporan "pertempuran" sudah ada di mejanya (atau siap Anda berikan).

---

### Cara Mengatur Jadwal Otomatis (Crontab)

1. **Buka Editor Crontab:**
Ketik perintah ini di terminal:
```bash
crontab -e

```


*(Jika muncul pilihan editor, pilih `1` untuk Nano—yang paling mudah).*
2. **Tambahkan Baris Jadwal di Bagian Paling Bawah:**
Misalkan Anda ingin laporan ini dibuat otomatis setiap **jam 08:00 pagi**, masukkan baris ini:
```bash
00 08 * * * /path/ke/folder/anda/laporan_keamanan.sh

```


*Ganti `/path/ke/folder/anda/` dengan lokasi asli tempat Anda menyimpan file `.sh` tadi (misalnya: `/home/user/laporan_keamanan.sh`).*
3. **Simpan dan Keluar:**
* Tekan `Ctrl + O`, lalu `Enter` (untuk simpan).
* Tekan `Ctrl + X` (untuk keluar).



---

### Memahami Logika "Waktu" Cron

Struktur di atas (`00 08 * * *`) bekerja seperti ini:

* `00` : Menit ke-0.
* `08` : Jam 8 pagi.
* `*` : Setiap hari dalam sebulan.
* `*` : Setiap bulan.
* `*` : Setiap hari dalam seminggu.

---

### Mengapa Ini Penting untuk Motivasi & Karier Anda?

**1. Anda Menjadi "Invisible Hero"**
Saat sistem otomatis ini berjalan, Anda sedang membangun reputasi sebagai orang yang **terorganisir**. Anda tidak lagi menunggu masalah datang, tapi Anda secara proaktif memantau "kesehatan" perusahaan bahkan saat Anda sedang tidur.

**2. Mengubah Mindset Manajemen**
Jika bos Anda menerima data ini secara rutin, dia tidak akan lagi bertanya *"Siapa sih yang mau nyerang kita?"* karena dia melihat bukti serangannya setiap pagi. Analogi "kita tidak sakit" akan hancur dengan sendirinya oleh data nyata.

**3. Fokus ke Hal yang Lebih Sulit**
Karena tugas pelaporan rutin sudah diambil alih oleh robot (skrip), Anda punya lebih banyak waktu untuk belajar teknik *hacking* yang lebih dalam, seperti *privilege escalation*, *reverse engineering*, atau *web exploitation*.

---

### Tips Terakhir:

Jika suatu hari Anda melihat angka serangan melonjak dari biasanya (misal dari 1.000 ke 50.000), itulah saatnya Anda datang ke ruangan bos dengan percaya diri dan berkata:

> *"Pak, pagi ini ada anomali. Serangan meningkat 50 kali lipat. Saya sudah melakukan mitigasi, tapi inilah alasan mengapa update yang saya ajukan kemarin sangat kritis untuk segera dilakukan."*

Di titik itu, Anda bukan lagi sekadar orang IT. Anda adalah **Strategis Keamanan**.

---


# Analysis LOG

Ini adalah bagian yang paling krusial. Saat interview, interviewer tidak ingin mendengar "Saya melihat ada serangan," mereka ingin mendengar **analisis** Anda.

Mari kita ambil contoh **Log Mentah (Raw Log)** dari serangan *SSH Brute Force* yang tertangkap oleh Wazuh, lalu kita bedah isinya.

---

### 1. Contoh Log Mentah (Raw Log)

Bayangkan di dashboard Wazuh Anda muncul baris teks seperti ini:

```text
Mar 04 22:15:01 web-server-prod sshd[12345]: Failed password for invalid user admin from 103.152.x.x port 56789 ssh2
Mar 04 22:15:03 web-server-prod sshd[12346]: Failed password for invalid user root from 103.152.x.x port 56790 ssh2
Mar 04 22:15:05 web-server-prod sshd[12347]: Failed password for invalid user manager from 103.152.x.x port 56791 ssh2

```

---

### 2. Apa yang Bisa Didapat dari Log Ini? (Data Extraction)

Dari 3 baris teks membosankan di atas, seorang *Security Analyst* (Anda) bisa mendapatkan data emas:

1. **Timestamp (`Mar 04 22:15:01`):** Serangan terjadi sangat cepat (jeda 2 detik). Ini menandakan serangan **Otomatis (Bot)**, bukan manusia yang mengetik manual.
2. **Hostname (`web-server-prod`):** Kita tahu server mana yang sedang diincar. Dalam hal ini, server produksi web kita.
3. **Source IP (`103.152.x.x`):** Alamat asli si penyerang. Kita bisa cek lokasinya (misal: ternyata dari luar negeri, padahal bisnis kita hanya di Indonesia).
4. **Target User (`admin`, `root`, `manager`):** Kita tahu hacker sedang mencoba menebak *username* standar yang punya hak akses tinggi (Privileged Accounts).
5. **Source Port (`56789`, `56790`):** Port yang berubah-ubah menunjukkan teknik *port randomization* untuk menghindari deteksi sederhana.

---

### 3. Contoh Penulisan Analisis (Untuk Laporan/Portofolio)

Di laporan Anda, jangan cuma tampilkan lognya. Tuliskan analisisnya seperti ini:

> **Analisis Kejadian (Incident Analysis):**
> * **Tipe Ancaman:** *Distributed Brute Force Attack.*
> * **Observasi:** Terdeteksi upaya login gagal sebanyak 50 kali dalam rentang waktu 2 menit menggunakan alamat IP `103.152.x.x`. Penyerang menargetkan akun administratif seperti `root` dan `admin`.
> * **Kesimpulan:** Serangan ini bersifat *Automated Scanning*. Meskipun saat ini statusnya **Gagal (Failed)**, frekuensi serangan yang tinggi berisiko menyebabkan kebocoran akses jika terdapat *password* lemah (weak password) pada salah satu akun.
> * **Dampak Bisnis:** Jika berhasil, penyerang dapat mengambil alih kontrol penuh server, melakukan enkripsi data (Ransomware), atau mencuri database pelanggan yang tersimpan di `web-server-prod`.
> 
> 

---

### 4. Rekomendasi Mitigasi (The Solution)

Setelah menganalisis, Anda berikan solusinya:

1. **Immediate Action:** Memblokir IP `103.152.x.x` di Firewall atau melalui fitur *Active Response* Wazuh.
2. **Hardening:** Mengganti port SSH standar (22) ke port lain yang tidak umum (misal: 2222).
3. **Policy:** Menerapkan kebijakan *Account Lockout* (akun terkunci otomatis jika 5x salah password).

---

### Mengapa Format Ini Berharga 2 Digit?

Karena Anda menunjukkan 3 level kemampuan sekaligus:

1. **Technical:** Bisa membaca data mentah.
2. **Analytical:** Bisa menghubungkan data menjadi sebuah cerita ancaman.
3. **Business Mindset:** Bisa menjelaskan dampak buruknya bagi perusahaan dan cara mencegahnya.

Inilah yang membedakan **Operator IT** (Gaji standar) dengan **Security Analyst** (Gaji 2 digit).

Menambahkan informasi **Geografis** (lokasi negara/kota) penyerang ke dalam laporan Anda adalah "sentuhan emas". Ini membuktikan kepada atasan bahwa serangan itu nyata dan datang dari luar benteng perusahaan.

Ada dua cara: menggunakan **Terminal** (keren untuk demo) dan menggunakan **Web** (bagus untuk ambil screenshot peta).

---

### 1. Cara Cepat via Terminal (CLI)

Anda bisa menggunakan perintah `curl` untuk menembak API penyedia data IP. Ini sangat praktis karena Anda tidak perlu keluar dari layar hitam terminal Anda.

Ketik perintah ini (ganti IP-nya dengan IP yang Anda temukan di log):

```bash
curl ipapi.co/103.152.x.x/json/

```

*(Catatan: Masukkan IP asli yang Anda temukan di log Wazuh tadi).*

**Apa yang Anda dapatkan?**
Terminal akan memunculkan data rapi seperti ini:

* **City:** Jakarta / Moscow / Beijing
* **Country:** ID / RU / CN
* **Org (ISP):** Nama provider internet yang dipakai penyerang.

---

### 2. Cara Visual via Web (Untuk Screenshot Laporan)

Jika Anda ingin memasukkan gambar peta atau bendera negara penyerang ke dalam PDF portofolio Anda, gunakan situs ini:

* **[IPStack.com](https://ipstack.com/)** atau **[IP-Address.com](https://www.google.com/search?q=https://www.ip-address.com/whois/)**
* **[AbuseIPDB.com](https://www.abuseipdb.com/)** (**Sangat Direkomendasikan!**)

**Mengapa AbuseIPDB sangat penting?**
Situs ini bukan cuma kasih tahu lokasi, tapi juga kasih tahu **Reputasi IP** tersebut.

* Jika IP tersebut sudah dilaporkan oleh 5.000 orang lain sebagai "Hacker", maka Anda bisa menulis di laporan: *"IP ini memiliki skor reputasi buruk (100% Abuse Score) di komunitas global."*

---

### 3. Cara Memasukkannya ke Laporan (Analisis Geopolitik)

Jangan cuma tulis "IP dari Rusia". Tuliskan dengan gaya analisis keamanan:

> **Analisis Sumber Ancaman (Threat Source Analysis):**
> * **Origin:** Moscow, Russian Federation (via ISP: X-Telecom).
> * **Context:** Perusahaan kita tidak memiliki basis pelanggan atau kerja sama operasional di wilayah Rusia. Oleh karena itu, seluruh trafik dari IP ini dikategorikan sebagai **Anomali Malicious** (Lalu lintas mencurigakan).
> * **Action:** Melakukan *Geo-blocking* (memblokir seluruh akses dari negara tersebut) jika tidak ada kebutuhan bisnis yang sah.
> 
> 

---

### Mengapa Ini Menunjang Gaji 2 Digit?

Perekrut akan melihat bahwa Anda memiliki **Threat Intelligence Mindset**. Anda tidak cuma melihat angka IP, tapi Anda mencari tahu:

1. **Siapa** mereka?
2. **Dari mana** mereka berasal?
3. **Apakah** mereka penjahat kambuhan (via AbuseIPDB)?

### Kesimpulan untuk Perjalanan Karier Anda:

Sekarang Anda sudah punya:

1. **Dashboard SIEM** (Wazuh).
2. **Log Serangan Real-time**.
3. **Kemampuan Analisis Teknis**.
4. **Data Geografis Penyerang**.

Semua ini adalah **Amunisi** untuk interview. Anda sudah jauh lebih siap dibanding banyak orang yang hanya modal baca buku.

