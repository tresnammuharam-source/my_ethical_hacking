<img width="790" height="201" alt="image" src="https://github.com/user-attachments/assets/3d66f8ca-31df-4285-b668-44963a473c55" />

# HTTP in detail
artinya kamu harus tau bagaimana cara kerja HTTP, isinya apa, alur pembuatannya seperti apa, dan informasi apa yang bisa kita ambil dari HTTP
## HyperText Transfer Protocol (HTTP)
## HyperText Transfer Protocol Secure (HTTPS)

# 🌐 Apa Itu HTTP?

HTTP adalah singkatan dari:

> **HyperText Transfer Protocol**

HTTP adalah protokol yang digunakan untuk:

> Mengirim dan menerima data antara client (browser) dan server (website).

Ketika kamu membuka:

```
http://example.com
```

Browser kamu menggunakan HTTP untuk berkomunikasi dengan server.

---

# 🧠 Cara Kerja HTTP (Sederhana)

Modelnya disebut:

> Client – Server Model

1️⃣ Client (browser) mengirim **HTTP Request**
2️⃣ Server menerima dan memproses
3️⃣ Server mengirim **HTTP Response**
4️⃣ Browser menampilkan hasilnya

---

# 📦 Struktur HTTP Request

Contoh request sederhana:

```
GET / HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

Mari kita pecah:

---

## 🔹 1️⃣ Request Line

```
GET / HTTP/1.1
```

Artinya:

* GET → method
* / → path
* HTTP/1.1 → versi protokol

---

## 🔹 2️⃣ Headers

Berisi informasi tambahan:

```
Host:
User-Agent:
Cookie:
Authorization:
```

Header penting banget dalam web hacking.

---

## 🔹 3️⃣ Body (Opsional)

Biasanya ada di method POST:

```
username=admin&password=1234
```

---

# 📥 Struktur HTTP Response

Contoh response:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1500
```

Lalu di bawahnya ada HTML.

---

# 📊 HTTP Status Code

Ini sangat penting di TryHackMe.

| Code | Arti                  |
| ---- | --------------------- |
| 200  | OK                    |
| 301  | Redirect              |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 500  | Internal Server Error |

Pentester sering mencari:

* 403 bypass
* 500 error untuk info leak

---

# 🔥 HTTP Methods (Sangat Penting)

| Method  | Fungsi                    |
| ------- | ------------------------- |
| GET     | Mengambil data            |
| POST    | Mengirim data             |
| PUT     | Update data               |
| DELETE  | Menghapus data            |
| PATCH   | Update sebagian           |
| OPTIONS | Cek method yang diizinkan |

Kadang server salah konfigurasi dan mengizinkan PUT atau DELETE.

Itu bisa jadi celah besar.

---

# 🔐 Apa Itu HTTPS?

HTTPS adalah:

> HTTP + SSL/TLS encryption

Bedanya:

HTTP → tidak terenkripsi
HTTPS → terenkripsi

Port:

* HTTP = 80
* HTTPS = 443

---

# 🎯 Konsep Penting di HTTP (Web Hacking)

---

## 1️⃣ Cookies

Digunakan untuk:

* Session login
* Tracking user

Contoh:

```
Cookie: PHPSESSID=abc123
```

Kalau dicuri → session hijacking.

---

## 2️⃣ Headers Manipulation

Kadang bisa bypass dengan ubah header:

```
X-Forwarded-For:
Referer:
User-Agent:
```

---

## 3️⃣ Parameter Tampering

Misalnya:

```
?id=10
```

Diubah jadi:

```
?id=1 OR 1=1
```

→ SQL Injection.

---

## 4️⃣ Directory Traversal

```
/page?file=../../etc/passwd
```

---

# 🔎 HTTP Version

| Version  | Ciri                      |
| -------- | ------------------------- |
| HTTP/1.1 | Paling umum               |
| HTTP/2   | Lebih cepat, multiplexing |
| HTTP/3   | Pakai QUIC                |

---

# 🛡 Dalam Analisa Packet (Wireshark)

Filter:

```
http
```

Kamu bisa lihat:

* Request
* Response
* Header
* Cookie
* Status code

Kalau HTTP (bukan HTTPS), semua bisa dibaca plaintext.

---

# 🔥 Kenapa HTTP Penting Untuk Cyber Security?

Karena:

