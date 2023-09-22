# Jarkom-Modul-Y-E09-2023

|Nama Anggota |NRP |
|---|---|
|Thoriq Fatihassalam | 5025201254 |
|Farah Dhia Fadhila | 5025211030 |

## Soal 1
User melakukan berbagai aktivitas dengan menggunakan protokol FTP. </br>
nc 10.21.78.111 12345

a. Berapakah sequence number (raw) pada packet yang menunjukkan aktivitas tersebut?</br>
b. Berapakah acknowledge number (raw) pada packet yang menunjukkan aktivitas tersebut?</br>
c. Berapakah sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut?</br>
d. Berapakah acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut?</br>
![ss soal 1](img/ss-soal-1.png)

### Jawaban
Pada protokol FTP kita mengenal "STOR" untuk mengupload file ke FTP server. Oleh karena itu saya memfilter packet yang mengandung string "STOR" dengan 
`tcp contains "STOR"`.</br>
![ss STOR](img/ss-stor.png)

Jika kita klik TCP, akan terlihat sequence number (raw) dan acknowledge number (raw) pada aktivitas tersebut. Lalu akan terlihat juga bahwa file yang diupload bernama **c75-GrabThePhisher.zip**

Lalu kita filter packet yang memiliki string "c75-GrabThePhisher.zip" untuk melihat aktivitas pada packet tersebut. </br>
![ss file STOR](img/ss-file-stor.png)

Sama seperti sebelumnya, ketika kita menklik TCP, akan terlihat sequence number (raw) dan acknowlegde number (raw) pada aktivitas tersebut.

## Soal 2
Sebutkan web server yang digunakan pada portal praktikum Jaringan Komputer! </br>
nc 10.21.78.111 13579 </br>
![ss nomor 2](img/ss-nomor-2.png)

## Jawaban
Seperti yang kita tau bahwa pengerjaan praktikum Jaringan Komputer ini dilakukan pada platform `link http://10.21.78.111:8000/`. Saya memfilter aktivitas yang source ip 10.21.78.111:8000 dnegan `ip.src == 10.21.78.111:8000` </br>
![ss ip nomor 2](img/ss-ip-nomor-2.png)

Pada packet tersebut akan terlihat bahwa server yang digunakan adalah gunicorn. Oleh karena itu jawabannya adalah `gunicorn`

## Soal 3
Dapin sedang belajar analisis jaringan. Bantulah Dapin untuk mengerjakan soal berikut: </br>
nc 10.21.78.111 13590 

a. Berapa banyak paket yang tercapture dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702?</br>
b. Protokol layer transport apa yang digunakan? </br>
![ss nomor 3](img/ss-nomor-3.png)

### Jawaban
Untuk soal 3a, saya memfilter IP address 239.255.255.250 dengan port 3702 dengan `ip.addr == 239.255.255.250 && udp.port == 3702`. Lalu kita menseleksi semua aktivitas yang telah terfilter, maka akan terlihat jumlah dari packet yang ada dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702.</br>
![ss 3a](img/ss-3a.png)

Kita juga bisa mengetahui protokol yang dipakai pada header protocol. Protokol yang digunakan adalah protokol `UDP`

## Soal 4
Berapa nilai checksum yang didapat dari header pada paket nomor 130?</br>
nc 10.21.78.111 13591 </br>
![ss nomor 4](img/ss-nomor-4.png)

### Jawaban
Pertama kita perlu memfilter paket dengan nomor 130 dengan `frame.number == 130` </br>
![ss filter 130](img/ss-filter-130.png)

Kita bisa bahwa checksum-nya adalah `0x18e5`

## Soal 5
Elshe menemukan suatu file packet capture yang menarik. Bantulah elshe untuk menganalisis file packet capture tersebut.

### Jawaban
Pertama kita perlu mendownload file soal5.pcap dan zippppfileee.zip lalu menuju file `connect.txt` pada folder s3crett. File txt tersebut harus dibuka dengan password yang perlu kita cari di file pcap. Lalu pada file pcap tersebut saya memfilter packet yang mengandung string "pass" dengan `tcp contains "pass"` </br>
![soal5 filter](img/soal5-filter.png)

Kita perlu mem-follow TCP Stream lalu akan terlihat passwordnya. </br>
![pass](img/pass.png)

Terlihat bahwa password yang diberikan perlu didecode dengan base64 untuk mendapatkan password sebenarnya. Saya menggunakan bantuan web base64decode.org untuk mendecode password tersebut dan didapatkan password sebenarnya. </br>
![decodepass](img/decodepass.png)

Selanjutnya saya masukkan password yang telah didapat untuk membuka file connect.txt dan mendapatkan netcat-nya.</br>
![ncat](img/ncat.png)

![soal5](img/soal5.png)
a. Berapa banyak packet yang berhasil di capture dari file pcap tersebut? </br>
b. Port berapakah pada server yang digunakan untuk service SMTP? </br>
c. Dari semua alamat IP yang tercapture, IP berapakah yang merupakan public IP?

Untuk soal 5a, kita perlu menseleksi semua aktivitas pada file soal5.pcap lalu akan terlihat bahwa total packet ada `60`.</br>
![5a](img/5a.png)

Lalu untuk soal 5b, saya memfilter packet yang menggunakan service SMTP dengan `tcp contains "SMTP"`, maka akan terlihat bahwa port yang digunakan adalah port `25`.</br>
![5b](img/5b.png)

Terakhir, untuk soal 5c alamat IP yang merupakan public IP adalah `74.53.140.153`
## Soal 6
## Soal 7
## Soal 8
## Soal 9
## Soal 10
## Kendala
