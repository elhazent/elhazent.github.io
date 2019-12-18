---
layout: post
title: Install Wordpress di Linux
date: 2018-11-30 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: wp-bg.jpg # Add image post (optional)
tags: [Js, Conference] # add tag
---

### Pengertian

WordPress merupakan sistem manajemen konten (CMS) yang paling banyak digunakan di dunia. Lebih dari 30% website dibuat di WordPress dan persentasenya masih akan terus meningkat!

Secara umum, sistem manajemen konten adalah aplikasi web yang memperbolehkan pemilik, editor, dan author untuk mengelola website dan menerbitkan konten tanpa harus menguasai istilah teknis dan bahasa pemrograman terlebih dulu.

WordPress menggunakan PHP dan MySQL, yang ternyata didukung oleh hampir semua penyedia web hosting. Terdapat juga paket WordPress hosting yang menawarkan kelebihan dalam kecepatan, performa, dan keandalan website.

Kelebihan WordPress lainnya terletak pada tipe website yang bisa dibuat di platform ini. CMS ini memungkinkan Anda tak hanya membuat blog sederhana, tapi juga situs ecommerce, portofolio, newspaper, atau apa pun yang diinginkan.

Salah satu hal terbaik WordPress adalah CMS ini memiliki software antarmuka yang intuitif dan mudah digunakan. Apabila Anda tahu cara menggunakan Microsoft Word, maka Anda tidak akan mengalami kesulitan saat hendak mengoperasikan WordPress: membuat dan menerbitkan konten semudah menjentikkan jari.

![Macbook]({{site.baseurl}}/assets/img/wp-1.jpg)

Selain itu, WordPress bersifat open-source dan bisa digunakan oleh siapa pun. Bahkan CMS WordPess memungkinkan jutaan orang di dunia untuk membuat website modern berkualitas tinggi – meski Anda masih pemula sekalipun.

### Installasi Wordpress di Linux

- **Step 1 : Install Apache2**

Kita diharuskan untuk menginstall apache2 terlebih dahulu, untuk instalasi apache2nya kalian bisa melihat postingan tentang instalasi apache2 dipostingan sebelumnya.

- **Step 2 : Install MySQL Database Server**

Kita membutuhkan MySQL Server. untuk proses instalasinya kalian juga dapat melihat postingan tentang instalasi MySQL Server dipostingan sebelumnya.

- **Step 3 : Install PHP Dan Modules**

Kita harus menginstall PHP dan beberapa modul untuk bekerja dengan server web dan database menggunakan perintah di bawah ini:

    $ sudo apt-get install php7.0 php7.0-mysql libapache2-mod-php7.0 php7.0-cli php7.0-cgi php7.0-gd

Selanjutnya, untuk menguji apakah php bekerja dalam kolaborasi dengan server web, kita perlu membuat file info.php di dalam `/var/www/html`.

    $ sudo vi /var/www/html/info.php

Dan paste kode di bawah ini ke dalam file `info.php`, lalu simpan dan keluar.

    <?php 
    phpinfo();
    ?>

Ketika sudah selesai semua, lalu buka browser web Anda dan ketik alamat ini http://localhost/info.php maka anda dapat melihat halaman info php di bawah ini sebagai konfirmasi kalau proses instalasi PHP sudah sempurna.

![Macbook]({{site.baseurl}}/assets/img/wp-3.png)

- **Step 4: Install WordPress CMS**

Unduh paket WordPress terbaru dan ekstrak dengan mengetikan perintah di bawah ini pada terminal:

    $ wget -c http://wordpress.org/latest.tar.gz
    $ tar -xzvf latest.tar.gz

Kemudian pindahkan file WordPress dari folder yang diekstrak ke direktori akar default Apache, `/var/www/html/` :

    $ sudo rsync -av wordpress/* /var/www/html/

Selanjutnya, atur permissions yang benar pada direktori situs web, yaitu memberikan kepemilikan file WordPress ke server web sebagai berikut:

    $ sudo chown -R www-data:www-data /var/www/html/
    $ sudo chmod -R 755 /var/www/html/

- **Step 5: Membuat WordPress Database**

Jalankan perintah di bawah ini dan berikan kata sandi pengguna root, lalu tekan Enter untuk berpindah ke shell mysql:

    $ mysql -u root -p 

Pada shell mysql, ketik perintah berikut, tekan Enter setelah setiap baris perintah mysql. Ingat untuk menggunakan nilai Anda sendiri, valid untuk **database_name**, **pengguna database**, dan juga menggunakan kata sandi yang kuat dan aman sebagai **databaseuser_password**:

    mysql> CREATE DATABASE wp_myblog;
    mysql> GRANT ALL PRIVILEGES ON wp_myblog.* TO 'your_username_here'@'localhost' IDENTIFIED BY 'your_chosen_password_here';
    mysql> FLUSH PRIVILEGES;
    mysql> EXIT;

Buka direktori `/var/www/html/` dan ganti nama **wp-config-sample.php** menjadi **wp-config.php**:

    $ sudo mv wp-config-sample.php wp-config.php

kemudian perbarui informasi database Anda di bawah bagian pengaturan MySQL (lihat kotak yang disorot pada gambar di bawah):

    // ** MySQL settings - You can get this info from your web host ** //
    /** The name of the database for WordPress */
    define('DB_NAME', `'database_name_here'`); /** MySQL database username */ define('DB_USER', `'username_here'`); /** MySQL database password */ define('DB_PASSWORD', `'password_here'`); /** MySQL hostname */ define('DB_HOST', `'localhost'`); /** Database Charset to use in creating database tables. */ define('DB_CHARSET', `'utf8'`); /** The Database Collate type. Don't change this if in doubt. */ define('DB_COLLATE', `''`);

Setelah itu, restart server web dan layanan mysql menggunakan perintah di bawah ini:

    $ sudo systemctl restart apache2.service 
    $ sudo systemctl restart mysql.service 

Buka browser web Anda, lalu masukkan alamat server Anda: `http://localhost` untuk mendapatkan halaman selamat datang di bawah ini. Baca melalui halaman dan klik "Let's go!" Untuk melangkah lebih jauh dan mengisi semua informasi yang diminta di layar.

![Macbook]({{site.baseurl}}/assets/img/wp-2.png)

Jika semuanya berjalan baik-baik saja, Anda sekarang dapat menikmati WordPress di sistem Anda. Namun, untuk mengungkapkan kekhawatiran atau mengajukan pertanyaan terkait langkah-langkah di atas atau bahkan memberikan informasi tambahan yang menurut Anda belum dimasukkan dalam tutorial ini, Anda dapat menggunakan bagian umpan balik di bawah ini untuk menghubungi kami kembali.

> Referensi :
> - https://www.tecmint.com/install-wordpress-on-ubuntu-16-04-with-lamp/
> - https://dhiaulhaq.com/2018/11/28/wordpress/