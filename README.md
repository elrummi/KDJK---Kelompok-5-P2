# Aplikasi Web "XYZ"


## Sekilas Tentang

Joomla adalah sebuah Content Management System (CMS) open-source yang digunakan untuk membangun dan mengelola situs web secara dinamis. Dikembangkan dengan menggunakan bahasa pemrograman PHP dan database MySQL atau MariaDB, Joomla menawarkan solusi yang fleksibel untuk pengelolaan konten, pembuatan berbagai halaman web, dan penambahan fitur tambahan. Joomla menggunakan sistem modular yang memungkinkan pengguna menambahkan ekstensi berupa komponen, modul, dan plugin untuk memperluas fungsionalitas situs. Ekstensi ini bisa mencakup fitur seperti e-commerce, forum, galeri gambar, hingga optimasi mesin pencari (SEO), membuatnya sangat serbaguna. Sistem template Joomla memungkinkan pengguna untuk mengubah tampilan situs secara dinamis tanpa mempengaruhi konten yang ada, serta mendukung desain responsif untuk perangkat seluler.

Joomla juga memiliki sistem manajemen pengguna yang sangat fleksibel, memungkinkan pengaturan hak akses pengguna pada berbagai tingkatan. Hal ini penting bagi situs yang melibatkan banyak pengguna dengan peran berbeda, seperti situs perusahaan besar atau portal komunitas. Salah satu fitur utamanya adalah dukungan multibahasa secara native, yang memudahkan dalam membuat situs multibahasa tanpa memerlukan ekstensi tambahan. Selain itu, Joomla dilengkapi dengan fitur SEO bawaan seperti URL ramah mesin pencari, pengelolaan metadata, dan pembuatan sitemap, yang membantu meningkatkan visibilitas situs di mesin pencari. Namun, Joomla memiliki kurva pembelajaran yang lebih tinggi dibandingkan dengan CMS lain seperti WordPress, terutama karena antarmuka yang lebih kompleks dan banyaknya opsi kustomisasi yang tersedia.

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
    - Download melalui [Official site Joomla](https://downloads.joomla.org/)
    
13. Unzip file yang didownload menuju ke `/var/www/html/` (sesuaikan nama version Joomla-nya)
    ```
    $ mkdir /var/www/html/joomla
    $ unzip Joomla_4.1.2-Stable-Full_Package.zip -d /var/www/html/joomla
    
14. Set directory ownership dari directory ke Apache user dan ubah permissions
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
      ![1](https://github.com/user-attachments/assets/66c3fee9-1367-4198-b747-dc474a0e9255)
      ![2](https://github.com/user-attachments/assets/44b0fc57-69a3-436b-90a8-47dc1265338d)
          
    - Masukan informasi database yang sudah dibuat diawal
      ![3](https://github.com/user-attachments/assets/88dff6da-8b1e-422f-87a2-4a2af17db361)
      ![4](https://github.com/user-attachments/assets/adcca55e-dab9-425c-964e-4ee7338ce677)
      ![5](https://github.com/user-attachments/assets/3c29c4ab-7f94-4e02-a3f1-fa9a86bee2a6)
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

Beberapa kelebihan yang dimiliki oleh Joomla, diantaranya: 
-Memberikan kontrol penuh kepada pengguna yang menginginkan desain dan fitur yang disesuaikan.
-Memiliki sistem manajemen pengguna yang lebih lengkap dibandingkan dengan CMS lain, sangat cocok untuk situs yang membutuhkan pengaturan akses tingkat lanjut.
-Mendukung multibahasa tanpa memerlukan plugin tambahan, menjadikannya ideal untuk situs yang melayani audiens global.
-Memiliki fleksibelitas untuk membangun situs yang kompleks, seperti portal komunitas, direktori bisnis, atau situs multi-bahasa, berkat sistem pengelolaan pengguna dan ekstensi yang kuat. Ini membuat Joomla cocok untuk pengembang atau perusahaan yang membutuhkan kontrol penuh terhadap desain dan fungsionalitas.
-Memberikan lebih banyak kontrol untuk optimasi SEO melalui fitur bawaan dan ekstensi yang tersedia, memungkinkan pengguna untuk mengoptimalkan situs mereka dengan lebih detail.
-Unggul dalam hal kustomisasi dan fleksibilitas fungsionalitas.

Disamping kelebihan yang dimiliki, beberapa kelemahan yang ada diantaranya, 
- Tidak adanya fitur untuk pembuatan akun pengguna secara mandiri. Pengguna tidak dapat mendaftar sendiri melalui situs, melainkan harus melalui admin, yang bisa menjadi kendala bagi situs yang membutuhkan interaksi pengguna yang tinggi. 
- Tidak ideal untuk situs besar dan kompleks. Masalah kinerja bisa terjadi seperti waktu muat yang lebih lambat dan peningkatan konsumsi sumber daya server. Hal ini dapat mengurangi pengalaman pengguna dan menghambat pengelolaan situs.
- Kurang intuitif dibandingkan dengan beberapa CMS lainnya. Antarmuka pengguna lebih kompleks dan kurang variatif, yang bisa membuatnya sulit dipahami dan digunakan, terutama bagi pemula. 

Dalam perbandingannya dengan Squarespace, perbedaan utama diantara keduanya terletak pada fleksibilitas kustomisasi dan fungsionalitas yang ditawarkan. Joomla menawarkan kustomisasi yang kompleks dan fungsionalitas khusus yang multifaset, membuatnya cocok untuk proyek yang membutuhkan fitur khusus dan struktur situs yang rumit memfasilitasi pengguna untuk eksplor dan menggunakan kreatifitasnya dalam melakukan kustomisasi dan penyesuaian fungsionalitas. 

Di lain sisi, Squarespace dikenal dengan template yang menarik dan kemudahan bagi penggunaannya. Squarespace ideal untuk pengguna yang mencari solusi cepat dan mudah tanpa pengetahuan teknis. 

## Dokumentasi
![WhatsApp Image 2024-10-11 at 23 09 24](https://github.com/user-attachments/assets/c970d3b9-eaf3-412a-a426-f3da12e18a12)
![WhatsApp Image 2024-10-11 at 23 09 30](https://github.com/user-attachments/assets/76d31dfc-029a-41ea-8116-31daae0ecc17)
![Screenshot_2024-09-27_12-55-29](https://github.com/user-attachments/assets/52295df7-0a6a-4cea-a1ae-5984d2de17dc)
![Screenshot_2024-09-27_12-55-07](https://github.com/user-attachments/assets/d3f8749d-ecf4-4ad5-94c3-55b557b5824b)
![Screenshot_2024-09-27_12-54-43](https://github.com/user-attachments/assets/00f8cdec-6afc-4579-9db0-d520c0267328)
![Screenshot_2024-09-27_12-54-24](https://github.com/user-attachments/assets/1f78160b-c4de-47c8-9c14-63214b3fb928)
![Screenshot_2024-09-27_12-54-08](https://github.com/user-attachments/assets/02d505aa-76df-48c8-9d79-ab2ca223034b)
![Screenshot_2024-09-27_12-53-40](https://github.com/user-attachments/assets/cb88ff20-0532-45c9-89cb-43ae8c7d6b79)
![Screenshot_2024-09-27_12-51-08](https://github.com/user-attachments/assets/dd5fc0c1-e5f4-46a2-b348-c0c343613183)
![Screenshot_2024-09-27_14-01-46](https://github.com/user-attachments/assets/ade8f574-d9c5-4ce5-8398-ea6a043490d9)
![Screenshot_2024-09-27_14-01-40](https://github.com/user-attachments/assets/45cab72f-614e-4b11-a2ae-fd54d4723528)
![Screenshot_2024-09-27_14-01-18](https://github.com/user-attachments/assets/5fc6acb5-2e71-4cf4-b7bc-7c1c7722d7ed)
![Screenshot_2024-09-27_14-01-01](https://github.com/user-attachments/assets/297d500c-f019-431e-b6a7-cba9348fee77)
![Screenshot_2024-09-27_12-57-22](https://github.com/user-attachments/assets/2d1cd17c-997c-4b36-900a-f70e913928b8)
![Screenshot_2024-09-27_12-56-58](https://github.com/user-attachments/assets/eabf7fdf-737e-49a3-a9d4-1173d5cc70bd)
![Screenshot_2024-09-27_12-56-16](https://github.com/user-attachments/assets/09c7094d-3e24-4682-a705-ccb9d49dde7a)
![Screenshot_2024-09-27_12-55-58](https://github.com/user-attachments/assets/a3d27f24-d88e-4749-b3cb-b2d8942747b8)



## Referensi
- [https://wiki.crowncloud.net/How_To_Install_Duf_On_Ubuntu_22_04?How_to_Install_Joomla_On_Ubuntu_22_04](https://wiki.crowncloud.net/How_To_Install_Duf_On_Ubuntu_22_04?How_to_Install_Joomla_On_Ubuntu_22_04)
- [https://fastdot.com/web-hosting-faq/joomla-strengths-weaknesses/#What_Are_the_Weaknesses_of_Joomla](https://fastdot.com/web-hosting-faq/joomla-strengths-weaknesses/#What_Are_the_Weaknesses_of_Joomla)
- https://www.biznetgio.com/news/apa-itu-joomla
- https://idcloudhost.com/blog/cmas-joomla/
