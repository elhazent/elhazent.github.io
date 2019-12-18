---
layout: post
title: Mencari Dan Menghapus File Duplicate Di Linux
date: 2018-11-05 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: fd-bg.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

Seringkali kita mungkin menemukan di dalam komputer kita ada sebuah direktory atau file yang sama di karenakan kita sudah mendownload atau mengcopynya sudah beberapa kali dan menyebabkan direktory kita menjadi berantakan dengan semua jenis direktory dan file duplikat yang tidak berguna.

Dalam Penjelasan kali ini kita akan belajar bagaimana mencari dan menghapus file duplikat di linux Lewat terminal.

> Note : Kita harus selalu berhati - hati dengan apa yang akan kita hapus pada komputer kita karena hal ini dapat menyebabkan kita kehilangan data yang sangat penting.

Dalam pencarian dan penghapus file duplikat ada dua command line, Yaitu :
* 1. rdfind 
* 2. fdupes

### Rdfind - Mencari Duplikat Data Pada Linux

Rdfind berasal dari kata  (Redundant Data Find) adalah command yang digunakan untuk mencari file duplikat di seluruh atau dalam beberapa direktory komputer kita. command ini bekerja menggunakan checksum dan mencari file duplikat tidak hanya berisi nama.

Rdfind menggunakan algoritma untuk mengklasifikasikan file dan mendeteksi duplikat mana yang merupakan file asli dan menganggap sisanya sebagai duplikat. Aturan peringkat adalah:

- Jika A ditemukan saat memindai argumen input lebih awal dari B, A adalah peringkat yang paling tinggi.
- Jika A ditemukan pada kedalaman lebih rendah dari B, A adalah peringkat yang lebih tinggi.
- Jika A ditemukan lebih awal dari B, A adalah peringkat yang lebih tinggi.

Aturan terakhir digunakan terutama ketika dua file ditemukan di direktori yang sama.

 Untuk menginstall rdfind di linux, gunakan perintah berikut sesuai dengan distribusi linux kita.

    * $ sudo apt-get install rdfind    [Pada distribusi linux ubuntu/debian]
    * $ sudo yum install epel-release && sudo yum install rdfind [On CentOS]
    * $ sudo dnf install rdfind         [On Fedora 22+]

Untuk menjalankan rdfind pada direktori cukup ketik rdfind dan direktori target. Berikut ini contohnya:

        $ rdfind /home/user

![Macbook]({{site.baseurl}}/assets/img/fd-01.png)

Seperti yang Anda lihat rdfind akan menyimpan hasil dalam file yang disebut results.txt yang terletak di direktori yang sama dari tempat Anda menjalankan program. File ini berisi semua file duplikat yang telah ditemukan oleh rdfind. Anda dapat meninjau file dan menghapus file duplikat secara manual jika Anda mau.

Hal lain yang dapat Anda lakukan adalah menggunakan opsi -dryrun yang akan memberikan daftar duplikat tanpa mengambil tindakan apa pun:

    $ rdfind -dryrun true /home/user  

Ketika kita menemukan duplikat, kita dapat memilih untuk menggantinya dengan hardlink.

    $ rdfind -makehardlinks true /home/user

Dan jika Anda ingin menghapus duplikat yang dapat Anda jalankan.

    $ rdfind -deleteduplicates true /home/user  

Untuk memeriksa opsi berguna lainnya dari rdfind, Anda dapat menggunakan manual rdfind dengan mengetikan perintah berikut :

    $ man rdfind

### Fdupes - Mencari File Duplikat di Linux

Fdupes adalah program lain yang memungkinkan Anda mengidentifikasi file duplikat di sistem kita. Ini gratis dan open source dan ditulis dalam C. Menggunakan metode berikut untuk menentukan file duplikat:

* Membandingkan tanda tangan md5sum parsial
* Membandingkan tanda tangan md5sum penuh
* Byte-by-byte comparison verification

Sama seperti rdfind itu memiliki opsi serupa:

* Cari secara rekursif
* Kecualikan file kosong
* Menunjukkan ukuran file duplikat
* Hapus duplikat segera
* Kecualikan file dengan pemilik yang berbeda
* Fdupes sintaks mirip dengan rdfind. Cukup ketikkan perintah yang diikuti oleh direktori yang ingin Anda pindai.

    $ fdupes <dir>

Untuk mencari file secara rekursif, Kita harus menentukan opsi -r seperti ini.

    $ fdupes -r <dir>

Kita juga dapat menentukan banyak direktori dan menentukan direktori yang akan dicari secara rekursif.

    $ fdupes <dir1> -r <dir2>

Agar fdupes menghitung ukuran file duplikat menggunakan opsi -S.

    $ fdupes -S <dir>

Untuk mengumpulkan informasi ringkasan tentang file yang ditemukan menggunakan opsi-m.

    $ fdupes -m <dir>

![Macbook]({{site.baseurl}}/assets/img/fd-02.png)

Akhirnya jika Kita ingin menghapus semua duplikat, gunakan opsi -d seperti ini.

    $ fdupes -d <dir>

Fdupes akan menanyakan file mana yang ingin dihapus. Kita harus memasukkan nomor file:

![Macbook]({{site.baseurl}}/assets/img/fd-03.png)

Solusi yang pasti tidak disarankan adalah menggunakan opsi -N yang akan menghasilkan pelestarian file pertama saja.

    $ fdupes -dN <dir>

untuk mendapatkan daftar opsi yang tersedia untuk digunakan dengan fdupes meninjau halaman bantuan dengan menjalankan.

    $ fdupes -help


> Kesimpulan :
Rdfind dan fdupes adalah alat yang sangat berguna untuk menemukan file duplikat pada sistem Linux Anda, tetapi Anda harus sangat berhati-hati saat menghapus file-file tersebut.

>Jika Anda tidak yakin jika Anda memerlukan file atau tidak, akan lebih baik untuk membuat cadangan file itu dan mengingat direktori sebelum menghapusnya. Jika Anda memiliki pertanyaan atau komentar, harap kirimkan di bagian komentar di bawah ini.

    Referensi : https://www.tecmint.com/find-and-delete-duplicate-files-in-linux/