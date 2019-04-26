---
title: VMWare vSphere ESXi 6.0 vs Xen Server 6.5
date: 2016-01-30 TRT
layout: post
---

Merhaba arkadaşlar, bugün biraz değişiklik yapalım ve sanalaştırma üzerine yoğunlaşalım.

![ESXi vs Xen](2016/01/vmvsxen.png)

**Birinci kısım** sanalaştırma yenir mi içilir mi?

Sanalaştırma öncelikli olarak nedir ve normal sunuculara oranlara ne gibi avatajları var ve 5-6 senedir neden bu kadar güzel dile dolandı, Linux tarafı bu konu da ne yaptı, Microsoft tarafı ne yaptı, Green Tecnology nedir gibi basit konulardan bahsedicem.

Sanallaştırma basit bir şekilde ifade edersem donanım üzerine kuruluan 1, 2 3. OS lara ve bunları yöneten tarafa ise Hypervisor deniyor.
Şimdi Hosted VM ler kullandığımız OS lar ile yani W7, W8 veya W2008R2 gibi işletim sistemlerin de bulunur.

Bare-Matel ise direk donanımın üzerine kurulun bir işletim sisteminden ibaret ve bunlara örnek işte ESXi veya Xen Server (ve daha nicesi).

Şimdi bu iki ürün de driver larını içinde bulunuduryorlar ve misafir istemciye bu driverları kurup hiçbir sıkıntı yaşamamanızı sağlıyor.

Hadi konuyu biraz daha basitleştiriyim. Elinizde bir donanım var ve siz ekstra bir donanım almadan nasıl daha fazla sunucu barındıracağınızı kara kara düşünüyorsunuz. Çözüm Virtual Machine ile. Şimdi sadece donanımdan para kurtarmayarak aynı zamanda elektrik faturasından, çalışan maaşından kurtarmış olucaksınız. Bununla da kalmayıp basit bir kontrol merkezi ile yöneticeksiniz onca sunucuyu.

Şimdi çoğu şirket, bu sanallaştırmada ki potansiyeli gördükçe sanallaştırma uyumlu bilgisayar alıyorlar (aldılar da).
Sanalaştırmanın sağlıklı olması için elbette altın kurallar vardır.

* Dual-Core üstü ve  2.00GHz üstü tercih edilir.
* Çoğu sanalaştırma programı zorunlu olaran VT-x ister. AMD tarafında ise AMD-V. Bunlar en basit özelliği x64 desteği sağlaması  (yani benim fark ettiğim).
* RAM olarak malesef 2-3 sunucu barındırmak istiyorsanız en az  3GB+1GB olarak ayarlamanız gerek. Aksi takdirde sistemin belleğini tüketen misafir sunucuda takılmalara neden olabilir.
* HDD tarafı ise biraz karışık. Kimisi SSD alıyor iSCSI ile bağlıyor fazla alan isterse. Yok ben HDD alıyım ama hızlı HDD alıyım der SAS 15k lara para bayarlar. Aslında fazlada bir seçeneğiniz yok. Raid 5 en önemli silanınız olucaktır. Raid 6 olayını girmeyi düşünmem.
* Elbette internet tarafı basit hemde en basit tarafı. 1 port ethernet kartınız olsun siz misafirleri kendiniz önceliğin belirleyin. Ama 2 port olması daha iyi olur. En azından trafi daha iyi dağıtırsınız.

Basit gibi gözüküyor değil mi. Aslında bir kere sanal pc ile uğraşın hiç reel pc ler ile uğraşmak istemeyeceksiniz. Yok ram takıp çıkarması yok sata power takmayı unutması, RJ-45 in hasar görmesi falan hepsi hikaye olucak (veya devam edecek).

Asıl sunucunuz da bunları kullanıyor olucak ama daha az uğraşıcaksınız emin olun.

Peki bu sanalaştırma yenir mi içilir mi? Bence ikiside değil ama ekmek teknenize önce bir yük sonra bir ferahlık getirecektir.

**İkinci kısım** Xen mi? ESXi mi?

Önce bir özelliklerinden bahsediyim sonra bencesini nedenlerini anlatıyım. Xen açık kaynak kodlu Hypervisor. ESXi ise bedava bir yazılım. İkisi de kullanabilene ve parası olana cidden güzel uygulamalar. Ama işte ne yaparsın para kazanma politikası olarak bedava sürümlerden birşeyi eksik edeceksin ki paralıya rağabet olsun. ESXi de Xen de aynı mantık ile gidiyor (en azından Microsoft gibi değil, linux tarafı az acıyor insana) İki marka da yeni başlayan kullanıcılar için bedava. Ama burada bir durun. Özel bir projeniz mi var? Özel bir şirketin alt yapısını mı hazırlıyorsunuz o zaman sizi ben "para ile lisans alma köşesine" alıyım. Yok ben alt tarafı evimde yatan bir sunucuda oyuncaklık bir vm arıyorum diyorsanız ikiside size göre. Xen de ESXi de control panel ile kontrol ediliyor. Bir kere kuruyorsunuz sorna 2-3 kere ziyaret ediyorsunuz sistemi. Daha detay için ayrı ayrı konu hazırlayacağım.

Bence Xen; nedeni aslında basit. Open-source ile güvenceye alınmış bir işletim sistemini ben tercih ederim. (Bakmayın Windows kullandığıma, oyunlar için :) ). Ayrıca Xen bence daha basit ve yalın. Elbette iki üç fantastik özelliği var o da ilgimi almasına neden oldu ama ESXi da farklıdır yeri. Sunucuların hepsi Windows Server, Red Hat Enterprise Linux, SuSE Enterprise Linux, Ubuntu Conanical ve VMWare ile sertifikalıdır. Ama orada dur. Xen nerede yok. Eğer siz sertifikalı bir ürün istiyorsanız (ki istiyorsunuz diye düşünüyorum). o zaman sizi VMWare köşesine alıyım. Xen de aslında RedHat çekirdeği kullanılan bir yazılım ama sertikaların arasında ismini göremiyoruz.

En yakın zamanda Xen Server, bakımı ve kurulumu hakkında geniş bir belge hazırlayacağım. Takipte kalın.
