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

## Validitas

Jawaban singkatnya: **Ya, 100% asli dan nyata.** Data yang kamu lihat di layar terminal itu bukan simulasi atau "permainan". Itulah alasan mengapa kamu membangun **Lab Isolasi**; karena alat-alat ini berinteraksi langsung dengan server dan perangkat di internet yang sebenarnya.

Berikut adalah penjelasan mengapa data tersebut dianggap "asli":

### 1. Keaslian Data Sherlock (Dunia Internet)
Saat kamu mengetik `python3 sherlock.py [username]`, script tersebut benar-benar mengirimkan permintaan (*request*) ke server asli milik Instagram, TikTok, Facebook, dan ratusan situs lainnya.

* **Realita:** Jika Sherlock menemukan link `instagram.com/paimon_123`, itu artinya memang ada akun dengan nama tersebut di server Instagram saat ini.
* **Bukan Tebakan:** Sherlock tidak menebak; ia memeriksa apakah profil tersebut dapat diakses secara publik.
* **Akurasi:** Terkadang ada "False Positive" (salah deteksi) jika sebuah situs sedang dalam perbaikan, tapi 90% hasilnya adalah data akun nyata milik orang asli.

---

### 2. Keaslian Data Nmap (Dunia Jaringan)
Nmap adalah standar industri yang digunakan oleh administrator jaringan dan peretas profesional di seluruh dunia.

* **Ketukan Pintu Nyata:** Saat kamu melakukan `nmap scanme.nmap.org`, Kali Linux kamu benar-benar mengirimkan paket data kecil ke server tersebut di Amerika Serikat. 
* **Respon Server:** Jika Nmap mengatakan `Port 80 is open`, itu artinya server tersebut memang sedang membuka pintu untuk lalu lintas web. Jika kamu mencoba memindai IP Windows kamu sendiri, Nmap akan melaporkan kondisi asli keamanan laptop kamu.
* **Bahaya Nyata:** Karena Nmap melakukan "ketukan pintu" yang nyata, server yang memiliki sistem keamanan ketat (seperti milik Bank atau Instansi Pemerintah) bisa mencatat alamat IP kamu dan menganggapnya sebagai upaya awal peretasan. Itulah sebabnya kita hanya memindai target yang diizinkan (seperti `scanme.nmap.org`).

---

### Mengapa Ini Penting untuk Kamu Pahami?

Sebagai seorang *Ethical Hacker*, kamu harus sadar bahwa setiap perintah yang kamu ketik di Terminal memiliki **konsekuensi di dunia luar**:

| Alat | Dampak di Dunia Nyata |
| :--- | :--- |
| **Sherlock** | Kamu mengumpulkan informasi pribadi seseorang (OSINT). Gunakan dengan bijak, jangan untuk *doxing* (menyebar data pribadi). |
| **Nmap** | Kamu sedang memeriksa lubang di pagar rumah orang lain. Melakukan ini tanpa izin bisa dianggap tindakan ilegal di beberapa negara. |

---

### Cara Menguji "Keaslian" secara Aman (Praktik Internal):
Ingin bukti bahwa ini nyata tanpa menyentuh internet luar? Coba ini di Lab kamu:

1.  **Cari IP Windows kamu:** Di CMD Windows, ketik `ipconfig`. Catat `IPv4 Address` (misal: `192.168.1.5`).
2.  **Pindai dari Kali Linux:** Di terminal Kali, ketik `nmap [IP_Windows_Kamu]`.
3.  **Lihat Hasilnya:** Nmap akan menampilkan port yang terbuka di laptop kamu saat ini. Itu adalah data asli dari perangkat yang sedang kamu pegang!

---

### Tips Snapshot:
Sekarang kamu sudah menjalankan Sherlock dan Nmap. Jika semua berjalan lancar, sekarang adalah waktu yang tepat untuk **mengambil Snapshot baru** dengan nama **"Tools Dasar Terpasang"**. 

Jadi, jika besok kamu mencoba alat lain yang lebih berbahaya dan Linux kamu rusak, kamu tidak perlu menginstal Sherlock lagi dari awal.

**Langkah selanjutnya:**
Apakah kamu ingin saya tunjukkan bagaimana cara **menyimpan hasil scan Nmap atau Sherlock** ke dalam sebuah file `.txt` atau `.xml` agar bisa kamu baca kembali nanti tanpa harus menjalankan ulang perintahnya?
