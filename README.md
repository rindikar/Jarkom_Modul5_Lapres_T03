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




