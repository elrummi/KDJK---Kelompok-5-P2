# Aplikasi Web "XYZ"


## Sekilas Tentang

Deskripsi singkat tentang aplikasi tsb.


## Instalasi

**Kebutuhan Sistem :**
- Windows / Linux / Ubuntu.
- Apache Web server.
- PHP.
- MySQL.

#### Proses Instalasi :

1. Pastikan seluruh paket sistem kita sudah ter _update_, dan install seluruh kebutuhan sistem seperti `Apache`, `PHP`, dan `MySQL`.
    ```
    $ sudo apt update
    $ sudo apt upgrade
    $ sudo apt install apache2 libapache2-mod-php openssl php-imagick php-gd php-imap php-intl php-json php-ldap php-mbstring php-mysql php-pgsql php-smbclient php-ssh2 php-sqlite3 php-xml php-zip
    ```

2. Verifikasi versi `Apache` yang telah terinstall.
    ```
    $ apache2 -version
    ```
    Output :
   ```
    root@crown:~# apache2 -version
    Server version: Apache/2.4.52 (Ubuntu)
    Server built:   2022-03-25T00:35:40
    ```

3. Start dan enable Apache web server.
    ```
    $ systemctl start apache2
    $ systemctl enable apache2 
    ```

4. Verifikasi status Apache.
    ```
    $ systemctl status apache2
    ```
    Output :
   ```
   root@crown:~# systemctl status apache2
    ● apache2.service - The Apache HTTP Server
         Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
         Active: active (running) since Fri 2022-04-08 18:34:36 UTC; 2h 21min ago
           Docs: https://httpd.apache.org/docs/2.4/
       Main PID: 659 (apache2)
          Tasks: 7 (limit: 1034)
         Memory: 14.0M
            CPU: 669ms
         CGroup: /system.slice/apache2.service
                 ├─ 659 /usr/sbin/apache2 -k start
                 ├─ 680 /usr/sbin/apache2 -k start
                 ├─ 681 /usr/sbin/apache2 -k start
                 ├─ 682 /usr/sbin/apache2 -k start
                 ├─ 690 /usr/sbin/apache2 -k start
                 ├─ 691 /usr/sbin/apache2 -k start
                 └─1603 /usr/sbin/apache2 -k start
   ```

5. Verifikasi PHP.
    ```
    $ php -v
    ```
    Output:
   ```
   root@crown:~# php -v
    PHP 8.1.4 (cli) (built: Apr  4 2022 13:36:22) (NTS)
    Copyright (c) The PHP Group
    Zend Engine v4.1.4, Copyright (c) Zend Technologies
        with Zend OPcache v8.1.4, Copyright (c), by Zend Technologies
   ```

6. Install `MariaDB`.
    ```
    $ apt install mariadb-server
    ```

9. MariaDB secara default tidak secure, maka akan kita secure database engine nya.
    ```
    $ mysql_secure_installation
    ```
10. Membuat database Joomla (sesuaikan masing-masing)
    ```
    $ mysql -u root -p
    ```
    ```
    MariaDB [(none)]> CREATE DATABASE joomla;
    MariaDB [(none)]> GRANT ALL PRIVILEGES ON joomla.* TO 'joomla'@'localhost' IDENTIFIED BY  'StrongPassword';
    MariaDB [(none)]> FLUSH PRIVILEGES;
    MariaDB [(none)]> EXIT;
    ```
