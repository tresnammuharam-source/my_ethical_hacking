# MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge)

## Mengenal MITRE ATT&CK

**MITRE ATT&CK** (Adversarial Tactics, Techniques, and Common Knowledge) adalah sebuah basis pengetahuan (knowledge base) yang mendokumentasikan perilaku penyerang siber berdasarkan observasi di dunia nyata. Jika dianalogikan dalam dunia kepolisian, ini adalah kumpulan "Modus Operandi" para kriminal digital yang disusun secara sistematis.

Framework ini menjadi standar industri bagi tim keamanan (Blue Team) untuk memahami cara kerja penyerang dan bagi penguji keamanan (Red Team) untuk mensimulasikan ancaman yang nyata.

---

### 1. Struktur Utama: Taktik, Teknik, dan Prosedur (TTP)

Untuk memahami ATT&CK, kita harus melihat tiga komponen utamanya yang sering disebut sebagai **TTP**:

* **Tactics (Taktik):** Merupakan tujuan strategis penyerang (the "Why"). Mengapa penyerang melakukan tindakan tersebut? Contohnya: *Initial Access* (mendapatkan akses masuk) atau *Exfiltration* (mencuri data).
* **Techniques (Teknik):** Merupakan cara spesifik penyerang mencapai tujuan taktis tersebut (the "How"). Contohnya: Untuk mencapai taktik *Initial Access*, penyerang mungkin menggunakan teknik *Phishing*.
* **Procedures (Prosedur):** Merupakan implementasi spesifik atau langkah demi langkah yang digunakan oleh kelompok penyerang tertentu (APT). Contohnya: "Grup APT28 mengirim email phishing dengan lampiran dokumen Word berbahaya yang mengeksploitasi celah CVE-2017-0199."

---

### 2. Matriks ATT&CK

MITRE membagi basis pengetahuan ini ke dalam beberapa matriks berdasarkan lingkungan target:

1. **Enterprise:** Mencakup sistem operasi tradisional (Windows, macOS, Linux) serta infrastruktur Cloud (AWS, Azure, GCP, Office 365) dan Network.
2. **Mobile:** Berfokus pada ancaman terhadap perangkat Android dan iOS.
3. **ICS (Industrial Control Systems):** Berfokus pada infrastruktur kritis seperti pembangkit listrik atau pabrik.

Di dalam matriks Enterprise, terdapat **14 Taktik** utama yang mengikuti alur serangan dari awal hingga akhir (sering disebut sebagai *Kill Chain*):

| Taktik | Penjelasan Singkat |
| --- | --- |
| **Reconnaissance** | Mengumpulkan informasi untuk merencanakan serangan. |
| **Resource Development** | Menyiapkan infrastruktur (misal: membeli domain, menyewa VPS). |
| **Initial Access** | Mencoba masuk ke dalam jaringan target. |
| **Execution** | Menjalankan kode berbahaya di sistem. |
| **Persistence** | Menjaga akses agar tetap ada meskipun sistem di-reboot. |
| **Privilege Escalation** | Berusaha mendapatkan hak akses yang lebih tinggi (Admin/Root). |
| **Defense Evasion** | Menghindari deteksi oleh antivirus atau EDR. |
| **Credential Access** | Mencuri username dan password. |
| **Discovery** | Menjelajahi lingkungan internal untuk mencari tahu konfigurasi sistem. |
| **Lateral Movement** | Berpindah dari satu komputer ke komputer lain di dalam jaringan. |
| **Collection** | Mengumpulkan data yang menjadi target utama. |
| **Command and Control** | Berkomunikasi dengan sistem yang telah terinfeksi dari jarak jauh. |
| **Exfiltration** | Memindahkan data curian keluar dari jaringan. |
| **Impact** | Merusak, memanipulasi, atau mengganggu operasional sistem. |

---

### 3. Cara Menggunakan MITRE ATT&CK

Ada beberapa alat dan metode yang biasa digunakan untuk berinteraksi dengan framework ini:

* **ATT&CK Navigator:** Alat berbasis web yang memungkinkan kita memvisualisasikan matriks, memberi warna pada teknik tertentu, dan memetakan pertahanan yang kita miliki terhadap teknik penyerang.
* **Groups & Software:** MITRE menyediakan daftar kelompok penyerang (misal: APT41, Lazarus Group) dan perangkat lunak/malware yang mereka gunakan. Ini membantu tim keamanan melakukan *Threat Profiling*.
* **Mitigations & Detection:** Setiap teknik di MITRE disertai dengan saran cara mencegahnya (*Mitigation*) dan cara mendeteksinya (*Detection data sources*).

---

### 4. Contoh Kasus (Scenario)

Bayangkan sebuah insiden di mana seorang karyawan menerima email palsu dan mengklik link yang mengunduh file `.exe`.

1. **Taktik:** *Initial Access* -> **Teknik:** *Phishing* (Spearphishing Link).
2. **Taktik:** *Execution* -> **Teknik:** *User Execution* (Karyawan menjalankan file tersebut).
3. **Taktik:** *Persistence* -> **Teknik:** *Registry Run Keys* (Malware mendaftarkan diri di registry agar otomatis jalan saat PC menyala).

Dengan memetakan insiden ke dalam MITRE ATT&CK, tim SOC (Security Operations Center) dapat dengan mudah mengomunikasikan celah mana yang perlu diperbaiki dan log apa yang perlu dipantau di masa depan.

