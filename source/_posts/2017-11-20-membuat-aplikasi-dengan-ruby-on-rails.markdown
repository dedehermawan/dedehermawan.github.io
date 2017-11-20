---
layout: post
title: "Membuat aplikasi dengan ruby on rails"
date: 2017-11-20 13:11:06 +0700
comments: true
categories: [rails]
---
Sebelumnya saya sudah memposting bagaimana cara untuk install ruby on rails atau lebih di kenal dengan `rails` saja, itu artinya sekarang kita akan mencoba membuat aplikasi pertamamu dengan rails, apabila ada yang belum menginstall ruby maupun rails nya silakan baca postingan tentang bagaimana cara menginstall ruby dan rails [disini](/blog/2017/11/18/install-ruby-on-rails-di-ubuntu-16-dot-04/)  
Oke kalau rails sudah terpasang di sistem kamu, langsung saja ketikkan perintah berikut di terminal
{% codeblock %}
rails new NamaAplikasi
{% endcodeblock %}
Perintah di atas otomatis akan membuat aplikasi rails dengan nama **NamaAplikasi**.  
Untuk mengetahui perintah lain pada saat mau membuat aplikasi rails silakan gunakan perintah berikut
{% codeblock %}
rails new -h
{% endcodeblock %}
Perintah tersebut akan menampilkan perintah-perintah apa saja yang bisa di gunakan pada saat mau *create* aplikasi baru dengan rails
<!--more-->
{% codeblock %}
Usage:
  rails new APP_PATH [options]

Options:
  -r, [--ruby=PATH]                                      # Path to the Ruby binary of your choice
                                                         # Default: /home/aliya/.rvm/rubies/ruby-2.3.1/bin/ruby
  -m, [--template=TEMPLATE]                              # Path to some application template (can be a filesystem path or URL)
  -d, [--database=DATABASE]                              # Preconfigure for selected database (options: mysql/oracle/postgresql/sqlite3/frontbase/ibm_db/sqlserver/jdbcmysql/jdbcsqlite3/jdbcpostgresql/jdbc)
                                                         # Default: sqlite3
  -j, [--javascript=JAVASCRIPT]                          # Preconfigure for selected JavaScript library
                                                         # Default: jquery
      [--skip-gemfile], [--no-skip-gemfile]              # Don't create a Gemfile
  -B, [--skip-bundle], [--no-skip-bundle]                # Don't run bundle install
  -G, [--skip-git], [--no-skip-git]                      # Skip .gitignore file
      [--skip-keeps], [--no-skip-keeps]                  # Skip source control .keep files
  -M, [--skip-action-mailer], [--no-skip-action-mailer]  # Skip Action Mailer files
  -O, [--skip-active-record], [--no-skip-active-record]  # Skip Active Record files
  -P, [--skip-puma], [--no-skip-puma]                    # Skip Puma related files
  -C, [--skip-action-cable], [--no-skip-action-cable]    # Skip Action Cable files
  -S, [--skip-sprockets], [--no-skip-sprockets]          # Skip Sprockets files
      [--skip-spring], [--no-skip-spring]                # Don't install Spring application preloader
      [--skip-listen], [--no-skip-listen]                # Don't generate configuration that depends on the listen gem
  -J, [--skip-javascript], [--no-skip-javascript]        # Skip JavaScript files
      [--skip-turbolinks], [--no-skip-turbolinks]        # Skip turbolinks gem
  -T, [--skip-test], [--no-skip-test]                    # Skip test files
      [--dev], [--no-dev]                                # Setup the application with Gemfile pointing to your Rails checkout
      [--edge], [--no-edge]                              # Setup the application with Gemfile pointing to Rails repository
      [--rc=RC]                                          # Path to file containing extra configuration options for rails command
      [--no-rc], [--no-no-rc]                            # Skip loading of extra configuration options from .railsrc file
      [--api], [--no-api]                                # Preconfigure smaller stack for API only apps

Runtime options:
  -f, [--force]                    # Overwrite files that already exist
  -p, [--pretend], [--no-pretend]  # Run but do not make any changes
  -q, [--quiet], [--no-quiet]      # Suppress status output
  -s, [--skip], [--no-skip]        # Skip files that already exist

Rails options:
  -h, [--help], [--no-help]        # Show this help message and quit
  -v, [--version], [--no-version]  # Show Rails version number and quit

Description:
    The 'rails new' command creates a new Rails application with a default
    directory structure and configuration at the path you specify.

    You can specify extra command-line arguments to be used every time
    'rails new' runs in the .railsrc configuration file in your home directory.

    Note that the arguments specified in the .railsrc file don't affect the
    defaults values shown above in this help message.

Example:
    rails new ~/Code/Ruby/weblog

    This generates a skeletal Rails installation in ~/Code/Ruby/weblog.
{% endcodeblock %}
Setelah kamu sukses membuat aplikasi tersebut berpindahlah ke folder aplikasi tersebut
{% codeblock %}
cd NamaAplikasi
{% endcodeblock %}
Lalu ketikkan perintah berikut untuk menjalankan aplikasi railsnya
{% codeblock %}
rails s
{% endcodeblock %}
Apabila di terminal muncul kata-kata seperti berikut
{% codeblock %}
=> Booting Puma
=> Rails 5.1.4 application starting in development 
=> Run `rails server -h` for more startup options
Puma starting in single mode...
* Version 3.11.0 (ruby 2.4.0-p0), codename: Love Song
* Min threads: 5, max threads: 5
* Environment: development
* Listening on tcp://0.0.0.0:3000
Use Ctrl-C to stop
{% endcodeblock %}
Itu tandanya kamu telah berhasil menjalankan aplikasi rails kamu, untuk mengeceknya silakan buka browser dengan alamat [http://localhost:3000](localhost:3000).  
Jika tampilan pada browser kamu seperti gambar di bawah ini.  
  
{% img left /images/rails-home.png 'image' 'images' %}
  
Berarti kamu sudah berhasil membuat aplikasi rails di komputermu.