✔ Hampir semua aplikasi modern berbasis web
✔ 80% bug bounty ada di HTTP layer
✔ SQLi, XSS, IDOR, CSRF → semua lewat HTTP

Kalau kamu paham HTTP, kamu bisa:

* Membaca request mentah
* Menggunakan Burp Suite
* Memodifikasi request
* Melakukan fuzzing

---

# 🎯 Ringkasan Inti

HTTP adalah protokol komunikasi web.

Strukturnya:

* Request
* Response
* Header
* Body
* Status code

Digunakan hampir semua aplikasi internet.

---

bahas 3 hal:

1️⃣ Cara melihat HTTP request via CTRL+U (View Source)
2️⃣ Simulasi membaca HTTP request di Burp Suite
3️⃣ Cara latihan manual intercept & modifikasi request

Semua ini untuk latihan di lab seperti TryHackMe atau environment sendiri ya.

---

# 🧪 1️⃣ Melihat HTTP dengan CTRL + U (Dasar)

CTRL+U = View Page Source.

Yang kamu lihat:

* HTML
* CSS
* JS

⚠ Tapi ini BUKAN HTTP request mentah.

Untuk lihat request sebenarnya:

👉 Tekan F12
👉 Masuk tab “Network”
👉 Refresh halaman

Klik salah satu request → lihat:

* Method (GET/POST)
* URL
* Headers
* Response
* Cookies

---

# 🧠 Contoh HTTP Request Login

Misalnya kamu login ke website lab.

Di tab Network kamu mungkin lihat:

```
POST /login HTTP/1.1
Host: target.com
Content-Type: application/x-www-form-urlencoded
Cookie: session=abc123

username=admin&password=1234
```

Sekarang kita bedah.

---

## 🔎 Analisa

Method: POST → Mengirim data
Path: /login → Endpoint login
Cookie: session → Session ID
Body: username & password

Di sinilah semua serangan web dimulai.

---

# 🔥 2️⃣ Simulasi Membaca Request di Burp Suite

Langkah setup:

1️⃣ Buka Burp Suite
2️⃣ Set browser proxy ke 127.0.0.1:8080
3️⃣ Aktifkan “Intercept is On”
4️⃣ Buka website target

Sekarang request akan tertahan di Burp.

---

## 🎯 Contoh Request yang Tertangkap

```
POST /login HTTP/1.1
Host: lab.local
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 29

username=admin&password=admin
```

---

## 🧠 Cara Membacanya

Perhatikan:

### 🔹 1. Endpoint

`/login`

Bisa dicoba brute force atau SQLi.

---

### 🔹 2. Parameter

```
username=
password=
```

Bisa dimodifikasi.

Contoh uji SQLi:

```
username=admin' OR 1=1--
password=test
```

---

### 🔹 3. Cookie

```
Cookie: session=abc123
```

Bisa diuji:

* Session fixation
* Session hijacking

---

# 🧪 3️⃣ Cara Latihan Manual Intercept & Modifikasi

Sekarang bagian praktik mindset pentester.

---

## 🎯 Latihan 1: Ubah Parameter

Intercept request login.

Ubah:

```
username=user
```

Menjadi:

```
username=admin
```

Forward.

Lihat response.

---

## 🎯 Latihan 2: Ubah Role ID

Misalnya ada request:

```
GET /profile?id=2
```

Coba ubah jadi:

```
GET /profile?id=1
```

Lihat apakah bisa akses akun lain.

Ini disebut:
IDOR (Insecure Direct Object Reference).

---

## 🎯 Latihan 3: Coba Manipulasi Header

Tambahkan header:

```
X-Forwarded-For: 127.0.0.1
```

Kadang bisa bypass restriction admin.

---

# 🔍 Cara Analisa Response

Perhatikan:

Status Code:

* 200 → berhasil
* 302 → redirect
* 403 → forbidden
* 500 → error (menarik!)

Perhatikan juga:

* Perubahan ukuran response
* Perubahan pesan error

---

# 🧠 Mindset Saat Intercept

Tanya ke diri sendiri:

✔ Bisa ubah parameter?
✔ Ada parameter tersembunyi?
✔ Bisa ubah method GET → POST?
✔ Ada cookie sensitif?
✔ Ada token CSRF?

---

# 🚀 Latihan di Lab

Kamu bisa latihan di:

* Room HTTP di TryHackMe
* DVWA (Damn Vulnerable Web App)
* Juice Shop

Semua aman untuk latihan.

---
