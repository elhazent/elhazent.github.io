---
layout: post
title: Install GIT Di Terminal
date: 2018-09-12 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: git.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

Sebelum kalian menggunakan git, Kalian pastikan dulu kalau komputer kalian sudah install git atau belum.
Meskipun sudah terpasang, ada baiknya untuk mengupdate versi git kalian ke versi terbaru. Kalian bisa menginstalnya sebagai paket atau melalui penginstal lain, atau mengunduh kode sumber dan kompilasi sendiri.

>Tulisan ini ditulis menggunakan Git versi 2.17.1. Meskipun sebagian besar perintah yang kami gunakan semestinya berfungsi bahkan di versi kuno Git, beberapa dari mereka mungkin tidak atau mungkin bertindak sedikit berbeda jika Anda menggunakan versi yang lebih lama. Karena Git cukup bagus dalam menjaga kompatibilitas mundur, versi apa pun setelah 2.17.1 seharusnya bekerja dengan baik.

## Installing on linux

Jika Kalian ingin menginstal Git dasar di Linux melalui penginstal biner, Kalian biasanya dapat melakukannya melalui alat manajemen paket yang disertakan dengan distribusi Kalian. Jika Kalian menggunakan Fedora (atau distribusi berbasis RPM terkait-erat, seperti RHEL atau CentOS), Kalian dapat menggunakan dnf:

>$ sudo dnf install git-all

Dan jika Kalian ingin menginstallnya di linux berbasis Debian atau Ubuntu, Kalian bisa menggunakan apt :

>$ sudo apt install git-all

Untuk beberapa pengaturan lainnya, ada intruksi penginstallan git pada basis unix lainnya di http://git-scm.com/download/linux.

## Installing on mac

Ada beberapa cara untuk menginstal Git di Mac. Yang paling mudah mungkin adalah menginstal Xcode Command Line Tools. Pada Mavericks (10.9) atau di atas Kalian dapat melakukan ini hanya dengan mencoba menjalankan git dari Terminal untuk pertama kalinya.

>$ git --version

Jika Kalian belum menginstalnya, ia akan meminta Kalian untuk memasangnya.

Jika Kalian ingin versi yang lebih baru, Kalian juga dapat menginstalnya melalui installer biner. Penginstal macOS Git dikelola dan tersedia untuk diunduh di situs web Git, di http://git-scm.com/download/mac.

![Macbook]({{site.baseurl}}/assets/img/git-osx-installer.png)

Kalian juga dapat menginstalnya sebagai bagian dari instalasi GitHub untuk Mac. Alat GUI Git mereka memiliki opsi untuk menginstal alat baris perintah juga. Kalian dapat mengunduh alat itu dari situs web GitHub untuk Mac, di http://mac.github.com.