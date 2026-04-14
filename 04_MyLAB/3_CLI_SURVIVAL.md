# CLI SURVIVAL MY ADVENTURE

Menghabiskan waktu seharian di Command Line Interface (CLI) bisa menjadi sangat produktif dan menyenangkan jika Anda memiliki alur kerja yang tepat.
Berikut adalah daftar tugas dan aktivitas yang dapat dilakukan sepenuhnya di dalam terminal untuk membuat Anda merasa "nyaman" seharian:

### 1. Manajemen Tugas dan Waktu
Daripada membuka aplikasi kalender atau catatan berbasis GUI, Anda bisa mengelola hari Anda langsung dari prompt.
* **Taskwarrior:** Alat yang sangat kuat untuk mengelola daftar tugas (*to-do list*) melalui CLI.
* **Calcurse:** Aplikasi kalender dan penjadwalan berbasis teks (Ncurses) yang memungkinkan Anda melihat agenda harian.
* **Termdown:** Gunakan ini sebagai *countdown timer* atau *stopwatch* untuk teknik Pomodoro agar tetap fokus.

### 2. Navigasi dan Manajemen File
Efisiensi di CLI sangat bergantung pada seberapa cepat Anda berpindah antar direktori.
* **Ranger atau Yazi:** Manajer file visual di dalam terminal. Ini memberikan tampilan kolom seperti Finder di macOS atau Explorer di Windows, tetapi dijalankan dengan tombol pintas keyboard.
* **Zoxide:** Pengganti perintah `cd` yang cerdas. Ia "mengingat" direktori yang sering Anda kunjungi sehingga Anda cukup mengetik `z [nama_folder]` untuk melompat ke sana.
* **Fzf (Fuzzy Finder):** Alat pencarian interaktif yang memungkinkan Anda menemukan file atau perintah lama dengan sangat cepat.

### 3. Pengeditan Teks dan Penulisan
Dunia CLI identik dengan pengeditan teks tingkat tinggi.
* **Neovim atau Helix:** Editor teks modern yang sangat cepat dan dapat dikustomisasi sepenuhnya menjadi IDE (Integrated Development Environment) yang lengkap.
* **Pandoc:** Jika Anda perlu membuat laporan, tulislah dalam format Markdown, lalu gunakan Pandoc untuk mengubahnya menjadi PDF, DOCX, atau HTML langsung dari terminal.

### 4. Komunikasi dan Informasi
Anda tidak perlu keluar dari terminal untuk tetap terhubung dengan dunia luar.
* **Newsboat:** Pembaca RSS feed. Anda bisa membaca berita dari situs favorit (seperti BBC, TechCrunch, atau blog pribadi) tanpa gangguan iklan web.
* **Tuir atau TUI Clients:** Ada berbagai klien terminal untuk platform seperti Reddit atau Hacker News.
* **Curl/Wght:** Untuk mengecek cuaca dengan cepat, cukup ketik `curl wttr.in`.

### 5. Pemantauan Sistem (System Monitoring)
Melihat bagaimana komputer Anda bekerja bisa memberikan kepuasan tersendiri bagi pengguna CLI.
* **Btop atau Htop:** Menampilkan penggunaan CPU, RAM, dan jaringan dengan grafik warna-warni yang estetik di dalam terminal.
* **Neofetch atau Fastfetch:** Menampilkan ringkasan spesifikasi sistem dan logo OS Anda (sering digunakan untuk "pamer" estetika desktop).

### 6. Hiburan (Musik dan Santai)
* **Ncspot:** Jika Anda memiliki Spotify Premium, Anda bisa memutar musik langsung dari terminal tanpa beban memori dari aplikasi desktop Spotify yang berat.
* **Music Player Daemon (MPD) + ncmpcpp:** Kombinasi klasik untuk memutar koleksi musik lokal dengan visualisator spektrum yang keren.

### Tips Tambahan untuk Kenyamanan Maksimal:
1.  **Gunakan Multiplexer (Tmux):** Ini adalah alat wajib. Tmux memungkinkan Anda membagi satu jendela terminal menjadi banyak panel (split screen) dan menjalankan beberapa tugas sekaligus.
2.  **Pilih Emulator Terminal yang Baik:** Gunakan **Alacritty**, **Kitty**, atau **WezTerm** untuk performa yang cepat dan dukungan rendering GPU.
3.  **Zsh + Oh My Zsh:** Gunakan shell Zsh dengan tema (seperti Powerlevel10k) agar terminal Anda terlihat indah dan memberikan informasi berguna (seperti status Git atau direktori saat ini).

Dengan setup ini, terminal Anda bukan lagi sekadar tempat mengetik perintah teknis, melainkan sebuah ekosistem kerja yang lengkap dan minim gangguan.

