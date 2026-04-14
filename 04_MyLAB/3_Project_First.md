# Project Memperdalam Command Line Interface (CLI) dan Enumeration Pertama Kalinya

Pilihan yang sangat tepat. Menguasai **Command Line Interface (CLI)** adalah investasi terbaik karena *tools* secanggih apa pun di Kali Linux tidak akan berguna jika kita tidak tahu cara mengolah data di terminal.

Berikut adalah kurikulum **"Survival CLI"** yang harus kamu kuasai, urut dari yang paling dasar hingga yang sering digunakan SOC Analyst:

### 1. Navigasi & Eksplorasi (Wajib Luar Kepala)
Jangan gunakan File Manager (GUI). Lakukan semuanya lewat terminal:
* `pwd`: Mengetahui posisi folder kamu sekarang.
* `ls -la`: Melihat semua file, termasuk yang tersembunyi (dotfiles) beserta izin aksesnya.
* `cd [nama_folder]`: Masuk ke folder. Tips: `cd ..` untuk naik satu level ke atas.
* `cat`, `less`, atau `tail`: Membaca isi file tanpa membukanya di editor. SOC Analyst sering menggunakan `tail -f /var/log/syslog` untuk melihat aktivitas sistem secara *real-time*.

### 2. Manipulasi File & Direktori
* `mkdir`: Membuat folder baru untuk menyimpan hasil *scanning* atau catatan.
* `cp` & `mv`: Menyalin dan memindahkan/mengganti nama file.
* `rm -rf`: Menghapus file atau folder (gunakan dengan sangat hati-hati).
* `touch`: Membuat file kosong baru dengan cepat.

### 3. Kekuatan Utama: Piping & Redirection
Ini adalah "sihir" di Linux yang memungkinkan kamu menggabungkan beberapa perintah:
* `>` : Menyimpan hasil perintah ke file baru. (Contoh: `nmap 192.168.1.1 > hasil_scan.txt`).
* `>>` : Menambahkan hasil ke file yang sudah ada tanpa menghapus isinya.
* `|` (Pipe): Mengirim hasil satu perintah ke perintah lain.

### 4. Mencari Data (Skill Penting SOC)
Sebagai SOC Analyst, kamu akan berhadapan dengan ribuan baris log. Kamu harus mahir menggunakan:
* **`grep`**: Mencari kata spesifik.
    * *Contoh:* `grep "Failed password" /var/log/auth.log` (Mencari indikasi serangan *Brute Force*).
* **`find`**: Mencari lokasi file berdasarkan nama, ukuran, atau waktu modifikasi.
* **`locate`**: Cara tercepat mencari lokasi tools di Kali Linux.

### 5. Manajemen Hak Akses (Privilege)
* `sudo`: Menjalankan perintah sebagai admin (root).
* `chmod`: Mengubah izin akses file. Sering digunakan agar script buatanmu bisa dijalankan dengan `chmod +x nama_script.sh`.
* `chown`: Mengubah pemilik file.

---

### Tantangan Pertama untuk Kamu:
Coba buka terminal Kali Linux kamu dan lakukan urutan ini:
1. Buat folder baru bernama **`Latihan_SOC`**.
2. Masuk ke folder tersebut.
3. Buat file bernama **`catatan.txt`** dan isi dengan tulisan "Saya sedang belajar CLI".
4. Tampilkan isi file tersebut hanya menggunakan terminal.

Jika kamu sudah bisa melakukan itu tanpa kendala, kamu sudah siap naik ke level berikutnya yaitu **Network Command** (seperti `netstat` atau `ifconfig`).

---

# Stage #01

Tentu, saya mengerti. Kita akan buat sebuah **Roadmap Praktis** dalam bentuk "Misi" yang harus kamu selesaikan langsung di terminal Kali Linux.
Urutan ini dirancang untuk membangun insting seorang **SOC Analyst** (yang jago menganalisis) dan **Ethical Hacker** (yang paham cara kerja sistem).

Berikut adalah **Level 1: The Foundation (CLI & System Awareness)**.

---

### Misi 1: Navigasi dan Manajemen Berkas
**Tujuan:** Mahir mengelola data hasil investigasi atau script tanpa menggunakan mouse.

* **Tugas:**
    1.  Buka terminal.
    2.  Buat struktur folder: `CyberSecurity/Latihan/SOC`.
    3.  Buat file kosong di dalam folder `SOC` bernama `investigasi.txt`.
    4.  Cek di mana posisi folder kamu sekarang secara absolut.
