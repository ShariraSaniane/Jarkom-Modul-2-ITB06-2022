# Jarkom-Modul-2-ITB06-2022

Repository ini dibuat sebagai laporan resmi untuk pengerjaan [Soal Shift Modul 2](https://docs.google.com/document/d/11Mz2Fd3DKtGkCknHee9VZRdJYvZ3YAMIaifObHEpBFo/edit) dari praktikum Mata Kuliah Komunikasi Data dan Jaringan Komputer.

Repository ini dibuat oleh:

**Kelompok ITB06**

- Sarah Hanifah Pontoh 5027201006
- Sharira Saniane 5027201016
- Naufal Dhiya Ulhaq 5027201029

## Pembukaan soal

Twilight (〈黄昏 (たそがれ) 〉, <Tasogare>) adalah seorang mata-mata yang berasal dari negara Westalis. Demi menjaga perdamaian antara Westalis dengan Ostania, Twilight dengan nama samaran Loid Forger (ロイド・フォージャー, Roido Fōjā) di bawah organisasi WISE menjalankan operasinya di negara Ostania dengan cara melakukan spionase, sabotase, penyadapan dan kemungkinan pembunuhan. Berikut adalah peta dari negara Ostania:

!![image1.1](image/topologi1.png)

## Soal 1

WISE akan dijadikan sebagai DNS Master, Berlint akan dijadikan DNS Slave, dan Eden akan digunakan sebagai Web Server. Terdapat 2 Client yaitu SSS, dan Garden. Semua node terhubung pada router Ostania, sehingga dapat mengakses internet

### Jawaban Soal 1

Kami membuat topologi telebih dahulu sebagai berikut :

!![image1.2](image/topologi.png)

Langkah berikutnya kami akan melakukan konfigurasi pada setiap node yang ada :

- Ostania sebagai router

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

- SSS

```
auto eth0
iface eth0 inet static
	address 192.217.1.2
	netmask 255.255.255.0
	gateway 192.217.1.1
```

- Garden

```
auto eth0
iface eth0 inet static
	address 192.217.1.3
	netmask 255.255.255.0
	gateway 192.217.1.1
```

- Berlint

```
auto eth0
iface eth0 inet static
	address 192.217.2.2
	netmask 255.255.255.0
	gateway 192.217.2.1
```

- Eden

```
auto eth0
iface eth0 inet static
	address 192.217.2.3
	netmask 255.255.255.0
	gateway 192.217.2.1
```

- WISE

```
auto eth0
iface eth0 inet static
	address 192.217.3.2
	netmask 255.255.255.0
	gateway 192.217.3.1
```

melakukan testing dengan sebagai berikut

!![image1.3](image/no%201.png)

## Soal 2

Untuk mempermudah mendapatkan informasi mengenai misi dari Handler, bantulah Loid membuat website utama dengan akses **wise.yyy.com** dengan alias **www.wise.yyy.com** pada folder wise

### Jawaban Soal 2

- WISE

Mengedit konfigurasi pada WISE sebagai server di file `/etc/bind/named.conf.local` untuk emnambahkan zone baru.

```
nano /etc/bind/named.conf.local
```

```
zone "wise.ITB06.com"{
        type master;
        file "/etc/bind/wise/wise.ITB06.com";
};
```

Setelah itu buatlah direktori baru pada WISE

```
mkdir -p /etc/bind/wise
```

Mengedit konfigurasi lokal WISE untuk menambahkan domain di file `/etc/bind/wise/wise.ITB06.com`

```
nano /etc/bind/wise/wise.ITB06.com
```

```
$TTL    604800
@       IN      SOA     wise.ITB06.com. root.wise.ITB06.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@             IN      NS      wise.ITB06.com.
@             IN      A       $WISE_IP ; IP WISE
@             IN      AAAA    ::1
www           IN      CNAME   wise.ITB06.com.
```

Restart bind9 pada WISE

```
service bind9 restart
```

- SSS

Menambahkan nameserver pada konfigurasi SSS sebagai client. Jalankan perintah berikut satu persatu

```
apt update
apt install dnsutils -y
echo "nameserver 192.217.3.2" > /etc/resolv.conf
```

Testing pada client SSS

```
ping wise.itb06.com
```
