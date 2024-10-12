# Aplikasi Web "XYZ"


## Sekilas Tentang

Deskripsi singkat tentang aplikasi tsb.


## Instalasi
[`^ kembali ke atas ^`](#)
    **Kebutuhan Sistem :**
        - Windows / Linux / Ubuntu
        - Apache Web server
        - PHP
        - MySQL

#### Proses Instalasi :
1. Login kedalam server menggunakan SSH. Untuk pengguna windows bisa menggunakan aplikasi [PuTTY](http://www.putty.org/).
    ```
    $ ssh adam@172.18.88.88 -p 22
    ```

2. Pastikan seluruh paket sistem kita *up-to-date*, dan install seluruh kebutuhan sisrem seperti `Apache`, `PHP`, dan `MySQL`.
    ```
    $ sudo apt-get update
    $ sudo apt-get install apache2
    $ sudo apt-get install mysql-server
    $ sudo apt-get install php
    $ sudo apt-get install libapache2-mod-php
    $ sudo apt-get install php-mysql
    $ sudo apt-get install php-gd php-mcrypt php-mbstring php-xml php-ssh2 php-curl php-zip php-intl
    $ sudo apt-get install unzip
    ```

3. Unduh **Prestashop** ke dalam direktori kita. 
    ```
    $ wget https://download.prestashop.com/download/releases/prestashop_1.7.0.5.zip
    ```

4. Ekstrak file yang telah diunduh ke dalam direktori yang kita inginkan.
    ```
    $ sudo unzip prestashop_1.7.0.5.zip -d /var/www/html/prestashop
    ```

5. Ubah otorisasi kepemilikan ke user www-data (webserver)
    ```
    $ sudo chown -R www-data:www-data /var/www/html/prestashop
    ```

6. Buat database dan user untuk **Prestashop**.
    ```
    $ mysql -u root -p -v -e "
        CREATE DATABASE prestashop;
        CREATE USER 'prestashopuser'@'localhost' IDENTIFIED BY 'prestashoppassword';
        GRANT ALL PRIVILEGES ON `prestashop`.* TO 'prestashopuser'@'localhost';
        FLUSH PRIVILEGES;"
    ```

7. Konfigurasi Apache web server.
    ```
    $ sudo a2enmod rewrite
    $ sudo touch /etc/apache2/sites-available/prestashop.conf
    $ sudo ln -s /etc/apache2/sites-available/prestashop.conf /etc/apache2/sites-enabled/prestashop.conf
    $ sudo nano /etc/apache2/sites-available/prestashop.conf

    <VirtualHost *:80>
    ServerAdmin admin@your-domain.com
    DocumentRoot /var/www/html/prestashop/
    ServerName your-domain.com
    ServerAlias www.your-domain.com
    <Directory /var/www/html/prestashop/>
    Options FollowSymLinks
    AllowOverride All
    Order allow,deny
    allow from all
    </Directory>
    ErrorLog /var/log/apache2/your-domain.com-error_log
    CustomLog /var/log/apache2/your-domain.com-access_log common
    </VirtualHost>
    ```

8. Edit file `etc/php/7.0/apache2/php.ini` dan tambahkan baris berikut :
    ```
    memory_limit = 128M
    upload_max_filesize = 16M
    max_execution_time = 60
    file_uploads = On
    allow_url_fopen = On
    magic_quotes_gpc = Off
    register_globals = Off
    ```

9. Restart kembali Apache web server.
    ```
    $ sudo service apache2 restart
    ```

10. Kunjungi alamat IP web server kita untuk meneruskan instalasi.
    - Pilih Bahasa yang akan digunakan

      ![1](https://4.bp.blogspot.com/-4Bd2ScecDIs/WNfZ0H8j3UI/AAAAAAAAGjE/9f7Knlqzgw0a0Lgd2AVQ7Qt53bI-Of8bACLcB/s1600/36.PNG)

    - Setujui persyaratan yang berlaku

      ![2](https://4.bp.blogspot.com/-mglU1XDt-T0/WNfZ0OJ7n8I/AAAAAAAAGjI/bG23YpPUkyEOCiozy1_Qc4TnA29bJw0lACLcB/s1600/37.PNG)

    - Cek kecocokan sistem

      ![3](https://3.bp.blogspot.com/-ewzlTX1qtmw/WNfZ0HTeFuI/AAAAAAAAGjM/edNiBt1f24Qt4x4sWCoCHfyo7JXWWmoZwCLcB/s1600/38.PNG)

    - Isi informasi tentang toko yang kita buat

      ![4](https://2.bp.blogspot.com/-Q5cCz5hyubQ/WNfZ1FZod9I/AAAAAAAAGjU/H_uUfxtZLUE11VPDafwK8jR3-aealPKcgCLcB/s1600/39.png)

    - Konfigurasi database

      ![5](https://1.bp.blogspot.com/-rh08nNV2Leg/WNfZ1DAaDOI/AAAAAAAAGjY/R5oIKIMI4rYjg7gO71MgR26JSMahxtpxgCLcB/s1600/40.PNG)

    - Lanjutkan proses instalasi

      ![6](https://3.bp.blogspot.com/-t2MrsQBYXBU/WNfZ0x4YoWI/AAAAAAAAGjQ/zOqZVNSFIpQkQjY0awofbetdEowQLdGAwCLcB/s1600/41.PNG)

11. Setelah proses instalasi selesai hapus direktori install untuk alasan keamanan.
    ```
    $ sudo rm -rf /var/www/html/prestashop/install
    ```



- Prasyarat, apa saja yang harus diinstal sebelumnya.
- Langkah instalasi dalam CLI.


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


## Referensi

Cantumkan tiap sumber informasi yang anda pakai.
