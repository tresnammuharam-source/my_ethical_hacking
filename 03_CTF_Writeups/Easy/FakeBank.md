# FakeBank Write-Up (CODE:200)

## Objective
Menebak-nebak nama folder/file tersembunyi di website.
Directory Enumeration / Content Discovery.

## Enumeration
Tool used:
- dirb

Command:
dirb http://target-url

Discovered:
- /admin
- /images
- /backup
- /bank-transfer

## Exploitation
Accessed hidden admin panel.
Deposited $2000 into Account No. 8881.

## How to work:
- Jalankan perintah dirb
- Tunggu sampai selesai
- Perhatikan baris yang diawali dengan tanda +
- Akan ada 2 URL yang ditemukan
- Salah satu (atau keduanya) adalah weakness

## Fundamental
- Menggunakan wordlist
- Mencoba ribuan kemungkinan URL
- Menampilkan yang valid

## Vulnerability Identified
- Developer lupa menghapus halaman lama
- Folder admin tidak diproteksi
- File backup bisa diakses publik
- Siapa saja bisa akses
- Bisa memodifikasi data finansial

## Mitigation
- Implement authentication
- Restrict admin access
- Role-based authorization

## After DIRB Done:
Langkah berikutnya biasanya:
- Buka URL yang ditemukan
- Cek apakah ada login page
- Cek apakah ada informasi sensitif
- Coba akses tanpa autentikasi

## Summary
- Bahwa menemukan halaman tersembunyi saja sudah cukup untuk eksploitasi
- Broken Access Control adalah salah satu vulnerability terbesar (OWASP Top 10)
- Hacker sering hanya perlu akses admin panel tanpa login
