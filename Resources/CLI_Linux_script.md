# Kumpulan Command-Promt / Command-Lina Interface (CLI) Linux

Untuk menguasai CLI Linux, Anda harus berhenti menggunakan mouse dan mulai melakukan segala aktivitas melalui terminal. Fokuslah pada hierarki sistem file dan manipulasi teks karena di Linux, **semua adalah file**.

### Langkah Praktis Penguasaan CLI

| **Fungsi** | **Script** |
| --- | --- |
| **Navigasi Dasar:** | `pwd` (cek posisi), `ls -la` (list file tersembunyi), dan `cd` (pindah direktori). |
| **Manajemen File:** | `mkdir` (buat folder), `touch` (buat file), `cp` (salin), `mv` (pindah/ganti nama), dan `rm` (hapus). |
| **Intip Isi File:** | `cat`, `less`, atau `tail -f` untuk melihat log secara *real-time*. |
| **Izin Akses (Penting!):** | `chmod` untuk mengubah izin file dan `chown` untuk kepemilikan. |
| **Pencarian & Filter:** | `grep` untuk mencari kata, `find` untuk mencari file, dan **Piping (`|`)** untuk menghubungkan satu perintah ke perintah lain. |

### Tips Mempercepat Jam Terbang

1. **Gunakan `man <perintah>`:** Ini adalah buku manual internal. Jika bingung cara pakai `nmap`, ketik `man nmap`.
2. **Tab Completion:** Selalu gunakan tombol **Tab** untuk melengkapi nama file atau perintah secara otomatis agar tidak salah ketik.
3. **Hapus GUI:** Jika menggunakan VM, coba masuk ke mode *headless* (tanpa tampilan grafis) agar Anda terpaksa menggunakan CLI.

---

# CLI Intensif Guide for SOC
Rencana belajar intensif selama 4 minggu untuk menguasai CLI Linux, yang dirancang khusus untuk memperkuat fondasi Anda menuju karier **SOC Analyst**.

### **Minggu 1: Navigasi & Manipulasi File (Dasar)**

Fokus minggu ini adalah membiasakan diri bergerak di dalam sistem tanpa menggunakan mouse.

| Perintah | Fungsi | Kegunaan dalam Keamanan |
| --- | --- | --- |
| **`pwd`** | Menampilkan direktori kerja saat ini. | Memastikan posisi Anda sebelum menjalankan perintah sensitif. |
| **`ls -la`** | List file (termasuk yang tersembunyi). | Melihat file mencurigakan yang diawali tanda titik (`.`). |
| **`cd`** | Berpindah direktori. | Berpindah ke folder konfigurasi sistem atau log. |
| **`mkdir`** & **`touch`** | Membuat folder dan file baru. | Menyiapkan folder untuk menyimpan hasil scan/analisis. |
| **`cp`**, **`mv`**, **`rm`** | Salin, pindah, hapus file. | Mengelola data dan menghapus jejak (jika diperlukan). |

**Latihan:** Buat struktur folder `Lab/Analisis/Log`, buat file kosong di dalamnya, lalu pindahkan file tersebut ke folder `Analisis`.

---

### **Minggu 2: Membaca & Mengolah Teks (Krusial bagi SOC)**

Seorang analis banyak menghabiskan waktu membaca file log yang sangat besar. Perintah ini wajib dikuasai.

| Perintah | Fungsi | Kegunaan dalam Keamanan |
| --- | --- | --- |
| **`cat`**, **`less`** | Membaca isi file. | Memeriksa isi skrip atau file teks kecil. |
| **`head`** & **`tail -f`** | Lihat awal/akhir file (real-time). | **Sangat penting!** Memantau log sistem secara langsung. |
| **`grep`** | Mencari kata kunci tertentu. | Mencari IP penyusup di dalam ribuan baris log. |
| **`find`** & **`locate`** | Mencari lokasi file. | Menemukan letak file konfigurasi yang tidak diketahui. |
| **`nano`** / **`vim`** | Text Editor berbasis CLI. | Mengedit file konfigurasi server atau membuat skrip. |

**Latihan:** Buka file log sistem (`/var/log/syslog`), gunakan `grep` untuk mencari kata "error" atau "failed".

---

### **Minggu 3: Manajemen Sistem & Izin Akses**

Minggu ini Anda belajar mengontrol siapa yang boleh mengakses apa di dalam sistem.

