---
layout: post
title: Pengertian File System Linux
date: 2018-10-29 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: linux-file-systems.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

## Pengertian

File system adalah berkas struktur logika yang digunakan untuk mengendalikan akses terhadap data yang ada pada hardisk. Dengan kata lain, file system merupakan database khusus untuk penyimpanan, pengelolaan, manipulasi dan pengambilan data, agar mudah ditemukan dan diakses.

Hubungan antara system operasi dan  file system adalah file system merupakan interface yang menghubungkan system operasi dengan disk. Ketika program menginginkan pembacaan dari hardisk atau media penyimpanan lainnya, system operasi akan meminta file system untuk mencari lokasi dari file yang diinginkan. setelah file ditemukan, file system akan membuka dan membaca file tersebut, kemudian mengirimkan informasinya kepada system operasi dan akhirnya bisa dibaca oleh pengguna.

## Jenis-Jenis File System

### 1. Ext

Ext atau Extended File System merupakan jenis file system yang di perkenalkan pada tahun 1992, Ext memiliki beberapa versi :

#### >  Ext2 (2nd Extended)

Ext2 merupakan jenis file system linux paling tua yang masih ada. file system ini pertama kali dikenalkan pada januari 1993. File system ini ditulis oleh Remy Card, Theodore T, dan Stephen Tweedie. File system ini merupakan penulisan ulang besar-besaran dari Extended file system. Ext2 adalah file system yang paling ampuh di Linux dan menjadi dasar dari segala distribusi linux.

#### > Ext3 (3rd Extended)

Ext3 adalah peningkatan dari sistem file Ext2. Peningkatan ini memiliki beberapa keuntungan, diantaranya:
* Journaling,
dengan menggunakan journaling, maka waktu recovery pada shutdown mendadak tidak akan selama pada Ext2. Namun ini menjadi kekurangan dari Ext3, karena dengan adanya fitur journaling, maka membutuhkan memori yang lebih dan memperlambat operasi I/O (Input/Output).
* Integritas data,
Ext3 menjamin adanya integritas data setelah terjadi kerusakan atau unclean shut down. Ext3 memungkinkan kita memilih jenis dan tipe proteksi dari data.
* Kecepatan,
daripada menulis data lebih dari sekali, Ext3 mempunyai throughput yang lebih besar daripada Ext2 karena Ext3 memaksimalkan pergerakan head hard disk. Kita bisa memilih tiga jurnal mode untuk memaksimalkan kecepatan, tetapi integritas data tidak terjamin.
* Mudah dilakukan migrasi,
kita dapat berpindah dari sistem file Ext2 ke sistem file Ext3 tanpa melakukan format ulang.

#### > Ext4 (4th Extended)

Ext4 merupakan peningkatan dari sistem file Ext3. Ext4 dirilis secara lengkap dan stabil mulai dari kernel 2.6.28. Keuntungan menggunakan Ext4 adalah mempunyai pengalamatan 48-bit blok yang artinya dia akan mempunyai 1 EiB = 1.048.576 TB. Ukuran maksimum sistem file 16 TB.

### 2. JFS (Journalis File System)

JFS atau dikenal juga dengan nama IBM Journal File System merupakan sistem file pertama yang menawarkan journaling. JFS sudah bertahun-tahun digunakan dalam IBM AIX® OS sebelum digunakan ke GNU/Linux. JFS saat ini menggunakan sumber daya CPU paling sedikit dibandingkan sistem file GNU/Linux lainnya. JFS sangat cepat diformat, mounting dan fsck, serta memiliki kinerja sangat baik, terutama berkaitan dengan deadline I/O scheduler. Walaupun begitu, dukungan terhadap JFS tidak seluas sistem file Ext atau Reiser FS.

### 5. Reiser FS

Sistem file Reiser dibuat berdasarkan balance tree yang cepat dan unggul dalam hal kinerja, dengan algoritma yang lebih rumit. Sistem file Reiser juga memiliki jurnal yang cepat dan ciri-cirinya mirip sistem file Ext3. Sistem file Reiser lebih efisien dalam pemanfaatan ruang disk, dimana dapat menghemat disk sampai dengan 6 persen. Contohnya jika kita menulis file 100 bytes, hanya ditempatkan dalam satu blok sementara sistem file lain menempatkannya dalam 100 blok. Reiser file system tidak memiliki pengalokasian yang tetap untuk inode.

### 6. XFS

XFS mempunyai throughput yang sangat cepat pada file besar, dan sangat cepat di format dan mounting akan tetapi throughput nya lambat pada file kecil.

### 7. BTRFS (B-Tree File System)

BTRFS merupakan file system yang berada di bawah lisensi General Public Lisence. BTRFS membuat linux dapat lebih mengatur storage yang ada dan juga dapatmelakukan administrasi dan pengelolaan tempat penyimpanan dengan interface yang lebih bersih.

### 8. ZFS (Zettabytes File System)

ZFS merupakan file system terbaru yang dikembangkan oleh Sun,yang dirancang untuk menggunakan metode penyimapanan yang dikumpulkan(pooling).Dan juga telah dirancang unutk integritas data maksimum,mendukung snapshot data ,multiple penyalinan,dan checksum data.

	Referensi :
	* https://linuxacademy.com/cp/courses/lesson/course/1748/lesson/4/module/173
	* https://averoes12.com/file-system/
	* https://dosen.gufron.com/artikel/mengenal-sistem-file-file-system-linux/18/
	* http://achmad-zainuri.blogspot.com/2013/02/pengertian-file-system-dan-jenis-jenis.html