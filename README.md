# Jarkom-Modul-2-ITB06-2022

Repository ini dibuat sebagai laporan resmi untuk pengerjaan [Soal Shift Modul 2](https://docs.google.com/document/d/11Mz2Fd3DKtGkCknHee9VZRdJYvZ3YAMIaifObHEpBFo/edit) dari praktikum Mata Kuliah Komunikasi Data dan Jaringan Komputer.

Repository ini dibuat oleh:  

**Kelompok ITB06**
- Sarah Hanifah Pontoh	5027201006
- Sharira Saniane 	    5027201016
- Naufal Dhiya Ulhaq 	5027201029

## Pembukaan soal 
Twilight (〈黄昏 (たそがれ) 〉, <Tasogare>) adalah seorang mata-mata yang berasal dari negara Westalis. Demi menjaga perdamaian antara Westalis dengan Ostania, Twilight dengan nama samaran Loid Forger (ロイド・フォージャー, Roido Fōjā) di bawah organisasi WISE menjalankan operasinya di negara Ostania dengan cara melakukan spionase, sabotase, penyadapan dan kemungkinan pembunuhan. Berikut adalah peta dari negara Ostania:

![image1.1](image/topologi1.png)

## Soal 1
WISE akan dijadikan sebagai DNS Master, Berlint akan dijadikan DNS Slave, dan Eden akan digunakan sebagai Web Server. Terdapat 2 Client yaitu SSS, dan Garden. Semua node terhubung pada router Ostania, sehingga dapat mengakses internet

### Jawaban Soal 1
Kami membuat topologi telebih dahulu sebagai berikut : 

![image1.2](image/topologi.png)

Langkah berikutnya kami akan melakukan konfigurasi pada setiap node yang ada :

* Ostania sebagai router 
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.217.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.217.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.217.3.1
	netmask 255.255.255.0
```
* SSS
```
auto eth0
iface eth0 inet static
	address 192.217.1.2
	netmask 255.255.255.0
	gateway 192.217.1.1
```
* Garden
```
auto eth0
iface eth0 inet static
	address 192.217.1.3
	netmask 255.255.255.0
	gateway 192.217.1.1
```
* Berlint
```
auto eth0
iface eth0 inet static
	address 192.217.2.2
	netmask 255.255.255.0
	gateway 192.217.2.1
```
* Eden
```
auto eth0
iface eth0 inet static
	address 192.217.2.3
	netmask 255.255.255.0
	gateway 192.217.2.1
```
* WISE
```
auto eth0
iface eth0 inet static
	address 192.217.3.2
	netmask 255.255.255.0
	gateway 192.217.3.1
```
melakukan testing dengan sebagai berikut 

![image1.3](image/no%201.png)

## Soal 2
Untuk mempermudah mendapatkan informasi mengenai misi dari Handler, bantulah Loid membuat website utama dengan akses wise.yyy.com dengan alias www.wise.yyy.com pada folder wise

### Jawaban Soal 2
**Server WISE**

penjelasan)

``/etc/bind/named.conf.local``

```
zone "wise.itb06.com" {
        type master;
        file "/etc/bind/wise/wise.itb06.com";
};
```

**Testing tanpa SSS**
Saat kita melakukan testing menjalankan perintah 
``ping wise.itb06.com``

Berikut merupakan hasil dokumentasinya saat testing berjalan 

![image2.1](image/no2.png)

## Soal 3
Setelah itu ia juga ingin membuat subdomain eden.wise.yyy.com dengan alias www.eden.wise.yyy.com yang diatur DNS-nya di WISE dan mengarah ke Eden

### Jawaban Soal 3

langkah langkah

**Testing pada SSS**

dengan menjalankan perintah 

``ping eden.wise.itb06.com``

Berikut merupakan hasil dokumentasinya saat testing berjalan 

![image3.1](image/3.1.png)

dan menjalankan perintah 

``ping www.eden.wise.itb06.com``

![image3.2](image/3.2.png)

## Soal no 4
 Buat juga reverse domain untuk domain utama

 (penyelasaian )


**Testing pada SSS**

dengan menjalankan perintah 


``host -t PTR 192.217.3.2``

berikut dokumentasinya :

![image4](image/4.png)

## Soal 5 

Agar dapat tetap dihubungi jika server WISE bermasalah, buatlah juga Berlint sebagai DNS Slave untuk domain utama 

(penyelasaian )

**Testing pada SSS**

Perintah yang di jalankan 

``ping wise.itbo6.com``

berikut dokumentasinya :

![image5](image/5.png)

## Soal no 6 

Karena banyak informasi dari Handler, buatlah subdomain yang khusus untuk operation yaitu operation.wise.yyy.com dengan alias www.operation.wise.yyy.com yang didelegasikan dari WISE ke Berlint dengan IP menuju ke Eden dalam folder operation 

### Jawaban soal no 6

penjelasannya soon 

**Testing pada SSS**

Perintah yang di jalankan 

``ping operation.wise.itb06.com``

berikut dokumentasinya 

![image6.1](image/6.1.png)

dan perintah yang di jalankan 

``ping www.operation.wise.itb06.com``

berikut dokumentasinya 

![image6.2](image/6.2.png)


## Soal no 7

Untuk informasi yang lebih spesifik mengenai Operation Strix, buatlah subdomain melalui Berlint dengan akses strix.operation.wise.yyy.com dengan alias www.strix.operation.wise.yyy.com yang mengarah ke Eden

## Jawaban soal no 7 

penjelasan soon

**Testing pada SSS**
Perintah yang di jalankan 

``host -t CNAME www.strix.operation.wise.itb06.com``

berikut dokumentasinya 

![image7.1](image/7.1.png)

kemudian 

``ping strix.operation.wise.itb06.com``

berikut dokumentasinya 

![image7.2](image/7.2.png)

dan terakhir menjalankan perintah 

``host -t A strix.operation.wise.itb06.com``

berikut dokumentasinya 

![image7.3](image/7.3.png)

## Soal no 8 

Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.wise.yyy.com. Pertama, Loid membutuhkan webserver dengan DocumentRoot pada /var/www/wise.yyy.com

### Jawaban soal no 8 

penjelasan soon 

**Testing pada SSS**

Perintah yang di jalankan 

``lynx wise.ITB06.com``

output : 

![image8](image/8.png)

## Soal no 9 
Setelah itu, Loid juga membutuhkan agar url www.wise.yyy.com/index.php/home dapat menjadi menjadi www.wise.yyy.com/home 

### Jawaban soal no 9 

penjelasan soon 

**Testing pada SSS**

Perintah yang di jalankan 

``lynx www.wise.itb06.com/home``

output : 

![image9](image/8.png)

## Soal no 10 

Setelah itu, pada subdomain www.eden.wise.yyy.com, Loid membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/eden.wise.yyy.com

### Jawaban soal no 10

penjelasan soon

**Testing pada SSS**

Perintah yang di jalankan 

``lynx eden.wise.ITB06.com``

output : 

![image10](image/10.png)

## Soal no 11

Akan tetapi, pada folder /public, Loid ingin hanya dapat melakukan directory listing saja

### Jawaban soal no 11

penjelasan soon

**Testing pada SSS**

Perintah yang di jalankan 

``lynx eden.wise.ITB06.com/public``

output : 

![image11](image/11.png)

## Soal no 12

Tidak hanya itu, Loid juga ingin menyiapkan error file 404.html pada folder /error untuk mengganti error kode pada apache

### Jawaban soal no 12

penjelasan soon

**Testing pada SSS**

Perintah yang di jalankan 

``lynx eden.wise.ITB06.com/haloo``

output : 

![image12](image/12.png)

## Soal no 13

Loid juga meminta Franky untuk dibuatkan konfigurasi virtual host. Virtual host ini bertujuan untuk dapat mengakses file asset www.eden.wise.yyy.com/public/js menjadi www.eden.wise.yyy.com/js

### Jawaban soal no 13

penjelasan soon

**Testing pada SSS**

Perintah yang di jalankan 

``lynx eden.wise.ITB06.com/js``

output : 

![image13](image/13.png)

## Soal no 14 dan 15

Loid meminta agar www.strix.operation.wise.yyy.com hanya bisa diakses dengan port 15000 dan port 15500 dengan autentikasi username Twilight dan password opStrix dan file di /var/www/strix.operation.wise.yyy

### Jawaban soal no 14 dan 15

penjelasan soon

**Testing pada SSS**

Perintah yang di jalankan 

``lynx www.strix.operation.wise.itb06.com:1500``

output : 

![image14](image/14.png)

## Soal no 16

dan setiap kali mengakses IP Eden akan dialihkan secara otomatis ke www.wise.yyy.com

### Jawaban soal no 16

penjelasan soon

**Testing pada SSS**

Perintah yang di jalankan 

``lynx 192.217.2.3``

output : 

![image8](image/16.png)

## Soal no 17

Karena website www.eden.wise.yyy.com semakin banyak pengunjung dan banyak modifikasi sehingga banyak gambar-gambar yang random, maka Loid ingin mengubah request gambar yang memiliki substring “eden” akan diarahkan menuju eden.png. Bantulah Agent Twilight dan Organisasi WISE menjaga perdamaian! 


### Jawaban soal no 17

penjelasan soon

**Testing pada SSS**

Perintah yang di jalankan 

``lynx eden.wise.ITB06.com/edening.png``

output : 

![image17.1](image/17.1.png)
![image17.2](image/17.2.png)
![image17.3](image/17.3.png)
