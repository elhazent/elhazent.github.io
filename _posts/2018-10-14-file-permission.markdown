---
layout: post
title: Modifing File And Folder Permission In Linux
date: 2018-10-29 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: linux-permissions.jpg # Add image post (optional)
tags: [Productivity, Software] # add tag
---

Kebanyakan sistem berkas memiliki metode untuk memberikan izin atau hak akses untuk pengguna tertentu dan kelompok pengguna. Sistem ini mengontrol kemampuan pengguna untuk melihat atau membuat perubahan pada isi filesystem.

### Mengenal Jenis User Permission di Linux

Di system operasi Linux terdapat 3 user permission, Yaitu :

* User (U) : Username pemilik file(owner)
* Group (G): Groupuser yang memiliki hak akses yang sama terhadap file.
* Other (O) : Pengguna yang bukan owner dan group.

### Jenis-Jenis Hak Akses

Di dalam system operasi linux terdapa 3(tiga) hak akses pada file atau folder, Yaitu :

* Read (r) = Akun ini memiliki akses read untuk melihat isi suatu file. misalnya dengan perintah cat.
* Write (w) = Akun ini memilik akses write, dengan kata lain bisa menulis ulang kembali suatu file ataupun menghapus file itu sendiri. Jadi jangan heran kalau file yang kita buat dengan membuat write kepada tiap group maupun other yg diberikan akses write bisa saja akan terhapus.
* Execute (x) = Akun ini memiliki akses untuk execute suatu file (File yang dimaksudkan disini adalah program atau script).

### Bagaimana Cara Melihat Hak Akses Di Linux(Ubuntu)?

**Pertama**, kita bisa melihat hak akses dari file dengan mengetikkan perintah di terminal

	$ ls -l

Maka hasilnya akan keluar seperti ini :

![Macbook]({{site.baseurl}}/assets/img/fp-01.png)


### Cara Mengatur Hak Akses

Kita dapat mengatur hak akses file dengan perintah chmod. Di chmod terdapat 2 mode yang bisa di gunakan untuk konfigurasi hak akses file yaitu dengan cara simbolik dan numerik.

#### 1. Cara Simbolik :

**Pertama** : readers harus memutuskan apakah readers mengatur hak akses untuk pengguna (u), kelompok (g), pengguna lainnya (o), atau ketiganya (a).

**Kedua** : readers bisa menambahkan izin (+), menghapus (-), atau menghapus izin sebelumnya dan menambahkan izin yang baru (=)

**Ketiga** : tentukan perizinannya. Apakah readers mengatur izin read (r), write (w), execute (e), atau ketiganya.

**Keempat** : readers hanya tinggal memberikan perintah untuk chmod, hak akses mana yang akan di rubah.

**Contoh :**

Kita mempunyai sebuah directory bernama 'rahasia' didalam direcrtory latihan   dan directory tersebut memiliki izin akses penuh pada semua kelompok (ada perintah ‘rwx’).

![Macbook]({{site.baseurl}}/assets/img/fp-02.png)

lalu kita hapus semua hak akses yang sekarang dan mengganti dengan hanya izin akses read saja untuk semua user dengan mengetikan perintah :

	$ chmod a=r rahasia

Maka tampilan akan menjadi seperti ini :

![Macbook]({{site.baseurl}}/assets/img/fp-03.png)

selanjutnya kita akan memberikan izin kepada Grup (G) untuk di tambahkan izin execute.
	
	$ chmod g+x rahasia

Maka tampilan menjadi seperti ini :

![Macbook]({{site.baseurl}}/assets/img/fp-04.png)

selanjutnya kita akan memberikan izin kepada semua user untuk di tambahkan izin write.

	$ chmod ugo+w rahasia

Tampilan menjadi seperti ini :

![Macbook]({{site.baseurl}}/assets/img/fp-05.png)

selanjutnya kita akan menghapus izin execute yang ada pada Grup (G) untuk di hapus.

	$ chmod g-x rahasia

Tampilan menjadi seperti ini :

#### 1. Cara Numerik :

Mode dimana diwakili oleh 3 angka octal untuk perizinan filenya.

* 4 = Untuk hak akses read(r)
* 2 = Untuk hak akses write(w)
* 1 = Untuk hak akses execute(x)
* 0 = tidak ada izin hak akses(-)

Jika ingin mendapatkan hak akses yang kita inginkan kita hanya tinggal menjumlahkan angka yang sesuai .

**Contoh :**

Kita ingin mendapatkan hak akses Read Write dan Execute secara bersamaan maka numeriknya menjadi seperti ini:

Read + write + execute

4 + 2 + 1 = 7

Kita ingin mendapatan hak akses read dan execute secara bersamaan maka numeriknya akan menjadi seperti ini:

Read + Execute

4 + 1 = 5

**Contoh penerapan pada syntx :**

	$ chmod 755 rahasia
	
Tampilan menjadi seperti ini :

![Macbook]({{site.baseurl}}/assets/img/fp-06.png)

Syntax diatas menunjukan hak akses untuk User adalah 7 (rwx), untuk grup adalah 5 (rx), dan untuk others  juga 5 (rx).
	
	Referensi :
	* http://iyungtux.blogspot.com/2014/12/mengenal-permission-file-di-linux.html
	* https://prithaparamesthia.wordpress.com/2013/11/27/file-permission-hak-akses-file-dan-manajemen-file-di-linux-ubuntu/
	* https://averoes12.com/modifing-file-folder-linux/