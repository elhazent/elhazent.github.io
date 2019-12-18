---
layout: post
title: Install Docker di Ubuntu
date: 2018-12-04 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: dk-bg.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

### Pengertian

Perkembangan teknologi di zaman sekarang sudah tidak diragukan lagi begitu sangat cepat sehingga aplikasi yang tersedia pun begitu sangat beragam dan sangat banyak. Bagi developer, ketika mengembangkan sebuah aplikasi biasanya akan menjalankan virtualisasi pada server agar pembuatan aplikasi dapat berjalan di berbagai platform. Hal ini cukup ribet karena harus menyiapkan sebuah sistem operasi secara utuh.

Dengan adanya Docker,  hal tersebut dapat diminimalisir cukup baik. Docker adalah salah satu platform yang dibangun berdasarkan teknologi container. Docker merupakan sebuah project open-source yang menyediakan platform terbuka untuk developer maupun sysadmin untuk dapat membangun, mengemas, dan menjalankan aplikasi dimanapun sebagai sebuah wadah (container) yang ringan. Dengan sangat populernya docker, sebagian orang sering menganggap docker adalah sebutan lain untuk container.

Docker pertama kali dikembangkan oleh Solomon Hykes sebagai project internal di dotCloud bersama dengan beberapa koleganya seperti Andrea Luzzardi dan Francois-Xavier Bourlet. Perilisan platform ini secara open-source dilakukan pada mei 2013 silam. Docker terus berkembang hingga memiliki ribuan orang yang berkontribusi membuatnya menjadi lebih baik.

### Mengenal Istilah Pada Docker

**Docker Image**

Docker image merupakan template dasar untuk docker container. Image ini berisi sistem oeprasi ataupun aplikasi yang sudah selesai. Docker image ini berfungsi untuk menjalankan container.

**Docker Container**

Docker container merupakan sebuah image yang bersifat read-write. Pada setiap perubahan yang disimpan pada container akan menyebabkan terbentuknya layer baru di atas image. Developer dapat melakukan instalasi aplikasi didalamnya dan melakukan penyimpanan.

**Docker Registries**

Docker registries merupakan tempat penyimpanan (public atau private) di mana developer dapat mengunggah dan mengunduh image. Docker registries bersifat public disebut dengan Docker Hub. Disini, terdapat banyak image yang sudah dibuat atau image yang lain.

**Dockerfile**

Dockerfile merupakan script yang yang berisi dari serangkaian perintah yang akan dieksekusi secara otomatis dan berurutan untuk membuat sebuah image.

Dengan Docker, proses akan sangat ringan dan cepat dibandingkan dengan virtual mesin yang berbasis hypervisor. Besarnya overhead, hanya sebesar layanan aplikasi yang dijalankan pada container itu sendiri. Selain itu, para developer dapat menjalankan banyak container dalam mesin host.

### Installasi Docker di Ubuntu

**Step 1: Installasi Docker**

Paket instalasi Docker yang tersedia di repositori Ubuntu resmi mungkin bukan versi terbaru. Untuk memastikan kami mendapatkan versi terbaru, kami akan menginstal Docker dari repositori Docker resmi. Untuk melakukan itu, kami akan menambahkan sumber paket baru, tambahkan kunci GPG dari Docker untuk memastikan unduhan valid, dan kemudian instal paket.

Pertama, perbarui daftar paket Anda yang sudah ada:

    $ sudo apt update

Selanjutnya, instal beberapa paket prasyarat yang memungkinkan untuk menggunakan paket melalui HTTPS:

    $ sudo apt install apt-transport-https ca-certificates curl software-properties-common

Kemudian tambahkan kunci GPG untuk repositori Docker resmi ke sistem Anda:

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Tambahkan repositori Docker ke sumber APT:

    $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

Selanjutnya, perbarui paket database dengan paket Docker dari repo yang baru ditambahkan:

    $ sudo apt update

Pastikan Anda akan menginstal dari repo Docker bukan repo Ubuntu default:

    $ apt-cache policy docker-ce

Anda akan melihat output seperti ini, meskipun nomor versi untuk Docker mungkin berbeda:

    Output
    ● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
    Active: active (running) since Thu 2018-07-05 15:08:39 UTC; 2min 55s ago
     Docs: https://docs.docker.com
    Main PID: 10096 (dockerd)
    Tasks: 16
       CGroup: /system.slice/docker.service
           ├─10096 /usr/bin/dockerd -H fd://
           └─10113 docker-containerd --config /var/run/docker/containerd/containerd.toml