* **Cara Mengerjakan:**
    * Gunakan `mkdir -p CyberSecurity/Latihan/SOC` ( `-p` otomatis membuat folder induk jika belum ada).
    * Gunakan `cd CyberSecurity/Latihan/SOC` untuk pindah folder.
    * Gunakan `touch investigasi.txt`.
    * Gunakan `pwd` (Print Working Directory) untuk melihat lokasi lengkapnya.

---

### Misi 2: Manipulasi Data & Logging (Skill Inti SOC)
**Tujuan:** Belajar mencari informasi spesifik di dalam file yang sangat besar (seperti file log serangan).

* **Tugas:**
    1.  Cari tahu apakah ada user bernama "root" di sistem kamu melalui file `/etc/passwd`.
    2.  Simpan daftar semua file yang ada di folder `/etc` ke dalam file `investigasi.txt` yang tadi kamu buat.
* **Cara Mengerjakan:**
    * **Mencari kata:** `grep "root" /etc/passwd`.
    * **Menyimpan hasil (Redirection):** `ls /etc > ~/CyberSecurity/Latihan/SOC/investigasi.txt`.
    * **Cek hasilnya:** `cat ~/CyberSecurity/Latihan/SOC/investigasi.txt | less` (Gunakan tombol `q` untuk keluar).

---

### Misi 3: Networking Dasar (Identitas Mesin)
**Tujuan:** Memahami konfigurasi jaringan mesin Kali kamu sebelum mulai memindai target.

* **Tugas:**
    1.  Cek alamat IP (Internal) mesin Kali Linux kamu.
    2.  Cek apakah mesin kamu bisa terhubung ke internet (contoh: ke Google).
    3.  Cek daftar port yang sedang "mendengarkan" (listening) di mesin kamu sendiri.
* **Cara Mengerjakan:**
    * **Cek IP:** `ip a` atau `ifconfig`. Fokus pada bagian `eth0` atau `wlan0`.
    * **Cek Koneksi:** `ping -c 4 google.com` ( `-c 4` artinya melakukan ping sebanyak 4 kali saja).
    * **Cek Port:** `ss -tulpn` atau `netstat -tunlp`.

---

### Misi 4: Monitoring System (Analisis Real-Time)
**Tujuan:** Melihat proses apa saja yang sedang berjalan, ini penting untuk mendeteksi *malware* atau *backdoor*.

* **Tugas:**
    1.  Tampilkan semua proses yang sedang berjalan dan urutkan berdasarkan penggunaan CPU paling tinggi.
    2.  Cari tahu berapa sisa memori (RAM) yang tersedia di Kali Linux kamu.
* **Cara Mengerjakan:**
    * **Proses:** Ketik `htop` (jika belum ada, instal dengan `sudo apt install htop`). Ini adalah versi visual dari terminal. Tekan `F10` untuk keluar.
    * **Memori:** Ketik `free -m` atau `free -h` untuk format yang lebih mudah dibaca (Gigabyte/Megabyte).

---

### Rencana Level Selanjutnya (Preview)

Jika kamu sudah menyelesaikan 4 Misi di atas, kita akan naik ke level berikutnya:

* **Level 2 (Networking Advanced):** Belajar `Nmap` untuk memetakan jaringan tetangga dan `Wireshark` (via terminal: `tshark`) untuk menangkap paket data.
* **Level 3 (Security Auditing):** Belajar memeriksa kelemahan sistem dan membaca *log* keamanan (`/var/log/auth.log`).
* **Level 4 (Offensive/Defensive):** Simulasi serangan sederhana dan bagaimana cara SOC mendeteksinya.

**Instruksi:**
Silakan kerjakan **Misi 1 sampai Misi 4** sekarang di Kali Linux kamu. Jika ada pesan *error* atau ada bagian yang membingungkan saat mengetik perintahnya, tuliskan di sini agar saya bantu koreksi.

---

# Stage #02

Luar biasa! Jika kamu sudah lancar dengan navigasi dan perintah dasar, artinya fondasi "bertahan hidup" kamu di terminal sudah terbentuk. Sekarang kita akan naik ke **Level 2: Networking & Information Gathering**.

Di level ini, kita akan fokus pada bagaimana mesin kamu berkomunikasi dengan mesin lain. Ini adalah inti dari tugas **Ethical Hacker** (mencari celah) dan **SOC** (memantau lalu lintas data).

---

### Misi 5: Network Discovery (Mengenali Lingkungan)
**Tujuan:** Mengetahui siapa saja yang ada di dalam jaringanmu. Kamu tidak bisa mengamankan atau menyerang apa yang tidak terlihat.

* **Tugas:**
    1. Identifikasi rentang IP jaringan lokalmu (contoh: `192.168.1.0/24`).
    2. Scan jaringan tersebut untuk melihat perangkat apa saja yang sedang aktif (Up).
