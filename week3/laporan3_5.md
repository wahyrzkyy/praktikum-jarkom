# Laporan praktikum jarkom week3 (3.5 HTML Documents dengan Embedded Objects )

## Tujuan Praktikum
Supaya mahasiswa dapat menginvestigasi cara kerja protokol HTTP menggunakan Wireshark.

## Langkah Percobaan
1. Buka software wireshark anda
2. Lalu klik bagian wifi (jika menggunakan wifi)
3. Setelah itu buka browser anda terlebih dahulu dan pastikan cache browser Anda dibersihkan (jika belum, hapus terlebih dahulu cache dan history browser anda)
4. Jika sudah, mulai pengambilan paket Wireshark, dengan mengklik "start capturing packet"
5. Saat Wireshark sedang berjalan, masukkan URL: http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html dan tampilkan halaman tersebut di browser anda. 
6. Lalu ketik username dan password yang diminta ke dalam kotak pop up (Username adalah "wireshark-students", dan password adalah "network" (tanpa tanda kutip))
7. Setelah itu balik lagi ke wireshark dan stop capturing packets atau pencet logo stop yang berwarna merah
8. Masukkan atau filter bagian protocol http saja di display-filter-specification window (textfield filter paket di bagian atas daftar paket), sehingga hanya pesan HTTP yang diambil yang akan ditampilkan nanti di jendela daftar paket.
9. username (wireshark-students) dan password (network) yang telah masukkan sebelumnya, dikodekan dalam string karakter (d2lyZXNoYXJrLXN0dWRlbnRzOm5ldHdvcms=)
10. Untuk mengetahui string "Authorization: Basic d2lyZXNoYXJrLXN0dWRlbnRzOm5ldHdvcms=", Anda harus memeriksa paket HTTP GET yang dikirimkan klien setelah menerima pesan "401 Unauthorized" dengan cara Klik Paket Tersebut: Klik kiri pada baris paket No. 735 (setiap device mungkin berbeda).
11. Lalu periksa Di jendela bagian tengah (Packet Details), cari dan perluas (klik tanda panah >) bagian Hypertext Transfer Protocol (HTTP).
12. Cari Header Authorization: Di dalam detail HTTP tersebut, cari baris yang bertuliskan "Authorization: Basic ...".
13. Di sana Anda akan melihat string d2lyZXNoYXJrLXN0dWRlbnRzOm5ldHdvcms=
14. Untuk melihat username dan password yang telah dienkripsi dalam format Base64, buka http://www.motobit.com/util/base64-decoder-encoder.asp dan masukkan string yang disandikan base64 d2lyZXNoYXJrLXN0dWRlbnRz dan decode.

## Lampiran
![Hasil Percobaan](../assets/image/mod3_5.png)
![Hasil Percobaan](../assets/image/mod3_5.1.png)