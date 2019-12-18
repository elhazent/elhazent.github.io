---
layout: post
title: Penjelasan Command Find Linux #1
date: 2018-10-28 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: find.jpg # Add image post (optional)
tags: [Productivity, Software] # add tag
---

Pada Kali ini saya akan menjelaskan tentang command 'find',  Ketika kita sedang mengerejakan sesuatu di komputer kita, kadang kita lupa meletakkan directory atau file di dalam komputer kita, tetapi kita hanya mengingat namanya saja. Nah, Menggunakan command 'find' ini kita bisa menemukan directory atau file yang kita cari hanya dengan menuliskan nama atau type directory atau file tersebut.

Bagaiman cara menggunakannya?

Nah, Langsung saja kita ke contoh penggunaan command 'find'. Misal disini saya punya file bernama example.txt yang berada di directory 'latihan' didalam directory Document.

![Sosok Linus Torvalds, Pendiri Linux]({{site.baseurl}}/assets/img/01.png)

Terus suatu ketika saya ingin mencari file “example.txt” tersebut, tapi saya cuma ingat kalo ada di dalam Documents. Maka saya ketik

	$ find Document -name "example.txt"

![Sosok Linus Torvalds, Pendiri Linux]({{site.baseurl}}/assets/img/02.png)

Nah.. ketemu lah file tersebut berada. Jadi tulisan Documents sebelum ‘-name’ itu menunjukan tempat dimana kamu akan mencari, jika di kosongi (langsung ‘-name’) berarti dia akan mencari di current direktori(tempat sekarang kamu berada). Kalau saya ganti menjadi tempatnya menjadi Downloads maka tidak akan keluar hasil apa2, karna di Downloads tidak ada file itu.

![Sosok Linus Torvalds, Pendiri Linux]({{site.baseurl}}/assets/img/03.png)

Trus kalo bener2 lupa di mana tempat nyimpannya gimana?? ya.. tinggal mulai pencarian dari akar semua file “/”. Tapi untuk metode ini butuh hak akses root jadi harus di tambah command “sudo” sebelum command find

	$ find / -name "example.txt"

![Sosok Linus Torvalds, Pendiri Linux]({{site.baseurl}}/assets/img/04.png)

Mungkin Pada pembahasan kali ini cukup sampai di sini dulu.. untuk penjelasan command-command terminal yang lainnya silahkan dicek di home.