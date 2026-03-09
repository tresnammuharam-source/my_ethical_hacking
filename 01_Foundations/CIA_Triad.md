Materi yang kamu kirim dari **TryHackMe** menjelaskan konsep dasar keamanan yang sangat penting yaitu **CIA Triad**. Saya jelaskan **maksud materi dan tujuan latihan di room tersebut** secara lengkap.

---

# 1️⃣ Apa maksud materi ini

Materi ini ingin menunjukkan bahwa **CIA Triad bukan hanya teori**, tetapi cara berpikir (security mindset) yang digunakan oleh profesional cybersecurity saat menganalisis insiden keamanan.

CIA Triad terdiri dari 3 pilar utama:

1. **Confidentiality**
2. **Integrity**
3. **Availability**

Setiap **serangan cyber biasanya merusak salah satu atau lebih dari tiga aspek ini**.

Karena itu, ketika terjadi insiden, security analyst biasanya bertanya:

* Apakah **data rahasia bocor?** → Confidentiality
* Apakah **data diubah tanpa izin?** → Integrity
* Apakah **sistem tidak bisa diakses?** → Availability

Dengan memahami ini, seorang security professional bisa:

* menilai **dampak insiden**
* menentukan **prioritas respon**
* memilih **mitigation yang tepat**

---

# 2️⃣ Penjelasan CIA Triad

## 1. Confidentiality

Confidentiality berarti **informasi hanya boleh diakses oleh orang yang berwenang**.

Contoh pelanggaran:

* hacker mencuri database pelanggan
* password user bocor
* email rahasia dibaca orang lain

Contoh perlindungan:

* encryption
* authentication
* access control

---

## 2. Integrity

Integrity berarti **data harus tetap akurat dan tidak boleh diubah tanpa izin**.

Contoh pelanggaran:

* hacker mengubah saldo rekening
* malware mengubah file sistem
* attacker memodifikasi log

Contoh perlindungan:

* hashing
* digital signature
* file integrity monitoring

---

## 3. Availability

Availability berarti **sistem dan data harus tersedia saat dibutuhkan**.

Contoh pelanggaran:

* website tidak bisa diakses
* server down
* sistem crash

Contoh serangan:

* DDoS attack
* ransomware
* server overload

Contoh perlindungan:

* backup
* redundancy
* load balancing

---

# 3️⃣ Maksud Hands-on Scenario di TryHackMe

Dalam latihan ini kamu diberi **9 contoh insiden keamanan**.

Tugas kamu adalah:

1. Membaca setiap insiden
2. Menentukan **aspek CIA mana yang paling terdampak**
3. Menaruh insiden tersebut ke kategori:

   * Confidentiality
   * Integrity
   * Availability

Ini disebut **incident classification exercise**.

---

# 4️⃣ Contoh cara menjawab latihan ini

Contoh kasus:

### Case 1

> Hacker stole customer credit card database.

Jawaban:

```
Confidentiality
```

Karena **data rahasia bocor**.

---

### Case 2

> Attacker modified financial records.

Jawaban:

```
Integrity
```

Karena **data diubah**.

---

### Case 3

> Company website went offline due to DDoS attack.

Jawaban:

```
Availability
```

Karena **sistem tidak tersedia**.

---

# 5️⃣ Kenapa latihan ini penting

Latihan ini melatih cara berpikir seorang:

* SOC Analyst
* Security Analyst
* Incident Responder
* Pentester

Ketika terjadi insiden, mereka harus cepat memahami:

```
Apa yang rusak?
Data?
Sistem?
Kepercayaan?
```

Semua analisis itu biasanya dimulai dari **CIA triad**.

---

# 6️⃣ Alur berpikir security analyst

Ketika ada incident report, biasanya analis berpikir seperti ini:

```
Step 1
Apakah ada data rahasia bocor?
→ Confidentiality

Step 2
Apakah data diubah atau dimanipulasi?
→ Integrity

Step 3
Apakah sistem tidak bisa diakses?
→ Availability
```

---

# 7️⃣ Kesimpulan room ini

Tujuan room ini adalah:

* memahami **CIA Triad**
* memahami **dampak serangan cyber**
* belajar **mengklasifikasikan insiden keamanan**

Security professional selalu menilai insiden dengan pertanyaan:

```
What was compromised?
Confidentiality?
Integrity?
Availability?
```

---

💡 **Insight penting untuk cybersecurity career**

Hampir semua framework security menggunakan konsep CIA triad, misalnya:

* NIST Cybersecurity Framework
* OWASP
* ISO 27001

Karena itu CIA triad adalah **konsep fundamental dalam security**.

---
Dalam latihan **CIA Triad** di TryHackMe, biasanya kamu diminta **mengelompokkan beberapa incident ke dalam tiga kategori**:

* **Confidentiality** → kebocoran data
* **Integrity** → perubahan data tanpa izin
* **Availability** → sistem tidak bisa diakses

Biasanya ada **9 contoh insiden (3 untuk setiap kategori)**. Berikut contoh yang sangat sering muncul di latihan dasar cybersecurity.

---

# 1️⃣ Confidentiality (Kerahasiaan Data)

Confidentiality berarti **informasi hanya boleh diakses oleh pihak yang berwenang**.

Jika **orang yang tidak berhak bisa melihat data**, maka confidentiality dilanggar.

### Incident 1

**A hacker steals a database containing customer credit card numbers.**

➡️ Data rahasia dicuri.

Jawaban:

```
Confidentiality
```

---

### Incident 2

**An employee accidentally sends a confidential company document to the wrong email address.**

➡️ Informasi rahasia terbaca orang lain.

Jawaban:

```
Confidentiality
```

---

### Incident 3

**An attacker gains access to user passwords stored in a server.**

➡️ Password bocor.

Jawaban:

```
Confidentiality
```

---

# 2️⃣ Integrity (Keutuhan Data)

Integrity berarti **data harus tetap akurat dan tidak boleh diubah tanpa izin**.

Jika **data dimodifikasi**, maka integrity dilanggar.

### Incident 4

**An attacker changes the balance of bank accounts in the database.**

➡️ Data keuangan dimodifikasi.

Jawaban:

```
Integrity
```

---

### Incident 5

**Malware modifies important system configuration files.**

➡️ File sistem diubah malware.

Jawaban:

```
Integrity
```

---

### Incident 6

**A hacker alters the grades stored in a university database.**

➡️ Nilai mahasiswa diubah.

Jawaban:

```
Integrity
```

---

# 3️⃣ Availability (Ketersediaan Sistem)

Availability berarti **sistem harus tersedia ketika pengguna membutuhkannya**.

Jika **sistem tidak bisa diakses**, maka availability dilanggar.

### Incident 7

**A DDoS attack makes a company website unavailable.**

➡️ Website tidak bisa diakses.

Jawaban:

```
Availability
```

---

### Incident 8

**Ransomware encrypts files so employees cannot access them.**

➡️ File tidak bisa digunakan.

Jawaban:

```
Availability
```

---

### Incident 9

**A power outage shuts down the company's servers.**

➡️ Server mati.

Jawaban:

```
Availability
```

---

# Ringkasan Pola Jawaban (Trik Cepat)

Gunakan cara berpikir ini saat menjawab soal.

| Pertanyaan                                    | Jawaban         |
| --------------------------------------------- | --------------- |
| Apakah data **bocor atau dibaca orang lain?** | Confidentiality |
| Apakah data **diubah atau dimanipulasi?**     | Integrity       |
| Apakah sistem **tidak bisa digunakan?**       | Availability    |

---

# Cara berpikir seperti Security Analyst

Security analyst biasanya menganalisis incident seperti ini:

