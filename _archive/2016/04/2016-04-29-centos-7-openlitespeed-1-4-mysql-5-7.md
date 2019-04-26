---
title: CentOS 7, Openlitespeed 1.4 ve MySQL 5.7
date: 2016-04-29 TRT
layout: post
---

Merhaba okurlarım

Sonunda CentOS 7 yi kullanmak için güzel bir başlık buldum. Daha doğrusu bir istek üzerine hazırlıyorum bu başlığı. MySQL'i aslında anlatmaya gerek yok ama yüzeysel geçiyim. Kendisi açık kaynak kodlu bir database sunucusu yazılımı. Aynı zamanda çok işlekli olduğundan MSSQL'e oranla daha iyi. Bunun yanın da 4000-4500 sayfaya yakın administrator guide ı sayesinde istemediğiniz kadar bildi ile donatılıyorsunuz.

Openlitespeed ise, litespeedtech firmasına ait olup GPLv3 ile güvenceye alınan açık kaynak kodlu bir web sunucu yazılmıdır. Kullanılışı Apache, Nginx veya Lighttpd de ki gibi değil. Web kullanıcı arayüzü ile birçok işi yapıyorsunuz ki bu da bu yazlımı özel yapanlar arasında. Aynı zamanda aynı optimazsyonlar ile apache ye oranlar 30 kat daha hızlı tepki verebiliyor. Kullanıcı arayüzü oldukça sade ve kullanışlı. Bunun yanında web monitoring özelliğini de barındırıyor.

## CentOS 7 güncelleştirme, güvenlik ve optimizasyon

CentOS 7'de biz minimal sürümü fazlası ile yetecektir. Ayrıca belirtmek isterim bu işlemleri **root** kullanıcı olarak yapın.

```
yum update -y
```

güncelleme ilk işlemimizi yaptıralım. Ardından hiç kullanmayacağımız postfix'i kaldıralım.

```
systemctl stop postfix
yum remove postfix
```

Şimdi de ileride gerekecek uygulamaları da kuralım

```
yum install epel-release system-config-firewall-tui wget nano unzip
```

Buraya kadar geldiyseniz sistemi yeniden başlatmak iyi olacaktır.

```
reboot
```

Update sonrasında şişen ram'i azaltmamız gerekebilir. Onun önlemini almak için yaptık. Firewall kurallarını yapalım ama önce

```
systemctl firewalld stop
```

yaparak firewall daemon varsa durdurlsun yoksa bize hata verecektir zaten Şimdi tek tek firewall kurallarını girmekte. Biraz zordur ama emin olun işinize çok yaracaktır (güvenlik için gerekli).

```
system-config-firewall-tui
```

Şimdi önümüze mavi bir ekran, bordo butonlar var. Burada TAB tuşu ve yön tuşlarını kullanrak işlemler yapacağız. Bu kısmı fotoğraflar ile anlatmak istiyorum.

![](2016/05/centos_openlite_firewallgiris.png)

Burada yapacağınız işlem **boşluk** tuşununa basmanız yeterli. Böylelikle onu onaylamış oluyorsunuz. Alt taraftan **özelleştir** kısmına gelin ve sırası ile

* SSH
* WWW(HTTPS)
* WWW

Yapın burada eğer sunucunuz da ekstra birşey varsa diğerki portları da açmanız lazım. Ama önce sayfayı geçelim. **Forward** a basın ve **other ports** kısmında **add** kısmına gelin sırası ile

![](2016/05/centos_openlite_firewall7080.png)

![](2016/05/centos_openlite_firewall8088.png)

yaptıysanız tamam. Burada şimdi **Forward** a basarak geçin. Trusted Interfaces ,Masqerading ve Port Forwarding i de **Forward** a basarak geçin.

En son size ICMP için ne yapması gerektiğine danışacak burada yapacağınız işlem hepsini engellemek olucaksa -ki ben öyle yaparım özel bir durum olmadıkça- hepsini seçin.

![](2016/05/centos_openlite_firewallicmp.png)

Costum rules'unuz varsa buraya girin ve ardından **Close** diyerek en başa gelin ve burada **Tamam**'a basın ardından **Yes**'e basıp ayarlarınızı kayıt edersiniz.

ekranımızı temizlemek amacıyla

```
clean
```

## Openlitespeed 1.4, PHP5.6 kurulumu

```
rpm -ivh http://rpms.litespeedtech.com/centos/litespeed-repo-1.1-1.el7.noarch.rpm
yum install openlitespeed14
service lsws start
```

Openlitespeed sunucumuz kurldu ve en son komut ile de başlattık. Şimdi PHP yüklemey geldi.

```
yum install lsphp56 lsphp56-*
```

herzaman için güncel php yi kullanırım (PHP 7 daha geliştirme de). Ayrıca;

```
yum install lsphp53 lsphp53-*
yum install lsphp54 lsphp54-*
yum install lsphp55 lsphp55-*
```

Eski sürüm PHP isterseniz bunları da kullanabilirsiniz ama dediğim gibi 5.6 kullanmanızı tavsiye ederim.

```
ln -sf /usr/local/lsws/lsphp56/bin/lsphp /usr/local/lsws/fcgi-bin/lsphp5
```

Üsteki işlem sadece PHP5.6 içindir. Diğerki sürümler **56** yi değiştirseniz yeterli olacaktır.

## MySQL 5.7 kurulumu

```
rpm -ivh http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
yum install mysql-server
mysql_secure_installation
```

## Son adım

En son adım olarak arayüze girmek, Default web sitesine girmek olacak.
http://xxx.xxx.xx.xx:8088 sizin default web siteniz hatta burada PHP niz çalışıyor diye kontrol edebilirsiniz.

https://xxx.xxx.xx.xx:7080 ise sizin admin arayüzünüz giriş bilgileriniz.

* Kullanıcı adı: Admin
* Şifre: 123456

En sade kurulum bu. Gerisi artık size kaldı. MySQL'i daha açık bir şekilde farklı bir makale şeklinde alacağım. Sorularınız olursa yorumlar da bekliyorum.
