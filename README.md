<h1 align="center"><img src="https://github.com/user-attachments/assets/293d495a-bfad-4230-bf63-7b00e357058f"></h1>

| [Sekilas Tentang](#sekilas-tentang) |  [Instalasi](#instalasi)  | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) |  [Cara Pemakaian](#cara-pemakaian)  | [Pembahasan](#pembahasan) | [Referensi](#referensi) |
|:-----|:--------:|------:|:-----|:--------:|------:|------:|

<details open><summary> 
  
  # Sekilas Tentang
</summary>


**Drupal** adalah *Content Management System* (CMS) sumber terbuka dan gratis yang ditulis dalam `PHP` dan didistribusikan di bawah Lisensi Publik Umum GNU. Drupal menyediakan **kerangka kerja back-end** secara *open source* untuk setidaknya 14% dari 10.000 situs web teratas di seluruh dunia dan 1,2% dari 10 juta situs web teratas, mulai dari blog pribadi hingga situs perusahaan, politik, dan pemerintah. Drupal juga dapat digunakan untuk **manajemen pengetahuan** dan untuk **kolaborasi bisnis**.

</details>

<details><summary> 
  
  # Instalasi 
</summary>

<details><summary> 
  
  ### Kebutuhan Sistem 
</summary>
  
- Linux CLI.
- Apache Web server 2.4.62+.
- PHP 8.2.23+.
- MariaDB 11.4.3+.
- RAM minimal 100 Mb.
- Web Hosting (Localtonet.com)

</details>
  
<details><summary> 
  
  ### Langkah Instalasi 
</summary>
  
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

16. Kunjungi alamat http://localhost/drupal untuk meneruskan instalasi.
    - Pilih Bahasa yang akan digunakan
      <h1 align="center"><img src="https://github.com/user-attachments/assets/d95fad83-1598-4f55-a641-334675c3424a"></h1>
    - Pilih profil instalasi yang akan digunakan
      <h1 align="center"><img src="https://github.com/user-attachments/assets/2457f376-d707-4688-99da-d0ba593c1f60"></h1>
    - Verifikasi *requirements* yang dimiliki. Gulir ke bawah dan pilih opsi `continue anyway`
      <h1 align="center"><img src="https://github.com/user-attachments/assets/1c82a48f-c343-4978-99ad-cb35b1d96044"></h1>
      <h1 align="center"><img src="https://github.com/user-attachments/assets/fd704062-a3a0-452a-8a8d-8df40e4f6dd1"></h1>
    - Set up database dengan memasukkan nama database, username, dan password database. Pilih `save an continue`
      <h1 align="center"><img src="https://github.com/user-attachments/assets/28c7e8a2-1fae-40e8-b6bf-f5256735ae0b"></h1>
    - Tunggu proses instalasi hingga selesai
      <h1 align="center"><img src="https://github.com/user-attachments/assets/72de69e0-20e0-4f97-84fe-4fd8b11173d6"></h1>
    - Konfigurasi site. Setelah semuanya terisi, pilih `save and continue`
      <h1 align="center"><img src="https://github.com/user-attachments/assets/c38b3c2f-e7c5-416f-9487-7c4dbcbddc4c"></h1>
      <h1 align="center"><img src="https://github.com/user-attachments/assets/d58b57ef-bacd-48ec-a1e3-50c7b15cbd31"></h1>
      
17. Jika berhasil akan muncul tampilan seperti ini.
    <h1 align="center"><img src="https://github.com/user-attachments/assets/1c509c98-ca2c-4de4-9d5b-2d0510859cae"></h1>

</details>

<details><summary> 

  ### Hosting 
</summary>

1. Kunjungi situs web https://localtonet.com.
2. Sign up dan masukkan email untuk melakukan registrasi akun. Jika sudah memiliki akun, bisa langsung sign in.
    <h1 align="center"><img src="https://github.com/user-attachments/assets/7a8aec40-0af0-41e5-b8da-f05a2ab62e77"></h1>
3. Masuk ke submenu `HTTP` pada menu `My Tunnels` untuk membuat server.
    <h1 align="center"><img src="https://github.com/user-attachments/assets/068c1e03-d426-4c1a-aa75-87289a03e6a8"></h1>
4. Sesuaikan port localhost tempat untuk menyimpan **Drupal** (port 80), kemudian pilih create.
    <h1 align="center"><img src="https://github.com/user-attachments/assets/89d894ea-ef4b-4e2d-8253-576e5806992b"></h1>
5. Pilih tombol start untuk menjalankan server yang telah dibuat.
    <h1 align="center"><img src="https://github.com/user-attachments/assets/de9b6717-eb91-47d4-96a9-e9c3022e1d93"></h1>
6. Install localtonet sesuai sistem operasi yang digunakan sebagai server.
   ```
   $ wget https://localtonet.com/download/localtonet-linux-x64.zip
   $ unzip localtonet-linux-x64.zip
   $ chmod 777 ./localtonet
   ```
7. Kembali ke web localtonet, masuk ke menu `Dashboard` dan copy authtoken yang diberikan.
     <h1 align="center"><img src="https://github.com/user-attachments/assets/e2c4453c-81d8-407e-8482-a966a592a3d9"></h1>
8. Jalankan server dan masukkan authtoken.
   ```
    $ ./localtonet authtoken PASTE_HERE_COPIED_AUTHTOKEN
   ```
9. Tunggu proses status dari `connecting` hingga berubah menjadi `OK`.
10. Mengaktifkan **Drupal** pada komputer server.

    Sekarang server sudah berjalan melalui komputer server (Linux). Server akan tetap berjalan selama komputer servernya menyala.
12. Akses aplikasi yang telah dihosting menggunakan link yang telah dibuatkan secara otomatis ketika membuat server.

</details>

</details>

<details><summary> 
  
  # Konfigurasi
</summary>

- Jika kita masuk ke submenu `Configuration` pada menu `Manage`, kita dapat mengatur konfigurasi umum.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/137ec895-3c7d-488f-a807-8501ef2cf65d"></h1>
  <h1 align="center"><img src="https://github.com/user-attachments/assets/c8a89094-0b97-4de2-a357-e8ac576da952"></h1>
  
  - Kita dapat mengatur cache dan optimasi bandwidth dengan memilih opsi `Performance`.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/5d140670-1fff-4dc2-853c-58226e431858"></h1>
  
  - Kita dapat mengatur ukuran default gambar yang ditampilkan pada aplikasi dengan memilih opsi `Image Styles` kemudian edit.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/684a9caa-b608-4a7e-a04e-89604a701b68"></h1>

- Jika kita masuk ke submenu `Extend` pada menu `Manage`, kita dapat menambahkan fitur atau modul-modul tertentu sesuai yang dibutuhkan untuk melengkapi aplikasi.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/71b6e6a7-5369-44c6-9c59-051c83735c86"></h1>
  
- Jika kita masuk ke submenu `Appearance` pada menu `Manage`, kita dapat menerapkan berbagai macam tema aplikasi Untuk memperindah aplikasi.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/649a0f2b-48c3-4a42-814c-edc4dfc792e2"></h1>

- Jika kita masuk ke submenu `People` pada menu `Manage`, kita dapat mengatur batas akses aplikasi sesuai dengan role pengguna (anonymous, konten editor, admin).
  <h1 align="center"><img src="https://github.com/user-attachments/assets/ce42de4f-add0-4ec0-9b29-6d14535206a3"></h1>

</details>

<details><summary> 
  
  #  Maintenance
</summary>

Ketika ingin memodifikasi aplikasi yang sudah terinstall, kita mungkin tidak ingin ada orang lain yang membuka aplikasi kita. Pada saat seperti itu, kita dapat mengatur konfigurasi aplikasi kita untuk masuk ke dalam `maintenance mode`. Berikut langkah-langkah yang harus kita:
1. Login dengan akun administrator yang telah dibuat.
  
2. Masuk ke submenu `Configuration` pada menu `Manage`.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/80207d92-97ee-42ae-8c6e-26de1191f191"></h1>

3. Gulir ke bawah hingga menemukan opsi `Maintenance Mode`.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/ed0877b4-187f-4ede-9f42-8d70899ade9d"></h1>

4. Masuk ke menu `Maintenance Mode` dan centang kotak untuk mengubah status aplikasi menjadi maintenance mode. Kita juga dapat menyesuaikan pesan yang akan ditampilkan selama aplikasi sedang dalam maintenance mode.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/e699624b-1c50-45b2-a9f5-66c9e0959097"></h1>

5. Pilih `Save configuration` untuk menyimpan perubahan.

</details>

<details><summary> 
  
  # Otomatisasi  
</summary>

Jika masih kesulitan dalam meng-install **Drupal**, terdapat dua cara alternatif yang lebih mudah. Yaitu dengan menggunakan script shell yang otomatis akan menjalankan semua perintah instalasi pada terminal, atau dengan menggunakan layanan yang tersedia pada web-hosting provider. Dengan layanan tersebut kita hanya perlu mencari aplikasi yang dituju, kemudian klik untuk meng-installnya. Web-hosting provider yang menyediakan script instalasi **Drupal** secara otomatis diantaranya:
- [Freehostia](https://www.freehostia.com/free-cloud-hosting/)
- [Installatron](https://installatron.com/apps)
- [Softaculous](https://www.softaculous.com/apps/cms/Drupal)

Sebagai contoh, kita akan menggunakan layanan dari `Installatron`.
1. Kunjungi link tersebut kemudian cari aplikasi **Drupal** untuk di-install.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/61695fb8-4f17-4323-ae67-e58083520865"></h1>

2. Selanjutnya, klik tombol `Install this Application`.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/7fef6f52-60d3-4f1e-b267-43ca7e19a4df"></h1>

3. Isi semua informasi yang dibutuhkan, lalu klik tombol `Install`.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/e8b72617-99a3-4e34-9aab-767f03b187dd"></h1>

4. Tunggu hingga proses instalasi selesai.

</details>

<details><summary> 
  
  # Cara Pemakaian 
</summary>

Cara pemakaian CMS **Drupal** ini sangat mudah dan fleksibel. Dapat digunakan untuk membuat, mengelola, dan mempublikasikan berbagai jenis konten di website, mulai dari blog pribadi hingga situs perusahaan besar, organisasi pemerintahan, dan portal komunitas. Dalam hal akses aplikasi, Admin memiliki kendali penuh, mulai dari pengelolaan konten, manajemen pengguna, hingga pengaturan keamanan. Admin bertanggung jawab untuk mengatur izin pengguna, mengonfigurasi modul, tema, dan memastikan situs berjalan dengan aman serta efisien. Sedangkan pengguna biasa hanya memiliki akses yang terbatas, hanya pada pembuatan dan pengelolaan konten mereka sendiri. Pengguna tidak dapat mengubah pengaturan situs atau mengelola pengguna lain, melainkan hanya berinteraksi dengan bagian-bagian situs yang sudah diatur oleh Admin. 

<details><summary> 
  
  ## Pemakaian sebagai Administrator
</summary>

- Pertama-tama Admin harus `Login` terlebih dahulu.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/9c66a544-ccc3-4e07-8db6-bb6268998857"></h1>
  <h1 align="center"><img src="https://github.com/user-attachments/assets/a7c93927-5eff-442a-a0a8-9d172df4033d"></h1>

- Admin memiliki akses penuh ke seluruh fitur yang ada di aplikasi **Drupal**, antara lain sebagai berikut.
  - Content: Mengelola semua konten yang dibuat di situs, seperti artikel, halaman, dan media.
  - Structure: Mengelola struktur situs web, seperti blok, jenis konten, menu, taksonomi, dan formulir.
  - Appearance: Mengelola tema situs web, mengaktifkan, menonaktifkan, atau mengonfigurasi tema yang diinstal.
  - Extend: Menginstal dan mengelola modul tambahan yang memperluas fungsionalitas Drupal.
  - Configuration: Mengelola pengaturan dasar Drupal, termasuk konfigurasi sistem, pengguna, dan alur kerja.

- Admin juga memiliki fitur notifikasi update **Drupal** dari developer.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/da08c08c-f373-41f2-ae26-630912dc5d24"></h1>

- Pada menu Manage, Admin dapat mengelola akun pengguna di situs **Drupal**, misalnya pengguna anonim, registrasi akun baru, dan penghapusan akun pengguna. Sehingga situs akan dikelola secara aman dan efisien dari sisi pendaftaran akun pengguna dan perlindungan konten yang sudah dihasilkan oleh pengguna.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/04cedb87-f84b-409d-ad57-a8f39ea69ccb"></h1>

- Admin dapat membuat, mengedit, menghapus, dan mengelola akun pengguna, serta menetapkan peran dan izin yang berbeda untuk pengguna lain.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/ca198a78-3644-40ba-87fe-60ed4630422b"></h1>

- Selain itu, Admin juga dapat menghapus komentar, dan membuat, mengedit, atau menghapus semua konten di situs, termasuk konten yang dibuat oleh pengguna lain.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/754246ff-dd89-4951-bd00-15a5030a7ed6"></h1>

</details>

<details><summary> 
  
  ## Pemakaian sebagai Pengguna
</summary>

- Sebelum menggunakan **Drupal** kita harus membuat akun terlebih dahulu, kemudian `Login`.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/62e9183b-a6f4-4966-bdc4-b173b1895c1a"></h1>
  
- Setelah melakukan login, tampilan aplikasi akan seperti berikut.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/1d106be3-3909-4f90-bfa3-e1ef6a5e0f51"></h1>

- Pengguna dapat membuat suatu artikel melalui menu `Shortcuts`, kemudian klik `Add Content`. Pada menu ini, kita bisa memilih bentuk konten yang ingin dibuat, yaitu *Article* atau *Basic Page*.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/a88707d3-2000-4eca-85e8-26a17e68c8ab"></h1>

- Jika kita ingin membuat suatu konten berupa artikel, tampilannya akan seperti berikut.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/dff3da9a-c889-4d90-b53c-e1fb7bd0d2cf"></h1>

- Jika artikel sudah selesai ditulis, simpan artikel.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/d651b7a2-24c4-4516-a851-fcd6e76ea3ff"></h1>

- Setelah artikel berhasil disimpan, tampilannya seperti berikut.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/3c5b2fbd-2204-4f29-8d24-64bf3d956d22"></h1>

- Jika ingin melihat konten yang telah berhasil dibuat, klik menu `Manage`, kemudian `Content`.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/44e26f52-0d2f-4a7a-9cf0-df38e5a78d82"></h1>

- Konten bisa dibaca dan dikomentari oleh pengguna lain.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/3044cd22-b466-4d65-a12f-81e8ab19e362"></h1>
  <h1 align="center"><img src="https://github.com/user-attachments/assets/945a3426-63a3-43ac-beeb-a89064cb4369"></h1>

- Pengguna dapat melakukan beberapa aksi terhadap konten yang telah dibuat seperti *delete content, promote content, publish content*, dan aksi-aksi lainnya.
  <h1 align="center"><img src="https://github.com/user-attachments/assets/9664adc9-c62c-41c5-8ef5-205966000bd6"></h1>

</details>



</details>

<details><summary> 
  
  # Pembahasan
</summary>

**Drupal** merupakan salah satu CMS yang banyak digemari oleh beberapa orang di seluruh dunia. Drupal dapat mempermudah untuk mengelola konten dan mempublikasikannya secara cepat. Berikut ini merupakan beberapa **kelebihan Drupal**:
1. Mudah untuk dilakukan pengembangan karena bersifat *open source*.
2. Memiliki tingkat keamanan yang tinggi karena adanya pengecekan data secara teratur dan berkala ketika aplikasi diperbarui.
3. Memiliki tampilan yang *responsive*, sehingga dapat dibuka menggunakan *device* apapun.
4. Mudah untuk memahami mengenai penggunaan **Drupal** karena video pembelajaran atau pelatihan sudah banyak tersedia di internet. Selain itu, **Drupal** juga memiliki dokumentasi yang lengkap.

Selain memiliki banyak manfaat seperti yang telah dijelaskan sebelumnya, Drupal juga memiliki kekurangan yang dapat diantisipasi. Berikut ini merupakan beberapa **kekurangan Drupal**.
1. **Drupal** menyediakan banyak fitur menarik bagi penggunanya, sehingga memerlukan waktu yang cukup lama untuk bisa menguasai CMS ini.
2. Aplikasi **Drupal** yang memiliki banyak modul atau konten bisa mengalami penurunan performa jika tidak dioptimalkan dengan baik.
3. Pilihan tema bawaan **Drupal** sangat terbatas dan banyak yang berbayar, sehingga pengguna akan kesulitan jika memerlukan pengembangan tema khusus atau penyesuaian lebih mendalam untuk menciptakan tampilan yang diinginkan.
4. Panel admin CMS terkadang sangat rumit untuk digunakan jika tidak terbiasa dengan tampilannya.

Jika dibandingkan dengan CMS sejenis yaitu **WordPress**, baik **WordPress** maupun **Drupal** tentunya memiliki beberapa kelebihan dan kekurangan yang dapat dijadikan sebagai pertimbangan sebelum menggunakannya. Berikut adalah beberapa perbandingan antara kedua CMS ini.
1. **Drupal** mendukung instalasi manual dan otomatis, namun instalasi manual akan lebih sulit bagi pemula. Sedangkan **WordPress** juga memiliki dua metode instalasi, tetapi lebih mudah digunakan berkat fitur-fitur yang memudahkan.
2. **Drupal** mengoptimalkan kecepatan situs secara otomatis sehingga performanya cepat. Sedangkan **WordPress** sedikit sulit untuk meningkatkan kecepatan karena tidak ada alat khusus untuk optimasi.
3. **Drupal** menawarkan konten yang lebih kompleks dan beragam, termasuk fitur chat dan media hosting. Sedangkan **WordPress** lebih sederhana dalam hal konten, sesuai dengan sistem administrasinya yang tidak sekompleks Drupal.
4. **Drupal** memiliki tingkat keamanan yang sangat tinggi, membuatnya sulit diretas. **WordPress** juga aman, namun rentan jika menggunakan banyak plugin atau tema pihak ketiga.
5. Kustomisasi tema dan plugin di **Drupal** lebih rumit dan sering memerlukan biaya. Sedangkan di **WordPress**, kustomisasinya lebih mudah dan gratis tanpa perlu modul khusus.

</details>

<details><summary> 
  
  # Referensi
</summary>

- [Wikipedia Drupal](https://en.wikipedia.org/wiki/Drupal) - Wikipedia
- [Drupal Documentation](https://www.drupal.org/documentation) - Drupal
- [Drupal Review](https://www.g2.com/products/drupal/reviews) - G2: Business Software and Services Reviews
- [Perbandingan Drupal dan Wordpress](https://www.sekawanmedia.co.id/blog/pengertian-drupal/) - Sekawanmedia

</details>

# Anggota Kelompok
| Nama                                      | NIM          |
|-------------------------------------------|--------------|
| [Aditya Purwansyah](https://github.com/dittdott) | G6401221024  |
| [Viby Ladyscha Yalasena Winarno](https://github.com/VibyLadyscha/) | G6401221025  |
| [Noer Hanifah Suganda](https://github.com/haniniw) | G6401221041 |
| [Nabiel Muaafii Rahman](https://github.com/NabielMuaafiiR) | G6401221044  |
| [Yuuka Salsabila Sisvi](https://github.com/Yuukasalsabila) | G6401221117  |
