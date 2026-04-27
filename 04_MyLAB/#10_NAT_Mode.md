# NAT Mode dalam Kali Linux VM ware

Dalam mode NAT, fokus terbaik adalah pada target yang berada di luar jaringan lokal (Internet)
atau serangan yang tidak mengandalkan komunikasi langsung antar-perangkat di satu WiFi.

Berikut adalah aktivitas dan tools yang tetap berjalan optimal di mode NAT:

### Aktivitas yang Bisa Dilakukan
* **Web Application Pentesting:** Menguji celah keamanan pada website publik (SQL Injection, XSS).
* **Social Engineering:** Mengirim link phishing ke target mana pun.
* **OSINT:** Mengumpulkan informasi dari sumber terbuka di internet.
* **Cracking Password:** Menjalankan serangan *brute force* pada layanan cloud.

### Tools yang Cocok
| Kategori | Tools |
| :--- | :--- |
| **Web Pentest** | **Burp Suite**, OWASP ZAP, Nikto |
| **Exploitation** | **Metasploit** (menggunakan *reverse connection* via ngrok) |
| **Vulnerability Scanner** | **Nmap** (untuk target publik), Nuclei |
| **Phishing/Tunneling** | **Zphisher**, **Ngrok**, Cloudflared |
| **Information Gathering** | **TheHarvester**, Sherlock, Whois |

> **Penting:** Karena VM Anda "tersembunyi" di balik IP Host, Anda wajib menggunakan **Ngrok** atau **LocalXpose** jika ingin menerima koneksi balik (*reverse shell*) dari target di internet.

