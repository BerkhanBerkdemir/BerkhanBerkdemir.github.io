---
title: OpenSuSE 13.2 ve Teamspeak Server 3.0.12.3
date: 2016-04-27 TRT
layout: post
---

Merhaba arkadaşlar,

Biraz farklı bir işletim sistemi ile gideceğim. Ubuntu da Teamspeak kurulumu çok basit olduğundan ve çok fazla makale bulunduğundan farklı bir işletim sistemi ile yapacağım. Öncelikle anlatmak isterim bu işletim sistemini.

Öncelik OpenSuSE, SuSE firmasına ait olup tamamı ile bedava. Aynı RHEL'in Fedora'sı gibi (CentOS farklı bir konu). Türkçe desteğini SuSE Linux 8.0 da bile süper olan bir işletim sistemi. YaST (Yet another Setup Tool anlamına geliyor) SuSE yi özelleştiren bir parçası. RPM paket yönetimi ile de beslenebilir. Yeter ki SuSE için hazırlansın. OpenSuSE nin en sevdiğim yanı YaST yazılımına burada da önem verilmiş. Birçok yapılandırmayı text'ler ile değilde TUI (Text User Interface) ile yaparsınız (CentOS veya RHEL de ki "network-tui" veya `system-config-firewall-tui` gibi). Elbette Ubuntu veya CentOS da ki gibi grafik arayüze de sahip. KDE, Gnome gibi bilindik arayüzlere de bulunuyor. Ama ben sunucu için text arayüzü kullanılmasını tavsiye ederim.

Teamspeak ise bir VoIP ürünü. VoIP olmasına karşın içinde dosya yöneticisi bile var. Çok basit ve kullanışlı olan yazılım mumble gibi lisansız değil. Lisansız versiyonu 32 kişi ve 1 Virtual Server desteği veriyor. Eğer ürünüzü kayıt ederseniz 512 kişi 2 Virtual Server desteği alabilirsiniz.

Artık OpenSuSE 13.2 kurulumuna geçelim. Ben server kurulumu yapacağımdan text arayüzü kullanacağım. En yalın hali ile kuracağım.

## OpenSuSE kurulum, Sistem günceleme ve Firewall ayarları

![](2016/05/suse_teamspeak_kurulumAyarlari.png)

Ben aynı üstteki görselde ki gibi yapacağım kurulumu (SSH ve FW de ki SSH izini aktive ettim sadece). Fazla birşeye gerek yok. Zaten Teamspeak gerekli herşeyi barındırıyor. İleri dediğiniz anda kuruluma başlayacaktır.

![](2016/05/suse_teamspeak_login.png)

Bilgisayarınızı yeninden başlatıcaksınız ve "Boot From Harddisk" diyerek ilereyeceksiniz. Ardında karşısınıza 2-3 (duruma göre değişir) OK veya Failed gösterecek. (aynı resimde ki gibi). Mümkün mertebe Failed diyenleri gözden kaçırmayın.

![](2016/05/suse_teamspeak_loginRoot.png)

Bu ekran geldikten sonra size (kurulum esnasında girdiğiniz hesab adı ve şifresi) hesap adı ve şifresini isteyecektir. Bunları girin ve şu an sistemdesiniz. Ardından,

```
berkhan@linux-ctcw:~> sudo -i
```

diyerek root hesabı ile giriş yaptık ki devamlı "sudo" yazmaya gerek kalmasın. Tabiki bunu yazdığınızda şifre de isteyecektir sizden.

![](2016/05/suse_teamspeak_update.png)

Önce update işlemlerini yapalım ki sonrada bizi uğraştırmasın (çoğu uygulamasını kullanmaycağız ama güvenlik açıklıkları varsa onları kapatmak için gerekli).

```
linux-ctcw:~ # zypper refresh
linux-ctcw:~ # zypper update
Continue? [y/n/? shows all options] (y): y
linux-ctcw:~ # yast
```

![](2016/05/suse_teamspeak_yast.png)

Şimdi yast ekranındayız. Buraya girmeniz için Root kullanıcı olmanız gerektiğini bir kere daha söyleyeyim. Öncelikle gireceğimiz yer "Security and Users" ekranında "Firewall" sekmesine gelin.