11. Download **Joomla**.
        Download melalui [Official site Joomla](https://downloads.joomla.org/)
    
13. Unzip file yang didownload menuju ke `/var/www/html/` (sesuaikan nama version Joomla-nya)
    ```
    $ mkdir /var/www/html/joomla
    $ unzip Joomla_4.1.2-Stable-Full_Package.zip -d /var/www/html/joomla
    
14. Set directory ownership dari directory ke Apache user dan ubah peermissions
    ```
    $ chown -R www-data:www-data /var/www/html/joomla
    $ chmod -R 755 /var/www/html/joomla
    ```
15. Restart Apache web server
    ```
    $ systemctl restart apache2
    ```
16. Membuat virtual host file untuk Joomla
    ```
    $ nano /etc/apache2/sites-available/joomla.conf
    ```
17. Tambahkan ini ke file yang sudah ada (ganti "example.com dengan domain name yang asli)
    ```
    <VirtualHost *:80>
     ServerAdmin admin@example.com
     DocumentRoot /var/www/html/joomla/
     ServerName example.com
     ServerAlias www.example.com
    
     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined
    
     <Directory /var/www/html/joomla/>
            Options FollowSymlinks
            AllowOverride All
            Require all granted
     </Directory>
    </VirtualHost>
    ```
18. Enable virtual host file
    ```
    $ a2ensite joomla.conf
    $ a2enmod rewrite
    ```
19. Restart apache web server
    ```
    $ systemctl restart apache2
    ```
20. Install `snapd`
    ```
    $ apt install snapd
    ```
21. Cek apakah `snapd` sudah terupdate
    ```
    $ snapd install; sudo snap resresh core
    ```
22. Install `Certbot`
    ```
    $ snap install --classic certbot
    $ ln -s /snap/bin/certbot /usr/bin/certbot
    $ certbot --apache
    ```
23. Konfigurasi Joomla
    - Di browser kita akan mengatur Site name dan memasukan data data seperti Username, User Account, Super User         Password, and Email Address, setelah itui click tombol Setup Database Connection.
    - Masukan informasi database yang sudah dibuat diawal
    - Masukan username dan password yang sudah di atur sebelumnya
    - Cek databasenya
## Cara Pemakaian

- Tampilan aplikasi web
- Tampilan admin aplikasi web
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


## Pembahasan

- Pendapat anda tentang aplikasi web ini
    - kelebihan
    - kekurangan
- Bandingkan dengan aplikasi web lain yang sejenis

Disamping kelebihan yang dimiliki, beberapa kelemahan yang ada diantaranya, 
- Tidak adanya fitur untuk pembuatan akun pengguna secara mandiri. Pengguna tidak dapat mendaftar sendiri melalui situs, melainkan harus melalui admin, yang bisa menjadi kendala bagi situs yang membutuhkan interaksi pengguna yang tinggi. 
- Tidak ideal untuk situs besar dan kompleks. Masalah kinerja bisa terjadi seperti waktu muat yang lebih lambat dan peningkatan konsumsi sumber daya server. Hal ini dapat mengurangi pengalaman pengguna dan menghambat pengelolaan situs.
- Kurang intuitif dibandingkan dengan beberapa CMS lainnya. Antarmuka pengguna lebih kompleks dan kurang variatif, yang bisa membuatnya sulit dipahami dan digunakan, terutama bagi pemula. 

Dalam perbandingannya dengan Squarespace, perbedaan utama diantara keduanya terletak pada fleksibilitas kustomisasi dan fungsionalitas yang ditawarkan. Joomla menawarkan kustomisasi yang kompleks dan fungsionalitas khusus yang multifaset, membuatnya cocok untuk proyek yang membutuhkan fitur khusus dan struktur situs yang rumit memfasilitasi pengguna untuk eksplor dan menggunakan kreatifitasnya dalam melakukan kustomisasi dan penyesuaian fungsionalitas. 

Di lain sisi, Squarespace dikenal dengan template yang menarik dan kemudahan bagi penggunaannya. Squarespace ideal untuk pengguna yang mencari solusi cepat dan mudah tanpa pengetahuan teknis. 


## Referensi

Cantumkan tiap sumber informasi yang anda pakai.

[Pembahasan](https://fastdot.com/web-hosting-faq/joomla-strengths-weaknesses/#What_Are_the_Weaknesses_of_Joomla)
