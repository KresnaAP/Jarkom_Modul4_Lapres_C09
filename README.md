# Modul4_C09
Kelompok C09
- 05111840000028  M. Frediansyah Sinaga
- 05111840000072  Kresna Adhi Pramana

Praktikum Modul 4 berupa *Subnetting dan Routing*.


## Soal
![Soal](img/soal.png)

Catatan
1. Deadline hari Rabu, 9 Desember 2020 pukul 22.00
2. Soal shift dikerjakan pada Cisco Packet Tracer dan UML menggunakan metode
    perhitungan CLASSLESS yang berbeda .
    Keterangan: Bila di CPT menggunakan VLSM , maka di UML menggunakan CIDR
    atau Sebaliknya
3. Jika tidak ada pemberitahuan revisi soal dari asisten, berarti semua soal BERSIFAT BENAR
    dan DAPAT DIKERJAKAN .
4. CLOUD diberikan IP TUNTAP.
5. Server diberikan IP DMZ.
6. Berikan memori sebesar 64MB pada setiap UML.
7. Pembagian IP dan routing harus SE-EFISIEN MUNGKIN.
8. Pastikan semua UML dapat melakukan ping ke its.ac.id

Hal yang perlu diperhatikan
1. Hasil perhitungan subnetting dan pohon pembagian IP serta file .pkt dikirim ke email
    asisten penguji (Daftar asisten penguji keluar hari Rabu, 9 Desember 2020 pukul 12.00
    WIB)
2. File yang didemokan adalah file .pkt yang telah dikirim ke asisten.
3. Maksimal menghubungi asisten untuk demo hari Kamis, 10 Desember 2020 pukul
    20.00 WIB
4. Pengurangan nilai akan dilakukan ketika:
    1. Melanggar salah satu dari tulisan diatas.
    2. Hasil perhitungan untuk VLSM / CIDR, berbeda dengan di CPT / UML
    3. Pembagian IP kurang efisien
    4. Routing kurang efisien
    5. Tidak bisa menjelaskan cara perhitungan VLSM dan CIDR
    
    
## Jawaban

### VLSM - CPT
1. Membagi jaringan pada soal menjadi 13 subnet.
    ![Vlsm1](img/vlsm1.png)
    
   Pembagian IP Server menggunakan NID DMZ.
   
    ![Server](img/server.png)
    
2.  Menentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan melakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan.
    | Subnet  | Jumlah IP | Netmask   |
    | ------- | --------- | --------- |
    | A1      | 1001      | /22       |
    | A2      | 2         | /30       |
    | A3      | 2         | /30       |
    | A4      | 101       | /25       |
    | A5      | 2021      | /21       |
    | A6      | 701       | /22       |
    | A7      | 2         | /30       |
    | A8      | 502       | /23       |
    | A9      | 13        | /28       |
    | A10     | 521       | /22       |
    | A11     | 2         | /30       |
    | A12     | 252       | /24       |
    | A13     | 721       | /22       |
    | Total   | 5841      | /19       |
    
    Berdasarkan total IP dan netmask yang dibutuhkan, maka kita dapat menggunakan netmask /19 untuk memberikan pengalamatan IP pada subnet.
3. Subnetting dengan menggunakan pohon untuk pembagian IP sesuai dengan kebutuhan masing-masing subnet yang ada.
    ![Vlsm2](img/vlsm2.png)
4. Dari pohon tersebut akan mendapat pembagian IP sebagai berikut.
    
    ![Vlsm3](img/vlsm3.png)
5. Interface pada CPT  
   Setelah mendapat IP-nya dari pembagian IP diatas, isi Interface pada masing-masing device. Setelah diisi, berikut illustrasinya :  
   ![ifaceCPT](img/ifaceCPT.png)

6. Routing
    1. SURABAYA
        ```
        192.168.2.0/23 via 192.168.0.10
        192.168.0.16/28 via 192.168.0.10
        192.168.12.0/22 via 192.168.0.10
        192.168.0.12/30 via 192.168.0.10
        192.168.1.0/24 via 192.168.0.10
        192.168.16.0/22 via 192.168.0.10
        192.168.8.0/22 via 192.168.0.2
        192.168.0.4/30 via 192.168.0.2
        192.168.24.0/21 via 192.168.0.2
        192.168.0.128/25 via 192.168.0.2
        10.151.77.84/30 via 192.168.0.10
        ```
    2. PASURUAN
        ```
        0.0.0.0 via 192.168.0.1
        192.168.0.128/25 via 192.168.0.6
        192.168.24.0/21 via 192.168.0.6
        ```
    3. PROBOLINGGO
        ```
        0.0.0.0/0 via 192.168.0.5
        ```
    4. BATU
        ```
        0.0.0.0/0 via 192.168.0.9
        192.168.0.16/28 via 192.168.2.3
        10.151.77.84/30 via 192.168.0.14
        192.168.1.0/24 via 192.168.0.14
        192.168.16.0/22 via 192.168.0.14
        ```
    5. MADIUN
        ```
        0.0.0.0/0 via 192.168.2.1
        ```
    6. KEDIRI
        ```
        192.168.16.0/22 via 192.168.1.3
        0.0.0.0/0 via 192.168.0.13
        ```
    7. BLITAR
        ```
        0.0.0.0/0 via 192.168.1.1
        ```
        
