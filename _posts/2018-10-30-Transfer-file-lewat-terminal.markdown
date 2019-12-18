---
layout: post
title: Transfer File Atau Directory Lewat Terminal
date: 2018-10-30 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: Rsync-Over-SSH-Non-standard-Port.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

System operasi linux sudah memprovide sebuah program yang bernama terminal atau juga sering di sebut dengan bash, Terminal atau bash banyak sekali fungsinya. Salah satunya yaitu untuk mengirim atau mengsinkronkan file dan directory pada satu lokasi atau server ke lokasi lain. Untuk GUI mungkin kita bisa menggunakan FileZilla. Tapi pada kali ini kita akan mensinkronkan file atau directory dengan terminal atau bash.

**Mengubah Kepemilikan File Atau Directory**

Pertama yang harus kita lakukan untuk mensinkronkan file atau directory adalah Mengubah Ownership atau kepemilikan file atau directory tersebut dari root ke nama user komputer kita agar kita bisa menjalankan data tersebut.

Berikut perintah untuk mengubah ownership atau kepemilikan file atau directory :

        $ chown -R (nama user : nama user) (nama file / directory)

Sebagai Contoh, Didalam dir /opt/ saya punya dir yang bernama 'myapi'

![Macbook]({{site.baseurl}}/assets/img/ft-01.png)

Dir 'myapi' tersbut masih menggunakan sebagai root, saya akan mengubah dari root ke nama user saya dengan mengetikkan perintah berikut :

        $ sudo chown -R mee:mee myapi

Maka berubahlah kepemilikan dir tersebut dari root ke user saya.

![Macbook]({{site.baseurl}}/assets/img/ft-02.png)


> *NOTE* : -R tersebut untuk directory

Kemudian setelah kita mengubah ownership maka kita siapkan file atau directory yang ingin kita sinkron atau kita kirim. Di sini saya akan mengirim file yang bernama "script.conf" ke komputer teman saya.

![Macbook]({{site.baseurl}}/assets/img/ft-03.png)

Untuk mensinkronkan atau mengirimkan file tersebut kita ketik perintah :

    $ scp script.conf dhia@192.168.100.20:/opt/myapi/scipt.conf

Dengan keterangan :

    $ scp (file yang ingin di kirim) user@ipadress:(dir tujuan)

![Macbook]({{site.baseurl}}/assets/img/ft-04.png)

Ataua jika kita ingin menyamakan isi folder yang ada pada laptop/PC kita dengan laptop/PC tujuan atau mem back up foler yang kita punya ke laptop tujuan kita bisa menggunakan perintah di bawah ini :

    $ rsync (file yang ingin dikirim) user(tujuan)@ipadress(tujuan):(dir tujuan)

>*Note* : Jika kita ingin mengirimkan sebuah directory maka kita tambahkan perintah -r sebelum file yang ingin di kirim


maka folder yang ada di laptop/pc tujuan akan sama dengan yang ada pada pc /laptop kita termasuk permission nya juga.