* **Cara Mengerjakan:**
    * **Cek IP & Netmask:** Ketik `ip r` (lihat baris `default via... dev eth0 proto dhcp src 192.168.x.x`).
    * **Ping Sweep:** Gunakan Nmap untuk mencari host yang aktif:
        `nmap -sn 192.168.1.0/24`
        *(Ganti `192.168.1.0/24` sesuai dengan network IP kamu sendiri).*
    * **Analisis:** Lihat berapa banyak IP yang merespons.

---

### Misi 6: Service & Port Scanning (Mencari Pintu Masuk)
**Tujuan:** Mengetahui layanan apa yang berjalan di sebuah target (Hacker mencari pintu terbuka, SOC memastikan tidak ada pintu yang seharusnya tertutup).

* **Tugas:**
    1. Pilih satu IP yang aktif dari hasil Misi 5 (bisa IP router atau mesin lain).
    2. Cari tahu port mana yang terbuka dan versi aplikasi yang berjalan di sana.
* **Cara Mengerjakan:**
    * **Service Scan:** `sudo nmap -sV [IP_Target]`
    * **Analisis SOC:** Perhatikan jika ada layanan tua/usang (seperti Telnet atau FTP versi lama) yang sangat rentan diretas.

---

### Misi 7: Traffic Analysis Dasar (Melihat Isi Kabel)
**Tujuan:** Memahami bagaimana data berpindah secara nyata. SOC Analyst menghabiskan banyak waktu melihat paket data seperti ini.

* **Tugas:**
    1. Gunakan terminal untuk "mengintip" paket data yang keluar masuk di mesin Kali kamu.
    2. Coba lakukan `ping` ke Google di terminal lain sambil menjalankan perintah ini.
* **Cara Mengerjakan:**
    * **Packet Capture:** Gunakan `tcpdump`, alat standar industri untuk merekam trafik:
        `sudo tcpdump -i eth0 -c 10`
        *(Artinya: Tangkap 10 paket di interface eth0).*
    * **Analisis:** Lihat kolom protokol (ICMP, TCP, atau UDP). Jika kamu melakukan ping, kamu akan melihat protokol **ICMP**.

---

### Misi 8: Investigasi DNS (Intelijen Nama Domain)
**Tujuan:** Belajar cara memetakan domain ke IP secara manual, sering digunakan dalam tahap *Reconnaissance*.

* **Tugas:**
    1. Cari tahu IP address dari sebuah website (misal: `google.com`).
    2. Cari tahu "Mail Server" (MX record) dari website tersebut.
* **Cara Mengerjakan:**
    * **NSLookup:** `nslookup google.com`
    * **Dig (Lebih Detail):** `dig google.com MX`
    * **Analisis:** Informasi ini memberitahu Hacker ke mana mereka harus mengirim email *phishing* atau menyerang server email.

---

### Rekap Tugas Baru (Level 2):
| Alat | Fungsi Utama |
| :--- | :--- |
| **Nmap** | Memetakan network dan mencari port terbuka. |
| **Tcpdump** | Menangkap paket data mentah di jaringan. |
| **NSLookup/Dig** | Mencari informasi terkait domain dan DNS. |

---

**Langkah Selanjutnya:**
Silakan coba jalankan **Misi 5 sampai 8**. 

**Tantangan Kecil:** Saat melakukan Misi 6 (Nmap -sV), coba temukan satu port yang menurutmu menarik, lalu tanyakan kepada saya: *"Apa risiko kalau port [Nomor Port] ini terbuka?"*
Saya akan jelaskan dari sisi Hacker (cara masuknya) dan sisi SOC (cara menutupnya).

---

# Stage #03

Luar biasa! Kamu sudah melewati tahap **Reconnaissance (Pengintaian)** dan **Network Analysis**. Sekarang kita akan masuk ke **Level 3: Vulnerability Analysis & System Hardening**.

Di level ini, fokusnya adalah: **Hacker** mencari titik lemah (vulnerabilities), sementara **SOC** belajar cara mendeteksi serangan dan memperkuat pertahanan.

Berikut adalah **Misi 9 sampai 12**:

---

### Misi 9: Web Vulnerability Scanning (Basic)
**Tujuan:** Mengenali kerentanan pada server web. Website adalah pintu masuk paling umum bagi peretas.

* **Tugas:**
    1. Gunakan alat bernama **Nikto** untuk memindai sebuah server (Gunakan target yang aman, contoh: `scanme.nmap.org`).
    2. Analisis apakah ada folder sensitif atau versi software yang usang.
