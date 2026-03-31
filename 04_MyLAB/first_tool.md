## Menginstal dan Menjalankan Tools Pertama Anda

Selamat! Kamu sudah memiliki pondasi yang sangat kuat. Sekarang saatnya kita masuk ke tahap **"Live Action"**. Di dunia *ethical hacking*, kita akan memulainya dengan dua kategori penting: **Network Scanning** (Nmap) dan **OSINT** (Sherlock).

Karena kamu menggunakan Kali Linux, ada sedikit perbedaan cara antara keduanya.

---

### 1. Menjalankan Nmap (Network Mapper)
**Kabar gembira:** Nmap sudah terinstal secara bawaan di Kali Linux. Kamu tidak perlu mengunduhnya lagi. Nmap digunakan untuk memindai "pintu" (port) yang terbuka di sebuah server.

**Cara Menjalankan:**
1.  Buka Terminal di Kali Linux.
2.  Ketik perintah berikut untuk memindai server latihan resmi (milik Nmap):
    ```bash
    nmap scanme.nmap.org
    ```
3.  **Hasilnya:** Kamu akan melihat daftar port seperti `80/tcp open http`. Ini artinya "pintu" nomor 80 terbuka untuk akses website.



* **Tips Pro:** Gunakan perintah `sudo nmap -sV scanme.nmap.org` untuk melihat versi aplikasi apa yang berjalan di pintu tersebut. Kamu akan diminta memasukkan password (yaitu: `kali`).

---

### 2. Mengunduh & Menjalankan Sherlock
Berbeda dengan Nmap, **Sherlock** adalah alat dari GitHub yang harus kita ambil manual. Alat ini digunakan untuk mencari jejak *username* di ratusan media sosial secara otomatis.

**Langkah Instalasi di Terminal Kali:**

1.  **Pindah ke folder Desktop** (biar mudah terlihat):
    ```bash
    cd Desktop
    ```
2.  **Clone (Ambil) dari GitHub:**
    ```bash
    git clone https://github.com/sherlock-project/sherlock.git
    ```
3.  **Masuk ke folder Sherlock:**
    ```bash
    cd sherlock
    ```
4.  **Instal bahan-bahannya (Dependencies):**
    ```bash
    python3 -m pip install -r requirements.txt
    ```


---

### 3. Cara Menjalankan Sherlock
Setelah instalasi selesai, kamu bisa mulai berburu informasi. Misalnya, kamu ingin tahu apakah ada akun media sosial dengan nama "GeminiAI".

**Ketik perintah ini:**
```bash
python3 sherlock.py GeminiAI
```

* **Apa yang terjadi?** Sherlock akan memeriksa ratusan situs (Instagram, Twitter, Facebook, TikTok, dll).
* **Hasilnya:** Sherlock akan menampilkan link-link media sosial yang menggunakan username tersebut. File hasilnya juga akan tersimpan otomatis dalam format `.txt` di folder tersebut.

---

### 4. Protokol Keamanan (Penting!)
Sebelum kamu melakukan eksperimen lebih jauh, ingat aturan main di Lab Isolasi kamu:

1.  **Gunakan Snapshot:** Sebelum kamu menginstal banyak *tool* lain dari GitHub, pastikan kamu punya snapshot kondisi sekarang (Nmap & Sherlock sudah terpasang dan jalan).
2.  **Etika:** Jangan gunakan Nmap untuk memindai website pemerintah, bank, atau perusahaan tanpa izin. Gunakan hanya pada `scanme.nmap.org` atau perangkat kamu sendiri (seperti IP Windows kamu).
3.  **Update Berkala:** Selalu lakukan `sudo apt update` agar *tools* di Kali Linux kamu tidak ketinggalan zaman.

---

### Tantangan Pertama Kamu:
Coba jalankan Sherlock dengan **username kamu sendiri** atau username publik yang kamu tahu. Apakah kamu terkejut melihat berapa banyak akun yang ditemukan oleh script sederhana ini?

Setelah ini, apakah kamu ingin saya ajarkan cara mencari alamat IP Windows kamu dari dalam Kali Linux agar kamu bisa mencoba "mengetuk pintu" (Nmap) komputer kamu sendiri secara aman?