![](2016/05/suse_teamspeak_securityAndUsers.png)

YaST ekranına alışmak zordur ama bir kere alışırsanız işinizi çok kolaylaştıracak. (TAB ve Fonksiyon tuşlarını etkili bir şekilde kullanmak için altta bilgilendirmeler var) Firewall altından "Costum Rule" enter'e basarak girin.

![](2016/05/suse_teamspeak_costumRules.png)

TAB ile diğer tarafa geçin ve ok tuşları ile "Add" kısmına gelin

Aynen yukarıda ki gibi tek tek girecesiniz aşağıda ki portları (external zone altında yapıcaksınız bu işlemleri)

* 10011/TCP çıkış
* 30033/TCP çıkış
* 9987/UDP çıkış

Aynen bu şekilde olmalı

![](2016/05/suse_teamspeak_firewall10011.png)

![](2016/05/suse_teamspeak_interfacesExternalZone.png)

Eğer burada ki gibi External zone yapmazsanız sizin Firewall kurallarınız işletilmez.

## Teamspeak indirme ve kurulum

![](2016/05/suse_teamspeak_wget.png)

```
linux-ctcw:~ # wget http://ftp.4players.de/pub/hosted/ts3/releases/3.0.12.3/teamspeak3-server_linux_x86-3.0.12.3.tar.bz2
```

wget komutu ile bulunduğunuz dosya yoluna tar.bz2 formatında bir dosya indirecek. Burada yapacağımız işlem tar.bz2 dosyasını açmak.

```
linux-ctcw:~ #tar -jxvf teamspeak3-server_linux_x86-3.0.12.3.tar.bz2
```

Eğer bir yola çıkarmak isterseniz,

```
linux-ctcw:~ # tar -jxvf teamspeak3-server_linux_x86-3.0.12.3.tar.bz2 -C /home/berkhan/
```

home dan sonra "tab" tuşuna basmanız size ait olan dosya yolunu gösterecektir. (Eğer çoklu kullanıcı varsa kendi dosya adınızı girmeniz gerekcektir)

```
linux-ctcw:~ # mv /home/berkhan/teamspeak3-server_linux_x86/ /home/berkhan/ts3
```

önce ismini biraz kısaltalım ki zorlaştırmasın işimizi. Sonra dosyayı nereye çıkardıysanız, klorsörün içine gireceksiniz. Önceden belirtiyim.

> Eğer alttaki opsiyonelleri yapacaksanız start komutunu çalıştırmayın. İşnizi zorlaştırmasın.

```
linux-ctcw:/home/berkhan/ts3 # ./ts3server_startscript.sh start
```

komutunu işleterek sunucumuzu başlatıyoruz. Gerekli şifre ve privileges keyini alın ve IP adresine bağlanın (öğrenmek istiyorsanız ifconfig veya ip addr). Şimdi buraya kadar yaptıysanız gerisi (bence) en basit kısmı. Ayrıca belirtiyim altta ki kısım Teamspeak'in daha stabil ve otomatik çalışması için yazıldı. Altta yapacağım Güvenlik optimizasyonları sizin alacağınız saldırının **en fazla %10-15** ile karşı çıkabilir. Daha fazla Güvenlik ipucusu için makale mi bekleyin derim.

## Diğer optimizasyonlar (OPSIYONEL)

### Cron konfigrasyon

Init için çok fazla scipt yazmışlar. Ben bash bilmediğimden dolayı ve internette istediğiniz kadar ts3 bash script bulacağınızdan direk cron ile yapacağım. Ama size tavsiyem sadece "autoCrash" gibi olayları kontrol edecek bash ler yazabilirsiniz/bulabilirsiniz. Ben direk Cron işine dalıyorum :)

Öncelikle şunu belirtiyim.

```
linux-ctcw:/home/<span style="color: #ff0000;">berkhan</span>/ts3 # crontab -e
```

```
@reboot /home/berkhan/teamspeak3/ts3server_startscript.sh start
10 4 * * 0 /home/berkhan/teamspeak3/ts3server_startscript.sh stop
12 4 * * 0 tar -cvpzf /home/berkhan/backup/ts3backup-$(date +%Y-%m-%d).tar.gz2 /home/berkhan/teamspeak3
20 4 * * 0 /home/berkhan/teamspeak3/ts3server_startscript.sh start
```

