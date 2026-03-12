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