* **Cara Mengerjakan:**
    * Ketik: `nikto -h http://scanme.nmap.org`
    * **Analisis SOC:** Jika kamu melihat pesan seperti "Server leaks inodes via ETags" atau "Obsolete PHP version", itu adalah celah yang harus segera diperbaiki oleh tim IT.

---

### Misi 10: Analisis Log Keamanan (Skill Wajib SOC)
**Tujuan:** Belajar mendeteksi jejak digital penyerang. Penyerang sering mencoba masuk lewat SSH (Brute Force).

* **Tugas:**
    1. Periksa file log aktivitas autentikasi di Kali Linux kamu.
    2. Cari apakah ada percobaan login yang gagal (failed login).
* **Cara Mengerjakan:**
    * Ketik: `sudo grep "Failed password" /var/log/auth.log`
    * **Analisis:** Jika perintah ini memunculkan banyak baris, artinya ada seseorang (atau bot) yang mencoba menebak password akunmu. SOC Analyst menggunakan data ini untuk memblokir IP penyerang.

---

### Misi 11: Privilege Escalation Awareness (Izin Akses)
**Tujuan:** Memahami konsep "Sudo" dan bagaimana hacker mencoba menjadi "Root" (Admin Tertinggi).

* **Tugas:**
    1. Cek perintah apa saja yang bisa dijalankan user kamu dengan hak akses `sudo` tanpa perlu password (atau yang diizinkan).
    2. Lihat daftar semua user yang ada di sistem yang memiliki akses ke *shell*.
* **Cara Mengerjakan:**
    * Ketik: `sudo -l` (melihat izin sudo kamu).
    * Ketik: `grep "/bin/bash" /etc/passwd` (melihat user mana saja yang bisa masuk ke terminal).

---

### Misi 12: Dasar Enkripsi & Hashing
**Tujuan:** Memahami bagaimana data dilindungi. Hacker mencoba memecahkan hash, SOC memastikan hash yang digunakan kuat.

* **Tugas:**
    1. Buat sebuah kalimat dalam file teks, lalu ubah menjadi **MD5 Hash**.
    2. Buat hash lain menggunakan **SHA-256** dari kalimat yang sama dan bandingkan perbedaannya.
* **Cara Mengerjakan:**
    * Ketik: `echo "password123" | md5sum`
    * Ketik: `echo "password123" | sha256sum`
    * **Analisis:** Perhatikan bahwa SHA-256 jauh lebih panjang dan lebih aman daripada MD5. Sebagai SOC, kamu harus tahu bahwa MD5 sudah tidak aman lagi untuk menyimpan password.

---

### Ringkasan Level 3
| Alat / File | Fungsi |
| :--- | :--- |
| **Nikto** | Web scanner untuk mencari celah dasar pada website. |
| **/var/log/auth.log** | "Kitab Suci" SOC untuk melihat siapa yang mencoba masuk ke sistem. |
| **sha256sum** | Memastikan integritas data (data tidak diubah oleh hacker). |

---

### Apa yang harus dilakukan sekarang?
1.  Selesaikan **Misi 9-12**.
2.  **Saran Penting:** Sekarang saatnya kamu menginstal **Metasploitable 2** di VMware kamu sebagai target legal.
3.  Jangan terus-menerus memindai website orang lain atau `scanme.nmap.org` agar tidak dianggap serangan nyata.

**Pertanyaan untukmu:** Apakah kamu sudah pernah mendengar tentang **Metasploit**? Itu adalah alat "Legendaris" di Kali Linux untuk mengeksekusi serangan.
Jika kamu sudah selesai dengan Misi 12, kita akan mulai belajar cara "masuk" ke sistem target secara legal. Beritahu saya jika sudah siap!

---

# Stage #4

Wah, keren! Kamu bergerak sangat cepat. Dengan adanya **Kali Linux** sebagai mesin penyerang (*Attacker*) dan **VM Target** (seperti Metasploitable) sebagai korban,
kamu sekarang punya laboratorium *cyber security* yang lengkap di komputermu sendiri.

Sekarang kita masuk ke **Level 4: Exploitation & Defense Monitoring**. Di sini kita akan menggabungkan peran **Ethical Hacker** (melakukan serangan) dan **SOC** (mendeteksi serangan tersebut).

---

### Misi 13: Eksploitasi Pertama dengan Metasploit
**Tujuan:** Memahami bagaimana sebuah celah keamanan digunakan untuk mengambil alih sistem.

* **Tugas:**
    1.  Cari layanan yang rentan di VM target menggunakan `db_nmap`.
    2.  Gunakan modul `exploit` untuk mendapatkan akses terminal (*shell*) ke VM target.