Eğer /home/berkhan/backup adında bir klosözrünüz yoksa

```
linux-ctcw:/home/berkhan/ts3 # mkdir /home/berkhan/backup
```

İşlemi ile yeni bir dosya oluşturabilirsiniz. Üstteki cronjob ile yacağınız işlemler;

1. Sistem kapanıp açıldığında teamspeak3 başlatıcalacak
2. Her ayın pazar günü saat 4.10 da sistemi durdurup 4.12 de sıkıştırma işlemine başlayacak ve aynı günün 4.20 de ise ts3 ü tekrar başlatacak.

Cron için daha birçok şey yapabilirsiniz. Ama bu kadarı basit bir TS için fazla bile.

## Static IP atama

OpenSuSE'de aynı Ubuntu da veya RHEL' de ki gibi nano veya vim ile açarak da yapabilirsiniz ip atamasını. Ama OpenSuSE de YaST gibi bir nimet varken kimse o text editörler ile uğraşmak istemez.

```
linux-ctcw:~ # yast
```

Tekrar YaST arayüzündeyiz. Buradan ilk yapmanız gerek Network Device kısmına gelin

![](2016/05/suse_teamspeak_yastnetwork.png)

<p style="padding-left: 30px;">ardından Network Settings ayarlarına girin. Orası biraz karışıktır ama emin olun anlarsanız bu kısmı -ki çok uğraştırmayacaktır sizi- OpenSuSE de çok iş yapabilirsiniz.</p>

![](2016/05/suse_teamspeak_dns.png)

Ben her zaman için static ip atıyacağım zaman önce DNS, Gateway, Ip şeklinde giderim ki bence sizde öyle yapın. Özellikle Linux'da bunu yaparsanız hatayı bulmanız daha hızlı olabilir. Ben hemen OpenDNS'in IP'lerini veriyorum. Bence en iyi hizmet veren DNS'ler. Bir tane bile yazsanız yeter ama işi sağlama almak daha iyi. Name Server 3'de ağınız da ki bir DNS Server veya başka bir DNS IP si verebilirsiniz. Hostname ve Domain Name eğer basit bir TS kuruyorsanız hiç ellemeyin ve öyle kabul edin.

![](2016/05/suse_teamspeak_gateway.png)

Gateway'yi yazmak lazım aksi takdirde sıkıntı yaşayabilirsiniz. Benim ağım da ki Gateway
192.168.1.1 sizin eviniz de, iş yeriniz de çok farklı Gateway IP'leri alabilir.

![](2016/05/suse_teamspeak_ipaddress.png)

Şimdi en son ve en önemli kısım IP atama. Burada yapacağınız (sağolsun YaST) işlem çok basit. Sekme tuşuna basarak [Edit] kısmına gelin. Enter'a basın ve karşınıza

![](2016/05/suse_teamspeak_ipaddressadd.png)

Bu ekran gelecek. Buradan eviniz de veya ofisiniz de ki ip aralığı ne ise onu verin. Genel de Subnet /24 olur (255.255.255.0 anlamına gelir) hostname i burada ellerseniz diğer taraftan (2 üstte ki görsel de ki) yeri de düzeltmeniz gerekir. 192.168.1.0 ağı olduğundan ben 192.168.1.10 veriyorum. Dikkat edin, statik ip atadığınız zaman başka bir IP ile çakışırsa sıkıntı yaşarsınız. O yüzden önceden o IP'ye mutlaka ping atın (elbette bu sadece basit bir çözüm. Tam çözüm değildir!)

Ardından Next diyerek işleminizi kayıt edin. IP adresini görmek isterniz <em>ip addr</em> veya <em>ifconfig</em> komutlarını işletin.

### ClamAV virüs tarama

