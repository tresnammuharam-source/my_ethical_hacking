# SNORT

Snort dan perannya yang krusial dalam ekosistem SIEM (Security Information and Event Management).

Secara sederhana, jika SIEM adalah "pusat komando" yang memantau seluruh keamanan jaringan, Snort adalah salah satu "sensor lapangan" paling tajam yang mengirimkan laporan ke pusat tersebut.

Berikut adalah penjelasan mengenai hubungan keduanya:

1. Apa itu Snort?
Snort adalah sistem deteksi intrusi jaringan (Network Intrusion Detection System - NIDS) bersifat open-source.
Ia bekerja dengan cara mengamati lalu lintas jaringan secara real-time dan membandingkannya dengan kumpulan aturan (rules) untuk mendeteksi aktivitas mencurigakan, seperti:

- Pemindaian port (port scanning).
- Serangan buffer overflow.
- Upaya eksploitasi celah keamanan (SMB, HTTP, dll).
- Malware yang mencoba berkomunikasi ke luar.

2. Hubungan Snort dengan SIEM
Dalam arsitektur keamanan modern, Snort jarang berdiri sendiri. Snort bertugas menghasilkan log data yang kemudian dikirimkan ke SIEM (seperti Splunk, IBM QRadar, atau ELK Stack) untuk diproses lebih lanjut.

- Penyedia Data (Data Source): Snort menangkap ancaman di level paket data (Layer 2-7 OSI). Namun, log Snort bisa sangat banyak dan sulit dibaca secara manual. SIEM membantu mengumpulkan log tersebut di satu tempat.
- Korelasi Kejadian: SIEM dapat menghubungkan temuan dari Snort dengan data dari sumber lain. Misalnya:
- Snort mendeteksi upaya login paksa ke server.
- Log Windows menunjukkan akun administrator berhasil masuk.
- SIEM menggabungkan kedua info ini untuk membunyikan alarm "Akses Ilegal Terdeteksi!".
- Visualisasi dan Dashboard: Melalui SIEM, data dari Snort yang tadinya hanya berupa teks mentah dapat diubah menjadi grafik dan dasbor yang mudah dipahami oleh seorang SOC Analyst.

3. Mengapa Integrasi ini Penting?
Integrasi Snort ke dalam Lab atau lingkungan kerja memberikan beberapa keuntungan:

- Otomatisasi Respon: Beberapa SIEM bisa diprogram untuk memblokir IP penyerang secara otomatis di firewall setelah menerima peringatan dari Snort.
- Analisis Forensik: Jika terjadi peretasan, Anda bisa melihat kembali log Snort di SIEM untuk mengetahui kapan tepatnya serangan dimulai dan metode apa yang digunakan.

4. Implementasi Umum
Biasanya, Snort dipasang pada titik strategis di jaringan (misalnya di belakang firewall).
Log yang dihasilkan Snort akan dikirim menggunakan protokol Syslog atau bantuan agen pengirim log (seperti Filebeat atau Splunk Forwarder) menuju server SIEM.