* **Cara Mengerjakan:**
    * Buka Metasploit: `msfconsole`.
    * Cari target: `db_nmap -sV [IP_VM_Target]`.
    * Jika kamu pakai Metasploitable, coba cari layanan bernama **VSFTPD 2.3.4**.
    * Ketik: `search vsftpd`.
    * Ketik: `use exploit/unix/ftp/vsftpd_234_backdoor`.
    * Atur target: `set RHOSTS [IP_VM_Target]`.
    * Eksekusi: `exploit`.
    * **Hasil:** Jika berhasil, kamu akan masuk ke dalam mesin target. Ketik `whoami` untuk melihat apakah kamu sudah jadi **root**.

---

### Misi 14: Post-Exploitation (Jejak Sang Hacker)
**Tujuan:** Mengetahui apa yang dilakukan hacker setelah berhasil masuk.

* **Tugas:**
    1.  Setelah masuk ke shell target (Misi 13), coba buat file "pesan" di folder `/tmp` target.
    2.  Coba ambil (download) file `/etc/shadow` dari target ke Kali kamu (file ini berisi hash password).
* **Cara Mengerjakan:**
    * Di shell target: `echo "Hacked by [Nama Kamu]" > /tmp/warning.txt`.
    * Lihat isi file: `cat /tmp/warning.txt`.
    * Ini mensimulasikan pencurian data atau perusakan (*defacement*).

---

### Misi 15: Analisis SOC (Mendeteksi Serangan Metasploit)
**Tujuan:** Sebagai SOC, kamu harus tahu seperti apa rupa serangan tadi di dalam jaringan.

* **Tugas:**
    1.  Ulangi serangan di Misi 13, tapi kali ini jalankan `tcpdump` di terminal Kali yang lain secara bersamaan.
    2.  Simpan lalu lintasnya ke file `.pcap` untuk dianalisis nanti di Wireshark.
* **Cara Mengerjakan:**
    * Di terminal baru (sebelum exploit): `sudo tcpdump -i eth0 host [IP_VM_Target] -w serangan.pcap`.
    * Jalankan exploit di Metasploit.
    * Berhenti (`Ctrl+C`) pada tcpdump setelah exploit selesai.
    * **Analisis:** Buka file tersebut dengan Wireshark: `wireshark serangan.pcap`. Lihat bagaimana paket FTP dikirimkan.

---

### Misi 16: Scanning Kerentanan Otomatis (OpenVAS / Nessus)
**Tujuan:** Belajar menggunakan alat standar industri untuk audit keamanan skala besar.

* **Tugas:**
    1.  Pelajari konsep *Vulnerability Assessment*.
    2.  Instal atau pelajari cara kerja **Legion** (alat GUI di Kali yang menggabungkan banyak scanner).
* **Cara Mengerjakan:**
    * Ketik di terminal: `legion`.
    * Masukkan IP VM Target dan biarkan dia bekerja secara otomatis mencari celah.
    * **Analisis SOC:** Bandingkan hasil Legion dengan hasil manual Nmap kamu. Mana yang lebih detail?

---

### Ringkasan Level 4
| Skill | Deskripsi |
| :--- | :--- |
| **Exploitation** | Menggunakan *Framework* Metasploit untuk menembus target. |
| **Data Exfiltration** | Mensimulasikan pencurian data sensitif setelah tembus. |
| **Forensics Dasar** | Merekam serangan menjadi file `.pcap` untuk barang bukti. |

---

### Apa Langkah Berikutnya?
Setelah kamu mencoba **Misi 13** dan berhasil mendapatkan akses `root` di VM target, rasanya pasti luar biasa. Tapi ingat, tantangan terbesarnya adalah: **"Bagaimana cara mencegahnya?"**

**Saran Belajar:**
Sekarang kamu sudah punya *skill* teknis dasar. Saya sangat menyarankan kamu mulai mencatat setiap misi ini di **GitHub Portfolio** yang sedang kamu bangun. Tuliskan:
1. Apa tujuannya?
2. Perintah apa yang kamu gunakan?
3. Apa hasilnya?

Apakah kamu mengalami kesulitan saat menghubungkan Kali Linux dengan VM Target di VMware? (Biasanya masalah di pengaturan Network *Bridge* atau *NAT*).

---

# Stage #05

Luar biasa! Kamu sudah sampai di tahap di mana kamu bisa melakukan eksploitasi dan merekam jejaknya. Ini adalah titik balik penting. Sekarang, kita akan masuk ke **Level 5: Blue Team Defense & Log Forensics**.

