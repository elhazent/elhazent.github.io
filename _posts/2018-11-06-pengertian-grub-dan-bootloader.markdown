---
layout: post
title: Pengertian Grub Dan Bootloader
date: 2018-11-06 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: bl-bg.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

**Pengertian**

Pada saat kita menyalakan komputer, program yang pertama kali jalan setelah BIOS adalah GRUB apabila komputer kita menggunakan system operasi linux. Grub adalah singkatan dari GRand Unified Bootloader, yaitu program kecil yang menampilkan pilihan system operasi pada saat proses booting sehingga kita bisa memilih system operasi apa yang ingin kita jalankan. Grub sangat berguna apabila kita menginstall lebih dari satu system operasi pada satu komputer seperti Windows 10 dan Linux ubuntu yang bahasa lain nya adalah Dual Booting. Biasanya default sistem operasi pada menu GRUB adalah Linux Ubuntu. Istilah default disini artinya adalah sistem operasi yang akan dijalankan secara otomatis apabila kita tidak memilih sistem operasi lain pada daftar menu GRUB. GRUB dapat di konfigurasi sesuai keinginan. Namun apabila salah dalam pengeditan maka saat booting GRUB tidak akan dapat masuk ke system operasi yang tersedia. 

**Letak File Bootloader**

Untuk mengetahui letak/isi konfgurasi GRUB kita bisa mengetikkan perintah berikut :

    $ sudo cat /boot/grub/grub.cfg

Di dalam catatan grub.cfg tersebut kita tidak diperbolehkan untuk mengedit catatan tersebut dikarenakan bisa merusak file system kita.

Kita juga bisa melihat apa saja yang yang ditampilkan oleh grub dengan mengetikan perintah:

    $ cd /etc/grub.d
    $ ls -la

Di dalam dir grub.d tersebut terdapat beberapa file yang disertai nomor, fungsi nomor tersebut adalah untuk kita mengetahui bahwa file tersebut akan muncul pada bootloader di urutan ke berapa.

**Windows Tidak Muncul Pada GrubLoader?**

Dan apabila kita sudah melakukan install dual booting akan tetapi windows tidak muncul pada grubloader kita bisa mengetikan perintah berikut pada terminal bash linux :

    $ sudo update-grub

Nah, setelah menjalankan perintah di atas, secara otomatis windows sudah muncul pada bootloader.

    Referensi :
    * https://linuxacademy.com/cp/courses/lesson/course/1760/lesson/3/module/173
    * https://coretaniwans.wordpress.com/2014/07/16/pengertian-bootloader-grublilo-di-linux/