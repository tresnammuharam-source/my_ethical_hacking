# DI File ini belajar Nmap dari basic hingga advance dalam rangkumannya

<img width="1296" height="697" alt="image" src="https://github.com/user-attachments/assets/39a49f75-a93c-416a-933d-f1dce78e8b85" />

<img width="1172" height="404" alt="image" src="https://github.com/user-attachments/assets/c6dee4ce-e2ff-46f4-aa52-151ead574e39" />

<img width="1245" height="402" alt="image" src="https://github.com/user-attachments/assets/a4fafd89-237d-4882-8f20-c950a0c01954" />

<img width="1245" height="343" alt="image" src="https://github.com/user-attachments/assets/8a9350fa-213f-4f96-b33f-12f04532fcae" />

<img width="1252" height="279" alt="image" src="https://github.com/user-attachments/assets/e03f1dd2-070e-4716-8180-90cd05ac42ba" />

## summary

<img width="1010" height="802" alt="image" src="https://github.com/user-attachments/assets/b4b3e078-6a00-4272-b4dd-eb909b2bcc93" />

<img width="998" height="870" alt="image" src="https://github.com/user-attachments/assets/4f826b3a-dacf-4230-9809-5256fc0852f9" />

---

# How to create with namp

Perintah cepat Nmap:
<img width="743" height="499" alt="image" src="https://github.com/user-attachments/assets/576c2422-c340-4d21-a3d3-5a0357fe7b7b" />

Nmap (Network Mapper) adalah salah satu *tools* paling kuat dalam dunia keamanan siber yang digunakan untuk eksplorasi jaringan, manajemen aset, dan audit keamanan.

Untuk bisa menggunakannya dengan leluasa, kamu harus paham bahwa Nmap bekerja seperti seorang kurir yang mengetuk pintu-pintu di sebuah gedung (IP Address) untuk melihat siapa yang ada di dalam, pintu mana yang terbuka (Port), dan layanan apa yang sedang berjalan.

Berikut adalah penjelasan mendalam mengenai struktur, metode, flag spesifik, hingga penerapannya.

---

## 1. Struktur Anatomi Perintah Nmap

Secara umum, perintah Nmap ditulis dengan struktur berikut:
`nmap [Jenis Scan/Flag] [Opsi Tambahan] [Target]`

Flag atau argumen dalam Nmap biasanya sensitif terhadap huruf besar dan kecil (*case-sensitive*). Kombinasi huruf ini memiliki arti yang sangat spesifik.

---

## 2. Membedah Flag: `-Pn` dan `-sn`

Mari kita bedah pertanyaanmu tentang arti dari huruf-huruf di dalam flag Nmap. Secara garis besar, **huruf pertama (huruf kecil) biasanya menentukan *kategori* tindakan, dan huruf kedua menentukan *metode* spesifiknya.**

### **A. Flag `-Pn` (No Ping)**

Jika kamu menjalankan `nmap -Pn [IP_Address]`:

* **Arti Huruf:**
* `P` kepanjangannya adalah **Ping**.
* `n` di sini berarti **No** atau **Skip**.


* **Fungsinya:** Memerintahkan Nmap untuk **melewati tahap *host discovery* (ping)** dan langsung melakukan *port scanning*. Nmap akan menganggap target dalam keadaan aktif (*alive*), bahkan jika target tidak merespons ping.
* **Tujuannya:** Secara default, Nmap akan mengirimkan paket ping (ICMP, dll) terlebih dahulu. Jika target tidak merespons ping, Nmap akan berhenti dan menganggap target mati. Namun, banyak *firewall* modern yang memblokir paket ping ini demi keamanan. Flag `-Pn` digunakan untuk menembus kondisi tersebut.
* **Digunakan saat apa?** Ketika kamu tahu targetnya aktif, tetapi hasil scan biasa mengatakan target tersebut mati (*down*). Ini sangat sering digunakan saat melakukan penetrasi pada jaringan yang dilindungi *firewall* ketat.