Instalasi Docker sekarang memberi Anda bukan hanya layanan Docker (daemon) tetapi juga utilitas baris perintah docker, atau klien Docker. Kami akan mengeksplorasi cara menggunakan perintah docker nanti di tutorial ini.

**Step 2: Melaksanakan Perintah Docker Tanpa Sudo (Opsional).**

Secara default, perintah docker hanya dapat menjalankan pengguna root atau oleh pengguna dalam grup docker, yang secara otomatis dibuat selama proses pemasangan Docker. Jika Anda mencoba menjalankan perintah docker tanpa mengawali dengan sudo atau tanpa di grup docker, Anda akan mendapatkan output seperti ini:

    Output
    docker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
    See 'docker run --help'.

Jika Anda ingin menghindari mengetik sudo setiap kali Anda menjalankan perintah docker, tambahkan nama pengguna Anda ke grup docker:

    $ sudo usermod -aG docker ${USER}

Untuk menerapkan keanggotaan grup baru, keluar dari server dan kembali, atau ketik yang berikut:

    $ su - ${USER}

Anda akan diminta untuk memasukkan kata sandi pengguna Anda untuk melanjutkan.

Konfirmasikan bahwa pengguna Anda sekarang ditambahkan ke grup docker dengan mengetik:

    $ id -nG

    Output
    sammy sudo docker

Jika Anda perlu menambahkan pengguna ke grup docker yang tidak Anda masuki, nyatakan bahwa nama pengguna secara eksplisit menggunakan:

    $ sudo usermod -aG docker username

Bagian lain dari artikel ini mengasumsikan Anda menjalankan perintah `docker` sebagai pengguna dalam grup docker. Jika Anda memilih untuk tidak, silakan tambahkan perintah dengan `sudo`.

**Step 3: Bekerja Dengan Docker Image**

Kontainer Docker dibangun dari Docker image. Secara default, Docker menarik image-image ini dari Docker Hub, registri Docker yang dikelola oleh Docker, perusahaan di belakang proyek Docker. Siapa pun dapat menyimpan Docker imageb mereka di Docker Hub, sehingga sebagian besar aplikasi dan distribusi Linux yang Anda perlukan akan memiliki image yang dihosting di sana.

Untuk memeriksa apakah Anda dapat mengakses dan mengunduh gambar dari Docker Hub, ketik:

    $ docker run hello-world

Output akan menunjukkan bahwa Docker bekerja dengan benar:

    Output
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    9bb5a5d4561a: Pull complete
    Digest: sha256:3e1764d0f546ceac4565547df2ac4907fe46f007ea229fd7ef2718514bcec35d
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.
    ...

Docker awalnya tidak dapat menemukan image `hello-world` secara lokal, jadi itu mengunduh image dari Docker Hub, yang merupakan repositori default. Setelah image diunduh, Docker membuat wadah dari image dan aplikasi dalam penampung yang dijalankan, menampilkan pesan.

Anda dapat mencari image yang tersedia di Docker Hub dengan menggunakan perintah **docker** dengan perintah pencarian. Misalnya, untuk mencari image Ubuntu, ketik:

    $ docker search ubuntu

