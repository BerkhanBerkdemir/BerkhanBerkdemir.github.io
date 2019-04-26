---
title: Ubuntu 14.04 LTS üzerinde OwnCloud 8.2 kurulumu - SQLite
date: 2016-02-21 TRT
layout: post
---

Merhabalar,

Yazdığım bir önce ki 14.04 de bir sorun fark ettim. Sistem çalışmıyor. Daha doğrusu ben mysql ile alakalı bir yanlış yaptım. Bu yüzden de beyaz ekran geliyor ve web sitesi yüklenmiyor.

Tekrardan kurdum sistemi ve mysql database engine kullanmadım. SQLite ile bütün işi yaptım. Elbette Mysql kadar güven verici değil.

Video da aslına çoğu şey anlaşılır. Önerileriniz olursa benimle paylaşın.

[https://youtu.be/gHD2qNEGD8w](https://youtu.be/gHD2qNEGD8w)

```shell
sudo apt-get update && sudo apt-get upgrade
```

```shell
# /etc/network/interfaces

auto lo eth0
iface eth0 inet static
address 192.168.1.200
netmask 255.255.255.0
network 192.168.1.0
broadcast 192.168.1.255
gateway 192.168.1.1
dns-nameservers 208.67.222.222
dns-nameservers 208.67.220.220
```

CTRL+X ile kaydedip çıkın

```shell
sudo reboot
```

adress, netmask, network, broadcast, gateway, dns-nameservers lar tab (yani 4 boşluk) yapmak zorundasınız.

```shell
sudo apt-get install apache2 libapache2-mod-php5 php5-gd php5-json php5-sqlite php5-curl php5-intl php5-mcrypt php5-imagick php5-memcache
```

```shell
wget http://download.owncloud.org/community/owncloud-8.2.2.tar.bz2
sudo tar -xjf owncloud-8.2.2.tar.bz2
sudo cp -r owncloud /var/www/html
```

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

burayı kopyalayın ve alttaki kaydedip çıkın
CTRL+X 'E'

```shell
sudo chown -R www-data:www-data /var/www/html/owncloud/
sudo service apache2 restart
sudo a2nmod rewrite
```

```shell
sudo ufw enable
sudo ufw allow 80/tcp
sudo ufw allow 22/tcp
sudo ufw reload
```

```
# /etc/default/ufw

...
IPV6 = no
...
```

CTRL+X ve E ye basarak onaylayın