---

# Mission 1
Menjalankan Kali Linux di VMware memberikan Anda fleksibilitas untuk mencoba berbagai alat keamanan tanpa takut merusak sistem utama.
Agar Anda betah berlama-lama di CLI Kali Linux, Anda bisa mencoba aktivitas yang menggabungkan **estetika (look)**, **produktivitas**, dan **eksplorasi fitur keamanan**.

Berikut adalah daftar aktivitas untuk membuat terminal Kali Anda menjadi "rumah" yang nyaman:

### 1. Personalisasi Visual (Rice Your Terminal)
Agar betah, terminal harus enak dipandang. Kali Linux menggunakan **Zsh** secara *default*, yang sangat mudah dimodifikasi.
* **Oh My Zsh:** Instal kerangka kerja ini untuk mengelola konfigurasi Zsh Anda.
* **Tema Powerlevel10k:** Ini adalah tema paling populer yang memberikan prompt interaktif, menampilkan status baterai, ikon OS, hingga status Git dengan sangat estetik.
* **Color Schemes:** Ubah skema warna terminal Anda (misalnya ke *Dracula*, *Gruvbox*, atau *Nord*) agar mata tidak cepat lelah saat membaca baris kode.

### 2. Menguasai Multiplexing dengan Tmux
Di Kali Linux, Anda sering kali perlu menjalankan banyak alat sekaligus (misalnya satu panel untuk *scanning*, satu untuk *listening*, dan satu untuk mencatat).
* Instal **Tmux** (`sudo apt install tmux`).
* Belajarlah membagi layar menjadi beberapa bagian (*split panes*) secara vertikal dan horizontal dalam satu jendela terminal.
* Gunakan fitur *session* sehingga jika VMware tertutup secara tidak sengaja, pekerjaan Anda di terminal tetap berjalan di latar belakang.

### 3. Eksplorasi Alat Keamanan Berbasis TUI (Text User Interface)
Kali punya banyak alat canggih yang berjalan di CLI namun memiliki tampilan grafis berbasis teks yang keren:
* **Bettercap:** Gunakan ini untuk memantau jaringan secara interaktif. Tampilannya sangat dinamis dan memberikan kesan "hacker" yang kuat.
* **Metasploit (msfconsole):** Pelajari perintah-perintah dasar di dalamnya. Ini adalah *framework* penetrasi paling ikonik yang sepenuhnya dijalankan via CLI.
* **Nmap dengan Output Estetik:** Gunakan perintah `nmap` dan pelajari cara membaca hasilnya langsung di terminal untuk memetakan jaringan di sekitar VM Anda.

### 4. Manajemen File dan Navigasi Super Cepat
Jangan gunakan *file manager* grafis. Cobalah navigasi gaya "pro":
* **Ranger:** Instal dengan `sudo apt install ranger`. Ini adalah manajer file CLI dengan pratinjau gambar dan teks yang sangat nyaman.
* **Fzf (Fuzzy Finder):** Gunakan ini untuk mencari file atau perintah lama hanya dengan mengetik beberapa huruf. Ini akan menghemat banyak waktu daripada mengetik perintah `find` yang rumit.
* **Zoxide:** Instal sebagai pengganti `cd`. Anda cukup mengetik `z [nama_folder]` untuk berpindah antar direktori yang sering dikunjungi secara instan.

### 5. Membangun "Dashboard" Pemantauan
Biarkan satu tab terminal terbuka untuk memantau kesehatan sistem VM Anda:
* **Btop:** Instal dengan `sudo apt install btop`. Ini adalah monitor sistem paling estetik dengan grafik warna-warni untuk suhu CPU, penggunaan RAM, dan trafik jaringan.
* **Gping:** Gunakan ini daripada `ping` biasa untuk melihat grafik visual koneksi jaringan Anda.
* **Nethogs:** Untuk melihat aplikasi apa saja yang sedang memakan kuota data di Kali Linux Anda.

### 6. Belajar Markdown untuk Pencatatan (Notetaking)
Sebagai pengguna Kali, mencatat setiap temuan sangatlah penting.
* Gunakan **Neovim** atau **Vim** untuk menulis catatan dalam format Markdown langsung di terminal.
* Gunakan **Glow** (`sudo apt install glow`) untuk membaca file Markdown Anda dengan tampilan yang rapi dan berwarna di dalam CLI.

### Tips Tambahan khusus VMware:
* **Shared Folder:** Pastikan Anda bisa mengakses folder dari OS utama melalui CLI di `/mnt/hgfs/`. Ini memudahkan Anda memindahkan file hasil kerja dari terminal ke sistem utama.
* **Alias:** Buatlah perintah singkat (*alias*) di file `.zshrc` Anda. Misalnya, buat perintah `update` untuk menjalankan `sudo apt update && sudo apt upgrade`.

