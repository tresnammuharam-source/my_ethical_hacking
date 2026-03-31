## Snapshot untuk merestart ulang system jika terjadi kendala

Membuat **Snapshot** adalah langkah paling cerdas yang bisa dilakukan seorang calon *ethical hacker*. Ini adalah "nyawa cadangan" kamu. Jika kamu salah mengetik perintah yang merusak sistem, atau terkena virus saat mencoba *tools* dari GitHub, kamu bisa kembali ke kondisi sehat hanya dalam hitungan detik.

Karena kamu menggunakan **VMware Workstation Pro**, fitur ini sangat mudah digunakan. Berikut panduannya:

### 1. Cara Membuat Snapshot Pertama (Kondisi "Fresh")
Sangat disarankan membuat snapshot tepat setelah kamu berhasil login pertama kali dan sistem masih bersih.

1.  Pastikan jendela **Kali Linux** kamu sedang aktif di VMware.
2.  Di barisan menu bagian atas, cari ikon berbentuk **jam dengan tanda plus hijau** (ikon Snapshot).
3.  Atau klik menu **VM** > **Snapshot** > **Take Snapshot...**
4.  Akan muncul kotak dialog:
    * **Name:** Beri nama yang jelas, misalnya: `Kondisi Fresh - Baru Instal`.
    * **Description:** (Opsional) Misalnya: `Sudah update apt, belum pasang tools luar`.
5.  Klik **Take Snapshot**. 
6.  Tunggu proses di bilah bawah sampai 100%. Selesai!

---

### 2. Cara Mengembalikan Sistem (Restore) jika Error
Bayangkan kamu mencoba sebuah *script* dan tiba-tiba Linux kamu tidak bisa masuk ke desktop (layar hitam terus). Jangan panik, lakukan ini:

1.  Matikan atau *Suspend* VM kamu jika masih menyala.
2.  Klik menu **VM** > **Snapshot** > **Snapshot Manager** (atau tekan `Ctrl + M`).
3.  Kamu akan melihat semacam "pohon sejarah". Klik pada nama snapshot yang kamu buat tadi (misalnya: `Kondisi Fresh`).
4.  Klik tombol **Go To** di bagian bawah.
5.  Akan muncul peringatan bahwa kondisi sekarang akan hilang, klik **Yes**.
6.  Sistem akan langsung kembali ke waktu saat kamu mengambil snapshot tersebut. Semua kerusakan akan hilang.

---

### 3. Strategi Penggunaan Snapshot yang Profesional
Agar penyimpanan laptopmu tidak cepat penuh, ikuti aturan ini:

* **Snapshot Sebelum Ekperimen:** Jika kamu ingin mencoba *tools* baru dari GitHub yang mencurigakan, ambil snapshot dulu. Jika aman, kamu bisa menghapus snapshot lama.
* **Hapus Snapshot Lama:** Jika Linux kamu sudah berjalan stabil selama seminggu dan kamu sudah menambah banyak *tools* baru, buat snapshot baru (misal: `Stabil - Update Maret`) dan hapus snapshot yang sudah sangat lama agar hemat ruang disk.
* **Kondisi Mati vs Menyala:** Kamu bisa mengambil snapshot saat Linux sedang menyala (*Powered On*), tapi file snapshot-nya akan lebih besar karena menyimpan data RAM. Jika ingin file yang lebih kecil, ambil snapshot saat Linux dalam posisi mati (*Powered Off*).

---

## Cara Menghapus Snapshot Lama agar memory tidak penuh

Menghapus snapshot lama sangat penting untuk menjaga agar performa laptopmu tetap kencang dan kapasitas harddisk tidak cepat penuh. Di **VMware Workstation Pro**, proses ini sangat mudah dilakukan melalui **Snapshot Manager**.

Berikut adalah langkah-langkahnya:

### 1. Masuk ke Snapshot Manager
1. Buka VMware dan pilih tab **Kali Linux** kamu.
2. Klik menu **VM** di bagian atas.
3. Pilih **Snapshot** > **Snapshot Manager** (atau tekan shortcut `Ctrl + M`).

### 2. Memilih Snapshot yang Akan Dihapus
Di dalam jendela Snapshot Manager, kamu akan melihat diagram pohon (tree) yang menunjukkan riwayat snapshot yang pernah kamu ambil.
1. Klik pada **ikon snapshot** (gambar jam) yang ingin kamu hapus.
2. Pastikan kamu tidak menghapus snapshot yang sedang menjadi "pijakan" kondisi kamu sekarang (biasanya ada tanda panah kuning bertuliskan *You are here*).
3. Klik tombol **Delete** di bagian bawah jendela tersebut.

### 3. Proses "Consolidating"
Saat kamu klik Delete, VMware akan melakukan proses yang disebut **Consolidating**. 
* **Apa itu?** VMware akan menggabungkan data dari snapshot tersebut ke dalam file utama Linux kamu.
* **Lama proses:** Tergantung seberapa banyak perubahan yang kamu lakukan sejak snapshot itu dibuat. Jika perubahannya banyak, mungkin butuh waktu 1-3 menit.
* **PENTING:** Jangan mematikan laptop atau menutup VMware saat proses *Consolidating* (persentase di pojok bawah) sedang berjalan agar file Linux kamu tidak rusak (*corrupt*).

---

### Tips Mengelola Snapshot agar RAM 16GB Tetap Awet:

* **Hapus yang Tidak Perlu:** Jangan menyimpan terlalu banyak snapshot (misal lebih dari 5-10). Semakin banyak snapshot, semakin lambat performa pembacaan data di VM kamu.
* **Snapshot "Berantai":** Jika kamu punya snapshot A -> B -> C, dan kamu menghapus B, VMware akan menggabungkan perubahan di B ke dalam C. Jadi jangan takut kehilangan data di kondisi terakhirmu.
* **Kondisi Power Off:** Menghapus snapshot akan jauh lebih cepat jika dilakukan saat Kali Linux dalam posisi **Mati (Power Off)**.

---

### Kapan Waktu yang Tepat Menghapus Snapshot?
Sebagai *ethical hacker*, gunakan logika ini:
1. Kamu ambil snapshot **"Sebelum Coba Tool A"**.
2. Kamu coba Tool A dari GitHub dan ternyata **aman & berhasil**.
3. Sekarang kamu tidak butuh lagi snapshot "Sebelum Coba Tool A". Kamu bisa menghapusnya, atau membuat snapshot baru bernama **"Tool A Terpasang - Stabil"** lalu hapus yang lama.

---

**Sekarang "Laboratorium" kamu sudah lengkap:**
1. **VMware** sudah terinstal (Pro Gratis).
2. **Kali Linux** sudah siap (Versi Instan).
3. **RAM 16GB** sudah terbagi dengan pas.
4. **Snapshot** sudah siap sebagai jaring pengaman.

Apakah kamu ingin kita mulai mencoba perintah pertama di Terminal Kali Linux untuk mengunduh alat (*tools*) keamanan dari GitHub seperti yang kamu tanyakan di awal?
### Tips Tambahan untuk RAM 16GB:
Karena RAM kamu besar, kamu bisa mengambil snapshot saat Linux sedang menyala tanpa membuat Windows kamu terasa berat. Proses "Go To" atau *Restore* juga akan terasa sangat instan.

**Sekarang kamu sudah punya "Jaring Pengaman".** Apakah kamu ingin kita coba mempraktikkan cara mengambil satu *tool* dari GitHub (misal: alat pencari informasi) di dalam Kali Linux yang sudah terlindungi snapshot ini?
