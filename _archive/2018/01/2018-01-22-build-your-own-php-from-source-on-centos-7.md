---
title: Build your own PHP from source on CentOS 7
date: 2018-01-22
updated: 2018-03-25
layout: post
tags: CentOS
---

Hello guys,

Today I'm gonna write about PHP (php-fpm) installation from source codes. Yes, we know PHP is not compiled language but behind scene, when you are installing PHP you have to compile it like I'll do.

But, this is not big deal. I'm serious.  I will use CentOS (7.4.1153) for in this article.

Let's start.

## Install some dependencies

You can install new updates with `yum update -y` but I will just update my server repo packages with `yum makecache`. In container system you have to that because you don't want to see 1GB container size for small web application.

I have to download `libmcrypt-devel` that's why I will install _epel-release_ with `yum install -y epel-release`

and you will install those packages

```bash
yum install -y gcc gcc-c++ libxml2-devel pkgconfig openssl-devel bzip2-devel curl-devel libpng-devel libjpeg-devel libXpm-devel freetype-devel gmp-devel libmcrypt-devel mariadb-devel aspell-devel recode-devel autoconf bison re2c libicu-devel libwebp-devel libjpeg-turbo-devel freetype-devel libmcrypt-devel perl
```

> If you are using composer (Package Dependency Manager, after version 1.6) you can check PHP extension requirements with this way.
> `composer check-platform-reqs`

after that you can install those extensions.

## Let's download source file

In this stage you can use wget but, I am using cURL because this is default for CentOS/RHEL system. Let's download it.

```bash
curl -sSJOL "http://us3.php.net/distributions/php-7.1.13.tar.xz"
```

I usually download source files to /tmp folder. I recommend this way because you won't use it again. Right?

```bash
mkdir /tmp/source
mv php-7.1.13.tar.xz /tmp/source/php.tar.xz
cd /tmp/source
tar -xf php.tar.xz # we will decompress it without output
rm -f php.tar.xz # we won't use it again
mv php /usr/src/php # we will compile it over there (/usr/src/php)
cd /usr/src/php
```

### Configure it

Now we will configure it right now with `./configure`

```bash
./configure \
    --prefix=/usr/local/php \
    --with-config-file-path=/usr/local/php/etc \
    --with-config-file-scan-dir=/usr/local/php/etc/conf.d \
    --enable-bcmath \
    --with-bz2 \
    --with-curl \
    --enable-filter \
    --enable-fpm \
    --with-gd \
    --enable-gd-native-ttf \
    --with-freetype-dir \
    --with-jpeg-dir \
    --with-png-dir \
    --enable-intl \
    --enable-mbstring \
    --with-mcrypt \
    --enable-mysqlnd \
    --with-mysql-sock=/var/lib/mysql/mysql.sock \
    --with-mysqli=mysqlnd \
    --with-pdo-mysql=mysqlnd \
    --with-pdo-sqlite \
    --disable-phpdbg \
    --disable-phpdbg-webhelper \
    --enable-opcache \
    --with-openssl \
    --enable-simplexml \
    --with-sqlite3 \
    --enable-xmlreader \
    --enable-xmlwriter \
    --enable-zip \
    --with-zlib \
    --with-webp-dir \
    --with-xpm-dir
```

Yess, first stage successful. If you got an error, you can google it. Most of error means you didn't download right package (for dependencies). For example, if you wanted to use php-gd you have to download freetype-devel etc.

### Make it

Second stage you compile it with `make`

I'm gonna use this line

```bash
make -j$(nproc)
```

-j means worker also known as CPU cores. I am using i5-3320M physically 2 cores but you can see if you are run `nproc` 4. That's why I'm using nproc. It is to easy to use.

This process can take ten minutes or 1 minutes depends on your system/CPU

### Test it (Optional)

If you are using for development machine it is not neceserly, but I'm doing for this stuff (testing) when I install to server. This is optional. It can take over then ten minutes

```bash
make test
```

### Install it

Now, system ready to install the php to /usr/local/php/

```bash
make install
```

> This tutorial not provide any security solution. You have to do that when you are install new server like iptable, directory owners or permissions...

## Final shoot

You can use development configuration file (php.ini-development) or default production configuration file. I will use production configuration file.

Other lines of codes you have to do.

```bash
mkdir /usr/local/php/etc/conf.d
cp /usr/src/php/php.ini-production /usr/local/php/lib/php.ini
cp /usr/src/php/sapi/fpm/www.conf /usr/local/php/etc/php-fpm.d/www.conf
cp /usr/src/php/sapi/fpm/php-fpm.conf /usr/local/php/etc/php-fpm.conf
```

## Last words

```bash
/usr/local/php/bin/php -v
```

When you are run it you will see PHP version 7.1.13.

If you have a problem/error let me know. I can help you about that. Contact with me with disqus.
