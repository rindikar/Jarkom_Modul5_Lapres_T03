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