### **B. Flag `-sn` (Ping Scan / No Port Scan)**

Jika kamu menjalankan `nmap -sn [IP_Address/Subnet]`:

* **Arti Huruf:**
* `s` kepanjangannya adalah **Scan type** (Jenis Scan).
* `n` di sini berarti **No port scan**.


* **Fungsinya:** Kebalikan dari `-Pn`. Flag `-sn` hanya melakukan **Host Discovery (Ping)** untuk melihat perangkat mana saja yang aktif di jaringan, tanpa melakukan scan port sama sekali.
* **Tujuannya:** Untuk memetakan jaringan dengan sangat cepat tanpa membuang waktu memeriksa ribuan port di setiap perangkat.
* **Digunakan saat apa?** Saat kamu baru masuk ke sebuah jaringan baru dan ingin tahu, *"Ada perangkat apa saja sih yang sedang terhubung di jaringan ini sekarang?"*

---

## 3. Metode dan Penerapan Kasus Nyata

### **A. Scan IP Target Biasa**

**Perintah Standar:**

```bash
nmap 192.168.1.50

```

* **Kenapa perintahnya seperti itu?** Karena tanpa flag tambahan, Nmap akan menjalankan mode defaultnya. Nmap akan mengirim ping untuk memastikan IP tersebut aktif, lalu melakukan scan pada **1.000 port paling populer/sering digunakan** secara otomatis menggunakan metode *SYN Scan* (jika kamu *root*) atau *TCP Connect Scan*.
* **Kapan dikembangkan lagi?** Jika kamu ingin memeriksa **semua** port (total ada 65.535 port), kamu menambahkan flag `-p-`:
```bash
nmap -p- 192.168.1.50

```



### **B. Scan Router / Gateway**

Router adalah gerbang utama jaringan. Biasanya router memiliki IP pertama dalam subnet (misal: `192.168.1.1`).

**Perintah yang Disarankan:**

```bash
nmap -sV -O -p 21,22,23,53,80,443,8080 192.168.1.1

```

* **Kenapa perintahnya seperti itu?**
* Router biasanya membuka port spesifik untuk manajemen, seperti port `80`/`443` (Web Dashboard), `22` (SSH), atau `23` (Telnet). Menentukan port spesifik (`-p ...`) membuat scan jauh lebih cepat.
* **`-sV` (Service Version):** Router sering kali memiliki celah keamanan pada *firmware*-nya. Flag ini menyuruh Nmap menebak versi software/firmware yang berjalan pada port tersebut.
* **`-O` (Operating System):** Flag ini mencoba menebak sistem operasi atau jenis router (misal: MikroTik, Cisco, TP-Link) berdasarkan respon paketnya.



---

## Summary: Contekan Cepat untuk Pemula

Agar kamu lebih leluasa, ingat kombinasi dasar ini:

| Flag | Kepanjangan/Arti | Fungsi Utama |
| --- | --- | --- |
| **`-sS`** | *SYN Scan* | Scan paling populer, cepat, dan relatif tidak terlihat (*stealth*). |
| **`-sT`** | *Connect Scan* | Digunakan jika kamu tidak punya akses *root* di Kali Linux. |
| **`-sV`** | *Version Detection* | Mengetahui versi aplikasi/layanan yang berjalan di port. |
| **`-O`** | *OS Detection* | Mengetahui Sistem Operasi target. |
| **`-A`** | *Aggressive Scan* | Gabungan dari `-O`, `-sV`, `-sC` (script), dan *traceroute* sekaligus. |
| **`-v`** | *Verbose* | Menampilkan proses scan secara langsung di layar saat berjalan (*real-time*). |

**Contoh Perintah "Sakti" untuk Analisis Mendalam:**

```bash
nmap -p- -sV -sC -O -v 192.168.1.50

```

*Perintah di atas akan memeriksa semua port (`-p-`), mencari versinya (`-sV`), menjalankan script skan dasar (`-sC`), mendeteksi OS (`-O`), dan menampilkan prosesnya secara mendetail (`-v`).*

```