7. Untuk file .pkt dapat diakses [disini](Modul4_KelompokC09_Jarkom2020_VLSM.pkt).

### CIDR - UML
1. Membagi jaringan pada soal menjadi seperti gambar berikut.
    ![Cidr1](img/cidr1.png)  
   
   Pembagian IP Server menggunakan NID DMZ.
   
    ![Server](img/server.png)
2. Pembagian IP dengan pohon berdasarkan penggabungan subnet yang telah dilakukan.
    ![Cidr2](img/cidr2.png)  
3. Berdasarkan perhitungan, maka didapatkan pembagian IP sebagai berikut.

    ![Cidr3](img/cidr3.png)  
4. Membuat `topologi.sh` yang isinya :
   ```
   # Switch
    uml_switch -unix switch0 > /dev/null < /dev/null &
    uml_switch -unix switch1 > /dev/null < /dev/null & 
    uml_switch -unix switch2 > /dev/null < /dev/null & 
    uml_switch -unix switch3 > /dev/null < /dev/null & 
    uml_switch -unix switch4 > /dev/null < /dev/null & 
    uml_switch -unix switch13 > /dev/null < /dev/null & 
    uml_switch -unix switch15 > /dev/null < /dev/null & 
    uml_switch -unix switch16 > /dev/null < /dev/null & 
    uml_switch -unix switch17 > /dev/null < /dev/null & 
    uml_switch -unix switch18 > /dev/null < /dev/null & 
    uml_switch -unix switch19 > /dev/null < /dev/null & 
    uml_switch -unix switch20 > /dev/null < /dev/null & 
    uml_switch -unix switch21 > /dev/null < /dev/null & 
    uml_switch -unix switch22 > /dev/null < /dev/null & 
    uml_switch -unix switch25 > /dev/null < /dev/null & 

    # Router
    xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.40 eth1=daemon,,,switch1 eth2=daemon,,,switch0 eth3=daemon,,,switch2  eth4=daemon,,,switch13 mem=64M &
    xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch0 eth1=daemon,,,switch4 eth2=daemon,,,switch19 mem=64M &
    xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch4 eth1=daemon,,,switch15 eth2=daemon,,,switch16 mem=64M &
    xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch2 eth1=daemon,,,switch3 eth2=daemon,,,switch21 eth3=daemon,,,switch22 mem=64M &
    xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22 eth1=daemon,,,switch25 mem=64M &
    xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch3 eth1=daemon,,,switch17 eth2=daemon,,,switch18 mem=64M &
    xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17 eth1=daemon,,,switch20 mem=64M &

    # Server
    xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &
    xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &

    # Klien 
    xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
    xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
    xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
    xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
    xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
    xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
    xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
    xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
    xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &
    xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &
   ```
   
   Illustrasi Topologi :  
   ![topologi](img/topologi.jpg)