| Perintah | Fungsi | Kegunaan dalam Keamanan |
| --- | --- | --- |
| **`sudo`** | Menjalankan perintah sebagai admin. | Menjalankan alat penetrasi atau mengedit sistem. |
| **`chmod`** | Mengubah izin akses file (777, 644, dll). | Mengamankan file sensitif agar tidak bisa dibaca orang lain. |
| **`chown`** | Mengubah pemilik file. | Memperbaiki hak akses setelah melakukan pemindahan data. |
| **`ps aux`** & **`top`** | Melihat proses yang sedang berjalan. | Mendeteksi apakah ada virus atau malware yang berjalan. |
| **`kill`** | Menghentikan proses secara paksa. | Mematikan koneksi atau malware yang mencurigakan. |

**Latihan:** Buat sebuah file, ubah izinnya agar hanya Anda yang bisa membaca (menggunakan `chmod 400`), lalu coba baca file tersebut tanpa `sudo`.

---

### **Minggu 4: Jaringan & Troubleshooting (Expert)**

Sebagai calon SOC Analyst, perintah jaringan adalah "senjata" utama Anda.

| Perintah | Fungsi | Kegunaan dalam Keamanan |
| --- | --- | --- |
| **`ip a`** | Melihat alamat IP dan interface. | Mengetahui IP sendiri sebelum melakukan scan jaringan. |
| **`ping`** | Mengecek koneksi ke host lain. | Memastikan target sedang aktif (up). |
| **`netstat`** / **`ss`** | Melihat koneksi jaringan yang aktif. | Melihat port mana yang terbuka dan siapa yang terhubung. |
| **`ssh`** | Remote akses ke komputer lain. | Mengakses server target secara aman melalui terminal. |
| **`curl`** & **`wget`** | Mengunduh file dari internet. | Mengunduh alat eksploitasi atau skrip analisis. |

**Latihan:** Gunakan `ss -tunlp` untuk melihat port apa saja yang sedang terbuka di Kali Linux Anda.

---

### **Tips Agar Mahir dalam 4 Minggu:**

1. **Haramkan Mouse:** Selama belajar, sebisa mungkin jangan menyentuh mouse. Gunakan `Tab` untuk melengkapi nama file otomatis (*Auto-complete*).
2. **Gunakan TryHackMe:** Selesaikan Room **"Linux Fundamentals"** (Part 1-3). Ini akan memberikan Anda praktik langsung yang sangat baik.
3. **Catat di GitHub:** Dokumentasikan setiap perintah yang Anda pelajari dalam file `README.md` di GitHub Anda. Ini akan menjadi portofolio yang sangat bagus bagi perekrut.

---

# CLI Intensif Gued for Ethical Hacker

Sebagai seorang **Ethical Hacker** atau *Infiltrator*, terminal adalah pusat kendali Anda. Jika perintah SOC Analyst lebih banyak bersifat **defensif** (membaca log dan memantau), perintah *Offensive* fokus pada **pengumpulan informasi, eksploitasi, dan menjaga akses**.

Berikut adalah daftar perintah CLI yang harus Anda kuasai untuk mengoperasikan alat-alat di Kali Linux, disusun berdasarkan tahapan serangan (Kill Chain):

---

### **1. Tahap Reconnaissance & Enumeration (Pengumpulan Informasi)**

Ini adalah tahap paling krusial. Anda harus tahu apa yang ada di dalam jaringan sebelum menyerang.

| Perintah | Alat | Kegunaan |
| --- | --- | --- |
| **`sudo nmap -sC -sV [IP]`** | **Nmap** | Melakukan scan port dengan skrip default dan deteksi versi layanan. |
| **`dirsearch -u [URL]`** | **Dirsearch** | Mencari folder atau file rahasia yang tersembunyi di sebuah website. |
| **`enum4linux -a [IP]`** | **Enum4linux** | Mengambil informasi detail dari perangkat Windows/SMB (username, share, dll). |
| **`whatweb [URL]`** | **WhatWeb** | Mengidentifikasi teknologi yang digunakan website (CMS, versi PHP, server). |

---

### **2. Tahap Exploitation (Penetrasi)**

Setelah menemukan celah, perintah ini digunakan untuk masuk ke dalam sistem target.

| Perintah | Alat | Kegunaan |
| --- | --- | --- |
| **`msfconsole`** | **Metasploit** | Membuka framework eksploitasi paling populer di dunia. |
| **`searchsploit [keyword]`** | **ExploitDB** | Mencari kode eksploitasi secara offline di database Kali Linux. |
| **`sqlmap -u [URL] --dbs`** | **SQLMap** | Melakukan injeksi database secara otomatis untuk mengambil data sensitif. |
| **`hydra -l user -P pass.txt [IP] ssh`** | **Hydra** | Melakukan *brute force* (tebak password) secara cepat pada layanan SSH/FTP. |

---

