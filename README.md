# Jarkom_Modul2_Lapres_T8
#### Anggota Kelompok:
1. Kadek Nesya Kurniadewi (05311840000009)
2. Agung Mulyono (05311840000035)

Soal Shift Modul2 https://drive.google.com/drive/folders/1Gb90AYZSb-qw38avjn2eKAPxouR3fS8a

#### Membuat Topologi Jaringan
Sintaks file **topologi.sh**

* Setelah membuat file **topologi.sh**, kemudian bash file tersebut dengan perintah `bash topologi.sh`
* Memastikan semua UML yang dibuat berfungsi dengan baik dan login di tiap UML-nya
* Kemudian hilangkan tanda pagar (#) pada bagian `net.ipv4.ip_forward=1` dengan perintah `nano /etc/sysctl.conf` pada router **SURABAYA**. Lalu ketikkan `sysctl -p` untuk mengaktifkan perubahan yang ada.
* Setting IP pada setiap UML dengan mengetikkan `nano /etc/network/interfaces`
* Restart network pada semua UML dengan mengetikkan `service networking restart`
* Agar UML selain **SURABAYA** bisa melakukan koneksi ke jaringan luar, maka ketikkan `iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16`

#### Soal dan Penyelesaian
1. Membuat domain utama dengan alamat **http://semerut08.pw**
#### Penyelesaian

2. Membuat alias **http://www.semerut08.pw**
#### Penyelesaian

3. Membuat subdomain **http://penanjakan.semerut08.pw** yang diatur DNS-nya pada **MALANG** dan mengarah ke IP Server **PROBOLINGGO**
#### Penyelesaian

4. Membuat reverse domain untuk domain utama
#### Penyelesaian

5. Membuat DNS Server Slave pada **MOJOKERTO**
#### Penyelesaian

6. Membuat subdomain dengan alamat **http://gunung.semerut08.pw** yang didelegasikan pada server **MOJOKERTO** dan mengarah ke IP Server **PROBOLINGGO**
#### Penyelesaian

7. Membuat subdomain **http://naik.gunung.semerut08.pw**, domain diarahkan ke IP Server **PROBOLINGGO**
#### Penyelesaian

8. Mengatur web server dengan domain **http://semerut08.pw** memiliki *DocumentRoot* pada **/var/www/semerut08.pw**
#### Penyelesaian

9. Mengaktifkan mod rewrite agar url berubah dari **http://semerut08.pw/index.php/home** menjadi **http://semerut08.pw/home**
#### Penyelesaian

10. Membuat web **http://penanjakan.semerut08.pw** yang memiliki *DocumentRoot* pada **/var/www/penanjakan.semerut08.pw**
#### Penyelesaian

11. pada folder **/public** dibolehkan *directory listing* namun folder yang ada di dalamnya tidak boleh
#### Penyelesaian

12. Mengganti default error 404 dari Apache menjadi mengarah ke file **404.html** yang ada pada folder **/errors**
#### Penyelesaian

13. Membuat alias untuk menyederhanakan url dari **http://penanjakan.semerut08.pw/public/javascripts** menjadi
**http://penanjakan.semerut08.pw/js**
#### Penyelesaian

14. Mengatur domain **http://naik.gunung.semerut08.pw** pada port 8888. *DocumentRoot* web berada pada **/var/www/naik.gunung.semerut08.pw**
#### Penyelesaian

15. Membuat autentikasi web **http://naik.gunung.semerut08.pw** dengan username **"semeru"** dan password **"kuynaikgunung"**
#### Penyelesaian

16. Meredirect **IP PROBOLINGGO** menuju ke **http://semerut08.pw**
#### Penyelesaian

17. Karena pengunjung pada **/var/www/penanjakan.semerut08.pw/public/images** sangat banyak maka semua request gambar yang memiliki substring "semeru" akan diarahkan menuju semeru.jpg
#### Penyelesaian
