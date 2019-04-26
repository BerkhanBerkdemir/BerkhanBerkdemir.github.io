---
title: Ubuntu 14.04 LTS, LAMP
date: 2016-05-19 TRT
layout: post
---

Merhaba arkadaşlar,

Bu sefer Ubuntu'dan gideceğim ve OpenSuSE, CentOS ve Fedora içinde LAMP kurulumları yapacağım. Aynı zaman da <a href="http://linuxkafasi.org/2016/04/29/centos-7-openlitespeed-1-4-mysql-5-7/" target="_blank">CentOS 7, Openlitespeed ve MySQL kurulumu</a> da bakabilirsiniz.


Bu LAMP'i öncelikle tanıtmam gerek. Linux-Apache-MySQL-PHP anlamına gelen, kısaca bir web sunucusu için vazgeçilmez ürünleri temsil ediyor.

Öncelikle Apache'den bahsetmek isterim. Kendisi linux tarafından en çok kullanılan, açık kaynak kodlu, (biraz hantal ama fazlası ile iş görüyor), topluluk tarafından güvenlik yamaları hazırlanan bir sunucu yazılımıdır. Hantal dememin sebebi, litespeed veya nginx yanında çok geç cevap vermesi, sıkıştırma konusunda biraz başarısızlık yaşamasından dolayı dedim. Ama bu site gibi veya basit bir iş siteniz için fazlası ile yetecek özellik barındırıyor.

MySQL ise çoğu kurulumda da anlatmaktan kendimi alamadığım bir sunucu yazılımı. Kendisi içinde 5-6 dan fazla motor bulunduran, açık kayank kodlu, çok izlekli, herhangi bir limiti olmayan (daha doğrusu o limitlere henüz ulaşamayan), SQL sorgulamaları yapan sunucu yazılımı. MySQL aslında MariaDB olarak kullanabilirsiniz ama benim önerim MySQL ile devam etmeniz olacak. O yüzden ben CentOS da bile MySQL taraftarıyımdır.

PHP, web sitelerin dinamik olması için kullanılan dildir. En bilindik PHP ile hazırlanan site Facebook aklıma geliyor. PHP kullanım alanı malesef web sunucusu taraflı yazılır (sunucu taraflı betik denir).

Ürünleri kısaca tanıttım, şimdi de kuruluma geçelim.

Öncelikle Ubuntunun sayfasından 14.04 LTS server sürümünü indirelim

```shell
sudo -i
apt-get update && apt-get upgrade -y
reboot
```

Ne olur olmasın diye biz güncellemeri yapalım ve sistemi yeniden başlatsın. Ardından Apache ve PHP nin kurulumları ile başlayalım.

```shell
sudo -i
$ apt-get install apache2 php5
```

Bu kadar basit. Geriye kaldı MySQL 5.6 kurmak.

```shell
apt-get install mysql-server-core-5.6
```

veya

```
apt-get install mysql-server-5.6
```

Aralında ki fark şu. Üstte ki sadece sunucu rolü var. Yani localhost üzerinden sunucuyu yönetemezsiniz ki bu sadece web sunucu kullanıcıları için kötü bir seçenek. Ama en güvenlisi, en hızlısı ve en az yer kaplayan versiyonudur. Ama alttaki eğer siz basit bir sunucu yönetcekseniz ve komut arayüzüne ihtiyacınız varsa malesef en altta ki ni kurmanız gerekecektir.

İlk web sitemizi hatırlayalım.

```php
<?php
  # /var/www/html/info.php
  phpinfo();
?>
```

CTRL+X ardında "E" veya "Y" ile kayıt işlemini kayıt edin. Ve bilgisayarınızdan bir web browserver açıp, http://<span style="color: #ff0000;">xxx.xxx.xx.xx</span>/info.php enterlayın. Ve karşısında PHP'niz hakkında detaylı bilgilere kavuşacaksınız. İşiniz bittikten sonra bu dosyayı silin.

```shell
rm /var/www/html/info.php
```

Aynı zaman da UFW den basit güvenlik duvarı ayarlarını da hemen halledelim.

```shell
ufw enable
ufw default deny incoming
ufw default allow outgoing
ufw deny mysql
ufw deny https
ufw allow http
service ufw restart
```

aynı zamanda MySQL'e nasıl bağlantı kuracağınızı da belirtiyim

```
mysql_secure_installation
```

Burada şifrenizi girin ve her aşamada "Y" ile yanıt verin ki bu sunucunuz için en doğrusu olucaktır.

```
mysql -u root -p
```

Ardından size MySQL şifresi sorucak. Girin ve artık MySQL arayüzündesiniz. Buradan kullanıcı ekleyebilir, Database ekleyip silebilir kısaca MySQL'iniz buradan yöneteceksiniz. Ayrıntıları ben MySQL hakkında yazacağım bir makalede belirteceğim. Çıkmak isterseniz de

```
exit
```

veya

```
quit
```
