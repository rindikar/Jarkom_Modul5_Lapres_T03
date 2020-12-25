# Lapres Modul 5 Jarkom 2020 - T03
**Oleh:**
- I Made Dindra Setyadharma (05311840000008)
- Rindi Kartika Sari (05311840000013)

![soalShift-5](https://user-images.githubusercontent.com/49342639/103074430-25039900-45fc-11eb-9397-bd2b275280cb.PNG)
Keterangan:
- **SURABAYA** diberikan **IP TUNTAP**
- **MALANG** merupakan **DNS Server** diberikan **IP DMZ**
- **MOJOKERTO** merupakan **DHCP Server** diberikan **IP DMZ**
- **MADIUN** dan **PROBOLINGGO** merupakan **WEB Server**
- **Setiap Server** diberikan memory sebesar **128M**
- **Client dan Router** diberikan memori sebesar **96M**
- Jumlah host pada subnet **SIDOARJO 200 Host**
- Jumlah host pada subnet **GRESIK 210 Host**

## Preface
1. Melakukan pembagian subnet terhadap topologi yang ada
   
   ![subnet-5](https://user-images.githubusercontent.com/49342639/103075251-cc350000-45fd-11eb-9490-7b652539656a.PNG)
   Dari hasil pembagian subnet, kita mendapatkan sejumlah **6 subnet** yang terdiri atas **4 subnet untuk router-router dan router-client _(A1, A2, A3, A4)_**  dan **2 subnet untuk router-server _(A5 dan B1)_**

## Pembagian IP menggunakan metode VLSM
1. Menentukan jumlah alamat IP yang dibutuhkan oleh **5 subnet (A1, A2, A3, A4 dan A5)**, _kecuali B1 karena subnet B1 akan mendapatkan subnet dari IP DMZ_
   
   | Subnet | Jumlah IP | Netmask |
   | :---:  | :---:     | :---:   |
   | A1     | 2         | /30     |
   | A2     | 2         | /30     |
   | A3     | 211       | /24     | 
   | A4     | 201       | /24     |  
   | A5     | 3         | /29     |     
   | **Total**   | **419**   | **/23**     |   

   Namun, netmask **/23** tidak dapat kita gunakan untuk memberikan pengalamatan IP pada 5 subnet karena pohon yang akan dihasilkan oleh netmask **/23** tidak cukup. Sehingga, kita akan menggunakan netmask **/22** untuk memberikan pengalaman IP pada 5 subnet.

2. Subnet besar yang kami bentuk memiliki NID **192.168.1.0** dengan netmask **/22**. Lalu, kita mulai dengan perhitungan pembagian IP dengan bantuan pohon IP
   ![ip-5](https://user-images.githubusercontent.com/49342639/103080599-bbd65280-4608-11eb-8046-b6092190b145.PNG)
   Sehingga, pembagian IP yang memungkinkan untuk topologi yang ada adalah sebagai berikut:
    | Subnet | NID             | Netmask |
   | :---:  | :---:           | :---:   |
   | A1     | 192.168.3.8     | /30     |
   | A2     | 192.168.3.12    | /30     |
   | A3     | 192.168.1.0     | /24     | 
   | A4     | 192.168.2.0     | /24     |  
   | A5     | 192.168.3.0     | /29     |  
   | B1     | 10.151.73.152   | /29     | 
3. Pembuatan jumlah router, switch, server, klien dan banyaknya eth di UML disesuaikan dengan topologi yang diminta.
   Sintaks pembuatan topologi di UML ini berada pada file **topologi.sh**
   ![1  BUAT TOPOLOGI UML](https://user-images.githubusercontent.com/49342639/103081077-c218fe80-4609-11eb-90bb-ea4bf5fef70f.PNG)

   Selain itu, kami juga membuat sintaks untuk mempermudah penutupan UML di file **bye.sh**
   ![2  BUAT BYE TOPOLOGI UML](https://user-images.githubusercontent.com/49342639/103088520-b0415680-461d-11eb-9009-79e0825e8878.PNG)
4. Setting IP untuk setiap UML pada file **/etc/network/interfaces** sesuai dengan pembagian IP pada setiap subnet
   - **SURABAYA (Sebagai Router)**
  
    ![INTERFACES SURABAYA 1_New](https://user-images.githubusercontent.com/49342639/103094926-77ab7800-4631-11eb-8bd2-fbfa6a7c40a2.PNG)
    ![INTERFACES SURABAYA 2_New](https://user-images.githubusercontent.com/49342639/103095015-b2151500-4631-11eb-9ec0-02715b414e4e.PNG)

   - **KEDIRI (Sebagai Router)**
    
    ![INTERFACES KEDIRI 1_New](https://user-images.githubusercontent.com/49342639/103107702-57041200-4673-11eb-891c-87edbee6c369.PNG)
    ![INTERFACES KEDIRI 2_New](https://user-images.githubusercontent.com/49342639/103107703-59ff0280-4673-11eb-8f98-af4631be5030.PNG)

   - **BATU (Sebagai Router)**
    
    ![INTERFACES BATU 1_New](https://user-images.githubusercontent.com/49342639/103107740-c1b54d80-4673-11eb-9f4f-dafe659be1ca.PNG)
    ![INTERFACES BATU 2_New](https://user-images.githubusercontent.com/49342639/103107742-c417a780-4673-11eb-83f0-57461786f8db.PNG)

   _**Note**: untuk Klien **GRESIK** dan **SIDOARJO** diberikan IP Dinamis_
   - **GRESIK (Sebagai Klien)**
    
    ![INTERFACES GRESIK_New](https://user-images.githubusercontent.com/49342639/103107822-967f2e00-4674-11eb-8709-4f9d66fe3bd9.PNG)

   - **SIDOARJO (Sebagai Klien)**
    
    ![INTERFACES SIDOARJO_New](https://user-images.githubusercontent.com/49342639/103107826-a39c1d00-4674-11eb-86ec-e0bc8a69ca76.PNG)

   - **PROBOLINGGO (Sebagai Server)**
    
    ![INTERFACES PROBOLINGGO_New](https://user-images.githubusercontent.com/49342639/103107850-f07ff380-4674-11eb-9e73-53faddeea72a.PNG)

   - **MADIUN (Sebagai Server)**
    
    ![INTERFACES MADIUN_New](https://user-images.githubusercontent.com/49342639/103107853-fbd31f00-4674-11eb-8702-07b6c10b7458.PNG)

   - **MOJOKERTO (Sebagai Server)**
    
    ![INTERFACES MOJOKERTO_New](https://user-images.githubusercontent.com/49342639/103107871-2f15ae00-4675-11eb-93b6-fdb6f3bd6af9.PNG)

   - **MALANG (Sebagai Server)**
    
    ![INTERFACES MALANG_New](https://user-images.githubusercontent.com/49342639/103107875-3a68d980-4675-11eb-90df-839c277c57ca.PNG)

5. Routing pada setiap router dengan menambahkan dua perintah:
   1) ```post-up route add -net <NID> netmask <NETMASK> gw <GATEWAY>``` bertujuan agar  setelah *interfacenya* **nyala**, maka dia akan dapat secara otomatis menambahkan *static routenya*
   2) ```post-down route add -net <NID> netmask <NETMASK> gw <GATEWAY>``` bertujuan agar  setelah *interfacenya* **mati**, maka dia akan dapat secara otomatis menghilangkan *static routenya*
   
   Kedua perintah tersebut ditempatkan di file **/etc/network/interfaces/** dan di setiap barisan terbawah dari _interfaces_ yang menghubungkannya.

   - **SURABAYA (Sebagai Router)**
    
      _**Note**: Server SURABAYA diberikan route ke arah subnet A3, A4, A5 dan B1_
      
      ![ROUTE SURABAYA 1_New](https://user-images.githubusercontent.com/49342639/103107988-0346f800-4676-11eb-90ac-2fb9ffee1ada.PNG)
      ![ROUTE SURABAYA 2_New](https://user-images.githubusercontent.com/49342639/103107989-05a95200-4676-11eb-83be-cddffeb6f80f.PNG)

   - **KEDIRI (Sebagai Router)**
   
     _**Note**: Server KEDIRI diberikan default route_
     
     ![ROUTE KEDIRI 1_New](https://user-images.githubusercontent.com/49342639/103108035-8d8f5c00-4676-11eb-9a1a-989c429e3dd7.PNG)

   - **BATU (Sebagai Server)**
   
      _**Note**: Server KEDIRI diberikan default route_
      
      ![ROUTE BATU 1_New](https://user-images.githubusercontent.com/49342639/103108063-c4657200-4676-11eb-8149-6e91a0b72020.PNG)

6. Agar IP Dinamis yang diberikan kepada klien **GRESIK** dan **SIDOARJO** dapat berjalan, hal ini membutuhkan bantuan dari **MOJOKERTO (DHCP Server)**. Sehingga, kita perlu melakukan _setting_ konfigurasi DHCP Server di MOJOKERTO.
   - Oleh karena itu, hal pertama yang kita lakukan pada server MOJOKERTO adalah menginstall DHCP Server menggunakan _command_ ```apt-get install isc-dhcp-server```
   - Setelah proses penginstallan berhasil, kita mulai untuk melakukan _setting_ interfaces yang akan diberikan layanan DHCP oleh DHCP Server **MOJOKERTO** pada file **/etc/default/isc-dhcp-server**. Interfaces dari server **MOJOKERTO** hanya ada 1 (satu) interfaces yaitu ```eth0```, dimana interfaces ```eth0``` ini terhubung ke router **BATU** maka kita akan memilih interfaces ```eth0``` untuk diberikan layanan DHCP
   
       ![DHCP SERVER MOJOKERTO_New](https://user-images.githubusercontent.com/49342639/103111549-d0eec800-4680-11eb-976e-84e057a31f0c.PNG)
   
   - Agar DHCP Server **MOJOKERTO** dapat berjalan dengan lancar, maka kita perlu untuk melakukan deklarasi subnet yang terkoneksi pada **MOJOKERTO** yakni subnet _B1_, _A4_ dan _A3_ pada file **etc/dhcp/dhcpd.conf***
     - Deklarasi subnet _B1_
     
      _**Note**:Untuk subnet _B1_ ini hanya harus dideklarasikan, tetapi tidak harus memiliki settingan DHCP_
     
      ![DHCPD CONF MOJOKERTO SUBNET eth0 MOJOKERTO](https://user-images.githubusercontent.com/49342639/103111858-e74a5300-4683-11eb-8237-7d54f057e08c.PNG)

      - Deklarasi subnet _A4_
      
       ![DHCPD CONF MOJOKERTO SUBNET A4](https://user-images.githubusercontent.com/49342639/103111981-c46c6e80-4684-11eb-84fd-a7eb694c0aa2.PNG)

       _**Note**_: 
       1. ```range 192.168.2.2 192.168.2.201;```: Subnet _A4_ mendapatkan peminjaman alamat IP dengan _range_ dari **192.168.2.2** (karena dari pembagian IP untuk setiap subnet menunjukkan bahwa subnet _A4_ mendapatkan IP 192.168.2.0) sampai dengan **192.168.2.201** (karena jumlah host di subnet _A4_ berjumlah 201)
       2. ```option routers 192.168.2.1;```: IP gateway dari router menuju klien **SIDOARJO** adalah **192.168.2.1**
       3. ```option broadcast-address 192.168.2.255;```: IP broadcast dari subnet _A4_ adalah **192.168.2.255**
       4. ```option domain-name-servers 10.151.73.155 , 202.46.129.2 , 10.151.36.7;```: DNS yang ingin kita berikan kepada klien dari subnet _A4_ **(SIDOARJO)** yang terdiri dari **IP MOJOKERTO (10.151.73.155), 202.46.129.2 dan 10.151.36.7 secara otomatis
       5. ```default-lease-time 600;```: Lama waktu DHCP server meminjamkan alamat IP kepada klien dari subnet _A4_ **(SIDOARJO)**  adalah 10 menit (600 detik)
       6. ```max-lease-time 7200;```: Waktu maksimal yang di alokasikan untuk peminjaman IP oleh DHCP server ke klien dari subnet _A4_ **(SIDOARJO)**  adalah 120 menit (7200 detik)

      - Deklarasi subnet _A3_
      
       ![DHCPD CONF MOJOKERTO A3](https://user-images.githubusercontent.com/49342639/103112836-4dd26f80-468a-11eb-85c7-a7399d07f469.PNG)

      _**Note**_: 
       1. ```range 192.168.1.2 192.168.1.211;```: Subnet _A3_ mendapatkan peminjaman alamat IP dengan _range_ dari **192.168.1.2** (karena dari pembagian IP untuk setiap subnet menunjukkan bahwa subnet _A3_ mendapatkan IP 192.168.2.0) sampai dengan **192.168.1.211** (karena jumlah host di subnet _A3_ berjumlah 211)
       2. ```option routers 192.168.1.1;```: IP gateway dari router menuju klien **GRESIK** adalah **192.168.1.1**
       3. ```option broadcast-address 192.168.1.255;```: IP broadcast dari subnet _A3_ adalah **192.168.1.255**
       4. ```option domain-name-servers 10.151.73.155 , 202.46.129.2 , 10.151.36.7;```: DNS yang ingin kita berikan kepada klien dari subnet _A3_ **(GRESIK)** yang terdiri dari **IP MOJOKERTO (10.151.73.155), 202.46.129.2 dan 10.151.36.7 secara otomatis
       5. ```default-lease-time 600;```: Lama waktu DHCP server meminjamkan alamat IP kepada klien dari subnet _A3_ **(GRESIK)**  adalah 10 menit (600 detik)
       6. ```max-lease-time 7200;```: Waktu maksimal yang di alokasikan untuk peminjaman IP oleh DHCP server ke klien dari subnet _A3_ **(GRESIK)**  adalah 120 menit (7200 detik)
   
7. Agar DHCP Request dari subnet **SIDOARJO** dan subnet **GRESIK** dapat diteruskan ke DHCP Server **MOJOKERTO**, maka kita memerlukan DHCP Relay di ketiga router yaitu **SURABAYA**, **KEDIRI** dan **BATU**
   - Oleh karena itu, hal pertama yang kita lakukan pada router SURABAYA, KEDIRI dan BATU adalah menginstall DHCP Relay menggunakan _command_ ```apt-get install isc-dhcp-relay```
   - Setelah proses penginstallan berhasil, kita mulai untuk melakukan _setting_ server dan _setting_ interfaces yang membantu DHCP Request dapat diteruskan dengan baik ke DHCP Server pada file **/etc/default/isc-dhcp-relay**
   - **DHCP Relay pada BATU**
   
   ![DHCP RELAY BATU_New](https://user-images.githubusercontent.com/49342639/103114167-3302f980-4690-11eb-9a71-aa922ccedf73.PNG)

   _**Note**_:

   1. ```SERVERS="10.151.73.154"```: Server **MOJOKERTO** diminta oleh DHCP Relay  **BATU** untuk meneruskan DHCP Request, sehingga kita mengisi ```SERVERS=``` ini dengan IP dari DHCP Server **MOJOKERTO** yaitu 10.151.73.154
   2. ```INTERFACES="eth0 eth1 eth2"```: DHCP Relay **BATU** akan meneruskan DHCP Request dari subnet _A3_ (**GRESIK**) dan subnet _A4_ (**SIDOARJO**) dari network interfaces ```eth0 eth1 eth2```

   - **DHCP Relay pada SURABAYA**
   
    ![DHCP RELAY SURABAYA_New](https://user-images.githubusercontent.com/49342639/103118304-e07e0900-46a0-11eb-8e5b-85209708787e.PNG)

    _**Note**_:

    1. ```SERVERS="10.151.73.154"```: Server **MOJOKERTO** diminta oleh DHCP Relay  **SURABAYA** untuk meneruskan DHCP Request, sehingga kita mengisi ```SERVERS=``` ini dengan IP dari DHCP Server **MOJOKERTO** yaitu 10.151.73.154
    2. ```INTERFACES="eth1 eth2"```: DHCP Relay **SURABAYA** akan meneruskan DHCP Request dari subnet _A3_ (**GRESIK**) dari network interfaces ```eth1 eth2```

   - **DHCP Relay pada KEDIRI**
   
    ![DHCP RELAY KEDIRI_New](https://user-images.githubusercontent.com/49342639/103118409-49fe1780-46a1-11eb-8519-ec60e600e359.PNG)

    _**Note**_:

    1. ```SERVERS="10.151.73.154"```: Server **MOJOKERTO** diminta oleh DHCP Relay  **KEDIRI** untuk meneruskan DHCP Request, sehingga kita mengisi ```SERVERS=``` ini dengan IP dari DHCP Server **MOJOKERTO** yaitu 10.151.73.154
    2. ```INTERFACES="eth0 eth2"```: DHCP Relay **KEDIRI** akan meneruskan DHCP Request dari subnet _A3_ (**GRESIK**) dari network interfaces ```eth0 eth2```

## Soal 1
Agar topologi yang kita buat dapat mengakses keluar, kita diminta untuk mengkonfigurasi
**SURABAYA** menggunakan **iptables**, namun Bibah tidak ingin kalian menggunakan
MASQUERADE.

**Solusi**:
Syntax berikut diatur pada router **SURABAYA**:

```iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -j SNAT --to-source 10.151.72.78```

**Penjelasan**:

Kita menggunakan ```-t nat``` NAT Table pada ```-A POSTROUTING``` POSTROUTING chain untuk ```-j SNAT``` mengubah _source address_ yang awalnya berupa _private IPv4 address_ yang memiliki 16-bit blok dari _private IP addresses_ yaitu ```-s 192.168.0.0/16``` **192.168.0.0/16**  menjadi ```--to-source 10.151.72.78``` **IP eth0 SURABAYA** yaitu **10.151.72.78** karena **SURABAYA** adalah satu-satunya router yang terhubung ke cloud melalui **eth0**

## Soal 2
Kita diminta untuk mendrop semua akses SSH dari luar topologi kita pada server yang memiliki IP DMZ (DHCP Server **MOJOKERTO** dan DNS SERVER **MALANG**) pada **SURABAYA** demi menjaga keamanan

**Solusi**:

Syntax berikut diatur pada router **SURABAYA**:

```iptables -A FORWARD -d 10.151.73.152/29 -i eth0 -p tcp -m tcp --dport 22 -j DROP```

**Penjelasan**:

Kita menggunakan ```-A FORWARD``` FORWARD chain untuk menyaring paket dengan ```-p tcp -m tcp``` protokol TCP dari luar topologi menuju ke DHCP Server **MOJOKERTO** dan DNS Server **MALANG** (yang berada di satu subnet yang sama yaitu ```-d 10.151.73.152/29``` **10.151.73.152/29**), dimana akses SSH (yang memiliki ```--dport 22``` port 22) yang masuk ke DHCP Server **MOJOKERTO** dan DNS Server **MALANG** melalui ```-i eth0``` interfaces **eth0** dari  DHCP Server **MOJOKERTO** dan DNS Server **MALANG** agar ```-j DROP``` di DROP

## Soal 3
Karena tim kita maksimal terdiri dari 3 orang, Bibah meminta kita untuk membatasi DHCP Server **MOJOKERTO**
dan DNS server **MALANG** hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan yang berasal dari mana saja menggunakan iptables pada masing masing server, selebihnya akan di DROP

**Solusi**:

Syntax berikut diatur pada DHCP Server **MOJOKERTO** dan DNS Server **MALANG**:

```iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP```

**Penjelasan**:

Kita menggunakan ```-A INPUT ```INPUT chain untuk menyaring paket dengan ```-p icmp``` protokol ICMP yang masuk agar dibatasi ```-m connlimit --connlimit-above 3``` hanya sebatas maksimal 3 koneksi saja ``` --connlimit-mask 0``` darimana saja, sehingga selebihnya akan ```-j DROP``` di DROP

## Soal 4 dan 5
kemudian kita diminta untuk membatasi akses ke MALANG yang berasal dari subnet **SIDOARJO** dan subnet **GRESIK** dengan peraturan sebagai berikut:

4. Akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat.
5. Akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 hingga pukul 07.00 setiap
harinya.

Selain kedua peraturan tersebut, paket akan di REJECT

**Solusi untuk Soal 4**:

Syntax berikut diatur pada server **MALANG**:

```sh
iptables -A INPUT -s 192.168.2.0/24 -m time --weekdays Sat,Sun -j REJECT
iptables -A INPUT -s 192.168.2.0/24 -m time --timestart 00:00 --timestop 06:59 --weekdays Mon,Tue,Wed,Thu,Fri -j REJECT
iptables -A INPUT -s 192.168.2.0/24 -m time --timestart 17:01 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j REJECT
``` 

**Penjelasan**:

Syntax 1: 

- Kita menggunakan ```-A INPUT``` INPUT chain untuk menyaring paket yang masuk dari ```-s 192.168.2.0/24``` subnet **SIDOARJO** ```-m time --weekdays Sat,Sun``` di jam berapapun  pada hari Sabtu dan Minggu agar ```-j REJECT``` ditolak dan mengirimkan _error message_
  
Syntax 2:

- Kita menggunakan ```-A INPUT``` INPUT chain untuk menyaring paket yang masuk dari ```-s 192.168.2.0/24``` subnet **SIDOARJO** ```-m time --timestart 00:00 --timestop 06:59``` di waktu jam 00:00 sampai dengan jam 06:59 ```--weekdays Mon,Tue,Wed,Thu,Fri``` pada hari Senin, Selasa, Rabu, Kamis, Jum'at agar ```-j REJECT``` ditolak dan mengirimkan _error message_

Syntax 3:

- Kita menggunakan ```-A INPUT``` INPUT chain untuk menyaring paket yang masuk dari ```-s 192.168.2.0/24``` subnet **SIDOARJO** ```-m time --timestart 17:01 --timestop 23:59``` di waktu jam 17:01 sampai dengan jam 23:59 ```--weekdays Mon,Tue,Wed,Thu,Fri``` pada hari Senin, Selasa, Rabu, Kamis, Jum'at agar ```-j REJECT``` ditolak dan mengirimkan _error message_

**Solusi untuk Soal 5**:

Syntax berikut diatur pada server **MALANG**:

```sh
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 07:01 --timestop 16:59 -j REJECT
``` 

**Penjelasan**:

Kita menggunakan ```-A INPUT``` INPUT chain untuk menyaring paket yang masuk dari ```-s 192.168.1.0/24``` subnet **GRESIK** ```-m time --timestart 07:01 --timestop 16:59``` di waktu jam 07:01 sampai dengan jam 16:59 pada hari apapun agar ```-j REJECT``` ditolak dan mengirimkan _error message_