Di level ini, kita akan membalik meja. Kamu tidak lagi hanya fokus pada "cara masuk", tapi bagaimana seorang **SOC Analyst** mendeteksi serangan yang barusan kamu lakukan (Metasploit, Scanning, dll) agar bisa menghentikannya.

---

### Misi 17: Log Analysis Deep Dive (Mencari Jejak Penyerang)
**Tujuan:** Mengetahui perbedaan antara log aktivitas normal dan log saat serangan terjadi.

* **Tugas:**
    1.  Buka log sistem di VM Target (jika targetnya Linux) atau di Kali kamu sendiri.
    2.  Gunakan `grep` untuk mencari indikasi serangan "Reverse Shell" atau aktivitas ilegal.
* **Cara Mengerjakan:**
    * Ketik: `sudo tail -n 100 /var/log/syslog` (Melihat 100 aktivitas sistem terakhir).
    * Cari aktivitas mencurigakan: `grep -i "connection refused" /var/log/syslog` atau `grep -i "accepted" /var/log/auth.log`.
    * **Analisis SOC:** Perhatikan stempel waktu (*timestamp*). Jika ada puluhan login gagal dalam 1 detik, itu adalah serangan *Brute Force*.

---

### Misi 18: Menutup Celah (System Hardening)
**Tujuan:** Belajar menjadi "Dokter" bagi sistem yang sakit/rentan.

* **Tugas:**
    1.  Matikan layanan (service) yang tidak perlu di mesin target agar tidak bisa dieksploitasi lagi.
    2.  Gunakan Firewall sederhana (**UFW**) untuk menutup port tertentu.
* **Cara Mengerjakan:**
    * Cek layanan yang aktif: `systemctl list-units --type=service --state=running`.
    * Matikan layanan (misal FTP): `sudo systemctl stop vsftpd` dan `sudo systemctl disable vsftpd`.
    * Aktifkan Firewall: `sudo ufw enable` lalu `sudo ufw deny 21/tcp` (Menutup port FTP).

---

### Misi 19: Analisis Paket dengan Wireshark (Deep Packet Inspection)
**Tujuan:** Membedakan protokol yang aman dan yang berbahaya melalui lalu lintas data.

* **Tugas:**
    1.  Gunakan file `.pcap` yang kamu buat di Misi 15.
    2.  Cari paket yang berisi teks murni (*Cleartext*) seperti password.
* **Cara Mengerjakan:**
    * Buka Wireshark dan load file `serangan.pcap`.
    * Gunakan filter: `tcp.port == 21` (untuk FTP) atau `http`.
    * Klik kanan pada salah satu paket > **Follow** > **TCP Stream**.
    * **Analisis SOC:** Jika kamu bisa membaca username dan password di situ, artinya protokol tersebut tidak aman dan harus diganti ke SFTP atau HTTPS.

---

### Misi 20: Membuat Laporan Insiden (Incident Reporting)
**Tujuan:** Ini adalah tugas harian SOC Analyst yang paling penting. Kemampuan teknis tidak berguna jika tidak bisa dikomunikasikan ke atasan.

* **Tugas:**
    1.  Buat satu dokumen sederhana (bisa di `Leafpad` atau `Mousepad` di Kali) yang merangkum serangan di Misi 13.
* **Cara Mengerjakan (Gunakan format ini):**
    * **Ringkasan:** Terjadi eksploitasi pada layanan VSFTPD.
    * **Waktu:** (Lihat di log).
    * **Metode:** Remote Exploit menggunakan Metasploit.
    * **Dampak:** Penyerang mendapatkan akses *root*.
    * **Rekomendasi:** Update versi VSFTPD atau tutup port 21 dan gunakan SSH.

---

### Ringkasan Level 5
| Skill | Fokus Utama |
| :--- | :--- |
| **Defensive** | Menggunakan Firewall dan mematikan layanan berbahaya. |
| **Forensics** | Membaca log dan paket data untuk mencari bukti. |
| **Compliance** | Membuat laporan profesional sebagai hasil akhir kerja SOC. |

---

### Langkah Penutup untuk Menjadi SOC Analyst Level 1:
Setelah menyelesaikan Misi 20, kamu sudah melakukan siklus penuh: **Recon > Exploit > Detect > Fix > Report.**

**Tantangan Terakhir:**
Sekarang kamu punya banyak bahan. Apakah kamu sudah mulai memindahkan langkah-langkah perintah terminal ini ke dalam catatan permanen (seperti Notion, Obsidian, atau GitHub)?
Dokumentasi adalah kunci agar kamu tidak lupa perintah-perintah rumit di masa depan.