Mesin akan menelusuri Docker Hub dan menampilkan daftar semua image yang namanya cocok dengan string pencarian. Dalam hal ini, hasilnya akan serupa dengan ini:

    NAME                                                      DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
    ubuntu                                                    Ubuntu is a Debian-based Linux operating sys…   7917                [OK]
    dorowu/ubuntu-desktop-lxde-vnc                            Ubuntu with openssh-server and NoVNC            193                                     [OK]
    rastasheep/ubuntu-sshd                                    Dockerized SSH service, built on top of offi…   156                                     [OK]
    ansible/ubuntu14.04-ansible                               Ubuntu 14.04 LTS with ansible                   93                                      [OK]
    ubuntu-upstart                                            Upstart is an event-based replacement for th…   87                  [OK]
    neurodebian                                               NeuroDebian provides neuroscience research s…   50                  [OK]
    ubuntu-debootstrap                                        debootstrap --variant=minbase --components=m…   38                  [OK]
    1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5      ubuntu-16-nginx-php-phpmyadmin-mysql-5          36                                      [OK]
    nuagebec/ubuntu                                           Simple always updated Ubuntu docker images w…   23                                      [OK]
    tutum/ubuntu                                              Simple Ubuntu docker images with SSH access     18
    i386/ubuntu                                               Ubuntu is a Debian-based Linux operating sys…   13
    ppc64le/ubuntu                                            Ubuntu is a Debian-based Linux operating sys…   12
    1and1internet/ubuntu-16-apache-php-7.0                    ubuntu-16-apache-php-7.0                        10                                      [OK]
    1and1internet/ubuntu-16-nginx-php-phpmyadmin-mariadb-10   ubuntu-16-nginx-php-phpmyadmin-mariadb-10       6                                       [OK]
    eclipse/ubuntu_jdk8                                       Ubuntu, JDK8, Maven 3, git, curl, nmap, mc, …   6                                       [OK]
    codenvy/ubuntu_jdk8                                       Ubuntu, JDK8, Maven 3, git, curl, nmap, mc, …   4                                       [OK]
    darksheer/ubuntu                                          Base Ubuntu Image -- Updated hourly             4                                       [OK]
    1and1internet/ubuntu-16-apache                            ubuntu-16-apache                                3                                       [OK]
    1and1internet/ubuntu-16-nginx-php-5.6-wordpress-4         ubuntu-16-nginx-php-5.6-wordpress-4             3                                       [OK]
    1and1internet/ubuntu-16-sshd                              ubuntu-16-sshd                                  1                                       [OK]
    pivotaldata/ubuntu                                        A quick freshening-up of the base Ubuntu doc…   1
    1and1internet/ubuntu-16-healthcheck                       ubuntu-16-healthcheck                           0                                       [OK]
    pivotaldata/ubuntu-gpdb-dev                               Ubuntu images for GPDB development              0
    smartentry/ubuntu                                         ubuntu with smartentry                          0                                       [OK]
    ossobv/ubuntu
    ...

Di kolom RESMI, OK menunjukkan image yang dibuat dan didukung oleh perusahaan di belakang proyek. Setelah Anda mengidentifikasi image yang ingin Anda gunakan, Anda dapat mengunduhnya ke komputer Anda menggunakan perintah `pull`.

Jalankan perintah berikut untuk mengunduh image `ubuntu` resmi ke komputer Anda:

    $ docker pull ubuntu

anda akan melihat output sebagai berikut :

    Output
    Using default tag: latest
    latest: Pulling from library/ubuntu
    6b98dfc16071: Pull complete
    4001a1209541: Pull complete
    6319fc68c576: Pull complete
    b24603670dc3: Pull complete
    97f170c87c6f: Pull complete
    Digest: sha256:5f4bdc3467537cbbe563e80db2c3ec95d548a9145d64453b06939c4592d67b6d
    Status: Downloaded newer image for ubuntu:latest


Setelah image diunduh, Anda dapat menjalankan penampung menggunakan image yang diunduh dengan perintah `run`. Seperti yang Anda lihat dengan contoh `hello-world`, jika image belum diunduh ketika docker dieksekusi dengan perintah `run`, Docker client akan terlebih dahulu mengunduh image, lalu menjalankan penampung yang menggunakannya.

Untuk melihat image yang telah diunduh ke komputer Anda, ketik:

    $ docker images

Output akan terlihat seperti berikut:

    Output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    ubuntu              latest              113a43faa138        4 weeks     ago         81.2MB
    hello-world         latest              e38bc07ac18e        2 months ago        1.85kB

Seperti yang akan Anda lihat nanti dalam tutorial ini, image yang Anda gunakan untuk menjalankan kontainer dapat dimodifikasi dan digunakan untuk menghasilkan image baru, yang kemudian dapat diunggah (di-push secara istilah teknis) ke Docker Hub atau pendaftar Docker lainnya.

Mari kita lihat cara menjalankan penampung secara lebih detail.

**Step 4: Menjalankan Docker Kontainer**

Kontainer `hello-world` yang Anda jalankan pada langkah sebelumnya adalah contoh kontainer yang berjalan dan keluar setelah memancarkan pesan uji. Kontainer bisa jauh lebih bermanfaat daripada itu, dan bisa interaktif. Lagi pula, mereka mirip dengan mesin virtual, hanya lebih ramah sumber daya.

Sebagai contoh, mari kita jalankan sebuah kontainer menggunakan image terbaru Ubuntu. Kombinasi switch -i dan -t memberi Anda akses shell interaktif ke dalam wadah: 

    $ docker run -it ubuntu

Shell perintah Anda akan berubah untuk mencerminkan fakta bahwa Anda sekarang bekerja di dalam penampung dan harus mengambil formulir ini:

    Output
    root@d9b100f2f636:/#

Perhatikan id kontainer di command shell. Dalam contoh ini, ini adalah `d9b100f2f636`. Anda memerlukan ID penampung nanti untuk mengidentifikasi penampung saat Anda ingin membuangnya.

