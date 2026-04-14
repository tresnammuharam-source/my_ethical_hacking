# Schema **The Infiltrator (Red Team)**.

Bayangkan Anda baru saja menerima kontrak "Penetration Testing" resmi dari sebuah perusahaan teknologi fiktif bernama **"Arka-Data Corp"**.

---

### 🚨 Quest Name: "The Silent Entry"

**Objektif Utama:** Mendapatkan akses ke file "Financial_Report_2026.pdf" yang tersimpan di dalam server internal kantor pusat tanpa terdeteksi oleh sistem keamanan mereka.

---

### Tahap 1: Reconnaissance (Pengintaian)

Sebelum menyerang, Anda harus mengumpulkan informasi. Anda tidak langsung menabrak pintu depan.

* **Cara Main:** Anda melakukan *OSINT (Open Source Intelligence)*. Anda mencari profil karyawan Arka-Data di media sosial profesional.
* **Hasil:** Anda menemukan salah satu admin IT mereka baru saja memposting foto meja kerjanya. Di pojok foto, ada sebuah catatan kecil (post-it) yang berisi nama WiFi internal: `Arka-Guest-Pass`.
* **Target Berikutnya:** SSID WiFi tersebut.

### Tahap 2: Gaining Access (Masuk ke Sistem)

Anda pergi ke area sekitar kantor mereka (atau menggunakan teknik *remote attack*).

* **Cara Main:** Anda menggunakan **Kali Linux** dan alat seperti `Aircrack-ng` atau melakukan *Evil Twin Attack* (membuat WiFi palsu dengan nama yang sama).
* **Hasil:** Seorang karyawan yang sedang istirahat tidak sengaja terhubung ke WiFi palsu Anda. Anda berhasil menangkap *hash* password atau melakukan *Man-in-the-Middle* (MitM) untuk mendapatkan kredensial login VPN mereka.
* **Target Berikutnya:** Jaringan Internal.

### Tahap 3: Privilege Escalation (Naik Level)

Anda sudah berada di dalam jaringan, tapi Anda hanya punya akses sebagai "User Biasa". Anda tidak bisa membuka folder "Financial".

* **Cara Main:** Anda menjalankan pemindaian internal menggunakan `Nmap` untuk melihat komputer mana yang punya celah keamanan (misalnya: sistem yang lupa di-*update*). Anda menemukan satu server lama yang menjalankan layanan database versi tua.
* **Hasil:** Anda menggunakan *exploit* khusus untuk mengambil alih server tersebut dan mendapatkan hak akses sebagai **Administrator (Root)**.
* **Target Berikutnya:** Server File Utama.

### Tahap 4: Exfiltration (Mengambil Harta Karun)

Sekarang Anda adalah "Raja" di jaringan tersebut.

* **Cara Main:** Anda mencari file target. Anda menemukannya di `/mnt/secure_storage/finance/`.
* **Hasil:** Anda mengunduh file tersebut melalui jalur yang terenkripsi agar tidak memicu alarm di layar **SOC Analyst** (si penjaga benteng).
* **Misi Selesai:** Anda keluar dari sistem dan menghapus jejak log aktivitas Anda (*Clearing Tracks*).

---

### 📊 Hasil Akhir (Debriefing)

Sebagai *Ethical Hacker*, Anda tidak mencuri file itu untuk dijual. Anda membuat laporan:

1. **Celah:** Karyawan ceroboh memposting foto *password* di media sosial.
2. **Celah:** Ada server lama yang belum di-*patching*.
3. **Rekomendasi:** Edukasi keamanan bagi karyawan dan pembaruan sistem berkala.

---

### 🛠️ "Equipment" yang Anda Butuhkan (Skillset):

Jika Anda ingin serius di jalur ini, ini adalah *skill tree* yang harus Anda naikkan levelnya:

* **Networking Dasar:** Paham cara kerja IP, Subnet, dan Protokol (TCP/UDP).
* **Linux Mastery:** Mahir menggunakan terminal (Command Line).
* **Scripting:** Minimal paham dasar Python atau Bash untuk otomatisasi serangan.
* **Cybersecurity Tools:** Belajar menggunakan Nmap, Metasploit, dan Wireshark.

# Scheme The Guardian

Mari kita putar balik waktu. Sekarang, Anda adalah **The Guardian (SOC Analyst Tier 1)** yang sedang bertugas di markas keamanan **Arka-Data Corp**.

