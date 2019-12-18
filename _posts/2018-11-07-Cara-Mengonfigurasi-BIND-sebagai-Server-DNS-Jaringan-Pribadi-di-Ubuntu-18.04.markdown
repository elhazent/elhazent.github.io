---
layout: post
title: Konfigurasi Bind Sebagai Server DNS Jaringan Pribadi Di Ubuntu 18.04
date: 2018-11-07 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: dns-bg.jpg # Add image post (optional)
tags: [Productivity, Software] # add tag
---

### Pengertian

BIND adalah singkatan dari bahasa inggris dari Berkeley Internet Name Domain. Adalah salah satu software yang biasa digunakan untuk membuat, membangun dan mengatur sebuah DNS(Domain Name Server) pada sistem operasi linux. BIND awalnya dibuat oleh empat orang mahasiswa di CSRG Universitas California Berkeley dan pertama kali dirilis di dalam 4.3BSD. Paul Vixie kemudian meneruskan pengembangannya pada tahun 1988 saat bekerja di DEC.
Bagian terpenting dari pengelolaan konfigurasi server dan infrastruktur termasuk cara mudah untuk mencari antarmuka jaringan dan alamat IP berdasarkan nama, Dengan menyiapkan Domain Name System (DNS) yang tepat. Menggunakan nama domain yang sepenuhnya memenuhi syarat (FQDN), bukan alamat IP, untuk menentukan alamat jaringan memudahkan konfigurasi layanan dan aplikasi, dan meningkatkan pemeliharaan file konfigurasi. Menyiapkan DNS kita sendiri untuk jaringan pribadi kita adalah cara yang bagus untuk meningkatkan pengelolaan server kita.

### Syarat Dan Ketentuan

Untuk menyelesaikan tutorial ini, kita akan memerlukan infrastruktur berikut. Buat setiap server di pusat data yang sama dengan jaringan pribadi yang diaktifkan:

* Server Ubuntu 18.04 berfungsi sebagai server DNS Primer(utama), ns1
* (Recomended) Server Ubuntu 18.04 kedua berfungsi sebagai server DNS Sekunder, ns2
* Server tambahan di pusat data yang sama yang akan menggunakan server DNS Anda

Pada masing-masing server ini, konfigurasikan akses administratif melalui pengguna sudo dan firewall dengan mengikuti panduan penyiapan awal server Ubuntu 18.04 kami.

### Install BIND Pada Server DNS

Pada kedua server, kita di anjurkan untuk memperbarui package kita dengan mengetikan :

    $ sudo apt-get update

Setelah Update, Lalu kita install software yang kita butuhkan yaitu BIND :

    $ sudo apt-get instal bind9

### Setting BIND Ke Mode IPv4

Sebelum lanjutkan ke langkah selanjutnya, kita atur terlebih dahulu BIND-nya ke mode IPv4 karena jaringan pribadi menggunakan IPv4 secara ekslusif. Di kedua server, edit file pengaturan default bind9 dengan mengetikan :

    $ sudo nano /etc/default/bind9

Tambahkan "-4" pada akhir parameter OPTIONS. Seperti dibawah ini :

Save dan close kalau sudah selasai.

Restart BIND dengan perintah :

    $ sudo systemctl restart bind9

Sekarang BIND sudah terpasang, Mari kita ke langkah selanjutnya.

### Konfigurasi Server DNS Pertama (Utama)

Ada beberapa langkah pada konfigurasi server DNS pertama ini :

* **Konfigurasi File Options**

Buka file `named.conf.options` untuk di edit :

    $ sudo nano /etc/bind/named.conf.options

Pada file diatas kita tambahkan text berikut sebelum `options` :

    acl "trusted" {
        10.128.10.11;    # ns1 - can be set to localhost
        10.128.20.12;    # ns2
        10.128.100.101;  # host1
        10.128.200.102;  # host2
    };

