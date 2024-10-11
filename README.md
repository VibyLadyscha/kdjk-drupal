<h1 align="center"><img src="https://github.com/user-attachments/assets/293d495a-bfad-4230-bf63-7b00e357058f"></h1>

| [Sekilas Tentang](#sekilas-tentang) |  [Instalasi](#instalasi)  | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) |  [Cara Pemakaian](#cara-pemakaian)  | [Pembahasan](#pembahasan) | [Referensi](#referensi) |
|:-----|:--------:|------:|:-----|:--------:|------:|------:|

# Sekilas Tentang

**Drupal** adalah *content management system* (CMS) sumber terbuka dan gratis yang ditulis dalam `PHP` dan didistribusikan di bawah Lisensi Publik Umum GNU. Drupal menyediakan **kerangka kerja back-end** secara *open source* untuk setidaknya 14% dari 10.000 situs web teratas di seluruh dunia dan 1,2% dari 10 juta situs web teratas—mulai dari blog pribadi hingga situs perusahaan, politik, dan pemerintah. Drupal juga dapat digunakan untuk **manajemen pengetahuan** dan untuk **kolaborasi bisnis**.

# Instalasi

### Kebutuhan Sistem :
- Linux CLI.
- Apache Web server 2.4.62+.
- PHP 8.2.23+.
- MariaDB 11.4.3+.
- RAM minimal 100 Mb.
  
### Langkah Instalasi :
1. Login ke dalam perangkat sistem operasi yang akan digunakan.

2. Pastikan seluruh paket sistem kita *up-to-date*, dan *install* seluruh kebutuhan sisrem seperti `Apache`, `MariaDB`, dan `PHP`.
   ```
   $ sudo apt update
   $ sudo apt upgrade -y
   $ sudo apt-get install apache2 mariadb-server mariadb-client curl
   $ sudo apt install php php-mysql php-cli php-json php-opcache php-gd php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
   ```

3. Konfigurasi ke MySQL database.
   ```
   $ sudo su
   $ mysql_secure_installation
   ```

4. Tekan enter untuk login sebagai root.
   <h1 align="center"><img src="https://github.com/user-attachments/assets/1e6d6927-1e80-4af6-bdd9-f20542ea596e"></h1>

5. Tuliskan `Y` dan tekan enter untuk membuat password root, masukkan password baru sebanyak dua kali untuk konfirmasi.
<h1 align="center"><img src="https://github.com/user-attachments/assets/bccab3cc-3a4e-4e28-b28b-c66a95d9d495"></h1>

6. Tuliskan `Y` dan tekan enter untuk menghapus pengguna anonim.
   <h1 align="center"><img src="https://github.com/user-attachments/assets/b9129446-4162-489f-bb77-b532099a7c68"></h1>

7. Tuliskan `Y` dan tekan enter untuk tidak memperbolehkan *root login remotely*.
<h1 align="center"><img src="https://github.com/user-attachments/assets/227b05e5-1c1e-4d77-b391-50df733e90da"></h1>

8. Tuliskan `Y` dan tekan enter untuk menghapus database test.
<h1 align="center"><img src="https://github.com/user-attachments/assets/3b6e4a38-0275-4343-9fa0-f5a5a3e0bdaf"></h1>

9. Tuliskan `Y` dan tekan enter untuk *reload* tabel *privilege*
<h1 align="center"><img src="https://github.com/user-attachments/assets/df901f23-e0a6-4d98-97a6-1692cedeea3f"></h1>

10. Login ke MySQL dan lakukan autentikasi dengan password yang telah dibuat.
    ```
    $ mysql -u root -p
    ```

11. Buat database dan user untuk **Drupal**.
    ```
    CREATE DATABASE drupal DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
    GRANT ALL ON drupal.* TO 'drupal_rw'@'localhost' IDENTIFIED BY 'Dru4@l!!';
    FLUSH PRIVILEGES;
    EXIT;
    exit
    ```
    
12. Unduh **Drupal** ke dalam direktori kita.
    ```
    $ sudo wget -O drupal.tar.gz https://www.drupal.org/download-latest/tar.gz
    ```
    
13. Ekstrak file yang telah diunduh ke dalam direktori yang kita inginkan dan ubah folder **Drupal**.
    ```
    $ sudo tar xzvf drupal.tar.gz --directory /var/www
    $ sudo mv /var/www/drupal* /var/www/drupal
    ```
    
14. Konfigurasi Apache web server
    ```
    $ sudo nano /etc/apache2/sites-available/drupal.conf

    Alias /drupal "/var/www/drupal/"
    <Directory /var/www/drupal/>
      AllowOverride All
    </Directory>
    ```

15. Aktifkan situs **Drupal** dan modul PHP yang diperlukan.
    ```
    $ sudo a2ensite drupal
    $ sudo a2enmod rewrite
    $ sudo chown -R www-data:www-data /var/www/drupal
    $ sudo systemctl restart apache2
    ```

16. Kunjungi alamat `localhost/drupal` untuk meneruskan instalasi.
    - Pilih Bahasa yang akan digunakan
      <h1 align="center"><img src="https://github.com/user-attachments/assets/9f74f634-32aa-43e7-9157-22fee686c49f"></h1>
    - Pilih profil instalasi yang akan digunakan
      <h1 align="center"><img src="https://github.com/user-attachments/assets/57a86470-9e5b-453c-944f-d1c0a40e08d0"></h1>
    - Verifikasi **requirements** yang dimiliki. Gulir ke bawah dan pilih opsi `continue anyway`
    - Set up database dengan memasukkan nama database, username, dan password database. Pilih `save an continue` 
    - Tunggu proses instalasi hingga selesai
    - Konfigurasi site. Setelah semuanya terisi, pilih `save and continue`
      <h1 align="center"><img src="https://github.com/user-attachments/assets/c089d340-c5ba-4fa3-8d87-2d8f547490fa"></h1>

# Konfigurasi

Setting server tambahan yang diperlukan untuk meningkatkan fungsi dan kinerja aplikasi, misalnya:
- batas upload file
- batas memori
- dll

Plugin untuk fungsi tambahan
- login dengan Google/Facebook
- editor Markdown
- dll


#  Maintenance

Setting tambahan untuk maintenance secara periodik, misalnya:
- buat backup database tiap pekan
- hapus direktori sampah tiap hari
- dll


# Otomatisasi 

Skrip shell untuk otomatisasi instalasi, konfigurasi, dan maintenance.


# Cara Pemakaian

- Tampilan aplikasi web
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


# Pembahasan

- Pendapat anda tentang aplikasi web ini
    - kelebihan
    - kekurangan
- Bandingkan dengan aplikasi web lain yang sejenis


# Referensi
- Wikipedia https://en.wikipedia.org/wiki/Drupal
- Situs Drupal https://www.drupal.org/

Cantumkan tiap sumber informasi yang anda pakai.
