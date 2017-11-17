---
layout: post
title: "koneksi ke github dengan SSH"
date: 2017-11-17 23:02:54 +0700
comments: true
categories: [github]
---
### Tentang SSH
Menggunakan SSH kamu dapat terhubung dan mengotentifikasi untuk meremote server dan service, dengan SSH keys, kamu dapat terhubung ke Github tanpa harus menginputkan username dan password setiap kali mengunjunginya.
### Cek ketersediaan SSH keys
Buka terminal  
Ketikkan `ls -al ~/.ssh` untuk melihat apakah SSH keys sudah tersedia atau belum
{% codeblock %}
ls -al ~/.ssh
# List the file in your .ssh directory, if they exist
{% endcodeblock %}
Cek daftar direktori untuk melihat apakah kamu sudah mempunyai public SSH key.  
Secara default, nama file dari public keys biasanya  
* id_dsa.pub  
* idecdsa.pub  
* id_ed25519.pub  
* id.rsa.pub  
Apabila kamu tidak memiliki pasangan public dan private key, atau tidak ada satupun yang terhubung ke Github, maka langkah pertama adalah **generate SSH key baru**  
Tapi apabila kamu memiliki pasangan public dan private key (contoh *id_rsa_pub* dan *id_rsa*) maka yang harus kamu lakukan adalah tambahkan SSH key kamu ke ss-agent  
### Generate SSH key
Pastekan text dibawah ini, ganti alamat emailnya dengan alamat email Github kamu
{% codeblock %}
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
{% endcodeblock %}
Ini akan membuat SSH key baru, dengan menggunakan email yang telah di daftarkan sebelumnya sebagai label
{% codeblock %}
Generating public/private rsa key pair.
{% endcodeblock %}
Silakan isi pertanyaan yang muncul (passphrase bisa di kosongkan juga)
{% codeblock %}
Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
{% endcodeblock %}
### Tambahkan SSH key ke ssh-agent
{% codeblock %}
eval "$(ssh-agent -s)"
# Agent pid 59566
ssh-add ~/.ssh/id_rsa
{% endcodeblock %}
### Tambahkan SSH key ke akun Github
Copy dulu SSH key di *id_rsa_pub* ke clipboard.  
Login ke Github dan klik profile foto di kanan atas, lalu klik **setting** -> **SSH and GPG keys** -> **New SSH key** atau **Add SSH key**  
Di kolom title masukkan deskripsi label untuk key baru tersebut, lalu pada kolom key pastekan SSH key yang sudah di copy di *id_rsa_pub* sebelumnya, klik **Add SSH key** jika muncul pertanyaan silakan masukkan  password Github anda  
Untuk mengecek apakah SSH key kita sudah terhubung ke Github silakan masukan perintah di bawah ini di terminal
{% codeblock %}
ssh -T git@github.com
# Attempts to ssh to GitHub
{% endcodeblock %}
Dan apabila muncul pesan seperti berikut itu tandanya kamu sudah berhasil menghubungkan SSH key ke github
{% codeblock %}
Hi username! You've successfully authenticated, but GitHub does not
provide shell access.
{% endcodeblock %}
