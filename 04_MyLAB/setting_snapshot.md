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

### Tips Tambahan untuk RAM 16GB:
Karena RAM kamu besar, kamu bisa mengambil snapshot saat Linux sedang menyala tanpa membuat Windows kamu terasa berat. Proses "Go To" atau *Restore* juga akan terasa sangat instan.

**Sekarang kamu sudah punya "Jaring Pengaman".** Apakah kamu ingin kita coba mempraktikkan cara mengambil satu *tool* dari GitHub (misal: alat pencari informasi) di dalam Kali Linux yang sudah terlindungi snapshot ini?
