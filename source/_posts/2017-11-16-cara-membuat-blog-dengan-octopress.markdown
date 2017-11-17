---
layout: post
title: "Cara membuat blog dengan octopress"
date: 2017-11-16 15:33:08 +0700
comments: true
categories: Octopress
---

Sebelum mulai pastikan sistem anda  
1. Sudah terinstall Git  
2. Sudah terinstall ruby  
### Install Octopress
Buka terminal, lalu git clone dari repo Octopressnya
{% codeblock %}
git clone git://github.com/imathis/octopress.git octopress  
cd octopress
{% endcodeblock %}
Selanjutnya, Install dependecy
{% codeblock %}
gem install bundler
bundle install
{% endcodeblock %}
Install theme dafault dari Octopress
{% codeblock %}
rake install
{% endcodeblock %}
### Membuat post
{% codeblock %}
rake "new_post[Judul dari post]"
{% endcodeblock %}
Apabila di terminal muncul kata-kata `Creating new post: source/_posts/2017-11-02-judul-dari-post.markdown`  
itu tandanya kamu sudah berhasil membuat post

Untuk melihat hasil pembuatan post kita di browser caranya masukan perintah ini di terminal
{% codeblock %}
rake preview
{% endcodeblock %}
Apabila muncul kata-kata `>>> Compass is watching for changes. Press Ctrl-C to Stop.` di terminal  
Selanjutnya akses di browser dengan alamat `http://localhost:4000`  
untuk keluar dari mode preview tekan tombol Ctrl+c di keyboard  
### Deploy ke Github
Buat [repository baru di Github](https://github.com/repositories/new) dan beri nama repo tersebut dengan format `username.github.io`, dimana `username` tersebut adalah user name Github kamu atau nama organisasi.  
Github menggunakan branch master sebagai public directory di web server, tapi di octopress ini kamu bekerja di branch source oleh karena itu kamu harus commit dan push konten hasil generate ke github ke branch master, Untuk itu octopress memiliki perintah untuk konfigurasi yang akan membantu kamu menangani semuanya itu.
{% codeblock %}
rake setup_github_pages
{% endcodeblock %}
Perintah tersebut akan memintamu memasukaan alamat URL repo github kamu, (sebagai contoh masukan `git@github.com:username/username/github.io.git`)
Lalu jalankan
{% codeblock %}
rake generate
rake deploy
{% endcodeblock %}
Jangan lupa untuk commit source dari blog kamu
{% codeblock lang:ruby %}
git add .
git commit -m "pesan kamu"
git push origin source
{% endcodeblock %}