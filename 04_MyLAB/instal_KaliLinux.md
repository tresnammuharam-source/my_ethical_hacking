## Introduction spesifikasi PC on VM dan Kali Linux

Dengan RAM **16GB**, kamu berada di posisi yang **sangat ideal** untuk menjalankan Virtual Machine (VM). Ini adalah "sweet spot" atau titik paling pas bagi seorang pemula hingga tingkat menengah di dunia *cybersecurity*.

Laptop dengan RAM 16GB akan terasa jauh lebih "enak" dan lancar dibandingkan RAM 8GB. Berikut adalah alasan teknis dan cara pembagiannya agar performa PC kamu tetap kencang:

### 1\. Kenapa 16GB Itu "Enak"?

Dalam dunia VM, kamu harus membagi RAM fisikmu untuk sistem utama (Windows) dan sistem tamu (Kali Linux).

  * **Windows (Host):** Butuh sekitar 4GB - 6GB agar tetap lancar membuka Browser, Spotify, atau VS Code.
  * **Kali Linux (VM):** Idealnya diberi **4GB**. Dengan 4GB, Kali Linux bisa menjalankan alat berat seperti pemindai celah keamanan atau desktop grafis tanpa *laging*.
  * **Sisa RAM:** Kamu masih punya sisa sekitar **6GB - 8GB** sebagai "napas" tambahan agar PC tidak panas atau *hang*.

-----

### 2\. Rekomendasi Setting RAM di VMware

Saat kamu membuat VM nanti, gunakan pengaturan ini untuk performa terbaik:

| Komponen | Pengaturan Rekomendasi | Keterangan |
| :--- | :--- | :--- |
| **Memory (RAM)** | **4096 MB (4GB)** | Sudah sangat cukup untuk hampir semua *tools* hacking. |
| **Processors** | **2 atau 4 Cores** | Agar proses pemindaian (*scanning*) lebih cepat. |
| **Hard Disk** | **40GB - 80GB** | Pilih opsi *Dynamically Allocated* agar tidak langsung memakan tempat. |

-----

### 3\. Keuntungan RAM 16GB bagi Ethical Hacker

Dengan RAM sebesar ini, kamu bisa melakukan hal yang tidak bisa dilakukan RAM 8GB:

  * **Menjalankan 2 VM Sekaligus:** Kamu bisa menjalankan **Kali Linux** (sebagai penyerang) dan **Metasploitable/Windows 7** (sebagai target/korban) secara bersamaan untuk simulasi serangan nyata.
  * **Multitasking:** Kamu bisa membuka 20 tab di Google Chrome untuk membaca tutorial sambil menjalankan *tools* berat di dalam VM tanpa takut Windows kamu *blue screen*.

-----

### 4\. Tips Agar Tetap "Enteng"

Meski RAM kamu besar, tetap perhatikan hal ini:

1.  **Gunakan SSD:** RAM 16GB akan percuma jika penyimpananmu masih pakai HDD lama. SSD akan membuat VM terbuka dalam hitungan detik.
2.  **Matikan VM jika tidak dipakai:** Jangan dibiarkan *suspend* jika kamu ingin bermain game berat di Windows, agar RAM kembali penuh untuk Windows.

-----

## Langkah Berikutnya: Link Download Kali Linux Instan

Karena kamu sudah siap secara *hardware*, ini adalah link resmi untuk mendapatkan Kali Linux yang tinggal "klik dua kali" (tanpa instal):

1.  Pergi ke: **[kali.org/get-kali/](https://www.google.com/search?q=https://www.kali.org/get-kali/%23kali-virtual-machines)**
2.  Pilih bagian **"Virtual Machines"**.
3.  Pilih opsi **VMware** (pilih yang 64-bit).
4.  Setelah download (sekitar 3GB), kamu cukup ekstrak file `.zip`-nya.
5.  Di VMware, pilih **"Open a Virtual Machine"** dan cari file berakhiran `.vmx` di dalam folder ekstraksi tadi.

## Instal Kali Linux di VMware

Tentu! Menggunakan versi **"Pre-built"** atau instan adalah pilihan paling cerdas karena kamu tidak perlu melakukan proses instalasi Linux yang memakan waktu 30-60 menit. Kamu hanya perlu melakukan "Import".

Karena kamu sudah punya RAM 16GB, proses ini akan terasa sangat cepat. Berikut panduannya:

### Langkah 1: Ekstrak File Kali Linux
File yang kamu download dari situs Kali Linux biasanya berformat `.7z` atau `.zip`.
1. Cari file tersebut di folder *Downloads*.
2. Klik kanan pada file tersebut, lalu pilih **Extract All** atau **Extract to "kali-linux-..."**.
3. Pastikan kamu tahu di mana folder hasil ekstraknya berada. Di dalamnya akan ada banyak file, tapi yang paling penting adalah file dengan ikon VMware (ekstensi `.vmx`).

---

### Langkah 2: Membuka File di VMware
Sekarang, buka aplikasi **VMware Workstation Pro** yang sudah kamu instal:

1. Di halaman utama (*Home*), klik tombol **"Open a Virtual Machine"**.
2. Telusuri folder hasil ekstrak tadi.
3. Pilih file yang bernama **`kali-linux-202X.X-vmware-amd64.vmx`** (ikonnya biasanya berbentuk kotak biru kecil).
4. Klik **Open**.



---

### Langkah 3: Pengaturan RAM & CPU (Opsional tapi Disarankan)
Sebelum menyalakan, mari kita manfaatkan RAM 16GB kamu agar "ngebut":
1. Klik tulisan **"Edit virtual machine settings"**.
2. Di bagian **Memory**, geser angkanya ke **4096 MB (4GB)**.
3. Di bagian **Processors**, ubah *Number of cores* menjadi **2** atau **4** (tergantung jumlah core laptopmu).
4. Klik **OK**.

---

### Langkah 4: Menjalankan Kali Linux
1. Klik tombol hijau bertuliskan **"Power on this virtual machine"**.
2. Jika muncul pesan *"This virtual machine might have been moved or copied"*, pilih tombol **"I Copied It"**. (Ini penting agar VMware mengatur ulang jalur jaringannya secara otomatis).
3. Tunggu proses *booting* (layar hitam dengan logo naga) sampai muncul layar login.

---

### Langkah 5: Login Pertama Kali
Berbeda dengan instalasi manual, versi instan ini sudah punya username dan password bawaan dari pabriknya:

* **Username:** `kali`
* **Password:** `kali`



---

### Tips Setelah Masuk ke Desktop Kali Linux:

1.  **Layar Fullscreen:** Jika layarnya kecil, klik menu **View** di bagian atas VMware, lalu pilih **Fit Guest Now** atau cukup maksimalkan jendela VMware-nya.
2.  **Ganti Password:** Karena alasan keamanan, segera buka terminal (ikon kotak hitam di kiri atas) dan ketik perintah `passwd` untuk mengganti password "kali" menjadi password pilihanmu sendiri.
3.  **Update Sistem:** Ketik perintah ini di terminal agar Linux kamu punya versi terbaru:
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

### Bagaimana Jika Terjadi Error?
Jika saat klik "Power On" muncul pesan error tentang **"Side-channel mitigations"** atau **"Virtualization is disabled"**, itu artinya fitur virtualisasi di BIOS laptopmu belum aktif. Kamu harus masuk ke BIOS saat laptop baru dinyalakan dan mencari opsi **Intel VT-x** atau **AMD-V** untuk di-**Enable**.

Apakah kamu sudah berhasil mengunduh filenya, atau ada kendala saat proses ekstrak?
