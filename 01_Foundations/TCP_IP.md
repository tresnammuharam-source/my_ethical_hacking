# Apa itu TPC/IP???

**TCP/IP** adalah standar komunikasi data yang digunakan di internet agar berbagai perangkat bisa saling "berbicara". Protokol ini bekerja dalam empat lapisan utama:
<img width="471" height="447" alt="image" src="https://github.com/user-attachments/assets/0f2ca1a8-34f5-4763-9c39-96a62945cff5" />

1. **Network Access Layer:** Mengatur koneksi fisik (kabel, Wi-Fi, MAC Address).
2. **Internet Layer (IP):** Bertugas mengalamatkan data dan menentukan rute terbaik (routing) agar paket sampai ke tujuan menggunakan **IP Address**.
3. **Transport Layer (TCP/UDP):** Memastikan data terkirim dengan benar. **TCP** bersifat reliabel (ada pengecekan error), sedangkan **UDP** mengutamakan kecepatan (untuk *streaming/gaming*).
4. **Application Layer:** Lapisan tempat aplikasi bekerja, seperti browsing melalui **HTTP/S**, mengirim email via **SMTP**, atau transfer file via **FTP**.

Ibarat mengirim surat, **IP** adalah alamat di amplopnya, sedangkan **TCP** adalah kurir yang memastikan surat tersebut sampai ke tangan penerima tanpa sobek.

## cara melihat koneksi TCP yang sedang aktif di terminal Kali Linux

Jalankan perintah `ss -tunap` atau `netstat -tunap` di terminal Kali Linux Anda untuk melihat daftar koneksi aktif.

### Penjelasan Parameter:

* **-t**: Menampilkan koneksi **TCP**.
* **-u**: Menampilkan koneksi **UDP**.
* **-n**: Menampilkan alamat dan port dalam bentuk **angka** (bukan nama layanan).
* **-a**: Menampilkan semua *socket* (baik yang sedang mendengarkan maupun sudah terhubung).
* **-p**: Menunjukkan **program/proses** yang menggunakan koneksi tersebut.

Coba jalankan sekarang, apakah Anda melihat ada port **80 (HTTP)** atau **443 (HTTPS)** yang sedang *Established*?

Di CMD Windows, gunakan perintah **`netstat -ano`**.

### Penjelasan Parameter:

* **`-a`**: Menampilkan semua koneksi dan port yang sedang *listening*.
* **`-n`**: Menampilkan alamat dan nomor port dalam bentuk angka.
* **`-o`**: Menampilkan **PID** (Process ID) agar Anda tahu aplikasi mana yang memiliki koneksi tersebut.

Jika Anda ingin melihat aplikasi apa yang menggunakan PID tersebut, Anda bisa mencocokkannya di **Task Manager** pada tab *Details*.

## cara menghentikan (*kill*) koneksi yang mencurigakan melalui CLI

Untuk menghentikan proses atau koneksi mencurigakan di Linux, Anda perlu menemukan **PID (Process ID)** terlebih dahulu menggunakan perintah `ss -tunap` atau `netstat -tap`.

### Langkah Menghentikan Proses:

1. **Identifikasi PID**: Lihat kolom paling kanan pada hasil perintah `ss` atau `netstat`.
2. **Gunakan perintah `kill**`:
* `sudo kill <PID>` : Mengirim sinyal terminasi standar (lebih halus).
* `sudo kill -9 <PID>` : Memaksa proses berhenti seketika (digunakan jika proses membandel).

### Contoh di Windows (CMD):

Jika Anda di Windows, gunakan:

* `taskkill /PID <nomor_pid> /F`

**Hati-hati:** Jangan menghentikan proses sistem yang kritikal (seperti PID 1 di Linux) karena bisa menyebabkan sistem *crash*.

## Cara melacak lokasi geografis dari sebuah IP yang sedang terkoneksi ke komputer kita

Untuk melacak lokasi geografis sebuah IP di Kali Linux, Anda bisa menggunakan perintah **`curl`** yang dikombinasikan dengan API pelacak IP publik.

### Langkah Melacak IP:

1. Dapatkan IP tujuan dari hasil `ss -tunap` sebelumnya.
2. Ketik perintah berikut di terminal:
`curl ipapi.co/8.8.8.8/json/`
*(Ganti `8.8.8.8` dengan IP yang ingin Anda selidiki).*

### Informasi yang Didapat:

* **City & Region**: Lokasi kota dan provinsi.
* **Country**: Nama negara.
* **Org/ISP**: Penyedia layanan internet (misal: Telkomsel, Biznet, atau Google).

Ini sangat berguna untuk mendeteksi apakah ada koneksi dari negara yang tidak seharusnya (misalnya koneksi mencurigakan dari luar negeri).

## Cara melacak IP publik sendiri

Gunakan perintah `curl ifconfig.me` untuk mengetahui **IP Publik** Anda sendiri terlebih dahulu. Setelah itu, masukkan IP tersebut ke dalam perintah pelacakan:

`curl ipapi.co/[IP_ANDA]/json/`

### Analisis Hasil:

* **Org/ASN:** Menunjukkan ISP yang Anda gunakan (seperti Telkom, Indosat, atau Biznet).
* **Latitude/Longitude:** Koordinat perkiraan lokasi perangkat Anda.

## cara melakukan "Whois" untuk melihat siapa pemilik domain atau IP tersebut secara lebih mendalam

Gunakan perintah `whois` untuk melihat data registrasi domain atau IP secara mendalam. Di terminal Kali Linux, cukup ketik:

`whois [alamat_ip_atau_domain]`

### Data yang Akan Muncul:

* **Registrant:** Nama pemilik atau organisasi.
* **Name Servers:** Server yang mengarahkan trafik domain.
* **Expiry Date:** Kapan masa aktif domain berakhir.
* **Contact Info:** Email atau nomor telepon untuk pelaporan penyalahgunaan (*abuse*).

Jika perintah `whois` belum terpasang, instal dengan `sudo apt install whois`.

## cara mencari "pintu masuk" (port) yang terbuka pada IP tersebut menggunakan Nmap

Gunakan perintah **`nmap`** untuk memindai port yang terbuka pada sebuah target. Di terminal Kali Linux, ketik:

`nmap -v [alamat_ip_atau_domain]`

### Penjelasan Parameter:

* **`-v` (Verbose):** Menampilkan proses pemindaian secara *real-time* agar Anda tidak menunggu dalam ketidakpastian.
* **Port & State:** Hasilnya akan menunjukkan nomor port (misal: 80, 443, 22) dan statusnya (**Open** berarti pintu terbuka, **Closed** berarti tertutup).
* **Service:** Memberitahu layanan apa yang berjalan di sana (seperti HTTP, HTTPS, atau SSH).

**Hati-hati:** Jangan memindai server milik orang lain tanpa izin tertulis karena bisa dianggap sebagai upaya serangan ilegal.

