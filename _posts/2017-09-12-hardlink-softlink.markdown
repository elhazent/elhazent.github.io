---
layout: post
title: Mengenal Hardlink Dan Softlink Dalam Linux
date: 2018-10-31 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: unix-linux.jpg # Add image post (optional)
tags: [Productivity, Software] # add tag
---
Hardlink dan softlink yang biasa disebut dengan shortcut (jalan pintas yang digunakan untuk menjalankan suatu perintah pada komputer.)

**Perbedaan Hardlink dan Softlink**

* Hardlink  : jika file utama dihapus maka file yang dilink tetap jalan.
* Softlink  : jika file utama dihapus maka file yang dilink tidak bisa berjalan.

**Cara Menggunakan Hardlink Dan Softlink**

* Hardlink
    
        $ ln  fileasal filelink

* Softlink

        $ ln -s fileasal filelink

Contoh :
* Hardlink :

    $ ln latihan/script.sh file

* Softlink :

    $ ln -s latihan/script.sh file

untuk menampilkan file dengan inode atau i-number atau inode-number (inode).

    $ ls -ali

hardlink mempunyai kesamaan inode sedangkan softlink tidak :

![Macbook]({{site.baseurl}}/assets/img/symbolic.png)

symbolic link yang sudah dihapus file sumbernya

![Macbook]({{site.baseurl}}/assets/img/symbolic_h.png)


hardlink mempunyai kesamaan inode sedangkan softlink tidak

**Cara Menghapus Link**

Untuk menghapus link ada dua cara :

**1. Menggunakan unlink**

    $ unlink (namalink)

**2. Menggunakan rm**

    $ rm (namalink)

Sekian Pembahasan tentang link dari saya, bagi para pembaca jika ingin menambahkan boleh komentar dibawah.

    Referensi :
    * https://linuxacademy.com/cp/courses/lesson/course/1748/lesson/9/module/173
    * https://averoes12.com/hard-link-soft-link/
    * https://ambilgratis.com/2013/05/08/mengenal-hardlinks-dan-softlinks-dalam-linux/

