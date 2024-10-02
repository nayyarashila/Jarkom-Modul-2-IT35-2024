# Jarkom-Modul-2-IT35-2024

| Nama          | NRP          |
| ------------- | ------------ |
| RM Novian Malcolm Bayuputra | 5027231035 |
| Nayyara Ashila | 5027231083 |


# Laporan Resmi praktikum Jarkom Modul 2
## Daftar Isi
1. [Topologi](#Topologi)
2. [Setup Config](#Setup-Config)
3. [Bashrc](#Bashrc)
4. [Soal 1](#Soal-1)
   
## Topologi

![Screenshot 2024-10-01 011026](https://github.com/user-attachments/assets/d6c00f38-a6c2-4c5b-b6c1-010b94d2f882)


## Setup Config

* Nusantara
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.234.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.234.2.1
	netmask 255.255.255.0
```

* Sanjaya
```
auto eth0
iface eth0 inet static
	address 192.234.1.2
	netmask 255.255.255.0
	gateway 192.234.1.1
```

* Sriwijaya
```
auto eth0
iface eth0 inet static
	address 192.234.1.3
	netmask 255.255.255.0
	gateway 192.234.1.1
```

* Solok
```
auto eth0
iface eth0 inet static
	address 192.234.1.4
	netmask 255.255.255.0
	gateway 192.234.1.1
```

* Samaratungga
```
auto eth0
iface eth0 inet static
	address 192.234.1.5
	netmask 255.255.255.0
	gateway 192.234.1.1
```

* Ken Arok
```
auto eth0
iface eth0 inet static
	address 192.234.1.6
	netmask 255.255.255.0
	gateway 192.234.1.1
```

* Majapahit
```
auto eth0
iface eth0 inet static
	address 192.234.2.2
	netmask 255.255.255.0
	gateway 192.234.2.1
```

* Kotalingga
```
auto eth0
iface eth0 inet static
	address 192.234.2.3
	netmask 255.255.255.0
	gateway 192.234.2.1
```

* Tanjungkulai
```
auto eth0
iface eth0 inet static
	address 192.234.2.4
	netmask 255.255.255.0
	gateway 192.234.2.1
```

* Bedahulu
```
auto eth0
iface eth0 inet static
	address 192.234.2.5
	netmask 255.255.255.0
	gateway 192.234.2.1
```
##  Bashrc

* Setup Server
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y

```

* Setup Client
```
echo nameserver `192.168.122.1` > /etc/resolv.conf

```

* Setup Client
```
echo nameserver `192.168.122.1` > /etc/resolv.conf

```


## Soal 1

*Lakukan setup diatas
* Masukkan `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.234.0.0/16` pada baris bawah file `nano /root/.bashrc` 
* Kemudian apabila `cat /etc/resolv.conf` maka akan keluar nameserver seperti dibawah

![image](https://github.com/user-attachments/assets/fa728a39-dc6d-426d-a73a-1efff7583ac3)

* Kemudian lakukan `ping google.com` untuk ping dalam

![Screenshot 2024-10-02 215907](https://github.com/user-attachments/assets/0e2fd449-d7b7-4c51-afe7-e4bb98d2b0c1)


## 2. Sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com 

* Buatlah domain, disini saya memakai `Sriwijaya2.bashrc` kemudian isi config seperti dibawah

```
#!/bin/bash
apt update
apt install bind9 -y

echo 'zone "sudarsana.it35.com" {
	type master;
	file "/etc/bind/jarkom/sudarsana.it35.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/sudarsana.it35.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sudarsana.it35.com. root.sudarsana.it35.com. (
                        2024100104      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      sudarsana.it35.com.
@       IN      A         10.77.2.4   ; IP Kotalingga
www     IN      CNAME   sudarsana.it27.com.' > /etc/bind/jarkom/sudarsana.it35.com

service bind9 restart
```

* Jalankan menggunakan command `./Sriwijaya2.bashrc`
* Kemudian jalankan `ping sudarsana.it35.com`

--Result--

![Screenshot 2024-10-02 215907](https://github.com/user-attachments/assets/ac19c9d4-4f3b-42b0-af6c-1180b3ecc7c4)

## Soal 3
> Domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga

* Buatlah domain, disini saya memakai `sriwijaya3.bashrc` kemudian isi config seperti dibawah
```
#!/bin/bash
apt update
apt install bind9 -y

echo 'zone "pasopati.it35.com" {
	type master;
	file "/etc/bind/jarkom/pasopati.it35.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/pasopati.it35.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it35.com. root.pasopati.it35.com. (
                        2024100104      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it35.com.
@       IN      A            ; IP Kotalingga
www     IN      CNAME   sudarsana.it35.com.' > /etc/bind/jarkom/sudarsana.it35.com

service bind9 restart
```

* Jalankan menggunakan command `./sriwijaya3.bashrc`
* Kemudian jalankan `ping pasopati.it35.com`

--Result--

![Screenshot 2024-10-01 230103](https://github.com/user-attachments/assets/e80e22df-5b97-43b0-a524-4842b8e1ec89)


## Soal 4
Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com

* Buatlah domain, disini saya memakai `sriwijaya4.bashrc` kemudian isi config seperti dibawah

```
#!/bin/bash
apt update
apt install bind9 -y

echo 'zone "pasopati.it35.com" {
	type master;
	file "/etc/bind/jarkom/rujapalai.it35.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/rujapala.it35.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it35.com. root.rujapalai.it35.com. (
                        2024100104      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      rujapala.it35.com.
@       IN      A   192.234.2.3          ; IP Kotalingga
www     IN      CNAME  rujapala.it35.com.' > /etc/bind/jarkom/rujapala.it35.com

service bind9 restart
```
* Jalankan menggunakan command `./sriwijaya4.bashrc`
* Kemudian jalankan `ping rujapala.it35.com`


## Soal 5 
> Ping domain seluruh komputer (client) yang berada di Nusantara

* Untuk tes lakukan `ping google.com`
  
 ![Screenshot 2024-10-02 221020](https://github.com/user-attachments/assets/530a1715-3606-4a5e-b7c7-864a2607763f)

* Kemudian coba pada client, disini saya memakai IP Sriwijaya yaitu `192.234.1.3`
  
![Screenshot 2024-10-02 220935](https://github.com/user-attachments/assets/92bec5c1-35e6-4668-a1af-51bbbb5454c1)


## Soal 6 
> Pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga




