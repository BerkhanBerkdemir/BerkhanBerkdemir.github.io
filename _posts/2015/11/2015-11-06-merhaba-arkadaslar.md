---
title: Merhaba Arkadaşlar...
date: 2015-11-06 TRT
layout: post
---
Merhaba Arkadaşlar. Ben Berkhan. Linux hakkında ki bilgilerimi sizin ile
paylaşmak istiyorum. Özellikel IPFire ve Zentyal hakkında çok fazla kurcalamam
sonucunda elde ettiğim bu basit ama gerekli bir çok örneği blog'umu takip ederek
elde edebilirsiniz.  Öncellikle belirtmek isterim arasıra İngilizce tabirleri
kullanma sebebim Türkçe'de malesef karşılığı olmamasıdır.

Linux nedir sizce. (Açık Kaynaklı ürünlerin dağıtıldığı, Windows'a rakip işletim
sistemi). Keşke bu kadarı ile kalsa ama malesef Windows'a rakip değil. Aslında
amacı bu değil. Elbette Açık Kaynaklı ürünler Windows'da da var ama Linux'un
temeli Açık Kaynaklı. O yüzden lütfen Linux ile Windows karşılaştırmalarını
yapmaya gerek yok şimdiden.

Ben aslında bu Linux merakını, Sonicwall UTM'leri hakkında bir seminerde saldım.
Windows bana cidden çok sıkıcı bir arayüz, belli komutlar da sıkıntı vermesi
veya istedğim hızı alamamak beni rahatsız ediyordu üzüyordu. Benim ilk kararımda
Windows'u silip yüklediğim işletim istemi olan CentOS 5 halen kullanıyorum.
Sizce Windows sadece XP ve 7 başarısı sağlarken Red Hat Enter. ve CentOS her
serisinde stabil çalışabiliyorsa. Burada bir sıkıntı vardır demek oluyor. (veya
başka dağıtıcılar; Ubuntu, Fedora, Gentoo, Linux Mint vb.) Aslında sıkıntı
şurada Windows hep para politikası yüzünden W95 tanıtımda bile "Blue Screen"
yemeye layık görülmüştür. Burada Windows elbette başarı hikayeleri var. Server
2003R2 Standart kullanıyoruz ofisimizde. yaklaşık olarak 3-5 sene aralıksız
çalışan makina artık anakart buraya kadar dedi ve bitti. Bizde sadece
harddisk'i alarak yolumuza devam ettik. (Elbette aynı model anakart alarak
yoksa driver sıkıntısı olucak). Windows'un diğer bir olayı ise malesef "Driver"
bulmak ve onu yüklemek. Elbette yeni çıkan Anakartlarda (Intell LGA 1366 ve AMD
AM2+ serisinde) içlerinde dahili olarak Driver'ların çoğu yüklü olarak geliyor.
Nasıl mı ? BIOS veya UEFI bu sürücüleri işletim sistemine tanıştırıyor ve en
azından internete bağlanan bir bilgisayar veya en güzeli 800x600 çözünürlükte
değilde 1280x1024 çözünürlükte hangi sürücü kurulmamış diye bakabilirsiniz. Bu
elbette güzel bir şey. Ama en yakın zamanda mutlaka en yeni sürücüleri kurmayı
da unutmayın.

Linux bana ne kazandırdı derseniz Windows'da halen paralı satılan bir çok
uygulama (3Ds MAX gibi) ücretsiz olarak Ubuntu Store'dan veya RHEL REPO'dan
sadece bir tık ile indirmek veya bir kaç basit komut ile indirmek. (Ubuntu'da
`sudo apt-get install`; Red Hat `sudo yum install`) Elbette bunlar güzel şeyler.
Ama Windows'da ki bir 3Ds MAX gibi olmuyor malesef. Eksikler olucak. Bu
eksikleri ise Gönüllü programcılar veya Bağış yapan kişiler kapatıyor arayı. Şu
an Blender3D ile o ilk beta sürümleri arasında ki görseniz dudağınız uçuklar.
Tabiki burada sadece bağış yapmak veya iki üç modul tasarlayıp programa entegre
etmek önemli değil. O uygulamanın gerçekten Linux dünyasına gerçekten gerekli mi
o da önemli.

Ben Windows Server 2003R2 Standart kullanan birisyim. Yani sunucum öyle 2 tane
işlemcisi 32 GB lık RAM'i yok. Tamam XP zaten süper bir işletim sistemi ve
desteği bitmesine rağmen halen her yerde kamu kuruluşu olsun özel kuruluş olsun,
askeri kuruluş olsun fark etmez. Halen kullanılıyor. Çünkü 1 GB ram 3 GHz
işlemci 40 GB harddisk yeter en fazla yapacağınız ram arttırmak. Ama Linux daha
güzel. 384 MB RAM 2 GHz CPU ve 10 GB Harddisk. Hemde bedava. Bu size daha cazip
gelmiyor mu ? Ben Server 2003R2 desteği bittiği anda bitirdim Windows Server
serisini. Bütün SQL verilerimi yedekliyorum her gün. Bu size hiç bir şey ifade
etmeyebilir. Her gün, her hafta sunucu çöküyor. Bir ay da tam tamına 18 kere
çöktü ve iyi ki hep gece saatleri yani verileri etkileyecek bir şey değil. Ama
Linux'da "Blue Screen" var da ben halen görmedim :) Elbette Microsoft çok büyük
bir şirket ama para ile alıyoruz o kadar en düşük istemci işletim sistemi
malesef 120-150$ arasında. Linux da ise 0-70$. Red Hat Enterprise Linux ve SuSE
Enterprise Linux paralı satıyor o da gennelikel destek için alıyorlar ücreti
(birnevi bağış gibi düşünün) Elbette RHEL (Red Hat'ten bahsedereken RHEL diye
yazıcam artık) Mühendis çalıştırma farkı ile bu Linux sektöründe ve halen tek ve
tek (bence) Linux dağıtıcı. İlla RHEL satın almanıza gerek yok. CentOS veya
Fedora da RHEL'e ait. Ama size nacizane önerim CentOS'u en azından bir sanal
bilgisayara kurun ve orada ki nimetlerden faydalanın. Eminim artık o sıkıcı
Windows butonlarından kurtulunca cidden rahatlıyacaksınız. Ama size hiçbir zaman
önermim hadi gel Linux dünyasına olmaz. Çünkü Windows'da ki bir temeli hemen
Linux'a aktaramazsınız.

Öncelikle oyun oynamayı seven arkadaşlara kötü bir haberim var. Malesef Linux
oyunları biraz sıkıcıdır. Ama Steam'dan Linux destekli oyunlar indirebilirsiniz.

Bir sonraki makalem "IPFire ve Firewall Hakkında" olucak.
