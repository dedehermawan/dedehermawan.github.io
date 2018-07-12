---
layout: post
title: "Cara install aplikasi di ubuntu"
date: 2017-08-24 09:44:20 +0700
comments: true
categories: Ubuntu
---
### .deb
Untuk menginstall file **.deb** melalui terminal console lakukan langkah-langkah berikut:
{% codeblock %}
sudo dpkg -i nama-file.deb
{% endcodeblock %}
Atau kamu bisa double-click file tersebut dan akan terbuka **Ubuntu Software Center**, maka kamu bisa install dengan mengklik tombol **Install**
### tar.gz
Untuk menginstall file **tar.gz** melalui terminal console lakukan langkah-langkah berikut:
{% codeblock %}
tar zxvf nama-file.tar.gz
{% endcodeblock %}
Terus masuk ke direktori tempat file hasil ekstrak kemudian baca file README atau INSTALL file tersebut sebagai petunjuk utama instalasi file.
 <!-- more -->
Tapi secara umum, sebagian besar instalasi paket tarbal (tar.gz atau tar.bz2) bisa melalui langkah-langkah berikut (lewat terminal)
{% codeblock %}
cd folder-ekstrak
./configure
{% endcodeblock %}
pastikan saat ini tidak ada masalah. Jika ada paket-paket lain yg harus diinstal, instal terlebih dulu paket-paket yg dibutuhkan.  
Lalu lakukan kompilasi
{% codeblock %}
make
{% endcodeblock %}
Lalu install(sebagai root)
{% codeblock %}
su
#make install
{% endcodeblock %}

