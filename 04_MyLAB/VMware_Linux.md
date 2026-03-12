# Cara Menginstal Kali Linux dan VMware

Karena Anda menggunakan **VirtualBox** atau **VMware**, Anda memiliki akses penuh ke fitur jaringan Kali Linux dibandingkan menggunakan WSL.

Agar alat seperti `arpspoof` atau `netdiscover` bisa mendeteksi perangkat lain di Wi-Fi Anda, pastikan pengaturan **Network Adapter** di mesin virtual diatur ke mode **Bridged Adapter**, bukan NAT.

### Cara Cek Akses di VM:

1. Ketik `ip a` di terminal Kali Linux.
2. Jika IP yang muncul satu segmen dengan router Anda (misal `192.168.1.xxx`), berarti Anda sudah siap beraksi.
3. Jika IP yang muncul `10.0.2.xxx`, Anda masih dalam mode NAT dan tidak bisa melihat perangkat lain di jaringan.

Berikut adalah perbedaan mendasar antara mode isolasi (NAT/Host-Only) dan mode eksternal (Bridged) di Virtual Machine:

### Perbandingan Mode Jaringan

| Fitur | **NAT (Isolasi Lab)** | **Bridged (Eksploit Keluar)** |
| --- | --- | --- |
| **Alamat IP** | Berbeda segment dengan router (biasanya `10.0.2.x`). | Satu segment dengan router (sama dengan PC host). |
| **Akses Internet** | Bisa (melalui Host). | Bisa (langsung ke Router). |
| **Deteksi Perangkat** | Hanya bisa melihat VM lain di lab internal yang sama. | Bisa melihat semua perangkat (HP, Laptop, CCTV) di Wi-Fi. |
| **Keamanan** | **Aman**. Eksperimen tidak akan menyebar ke jaringan asli. | **Beresiko**. VM Anda terlihat dan bisa menyerang jaringan asli. |

---

### Cara Mengubah Pengaturan

1. Matikan VM Kali Linux Anda.
2. Buka **Settings** > **Network**.
3. Ubah **Attached to** menjadi:
* **NAT** jika ingin lab tertutup (belajar perintah dasar).
* **Bridged Adapter** jika ingin memindai atau memutuskan koneksi perangkat lain di Wi-Fi Anda.

**Bridged Mode** memposisikan VM Anda seolah-olah perangkat fisik yang terhubung langsung ke router. Dalam mode ini, Kali Linux mendapatkan alamat IP asli dari jaringan Wi-Fi, sehingga Anda bisa melakukan pemindaian, *man-in-the-middle*, atau eksploitasi terhadap perangkat nyata seperti ponsel atau laptop lain di rumah Anda.

### Langkah setelah masuk Mode Bridged:

1. Jalankan `sudo netdiscover -r [Network_IP]/24` untuk memetakan seluruh target di jaringan.
2. Pilih satu IP target untuk dipindai port-nya menggunakan `nmap`.

## Experiment di VM Kali Linux dalam Isolasi Lab Mode

Anda harus membuat **Target Lab** berupa mesin virtual kedua (seperti Metasploitable atau Windows VM) yang diatur dalam jaringan yang sama (**NAT Network** atau **Host-Only**). Dengan cara ini, Anda bisa bebas berlatih menyerang tanpa risiko merusak jaringan asli atau melanggar hukum.

### Aktivitas yang Bisa Dilakukan di Lab Terisolasi:

* **Scanning & Enumeration:** Melatih `nmap` untuk mendeteksi layanan pada VM target.
* **Exploitation:** Menggunakan **Metasploit** untuk menembus celah keamanan VM target.
* **Brute Force:** Mencoba menebak *password* layanan SSH atau FTP pada mesin lab.
* **Sniffing:** Belajar membaca lalu lintas data antar VM menggunakan Wireshark.

Keuntungannya adalah Anda bisa sengaja membuat VM target menjadi lemah dan rentan agar bisa belajar cara kerja serangan secara aman.

Jika Anda baru pertama kali belajar **CLI (Command Line Interface)**, sangat disarankan menggunakan **mode isolasi (NAT)**.

### Mengapa Memilih Isolasi?

* **Keamanan:** Anda tidak akan sengaja mengirim paket data yang dianggap berbahaya oleh router atau ISP Anda.
* **Fokus:** Anda bisa belajar perintah dasar seperti `ls`, `cd`, `mkdir`, dan `grep` tanpa gangguan dari lalu lintas jaringan luar yang kompleks.
* **Eksperimen Bebas:** Anda bisa mencoba menghapus atau memodifikasi file sistem tanpa takut merusak koneksi perangkat lain di rumah.

### Langkah Belajar Pertama:

1. Gunakan mode **NAT** agar tetap punya akses internet untuk *update* paket (`sudo apt update`).
2. Pelajari navigasi direktori dan pengelolaan file.
3. Gunakan perintah `man [nama_perintah]` untuk membaca buku manual setiap alat.

