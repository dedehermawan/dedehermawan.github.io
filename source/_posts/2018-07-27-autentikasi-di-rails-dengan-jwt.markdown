---
layout: post
title: "autentikasi di rails dengan JWT"
date: 2018-07-27 08:17:06 +0700
comments: true
categories: [rails, api]
---
Sudah lama ni saya tidak update blog saya ini, ya mungkin karena saya tidak pandai dalam hal menulis blog sih hhe..

Oke untuk sekarang ini saya akan mencoba menulis tentang membuat aplikasi web berbasis **api** menggunakan rails. Disini saya akan sekaligus membuat aplikasi api terkait autentikasi menggunakan gem [JWT](https://jwt.io).  
Oke langsung saja kita membuat proyek rails app nya
{% codeblock %}
rails new auth_jwt --api -T -d postgresql
{% endcodeblock %}
Setelah proyek selesai di generate langsung saja masuk ke direktori app tersebut "**auth_jwt**".  

Selanjutnya  kita buat model **User** untuk kepentingan autentikasi, disini kita gunakan atribut email dan password _digest sebagai dasar dari model User 
{% codeblock %}
rails g model user email password_digest
rake db:migrate
{% endcodeblock %}
## Validation
Untuk proses create user kita tambahkan validasi pada model **app/model/user.rb**
```ruby
class User < ApplicationRecord
  validates_presence_of :email
  validates_uniqueness_of :email, case_sensitive: false
  validates_format_of :email, with: /@/
```
## Hash password
Untuk hash password kita gunakan gem '**bcrypt**', silakan kamu tambahkan gem 'bcrypt' di file **Gemfile**
```ruby
...
gem 'bcrypt'
...
```
lalu tambahkan sintak dibawah ini pada **app/model/user.rb**
```ruby
class User < ApplicationRecord
  has_secure_password
  ...
```
Supaya format email berupa huruf kecil semua dan menghilangkan spasi pada email, kita buat _callback_ method di **app/model/user.rb**
```ruby
class User < ApplicationRecord
  ...
  ...
  before_save :downcase_email

  def downcase_email
    self.email = self.email.delete(' ').downcase
  end
```
## User create 
Sekarang kita akan buat endpoint untuk method user create
{% codeblock %}
rails g controller users
{% endcodeblock %}
tambahkan sintak di bawah ini di **config/routes.rb**
```ruby
resources :users, only: :create
```
Selanjutnya kita buat method create di **app/controllers/users_controller.rb**
```ruby
def create
  user = User.new(user_params)

  if user.save
    render json: {status: 'User created successfully'}, status: :created
  else
    render json: {errors: user.errors.full_messages}, status: :bad_request
  end
end

private

def user_params
  params.require(:user).permit(:email, :password, :password_confirmation)
end
```
Sekarang coba kamu buat user dengan mengirimkan request **POST** ke alamat http://localhost:3000/users menggunakan curl di terminal
{% codeblock %}
curl -d '{"user": {"email": "test@email.com", "password": "12345", "password_confirmation": "12345"}}' -H "Content-Type: application/json" -X POST http://localhost:3000/users
{% endcodeblock %}
Jika respon yang dihasilkan adalah seperti dibawah ini, berarti proses create user kamu berhasil
{% codeblock %}
{"status":"User created successfully"}
{% endcodeblock %}
## Confirmation
Disini kita akan membuat proses konfirmasi email mungkin tidak terlalu kompleks tetapi bisa mewakili proses konfirmasi itu sendiri, proses konfirmasi ini di perlukan apabila waktu mau login tetapi email belum di verifikasi maka user tidak akan bisa login.

Oke pertama-tama kita buat migration untuk menambahkan atribut pada model user / field pada tabel users
{% codeblock %}
rails g migration add_confirmation_email_to_users confirmation_token confirmed_at:date confirmation_sent_at:date
rake db:migrate
{% endcodeblock %}
tambahkan _callback_ method **generate_confirmation_instructions** di **app/model/user.rb**, untuk menggenerate berupa string random pada field confirmation_token dan menggenerate waktu pada saat user itu di create pada field confirmation_sent_at.
```ruby
class User < ApplicationRecord
  ...
  ...
  before_create :generate_confirmation_instructions

  ...
  ...
  def generate_confirmation_instructions
    self.confirmation_token = SecureRandom.hex(10)
    self.confirmation_sent_at = Time.now.utc
  end
```
Sekarang kita tambahkan routes **confirm** pada **config/routes**
```ruby
resources :users, only: :create do
  collection do
    post 'confirm'
  end
end
```
Lalu kita buat method **confirm** di **users_controller.rb**
```ruby
...
def confirm
  token = params[:token].to_s

  user = User.find_by(confirmation_token: token)
  
  if user.present && user.confirmation_token_valid?
    user.mark_as_confirmed!
    render json: {status: 'User confirmed successfully'}, status: :ok
  else
    render json: {status: 'Invalid token'}, status: :not_found
  end
end
...
```
Oke sekarang kita coba proses confirm di atas dengan mengirimkan POST ke url **localhost:3000/users/confirm** dengan di sertakan data **token** berdasarkan isi dari field **confirmation_token**
{% codeblock %}
curl -d '{"token" = "1c2c2aea02e3b03fd0e1"}' -H "Content-Type: application/json" -X POST http://localhost:3000/users/confirm
{% endcodeblock %}
Apabila muncul keterangan seperti dibawah ini berarti proses konfirmasi berhasil
{% codeblock %}
{"status":"User confirmed successfully"}
{% endcodeblock %}