Sekarang Anda dapat menjalankan perintah apa pun di dalam penampung. Sebagai contoh, mari kita perbarui paket database di dalam kontainer. Anda tidak perlu awalan perintah apa pun dengan `sudo`, karena Anda beroperasi di dalam penampung sebagai pengguna `root`:

    root@d9b100f2f636:/# apt update

Untuk keluar dari shell docker ketikan `exit`.

Untuk keluar dari wadah, ketik `exit` pada prompt.

**Step 5: Mengelola Kontainer Docker**

Setelah menggunakan Docker untuk sementara waktu, Anda akan memiliki banyak kontainer aktif (yang berjalan) dan tidak aktif di komputer Anda. Untuk melihat yang aktif, gunakan:

    $ docker ps

Anda akan melihat output yang serupa dengan yang berikut:

    Output
    CONTAINER ID        IMAGE               COMMAND             CREATED    

dalam tutorial ini, Anda memulai dua kontainer; satu dari image `hello-world` dan yang lain dari image `ubuntu`. Kedua kontainer tidak lagi berjalan, tetapi masih ada di sistem Anda.

Untuk melihat semua kontainer - aktif dan tidak aktif, jalankan `docker ps` dengan ditambah `-a`:

    $ docker ps -a

Anda akan melihat hasil yang serupa dengan ini:

    d9b100f2f636        ubuntu              "/bin/bash"         About an hour ago   Exited (0) 8 minutes ago                           sharp_volhard
    01c950718166        hello-world         "/hello"            About an hour ago   Exited (0) About an hour ago                       festive_williams

Untuk melihat penampung terbaru yang Anda buat, berikan saja perintah `-l`:

    $ docker ps -l


    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
    d9b100f2f636        ubuntu              "/bin/bash"         About an hour ago   Exited (0) 10 minutes ago                       sharp_volhard

Untuk memulai kontainer yang berhenti, gunakan perintah `docker start`, diikuti oleh ID kontainer atau nama kontainer. Mari kita mulai kontainer berbasis Ubuntu dengan ID `d9b100f2f636`:

    $ docker start d9b100f2f636

Kontainer akan dimulai, dan Anda dapat menggunakan `docker ps` untuk melihat statusnya:

    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    d9b100f2f636        ubuntu              "/bin/bash"         About an hour ago   Up 8 seconds                            sharp_volhard

Untuk menghentikan kontainer yang berjalan, gunakan perintah `docker stop`, diikuti oleh ID atau nama kontainer. Kali ini, kami akan menggunakan nama yang diberikan Docker pada kontainer, yaitu `sharp_volhard`:

    $ docker stop sharp_volhard

Setelah Anda memutuskan Anda tidak lagi membutuhkan kontainer lagi, hapus dengan perintah `docker rm`, lagi-lagi menggunakan ID kontainer atau nama. Gunakan perintah `docker ps -a` untuk menemukan ID atau nama penampung untuk penampung yang terkait dengan image `hello-world` dan hapus.

    $ docker rm festive_williams

Anda dapat memulai kontainer baru dan memberinya nama menggunakan tombol `--name`. Anda juga dapat menggunakan tombol `-rm` untuk membuat penampung yang menghapus dirinya sendiri ketika dihentikan. Lihat perintah bantuan menjalankan docker untuk informasi lebih lanjut tentang opsi ini dan lainnya.

Kontainer dapat diubah menjadi image yang dapat Anda gunakan untuk membuat kontainer baru. Mari kita lihat cara kerjanya.

**Step 6: Melakukan Perubahan Dalam Kontainer ke Image Docker**

Ketika Anda memulai image Docker, Anda dapat membuat, memodifikasi, dan menghapus file seperti yang Anda bisa dengan mesin virtual. Perubahan yang Anda buat hanya akan berlaku untuk kontainer itu. Anda dapat memulai dan menghentikannya, tetapi setelah Anda menghancurkannya dengan perintah `docker rm`, perubahan akan hilang selamanya.

Bagian ini menunjukkan cara menyimpan status penampung sebagai image Docker baru.

Setelah menginstal `wordpress` di dalam kontainer Ubuntu, Anda sekarang memiliki kontainer yang menjalankan image, tetapi Kontainer berbeda dari image yang Anda gunakan untuk membuatnya. Tetapi Anda mungkin ingin menggunakan kembali kontainer Node.js ini sebagai dasar untuk image baru nanti.

    $ docker commit -m "What you did to the image" -a "Author Name" container_id repository/new_image_name

