# CYBER CHEF

Tentu, ini pilihan yang sangat cerdas. **CyberChef** sering disebut sebagai *"The Cyber Swiss Army Knife"* (Pisau Lipat Swiss-nya Cyber).

Jika Anda belajar SOC dan SIEM, CyberChef adalah alat yang akan paling sering Anda gunakan untuk membongkar "bungkus" dari sebuah serangan yang terekam di log.

---

### 1. Apa itu CyberChef?

CyberChef adalah aplikasi web sederhana namun sangat kuat yang digunakan untuk melakukan segala jenis operasi data: enkripsi, dekripsi, kompresi, dekompresi, analisis log, hingga pembersihan data (*data munging*).

Dibuat oleh **GCHQ** (Badan Intelijen Inggris), alat ini dirancang agar analis tidak perlu menulis skrip Python atau mencari alat *online* yang berbeda-beda hanya untuk mengubah format data.

### 2. Konsep Utama: "The Recipe" (Resep)

Cara kerja CyberChef sangat intuitif karena menggunakan logika "Dapur":

1. **Input:** Data mentah yang ingin Anda analisis (misal: kode aneh yang ditemukan di log SIEM).
2. **Operations:** Daftar alat (seperti *Base64*, *Hex*, *URL Decode*, *Extract IP*).
3. **Recipe:** Anda menarik dan melepaskan (*drag & drop*) alat ke area resep. Anda bisa menumpuk banyak alat sekaligus.
4. **Output:** Hasil akhir setelah data melewati semua proses di resep.

---

### 3. Mengapa CyberChef Penting untuk SOC Analyst?

Dalam dunia nyata, penyerang sering menyembunyikan aktivitas mereka agar tidak terbaca oleh sistem keamanan sederhana. CyberChef membantu Anda "melihat" apa yang sebenarnya terjadi.

**Contoh Skenario:**
Anda melihat log di SIEM yang mencurigakan seperti ini:
`powershell.exe -e JABjAGwAaQBlAG4AdAAgAD0A...` (kode panjang dan acak).

Dengan CyberChef, Anda bisa:

* Menggunakan operasi **From Base64** untuk mengubahnya jadi teks.
* Menggunakan **Remove Null Bytes** untuk membersihkan spasi antar huruf.
* **Hasilnya:** Anda bisa membaca skrip asli yang sedang mencoba mencuri data Anda.

---

### 4. Fitur-Fitur Andalan untuk Belajar SOC

Berikut adalah beberapa fungsi yang wajib Anda coba di CyberChef:

* **Data Extraction:** Bisa mengambil semua alamat IP, Email, atau URL secara otomatis dari tumpukan teks log yang berantakan menggunakan fitur *Extract IP Addresses*.
* **Decoding:** Mengubah data dari format Base64, Hex, Octal, atau Morse kembali ke teks biasa.
* **Deobfuscation:** Membongkar kode JavaScript atau PowerShell yang sengaja dibuat rumit oleh peretas agar tidak terdeteksi antivirus.
* **Networking:** Mengonversi alamat IP dari format Hex ke Desimal atau sebaliknya.

---

### 5. Cara Akses di Kali Linux

Kabar baiknya, Anda tidak perlu menginstal apa pun yang rumit:

