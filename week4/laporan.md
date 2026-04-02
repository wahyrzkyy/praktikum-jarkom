# Laporan praktikum jarkom week4/Modul 4 DNS

## Tujuan Praktikum
Supaya mahasiswa dapat menginvestigasi cara kerja DNS menggunakan Wireshark 

## 4.2 NSlookup

### Langkah Percobaan
1. Menjalankan nslookup untuk mendapatkan alamat IP dari server web www.capcom-games.com. Alamat ip nya adalah 18.64.37.44

### Hasil Pengujian
* Tujuan: Mencari alamat IP server web Capcom.
* Hasil: Domain www.capcom-games.com terhubung ke alamat IP 18.64.37.44.
* DNS Resolver: Permintaan diproses melalui gateway lokal 192.168.1.1.
![Hasil Percobaan](../assets/image/week4/gambar1.png)

2. Menjalankan nslookup agar dapat mengetahui server DNS otoritatif untuk universitas Oxford. 

### Hasil Pengujian
Berdasarkan pengujian menggunakan perintah nslookup -type=NS ox.ac.uk, didapatkan informasi sebagai berikut:

* Identifikasi Server Otoritatif: Terdapat 6 server nama (name server) yang bertanggung jawab atas domain University of Oxford, di antaranya adalah auth6.dns.ox.ac.uk, dns0.ox.ac.uk, dan dns2.ox.ac.uk. Keberadaan banyak server ini menunjukkan penerapan redundansi untuk menjaga ketersediaan layanan DNS.
* Alamat IP Server (IPv4): Sistem memberikan informasi tambahan berupa alamat IP fisik dari server tersebut. Contohnya, server dns0.ox.ac.uk memiliki alamat IPv4 129.67.1.190.
* Dukungan Dual-Stack (IPv6): Server auth6.dns.ox.ac.uk sudah mendukung protokol IPv6, yang terlihat dari adanya AAAA record dengan alamat 2a02:2770:11:0:21a:4aff:febe:759b.
* DNS Resolver Lokal: Permintaan diproses melalui gateway lokal dengan alamat IP 192.168.1.1 (Server Unknown).
![Hasil Percobaan](../assets/image/week4/gambar2.png)

3. Menjalankan nslookup untuk mencari tahu informasi mengenai server email dari Yahoo. alamat IP-nya

### Hasil Pengujian
Berdasarkan pengujian, dilakukan perintah nslookup yahoo.com 129.67.1.190. Berikut adalah poin-poin pentingnya:

* Server yang Digunakan: auth0.dns.ox.ac.uk (IP: 129.67.1.190). Server ini adalah Authoritative Name Server untuk wilayah Oxford.
* Masalah: Muncul pesan kesalahan Query refused.
* Penyebab: 1.  Bukan Otoritasnya: Server Oxford hanya bertugas memberikan jawaban untuk domain internal mereka (ox.ac.uk). Karena yahoo.com bukan bagian dari jaringan mereka, server menolak untuk menjawab. Penyebab 2. Rekursi Dimatikan: Server Authoritative biasanya mematikan fitur rekursi (mencari jawaban ke server luar) bagi pengguna umum internet. Hal ini dilakukan sebagai protokol keamanan untuk mencegah penyalahgunaan server DNS dari serangan luar (seperti DNS Amplification Attack).
![Hasil Percobaan](../assets/image/week4/gambar3.png)

## 4.3 Ipconfig

### Langkah Percobaan
1. Pertama ketik ipconfig dan pencet enter, maka akan menampilkan Daftar Adapter Jaringan, IPv4 Address, Subnet Mask, dan Default Gateway
![Hasil Percobaan](../assets/image/week4/gambar4.png)

2. Lalu ketik ipconfig/all maka akan menampilkan Koneksi Internet Utama (Wireless LAN adapter Wi-Fi), Jaringan Virtual (Ethernet adapter Ethernet 2), Informasi Tambahan (Yang Tidak Terkoneksi) dan Identitas Perangkat (Windows IP Configuration)
![Hasil Percobaan](../assets/image/week4/gambar5.png)

3. Ketik ipconfig/displaydns yang digunakan untuk menampilkan isi dari DNS Resolver Cache pada komputer
![Hasil Percobaan](../assets/image/week4/gambar6.png)

4. Terakhir ketik ipconfig/flushdns yang berfungsi untuk menghapus seluruh catatan DNS yang tersimpan dalam cache di komputer
![Hasil Percobaan](../assets/image/week4/gambar7.png)