Perintah `-m` adalah untuk pesan commit yang membantu Anda dan orang lain mengetahui perubahan apa yang Anda buat, sementara `-a` digunakan untuk menentukan pembuatnya. `Container_id` adalah judul yang Anda catat sebelumnya di tutorial ketika Anda memulai sesi Docker interaktif. Kecuali Anda membuat repositori tambahan di Docker Hub, repositori biasanya adalah nama pengguna Docker Hub Anda.

Misalnya, untuk pengguna `elhazent`, dengan ID kontainer `d9b100f2f636`, perintahnya adalah:

    $ docker commit -m "added wordpress_full" -a "sammy" d9b100f2f636 elhazent/wordpress_full

Saat Anda mengkomit image, image baru disimpan secara lokal di komputer Anda. Kemudian dalam tutorial ini, Anda akan belajar cara push image ke registri Docker seperti Docker Hub sehingga orang lain dapat mengaksesnya.

Mendata ulang image Docker lagi akan menampilkan image baru, serta yang lama yang berasal dari:

    $ docker images

Anda akan melihat output sebagai berikut:

    Output
    REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
    elhazent/wordpress_full   latest              7c1f35226ca6        7 seconds ago       179MB
    ubuntu                   latest              113a43faa138        4 weeks ago         81.2MB
    hello-world              latest              e38bc07ac18e        2 months ago        1.85kB

Dalam contoh ini, `wordpress_full` adalah image baru, yang berasal dari image `ubuntu` yang ada dari Docker Hub. Perbedaan ukuran mencerminkan perubahan yang dibuat. Dan dalam contoh ini, perubahannya adalah NodeJS dipasang. Jadi, kali berikutnya Anda perlu menjalankan kontainer menggunakan Ubuntu dengan NodeJS yang sudah terpasang sebelumnya, Anda cukup menggunakan image baru.

Anda juga dapat membuat image dari Dockerfile, yang memungkinkan Anda mengotomatiskan penginstalan perangkat lunak dalam image baru. Namun, itu di luar lingkup tutorial ini.

Sekarang mari berbagi image baru dengan orang lain sehingga mereka dapat membuat konatainer dari itu.

**Step 7: Push Image Docker ke Repository Docker**

Langkah logis berikutnya setelah membuat image baru dari image yang ada adalah membaginya dengan beberapa teman terpilih, seluruh dunia di Docker Hub, atau registri Docker lain yang dapat Anda akses. Untuk pushing image ke Docker Hub atau registri Docker lainnya, Anda harus memiliki akun di sana.

Bagian ini menunjukkan cara untuk pushing image Docker ke Docker Hub. Untuk mempelajari cara membuat registri Docker pribadi Anda sendiri, periksa Cara Mengatur Dokumentasi Docker Pribadi di Ubuntu 14.04.

Untuk pushing image Anda, pertama-tama masuk ke Docker Hub.

    $ docker login -u docker-registry-username

Anda akan diminta untuk mengotentikasi menggunakan kata sandi Docker Hub Anda. Jika Anda menentukan kata sandi yang benar, otentikasi harus berhasil.

> **Catatan**: Jika nama pengguna registri Docker Anda berbeda dari nama pengguna lokal yang Anda gunakan untuk membuat image, Anda harus menandai image Anda dengan nama pengguna registri Anda. Untuk contoh yang diberikan di langkah terakhir, Anda akan mengetik:
   
    $ docker tag elhazent/wordpress-full docker-registry-username/ubuntu-nodejs
>

Kemudian Anda dapat pushing image Anda sendiri menggunakan:

    $ docker push docker-registry-username/docker-image-name

Untuk pushing image `ubuntu-nodejs` ke repositori `elhazent`, perintahnya adalah:

    $ docker push elhazent/ubuntu-nodejs

Proses ini mungkin memerlukan waktu beberapa saat untuk mengunggah image, tetapi ketika selesai, hasilnya akan terlihat seperti ini:

    Output
    The push refers to a repository [docker.io/elhazent/wordpress_full]
    e3fbbfb44187: Pushed
    5f70bf18a086: Pushed
    a3b5c80a4eba: Pushed
    7f18b442972b: Pushed
    3ce512daaf78: Pushed
    7aae4540b42d: Pushed

    ...

Setelah pushing image ke registri, image akan terdaftar di dasbor akun Anda, seperti yang ditunjukkan pada gambar di bawah.

![Macbook]({{site.baseurl}}/assets/img/dk-1.png)

>**Referensi :**
>https://www.codepolitan.com/mengenal-teknologi-docker
>https://teknojurnal.com/pengertian-dan-istilah-pada-docker/
>https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04