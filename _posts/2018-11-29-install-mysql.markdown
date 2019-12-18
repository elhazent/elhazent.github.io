---
layout: post
title: Install MySQL Database Server
date: 2018-11-29 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: sql-bg.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

### Pengertian

MySQL merupakan database engine atau server database yang mendukung bahasa database pencarian SQL. MySQL adalah sebuah perangkat lunak sistem manajemen basis data SQL atau DBMS yang multithread, multi-user. MySQL AB membuat MySQL tersedia sebagai perangkat lunak gratis dibawah lisensi GNU General Public License (GPL), tetapi mereka juga menjual dibawah lisensi komersial untuk kasus-kasus dimana penggunaannya tidak cocok dengan penggunaan GPL.

MySQL sebenarnya merupakan turunan salah satu konsep utama dalam database sejak lama, yaitu SQL (Structured Query Language). SQL adalah sebuah konsep pengoperasian database, terutama untuk pemilihan atau seleksi dan pemasukan data, yang memungkinkan pengoperasian data dikerjakan dengan mudah dan cepat secara otomatis. Keandalan suatu sistem database (DBMS) dapat diketahui dari cara kerja optimizer-nya dalam melakukan proses perintah-perintah SQL, yang dibuat oleh user maupun program-program aplikasinya. Sebagai database server, MySQL dapat dikatakan lebih unggul dibandingkan database server lainnya dalam query data. Hal ini terbukti untuk query yang dilakukan oleh single user, kecepatan query MySQL bisa sepuluh kali lebih cepat dari PostgreSQL dan lima kali lebih cepat dibandingkan Interbase.

### Installasi MySQL Database server

Untuk instalasi MySQL ketikan perintah berikut pada terminal linux :

    $ sudo apt-get install mysql-client mysql-server

Selama instalasi paket, Anda akan diminta untuk mengatur kata sandi pengguna **root** untuk **mysql** seperti yang terlihat pada gambar di bawah ini. Pilih kata sandi yang bagus dan aman, lalu tekan tombol **OK** dua kali untuk melangkah lebih jauh.

![Macbook]({{site.baseurl}}/assets/img/sql-1.png)

Penyebaran server basis data belum aman, karena alasan ini, berikan perintah berikut untuk memperkuat keamanannya:

    $ sudo mysql_secure_installation 

Pertama, Anda akan diminta untuk menginstal plugin **'validate_password'**, jadi ketik `Y/Yes` dan tekan **Enter**, dan juga pilih tingkat kekuatan kata sandi default. Di sistem saya, saya sudah menginstalnya.

Yang penting, jika Anda tidak ingin mengubah kata sandi root, maka ketik `N/No` ketika diminta untuk melakukannya. Jawab `Y/Ya` untuk pertanyaan selanjutnya.

> Referensi :
> - http://edel.staff.unja.ac.id/blog/artikel/Pengertian-MySQL.html
> - https://www.tecmint.com/install-wordpress-on-ubuntu-16-04-with-lamp/