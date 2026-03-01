# 🔎 Apa Itu “Extending Your Network”?

Dalam konteks networking & security, **extending your network** berarti:

> Memperluas jaringan internal agar bisa:

* Terhubung ke internet
* Menghubungkan cabang
* Menghubungkan remote worker
* Menambah server publik
* Menambahkan DMZ

Begitu jaringan diperluas → **risiko meningkat**
Dan di sinilah firewall dan kontrol keamanan berperan.

---

# 🧱 Struktur Dasar Network yang Diperluas

Contoh arsitektur sederhana:

```
Internet
   |
[ Firewall ]
   |
[ Router ]
   |
-------------------------
|         |             |
LAN      Server        WiFi
```

Kalau diperluas lagi:

```
Internet
   |
[ Firewall ]
   |
------------------------
|                      |
DMZ                  Internal LAN
|                      |
Web Server           User PC
```

---

# 🔥 1️⃣ Firewall – Garda Terdepan

## Apa Itu Firewall?

Firewall adalah perangkat (hardware/software) yang:

> Mengontrol traffic masuk & keluar berdasarkan rule

Ia bekerja dengan membaca **packet** (IP, port, protocol).

---

## 🧠 Cara Kerja Firewall

Firewall membaca:

* Source IP
* Destination IP
* Port
* Protocol (TCP/UDP)
* State connection (kalau stateful)

Lalu mencocokkan dengan rule.

Contoh rule:

```
ALLOW 192.168.1.0/24 → ANY port 80
DENY  ANY → port 22
```

---

## 🔥 Jenis Firewall

### 1️⃣ Packet Filtering Firewall

* Cek header saja
* Cepat
* Tidak cek isi data

### 2️⃣ Stateful Firewall

* Cek status koneksi
* Tahu SYN, ACK, FIN
* Lebih aman

### 3️⃣ Next-Generation Firewall (NGFW)

* Bisa baca Layer 7
* Bisa deteksi malware
* Bisa inspeksi HTTPS (deep inspection)

---

# 🌐 2️⃣ NAT (Network Address Translation)

Kalau jaringan diperluas ke internet,
IP private tidak bisa langsung dipakai.

Maka digunakan NAT.

Contoh:

```
192.168.1.10 → 103.20.10.5
```

Firewall/router:

* Mengganti IP private jadi public
* Menyimpan tabel koneksi

### Risiko Security:

* NAT tidak sama dengan security
* Hanya menyembunyikan IP
* Bukan proteksi penuh

---

# 🌍 3️⃣ Port Forwarding

Jika kamu punya server di dalam LAN:

```
Public IP: 103.20.10.5
Web server internal: 192.168.1.20
```

Firewall rule:

```
Forward port 80 → 192.168.1.20
```

⚠ Risiko:

* Membuka akses dari internet
* Harus dikombinasikan dengan:

  * Firewall rule
  * IDS/IPS
  * Hardening server

---

# 🏰 4️⃣ DMZ (Demilitarized Zone)

Ini bagian penting dalam “Extending Your Network”.

DMZ adalah zona terpisah untuk server publik.

Struktur:

```
Internet
   |
[ Firewall ]
   |
   |---- DMZ (Web Server)
   |
Internal LAN (User, Database)
```

Kenapa?

Kalau web server diretas:

* Hacker tidak langsung masuk ke LAN
* Hanya sampai DMZ

---

# 🛡 5️⃣ IDS & IPS

Dalam network yang diperluas:

* Firewall = penjaga gerbang
* IDS = alarm
* IPS = alarm + bisa blokir

IDS membaca packet dan mendeteksi:

* Port scanning
* Brute force
* Malware signature
* Suspicious traffic

---

# 🔐 6️⃣ VPN (Virtual Private Network)

Kalau kamu punya cabang atau remote worker:

```
User di rumah → VPN → Firewall → LAN kantor
```

VPN:

* Enkripsi traffic
* Buat koneksi seolah-olah dalam LAN

Risiko:

* Jika credential bocor → attacker masuk seperti orang dalam

---

# 📡 7️⃣ Network Segmentation

Kalau jaringan makin besar:

Jangan semua device satu jaringan.

Pisahkan:

* VLAN User
* VLAN Server
* VLAN Finance
* VLAN Guest

Kenapa?

Jika satu PC kena ransomware:
→ Tidak langsung menyebar ke semua network

Ini prinsip **zero trust & least privilege**.

---

# 🔥 Contoh Serangan Jika Tidak Diamankan

| Fitur                  | Risiko                   |
| ---------------------- | ------------------------ |
| Port Forwarding        | Server langsung di-scan  |
| Tidak ada DMZ          | Hacker masuk ke database |
| Tidak ada firewall     | Semua port terbuka       |
| Tidak ada segmentation | Lateral movement mudah   |
| VPN tanpa MFA          | Credential stuffing      |

---

# 🎯 Dalam Perspektif SOC (Untuk Kamu)

Karena kamu mau bangun mindset SOC:

Ketika network diperluas, kamu harus monitor:

* Inbound traffic
* Outbound traffic aneh
* Banyak SYN?
* Port scanning?
* IP luar mencoba login?
* VPN login dari negara aneh?

Semua ini dianalisis dari **packet & log firewall**.

---

# 🔬 Hubungan dengan Ethical Hacking

Sebagai ethical hacker, kamu harus tahu:

Kalau mau pivot:

* Cari port forwarding salah
* Cari firewall rule longgar
* Cari DMZ yang salah konfigurasi
* Cari segmentation lemah

---

# 🧠 Inti Materi “Extending Your Network”

Semakin luas jaringan:
→ Semakin besar attack surface
→ Semakin penting kontrol keamanan

Prinsipnya:

1. Deny by default
2. Buka hanya yang perlu
3. Segmentasi
4. Monitor traffic
5. Enkripsi koneksi

