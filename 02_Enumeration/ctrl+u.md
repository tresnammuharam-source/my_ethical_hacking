## Sekarang kita fokus ke **analisa website dari sisi browser**, bukan dari sisi network scanning.

Kita bahas:

1️⃣ Apa itu CTRL+U
2️⃣ Bagaimana cara kerjanya
3️⃣ Apa yang harus dicari
4️⃣ Manfaatnya dalam security / pentesting

---

# 🧠 Apa Itu CTRL+U?

CTRL+U = **View Page Source**

Fungsi:
Menampilkan **kode HTML mentah** dari halaman website.

Yang kamu lihat:

* Struktur HTML
* Komentar developer
* Script JavaScript
* Link file CSS
* Link file JS
* Kadang informasi tersembunyi

⚠ Ini bukan hacking. Ini fitur normal browser.

---

# 🔍 Bagaimana Cara Kerjanya?

Ketika kamu buka website:

1. Browser kirim HTTP request
2. Server kirim HTML response
3. Browser render halaman
4. CTRL+U menampilkan HTML asli sebelum dirender

Jadi kamu melihat **source code yang dikirim server**.

---

# 🧪 Apa Yang Harus Dicari Saat CTRL+U?

Ini bagian penting 🔥

## 1️⃣ Komentar Developer

Cari:

```html
<!-- admin login at /secret_admin -->
```

Kadang developer lupa hapus komentar sensitif.

---

## 2️⃣ Hidden Input Field

Contoh:

```html
<input type="hidden" name="role" value="user">
```

Kalau diubah jadi `admin` bisa jadi celah.

---

## 3️⃣ File JavaScript

Cari file seperti:

```html
<script src="app.js"></script>
```

Buka file JS → kadang ada:

* API key
* Endpoint rahasia
* Token
* URL internal

---

## 4️⃣ Directory / Endpoint Tersembunyi

Misalnya kamu lihat:

```html
<a href="/backup/">
```

Atau:

```html
<form action="/process_login.php">
```

Itu bisa jadi target enumerasi.

---

## 5️⃣ Meta Data

Contoh:

```html
<meta name="generator" content="WordPress 5.4">
```

Sekarang kamu tahu:
Website pakai WordPress versi tertentu → bisa cari vulnerability.

---

## 6️⃣ Email atau Informasi Internal

Kadang ada:

```html
<!-- Contact dev: admin@company.local -->
```

Bisa dipakai untuk recon.

---

# 🎯 Manfaat CTRL+U Dalam Security

| Manfaat                      | Kenapa Penting              |
| ---------------------------- | --------------------------- |
| Recon                        | Mengumpulkan informasi awal |
| Temukan endpoint tersembunyi | Bisa jadi entry point       |
| Identifikasi teknologi       | Bisa cari exploit           |
| Cari komentar sensitif       | Info leak                   |
| Analisa form                 | Uji parameter               |

---

# ⚠ Apa Yang Tidak Bisa Dilihat Dengan CTRL+U?

CTRL+U TIDAK bisa melihat:

* Password database
* Source code backend (PHP asli, Python, dll)
* Server configuration
* File di server yang tidak di-link

Karena kamu hanya melihat:
👉 Apa yang dikirim ke browser.

---

# 🔥 Lebih Powerful Dari CTRL+U

Untuk analisa lebih dalam gunakan:

## F12 → Developer Tools

Tab penting:

* Network → lihat HTTP request
* Application → lihat cookie
* Console → lihat error JS
* Sources → lihat file JS lengkap

---

# 🧪 Contoh Mindset Praktik

Saat buka website, lakukan:

1. CTRL+U → cari komentar & hidden data
2. F12 → cek request login
3. Lihat cookie → ada session?
4. Lihat file JS → ada endpoint API?

---

# 🧠 Contoh Kasus Nyata

Kadang developer meninggalkan:

```html
<!-- TODO: remove admin_test.php before production -->
```

Kalau kamu akses:

```
website.com/admin_test.php
```

Dan terbuka → itu vulnerability.

---

# 🚨 Tapi Ingat

Gunakan hanya pada:

* Website milik sendiri
* Lab seperti TryHackMe
* Platform legal seperti Hack The Box

Jangan uji ke website orang tanpa izin.

---

# 🎓 Kesimpulan

CTRL+U adalah:

✔ Teknik recon dasar
✔ Cara memahami struktur website
✔ Langkah awal sebelum pakai Burp Suite
✔ Membantu menemukan titik masuk

---