Mau saya bantu buatkan struktur *Readme* untuk GitHub kamu agar terlihat profesional di mata perekrut kerja nantinya?

# Stage #06

Wah, progres kamu sangat pesat! Kamu sudah menyelesaikan siklus teknis dari penyerangan hingga pelaporan. Sekarang kita masuk ke **Level 6: Automation, Scripting, & Security Monitoring**.

Di level ini, kita fokus pada **efisiensi**. Seorang SOC Analyst atau Ethical Hacker profesional tidak bekerja secara manual satu per satu, tapi menggunakan *script* untuk mempercepat pekerjaan.

---

### Misi 21: Automasi Bash Scripting (Tool Buatan Sendiri)
**Tujuan:** Membuat alat pemindai jaringan sederhana sendiri agar tidak perlu mengetik perintah panjang berulang kali.

* **Tugas:**
    1. Buat sebuah script Bash yang otomatis melakukan `ping` ke target dan menjalankan `nmap` jika target tersebut aktif.
* **Cara Mengerjakan:**
    * Buka terminal, ketik `nano pindaiku.sh`.
    * Masukkan kode sederhana ini:
      ```bash
      #!/bin/bash
      echo "Masukkan IP Target:"
      read target
      ping -c 1 $target > /dev/null
      if [ $? -eq 0 ]; then
          echo "Target aktif! Memulai scanning..."
          nmap -sV $target
      else
          echo "Target tidak merespons."
      fi
      ```
    * Simpan (`Ctrl+O`, `Enter`, `Ctrl+X`).
    * Beri izin eksekusi: `chmod +x pindaiku.sh`.
    * Jalankan: `./pindaiku.sh`.

---

### Misi 22: Pengenalan SIEM Dasar (Log Watcher)
**Tujuan:** Belajar memantau log secara otomatis tanpa harus membukanya manual. Ini adalah simulasi kecil dari sistem **SIEM (Security Information and Event Management)**.

* **Tugas:**
    1. Gunakan perintah `watch` untuk memantau perubahan pada file log secara *real-time*.
* **Cara Mengerjakan:**
    * Ketik: `watch -n 1 "tail -n 5 /var/log/auth.log"`.
    * Sambil perintah itu berjalan, buka terminal baru dan coba lakukan `sudo` dengan password yang salah sengaja.
    * Lihat bagaimana terminal pertama menangkap aktivitas tersebut secara otomatis.

---

### Misi 23: Password Cracking (Lab Keamanan)
**Tujuan:** Memahami mengapa kebijakan password yang kuat itu penting. Hacker menggunakan ini, SOC memastikan user tidak pakai password lemah.

* **Tugas:**
    1. Gunakan **John the Ripper** untuk mencoba memecahkan hash password yang kamu buat sendiri di Misi 12.
* **Cara Mengerjakan:**
    * Simpan sebuah hash ke file: `echo "teks_hash_kamu" > hash_target.txt`.
    * Jalankan: `john hash_target.txt`.
    * **Analisis SOC:** Jika password berhasil pecah dalam hitungan detik, artinya password tersebut terlalu sederhana.

---

### Misi 24: Audit Keamanan Sistem dengan Lynis
**Tujuan:** Melakukan audit otomatis pada sistem Linux untuk menemukan lubang keamanan yang terlewat.

* **Tugas:**
    1. Jalankan audit sistem secara menyeluruh pada mesin Kali kamu atau VM target.
* **Cara Mengerjakan:**
    * Instal jika belum ada: `sudo apt install lynis`.
    * Jalankan audit: `sudo lynis audit system`.
    * **Analisis SOC:** Scroll ke bagian "Suggestions". Lynis akan memberitahu apa saja yang harus kamu perbaiki (misalnya: "Install a malware scanner" atau "Hardening SSH").

---

### Ringkasan Level 6
| Skill | Manfaat |
| :--- | :--- |
| **Bash Scripting** | Menghemat waktu dengan mengotomatiskan tugas rutin. |
| **SIEM Mentality** | Memantau sistem secara proaktif, bukan reaktif. |
| **Audit Otomatis** | Menemukan celah keamanan di seluruh sistem dalam sekali klik. |

---

### Apa Langkah Besar Berikutnya?
Setelah menyelesaikan Misi 24, kamu sudah memiliki kapabilitas teknis yang sangat baik untuk ukuran pemula. Langkah selanjutnya yang paling krusial bagi seseorang yang ingin bekerja sebagai **SOC Analyst** adalah:

**Membangun Lab Monitoring yang Lebih "Real":**
Saya sarankan kamu mulai melirik **Splunk** atau **ELK Stack (Elasticsearch, Logstash, Kibana)**. Itu adalah software standar industri yang digunakan SOC di perusahaan besar.