5. Mengisi interface pada masing-masing UML dengan menggunakan perintah ``` nano /etc/network/interfaces ```
    1. SURABAYA (Router)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 10.151.76.42
    netmask 255.255.255.252
    gateway 10.151.76.41

    auto eth1
    iface eth1 inet static
    address 192.168.64.1
    netmask 255.255.252.0

    auto eth2
    iface eth2 inet static
    address 192.168.192.1
    netmask 255.255.255.252

    auto eth3
    iface eth2 inet static
    address 192.168.32.1
    netmask 255.255.255.252

    auto eth4
    iface eth2 inet static
    address 10.151.77.81
    netmask 255.255.255.252
    ```
    2. BATU (Router)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.32.2
    netmask 255.255.255.252

    auto eth1
    iface eth1 inet static
    address 192.168.8.1
    netmask 255.255.255.252

    auto eth2
    iface eth2 inet static
    address 192.168.20.1
    netmask 255.255.252.0

    auto eth3
    iface eth3 inet static
    address 192.168.16.1
    netmask 255.255.254.0
    ```
    3. KEDIRI (Router)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.8.2
    netmask 255.255.255.252

    auto eth1
    iface eth1 inet static
    address 192.168.4.1
    netmask 255.255.255.0

    auto eth2
    iface eth2 inet static
    address 10.151.77.85
    netmask 255.255.255.252
    ```
    4. PASURUAN (Router)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.192.2
    netmask 255.255.255.252

    auto eth1
    iface eth1 inet static
    address 192.168.144.1
    netmask 255.255.255.252

    auto eth2
    iface eth2 inet static
    address 192.168.160.1
    netmask 255.255.252.0
    ```
    5. PROBOLINGGO (Router)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.144.2
    netmask 255.255.255.252

    auto eth1
    iface eth1 inet static
    address 192.168.136.1
    netmask 255.255.255.128

    auto eth2
    iface eth2 inet static
    address 192.168.128.1
    netmask 255.255.248.0
    ```
    6. MADIUN (Router)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.16.3
    netmask 255.255.254.0

    auto eth1
    iface eth1 inet static
    address 192.168.18.1
    netmask 255.255.255.240
    ```
    7. BLITAR (Router)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.4.3
    netmask 255.255.255.0

    auto eth1
    iface eth1 inet static
    address 192.168.0.1
    netmask 255.255.252.0
    ```
    8. MALANG (Server)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 10.151.77.86
    netmask 255.255.255.252
    gateway 10.151.77.85
    ```
    9. MOJOKERTO (Server)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 10.151.77.82
    netmask 255.255.255.252
    gateway 10.151.77.81
    ```
    10. BANYUWANGI (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.128.3
    netmask 255.255.248.0
    gateway 192.168.128.1
    ```
    11. BOJONEGORO (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.18.2
    netmask 255.255.255.240
    gateway 192.168.18.1
    ```
    12. BONDOWOSO (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.136.2
    netmask 255.255.255.128
    gateway 192.168.136.1
    ```
    13. JEMBER (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.128.2
    netmask 255.255.248.0
    gateway 192.168.128.1
    ```
    14. JOMBANG (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.16.2
    netmask 255.255.254.0
    gateway 192.168.16.1
    ```
    15. LUMAJANG (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.4.2
    netmask 255.255.255.0
    gateway 192.168.4.1
    ```
    16. NGANJUK (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.20.2
    netmask 255.255.252.0
    gateway 192.168.20.1
    ```
    17. SAMPANG (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.64.2
    netmask 255.255.252.0
    gateway 192.168.64.1
    ```
    18. SIDOARJO (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.160.2
    netmask 255.255.252.0
    gateway 192.168.160.1
    ```
    19. TULUNGAGUNG (Klien)
    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.168.0.2
    netmask 255.255.252.0
    gateway 192.168.0.1
    ```
    
6. Interface pada UML
   
   Berikut adalah ilustrasi setelah kita menambahkan interface pada masing-masing UML
   ![ifaceUML](img/ifaceUML.png) 

7. Routing

   Pertama, pada UML SURABAYA kita harus menjalankan perintah ``` iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16 ```  
   Lalu, berikut ini adalah routing pada masing-masing router :
   * SURABAYA : D1,D2, dan Server Malang
   * BATU     : B1,A9, dan Server Malang
   * KEDIRI   : A13
   * PASURUAN : B2 
   
   Sisanya bisa memakai 0.0.0.0.
   
    1. SURABAYA
        ```
        route add -net 192.168.128.0 netmask 255.255.192.0 gw 192.168.192.2
        route add -net 192.168.0.0 netmask 255.255.224.0 gw 192.168.32.2
        route add -net 10.151.77.84 netmask 255.255.255.252 gw 192.168.32.2
        ```
    2. BATU 
        ```
        route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.32.1
        route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.8.2
        route add -net 192.168.18.0 netmask 255.255.255.240 gw 192.168.16.3
        route add -net 10.151.77.84 netmask 255.255.255.252 gw 192.168.8.2
        ```
    3. KEDIRI 
        ```
        route add -net 192.168.0.0 netmask 255.255.252.0 gw 192.168.4.3
        route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.8.1
        ```
    4. PASURUAN 
        ```
        route add -net 192.168.128.0 netmask 255.255.240.0 gw 192.168.144.2
        route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.192.1
        ```
    5. PROBOLINGGO
        ```
        route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.144.1
        ```
    6. MADIUN
        ```
        route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.16.1
        ```
    7. BLITAR
        ```
        route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.4.1
        ```