1. **Online:** Buka [gchq.github.io/CyberChef](https://gchq.github.io/CyberChef/).
2. **Offline (Kali Linux):**
* Biasanya sudah tersedia di menu Kali (cari "CyberChef").
* Jika belum, Anda bisa mendownload file `.html`-nya dari GitHub, lalu buka dengan Firefox di dalam VMware. Ini jauh lebih aman karena data sensitif yang Anda analisis tidak akan keluar ke internet.

---

### Kesimpulan untuk Ekosistem Anda:

Nantinya, alurnya akan seperti ini:

1. **Snort** mendeteksi paket mencurigakan.
2. **SIEM** mencatat log paket tersebut (tapi biasanya masih dalam bentuk kode Hex/Base64).
3. **Anda (SOC Analyst)** menyalin kode tersebut ke **CyberChef** untuk mencari tahu: *"Ini virus jenis apa?"* atau *"IP mana yang diserang?"*.

Apakah Anda ingin saya berikan satu contoh kasus/data acak untuk Anda coba "bongkar" sendiri di CyberChef sebagai latihan awal?

---

Ini adalah contoh kasus klasik yang sering ditemui oleh seorang SOC Analyst. Kita akan melakukan simulasi **"Deobfuscation"** (membongkar kode yang disembunyikan).

Bayangkan SIEM Anda menangkap aktivitas mencurigakan dari sebuah komputer kantor pada jam 2 pagi. Log menunjukkan sebuah perintah PowerShell dijalankan secara otomatis.

---

### Bagian 1: Temuan Kasus (The Evidence)

Anda menemukan potongan kode "sampah" berikut ini di dalam log SIEM:

> **Data Input:**
> `aHR0cHM6Ly9tYWx3YXJlLWRlcG90LmNvbS9zaGVsbC5wcmU=`

---

### Bagian 2: Analisis Per Bagian

Sebagai analis, Anda harus membedah data tersebut menggunakan insting keamanan:

1. **Identifikasi Format:** Teks di atas diakhiri dengan tanda sama dengan (`=`) dan terdiri dari karakter alfanumerik acak. Ini adalah ciri khas **Base64**. Penyerang menggunakan ini agar sistem keamanan (seperti Antivirus) tidak langsung mengenali kata-kata berbahaya seperti "malware" atau "download".
2. **Konteks Eksekusi:** Jika kode ini muncul di log PowerShell, kemungkinan besar ini adalah perintah untuk mengunduh sesuatu dari internet secara diam-diam.
3. **Tujuan Penyerang:** Menyembunyikan URL asli agar tidak diblokir oleh *Firewall* atau *Web Filter*.

---

### Bagian 3: Langkah Praktek di CyberChef

Sekarang, silakan buka **CyberChef** di Kali Linux atau browser Anda, lalu ikuti langkah-langkah ini untuk belajar:

1. **Input:** Copy dan Paste kode `aHR0cHM6Ly9tYWx3YXJlLWRlcG90LmNvbS9zaGVsbC5wcmU=` ke kolom **Input** (kanan atas).
2. **Cari Operasi:** Di kolom pencarian (kiri), ketik **"From Base64"**.
3. **Masak Resep:** Tarik operasi **"From Base64"** tersebut ke kolom **Recipe** (tengah).
4. **Lihat Hasil:** Perhatikan kolom **Output** (kanan bawah).

---

### Bagian 4: Apa yang Harus Anda Lakukan untuk Belajar?

Setelah Anda berhasil membongkar teks tersebut, jangan berhenti di sana. Lakukan langkah-langkah pendalaman ini:

* **Lakukan Reverse Engineering:** Coba balikkan prosesnya. Ketik nama Anda di Input, gunakan operasi **"To Base64"**, dan lihat perubahannya. Ini melatih Anda mengenali pola data yang terenkripsi.
* **Gunakan Operasi Berantai:** Penyerang sering melakukan enkripsi dua kali. Coba gunakan fitur **"Magic"** di CyberChef. Fitur ini akan mencoba menebak secara otomatis jenis enkripsi apa yang digunakan jika Anda bingung itu format apa.
* **Identifikasi IOC (Indicator of Compromise):** Setelah teks terbongkar (menjadi sebuah URL), tanyakan pada diri sendiri:
* *"Apakah URL ini aman?"*
* *"Apakah saya harus memblokir domain ini di Firewall?"*


* **Cari Tahu "Why":** Kenapa penyerang menggunakan Base64? Kenapa bukan Hex? (Base64 lebih efisien dalam mengirim data biner lewat protokol teks seperti HTTP).

---

**Tantangan Kecil untuk Anda:**
Jika Anda sudah mencoba langkah di atas, Anda akan melihat sebuah URL. Di ujung URL tersebut ada file bernama `shell.pre`.

* Cobalah cari operasi **"URL Decode"** di CyberChef.
* Atau coba masukkan teks **Hex** berikut ini ke Input: `53 4f 43 20 41 6e 61 6c 79 73 74` lalu gunakan operasi **"From Hex"**. Apa bacaannya?

Dengan membiasakan diri bongkar-pasang data di CyberChef, Anda sedang mengasah kemampuan mata Anda untuk mengenali ancaman meskipun sedang "menyamar".

---

<img width="1239" height="613" alt="image" src="https://github.com/user-attachments/assets/3fafbd3b-2bcd-4079-9f46-96ed5946a428" />

