---
title: Ubuntu 14.04 LTS üzerinde OwnCloud 9 -SQLite
date: 2016-03-12 TRT
layout: post
---

Merhaba arkadaşlar,

Bir önce ki owncloud kurulumundan bir farkı yok. Ben yine kolaylık olsun diye
SQLite kullandım. Daha kurumsal bir kurulum yapacaksanız PostgreSQL veya MySQL
kullanmanızı öneririm.

önce gerekli olan modülleri yükleyelim

```shell
sudo apt-get install apache2 libapache2-mod-php5 php5-gd php5-json php5-sqlite php5-curl php5-intl php5-mcrypt php5-imagick php5-memcache
```

OwnCloud'un sitesinden tar.bz2 şeklinde indirip çıkartalım. Sonrada `cp` ile
copy edelim ve `/var/www/html` altına atalım bu işlem root kullanıcısı
gerektirir.

```shell
wget https://download.owncloud.org/community/owncloud-9.0.0.tar.bz2
tar -xjf owncloud-9.0.0.tar.bz2
sudo cp -r owncloud /var/www/html
```

Bu config OwnCloud ekibinin hazırladığı bir dosyadır. Sadece Nano ile girip
yapıştırın ardından kaydedin.


```apache
# /etc/apache2/sites-available/owncloud.conf

<Directory /var/www/html/owncloud/>
  Options +FollowSymlinks
  AllowOverride All

  <IfModule mod_dav.c>
    Dav off
  </IfModule>

  SetEnv HOME /var/www/html/owncloud
  SetEnv HTTP_HOME /var/www/html/owncloud

</Directory>
```

```shell
sudo chown -R www-data:www-data /var/www/html/owncloud/
sudo service apache2 restart
sudo a2nmod rewrite
```

Gerekli izinleri verip işlemimiz biter.

Dilerseniz UFW kullanarak

```shell
sudo ufw enable
sudo ufw allow 80/tcp
sudo ufw allow 22/tcp
sudo ufw reload
```

```shell
# /etc/default/ufw

...
IPV6 = no
...
```

CTRL+X 'E'

yaparsanız 22 (SSH) ve 80 (HTTP) portunu açarsınız.

Eğer bir sıkıntı yaşarsanız -ki yaşamayazsınız diye ümit ediyorum- bir önce ki
makaleme [link](/) bakıp sadece wget komutunu değiştirseniz yeterli olacaktır.

Ben ayrıca MySQL veya PostgreSQL için de ayrı bir makale yazmayı da düşünüyorum