Lalu pada konfigurasi `options` kita tambahkan text berikut :

    options {
        directory "/var/cache/bind";

        recursion yes;                 # enables resursive queries
        allow-recursion { trusted; };  # allows recursive queries from "trusted" clients
        listen-on { **Ip Adress kita**; };   # ns1 private IP address - listen on private network only
        allow-transfer { none; };      # disable zone transfers by default

        forwarders {
                8.8.8.8;
                8.8.4.4;
        };
    };

Ketika sudah selesai, save dan tutup file `named.conf.options`. Konfigurasi di atas menentukan bahwa hanya server kita sendiri (yang "tepercaya") yang dapat meminta query server DNS kita untuk domain luar.

Selanjutnya, kita akan mengkonfigurasi file lokal, untuk menentukan zona DNS kami.

* **Konfigurasi File Local**

Buka file `named.conf.local` untuk kita edit :

    $ sudo nano /etc/bind/named.conf.local

masukan text berikut :

    zone "nyc3.example.com" {
    type master;
    file "/etc/bind/zones/db.nyc3.example.com"; # zone file path
    allow-transfer { 10.128.20.12; };           # ns2 private IP address - secondary
    };
    
    zone "128.10.in-addr.arpa" {
    type master;
    file "/etc/bind/zones/db.10.128";  # 10.128.0.0/16 subnet
    allow-transfer { 10.128.20.12; };  # ns2 private IP address - secondary
    };

>Dengan asumsi bahwa subnet pribadi kami adalah 192.168.100.31, tambahkan zona reverse dengan dengan baris berikut (perhatikan bahwa nama zona reverse kami dimulai dengan "168.192" yang merupakan pembalikan oktet dari "192.168").

* **Membuat Lanjutan File Zona**
Lanjutan file zona adalah tempat kami menentukan catatan DNS untuk pencarian DNS ke depan. Yaitu, ketika DNS menerima query nama, "host1.nyc3.example.com" misalnya, DNS akan melihat dalam file zona lanjutan untuk menyelesaikan alamat IP pribadi host1.

Mari kita buat direktori tempat file zona kita akan berada. Menurut konfigurasi named.conf.local kami, lokasi itu harus / etc / bind / zones:

    $ sudo mkdir /etc/bind/zones

Kami akan mendasarkan file lanjutan zone kami pada file sample db.local zone. Salin ke lokasi yang tepat dengan perintah berikut:

    $ sudo cp /etc/bind/db.local /etc/bind/zones/db.nyc3.example.com

Sekarang mari kita edit file forward zone kita:

    $ sudo nano /etc/bind/zones/db.nyc3.example.com

Awalnya, akan terlihat seperti berikut:

    $TTL    604800
    @       IN      SOA     localhost. root.localhost. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      localhost.      ; delete this line
    @       IN      A       127.0.0.1       ; delete this line
    @       IN      AAAA    ::1             ; delete this line

Pertama, Hapus Seluruh isi file tersebut lalu kita ganti dengan text berikut :

    $TTL    604800
    @       IN      SOA     ns1.nyc3.example.com. admin.nyc3.example.com. (
                  3     ; Serial
             604800     ; Refresh
              86400     ; Retry
            2419200     ; Expire
             604800 )   ; Negative Cache TTL
    ;
    ; name servers - NS records
     IN      NS      ns1.nyc3.example.com.
     IN      NS      ns2.nyc3.example.com.

    ; name servers - A records
    ns1.nyc3.example.com.          IN      A       Ip Address kita
    ns2.nyc3.example.com.          IN      A       Ip Address kita

    ; 10.128.0.0/16 - A records
    host1.nyc3.example.com.        IN      A      Ip Address kita
    host2.nyc3.example.com.        IN      A      Ip Address kita

* **Membuat File Reverse Zone**

File zona reverse adalah tempat kami menentukan catatan PTR DNS untuk pencarian DNS terbalik. Yaitu, ketika DNS menerima kueri berdasarkan alamat IP, "192.168.100.31" misalnya, akan terlihat dalam file zona reverse (s) untuk menyelesaikan FQDN yang sesuai, "host1.nyc3.example.com" dalam kasus ini .

