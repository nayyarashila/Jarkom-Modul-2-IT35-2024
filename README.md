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
echo -e "nameserver 192.234.1.3\nnameserver 192.234.2.2" > /etc/resolv.conf
```


## Soal 1

* Lakukan setup diatas
* Masukkan `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.234.0.0/16` pada baris bawah file `nano /root/.bashrc` 
* Kemudian apabila `cat /etc/resolv.conf` maka akan keluar nameserver seperti dibawah

![image](https://github.com/user-attachments/assets/fa728a39-dc6d-426d-a73a-1efff7583ac3)

* Kemudian lakukan `ping google.com` untuk ping dalam

![Screenshot 2024-10-02 215907](https://github.com/user-attachments/assets/0e2fd449-d7b7-4c51-afe7-e4bb98d2b0c1)


## 2. Sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com 

* Buatlah domain, disini saya memakai `sriwijaya2.sh` kemudian isi config seperti dibawah

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
@       IN      A       192.234.1.4   ; IP Solok
www     IN      CNAME   sudarsana.it35.com.' > /etc/bind/jarkom/sudarsana.it35.com

service bind9 restart
```

* Jalankan menggunakan command `./sriwijaya2.sh`
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

* Sriwijaya
```
echo 'zone "2.234.192.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/2.234.192.in-addr.arpa";
};' >> /etc/bind/named.conf.local

mkdir -p /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/2.234.192.in-addr.arpa

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it35.com. root.pasopati.it35.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
2.234.192.in-addr.arpa.   IN      NS      pasopati.it35.com.
4                       IN      PTR     pasopati.it35.com.
' > /etc/bind/jarkom/2.234.192.in-addr.arpa

service bind9 restart
```
Testing

