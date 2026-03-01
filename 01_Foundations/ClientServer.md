# 1️⃣ Apa Itu Client dan Server?

## 🖥 Client

Client adalah perangkat atau aplikasi yang:

* Meminta layanan
* Mengirim request
* Menginisiasi komunikasi

Contoh:

* Browser (Chrome, Edge)
* Aplikasi mobile
* Curl
* Nmap (saat scanning)

---

## 🗄 Server

Server adalah:

* Sistem yang menyediakan layanan
* Menunggu request
* Memberikan response

Contoh:

* Web server
* DNS server
* Database server
* FTP server

---

# 2️⃣ Bagaimana Client-Server Berkomunikasi?

Model dasar:

```id="9q7dnx"
Client  →  Request  →  Server
Client  ←  Response ←  Server
```

Contoh nyata:
Kamu buka:

```id="kd7z2m"
https://example.com
```

Yang terjadi:

1. Client kirim request
2. Server proses
3. Server kirim response
4. Client tampilkan hasil

---

# 3️⃣ Request dan Response (Struktur Dasar)

Dalam HTTP misalnya:

## 🔹 HTTP Request

Berisi:

* Method (GET, POST, PUT, DELETE)
* URL
* Header
* Body (opsional)

Contoh:

```id="4kx2pq"
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla
```

---

## 🔹 HTTP Response

Berisi:

* Status code
* Header
* Body

Contoh:

```id="w8f3nd"
HTTP/1.1 200 OK
Content-Type: text/html

<html>...</html>
```

---

# 4️⃣ Port dan Service

Server “menunggu” di port tertentu.

Contoh umum:

| Service | Port |
| ------- | ---- |
| HTTP    | 80   |
| HTTPS   | 443  |
| SSH     | 22   |
| FTP     | 21   |
| DNS     | 53   |

Kalau kamu scan dengan nmap:

```id="cx4d1t"
nmap 192.168.1.10
```

Kamu sedang mencari:

> Service apa yang dijalankan server?

---

# 5️⃣ TCP 3-Way Handshake (Bagian Penting)

Sebelum client-server kirim data (kalau TCP), mereka buat koneksi dulu.

Prosesnya:

```id="v3s8mn"
1. Client → SYN
2. Server → SYN-ACK
3. Client → ACK
```

Baru setelah itu data dikirim.

Ini penting banget di cybersecurity karena:

* SYN flood attack menyerang tahap ini
* Firewall membaca proses ini
* IDS mendeteksi anomali handshake

---

# 6️⃣ Stateless vs Stateful

## 🔹 Stateless

Setiap request berdiri sendiri.
Contoh: HTTP biasa.

Server tidak ingat client.

---

## 🔹 Stateful

Server menyimpan status koneksi.
Contoh:

* Login session
* TCP connection
* Web app session cookie

Kalau session dicuri → attacker bisa ambil alih akun.

---

# 7️⃣ DNS dalam Client-Server

Sebelum client bisa connect ke server:

```id="3c8mzy"
example.com → 93.184.216.34
```

Client tanya DNS server dulu.

Prosesnya:

1. Client → DNS request
2. DNS → IP address
3. Client → connect ke IP itu

Serangan yang sering terjadi:

* DNS spoofing
* DNS poisoning

---

# 8️⃣ Hubungan Dengan Cyber Security 🔥

Sekarang kita masuk mindset ethical hacker.

---

## 🎯 1. Enumeration

Kamu sebagai attacker:

* Scan port
* Identifikasi service
* Cek versi server

Contoh:

* Apache 2.4.49 → ada vulnerability
* OpenSSH versi lama → bisa brute force

---

## 🎯 2. Brute Force

Karena client-server model:

```id="af2m6k"
Client → login request
Server → response
```

Attacker bisa kirim ribuan request login.

---

## 🎯 3. Man in The Middle

Jika komunikasi tidak terenkripsi:

* Attacker bisa baca request
* Bisa ubah response

Makanya HTTPS penting.

---

## 🎯 4. Exploiting Server

Kalau server:

* Salah konfigurasi
* Patch lama
* Port terbuka tidak perlu

Attacker bisa:

* Remote code execution
* Data exfiltration
* Privilege escalation

---

# 9️⃣ Perspektif SOC (Defender Mindset)

Sebagai calon SOC Analyst, kamu harus bisa baca:

* Banyak request dari 1 IP?
* Banyak login gagal?
* Banyak SYN tapi tidak ACK?
* Response error 500 berulang?

Itu semua tanda serangan di model client-server.

---

# 🔟 Ringkasan Alur Komunikasi Client-Server

Urutannya seperti ini:

```id="s9x2tw"
1. Client butuh layanan
2. Client resolve DNS
3. Client kirim SYN
4. Server balas SYN-ACK
5. Client ACK
6. Client kirim request
7. Server proses
8. Server kirim response
9. Koneksi ditutup (FIN)
```

---

# 🧠 Kenapa Ini Fundamental Buat Kamu?

Karena semua serangan di TryHackMe:

* Web exploitation
* Network attack
* Privilege escalation
* Reverse shell

Semuanya berbasis model client-server.

Bahkan reverse shell pun:

> Target jadi client → connect ke attacker server


# 🍕 Analogi Client–Server = Pesan Pizza

## 🎭 Peran

