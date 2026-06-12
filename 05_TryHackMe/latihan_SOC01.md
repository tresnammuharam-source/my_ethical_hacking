# muscle memory SOC01

Sikap dan persiapan Anda sudah sangat tepat. Dengan harga ujian sebesar $130 USD, melakukan simulasi mandiri di Kali Linux adalah cara terbaik untuk membangun *muscle memory* dan kepercayaan diri sebelum menghadapi *browser-based lab* asli di TryHackMe.

Berikut adalah panduan lengkap untuk melakukan pengaturan (*setting*) laboratorium latihan Anda, diikuti dengan **7 Modul Soal Hands-on** yang dirancang mirip dengan format ujian SEC01.

---

## BAGIAN 1: Panduan Setting Lab & Tools di Kali Linux

Agar Anda bisa mengerjakan soal latihan di bawah, pastikan Kali Linux Anda terhubung ke internet dan beberapa *tools* berikut sudah siap.

### 1. Update Sistem & Install Tools Utama

Buka terminal di Kali Linux Anda, lalu jalankan perintah berikut untuk memastikan semua perangkat lunak berada dalam versi terbaru dan *tools* yang dibutuhkan sudah terinstal:

```bash
sudo apt update && sudo apt install -y wireshark tshark hydra john hashcat curl nikto snort apache2

```

### 2. Mengaktifkan Layanan Korban (Target) Secara Lokal

Untuk menyimulasikan target yang akan diserang atau dianalisis (seperti web server atau layanan SSH), kita akan mengaktifkan beberapa servis bawaan di Kali Linux Anda sendiri:

* **Mengaktifkan Web Server (Apache):**
```bash
sudo systemctl start apache2

```


* **Mengaktifkan SSH Server (untuk latihan Brute Force):**
```bash
sudo systemctl start ssh

```



### 3. Menyiapkan Wordlist Penting

TryHackMe sering kali menggunakan wordlist standar `rockyou.txt`. Di Kali Linux, file ini biasanya masih terkompresi. Jalankan perintah ini untuk mengekstraknya:

```bash
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz 2>/dev/null

```

*(Jika file tidak ditemukan, Anda bisa menggunakan wordlist alternatif `/usr/share/wordlists/fasttrack.txt`)*.

---

## BAGIAN 2: 7 Modul Soal Latihan Hands-on (Simulasi Ujian SEC01)

*Catatan: Karena Anda menggunakan Kali Linux, untuk bagian **Windows Fundamentals**, kita akan menyimulasikannya menggunakan perintah pencarian informasi sistem versi Linux/Unix yang memiliki konsep logika serupa (mencari konfigurasi dan file tersembunyi).*

Masing-masing soal di bawah ini akan menghasilkan sebuah **Flag** unik jika Anda berhasil mengerjakannya dengan benar.

### Modul 1: Windows & System Fundamentals (Simulasi Navigasi Sistem)

**Skenario:** Seseorang telah menyembunyikan file rahasia yang berisi informasi lisensi penting di dalam direktori sistem.

* **Tugas:** 1. Masuk ke direktori `/var/tmp/`.
2. Cari tahu apakah ada file tersembunyi (file yang diawali dengan tanda titik `.`).
3. Jika ada file bernama `.system_flag.txt`, baca isinya.
* **Petunjuk Perintah:** Gunakan kombinasi perintah `ls -la` untuk melihat file tersembunyi dan `cat` untuk membaca file.
* **Flag yang dicari:** Isi teks di dalam file `.system_flag.txt`.
*(Catatan Mandiri: Jika file belum ada, Anda bisa membuatnya sendiri terlebih dahulu untuk latihan dengan perintah: `echo "THM{SYS_NAV_MASTER_99}" > /var/tmp/.system_flag.txt`)*

### Modul 2: Linux Fundamentals (Manipulasi & Analisis File)

**Skenario:** Anda mendeteksi adanya aktivitas mencurigakan pada file log server. Anda diminta mencari entri spesifik yang menunjukkan kegagalan akses.

* **Tugas:** 1. Buat sebuah file latihan di folder home Anda dengan perintah:
`bash echo -e "User admin logged in\nUser guest login failed\nUser test logged in\nTHM{LINUX_GREP_CHALLENGE}" > ~/auth_sim.log `
2. Tanpa membuka file tersebut secara utuh, gunakan perintah CLI untuk mencari baris yang mengandung kata **"failed"** atau mencari pola teks **"THM{"**.
* **Petunjuk Perintah:** Gunakan perintah `grep` diikuti dengan kata kunci dan nama filenya.
* **Flag yang dicari:** String `THM{...}` yang ditemukan di dalam file log tersebut.

### Modul 3: Network Traffic Fundamentals (Analisis Lalu Lintas Jaringan)

**Skenario:** Sebuah komputer mengirimkan paket data ping (ICMP) secara terus-menerus ke jaringan local. Anda diminta menangkap lalu lintas tersebut dan menganalisisnya.

* **Tugas:**
1. Buka terminal baru, jalankan perintah penangkapan paket selama 10 detik ke sebuah file:
```bash
sudo tshark -i lo -w ~/traffic.pcap -a duration:10

```


