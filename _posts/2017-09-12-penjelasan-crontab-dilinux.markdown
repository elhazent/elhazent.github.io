---
layout: post
title: Crontab Linux Administrator
date: 2018-10-30 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: crontab.webp # Add image post (optional)
tags: [Productivity, Software] # add tag
---

Apa itu cron / atau crontab? Crontab adalah aplikasi daemon (Yang berjalan dibalik layar) yang digunakan untuk menjalankan tugas yang dijadwalkan pada suatu waktu di system operasi linux. Tugas yang dikenal dengan istilah *cronjobs* ini merupakan hal mendasar yang harus dipahami setiap System Administrator. Cronjobs sangat berguna untuk mengotomatiskan suatu script sehingga mereka dapat dijalankan diwaktu-waktu yang sudah terjadwalkan.  Crontab biasa digunakan untuk membuat backup secara otomatis, sinkronisasi files, dll.

**Cara Menginstall Crontab**

Bagi yang belum diinstall crontabnya, maka ketikan perintah berikut di terminal :

    $ sudo apt-get install cron

**Perintah Dasar Crontab**

* crontab -e = Mengubah atau Membuat file crontab jika belum ada.
* crontab -l = Menampilkan isi file crontab.
* crontab -r = Menghapus file crontab.
* crontab -v = Menampilkan waktu terakhir mengubah isi file crontab (Hanya tersedia dibeberapa sistem).\


**Crontab Parameters**

        # m h dom mon dow command

Baris yang dikomentariidi atas menampilkan tentang bagaimana crontab mendefinisikan setiap cronjobs.

**Daftar Parameters Crontab**

* m = Minute (menit)-0 sampai 59
* h = Hour (jam)-0 sampai 23
* dom = Day of mounth (tanggal)-0 sampai 31
* dow = Day 0f week (nomor hari)- 0 sampai 7

Berikuat grafik Untuk mempermudah :

    * * * * * perintah yang akan dieksekusi
    – – – – –
    | | | | |
    | | | | +—– day of week (0 – 7) (Sunday=0)
    | | | +——- month (1 – 12)
    | | +——— day of month (1 – 31)
    | +———– hour (0 – 23)
    +————- min (0 – 59)

Parameter-parameter di atas memungkinkan kita untuk membuat suatu jobs yang berjalan pada waktu-waktu tertentu. Setiap parameter yang dipilih dapat mengatur details waktu eksekusi sampai ke menit. Ada karakter khusus yang dapat membuat crontab lebih fleksibel.

**Karakter Khusus**

Kita dapat menggunakan karakter khusus disebuah cron untuk memperbolehkan pengguna menentukan interval waktu bagi sebuah job untuk dieksekusi. Karakter khusus ini dipakai di crontab untuk mendeklarasi cronjob.

* **Karakter khusus: Asterisk (bintang)**
Karakter Asterisk (bintang) merupakan karakter wild card yang dipakai untuk membuat sebuah job dijalankan setiap menit, setiap jam, setiap, hari, setiap bulan (tergantung posisi dimana ia ditulis, lihat grafik di atas).

Contoh :

        # * * * * * /home/user/script.sh

* **Karakter khusus: Koma**
Karakter koma saat kita ingin mengeksekusi sebuah job di dua waktu atau lebih. Contoh di bawah ini misalnya, kita ingin mengeksekusi /home/user/script.sh setiap menit ke 0, 15, dan 25.

Contoh : 

     # 0,15,25 * * * * /home/user/script.sh

* **Karakter khusus: Hyphen (-)**
Karakter - dipakai untuk memberikan jarak waktu antar eksekusi job.

Contoh :

     # 0-59 0-23 * * * /home/user/script.sh

* **Karakter khusus: Forward Slash (/)**

Karakter / dipakai jika kita ingin memberikan interval antar eksekusi job. Pada contoh di bawah ini kita ingin agar script.sh dieksekusi pada menit ke 0 lalu 20 kemudian 40 dan 60 (20 menit sekali.

Contoh :

    #*/20 * * * * /home/user/script.sh

**Contoh Crontab**
Sebagian besar crontab dapat memiliki metode sendiri dalam pembuatannya dengan menggunakan wild card atau mendefinisikan sebuah jarak.

* Setiap Menit Setiap Hari

        # m h dom mon dow command 
        * * * * * /home/user/script.sh

Atau

    # m h dom mon dow command
    0-59 0-23 0-31 0-12 0-7 /home/user/script.sh

* Setiap 5 menit pada pukul 6 pagi dimulai pada 6:07

    # m h dom mon dow command
    07-59/5 06 * * * /home/user/script.sh
    # Perintah ini  akan berjalan pada 6:07, 6:012, 6:17, 6:22, 6:27, seterusnya sampai 6:57

* Setiap Hari Tengah Malam

    # m h dom mon dow command
    0 0 * * * /home/user/script.sh

Atau 

    # m h dom mon dow command
    0 0 * * 0-7 /home/user/script.sh

Dan masih Banyak yang lainnya.

**Penggunaan String Khusus**

Kita juga dapat menggunakan string khusus sebagai pengganti kelima parameter di atas untuk memudahkan pembacaan.

* @reboot - Dijalankan sekali setiap kali sistem dihidupkan
* @yearly - Dijalankan sekali setahun 0 0 1 1 *
* @annually - Sama seperti @yearly
* @monthly - Dijalankan sekali sebulan 0 0 1 * *
* @weekly - Dijalankan sekali seminggu 0 0 * * 0
* @daily - Dijalankan setiap hari 0 0 * * *
* @midnight - Sama seperti @daily
* @hourly - Dijalankan setiap jam 0 * * * *

**Contoh Penggunaan String**

* Setiap Jam

        @hourly /home/user/script.sh

* Setiap Bulan

        @monthly /home/user/script.sh

Sekian dulu untuk penjelasan kali ini, dan jangan lupa baca juga tulisan yang lainnya.

    Referensi :
    * https://www.codepolitan.com/memahami-perintah-perintah-crontab-paling-lengkap-59f69445130a0
    * https://gosigitgo.wordpress.com/2010/03/18/tutorial-penggunaan-crontab-scheduler-di-ubuntu/
    * https://www.danlogs.com/2014/08/membuat-cron-jobs-di-linux