Di depan Anda ada deretan monitor yang menampilkan grafik trafik jaringan dan ribuan baris log yang terus berjalan. Tugas Anda: **Deteksi, Analisis, dan Hentikan penyusup.**

### 🛡️ Quest Name: "The Red Alert"

**Objektif Utama:** Mengidentifikasi aktivitas mencurigakan di jaringan internal dan memutus akses penyusup sebelum mereka berhasil mencuri file "Financial_Report_2026.pdf".

### Tahap 1: Monitoring & Detection (Radar Aktif)

Anda sedang menyeruput kopi ketika tiba-tiba dasbor **SIEM** (Security Information and Event Management) Anda menyalakan lampu kuning.

* **Kejadian:** Muncul peringatan *"Multiple Failed Login Attempts"* dari satu akun karyawan (Si Admin IT yang fotonya viral tadi).
* **Cara Main:** Anda melihat log mentah. Ternyata ada upaya login VPN dari IP publik yang tidak dikenal (bukan dari rumah karyawan tersebut).
* **Tindakan:** Anda menandai IP tersebut sebagai *Suspicious*.

### Tahap 2: Triage & Analysis (Detektif Digital)

Penyusup (Infiltrator) berhasil masuk menggunakan kredensial yang ia curi lewat WiFi palsu. Di layar Anda, status berubah menjadi **High Alert**.

* **Kejadian:** Akun karyawan tersebut melakukan *Network Scanning* (menggunakan `Nmap`) ke seluruh server internal. Ini perilaku yang sangat tidak wajar untuk seorang karyawan biasa.
* **Cara Main:** Anda membuka **Wireshark** atau alat analisis trafik lainnya. Anda melihat ribuan paket data "ping" yang dikirimkan dalam waktu singkat ke berbagai IP server.
* **Analisis:** "Ini bukan error sistem, ini adalah pengintaian aktif!"

### Tah  3: Containment (Mengunci Pintu)

Penyusup berhasil menemukan server database tua yang memiliki celah (vulnerabilitas) dan mencoba melakukan *Exploitation*.

* **Kejadian:** Muncul peringatan *"Unauthorized Privilege Escalation"* di server database. Seseorang mencoba menjadi **Root/Administrator**.
* **Cara Main:** Anda tidak menunggu sampai dia berhasil. Anda menggunakan **EDR** (Endpoint Detection and Response) untuk mengisolasi server tersebut dari jaringan agar penyusup tidak bisa berpindah ke server lain (*Lateral Movement*).
* **Tindakan:** Anda menonaktifkan akun VPN karyawan yang disusupi secara paksa (*Force Logout*) dan meriset *password*-nya saat itu juga.

### Tahap 4: Eradication & Recovery (Pembersihan)

Penyusup sekarang terputus koneksinya. Dia gagal mengambil file finansial.

* **Kejadian:** Anda memeriksa apakah ada "pintu belakang" (*Backdoor*) yang sempat ditinggalkan oleh penyusup.
* **Cara Main:** Anda melakukan *Deep Scan* pada server database yang sempat disentuh. Anda menemukan satu file skrip mencurigakan bernama `hidden_shell.php`.
* **Tindakan:** Anda menghapus skrip tersebut, menambal (*patching*) celah di server database tersebut, dan membuat laporan insiden.

### 📊 Hasil Akhir (Win Condition)

Sebagai **SOC Analyst**, kemenangan Anda adalah:

1. **Detection Time:** Anda mendeteksi serangan dalam hitungan menit sejak dimulai.
2. **Data Integrity:** File rahasia perusahaan tetap aman dan tidak sempat terunduh.
3. **Future Proof:** Anda merekomendasikan tim IT untuk segera mematikan server database tua dan mewajibkan MFA (Multi-Factor Authentication) bagi semua karyawan.

### 🛠️ "Equipment" (Skillset) yang Anda Gunakan:

Untuk menjadi Guardian yang hebat seperti ini, Anda perlu mengasah:

* **Log Analysis:** Paham cara membaca aktivitas di Windows, Linux, dan Firewall.
* **SIEM Tools:** Mahir menggunakan alat seperti Splunk, ELK Stack, atau Microsoft Sentinel.
* **Threat Intelligence:** Selalu *update* tentang metode serangan terbaru agar tahu apa yang harus dicari.
* **Incident Response:** Tenang di bawah tekanan saat harus mengambil keputusan cepat (mematikan server atau memutus akun).

