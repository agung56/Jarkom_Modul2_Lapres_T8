# Jarkom_Modul2_Lapres_T8
#### Anggota Kelompok:
1. Kadek Nesya Kurniadewi (05311840000009)
2. Agung Mulyono (05311840000035)

Soal Shift Modul2 https://drive.google.com/drive/folders/1Gb90AYZSb-qw38avjn2eKAPxouR3fS8a

### Membuat Topologi Jaringan
Sintaks file **topologi.sh**<br>
![topologi](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/topologi.png)
* Setelah membuat file **topologi.sh**, kemudian bash file tersebut dengan perintah `bash topologi.sh`
* Memastikan semua UML yang dibuat berfungsi dengan baik dan login di tiap UML-nya
* Kemudian hilangkan tanda pagar (#) pada bagian `net.ipv4.ip_forward=1` dengan perintah `nano /etc/sysctl.conf` pada router **SURABAYA**. Lalu ketikkan `sysctl -p` untuk mengaktifkan perubahan yang ada. <br>
![forward](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/ipsurabaya.png)
* Setting IP pada setiap UML dengan mengetikkan `nano /etc/network/interfaces`
![surabaya](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/iptuntapsurabaya.png)<br>
![malang](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/ipmalang.png)<br>
![mojokerto](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/ipmojokerto.png)<br>
![probolinggo](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/ipprobolinggo.png)<br>
![gresik](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/ipgresik.png)<br>
![sidoarjo](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/ipsidoarjo.png)<br>
* Restart network pada semua UML dengan mengetikkan `service networking restart`
* Agar UML selain **SURABAYA** bisa melakukan koneksi ke jaringan luar, maka ketikkan `iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16`
* Export proxy pada setiap UML dengan sintaks <br>
`export http_proxy=”http://DPTSI-564876-66b39:c3f12@proxy.its.ac.id:8080”` <br>
`export https_proxy=”http://DPTSI-564876-66b39:c3f12@proxy.its.ac.id:8080”` <br>
`export ftp_proxy=”http://DPTSI-564876-66b39:c3f12@proxy.its.ac.id:8080”` <br>
* Setelah itu lakukan update dengan mengetikkan `apt-get update`


### Soal dan Penyelesaian
### 1. Membuat domain utama dengan alamat http://semerut08.pw
#### Penyelesaian
* Lakukan update pada **MALANG** dengan mengetikkan `apt-get update`
* Kemudian install bind9 dengan menggunakan perintah `apt-get install bind9 -y`
* Isikan perintah pada **MALANG** seperti berikut. <br>
`nano /etc/bind/named.conf.local`
* Isikan konfigurasi domain **semerut08.pw** sesuai dengan sintaks berikut. <br>
```
zone "semerut08.pw"{
	type master;
	file "/etc/bind/jarkom/semerut08.pw";
};
```
 ![zonemalang](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/bindmalang.png)<br>
 * Buat file **jarkom** dalam **/etc/bind**<br>
 `mkdir /etc/bind/jarkom`<br>
 * Copykan file **db.local** pada path **/etc/bind** ke dalam folder **jarkom** yang baru saja dibuat dan ubah namanya menjadi **semerut08.pw** <br>
 `cp /etc/bind/db.local /etc/bind/jarkom/semerut08.pw`<br>
 * Edit file **semerut08.pw** dengan mengetikkan perintah `nano /etc/bind/jarkom/semerut08.pw`seperti gambar dibawah.<br>
 ![semerut08](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/semerut08.png)
 * Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
### 2. Membuat alias http://www.semerut08.pw
#### Penyelesaian
* Tambahkan **www** pada file **semerut08.pw** seperti pada gambar dibawah.<br>
![semerut081](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/semerut08.png)<br>
* Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
### 3. Membuat subdomain http://penanjakan.semerut08.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO
#### Penyelesaian
* Tambahkan subdomain **penanjakan** seperti pada gambar dibawah . <br>
![semerut082](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/semerut08.png)<br>
* Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
### 4. Membuat reverse domain untuk domain utama
#### Penyelesaian
* Buka `nano /etc/bind/jarkom/semerut08.pw`
* Tambahkan konfigurasi berikut ke dalam file **named.conf.local**<br>
```
zone "83.151.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/83.151.10.in-addr.arpa";
};
```
![zoneptr](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/bindmalang.png)<br>
* Copykan file **db.local** pada path **/etc/bind** ke dalam folder **jarkom** yang baru saja dibuat dan ubah namanya menjadi **83.151.10.in-addr.arpa**<br>
`cp /etc/bind/db.local /etc/bind/jarkom/83.151.10.in-addr.arpa`<br>
* Edit file **83.151.10.in-addr.arpa** seperti gambar dibawah
![ptr](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/ptrmalang.png)<br>
* Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
### 5. Membuat DNS Server Slave pada MOJOKERTO
#### Penyelesaian
**I. Konfigurasi pada server MALANG**
* Edit file **/etc/bind/named.conf.local** dan sesuaikan dengan sintaks berikut
```
zone "semerut08.pw" {
    type master;
    notify yes;
    also-notify { 10.151.83.147; };
    allow-transfer { 10.151.83.147; };
    file "/etc/bind/jarkom/semerut08.pw";
};
```
![bind1malang](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/bindmalang.png)<br>
* Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
**II. Konfigurasi pada server MOJOKERTO**
* Buka **MOJOKERTO** dan update package lists dengan menggunakan perintah `apt-get update`
* Kemudian install bind9 dengan menggunakan perintah `apt-get install bind9 -y`
* Kemudian buka file **/etc/bind/named.conf.local** pada **MOJOKERTO** dan tambahkan sintaks berikut
```
zone "semerut08.pw" {
    type slave;
    masters { 10.151.83.146; };
    file "/var/lib/bind/semerut08.pw";
};
```
![bindmojokerto](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/bindmojokerto.png)<br>
* Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
**III.Testing**
* Pada server **MALANG** matikan bind9 dengan cara mengetikkan `service bind9 stop`
* Pada client **GRESIK** beri tanda pagar pada nameserver **MALANG**
![optiongresik](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/nameservergresik2.png)<br>
* Kemudian lakukan **ping semerut08.pw** pada client **GRESIK**
### 6. Membuat subdomain dengan alamat http://gunung.semerut08.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO
#### Penyelesaian
**I. Konfigurasi pada server MALANG**
* Pada **MALANG**,edit file **/etc/bind/jarkom/semerut08.pw** dan ubah menjadi seperti dibawah `nano /etc/bind/jarkom/semerut08.pw`<br>
![semerut083](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/semerut08.png)<br>
* Kemudian edit file **/etc/bind/named.conf.options** pada **MALANG** `nano /etc/bind/named.conf.options`<br>
* Kemudian comment **dnssec-validation auto** dan tambahkan baris berikut pada **/etc/bind/named.conf.options** `allow-query{any;};`<br>
![optionsmalang](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/optionsmalang.png)
* Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
**II. Konfigurasi pada server MOJOKERTO**
* Pada **MOJOKERTO** edit file **/etc/bind/named.conf.options** `nano /etc/bind/named.conf.options`
* Kemudian comment **dnssec-validation auto** dan tambahkan baris berikut pada **/etc/bind/named.conf.options** `allow-query{any;};`<br>
![optionsmojokerto](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/optionsmojokerto.png)
* Lalu edit file /etc/bind/named.conf.local menjadi seperti gambar di bawah
```
zone "gunung.semerut08.pw {
    type master;
    file "/etc/bind/delegasi/gunung.semerut08.pw";
    allow-transfer { any; };
};
```
![bindmojokerto1](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/bindmojokerto.png)
* Kemudian buat direktori dengan nama **delegasi**
* Copy **db.local**, edit namanya menjadi **gunung.semerut08.pw**
```
mkdir /etc/bind/delegasi
cp /etc/bind/db.local /etc/bind/delegasi/gunung.semerut08.pw
```
* Edit file **gunung.semerut08.pw** menjadi seperti dibawah ini
![naikgunung](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/naikgunung.png)
* Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
### 7. Membuat subdomain **http://naik.gunung.semerut08.pw**, domain diarahkan ke IP Server **PROBOLINGGO**
#### Penyelesaian
* Edit file **gunung.semerut08.pw** menjadi seperti dibawah ini
![naikgunung](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/naikgunung.png)
* Setelah itu restart bind9 dengan menggunakan perintah `service bind9 restart`<br>
### 8. Mengatur web server dengan domain **http://semerut08.pw** memiliki *DocumentRoot* pada **/var/www/semerut08.pw**
#### Penyelesaian
* Install apache2 di **PROBOLINGGO** `apt-get install apache2`
* Install php5 di **PROBOLINGGO** `apt-get install php5`
* Pindah ke direktori **/etc/apache2/sites-available** dan copy file **default** ke file **semerut08.pw** `cp /etc/apache2/sites-available/default /etc/apache2/sites-available/semerut08.pw`
* Buka file **semerut08.pw** dan tambahkan konfigurasi seperti dibawah `nano /etc/apache2/sites-available/semerut08.pw`
```
ServerName semerut08.pw
ServerAlias www.semerut08.pw
```
![serversemerut](https://github.com/agung56/Jarkom_Modul2_Lapres_T8/blob/main/img/serversemerut08.png)
* Aktifkan konfigurasi **semerut08.pw** dengan menggunakan perintah `a2ensite semerut08.pw` dan restart apache2 dengan mengetikkan `service apache2 restart`
* Pindah ke directori **/var/www** `cd /var/www`. Lalu unzip file hasil download dari **wget 10.151.36.202/semeru.pw.zip** dan ubah nama menjadi **semerut08.pw**
### 9. Mengaktifkan mod rewrite agar url berubah dari http://semerut08.pw/index.php/home menjadi http://semerut08.pw/home
#### Penyelesaian
* Jalankan perintah `a2enmod rewrite` untuk mengaktifkan *module rewrite*
* Restart apache2 menggunakan perintah `service apache2 restart`
* Pindah ke direktori **/var/www/semerut08.pw** dan buat file **.htaccess** dengan isi file
![htaccess]()
* Kemudian buka file **/etc/apache2/sites-available/semerut08.pw** dan tambahkan konfigurasi berikut
```
<Directory /var/www/semerut08.pw>
     Options +FollowSymLinks -Multiviews
     AllowOverride All
 </Directory>
 ```
 * restart apache2 dengan menggunakan perintah `service apache2 restart`
### 10. Membuat web **http://penanjakan.semerut08.pw** yang memiliki *DocumentRoot* pada **/var/www/penanjakan.semerut08.pw**
#### Penyelesaian
* Pindah ke direktori **/etc/apache2/sites-available** dan copy file **default** ke file **penanjakan.semerut08.pw** `cp /etc/apache2/sites-available/default /etc/apache2/sites-available/penanjakan.semerut08.pw`
* Buka file **penanjakan.semerut08.pw** dan tambahkan konfigurasi seperti dibawah `nano /etc/apache2/sites-available/penanjakan.semerut08.pw`
```
ServerName penanjakan.semerut08.pw
ServerAlias www.penanjakan.semerut08.pw
```
![penanjakansemeru]()<br>
* Aktifkan konfigurasi **penanjakan.semerut08.pw** dengan menggunakan perintah `a2ensite penanjakan.semerut08.pw` dan restart apache2 dengan mengetikkan `service apache2 restart`
* Pindah ke directori **/var/www** `cd /var/www`. Lalu unzip file hasil download dari **wget 10.151.36.202/penanjakan.semeru.pw.zip** dan ubah nama menjadi **penanjakan.semerut08.pw**
### 11. pada folder **/public** dibolehkan *directory listing* namun folder yang ada di dalamnya tidak boleh
#### Penyelesaian
* Tambahkan konfigurasi pada file **/etc/apache2/sites-available/penanjakan.semerut08.pw** seperti dibawah
![penanjakansemeru2]()
* Setelah itu restart apache2 dengan mengetikkan `service apache2 restart`
### 12. Mengganti default error 404 dari Apache menjadi mengarah ke file **404.html** yang ada pada folder **/errors**
#### Penyelesaian
* Pindah ke direktori **/var/www/penanjakan.semerut08.pw** dan buat file **.htaccess** dengan isi file
![htaccesspenanjakan]()
* Kemudian buka file **/etc/apache2/sites-available/penanjakan.semerut08.pw** dan tambahkan 
```
<Directory /var/www/penanjakan.semerut08.pw>
     Options +FollowSymLinks -Multiviews
     AllowOverride All
 </Directory>
```
* Setelah itu restart apache2 dengan mengetikkan `service apache2 restart`
### 13. Membuat alias untuk menyederhanakan url dari http://penanjakan.semerut08.pw/public/javascripts menjadi http://penanjakan.semerut08.pw/js
#### Penyelesaian
* Buka file **/etc/apache2/sites-available/penanjakan.semerut08.pw** dan tambahkan konfigurasi seperti berikut<br>
![alias]()<br>
* Setelah itu restart apache2 dengan mengetikkan `service apache2 restart`
### 14. Mengatur domain **http://naik.gunung.semerut08.pw** pada port 8888. *DocumentRoot* web berada pada **/var/www/naik.gunung.semerut08.pw**
#### Penyelesaian

### 15. Membuat autentikasi web **http://naik.gunung.semerut08.pw** dengan username **"semeru"** dan password **"kuynaikgunung"**
#### Penyelesaian

### 16. Meredirect IP **PROBOLINGGO** menuju ke **http://semerut08.pw**
#### Penyelesaian
* Buka file **/etc/apache2/sites-available/default** dan tambahkan konfigurasi seperti berikut<br>
![redirect]()<br>
* Setelah itu restart apache2 dengan mengetikkan `service apache2 restart`
### 17. Karena pengunjung pada **/var/www/penanjakan.semerut08.pw/public/images** sangat banyak maka semua request gambar yang memiliki substring "semeru" akan diarahkan menuju semeru.jpg
#### Penyelesaian
