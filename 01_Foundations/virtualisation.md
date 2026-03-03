# Virtualisation Basics
Learn why virtualisation powers modern IT, improving efficiency and safely isolating environments.

Kalau kamu masuk ke materi **Virtualisation Basics** di TryHackMe, itu artinya kamu sedang masuk ke fondasi yang sangat penting untuk:

* Lab ethical hacking
* SOC simulation
* Cloud security
* Malware analysis
* Red team & blue team

Sekarang kita bahas runtut seperti alur materi di TryHackMe, tapi lebih dalam.

# 1️⃣ Apa Itu Virtualisation?

## 📌 Definisi Sederhana

Virtualisation adalah:

> Menjalankan banyak sistem operasi di dalam satu mesin fisik menggunakan software.

Bayangkan:

* Kamu punya 1 laptop
* Tapi bisa menjalankan:

  * Windows
  * Linux
  * Kali Linux
  * Server Ubuntu

Semua berjalan bersamaan.

---

# 2️⃣ Kenapa Virtualisation Penting?

Sebelum virtualisasi:

1 server fisik = 1 sistem operasi
Boros biaya dan resource.

Sekarang:

1 server fisik = banyak virtual machine (VM)

Keuntungannya:

* Hemat hardware
* Isolasi lingkungan
* Aman untuk testing
* Fleksibel
* Bisa snapshot & rollback

---

# 3️⃣ Komponen Utama Virtualisation

## 🖥 Host

Mesin fisik tempat virtual machine berjalan.

Contoh:
Laptop kamu.

---

## 💻 Guest

Sistem operasi virtual yang berjalan di atas host.

Contoh:

* Kali Linux
* Ubuntu Server
* Windows Server

---

## 🧠 Hypervisor

Ini inti dari virtualisasi.

Hypervisor adalah software yang:

> Mengatur dan membagi resource hardware ke VM

Ia bertindak sebagai “manajer”.

---

# 4️⃣ Jenis Hypervisor

## 🔹 Type 1 (Bare Metal)

Hypervisor langsung berjalan di atas hardware.

Contoh:

* VMware ESXi
* Hyper-V Server

Digunakan di data center.

---

## 🔹 Type 2 (Hosted)

Hypervisor berjalan di atas OS biasa.

Contoh:

* VirtualBox
* VMware Workstation

Biasanya untuk lab dan pembelajaran.

Kalau kamu bikin lab ethical hacking di laptop:
→ Itu pakai Type 2.

---

# 5️⃣ Bagaimana VM Bekerja?

Misalnya:

Laptop kamu punya:

* RAM 16GB
* CPU 8 core

Kamu buat:

* VM Kali → 4GB RAM, 2 core
* VM Ubuntu → 4GB RAM, 2 core

Hypervisor membagi resource itu.

VM tidak tahu dia bukan mesin fisik.

---

# 6️⃣ Virtual Network

Ini penting banget buat kamu.

VM bisa punya network sendiri:

Mode umum:

## 🔹 NAT

VM bisa internet, tapi tidak terlihat dari luar.

Aman untuk lab.

---

## 🔹 Bridged

VM seperti perangkat biasa di jaringan rumah.

Bisa di-scan dari device lain.

---

## 🔹 Host-Only

VM hanya bisa komunikasi dengan host.

Dipakai untuk lab isolated.

---

# 7️⃣ Kenapa Virtualisation Penting dalam Cyber Security?

Ini bagian yang paling penting buat kamu.

---

## 🔥 1. Isolasi

Kalau kamu:

* Eksploit malware
* Uji exploit
* Jalankan payload

Kalau rusak?
→ Hanya VM yang rusak, bukan laptop utama.

---

## 🔥 2. Snapshot

Sebelum exploit:

Klik snapshot.

Kalau gagal?
→ Rollback.

Ini seperti save point di game.

---

## 🔥 3. Simulasi Jaringan

Kamu bisa buat:

```text
VM 1 = Attacker (Kali)
VM 2 = Victim (Windows)
VM 3 = Server
```

Dan latih:

* Port scanning
* Exploit
* Lateral movement

Tanpa ganggu jaringan rumah.

---

## 🔥 4. Malware Analysis

Malware dijalankan di VM agar:

* Tidak menyebar
* Bisa dipantau
* Bisa dihancurkan setelah selesai

---

# 8️⃣ Virtualisation vs Container

Virtual Machine:

* Punya OS sendiri
* Lebih berat
* Lebih terisolasi

Container:

* Berbagi kernel OS
* Lebih ringan
* Cepat

Dalam cybersecurity:
VM lebih aman untuk testing exploit.

---

# 9️⃣ Risiko Virtualisation

Tidak 100% aman.

Ada konsep:

## VM Escape

Jika exploit berhasil:
Malware bisa keluar dari VM ke host.

Jarang, tapi mungkin.

Makanya:

* Update hypervisor
* Jangan sembarangan buka file malware

---

# 🔟 Hubungan Dengan Lab Ethical Hacking Kamu

Karena kamu mau bangun mindset SOC & lab sendiri:

Struktur ideal:

```text
Host (Windows utama)

VM 1 → Kali Linux (Attacker)
VM 2 → Ubuntu Server (Target)
VM 3 → Windows VM (Victim)
```

Network:

* Host-only atau NAT

Tambahkan:

* Wireshark untuk capture packet
* IDS seperti Snort

---

# 🧠 Kenapa TryHackMe Mengajarkan Ini?

Karena semua room hacking:

* Jalan di VM
* Gunakan isolasi
* Simulasikan target

Tanpa virtualisasi:
Tidak ada lab modern cybersecurity.

---

# 🎯 Inti Konsep yang Harus Kamu Tangkap

1. Virtualisasi memungkinkan banyak OS dalam satu mesin.
2. Hypervisor mengatur resource.
3. VM aman untuk testing.
4. Snapshot memungkinkan rollback.
5. Network mode menentukan isolasi.
6. Penting untuk lab ethical hacking & SOC simulation.

