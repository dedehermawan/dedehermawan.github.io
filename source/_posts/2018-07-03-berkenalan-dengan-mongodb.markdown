---
layout: post
title: "Berkenalan dengan MongoDB"
date: 2017-11-23 13:35:14 +0700
comments: true
categories: [mongodb]
---
## Apasih MongoDB?
MongoDB merupakan sebuah database yang memiliki konsep _NoSQL_. Istilah ini dapat diartikan secara awam dengan non relasional karena berbeda dengan MySQL yang merupakan RDBMS (_Relational DataBase Management System_).

Untuk memulai berkenalan kamu terlebih dahulu harus mengetahui beberapa perbedaan yang mendasar antara MongoDB dengan RDBMS, diantaranya:

* _Table_ pada MongoDB dikenal dengan _Collections_
* _Rows_ pada MongoDB dikenal dengan _Documents_
* Setiap _documents_ bisa berisi kolom yang berbeda dengan _documents_ lainnya
* Sebuah _collections_ dapat membuat setiap _documents_ memiliki kolom yang sama dengan membuat parameter capped menjadi true saat pembuatan _collections_
* Query yang digunakan oleh MongoDB tidak menggunakan bahasa query seperti SQL, tapi menggunakan Javascript. Bahkan Anda dapat membuat semacam _stored procedure_ yang ditulis menggunakan Javascript
* Secara default setiap membuat _documents_ baru, id dari _documents_ tersebut akan tercipta otomatis. Jadi Anda tidak perlu membuat id sendiri jika membutuhkan id
* dan masih banyak lagi
<!--more-->
## Instalasi MongoDB
Untuk proses instalasi sudah dijelaskan secara jelas di official [web MongoDB nya](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)  
Apabila proses instalasi sudah selesai selanjutnya cek apakah MongoDB sudah terpasang dengan benar atau belum dengan mengetikan perintah di bawah ini:
{% codeblock %}
mongo --version
mongod --version
{% endcodeblock %}
{% img /images/mongo-version.png 'image' 'images' %}

apabila muncul tampilan seperti gambar diatas berarti MongoDB sudah berhasil terpasang di _system_ kita
## Cara mengoperasikan MongoDB
Menyalakan server MongoDB
{% codeblock %}
sudo service mongod start
{% endcodeblock %}
Mematikan server MongoDB
{% codeblock %}
sudo service mongod stop
{% endcodeblock %}
Menyalakan ulang server MongoDB
{% codeblock %}
sudo service mongod restart
{% endcodeblock %}
Melihat status server MongoDB
{% codeblock %}
sudo service mongod status
{% endcodeblock %}
## Mengakses server MongoDB
Jalankan **mongo** _shell_ di mesin yang sama dengan **mongod**. Gunakan perintah **--host** untuk spesifikasi alamat localhost dan port dari **mongod**
{% codeblock %}
mongo --host 127.0.0.1:27017
{% endcodeblock %}
Secara _default_ database ketika kita masuk ke server MongoDB namanya adalah _test_
{% img /images/sintaks-db.png 'image' 'images' %}  
Berikut penjelasan gambar diatas

* **db**, untuk melihat database yang sedang aktif
* **show dbs**, untuk melihat daftar database
* **use &lt;nama-database&gt;** untuk membuat database baru, (database belum tersimpan karena data masih kosong)

Sekarang ayo kita membuat sebuah koleksi(_collections_). Koleksi berisi kumpulan dokumen atau data dalam bentuk JSON, kalau di SQL kita menyebutnya dengan _record_/baris  
Koleksi bisa di buat dengan perintah:
{% codeblock %}
db.createCollections("nama_koleksi")
{% endcodeblock %}
Atau bisa juga otomatis terbuat pada saat _insert_ data 
{% codeblock %}
db.<koleksi>.insert(<data>)
{% endcodeblock %}
atau
{% codeblock %}
db.<koleksi>.save(<data>)
{% endcodeblock %}

* koleksi adalah nama koleksi yang akan dibuat
* data adalah data yang akan disimpan ke dalam koleksi dengan format JSON

Sebagai contoh kita akan membuat koleksi dengan nama buku, **db.koleksi.insert**
{% img /images/collection-insert.png 'image' 'images' %}  
Menampilkan semua data pada koleksi, **db.koleksi.find().pretty()**, pretty() berfungsi untuk mempercantik format tampilan JSON supaya lebih mudah di baca
{% img /images/collection-find.png 'image' 'images' %}  
Menampilkan data pada koleksi berdasarkan kondisi/query, **db.koleksi.find({query}).pretty()**
{% img /images/collection-find-kondisi.png 'image' 'images' %}  
Mengubah data menggunakan perintah _update_, **db.koleksi.update({query}, {data-baru})**
{% img /images/collection-update.png 'image' 'images' %}  
Diatas kita mengupdate buku dengan judul "Belajar membaca" ditambahkan harga senilai 15000, sehingga apabila kita tampilkan ulang data dengan judul "Belajar membaca" akan memiliki harga seperti yang di insertkan  

{% img /images/collection-find-update.png 'image' 'images' %}  
Untuk menghapus koleksi gunakan perintah, **db.koleksi.remove({query})**
{% img /images/collection-hapus.png 'image' 'images' %}  
Apabila kita ingin menghapus semua data dalam koleksi, kita kosongkan saja nilai query-nya
## Menghapus database dan koleksi
menghapus koleksi
{% codeblock %}
db.koleksi.drop();
{% endcodeblock %}
Menghapus database
{% codeblock %}
db.dropDatabase();
{% endcodeblock %}
Mungkin cukup sekian dulu perkenalan dengan MongoDB nya, semoga bermanfaat.
