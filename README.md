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
5. [Soal 2](#Soal-2)
6. [Soal 3](#Soal-3)
7. [Soal 4](#Soal-4)
8. [Soal 5](#Soal-5)
9. [Soal 6](#Soal-6)
10. [Soal 7](#Soal-7)
11. [Soal 8](#Soal-8)
12. [Soal 9](#Soal-9)
13. [Soal 10](#Soal-10)
14. [Soal 11](#Soal-11)
15. [Soal 12](#Soal-12)
   
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

* Lakukan setup diatas
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
> Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com

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

## Soal 7
> Membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya

* Sriwijaya
```
  echo 'zone "sudarsana.it35.com" {
        type master;
        file "/etc/bind/jarkom/sudarsana.it35.com";
        allow-transfer { 192.234.2.2; };
        also-notify { 192.234.2.2; };
};' > /etc/bind/named.conf.local

echo 'zone "pasopati.it35.com" {
        type master;
        file "/etc/bind/jarkom/pasopati.it35.com";
        also-notify { 192.234.2.2; };
        allow-transfer { 192.234.2.2; };

};' >> /etc/bind/named.conf.local

echo 'zone "rujapala.it35.com" {
        type master;
        file "/etc/bind/jarkom/rujapala.it35.com";
        also-notify { 192.234.2.2; };
        allow-transfer { 192.234.2.2; }; 
   
};' >>/etc/bind/named.conf.local
```

* Majapahit
```
echo 'zone "sudarsana.it35.com" {
    type slave;
    masters { 192.234.1.3; }; 
    file "/var/lib/bind/sudarsana.it35.com";
};

zone "pasopati.it35.com" {
    type slave;
    masters { 192.234.1.3; }; 
    file "/var/lib/bind/pasopati.it35.com";
};

zone "rujapala.it35.com" {
    type slave;
    masters { 192.234.1.3; }; 
    file "/var/lib/bind/rujapala.it35.com";
};'  > /etc/bind/named.conf.local
```


## Soal 8 
> Membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu


* Sriwijaya2 update
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
@       IN      A       192.234.2.3   ; IP Kotalingga
www     IN      CNAME   sudarsana.it35.com.
cakra   IN      A       192.234.2.5   ;' > /etc/bind/jarkom/sudarsana.it35.com

service bind9 restart
```

## Soal 9 
> Membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.

* Sriwijaya
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it35.com. root.pasopati.it35.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it35.com.
@       IN      A       192.234.2.3
www     IN      CNAME   pasopati.it35.com.
ns1     IN      A       192.234.2.2     ; IP Majapahit
panah   IN      NS      ns1' > /etc/bind/jarkom/pasopati.it35.com


echo "options {
    directory \"/var/cache/bind\";

    allow-query { any; };
    auth-nxdomain no;
    listen-on-v6 { any; };
};" > /etc/bind/named.conf.options

service bind9 restart
```

* Majapahit
```
echo "
options {
        directory \"/var/cache/bind\";
        allow-query{any;};
        auth-nxdomain no;    
        listen-on-v6 { any; };
};
" > /etc/bind/named.conf.options

echo '

zone "panah.pasopati.it35.com"{
        type master;
        file "/etc/bind/panah/panah.pasopati.it35.com";
};
'>> /etc/bind/named.conf.local

mkdir /etc/bind/panah

echo "
\$TTL    604800
@       IN      SOA     panah.pasopati.it35.com. root.panah.pasopati.it35.com. (
                        2021100401      ; Serial
                        604800         ; Refresh
                        86400         ; Retry
                        2419200         ; Expire
                        604800 )       ; Negative Cache TTL
;
@               IN      NS      panah.pasopati.it35.com.
@               IN      A       192.234.2.3       ;ip Kotalingga
www             IN      CNAME   panah.pasopati.it35.com.
" > /etc/bind/panah/panah.pasopati.it35.com
service bind9 restart
```

## Soal 10 
> Buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga

* majapahit
```
echo "
\$TTL    604800
@       IN      SOA     panah.pasopati.it35.com. root.panah.pasopati.it35.com. (
                        2021100401      ; Serial
                        604800         ; Refresh
                        86400         ; Retry
                        2419200         ; Expire
                        604800 )       ; Negative Cache TTL
;
@               IN      NS      panah.pasopati.it35.com.
@               IN      A       192.234.2.3       ;
www             IN      CNAME   panah.pasopati.it35.com.
log             IN      A       192.234.2.3       ; 
www.log         IN      CNAME   log.panah.pasopati.it35.com." > /etc/bind/panah/panah.pasopati.it35.com
service bind9 restart
```

## Soal 11 
>  Buatlah konfigurasi agar warga IT yang berada diluar Majapahit dapat mengakses jaringan luar melalui DNS Server Majapahit

* majapahit
```
echo 'options {
    directory "/var/cache/bind";

    // If there is a firewall between you and nameservers you want
    // to talk to, you may need to fix the firewall to allow multiple
    // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

    // If your ISP provided one or more IP addresses for stable
    // nameservers, you probably want to use them as forwarders.
    // Uncomment the following block, and insert the addresses replacing
    // the all-0s placeholder.
    forwarders {
        192.168.122.1;
    };

    //========================================================================
    // If BIND logs error messages about the root key being expired,
    // you will need to update your keys.  See https://www.isc.org/bind-keys
    //========================================================================
    //dnssec-validation auto;

    allow-query { any; };
    auth-nxdomain no;
    listen-on-v6 { any; };
};' > /etc/bind/named.conf.options
```


## Soal 12
> isi soal
