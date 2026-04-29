# LOGS

Dalam sebuah incident kita akan mengetahui bahwa incident tersebut dimulai dari alent dan kita akan mengidentivikasi alent tersebut dan mengkatagorikan kedalam true positive dan false positive.

- false positive adalah aktivitas yang tertriger menjadi aktivitas berbahaya padahal itu legal, seperti alent adanya pemindahan data dalam jumlah banyak dalam satu waktu, padahal setelah diinvestigasi bahwa aktivitas tersebut adalah proses backup
- true positive adalah aktivitas yang terjadi memang karena adanya aktivitas berbahaya, seperti pecobaan login berkali2, pengiriamn pishing, pengiriman malware dan lainnya, inilah yg disebut dengan incident.

dari incident tersebut kita kelompokan kedalam category sesuai tingkat keparahannya dan urgensinya (severity) dimana kita harus melakukan tindakan duluan kepada severity yang paling tinggi.

severity :
- low
- medium
- high
- critical

setelah kita mengetahui incidentnya kita harus melakukan tindakan terhadap incident tersebut dan ini dikemas dalam sebauh framework atau panduan yaitu SANS dan NIST.

setalah inciden ditangani kita harus melakukan analisa kenapa kejadian teresebut terjadi dan bagaiman cara menutupnya, agar dikemudian hari tidak terjadi lagi.

dalam hal ini proses identifikasi dan investigasi ini dibantu dengan tools agar pekerjaan kita bisa lebih akurat diantaranya:
- SIEM
- AV (antivirus)
- EDR (Endpoint Detection and Responses)

dalam proses investigasi ini kita melakukan penggalian dari sebuah data yaitu LOGS.

LOGS ini di kemas dalam berbagai LOGS sesuai peruntukannya, seperti:
- Audit Logs
- System Logs
- Network Logs
- System Logs

dari sini kita bisa mengecek terutama dalam network dengan code2 yang harus kita pantau lebih maksimal, yaitu:
<img width="1244" height="585" alt="image" src="https://github.com/user-attachments/assets/cb9988ec-4a52-408e-add6-9b2972c97271" />

dari daftar kode Logs_id diartas kita harus pantau aktivitas terutama pada code 4625 (filed login) dan 4724 (reset password)

