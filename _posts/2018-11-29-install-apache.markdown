---
layout: post
title: Install Apache Web Server
date: 2018-11-29 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: aws-bg.jpeg # Add image post (optional)
tags: [Productivity, Software] # add tag
---

### Pengertian

Apache adalah software web server yang gratis dan bersifat open source. Server ini telah menjadi platform bagi 46% website di seluruh dunia. Nama resminya adalah Apache HTTP Server, dan software ini dikelola dan dikembangkan oleh Apache Software Foundation.

Apache memudahkan pemilik website untuk mebuat konten di web – dan karena itulah software diikuti dengan kata ‘web server’. Apache adalah salah satu web server tertua dan dapat diandalkan. Versi pertamanya telah dirilis lebih dari 20 tahun yang lalu, tepatnya pada tahun 1995.

Ketika seseorang hendak mengakses suatu website, ia harus memasukkan nama domain ke kolom alamat pada browser. Setelah itu, web server akan mengirimkan file yang diminta. Dalam hal ini, server berperan sebagai pengirim virtual.

Di Hostinger, infrastruktur web hosting kami mengunakan Apache yang sejajar dengan NGINX, yang juga merupakan software web server yang banyak digunakan. Pengaturan khusus ini memudahkan kami untuk memaksimalkan baik server maupun web hosting. Pengaturan tersebut juga menaikkan performa server dengan menyeimbangkan kelemahan salah satu server dan kelebihan server lainnya.

### Installasi Apache Web Server

Untuk menginstall Apache web server, ketikan perintah berikut di terminal :

    $ sudo apt-get install apache2 apache2-utils 

Kita perlu mengaktifkan Apache web server untuk memulai pada waktu boot sistem, serta memulai layanan sebagai berikut:

    $ sudo systemctl enable apache2
    $ sudo systemctl start apache2

Untuk menguji apakah server berjalan, buka browser web Anda dan masukkan `http://localhost`. Halaman indeks default Apache2 akan ditampilkan jika server web aktif dan berjalan.

![Macbook]({{site.baseurl}}/assets/img/aws-1.png)


> Referensi :
> - https://www.hostinger.co.id/tutorial/apa-itu-apache/#gref
> - https://www.tecmint.com/install-wordpress-on-ubuntu-16-04-with-lamp/