Pada ns1, untuk setiap reverse zone yang ditentukan dalam file named.conf.local, buat file reverse zone. Kami akan mendasarkan file zona reverse kami (s) pada file zona sampel db.167. Salin ke lokasi yang tepat dengan perintah berikut (mengganti nama file tujuan sehingga cocok dengan definisi zona reverse Anda):

    $ sudo cp /etc/bind/db.127 /etc/bind/zones/db.10.128

Lalu kita rename file `db.10.128` menjadi `Ip subnet reverse`, Sebagai contoh punya kami ip subnetnya adalah 192.168, maka di balik menjadi 168.192,maka file tersebut diberi nama `db.192.168`.

Kita edit file zona reverse tersebut dengan menghapus seluruh isi file dengan menggatinya dengan text berikut:

    $TTL    604800
    @       IN      SOA     nyc3.example.com. admin.nyc3.example.com. (
                              3         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
    ; name servers
      IN      NS      ns1.nyc3.example.com.
      IN      NS      ns2.nyc3.example.com.

    ; PTR Records
    11.10   IN      PTR     ns1.nyc3.example.com.    ; Ip Address kita
    12.20   IN      PTR     ns2.nyc3.example.com.    ; Ip Address kita
    101.100 IN      PTR     host1.nyc3.example.com.  ; Ip Address kita
    102.200 IN      PTR     host2.nyc3.example.com.  ; Ip Address kita

Setelah edit file zone reverse lalu kita cek file kita untuk mengetahui ada error atau tidak.

* **Memeriksa Sintaks Konfigurasi BIND**

Jalankan perintah berikut untuk memeriksa file `named.conf` :

    $ sudo named-checkconf

Jika file `named.conf` kita tidak memiliki kesalahan sintaks, kita akan kembali ke prompt shell Anda dan tidak melihat pesan kesalahan. Jika ada masalah dengan file `named.conf`, periksa kembali kesalahan pada bagian "Konfigurasi DNS Server Utama", kemudian jalankan kembali perintah di atas.

Perintah bernama-checkzone dapat digunakan untuk memeriksa kebenaran file zona kita. Argumen pertamanya menentukan nama zona, dan argumen kedua menentukan file zona terkait, yang keduanya didefinisikan di `named.conf.local`.

Sebagai contoh, untuk memeriksa "nyc3.example.com" konfigurasi zona lanjutan, jalankan perintah berikut (ubah nama untuk mencocokkan forward zone dan file kita):

    $ sudo named-checkzone nyc3.example.com db.nyc3.example.com

Dan untuk memeriksa "128.10.in-addr.arpa" konfigurasi zona reverse, jalankan perintah berikut (ubah angka agar sesuai dengan zona reverse dan file Anda):

    $ sudo named-checkzone 128.10.in-addr.arpa /etc/bind/zones/db.192.128

Ketika semua file konfigurasi dan zona kita tidak memiliki kesalahan di dalamnya, kita harus restart layanan BIND kalau sudah mengedit.

* **Restart Layanan BIND**

Restart BIND dengan mengetikan perintah berikut :

    $ sudo systemctl restart bind9

Dan untuk mengaktifkan firewall kita jalankan perintah berikut :

    $ sudo ufw allow Bind9

Server DNS utama Anda sekarang sudah siap dan siap untuk merespons permintaan DNS.

### Konfigurasi DNS Client

Konfigurasi DNS client hanya dengan mengubah dns nya di file  `resolv.conf`

    $ sudo nano /etc/resolv.conf

Lalu tambahkan text berikut :
    
    nameserver Ip Address kita
    nameserver Ip Address kita
    search nyc3.example.com

### Test Server

Untuk mengetest apakah dns server kita berjalan atau tidak jalankan perintah berikut:

    $ ping ns1.nyc3.example.com

`ns1.nyc3.example.com` ini adalah file contoh yang saya buat.

    Referensi :
    * https://id.wikipedia.org/wiki/BIND
    *https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-ubuntu-18-04
    * https://linuxacademy.com/cp/courses/lesson/course/1789/lesson/1/module/173