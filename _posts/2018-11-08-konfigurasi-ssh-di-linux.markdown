---
layout: post
title: Konfigurasi SSH Server Di Linux
date: 2018-11-09 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: git.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

### Pengertian

SSH adalah aplikasi pengganti remote login seperti telnet, rsh, dan rlogin, yang jauh lebih aman yang dapat berjalan di system operasi linux. Fungsi utam dari ssh ini adalah untuk mengakses mesin secara remote. SSH Client menyediakan user dengan shell untuk remote ke mesin. Dengan menggunakan SSH kita dapat bergerak bebas melalui struktur file akun hosting. kita juga dapat bebas melakukan monitoring log file dan memulai atau menghentikan service.

### Install dan Konfigurasi SSH Server di Linux

Untuk menginsall ssh kita dapat menjalankan perintah berikut :

    $ sudo apt-get install open-ssh-server

Tunggu hingga proses installasi selesai.

Secara default ssh server yang sudah terinstall biasanya menggunakan **port 22**, namun untuk keamanan kita juga dapat mencustom dengan cara melakukan konfigurasi ssh server.

### Konfugurasi SSH Server


Untuk melakukan konfigurasi ssh server kita dapat mengaturnya di file `sshd_config` :

    $ sudo nano /etc/ssh/sshd_config

Maka akan muncul tampilan text editor nano yang berisikan file `sshd_config`.

Lalu kemudian cari text yang bertuliskan **port 22**, kemudian ganti angka 22 dengan nomor port yang kita inginkan, misalnya 1022. Lalu simpan dengan menekan tombol CTRL + X Lalu Y kemudian enter.

Setelah melakukan edit port ssh, kita harus jalankan restart ssh agar pengeditan port tersebut berfungsi. Untuk melakukan restart ssh ketikan perintah :

    $ /etc/init.d/ssh restart

setelah di restart kita dapat melakukan pengujian ssh server. pengujian ini dilakukan untuk memastikan bahwa ssh server sudah aktif dan berjalan dengan baik. Pengujian ssh server bisa dilakukan di komputer client atau server atau komputer manapun.

Untuk kali ini saya akan menjalankan ssh ke komputer teman saya. Ip Address teman saya adalah 192.168.100.87 dan port 1022.

    $ ssh user@192.168.100.87 -p 1022

`User` adalah nama user komputer teman saya. dan `-p` itu bermakna **port**.




http://referensisiswa.blogspot.com/2017/09/cara-install-dan-konfigurasi-ssh-server.html
http://septianze.blogspot.com/2016/12/pengertian-ssh-server-fungsi-dan-cara.html