Bagaimana menurutmu? Apakah kamu ingin mencoba membuat *script* yang lebih kompleks, atau ingin saya tunjukkan cara mendokumentasikan semua hasil misi ini ke GitHub agar terlihat menarik bagi HRD?

# Stage #07

Luar biasa! Kamu sudah menyelesaikan 24 misi yang mencakup dasar terminal, networking, eksploitasi, hingga analisis log dan automasi. Ini adalah pencapaian yang sangat solid untuk membangun "otot" teknis.

Namun, jika yang kamu maksud dengan **"hunting"** adalah mencari kerentanan di sistem nyata (seperti *Bug Bounty*) atau bekerja sebagai **Threat Hunter** di SOC profesional, ada satu jembatan lagi yang harus kamu seberangi.

Dalam dunia profesional, teknik yang kamu pelajari disebut **"Known Vulnerabilities"** (kerentanan yang sudah diketahui). Untuk benar-benar terjun ke lapangan, kamu perlu menguji mental dan instingmu di skenario yang tidak terpandu.

Berikut adalah **Misi Level 7 (The Bridge to Hunting)** yang akan menentukan apakah kamu benar-benar siap:

---

### Misi 25: Capture The Flag (CTF) - Ujian Mental
**Tujuan:** Menguji apakah kamu bisa menemukan jalan masuk tanpa diberi tahu "caranya" (seperti di misi-misi sebelumnya).

* **Tugas:** Buka [VulnHub](https://www.vulnhub.com/) atau [TryHackMe](https://tryhackme.com/). Pilih mesin kategori "Easy" (Contoh: *Kioptrix* atau *Pickle Rick*).
* **Target:** Dapatkan file `root.txt` atau `flag.txt` di dalam mesin tersebut tanpa bantuan tutorial (walkthrough).
* **Mengapa ini penting?** Hunting memerlukan kreativitas. Jika kamu hanya mengikuti instruksi, kamu adalah operator. Jika kamu bisa menemukan jalan sendiri, kamu adalah *Hunter*.

---

### Misi 26: Threat Hunting (Mendeteksi yang Tak Terlihat)
**Tujuan:** Sebagai SOC, kamu harus bisa mendeteksi serangan yang lebih "halus" daripada Metasploit.

* **Tugas:** Gunakan **Snort** atau **Suricata** (Intrusion Detection System) di Kali Linux kamu.
* **Cara Mengerjakan:**
    1.  Instal Snort: `sudo apt install snort`.
    2.  Jalankan Snort untuk memantau trafik.
    3.  Lakukan *Stealth Scan* dari mesin lain: `nmap -sS [IP_Kali]`.
    4.  Cek apakah Snort berhasil menangkap *alert* serangan tersebut.
* **Analisis SOC:** Hunter tidak menunggu laporan, mereka mencari anomali di trafik yang terlihat "normal".

---

### Misi 27: OSINT (Open Source Intelligence)
**Tujuan:** Mencari informasi tanpa menyentuh target sama sekali. Ini adalah tahap awal sebelum "hunting".

* **Tugas:** Gunakan alat **TheHarvester** atau **Maltego** di Kali Linux.
* **Cara Mengerjakan:**
    1.  Ketik: `theHarvester -d [nama_domain_perusahaan_publik] -l 500 -b google`.
    2.  Lihat apakah kamu bisa menemukan alamat email karyawan atau sub-domain yang tersembunyi.
* **Risiko:** Ini adalah data publik, tapi bagi seorang Hunter, ini adalah peta jalan.

---

### Apakah kamu sudah siap?
**Coba jawab 3 pertanyaan ini untuk dirimu sendiri:**
1.  Apakah kamu bisa menjelaskan perbedaan antara **TCP** dan **UDP** tanpa melihat catatan?
2.  Jika kamu melihat log `403 Forbidden` yang muncul 1000x dalam 1 menit, apa yang sedang terjadi?
3.  Apakah kamu sudah merasa nyaman bekerja di terminal selama 2-3 jam tanpa menyentuh mouse?

**Saran Saya:**
Jika jawabannya "Ya", kamu siap untuk mencoba **Bug Bounty Program** (seperti di HackerOne atau Bugcrowd) pada kategori *VDP (Vulnerability Disclosure Policy)* yang legal.

**Apa yang ingin kamu coba sekarang?**
Apakah kamu ingin saya pandu memilih mesin CTF pertama untuk membuktikan kemampuanmu, atau ingin memperdalam **OSINT** agar bisa "berburu" informasi target?

---
