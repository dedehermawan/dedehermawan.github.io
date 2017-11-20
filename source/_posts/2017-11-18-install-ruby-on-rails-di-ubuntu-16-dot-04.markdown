---
layout: post
title: "Install Ruby on Rails di Ubuntu 16.04"
date: 2017-11-18 22:06:42 +0700
comments: true
categories: [ruby, rails]
---
### Install Ruby
Untuk memastikan kita memiliki semua yang diperlukan untuk dukungan Webpacker di Rails, pertama-tama kita tambahkan repository NodeJs dan Yarn ke sistem kita sebelum menginstall.
{% codeblock %}
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev nodejs yarn
{% endcodeblock %}
Selanjutnya kita akan menginstall ruby dengan menggunakan salah satu dari 3  cara, yaitu yang pertama yang paling banyak di gunakan untuk install ruby yaitu menggunakan `rbenv`, yang kedua menggunakan `rvm` dan yang ketiga adalah dengan cara langsung mengambil dari sumbernya.<!-- more -->
Tapi karena saya menggunakan rvm untuk menginstall ruby di sistem saya maka saya akan membahas install ruby dengan rvm saja hhe..untuk cara selain rvm kamu bisa lihat [disini](https://gorails.com/setup/ubuntu/16.04#ruby).  
Oke untuk menginstall ruby dengan rvm masukan perintah ini di terminal.
{% codeblock %}
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.4.0
rvm use 2.4.0 --default
{% endcodeblock %}
Coba perhatikan potongan perintah di atas `rvm install 2.4.0` itu artinya kita menginstall ruby dengan versi 2.4.0, kamu bisa cek versi lain/terbaru dari ruby [disini](https://www.ruby-lang.org/en/downloads/).  
Langkah terakhir jalankan install bundler
{% codeblock %}
gem install bundler
{% endcodeblock %}
Coba sekarang cek apakah ruby sudah terinstall dengan benar
{% codeblock %}
ruby -v
# ruby 2.4.0p0 (2016-12-24 revision 57164) [x86_64-linux]
{% endcodeblock %}
Apabila muncul kata-kata seperti di atas maka berarti proses instal ruby kamu berhasil.  
### Install Rails
Semenjak Rails mengikutsertakan banyak dependency akhir-akhir ini, kita butuh menginstall Javascript Runtime seperti NodeJS, Ini memungkinkan kamu menggunakan Coffeescript dan Asset Pipeline di Rails yang menggabungkan dan meminimalkan javascript untuk menyediakan production environment secara lebih cepat.  
Untuk menginstall NodeJs, kita akan menambahkannya dengan menggunakan ofisial repositori
{% codeblock %}
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodej
{% endcodeblock %}
Selanjutnya install Rails dengan gem
{% codeblock %}
gem install rails
{% endcodeblock %}
Sekarang coba cek dengan menjalankan `rails -v` untuk memastikan semuanya terinstal dengan benar
{% codeblock %}
rails -v
# Rails 5.1.4
{% endcodeblock %}
Dan lagi-lagi apabila muncul kata-kata `Rails 5.1.4` berarti proses instal rails kamu sukses.  
  
Oke sekian penjelasan mengenai bagaimana cara menginstall ruby on rails di ubuntu, untuk postingan selanjutnya kita akan mencoba bagaimana membuat web dengan menggunakan framework Rails, jadi tetap ikuti blog saya ini ya
