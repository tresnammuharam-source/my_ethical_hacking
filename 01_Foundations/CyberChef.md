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
