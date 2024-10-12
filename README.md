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
