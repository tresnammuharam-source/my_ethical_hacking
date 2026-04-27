# [Judul Singkat & Jelas: Deskripsi Bug di Domain/Endpoint]

## 1. Executive Summary
**Vulnerability:** [Nama Bug, misal: IDOR, SQLi, dsb]

**Severity:** [Critical/High/Medium/Low]

**Target:** `https://api.target.com/v1/user/data`

**Reporter:** @username_anda

---

## 2. Description
[Jelaskan secara singkat apa itu bug tersebut dan mengapa itu berbahaya. Fokus pada fungsionalitas yang terganggu.]

## 3. Impact
[PENTING: Jelaskan apa yang bisa dilakukan penyerang. Misal: "Penyerang dapat mengambil alih akun user lain tanpa interaksi" atau "Mengekspos data PII seperti NIK dan Alamat".]

## 4. Proof of Concept (PoC)
### Prerequisites:
- Akun A (Attacker)
- Akun B (Victim)

### Steps to Reproduce:
1. Login ke Akun A.
2. Buka menu Pengaturan Profil.
3. Klik "Simpan" sambil menangkap request menggunakan Burp Suite.
4. Perhatikan parameter `user_id=123`.
5. Ubah `user_id` menjadi `124` (ID Akun B).
6. Server merespon dengan `200 OK` dan data Akun B muncul.

### Payload/Code (Jika ada):
`GET /api/v1/user/data?id=124 HTTP/1.1`

---

## 5. Supporting Materials
* [Tautan ke Gambar/Screenshot]
* [Tautan ke Video Record]

## 6. Recommended Mitigation
[Berikan saran perbaikan, misal: "Implementasikan pemeriksaan otorisasi di sisi server (IDOR check) sebelum mengembalikan data."]