2. Sembari terminal di atas berjalan, buka terminal satu lagi dan lakukan ping ke diri sendiri:
```bash
ping -c 4 127.0.0.1

```


3. Setelah selesai, buka file `~/traffic.pcap` menggunakan aplikasi grafis **Wireshark** (`wireshark ~/traffic.pcap`).


* **Petunjuk Analisis:** Di kolom *Filter* Wireshark, ketik `icmp`. Perhatikan paket yang tersaring.
* **Flag/Pertanyaan yang harus dijawab:** Berapa jumlah total paket ICMP (*Request* dan *Reply*) yang berhasil Anda tangkap?

### Modul 4: Web Pentesting Fundamentals (Eksplorasi Kerentanan Web)

**Skenario:** Anda diminta melakukan pemindaian awal terhadap web server lokal untuk melihat apakah ada direktori tersembunyi yang tidak terlihat di halaman utama.

* **Tugas:**
1. Pastikan Apache2 Anda sudah menyala (`sudo systemctl start apache2`).
2. Lakukan *Directory Brute Forcing* atau *Web Scanning* terhadap IP lokal Anda (`http://127.0.0.1`) menggunakan alat bernama `nikto`.


* **Petunjuk Perintah:** ```bash
nikto -h http://127.0.0.1
```

```


* **Flag/Pertanyaan yang harus dijawab:** Tuliskan versi Apache server yang berhasil dideteksi oleh tool `nikto` tersebut.

### Modul 5: Security Operations Fundamentals (Analisis Log & Kriptografi)

**Skenario:** Tim insiden siber menemukan sebuah string teks acak yang ditinggalkan oleh penyerang di komputer korban. String tersebut diduga merupakan hasil enkripsi Base64.

* **Tugas:**
1. Penyerang meninggalkan string berikut: `VEhNe0JMVUVfVEVBTV9MT0dfQU5BTFlTSVN9`
2. Lakukan dekode (*decode*) pada string tersebut menggunakan terminal Kali Linux atau alat bantu web CyberChef bawaan Kali.


* **Petunjuk Perintah:** Gunakan perintah `echo` dan *pipe* (`|`) menuju utilitas `base64 -d`.
```bash
echo "VEhNe0JMVUVfVEVBTV9MT0dfQU5BTFlTSVN9" | base64 -d

```


* **Flag yang dicari:** Hasil terjemahan teks asli dari string Base64 tersebut.

### Modul 6: Bruteforcing and Cracking Fundamentals (Pencarian Kredensial)

**Skenario:** Anda berhasil mendapatkan nilai *hash* dari kata sandi akun seorang user. Anda perlu memecahkan *hash* tersebut untuk mengetahui kata sandi aslinya.

* **Tugas:**
1. Buat sebuah file bernama `target_hash.txt` dan masukkan nilai hash MD5 berikut ke dalamnya: `098f6bcd4621d373cade4e832627b4f6`
2. Gunakan tool **John the Ripper** bersama wordlist `fasttrack.txt` untuk memecahkan hash tersebut.


* **Petunjuk Perintah:**
```bash
echo "098f6bcd4621d373cade4e832627b4f6" > ~/target_hash.txt
john --format=Raw-MD5 --wordlist=/usr/share/wordlists/fasttrack.txt ~/target_hash.txt

```


* **Flag/Jawaban yang dicari:** Apa kata sandi asli (teks biasa) di balik hash MD5 tersebut?

### Modul 7: Malware Analysis Fundamentals (Analisis Statis Dasar)

**Skenario:** Anda menemukan file biner mencurigakan yang diduga merupakan malware. Anda diminta mencari indikasi alamat IP server *Command and Control* (C2) yang tertanam di dalam file tanpa mengeksekusinya.

* **Tugas:**
1. Kita simulasikan file malware dengan perintah berikut:
```bash
echo -e "MALWARE_DATA_⚠️\nSERVER_IP=192.168.100.50\nTHM{STATIC_MALWARE_ANALYSIS_SUCCESS}" > ~/suspicious_file.bin

```


2. Gunakan perangkat analisis statis dasar untuk mengekstrak teks yang dapat dibaca manusia (*human-readable strings*) dari file biner tersebut.


* **Petunjuk Perintah:** Gunakan perintah `strings` di terminal.
```bash
strings ~/suspicious_file.bin

```


* **Flag yang dicari:** Temukan string berformat `THM{...}` dan Alamat IP server yang tersembunyi di dalam file tersebut.

---

### Tips Tambahan untuk Berlatih:

* Jangan melihat kunci jawaban atau petunjuk pengerjaan terlebih dahulu sebelum Anda benar-benar mencoba mengetikkan perintahnya sendiri.
* Jika Anda mengalami eror (misal: *command not found*), biasakan untuk membaca pesan erornya dengan teliti. Di dunia siber, kemampuan menyelesaikan masalah (*troubleshooting*) secara mandiri adalah kunci kelulusan terbesar.

Selamat berlatih di Kali Linux Anda. Jika ada kendala saat mengeksekusi modul-modul di atas, silakan tanyakan kembali!