Dengan mengombinasikan **Tmux**, **Powerlevel10k**, dan **Ranger**, terminal Kali Linux Anda akan terasa seperti pusat kendali yang sangat profesional dan nyaman digunakan seharian.

---

# Mission 2

Untuk navigasi sepenuhnya tanpa mouse di terminal Kali Linux, Anda harus menguasai pintasan keyboard untuk berpindah antar direktori dan mengelola layar.

### Navigasi File (Perintah Dasar)
* **`ls`**: Melihat isi folder (gunakan `ls -la` untuk melihat file tersembunyi).
* **`cd [nama_folder]`**: Masuk ke folder tujuan.
* **`cd ..`**: Kembali ke folder sebelumnya (naik satu tingkat).
* **`cd ~`**: Langsung kembali ke folder Home.
* **`pwd`**: Mengetahui posisi folder Anda saat ini.

### Kontrol Terminal (Keyboard Shortcuts)
* **Tab**: Tekan sekali untuk melengkapi nama file/folder secara otomatis (**Auto-complete**).
* **Ctrl + L**: Membersihkan layar terminal agar rapi kembali.
* **Ctrl + C**: Menghentikan paksa perintah atau program yang sedang berjalan.
* **Ctrl + Alt + T**: Membuka jendela terminal baru.
* **Panah Atas/Bawah**: Melihat riwayat perintah yang pernah Anda ketik sebelumnya.

### Navigasi dalam Teks (Editor)
Jika Anda membuka file dengan `nano` atau `vim`:
* **`nano [nama_file]`**: Gunakan tombol panah untuk bergerak, **Ctrl + O** untuk simpan, dan **Ctrl + X** untuk keluar.
* **`less [nama_file]`**: Gunakan tombol **Space** untuk scroll ke bawah dan **q** untuk berhenti melihat file.

Jika Anda ingin kenyamanan maksimal, sangat disarankan menginstal **Tmux** agar bisa berpindah antar panel terminal hanya menggunakan kombinasi tombol keyboard tanpa menyentuh mouse sama sekali.

---

# Mission 3

Setelah menginstal **tmux**, Anda bisa mengelola banyak sesi dalam satu layar tanpa menyentuh mouse. Berikut adalah perintah navigasi dasarnya (secara default, tombol awalan adalah **Ctrl + b**):

### 1. Navigasi Panel (Splitting)
Gunakan ini untuk membagi satu layar menjadi beberapa bagian:
* **`Ctrl + b` lalu `%`**: Bagi layar secara **vertikal**.
* **`Ctrl + b` lalu `"`**: Bagi layar secara **horizontal**.
* **`Ctrl + b` lalu Tombol Panah**: Berpindah antar panel yang sedang aktif.
* **`Ctrl + b` lalu `x`**: Menutup panel yang aktif.
* **`Ctrl + b` lalu `z`**: Membuat satu panel menjadi layar penuh (Zoom), tekan lagi untuk mengecilkan.

---

### 2. Navigasi Jendela (Windows)
Jika satu layar sudah terlalu penuh, buat "tab" baru:
* **`Ctrl + b` lalu `c`**: Membuat **jendela baru**.
* **`Ctrl + b` lalu `n`**: Pindah ke jendela berikutnya (*Next*).
* **`Ctrl + b` lalu `p`**: Pindah ke jendela sebelumnya (*Previous*).
* **`Ctrl + b` lalu `0-9`**: Pindah ke jendela berdasarkan nomor indeksnya.
* **`Ctrl + b` lalu `w`**: Menampilkan daftar semua jendela yang sedang terbuka.

---

### 3. Navigasi Teks (Copy Mode)
Untuk melihat riwayat teks yang sudah tergulung ke atas (*scroll*):
* **`Ctrl + b` lalu `[`**: Masuk ke mode gulir. Gunakan **Panah** atau **Page Up/Down** untuk melihat teks lama.
* **`q`**: Keluar dari mode gulir dan kembali ke prompt aktif.

---

### 4. Sesi (Detach & Attach)
Ini adalah fitur terbaik tmux agar pekerjaan tidak hilang saat VM tertutup:
* **`Ctrl + b` lalu `d`**: Keluar dari tmux tanpa mematikan proses (*Detach*).
* **`tmux attach`**: (Ketik di terminal biasa) Untuk masuk kembali ke sesi pekerjaan Anda yang terakhir.

**Tips:** Agar navigasi lebih lancar, Anda bisa menahan tombol **Ctrl + b** lalu tekan tombol perintahnya dengan cepat. Jangan menekan semuanya bersamaan.

---