### **3. Tahap Privilege Escalation (Meningkatkan Akses)**

Biasanya saat berhasil masuk, Anda hanya menjadi user biasa. Perintah ini membantu Anda menjadi **Root/Admin**.

| Perintah | Fungsi | Kegunaan |
| --- | --- | --- |
| **`sudo -l`** | Cek Privilese | Melihat perintah apa yang bisa dijalankan user Anda sebagai Root tanpa password. |
| **`find / -perm -u=s -type f`** | Cari SUID | Mencari file yang memiliki izin khusus yang bisa disalahgunakan untuk jadi Root. |
| **`uname -a`** | Informasi Kernel | Mengecek versi Kernel Linux untuk mencari celah *Dirty Pipe* atau *Dirty Cow*. |

---

### **4. Tahap Post-Exploitation & Lateral Movement**

Tahap setelah sistem dikuasai untuk mengambil data atau berpindah ke komputer lain di jaringan.

| Perintah | Alat | Kegunaan |
| --- | --- | --- |
| **`nc -nlvp [Port]`** | **Netcat** | Membuka "pintu belakang" (listener) untuk menerima koneksi *Reverse Shell*. |
| **`scp [file] user@[IP]:/path`** | **SCP** | Mencuri file dari komputer korban ke komputer Anda melalui jalur SSH. |
| **`hashcat -m 0 hash.txt dict.txt`** | **Hashcat** | Memecahkan hash password yang berhasil Anda curi dari database. |

---

### **Rencana Belajar 4 Minggu (Mode Infiltrator)**

1. **Minggu 1: Network Scanning Mastery**
* Kuasai **Nmap** secara mendalam (berbagai jenis flag seperti `-sU`, `-Pn`, `-O`).
* Latihan: Scan VM target (seperti Metasploitable) dan petakan semua port yang terbuka.

2. **Minggu 2: Web & Vulnerability Research**
* Belajar menggunakan **Nikto**, **Dirsearch**, dan **Searchsploit**.
* Latihan: Cari versi layanan yang berjalan di target dan cari celah keamanannya di Google/ExploitDB.

3. **Minggu 3: Exploitation Framework**
* Fokus pada **Metasploit (`msfconsole`)**. Belajar cara memilih *exploit*, mengatur *payload*, dan melakukan *exploit*.
* Latihan: Coba dapatkan shell pada mesin latihan di TryHackMe.

4. **Minggu 4: Password Attacks & Sniffing**
* Belajar **John the Ripper** atau **Hashcat** untuk pecah password, dan **Bettercap** untuk memutus/mengintip jaringan.
* Latihan: Buat file teks berisi password acak dan coba pecahkan menggunakan daftar kata (*wordlist*).

## cara membedakan perangkat asli dan perangkat virtual hanya lewat CLI

Membezakan antara peranti fizikal (asli) dan peranti virtual melalui CLI adalah kemahiran penting untuk memastikan siapa yang berada di dalam rangkaian anda. Cara yang paling tepat adalah dengan menganalisis **MAC Address** dan **TTL (Time to Live)**.

Berikut adalah teknik-teknik yang boleh anda gunakan menggunakan **Nmap** di Kali Linux:

### 1. Mengenal Pasti Melalui OUI (Organizationally Unique Identifier)

Setiap kad rangkaian mempunyai MAC Address yang unik. 3 bait pertama (6 digit pertama) MAC Address menunjukkan pengeluar perkakasan tersebut.

Gunakan arahan ini:
`sudo nmap -sP 192.168.1.0/24`

**Cara Membacanya:**

* **Peranti Virtual:** Jika anda melihat pengeluar seperti **VMware**, **Oracle VirtualBox**, atau **Microsoft Hyper-V**, itu sah peranti virtual.
* **Peranti Asli:** Jika anda melihat nama seperti **Samsung**, **Apple**, **TP-Link**, atau **Intel**, itu adalah peranti fizikal (telefon atau laptop keluarga).

### 2. Teknik OS Detection (Fingerprinting)

Nmap mempunyai pangkalan data yang luas untuk meneka sama ada sistem itu berjalan di atas perkakasan sebenar atau lapisan virtual.

Gunakan arahan:
`sudo nmap -O [IP_Target]`

**Hasil yang perlu diperhatikan:**

* Nmap biasanya akan menyatakan secara spesifik: *"Device type: general purpose | OS details: Linux 5.x (VirtualBox)"*.
* Jika ia adalah peranti asli, ia akan menunjukkan model yang lebih spesifik seperti *"Google Android 11"* atau *"Apple iOS 14"*.

### 3. Analisis TTL (Time to Live)

