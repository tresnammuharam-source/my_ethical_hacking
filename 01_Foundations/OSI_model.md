# OSI model (or Open Systems Interconnection Model)

Model ini menyediakan kerangka kerja yang mengatur bagaimana semua perangkat dalam jaringan mengirim, menerima, dan menafsirkan data.

Salah satu manfaat utama dari model OSI adalah perangkat dapat memiliki fungsi dan desain yang berbeda dalam suatu jaringan tetapi tetap dapat berkomunikasi satu sama lain. Data yang dikirim melalui jaringan yang mengikuti standar model OSI dapat dipahami oleh perangkat lain.

Model OSI terdiri dari tujuh layer (lapisan) yang ditunjukkan pada diagram. Setiap layer memiliki tanggung jawab yang berbeda dan disusun dari Layer 7 hingga Layer 1.

Pada setiap layer yang dilewati oleh data, terdapat proses tertentu yang terjadi, dan potongan informasi tambahan ditambahkan ke data tersebut. Proses ini disebut encapsulation (enkapsulasi). Untuk saat ini, kita hanya perlu memahami bahwa proses tersebut disebut encapsulation dan bagaimana struktur model OSI terlihat dalam diagram tersebut.

- 7 Application
- 6 Presentation
- 5 Session
- 4 Transport
- 3 Network
- 2 Data Link
- 1 Physical

OSI MODEL adalah Kerangka kerja yang menjelaskan bagaimana data bergerak dari satu device ke device lain melalui jaringan.

Model ini dibuat supaya semua perangkat (Windows, Linux, Cisco, dll) bisa berkomunikasi dengan standar yang sama.

Tanpa model seperti ini, jaringan akan kacau karena tiap vendor bisa pakai aturan sendiri.

Bayangkan kamu kirim pesan lewat internet.

Pesan itu dalam prosesnya harus:

1. Dibuat oleh aplikasi
2. Diubah menjadi format jaringan
3. Diberi alamat tujuan
4. Dikirim lewat kabel / WiFi
5. Diterima
6. Dibuka kembali oleh aplikasi

OSI membagi semua proses itu menjadi 7 layer supaya lebih terstruktur.

tahapan OSI disebut dengan Layer:

- 7 Application :	Interaksi dengan aplikasi (browser, email)
- 6 Presentation :	Enkripsi & format data
- 5 Session :	Mengatur sesi komunikasi
- 4 Transport	: Mengatur pengiriman (TCP/UDP)
- 3 Network :	Routing & IP address
- 2 Data Link	: MAC address & switch
- 1 Physical	: Kabel, sinyal, listrik

Encapsulation adalah Proses menambahkan informasi tambahan pada data saat turun dari Layer 7 ke Layer 1.

dalam cyber security pemaham OSI Model ini penting karean setiap layernya mempunya kerentanan keamanan:
Karena hampir semua serangan terjadi di layer tertentu.

Contoh:

1. Phishing → Layer 7
2. SSL attack → Layer 6
3. Session hijacking → Layer 5
4. TCP SYN flood → Layer 4
5. IP spoofing → Layer 3
6. ARP spoofing → Layer 2
7. Kabel dicabut → Layer 1

Jika kita memahami maka kita akan tahu:

✔ Tahu serangan terjadi di layer mana
✔ Tahu harus troubleshooting di mana
✔ Tahu bagaimana paket dimanipulasi

