---
title: cPanel alternatifi bedava web paneller
date: 2016-06-14 TRT
layout: post
---

Merhaba okurlarım,

Öncelikle web paneller kimler için kimlere, ne için kullanılır gibi basit sorular ile başlamak istiyorum

## Neden web paneller?

Web panellerin amacı grafik arayüzü ile işinizi daha basitleştirmek ve web sitenizi daha hızlı yönetmek. Bunun yanında çok fazla bilgi olmadan tek tuş ile yönet...

## Hangi web panel?

Linux tarafı için konuşacağımı önceden belirtmek isterim. Linux tarafında malesef tek profesyonel alternatif cPanel. Ama ona bedava istemediğiniz çok panel var. Ayrıca cPanel açık kaynak kodlu bir panel değil ve RHEL (CentOS, RHEL, Cloudlinux) ürünlerine bir tek destek veriyor.

[https://www.youtube.com/watch?v=l2AVlwMICCc](https://www.youtube.com/watch?v=l2AVlwMICCc)

### Ajenti

Ajenti bence en etkili sunucu yönetim panelidir. Ayrıca videoda da kurulumunu göstermiş bulunmaktayım. Ajenti web sunucusu olarak NGINX veya Apache kullanıyor. Database yönetimi tarafı ise MySQL veya MongoDB. BIND9 DNS server bulunuyor üstünde. Dosya yöneticisi sayesinde basit bir şekilde upload, download edebilirsiniz. Güvenlik duvarı tarafı CSF veya IPTables. Malesef mail server özelliği bulunmuyor. En güzel yanlarından biri olan çok az kaynak kullanan python alt yapısı ile hazırlanmış. Açık kaynak kodlu olması da Ajenti kullanmanıza sebep

#### Artıları

* Çok yalın bir panel, widget ekleyerek yeteneklerini arttırabilirsiniz
* MySQL, NGINX ve PHP 5.6 ile süper bir web sitesi hazırlayabiliriniz 5-10 dakika da hazırlayabilirisniz
* Python alt yapılı olduğu için kod kısmını emin olun bilmeseniz de birşeyler kapıcaksınız (o kadar yalın yazılmış)
* Normal bir sunucu yönetimi için gerekli ürünleri size standart bir şekilde getiriyor

#### Eksileri

* NGINX veya Apache'den başka bir web server kurmak istiyorsanız malesef Ajenti size göre değil
* Mail server özelliği yok
* MySQL sunucuza bağlanmak için gerekli tool lar bulunmuyor.

### VestaCP

VestaCP çok işlevli bir panel ve Ajenti'ye oranla çok daha etkili. Tek sıkıntısı kaynak kullanımı. Sunucuz eğer ki 2GB ram ve 2 çekirdekten oluşmuyorsa, MySQL sorgularınız dan tutunda Apache isteklerinin yavaşlamasına kadar her türlü sorunu yaşarsınız. VestaCP neden yetenekli o kısımdan da bahsedip artı ve eksi yönlerine geçeyim. VestaCP tam tamına cPanel alternatifi. Normal de cPanel de MySQL database oluşturma, kullanıcı oluşturma, e posta kullanıcısı oluşturma, kota ayarlama gibi, kısaca web sunucusunun bütün hayati ürünleri bulunuyor. Fakat şöyle bir sorunumuz var. phpMyadmin, veya en kötü ihtimal ile bir webmail özelliği yok. Bu özellikleri sizin el ile apache web sunucunun içine eklemeniz gerek.

Ayrıca [link](https://demo.vestacp.com) den vestacp nin demosunu görebilirsiniz.

#### Artıları

* Mail, MySQL, spam ve virüs koruma ve bunun yanın da güzel ve kulanışlı bir arayüz
* Yetkili kullanıcı ekleyip, sunucuz üzerinden satış yapabilirsiniz. (Reseller paketlerde olduğu gibi)
* Kota yönetimi çok basit ve yalın.
* Yedek sistemi çok kulanışlı

#### Eksileri

* Çok fazla kaynak kullanmasını sıkıntı etmezseniz
* cPanel kadar güven verici değil
* Çok özellikli bir firewall'a sahip değil
* Spam ve Virüs koruması çok iyi değil
* phpMyadmin veya web mail gibi toollar yok.

### ISP Config

ISP Config en kapsamlı fakat bir o kadar da ağır olan web paneldir. Bence cPanel'e en çok benzeyen (görünüş olarak değil) web paneldir. Hatta cPanel de olmayan bir kaç özelliği (dahası vardır da araştırmak lazım) var. Bunlar,

* vServer - sanal bilgisayar kurmak için OpenVZ tabanlı web arayüzlü sistem
* Monitor - elbette cPanel de de var ama ISP Config kadar gelişmi değil.
* Reseller, User - satış yapacaksanız süper bir özelliğidir.

Ayrıca [link](http://www.ispconfig.org/ispconfig/online-demo) den ISP Config'in demosunu görebilirsiniz.

#### Artıları

* cPanel için en iyi alternatif
* cPanel de bulunmayan özellikleri var
* Admin, Reseller, User adında 3 yetki sistemi

#### Eksileri

* Çok ağır bir panel
* Öğrenmesi çok zaman alıyor
* Sıkınıcı bir arayüzü var
* Kurulumu fazlası ile zahmetli

### CWP - CentOS Web Panel

CWP, adı üsütnde aslında. RHEL ürünleri için hazırlanmış bir panel. Hafif amma velakin MySQL'i kapatırsanız, mail server özelliğini kapatırsanız hafif oluyor. Nedeni de basit aslında mail server kullanıcı başına 10 MB, spam veya virüs tarama özelliği açarsanız +30MB, MySQL ise database kurmasanız bile en az 500MB toplamı ise (tek kullanıcı için) 550MB çöp oldu. Ama bunun dışında çok hafif, kullanışlı bir arayüze sahip.

Ayrıca [link](http://centos-webpanel.com/demo) den CWP'nin demosunu görebilirsiniz

#### Artıları

* widget ile çok daha fazla özellik kısa bir sürede elde edebilirisniz.
* Çok yetenkli, bir web panel de istediğiniz her özellik var (phpmyadmin, pgmyadmin gibi)
* PHP Switcher, Apache veya NGINX web server, Vanish cache server kısaca web sunucunun hayati ürünleri
* Postfix & Dovecot, antispam antivirüs, roundcube web mail standart hale gelmiş mail server yazılımları
* Gelişmil firewall (CSF sayesinde)
* Backup yönetimi
* Çok güzel görünüşlü arayüze sahip

#### Eksileri

* Sadece CentOS, RHEL ve Cloudlinux da çalışıyor.
* Destek için ticket atmanız için malesef tek seferlik ücret ödemeniz (7$ zaten. Bu işe giriştiyseniz yapın) gerek.
* Cluster hayelleriniz varsa hiç düşünmeyin (veya düşünün ama aylık 35$)
* Öğrenilmesi gerek yoksa hemn döküman okumanız gerekecek

## Son söz

Ajenti, VestaCP, ISP-Config, CWP. Hepsi de birbirinden önemli özellikleri var hepsi kendisini öne çıkaran özelliği sayesinde tutuluyor. Benim önerim basit bir web sunucusu rolü ile iş yapacaksanız Ajenti. Daha etkili bir sunucu ise VestaCP. Bana VestaCP nin verdiği avantajlar işimi görmez diyorsanız ve ben RHEL ciyim diyorsanız (benim gibi) CWP. Ben CentOS cu falan değilim. Ubuntu taraftarıyım diyorsanız ise ISP-Config bütün işlerinizi görecektir.