Aslında Antivirüs ün de bir tanımını yapsam daha iyi olur diye düşünüyorum. Antivirüs programları veya yazılımları zararlı olan (bazen de yararlı) virüsleri, solucanları, bombaları uzak tutar sistem de. Anti virüs yazılımları İnsan da suyun yeri kadar Windows da ki yeri de aynıdır. Ama Linux da malesef böyle değildir. Daha doğrusu Linux zorunda kalmadıkça anti virüs kurmaya bile gerek yok. Sebebi çok belli bu da [link](https://www.google.com.tr/url?sa=i&amp;rct=j&amp;q=&amp;esrc=s&amp;source=images&amp;cd=&amp;cad=rja&amp;uact=8&amp;ved=0ahUKEwjz0paA267MAhXDOBQKHWlIBKkQjRwIBw&amp;url=https%3A%2F%2Feugene.kaspersky.com%2F2014%2F09%2F29%2Fthe-evolution-of-os-x-malware%2F&amp;bvm=bv.120551593,d.bGg&amp;psig=AFQjCNGjYTE-JYdpVVZnbnNh9qgLpinzVg&amp;ust=1461842459184270)i

![Linux and Virus](https://eugene-kaspersky-wpengine.netdna-ssl.com/files/2014/09/macosxos.jpg)

Linux için virüs tasarlanmıyor bile. Dünyaca en çok kullanılan iki işletim sistemi var. Windows ve Mac OS x. Grafiğe de bakarsanız %80-90 ile Windows tahtını koruyor. Şaşırtan şu ki Mac sistemlerine güveni yüksek olsa da virüsün yanında en çok ve en tehlikeli güvenlik açığında da Mac tahtını korkuyor. Linux ise topluluğu sayesinde (Red Hat, SuSE ve Ubuntu) virüs ve güvenlik açığı sayısı yok denecek kadar azaltıldı ve daha da azaltılıyor. Aranıza da mutlaka XP kullananlar da vardır. MS'in malesef para kazanma yönetimi olarak XP'ye desteği bitirmesi daha da açığın ortaya çıkmasına neden oldu. Ama şunu belirtiyim bir sunucu kuracaksanız asla şu cümleyi kurmayın; *yahu linux bu virüs yemez*. Bu cümleleri kuranlar kendini linux'un özgürlüğüne kaptırmıştır.

Çok fazla lafı uzatmadan kuruluma geçiyim

```
linux-ctcw:~ #zypper install clamav
```

Üstte ki komutu işleterek indirin. Ardından

```
linux-ctcw:~ # freshclam
```

Virüs database'ini tazeliyelim (yani yeni virüsleri clamav'ye tanıtma işlemi diyebilirim) ayrca belirtiyim bu işlem biraz uzun sürüyor. Aslında buraya kadar yapmak çok basitti değil mi? Şimdi işimizi daha da basitleştirelim. ve otomatik bir şekilde her pazar günü yaptığımız yedek sonra sadece teamspeak 3 ün file tarafını tarasın.

```
linux-ctcw:~ #crontab -e
```

```
25 4 * * 0 freshclam
35 4 * * 0 clamscan -r /berkhan/teamspeak/
```

Pazar saat 4.25 de database'i tazeleyecek yine aynı gün saat 4.35 de /berkhan/teamspeak/ klosörünü taramaya başlayacaktır. İsterseniz komple sistemi taratabilirsiniz ama gereksiz. Çünkü sistem CPU kullanımı %100 olacağından sistemi çok yavaşlayacak. Bu yüzden küçük parçalara ayırarak tarama yapın.

## Son söz

Öncelikle belirtiyim burada yapacağınız her ayarı buraya bakarak yapmayın. Örneğin kırmızı ile belirttiğim yerli silin ve kendi sisteminize göre ayarlayın. siyah ile belirttiğim yerler statik bilgidir. Aynı zaman da şunu da belirtmek isterim bu yaptığımız sistem ciddi bir koruma sistemine de ihtiyacı var bunlara örnek olarak bir firewall ve ona takiben DDoS koruma aygıtlarına ihtiyacınız var. Aynı zaman da yüksek bant genişliğine ihtiyacı olduğundan eviniz de ki ADSL den bu sunucuyu host etmenizi tavsiye etmem. Bir VPS üzerinden de bu tip bir sistemi host edebilirsiniz.

[Teamspeak Ana sayfa](https://www.teamspeak.com)   
[OpenSuSE Anasayfa](https://tr.opensuse.org)
