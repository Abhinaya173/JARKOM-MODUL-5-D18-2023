# JARKOM-MODUL-5-D18-2023
- Abhinaya Radiansyah Listiyanto (5025211173) 
- Fauzi Rizki Pratama (5025211220)

# Pembagian Subnet
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/5d85abc9-8f5f-4cb2-ade7-09049d86d3f5)

# Tree
<img width="1899" alt="Untitled" src="https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/b5509eea-eb22-41f6-88c0-0bb537e9faec">

# Pembagian IP
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/a8987aad-c13a-4675-b640-d674cf628390)

# Konfigurasi Route
Aura:
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/a1bca767-650b-4a04-91e5-4ad6e770b0a6)

Heiter:
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/f3e4e655-c7df-46e5-b7a5-ccc3aaffd8b9)

Frieren:
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/3b71f202-6a36-400d-b679-68c854c84515)

Himmel:
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/b53fde0e-3fcd-43b1-95ce-be66ee11dedb)

Fern:
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/b67c7470-6225-4bb1-a0bd-7e568f7eabfe)

# Konfigurasi DNS

# Soal 1
## Pertanyaan:
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

## Jawaban:
```
iptables -t nat -A POSTROUTING -s 192.200.0.0/16 -o eth0 -j SNAT --to-s 192.168.122.5
```
tujuan dari perintah ini adalah melakukan SNAT pada paket yang berasal dari jaringan dengan rentang IP 192.200.0.0/16, yang menuju keluar melalui antarmuka eth0, dengan mengubah alamat sumber mereka menjadi 192.168.122.5.
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/3ebbd009-d9a5-4de2-a4a0-59feb9274883)

# Soal 2
## Pertanyaan:
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.
## Jawaban:
```
iptables -F
iptables -A INPUT -p udp -j DROP
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p tcp -j DROP
```
baris 1 berfungsi untuk  menghapus semua rules dari tabel iptables, baris 2 dan 4 mengedrop paket TCP dan UDP, baris 3 ini akan mengizinkan paket TCP yang menuju port 8080 masuk.


# Soal 3
## Pertanyaan:
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.
## Jawaban:
```

```

# Soal 4
## Pertanyaan:
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.
## Jawaban:
Sein & Stark
```
iptables -A INPUT -p tcp --dport 22 -s 192.200.8.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```
baris 1 mengizinkan paket TCP yang menuju ke port 22 dan berasal dari IP GrobeFores untuk melewati chain INPUT
baris 2 semua paket TCP yang menuju ke port 22 akan didrop

# Soal 5
## Pertanyaan:
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.
## Jawaban:
```
# jam kerja (Senin-Jumat pukul 08.00-16.00)
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 08:00 --timestop 16:00 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -j DROP
```
baris 1 aturan yang memungkinkan koneksi SSH hanya pada hari Senin sampai Jumat pada rentang waktu antara pukul 08:00 dan 16:00.
baris 2 aturan yang menolak koneksi SSH di luar jadwal kerja yang telah ditetapkan.

# Soal 6
## Pertanyaan:
Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).
## Jawaban:
```
# jam kerja (Senin-Jumat pukul 08.00-16.00)
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 08:00 --timestop 11:00 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 13:00 --timestop 16:00 -j ACCEPT

# waktu istirahat (Senin-Kamis pukul 12.00-13.00)
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m time --weekdays Mon,Tue,Wed,Thu --timestart 12:00 --timestop 13:00 -j DROP

# waktu Jumatan (Jumat pukul 11.00-13.00)
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m time --weekdays Fri --timestart 11:00 --timestop 13:00 -j DROP
```
untuk no6 ini hampir sama dengan no 5 yang membedakan hanya peletakan jamnya pada time start dan time stop.

# Soal 7
## Pertanyaan:
Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.
## Jawaban:
```

```

# Soal 8
## Pertanyaan:
Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.
## Jawaban:
sein & stark:
```
iptables -A INPUT -p tcp --dport 80 -m time --datestart 2024-02-14T00:00:00 --datestop 2024-03-20T23:59:59 -j DROP
```
melakukan penginputan tanggal mulai 14-02-2024 sampai 20-03-2024

# Soal 9
## Pertanyaan:
Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. 
(clue: test dengan nmap)
## Jawaban:
sein & stark:
```

```

# Soal 10
## Pertanyaan:
Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.
## Jawaban:
```
iptables -A INPUT -j LOG --log-prefix "Dropped: " --log-level 7
```
setiap kali paket di-drop oleh aturan dalam rantai INPUT, pesan log dengan prefix "Dropped: " akan dicatat dalam log sistem.