| Dunia IT | Dunia Nyata                                   |
| -------- | --------------------------------------------- |
| Client   | Kamu yang pesan pizza                         |
| Server   | Restoran pizza                                |
| Request  | Pesanan kamu                                  |
| Response | Pizza yang dikirim                            |
| Port     | Nomor telepon restoran                        |
| Protocol | Cara komunikasi (telepon, WhatsApp, aplikasi) |

---

# 1️⃣ Client Menginisiasi Komunikasi

Dalam dunia IT:

> Client selalu memulai komunikasi.

Dalam analogi:
Kamu (client) yang:

* Telepon restoran
* Buka aplikasi
* Kirim pesan

Restoran tidak tiba-tiba kirim pizza tanpa kamu pesan.

---

# 2️⃣ Request = Pesanan

Kamu bilang:

```id="p1x8vd"
Saya mau 1 pizza pepperoni ukuran large.
```

Itu sama seperti:

```id="q2k9az"
GET /menu
POST /order
```

Request berisi:

* Apa yang diminta
* Detail pesanan
* Informasi tambahan (alamat, metode bayar)

Dalam HTTP:

* Method
* Header
* Body

---

# 3️⃣ Server Memproses Permintaan

Restoran:

* Cek stok
* Buat pizza
* Siapkan pengiriman

Server:

* Proses logic
* Ambil data dari database
* Generate response

---

# 4️⃣ Response = Pizza Dikirim

Restoran kirim:

```id="z7m4rt"
Pizza + struk pembayaran
```

Server kirim:

```id="x6w3nf"
HTTP 200 OK
<html>...</html>
```

Kalau stok habis?

```id="a8v2kl"
HTTP 404 Not Found
```

Kalau dapur error?

```id="b3y9pd"
HTTP 500 Internal Server Error
```

---

# 5️⃣ Port = Nomor Telepon Restoran

Restoran bisa punya banyak layanan:

* Telepon biasa
* WhatsApp
* Aplikasi online

Dalam server:

| Service    | Port |
| ---------- | ---- |
| Web        | 80   |
| Secure Web | 443  |
| SSH        | 22   |
| FTP        | 21   |

Kalau kamu salah nomor?
→ Tidak terhubung.

---

# 6️⃣ Protocol = Cara Berkomunikasi

Kamu bisa pesan lewat:

* Telepon
* WhatsApp
* Aplikasi

Dalam IT:

* HTTP
* HTTPS
* FTP
* SSH

Kalau beda protocol?
→ Tidak bisa saling mengerti.

---

# 7️⃣ TCP Handshake = "Halo, Tersambung?"

Sebelum pesan:

```id="c9n1zw"
Kamu: Halo?
Restoran: Halo?
Kamu: Ya saya mau pesan.
```

Itu seperti:

```id="h7d2ms"
SYN
SYN-ACK
ACK
```

Baru setelah itu pesanan disampaikan.

---

# 8️⃣ Stateless vs Stateful (Dalam Analogi)

## 🔹 Stateless

Setiap kali pesan:
Restoran tidak ingat kamu.

Kamu harus ulang:

* Nama
* Alamat
* Nomor HP

Itu seperti HTTP tanpa session.

---

## 🔹 Stateful

Restoran punya sistem member.
Begitu kamu telepon:

```id="k4r8tp"
"Oh Pak Tresna, biasa pesan pepperoni ya?"
```

Itu seperti:

* Cookie
* Session ID

---

# 9️⃣ Bagaimana Ini Jadi Serangan? (Versi Hacker)

Sekarang kita masuk mindset ethical hacking.

---

## 🎯 1. Brute Force

Orang iseng telepon ribuan kali:

```id="m6x1qr"
Pesan atas nama A
Pesan atas nama B
Pesan atas nama C
```

Itu seperti brute force login.

---

## 🎯 2. DDoS

Seribu orang telepon bersamaan.
Restoran tidak bisa angkat semua.

Server overload.

---

## 🎯 3. Man in the Middle

Ada orang menyadap telepon kamu.
Dia dengar alamat dan detail pesanan.

Kalau tidak HTTPS → data bisa disadap.

---

## 🎯 4. SQL Injection

Kamu bilang:

```id="v2p5lj"
Nama: ' OR 1=1 --
```

Kalau sistem restoran bodoh?
→ Semua data bocor.

---

# 🔟 Reverse Shell dalam Analogi

Biasanya:
Kamu telepon restoran.

Tapi reverse shell itu seperti:

Restoran tiba-tiba telepon kamu dan bilang:

```id="t8f6yd"
Sekarang saya ikut instruksi kamu.
```

Target jadi client.
Attacker jadi server.

---

# 🔥 Inti Konsep yang TryHackMe Mau Kamu Pahami

1. Client selalu menginisiasi komunikasi
2. Server menunggu request
3. Komunikasi menggunakan port dan protocol
4. Ada request dan response
5. Ada proses koneksi (handshake)
6. Semua serangan web berbasis model ini

---

# 🎯 Kenapa Ini Penting Buat Kamu?

Karena kalau kamu:

* Mau exploit web
* Mau analisa log
* Mau jadi SOC analyst
* Mau paham reverse shell

Kamu harus selalu tanya:

> Siapa client?
> Siapa server?
> Siapa yang mulai koneksi?
> Data lewat port berapa?
> Apakah terenkripsi?


