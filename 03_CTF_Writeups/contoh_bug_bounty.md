## Contoh Laporan Nyata (Case: Broken Access Control)

Berikut adalah contoh bagaimana template di atas diisi agar terlihat sangat meyakinkan:

# [IDOR] Disclosure of Private User Addresses via `/api/v1/shipping/`

## 1. Executive Summary
* **Vulnerability:** Insecure Direct Object Reference (IDOR)
* **Severity:** **High (8.2)**
* **Target:** `https://shop.example.com/api/v1/shipping/`

---

## 2. Description
Ditemukan kerentanan IDOR pada endpoint pengiriman barang. Sistem tidak melakukan verifikasi apakah `address_id` yang diminta benar-benar milik pengguna yang sedang login (authenticated user).

## 3. Impact
Penyerang dapat melakukan *scraping* massal terhadap seluruh alamat fisik pengguna di platform, termasuk nama lengkap dan nomor telepon. Ini melanggar regulasi privasi data (GDPR/UU PDP).

## 4. Proof of Concept (PoC)
1. Login sebagai `user_attacker`.
2. Akses alamat pengiriman saya sendiri di `https://shop.example.com/api/v1/shipping/999`.
3. Ganti ID `999` menjadi `1000`, `1001`, dst.
4. Server mengembalikan data lengkap milik pengguna lain.

### HTTP Request:
```http
GET /api/v1/shipping/1000 HTTP/1.1
Host: shop.example.com
Authorization: Bearer <attacker_token>
```

### HTTP Response (Victim Data Exposed):
```json
{
  "status": "success",
  "data": {
    "full_name": "Budi Santoso",
    "phone": "+62812345678",
    "address": "Jl. Sudirman No. 1, Jakarta Pusat"
  }
}
```

---

## 5. Supporting Materials
* **Screenshot:** `![Alt text](https://i.imgur.com/link_po_anda.png)`
* **Video PoC:** Attached (poc_video.mp4)

## 6. Recommended Mitigation
Pastikan backend memvalidasi kepemilikan objek:
```sql
SELECT * FROM addresses WHERE id = ? AND user_id = ?;
```

---

### Tips Agar Cepat Dibayar:
1.  **Jangan Berlebihan (Don't Oversell):** Jika bugnya Medium, jangan dipaksa jadi Critical. Triage akan lebih menghargai kejujuran teknis.
2.  **Sertakan HTTP Request/Response:** Ini memudahkan mereka melakukan reproduksi instan tanpa menebak-nebak.
3.  **Gunakan Bahasa Inggris yang Jelas:** Jika melaporkan ke platform internasional, gunakan bahasa Inggris yang *to-the-point*.
4.  **Format Markdown:** Gunakan blok kode (seperti contoh di atas) agar kode tidak berantakan.

Apakah Anda sedang menangani temuan tertentu yang ingin saya bantu susun kalimat penjelasannya?