```
Did someone see data they shouldn't?
→ Confidentiality

Was the data changed?
→ Integrity

Was the system unavailable?
→ Availability
```
Berikut **5 contoh serangan cyber nyata di dunia** yang sering digunakan sebagai contoh untuk menjelaskan **CIA Triad** dalam kelas cybersecurity. Saya jelaskan **kejadian, dampak, dan bagian CIA yang dilanggar**.

---

# 1️⃣ Kebocoran Data Facebook (2019–2021)

Perusahaan: Meta Platforms

### Apa yang terjadi

Sekitar **533 juta data pengguna** dari **Facebook** bocor di internet.

Data yang bocor meliputi:

* nomor telepon
* nama
* lokasi
* tanggal lahir
* email

Data ini kemudian **diposting gratis di forum hacker**.

### Dampak

Hacker bisa menggunakan data tersebut untuk:

* phishing
* scam
* identity theft

### CIA yang dilanggar

```
Confidentiality
```

Karena **data pribadi pengguna terekspos ke publik**.

---

# 2️⃣ Serangan Ransomware Rumah Sakit Inggris (2017)

Serangan ini terjadi melalui malware **WannaCry**.

Target utama:

National Health Service

### Apa yang terjadi

Ransomware mengenkripsi file rumah sakit sehingga:

* dokter tidak bisa mengakses data pasien
* sistem medis berhenti
* operasi harus ditunda

### Dampak

* ribuan appointment dibatalkan
* sistem kesehatan lumpuh

### CIA yang dilanggar

```
Availability
```

Karena **sistem tidak bisa diakses oleh dokter dan staf**.

---

# 3️⃣ Serangan SolarWinds Supply Chain (2020)

Perusahaan: SolarWinds

### Apa yang terjadi

Hacker menyusup ke proses update software SolarWinds.

Update yang terinfeksi malware kemudian diinstall oleh:

* perusahaan besar
* pemerintah
* organisasi global

### Dampak

Penyerang bisa:

* mengakses jaringan internal
* memata-matai organisasi

### CIA yang dilanggar

```
Confidentiality
```

Karena hacker **mengakses informasi rahasia organisasi**.

---

# 4️⃣ Serangan Sony Pictures (2014)

Perusahaan: Sony Pictures

### Apa yang terjadi

Hacker berhasil masuk ke jaringan Sony dan:

* mencuri email internal
* mencuri film yang belum dirilis
* merusak data perusahaan

### Dampak

* data sensitif karyawan bocor
* reputasi perusahaan rusak

### CIA yang dilanggar

```
Integrity
```

Karena **data perusahaan dimodifikasi dan dirusak**.

---

# 5️⃣ Serangan DDoS Dyn DNS (2016)

Target: Dyn

Serangan menggunakan botnet malware **Mirai**.

### Apa yang terjadi

Jutaan perangkat IoT (kamera CCTV, router, dll) digunakan untuk melakukan **DDoS attack**.

Akibatnya banyak website besar tidak bisa diakses, termasuk:

* Twitter
* Netflix
* Reddit

### Dampak

* website besar down selama beberapa jam

### CIA yang dilanggar

```
Availability
```

Karena **layanan tidak tersedia bagi pengguna**.

---

# Ringkasan 5 Kasus

| Serangan            | CIA yang dilanggar |
| ------------------- | ------------------ |
| Facebook data leak  | Confidentiality    |
| WannaCry ransomware | Availability       |
| SolarWinds attack   | Confidentiality    |
| Sony Pictures hack  | Integrity          |
| Dyn DNS DDoS        | Availability       |

---

# Cara berpikir profesional cybersecurity

Security analyst biasanya selalu bertanya:

```
Apakah data bocor?
→ Confidentiality

Apakah data diubah?
→ Integrity

Apakah sistem tidak bisa digunakan?
→ Availability
```

Inilah cara **CIA Triad digunakan dalam incident response**.

---
