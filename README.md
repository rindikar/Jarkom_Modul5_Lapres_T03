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