![Screenshot 2024-10-03 002649](https://github.com/user-attachments/assets/26aefae0-3387-4e9a-a22a-a591d65ba14f)

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
Testing
service bind9 stop di Sriwijaya, tapi tetep bisa ping

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
Testing
ping cakra.sudarsana.it35.com lupa belum di ss

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

Testing

![Screenshot 2024-10-03 195153](https://github.com/user-attachments/assets/2df28f89-08be-44f3-9557-940f3efac68d)


## Soal 10 
> Buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga

* Majapahit
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

Testing

![Screenshot 2024-10-03 213932](https://github.com/user-attachments/assets/f5b6ba97-954d-4fb3-b015-2645bae6e02e)

## Soal 11 
>  Buatlah konfigurasi agar warga IT yang berada diluar Majapahit dapat mengakses jaringan luar melalui DNS Server Majapahit

* Majapahit
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

Testing

![Screenshot 2024-10-03 215853](https://github.com/user-attachments/assets/8723f76e-460c-47c1-8b37-47888a6be878)

## Soal 12
> Karena pusat ingin sebuah laman web yang ingin digunakan untuk memantau kondisi kota lainnya maka deploy laman web ini (cek resource yg lb) pada Kotalingga menggunakan apache

* client
```
apt-get update
apt-get install lynx -y
```

* kotalingga
```
apt-get update
apt-get install lynx -y
apt-get install apache2 -y
apt-get install libapache2-mod-php7.0 -y
apt-get install unzip -y
apt-get install php -y
apt-get install wget -y
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/it35.conf
rm /etc/apache2/sites-enabled/000-default.conf
echo '
<VirtualHost *:8080>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
' > /etc/apache2/sites-available/it35.conf
echo 'Listen 80
Listen 8080

<IfModule ssl_module>
    Listen 443
</IfModule>

<IfModule mod_gnutls.c>
    Listen 443
</IfModule>
' > /etc/apache2/ports.conf
a2dissite 000-default.conf
a2ensite it35.conf
service apache2 reload
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1Sqf0TIiybYyUp5nyab4twy9svkgq8bi7' -O lb.zip
unzip lb.zip -d lb
mv ./lb/worker/index.php /var/www/html/index.php
service apache2 restart
```

testing

![Screenshot 2024-10-04 013621](https://github.com/user-attachments/assets/23b06428-4bec-4a86-9ce9-263ff911ac88)

## Soal 13
> Karena Sriwijaya dan Majapahit memenangkan pertempuran ini dan memiliki banyak uang dari hasil penjarahan (sebanyak 35 juta, belum dipotong pajak) maka pusat meminta kita memasang load balancer untuk membagikan uangnya pada web nya, dengan Kotalingga, Bedahulu, Tanjungkulai sebagai worker dan Solok sebagai Load Balancer menggunakan apache sebagai web server nya dan load balancer nya.

* Sriwijaya dan Majapahit
```
/etc/resolv.conf tambah nameserver 192.234.1.4
```

* Semua webserver
```
apt-get update
apt-get install lynx -y
apt-get install apache2 -y
apt-get install libapache2-mod-php7.0 -y
apt-get install unzip -y
apt-get install php -y
apt-get install wget -y
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/it35.conf
rm /etc/apache2/sites-enabled/000-default.conf
echo '
<VirtualHost *:8080>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
' > /etc/apache2/sites-available/it35.conf
echo 'Listen 80
Listen 8080

<IfModule ssl_module>
    Listen 443
</IfModule>

<IfModule mod_gnutls.c>
    Listen 443
</IfModule>
' > /etc/apache2/ports.conf
a2dissite 000-default.conf
a2ensite it35.conf
service apache2 reload
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1Sqf0TIiybYyUp5nyab4twy9svkgq8bi7' -O lb.zip
unzip lb.zip -d lb
mv ./lb/worker/index.php /var/www/html/index.php
service apache2 restart
```

* Solok
```
apt-get update
apt-get install apache2 -y
apt-get install libapache2-mod-php7.0 -y
apt-get install php -y

a2enmod proxy
a2enmod proxy_http
a2enmod proxy_balancer
a2enmod lbmethod_byrequests

service apache2 start
echo '
<VirtualHost *:80>
    <Proxy balancer://serverpool>
        BalancerMember http://192.234.2.3/
        BalancerMember http://192.234.2.5/
        BalancerMember http://192.234.2.4/
        ProxySet lbmethod=byrequests
    </Proxy>
    ProxyPass / balancer://serverpool/
    ProxyPassReverse / balancer://serverpool/
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf

service apache2 restart
```

Testing

https://github.com/user-attachments/assets/b7ccb87d-efbc-422d-815d-03802e8c2e14

## Soal 14
> Selama melakukan penjarahan mereka melihat bagaimana web server luar negeri, hal ini membuat mereka iri, dengki, sirik dan ingin flexing sehingga meminta agar web server dan load balancer nya diubah menjadi nginx.

* semua server
```
apt-get update
apt-get install dnsutils -y
apt-get install lynx -y
apt-get install nginx -y
apt-get install apache2 -y
apt-get install libapache2-mod-php7.0 -y
apt-get install wget -y
apt-get install unzip -y
apt-get install php -y 
apt-get install php-fpm -y

service php7.0-fpm start
service nginx start

wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1Sqf0TIiybYyUp5nyab4twy9svkgq8bi7' -O lb.zip
unzip lb.zip -d lb

mv ./lb/worker/index.php /var/www/html/index.php
rm -rf ./lb
rm lb.zip

echo 'server {
    listen 8082;
    root /var/www/html;

    index index.php index.html index.htm;
    server_name _;

    location / {
        try_files \$uri \$uri/ /index.php?\$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
     deny all;
    }

    error_log /var/log/nginx/jarkom-it35_error.log;
    access_log /var/log/nginx/jarkom-it35_access.log;
}' > /etc/nginx/sites-available/it35

ln -s /etc/nginx/sites-available/it35 /etc/nginx/sites-enabled
rm /etc/nginx/sites-enabled/default
service nginx restart
```

* solok
```
apt-get update
apt-get install dnsutils -y
apt-get install lynx -y
apt-get install nginx -y
apt-get install apache2 -y
apt-get install libapache2-mod-php7.0 -y
apt-get install wget -y
apt-get install unzip -y
apt-get install php -y 
apt-get install php-fpm -y

service php7.0-fpm start
service nginx start

echo 'upstream webserver  {
    ip_hash;
    server 192.234.2.3:8082; 
    server 192.234.2.5:8083; 
    server 192.234.2.4:8084;
}

server {
  listen 8082;
  server_name 192.234.2.3;

  location / {
    proxy_pass http://webserver;
  }
}

server {
  listen 8083;
  server_name 192.234.2.5;

  location / {
    proxy_pass http://webserver;
  }
}

server {
  listen 8084;
  server_name 192.234.2.4;

  location / {
    proxy_pass http://webserver;
  }
}' > /etc/nginx/sites-available/it35

ln -s /etc/nginx/sites-available/it35 /etc/nginx/sites-enabled
rm /etc/nginx/sites-enabled/default

service nginx restart
```

Testing

![Screenshot 2024-10-04 030916](https://github.com/user-attachments/assets/e793d648-7e2d-4147-ae39-9979accb5fac)

![Screenshot 2024-10-04 030951](https://github.com/user-attachments/assets/ea7f678b-2898-42fd-ac4e-a75293f7ef48)

![Screenshot 2024-10-04 031014](https://github.com/user-attachments/assets/98cc00ea-748c-4391-a6c7-d791c84fc8c6)

