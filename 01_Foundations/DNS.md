# apa itu DNS?


try tools in VM :
user@thm:~$ nslookup --type=CNAME website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

** server can't find .website.thm: NXDOMAIN
user@thm:~$ nslookup 127.0.0.53.website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

** server can't find 127.0.0.53.website.thm: NXDOMAIN
user@thm:~$ nslookup --type=A website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
Name: website.thm
Address: 10.10.10.10

user@thm:~$ nslookup website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

** server can't find .website.thm: NXDOMAIN
user@thm:~$ nslookup --type=MX website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
website.thm mail exchanger = 30 alt4.aspmx.l.google.com

user@thm:~$ nslookup --type=TXT website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
website.thm text = "THM{7012BBA60997F35A9516C2E16D2944FF}"

user@thm:~$ nslookup --type=CNAME shop.website.thm
Server: 127.0.0.53
Address: 127.0.0.53#53

Non-authoritative answer:
shop.website.thm canonical name = shops.myshopify.com

user@thm:~$ nslookup website.thm

Mantap 🔥 ini sudah masuk ke level practical pentesting + defensive analysis.

Saya akan bagi jadi 3 bagian:

1️⃣ Praktik DNS Enumeration di Lab
2️⃣ Simulasi DNS Spoofing (konsep & alur)
3️⃣ Cara membaca log / packet hasil serangan DNS

Semua ini untuk tujuan edukasi & defensive awareness ya.

---

# 🧪 1️⃣ Praktik DNS Enumeration di LAB

Kamu bisa praktik di:

* Lab pribadi (Kali Linux + target VM)
* Atau room DNS di TryHackMe

---

## 🎯 Tujuan DNS Enumeration

Mencari:

* IP target
* Subdomain
* Mail server
* Nameserver
* Zone transfer misconfig

---

## 🔹 A. Menggunakan nslookup

Cek A record:

```
nslookup example.com
```

Cek MX record:

```
nslookup -type=mx example.com
```

Cek NS record:

```
nslookup -type=ns example.com
```

---

## 🔹 B. Menggunakan dig (lebih powerful)

Cek A record:

```
dig example.com
```

Cek semua record:

```
dig example.com ANY
```

Cek zone transfer:

```
dig axfr example.com @ns1.example.com
```

Kalau zone transfer berhasil → semua subdomain akan muncul.

Itu vulnerability serius.

---

## 🔹 C. Brute Force Subdomain

Gunakan:

```
dnsrecon -d example.com
```

Atau:

```
dnsenum example.com
```

Tujuan:
Menemukan subdomain tersembunyi seperti:

```
admin.example.com
dev.example.com
vpn.example.com
```

Ini sering jadi entry point.

---

# 🎭 2️⃣ Simulasi DNS Spoofing (Konsep Serangan)

DNS Spoofing = memalsukan jawaban DNS.

---

## 🎯 Skenario

Korban ingin buka:

```
bank.com
```

Normalnya:

```
bank.com → 192.10.10.5
```

Tapi hacker memalsukan:

```
bank.com → 10.10.10.66 (server palsu)
```

---

## 🔥 Alur Serangan di LAN

1️⃣ Hacker lakukan ARP spoofing
2️⃣ Jadi man-in-the-middle
3️⃣ Jalankan DNS spoof tool
4️⃣ Korban kirim DNS request
5️⃣ Hacker jawab lebih cepat dari DNS asli
6️⃣ Korban diarahkan ke website palsu

---

## 🔎 Kenapa Bisa Berhasil?

Karena:

* DNS default tidak terenkripsi
* UDP tidak ada validasi kuat
* Client percaya jawaban pertama yang datang

---

# 🛡 Cara Mendeteksi DNS Spoofing

Sekarang bagian defensive mindset.

---

# 🔍 3️⃣ Cara Membaca Log / Packet DNS

Gunakan:

* Wireshark
* tcpdump
* Log firewall
* Log DNS server

---

## 🎯 A. Di Wireshark

Filter:

```
dns
```

Perhatikan:

* Apakah ada 2 response untuk 1 request?
* Apakah IP jawaban berbeda dari biasanya?
* Apakah TTL aneh (misal sangat kecil)?

Normal:

```
Standard query response A 192.168.1.10
```

Spoofing bisa terlihat:

```
Response from IP yang bukan DNS server resmi
```

---

## 🎯 B. Indikator DNS Spoofing

✔ Jawaban datang sangat cepat dan tidak dari server resmi
✔ IP tujuan aneh (misal IP lokal untuk domain publik)
✔ Banyak NXDOMAIN aneh
✔ TTL sangat kecil

---

## 🎯 C. Di Log DNS Server

Cek:

* Query berulang mencurigakan
* Domain panjang random (indikasi DNS tunneling)
* Lonjakan traffic port 53

---

# 🔥 Contoh Analisa Profesional

Jika kamu melihat di packet:

Request:

```
Query: bank.com
```

Response:

```
Answer: 10.0.0.66
```

Padahal seharusnya IP publik.

Artinya:

🚨 Kemungkinan DNS poisoning
🚨 Atau local hosts file manipulation
🚨 Atau rogue DHCP memberi DNS palsu

---

# 🧠 Mindset Pentester vs Defender

Sebagai pentester:

* Coba zone transfer
* Coba subdomain brute force
* Cek misconfigured DNS

Sebagai defender:

* Aktifkan DNSSEC
* Monitor traffic DNS
* Batasi zone transfer
* Gunakan IDS/IPS

---

# 🚀 Level Selanjutnya

Kalau kamu mau, saya bisa jelaskan:

* Apa itu DNSSEC dan bagaimana mencegah spoofing
* Cara analisa DNS tunneling malware
* Atau buatkan mini lab scenario step-by-step untuk latihan

Kamu sekarang sudah masuk ke tahap network security analysis 🔥

