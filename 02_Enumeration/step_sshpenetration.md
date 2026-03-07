# **cara berpikir seorang pentester / hacker saat menyerang server melalui SSH**

---

# 1. Apakah IP server sama seperti IP di `ipconfig`?

Jawabannya: **bisa sama, bisa juga berbeda.**

Ketika kita menjalankan:

```bash
ipconfig
```

di Windows, kita akan melihat **IP address perangkat kita sendiri**.

Contoh:

```
IPv4 Address : 192.168.1.25
Subnet Mask  : 255.255.255.0
Default Gateway : 192.168.1.1
```

Artinya:

| IP           | Fungsi         |
| ------------ | -------------- |
| 192.168.1.25 | IP laptop kita |
| 192.168.1.1  | IP router      |

Jadi **IP di ipconfig adalah IP device tersebut di jaringan**.

---

# 2. Dari mana IP address didapat?

Biasanya dari **DHCP server (router atau server jaringan)**.

Alurnya seperti ini:

```
Laptop dinyalakan
        ↓
Laptop meminta IP ke router
        ↓
Router (DHCP) memberikan IP
        ↓
Laptop mendapatkan IP seperti 192.168.1.25
```

Ini disebut **Dynamic IP**.

Kadang server memakai **Static IP** supaya tidak berubah.

Contoh server perusahaan:

```
192.168.1.10 → Server database
192.168.1.15 → Server website
192.168.1.20 → Server SSH
```

---

# 3. Apakah hacker bisa mengetahui IP server?

Ya, ada beberapa cara.

### 1️⃣ Scan jaringan

Tool yang biasa dipakai:

```
nmap
```

Contoh:

```bash
nmap 192.168.1.0/24
```

Artinya:

➡️ Scan semua IP dalam network tersebut.

Output bisa seperti:

```
192.168.1.10
192.168.1.15
192.168.1.20
```

---

### 2️⃣ OSINT (Open Source Intelligence)

Kadang server bisa ditemukan dari:

* DNS
* domain
* shodan
* censys

Contoh:

```
example.com
```

di-resolve menjadi:

```
34.201.12.10
```

---

# 4. Dari mana hacker mengetahui username?

Ada banyak cara.

### 1️⃣ Default username

Banyak sistem memakai default:

```
root
admin
ubuntu
ec2-user
user
```

---

### 2️⃣ Dari kebocoran data

Contoh:

```
email perusahaan
username github
dokumen internal
```

---

### 3️⃣ Dari folder server

Kadang hacker sudah masuk sebagai user lain.

Lalu menjalankan:

```bash
ls /home
```

Output:

```
sammie
johnny
linda
```

Ini artinya ada 3 user di server.

---

### 4️⃣ Username enumeration

Beberapa service bisa menunjukkan username valid.

Misalnya melalui:

```
SSH
FTP
Web login
```

---

# 5. Alur lengkap serangan SSH (mindset hacker)

Ini **workflow umum dalam penetration testing**.

---

# STEP 1 — Reconnaissance (Pengumpulan informasi)

Hacker mencari informasi tentang target.

Tools:

```
whois
nslookup
shodan
google dork
```

Tujuan:

* menemukan IP
* domain
* teknologi yang digunakan

Contoh:

```
target.com → 34.210.22.11
```

---

# STEP 2 — Network Scanning

Setelah dapat IP, hacker scan port.

Tool:

```
nmap
```

Contoh:

```bash
nmap -sS 34.210.22.11
```

Output:

```
22/tcp open  ssh
80/tcp open  http
443/tcp open https
```

Artinya:

➡️ Server membuka **port 22 (SSH)**.

---

# STEP 3 — Service Enumeration

Hacker mencari informasi tentang service SSH.

Contoh:

```bash
nmap -sV -p22 34.210.22.11
```

Output:

```
OpenSSH 7.6
```

Tujuan:

* mengetahui versi
* mencari vulnerability

---

# STEP 4 — Username Enumeration

Hacker mencoba mengetahui user.

Contoh:

```
root
admin
ubuntu
john
sammie
```

Kadang ditemukan dari:

```
/home
leaked data
github
```

---

# STEP 5 — Password Attack

Jika username sudah diketahui, hacker mencoba password.

Metode:

### 1️⃣ brute force

Tool:

```
hydra
medusa
ncrack
```

Contoh:

```bash
hydra -l sammie -P rockyou.txt ssh://10.10.10.5
```

Artinya:

* user: sammie
* password list: rockyou.txt

---

### 2️⃣ password guessing

Contoh:

```
dragon
password123
company2024
```

Ini yang dilakukan di **TryHackMe lab**.

---

# STEP 6 — Initial Access

Jika password benar:

```
ssh sammie@10.10.10.5
```

Hacker berhasil masuk server.

Sekarang mereka memiliki **low privilege access**.

---

# STEP 7 — Post Exploitation

Setelah masuk server, hacker mulai eksplorasi.

Command umum:

```
whoami
id
ls
pwd
cat
```

Contoh:

```
whoami
```

Output:

```
sammie
```

---

# STEP 8 — Privilege Escalation

Hacker mencoba menjadi **root**.

Contoh:

```
sudo -l
```

atau mencari:

```
misconfigured sudo
SUID files
cron jobs
kernel exploit
```

Jika berhasil:

```
root access
```

---

# STEP 9 — Persistence

Hacker memastikan tetap bisa masuk.

Contoh:

```
menambah SSH key
membuat user baru
```

Misalnya:

```
user: backupadmin
```

---

# STEP 10 — Covering Tracks

Hacker menghapus jejak.

Contoh:

```
history -c
clear log
```

atau menghapus log:

```
/var/log/auth.log
```

---

# Gambaran lengkap serangan SSH

```
Recon
   ↓
IP ditemukan
   ↓
Scan port (nmap)
   ↓
Port 22 terbuka
   ↓
Cari username
   ↓
Brute force password
   ↓
SSH login berhasil
   ↓
Exploration
   ↓
Privilege escalation
   ↓
Persistence
   ↓
Cover tracks
```

---

# Hal penting yang perlu kamu tahu (defense)

Server yang aman biasanya memiliki:

✅ **fail2ban**
(blok brute force)

✅ **SSH key authentication**

✅ **disable password login**

✅ **limit login attempts**

✅ **2FA**

---