TTL adalah nilai dalam paket data yang menunjukkan berapa banyak "lompatan" (hops) yang boleh dilalui paket tersebut. Peranti virtual sering kali mempunyai nilai TTL yang berbeza daripada peranti fizikal semasa tindak balas.

Gunakan arahan:
`sudo nmap -sn --traceroute [IP_Target]`

* Jika `traceroute` menunjukkan hanya **1 hop** tetapi peranti tersebut berkelakuan pelik (latensi sangat rendah, di bawah 1ms), ada kemungkinan ia adalah VM yang berjalan di dalam komputer anda sendiri (Host-Only/NAT).

---

### Cara Membezakan Peranti Sendiri vs Penyusup

Untuk mengenali peranti keluarga di rumah, anda boleh menggunakan strategi **"White-listing"**:

1. **Imbas semasa semua orang ada di rumah:**
Jalankan scan dan catat semua MAC Address peranti keluarga (HP Isteri, Laptop Anak, dsb).
`sudo nmap -sP 192.168.1.0/24 > senarai_peranti_sah.txt`
2. **Bandingkan dengan Vendor:**
* **Penyusup:** Jika anda nampak IP dengan vendor **"Espressif Inc"** tetapi anda tidak mempunyai peranti Smart Home (lampu pintar/CCTV), itu mungkin penyusup yang menggunakan modul Wi-Fi murah.
* **Penyusup Virtual:** Jika anda nampak vendor **"VMware"** tetapi anda tidak menjalankan sebarang Lab, itu mungkin seseorang sedang melakukan serangan menggunakan Kali Linux dari dalam laptop mereka.

### Latihan CLI:

Cuba jalankan arahan ini untuk melihat peranti di sekitar anda sekarang:
`sudo nmap -sn -PR 192.168.1.0/24`
*(Flag `-PR` menggunakan ARP request, sangat pantas dan tepat untuk rangkaian lokal).*

---

## Rangkuman CLI yang sering dipakai

| Perintah | Fungsi | Kegunaan dalam Keamanan |
| --- | --- | --- |
| **`pwd`** | Menampilkan direktori kerja saat ini. | Memastikan posisi Anda sebelum menjalankan perintah sensitif. |
| **`ls -la`** | List file (termasuk yang tersembunyi). | Melihat file mencurigakan yang diawali tanda titik (`.`). |
| **`cd`** | Berpindah direktori. | Berpindah ke folder konfigurasi sistem atau log. |
| **`echo`** | Membuat teks | menulis teks yg bisa langsung dibuatkan dalam file .txt, atau sekedar print teks |
| **`whoami`** | melihat username server | mengetahui server siapa yang sedang digunakan |
| **`cat`** | membaca file | concatenate membuka file dan melihat isinya |
| **`find -name (nama file yg dicari)`** | mencari lokasi direktori dari file yang dicari | melihat lokasi file secara urutan direktori, jika `find -name *.txt` artinya mencari file-file semua file yg .txt di di rektory tersebut |
| **`wc -l (nama file)`** | melihat baris pada file .txt | melihat jumlah baris agar tidak langsung banyak membukanya jika file barinya banyak |
| **`grep ("kata yg dicari")`** | mencari kata yg di cari dalam suatu file | jika memakai -R (recursive) maka jadi `grep -R ("kata yg dicari")` atau `grep -R ("lata yg dicari") /etc/` akan mencari di semua direktori dan subdirektory |
| **`>`** | memasukan kata ke dalam file | echo hello > note (txt) = akan mereplace semua kata di note.txt menjadi hello |
| **`>>`** | menambahkan kata ke dalam file | echo dunia >> note (txt) = maka akan menambahakan kata dunia ke dalam file txt note tanpa menghilangkan kata yang sudah ada di dalamnya |
| **`touch`** | touch	Create fil | membuat file di direktory |
| **`mkdir`** | make directory untuk Create a folder | membuat folder di direktory, `mkdir folder4` akan menjadi folder4 |
| **`cp`** | Copy a file or folde | melakukan copy `cp note.txt` |
| **`mv`** | Move a file or folder | memindahkan file atau folder ke tempat yang di tuju, `mv catatan folder4` memindahkan file catatan ke folder folder4 |
| **`rm`** | Remove a file or folder | melakukan penghapusan file atau folder, `mr catatan` akan menghapus file catatan, `mr *` akan menghapus semua file di folder yg ditempati |
| **`file`** | Determine the type of a file | untuk melihat jenis file yang disebut, `file catatan` maka akan muncul hasilnya `catatan.txt` karena formatnya .txt, `file -l` akan membuka semua jenis file di direktory tersebut |

