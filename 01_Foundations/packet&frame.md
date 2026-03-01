---

# 1️⃣ Apa Itu Packet?

## 📦 Packet = Unit Data di Layer Network (Layer 3 – IP)

**Packet** adalah potongan data yang dikirim melalui jaringan berdasarkan protokol IP.

Kalau internet itu jalan raya, maka:

* **Packet = mobil yang membawa barang**
* Isinya ada:

  * Alamat tujuan
  * Alamat pengirim
  * Data yang dikirim

### Struktur Packet (IP Packet)

Di dalam packet ada:

1. **IP Header**

   * Source IP
   * Destination IP
   * TTL
   * Protocol (TCP / UDP / ICMP)

2. **Payload**

   * Isi data (misalnya HTTP request, DNS query, dll)

Contoh:

```
Source IP: 192.168.1.10
Destination IP: 8.8.8.8
Protocol: TCP
Data: GET /index.html
```

---

# 2️⃣ Apa Itu Frame?

## 🖼 Frame = Unit Data di Layer Data Link (Layer 2 – Ethernet)

**Frame adalah pembungkus packet.**

Kalau packet itu mobil,
maka frame itu seperti **kontainer/truk yang mengangkut mobil di dalam satu kota (LAN).**

Frame bekerja di jaringan lokal.

### Struktur Frame (Ethernet Frame)

1. **MAC Address Tujuan**
2. **MAC Address Sumber**
3. **Type (IPv4 / IPv6)**
4. **Payload (berisi packet)**
5. **FCS (Error checking)**

Jadi urutannya seperti ini:

```
Frame
 └── Packet
      └── Segment (TCP/UDP)
           └── Data
```

---

# 3️⃣ Alur Kerja Packet & Frame (Step-by-step)

Misalnya kamu akses:

```
https://google.com
```

### 🔁 Prosesnya:

### 1️⃣ Data Dibuat di Aplikasi

Browser membuat HTTP request.

### 2️⃣ Dibungkus Jadi Segment (Layer 4)

TCP menambahkan:

* Source port
* Destination port

### 3️⃣ Dibungkus Jadi Packet (Layer 3)

IP menambahkan:

* Source IP
* Destination IP

### 4️⃣ Dibungkus Jadi Frame (Layer 2)

Ethernet menambahkan:

* Source MAC
* Destination MAC

### 5️⃣ Dikirim ke Router

Router:

* Membuka frame
* Membaca packet
* Membungkus ulang jadi frame baru
* Kirim ke jaringan berikutnya

Ini terjadi berkali-kali sampai ke tujuan.

---

# 4️⃣ Hubungan Dengan Cyber Security 🔥

Ini bagian yang penting buat kamu sebagai calon ethical hacker.

---

## 🎯 1. Packet Sniffing

Tools seperti:

* Wireshark
* tcpdump

Bekerja dengan membaca **packet & frame yang lewat di jaringan**.

Attacker bisa:

* Mencuri credential
* Melihat HTTP plaintext
* Melihat DNS query

Makanya HTTPS penting.

---

## 🎯 2. Packet Manipulation

Di penetration testing, kamu bisa:

* Mengubah packet
* Membuat packet palsu
* Kirim packet custom

Tools:

* Scapy
* hping3

Contoh:

* SYN flood (DDoS)
* Spoofing IP

---

## 🎯 3. ARP Spoofing (Layer 2 Attack)

Karena frame menggunakan MAC Address,
maka attacker bisa:

* Mengirim ARP palsu
* Mengganti MAC address gateway
* Jadi Man-in-the-Middle

Inilah kenapa ARP poisoning bahaya di jaringan lokal.

---

## 🎯 4. IDS/IPS & SOC Monitoring

Di dunia SOC (Security Operation Center):

* Firewall memeriksa packet
* IDS membaca header
* SIEM mencatat traffic

Mereka menganalisa:

* Source IP mencurigakan?
* Port scanning?
* Banyak SYN tapi tidak ACK?

Semua berbasis analisis packet.

---

# 5️⃣ Ringkasan Konsep (Versi Lab TryHackMe)

| Layer   | Unit Data | Fungsi                            |
| ------- | --------- | --------------------------------- |
| Layer 2 | Frame     | Kirim data di LAN (pakai MAC)     |
| Layer 3 | Packet    | Routing antar jaringan (pakai IP) |
| Layer 4 | Segment   | Komunikasi aplikasi (port)        |

---

# 6️⃣ Kenapa Ini Penting Buat Kamu?

Karena kalau kamu ingin:

* Bangun LAB SOC rumahan
* Analisa log firewall
* Pahami PCAP file
* Lolos challenge TryHackMe networking

Kamu HARUS paham:

> Mana yang MAC level (frame)
> Mana yang IP level (packet)

---

# 7️⃣ Gambaran Serangan Berdasarkan Layer

| Layer   | Contoh Attack |
| ------- | ------------- |
| Layer 2 | ARP spoofing  |
| Layer 3 | IP spoofing   |
| Layer 4 | SYN flood     |
| Layer 7 | SQL injection |

---
