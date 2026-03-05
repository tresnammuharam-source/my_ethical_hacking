## Operating Systems (OS)

materi penting banget karena semua serangan, defense, forensik, dan cloud nantinya akan berdiri di atas konsep OS ini.

Materi **Operating Systems Basics** di TryHackMe biasanya membahas dari:

* OS Introduction
* User & Kernel Mode
* Processes
* Memory
* File Systems
* Permissions
* Basic Commands

Aku akan jelaskan lebih dalam + analogi + hubungan ke cybersecurity supaya benar-benar nyambung.

---

# 🧠 1️⃣ OS Introduction – Apa Itu Operating System?

## 📌 Definisi

Operating System (OS) adalah software inti yang:

* Menghubungkan user dengan hardware
* Mengatur CPU, RAM, Storage
* Mengontrol proses & file
* Mengatur permission

Tanpa OS → komputer tidak bisa dipakai.

---

## 🏢 Analogi: OS = Manajer Gedung

Bayangkan komputer adalah gedung besar.

* CPU = Mesin utama
* RAM = Meja kerja
* Storage = Gudang
* User = Penyewa

OS adalah **manajer gedung** yang:

* Atur siapa boleh masuk
* Atur listrik
* Atur ruangan
* Atur jadwal

---

# 🔐 2️⃣ Kernel Mode vs User Mode

Ini bagian penting.

## Kernel Mode

* Akses penuh ke hardware
* Bisa akses memory semua program
* Bisa kontrol CPU

## User Mode

* Tempat aplikasi berjalan
* Akses terbatas
* Tidak bisa akses hardware langsung

---

## 🧠 Kenapa Dipisah?

Kalau semua program punya akses kernel:

* Malware bisa kontrol seluruh sistem
* Sistem mudah crash

Jadi dibuat pembatasan privilege.

---

## 🔥 Hubungan ke Hacking

Privilege escalation =
User mode → naik ke kernel mode

Kalau berhasil → attacker punya kontrol penuh.

---

# ⚙️ 3️⃣ Processes

## Apa Itu Process?

Program yang sedang berjalan.

Contoh:

* Browser dibuka → jadi process
* Terminal dibuka → jadi process

---

## Komponen Process

* PID (Process ID)
* Memory allocation
* CPU usage
* Owner (user)

---

## 🧠 Analogi

Program = resep
Process = masakan yang sedang dibuat

---

## Perintah Linux

```bash
ps aux
top
htop
```

---

## 🔥 Kenapa Penting?

Attacker:

* Inject code ke process
* Hijack process
* Spawn reverse shell

Defender:

* Monitor process aneh
* Deteksi malware

---

# 🧵 4️⃣ Threads

Process bisa punya beberapa thread.

Thread = unit eksekusi kecil dalam process.

Contoh:
Browser:

* 1 thread untuk UI
* 1 thread untuk network
* 1 thread untuk rendering

Lebih efisien daripada buat process baru.

---

# 🧠 5️⃣ Memory Management

OS harus:

* Mengatur RAM
* Menghindari tabrakan memory
* Menggunakan virtual memory

---

## Virtual Memory

Kalau RAM penuh:
OS pakai disk sebagai swap.

---

## Memory Isolation

Setiap process:

* Punya ruang memory sendiri
* Tidak bisa akses memory process lain

---

## 🔥 Serangan di Memory

* Buffer overflow
* Memory corruption
* Use-after-free
* Heap exploitation

Semua ini terjadi karena manipulasi memory.

---

# 📂 6️⃣ File System

OS mengatur:

* Bagaimana file disimpan
* Struktur folder
* Metadata

---

## Struktur Linux

```bash
/
├── bin
├── etc
├── home
├── var
├── root
```

---

## Pentingnya Permission

Setiap file punya:

* Owner
* Group
* Permission

---

# 🔑 7️⃣ Permissions

Format:

```bash
-rwxr-xr--
```

Artinya:

| Posisi | Arti    |
| ------ | ------- |
| r      | read    |
| w      | write   |
| x      | execute |

---

## User Types

* root (superuser)
* normal user
* system user

---

## 🔥 Hubungan ke Privilege Escalation

Salah permission bisa:

* Bikin file bisa diubah attacker
* Bikin script root bisa dimodifikasi
* Bikin SUID abuse

---

# 👤 8️⃣ Users & Groups

OS mengatur:

* Banyak user
* Hak akses berbeda

Contoh:

```bash
/etc/passwd
/etc/shadow
```

---

## Root

User paling kuat di Linux.

Root bisa:

* Baca semua file
* Kill semua process
* Install apapun

---

# 🖥 9️⃣ Shell & CLI

Shell adalah interface ke OS.

Contoh:

* bash
* zsh

Shell menjalankan:

* Perintah
* Script
* Program

---

## Kenapa Penting di Cyber?

Semua hacking di Linux:

* Reverse shell
* Privilege escalation
* Enumeration
* Exploitation

Dilakukan lewat shell.

---

# 🔄 🔟 Boot Process (Ringkas)

Saat komputer dinyalakan:

1. BIOS/UEFI aktif
2. Load bootloader
3. Load kernel
4. Kernel start system services
5. Login screen muncul

---

# 🧠 1️⃣1️⃣ Interrupt & System Calls

User mode tidak bisa akses hardware langsung.

Jadi gunakan:

System Call

Contoh:

* Open file
* Read file
* Create process

Kernel yang mengerjakan.

---

# 🔐 1️⃣2️⃣ Kenapa Semua Ini Penting untuk Cybersecurity?

Karena serangan selalu melibatkan OS.

Contoh:

| Layer   | Serangan         |
| ------- | ---------------- |
| Process | Code injection   |
| Memory  | Buffer overflow  |
| File    | Permission abuse |
| User    | Credential theft |
| Kernel  | Rootkit          |

---

# 🧩 Gambaran Besar Final

```text
Hardware
↑
Kernel (akses penuh)
↑
System Calls
↑
User Space
↑
Process
↑
User
```

Semua berjalan bertingkat.

---

# 🎯 Inti yang Harus Kamu Kuasai

1. OS adalah pengatur hardware.
2. Kernel punya akses penuh.
3. Process adalah program berjalan.
4. Memory diisolasi.
5. File punya permission.
6. User punya privilege berbeda.
7. Root = kontrol penuh.
8. Semua serangan OS berhubungan dengan privilege & memory.

---
