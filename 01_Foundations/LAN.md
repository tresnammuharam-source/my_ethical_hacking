# apa itu LAN?
LAN singkatan dari Local Area Network, yang artinya jaringan dalam skala kecil/terbatas yang menghubungkan beberapa device

bayangkan lagi saat kamu sebagai siswa di suatu kelas yang mempunyai idetitas yaitu IP address dan mempunyai alat tulis buku dan lainnya yg masing-masing memiliki MAC address (Media Access Control).
kamu duduk di meja kelas depan bersama teman kamu yang mempunyai IP Address juga dan mempunyai MAC Address juga. kamu saling berkomunikasi di meja kamu, maka satu meja tersebut adalah berjaringan LAN (Locak Area Network).
di dalam kelas tersebut ada berbagai meja dan mereka saling berkomunikasi, dan komunikasi juga antar meja. pada saat siswa tersebut berkomunikasi dibatasi dengan tembok yg di sebut lingkungan kelas maka komunikasi tersebut disebut LAN.
kenapa LAN karena jika di kelas tersebut setiap meja adalah kelompok belajar atau kelompokl diskusi, mereka semua dengan IP address dan MAC address mereka masing=masing.
maka masing2 harus melapor ke ketua kelompok disebut switch dan ketua kelompok melapor ke guru, dan guru di kelas tersebut disebut dengan router yang mengatur jaringan komunikasi antar private network (routing)

ketua kelompok itu fungsinya menghubungkan komunikasi antara semua anggotanya di dalam kelompok. itulah switch yang berfungsi menghubungkan device dalam satu jaringan yang mainnya di MAC address

sedangkan guru adalah yang mengatur alurnya diskusi besar dalam kelas. yang bisa menghubungan pertanyaan dari kelompok 1 ke kelompok 3 dan lainnya. sama seperti router yang fungsinya menghubungkan antar jaringan yang berbeda.
mainnya di IP address. sesuai permintaan dan pertanyaan dari IP address.

# Dalam Cyber Security
## Kalau Serangan di LAN
Switch relevan:
- ARP spoofing
- MAC flooding
- VLAN hopping

## Kalau Serangan antar jaringan
Router relevan:
- IP spoofing
- Routing attack
- MITM via gateway

## Perbedaan Singkat Super Cepat
Switch:
- Dalam satu jaringan
- Pakai MAC
- Layer 2

Router:
- Antar jaringan
- Pakai IP
- Layer 3

# VLAN (Virtual Local Area Network)

VLAN berfungsi untuk membagi jaringan dalam subjaringan2 tertentu. ini mainya di tingkat switch. Membagi satu jaringan fisik menjadi beberapa jaringan logis (virtual).
seperti halnya di sekolah tadi, siswa di kelas yang sedang diskusi kelompok, kelompok tersebut terdiri dari beberapa orang, VLAN itu didalam kelompoknya yang saling komunikasi, dan bisa juga si guru hanya menentukan diskusi antara kelompok 1 dan kelompok 3 maka proses komunikasi tersebut VLAN antara kelompok 1 dan kelompok 3 yang diatur oleh guru sebagai router dan sekaligus yang menentukan VLAN.

VLAN ini untuk menurunkan tingkat resiko, karena mereka berkumunikasi dalam VLAN yang berbeda meski dalan LAN yang sama.
kenapa VLAN penting?
Karena:
✔ Membatasi lateral movement
✔ Membatasi broadcast attack
✔ Memisahkan network sensitif

Kalau hacker masuk ke VLAN 10,

dia tidak langsung bisa akses VLAN 20.

Kecuali ada misconfiguration.

# Subnetting
Subnetting konsepnya hampir sama dengan VLAN namun subnetting membagi2 jaringan dalam tingkat IP.
Tujuannya:
- Mengatur IP
- Mengurangi broadcast
- Membantu routing

Bayangkan gedung kantor:
- VLAN = Membagi lantai (HR di lantai 1, IT di lantai 2)
- Subnet = Memberi nomor ruangan di tiap lantai

Subnets use IP addresses in three different ways:
- Identify the network address
- Identify the host address
- Identify the default gateway

# ARP (Address Resolution Protocol)

ARP berfungsi untuk Menerjemahkan IP Address menjadi MAC Address. tanpa ada ARP maka IP tidak bisa dikirim di LAN.

- Switch bekerja dengan MAC
- Manusia & aplikasi bekerja dengan IP

misal ada pengantar paket (ketua kelompok) di kirim ke kelas paket tersebut (ARP) harus di kirim ke yg namanya si Udin (IP address) tapi buku catetannya ga atau apet itu harus buku catetan Biologi atau fisika dll (MAC address).
si orang yg pegang paket di kelas melakukan pengumuman / broadcast ke semua.

wooooyyyy siapa yang IP address 192.168.1.7 maka, dari sekian siswa tersebut akan mengangkat tangan karean dia IP addressnya. "itu saya,,, MAC address saya XXXX. maka dikrimkan paket itu ke IP addressnya.

si ketua kelompok adalah switch. maka switch itu mengirim pake berdasarkan MAC address.

masalahnya ARP tidak punya authentication. siapa pun akan bilang "woy itu punya saya..." maka disebut APR Spoofing (berpura2 jadi device yang dituju)

# DHCP (dynamic Host Control Protocol)

- DHCP adalah sistem otomatis yang memberikan IP address ke perangkat.
- Tanpa DHCP, setiap perangkat harus diatur IP-nya satu per satu secara manual.
- Proses DHCP (Disebut DORA)

Bayangkan di kantor ada 200 komputer.
Kalau tidak ada DHCP → admin harus isi IP satu-satu. Ribet banget.

DHCP Discover >>> DHCP Discover >>> DHCP Request >>> DHCP ACK (Acknowledgment)

Alamat IP bisa diberikan dengan dua cara:
Secara manual (diisi langsung pada perangkat), atau Secara otomatis dan paling umum menggunakan server DHCP (Dynamic Host Configuration Protocol). Ketika sebuah perangkat terhubung ke jaringan dan belum memiliki alamat IP yang ditentukan secara manual, perangkat tersebut akan mengirimkan permintaan (DHCP Discover) untuk mencari apakah ada server DHCP di jaringan. Server DHCP kemudian membalas dengan menawarkan alamat IP yang bisa digunakan oleh perangkat tersebut (DHCP Offer). Perangkat kemudian mengirimkan balasan bahwa ia ingin menggunakan alamat IP yang ditawarkan tersebut (DHCP Request). Terakhir, server DHCP mengirimkan balasan bahwa proses telah selesai dan perangkat boleh mulai menggunakan alamat IP tersebut (DHCP ACK).

1️⃣ DHCP Discover

Perangkat baru masuk jaringan.

Dia belum punya IP.

Maka dia broadcast ke seluruh jaringan:

"Apakah ada DHCP server di sini?"

Karena belum punya IP, dia pakai alamat khusus 0.0.0.0 dan broadcast ke 255.255.255.255.

2️⃣ DHCP Offer

Server DHCP menjawab:

"Saya ada. Kamu bisa pakai IP ini: 192.168.1.25"

Biasanya juga dikirim:

Subnet mask

Default gateway

DNS server

3️⃣ DHCP Request

Perangkat bilang:

"Oke, saya mau pakai IP itu."

4️⃣ DHCP ACK (Acknowledgment)

Server menjawab:

"Disetujui. Sekarang kamu resmi pakai IP itu."

Selesai ✅
Perangkat sekarang punya IP dan bisa komunikasi.