## 4.4 Tracing DNS dengan Wireshark

### Langkah percobaan

1. Gunakan ipconfig untuk mengosongkan catatan DNS di host
2. Buka browser dan kosongkan cache-nya.
3. Buka Wireshark dan masukkan ip.addr == your_IP_address ke dalam filter. Bagian your_IP_address diisi dengan alamat IP yang didapatkan melalui ipconfig (ip saya: 192.168.1.7)
4. Setelah itu mulai pengambilan paket di Wireshark. 
5. Lalu kunjungi halaman web: http://www.ietf.org
6. Hentikan pengambilan paket.

### Jawab soal

1. Pesan permintaan DNS sudah ditemukan dan pesan tersebut dikirimkan melalui UDP
![Hasil Percobaan](../assets/image/week4/gambar8.png)

2. Port tujuannya adalah 53, sedangkan portsumbernya adalah 52740
![Hasil Percobaan](../assets/image/week4/gambar9.png)

3. Pada pesan permintaan DNS, alamat IP tujuannya adalah 192.168.1.1, alamat IP server DNS lokal saya adalah 192.168.1.7 dan kedua alamat IP tersebut berbeda 
![Hasil Percobaan](../assets/image/week4/gambar10.png)

4. Pesan permintaan DNS nya adalah type A, dan pesan permintaan tersebut tidak ada jawaban atau 0
![Hasil Percobaan](../assets/image/week4/gambar11.png)

5. Pesan balasan DNS yang terdapat didalamnya sebanyak 2 jawaban
![Hasil Percobaan](../assets/image/week4/gambar12.png)

6. alamat IP pada paket tersebut sesuai dengan alamat IP yang tertera pada pesan balasan DNS yaitu 104.16.45.99
![Hasil Percobaan](../assets/image/week4/gambar13.png)

7. host tidak perlu mengirimkan pesan permintaan DNS baru
![Hasil Percobaan](../assets/image/week4/gambar14.png)

### Langkah percobaan 4.4 bagian 2

1. Mulai pengambilan paket. 
2. Ketik perintah nslookup www.mit.edu di cmd/powershell
3. Hentikan pengambilan paket

### Jawab soal bagian 2

1. Port tujuan pada pesan permintaan DNS adalah 53 dan port sumber pada pesan balasan DNS adalah 3742
![Hasil Percobaan](../assets/image/week4/gambar15.png)

2. Ke alamat IP 128.238.29.22 pesan permintaan DNS dikirimkan dan alamat IP tersebut bukan alamat IP server DNS lokal 
![Hasil Percobaan](../assets/image/week4/gambar16.png)

3. Pesan permintaan DNS tersebut bertype A dan tidak mengandung jawaban atau answer
![Hasil Percobaan](../assets/image/week4/gambar17.png)

4. Pada pesan balasan DNS hanya ada 1 jawaban atau answer saja
![Hasil Percobaan](../assets/image/week4/gambar18.png)

### Jawab soal bagian 3

1. Ke alamat IP 192.168.1.1 pesan permintaan DNS dikirimkan dan alamat IP tersebut bukan alamat IP server DNS lokal saya
![Hasil Percobaan](../assets/image/week4/gambar19.png)

2. Pesan permintaan DNS tersebut bertype NS dan tidak mengandung jawaban atau answer
![Hasil Percobaan](../assets/image/week4/gambar20.png)

3. Nama Server (NS) MIT yang diberikan oleh pesan balasan, antara lain:

* asia2.akam.net
* ns1-37.akam.net
* usw2.akam.net
* use2.akam.net
* eur5.akam.net
* ns1-173.akam.net
* asia1.akam.net

dan pesan balasan ini juga memberikan alamat IP untuk server MIT
![Hasil Percobaan](../assets/image/week4/gambar21.png)

### Jawab soal bagian 4

1. Ke alamat IP 192.168.1.1 pesan permintaan DNS dikirimkan dan alamat IP tersebut bukan alamat IP server DNS lokal saya
![Hasil Percobaan](../assets/image/week4/gambar22.png)

2. Pesan permintaan DNS tersebut bertype AAAA dan tidak mengandung jawaban atau answer
![Hasil Percobaan](../assets/image/week4/gambar23.png)

3. Pada pesan balasan DNS hanya ada 2 jawaban atau answer
![Hasil Percobaan](../assets/image/week4/gambar24.png)