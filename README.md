# JARKOM-MODUL-5-D18-2023
- Abhinaya Radiansyah Listiyanto (5025211173) 
- Fauzi Rizki Pratama (5025211220)

# Soal 1
## Pertanyaan:
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

## Jawaban:
```
iptables -t nat -A POSTROUTING -s 192.200.0.0/16 -o eth0 -j SNAT --to-s 192.168.122.5
```
tujuan dari perintah ini adalah melakukan SNAT pada paket yang berasal dari jaringan dengan rentang IP 192.200.0.0/16, yang menuju keluar melalui antarmuka eth0, dengan mengubah alamat sumber mereka menjadi 192.168.122.5.
![image](https://github.com/Abhinaya173/JARKOM-MODUL-5-D18-2023/assets/114990549/3ebbd009-d9a5-4de2-a4a0-59feb9274883)
