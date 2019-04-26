---
title: Web hosting seçimi ve yönetimi
date: 2016-05-15 TRT
layout: post
---

Merhaba arkadaşlar

Bu yazımda aslında bu kadar online olmama sebebi ile birlikte küçük bir neden hosting, peki bu hosting de ben neyi seçeceğim ve nasıl yöneteceğim soruları ile başlıyorum

## Hosting nedir?

Hosting aslında basit bir tanım ile ISP'lerin size sunduğu hizmet. Ve bu hizmetler dağılıyor -paylaşımlı hosting, sunucu hosting, cpanel hosting vb.- Ben site daha yeni ve çok az kullanıcı girdiği için paylaşımlı hosting kullanıyorum. Bunun yaralarıdan çok zararları var diyebilirim ki bunların en önemlisi önemli dosyalara müdahale edemiyorsunuz. Mesela PHP config dosyalarında kendize göre değişilkik yaparsanız başka siteler de etkilenebilir. Belli bir işlemci ve RAM kullanma yetkiniz var. Belli miktarda I/OPS (anlamı da "saniye de Giriş/Çıkış"). Ama en güzel yanı basit projelerinizi burada oynatırsanız sizi delirtme veya çıldırtma özelliği var.

Bunlar iç karartıcı yanı. Güzel yanı ise siz abuk sabuk sunucu çöktümü, sunucuya DDoS atılıyor mu, birisi brute force yapıyor mu sorularundan da kurtuluyorsunuz. Bunun yanında normal sunucuya oranla 5 hatta 10 kat daha ucuz oluyor. Bu yüzden de basit web siteleri için shared hosting kullanırlar.

Şimdi benim önceki firma (firma demeye bile gerek yok ama neyse) Hostinger di. Bir amatör hatası olarak hostinger den hosting hesabı aldım. İyi ki de paralı olarak kullanmadım ve bedava olarak kullanmaya başladım. Bedava domain aldım. Ama hep içim de bir kurt kemiriyordu. Yorumlarda hep Hostinger için kötü yorumlar vardı ki ben hiçbir kötü yanını daha görmemiştim. Taki 3 Mayıs 2016 ya kadar. O gün bana şu saçma ama bir o kadar sinir bozucu Mail geldi.

He bu arada mail atan Hostingerin hiç durmadan çalışan ÇALışanı Gürcan dan,

```
Sayın Berkhan Berkdemir,

<span class="il">Hosting</span> hesabınız askıya alınmıştır. Hesap detayları aşağıdaki gibidir:

<span class="il">Hosting</span> Planı: Ücretsiz
Alan Adı: <a href="http://linuxkafasi.xyz/" target="_blank" data-saferedirecturl="https://www.google.com/url?hl=tr&amp;q=http://linuxkafasi.xyz&amp;source=gmail&amp;ust=1463401823258000&amp;usg=AFQjCNFQNsrMonIf9FOcyBjGuV3tlzdRAw">linuxkafasi.xyz</a>
Sebep: Suistimal
Ek Bilgiler: Bikmem bunu neden gene yaptığımı. Bağlımlılık

Lütfen sitenizin tekrar çevrimiçi olabilmesi için bizimle irtibata geçiniz.
```

Bu maili alan birisi olarak o gün ağzınıza gelen ilk şey. Bu da neyin nesi dersiniz. Birisi dalgamı geçiyor. Aynı zamanda sosyal mühendisliğe bir ilgim de var ilk önce bu bana yapılan bir "lamer" veya "script kidie" şakasımı diye düşündüğümde (kısaca arkadaşlarımda bu tip bir maili yollamış olabilir diye düşündüm) mail yollayanı 2-3 kere kontrol ettim ve GERÇEK.

(artık hostinger diyerek size aleksa da puan kazandırmayacağım. HST kısaltması ile devam edeceğim.) HST ile işte o gün hatta o saat yollarımı ayırdım. Mail adresimi hemen sahte bir mail adresi yarattım ve kayıt ettim. Şifreyi değiştirdim ve o günden itibaren o sitelerine bir kere bile girmedim.

HST ile daha iş yaparmıyım asla ve kat'a yapmam.  cPanel de de şu yazıyordu

```
Web siteniz hız limitini x27 kere aştı.
```

Bu sebep ile sildiler. ~~Anlamadığım o kadar da sitenin işlemci kullanımını düşürmek için optimizasyonlar yaptım. Hatta sonradan kontrol ettiğimde 5 kullanıcı aynı anda girdiğinde %2-3 arasında kullanım yapıyordu.~~

> Mert Bey'in uyarı üzerine biraz yanlış anlaşıldığımı düşündüm ve üstteki yazıyı sildim ve şu sözleri ekledim (altta yorumlardan da bakabilirsiniz 2016.11.23)
>
> Merhaba Mert Bey,
> Yorumunuz için teşekkür ederim. Olay aslında şöyle detaylandırabilirim..
> Kullandığım script WordPress’in hazır scripti ki bunu rahatlıkla evinizde ki sistemlerde de kullanbilirsiniz. Eğer ki sizde evinizde küçük bir lab ortamında kullanırsanız ve birazda meraklı olursanız wordpress’in %2-3 lük bir CPU (admin panelinde aktif işlemde) kullanımı olduğunu görebilirsiniz. Orada ki cümle düşüklüğüm için özür dilerim. Benim kastım kendi kurduğum lab da %2-3 aldığım CPU kullanımından HST nin böyle bir sıkıntı yaşamasıdır. Zaten HSTNGR ile bir kere bile çalışsanız emin olun bunu yazmanıza bile gerek kalmayacaktı. Aynı zamanda cPanel üzerinde sistem kaynaklarını görüntüleyebiliyorsunuz bunun için dahi olmaya mı gerek vardı?
>
> Aynı zamanda sonradan oturup yazımı okuduğum şunlarıda eklemem gerektiğini düşünüyorum.
> Ben BackWPup ile yaklaşık 60-70MB lık büyüklükte zip türünde yedek alıyorum ve bu yedeği bulut sisteme atıyorum. Bir tek bu durumda CPU kullanımı tavan (%25’e en fazla izin veriyor du benim siteyi barındırdığımda 180-190 saniye de bitiyordu) oluyor ama saat 03.00 da olan bir yedek işlemi. Bu yasaklanma iş saatleri içinde olduğu için bunu ekleme gereğinde bulunmadım.
>
> Umarım bu konuda ne düşündüğüm aklınızda canlanmıştır.
>
> İyi günler dilerim.

Neyse ben konuya geri döneyim.

## Hosting seçimi

Hosting seçimi hem kolay hem zordur ki ben çok basit bir şey diye zanediyordum. Yok işte MySQL sürümleri ne hangi PHP versiyonları var, hangi paneli kullanıyorlar, cPanel ise sürüm kaç, destekleri nasıl (destek için ayrı bir konu içinde bahsedeceğim), Up-time garantileri ne (konu için de belirteceğim) uzar da uzar.

Ben cPanel kullandığımdan (daha doğrusu tecrübeli olduğumdan), linux işletim sistemi altından devam etmem gerekirdi. Ki öyle yapıyorum. İşletim sistemi olarak Debian ve CloudLinux seçeneği vardı ve hiç düşünmeden CL yi seçtim.

İlk başta Natro ile bir anlaşmazlık yaşadım domain konusunda ama o da benim cahilliğim (daha doğrusu yanlışlığım dı). Ama sunucularının en başta hızı, PHP de bir sıkıntı yaşmaması o kadar hoşuma gidiyor ki anlatamam.

Ben dediğim gibi shared hosting taraftarıyım (mâlum bütçeler orta da), Limitsiz kaynak veriyor ama o da nereye kadar :)

Hosting seçerken mutlaka cPanel veya Plesk gibi bilindikleri kullanmaya gayret edin ki gözünüz yorulmasın. Bir de Türkiye de bence hosting alınacak daha doğrusu başlangıç olarak GoDaddy'dir. Ucuz, hızlı ve desteği süperdir. Sonra Alystar'a, İsim tescil -ki bu aralar bazı webmasterlar memnun değil-, Natro, SH geçersiniz ve uzmanlığınızı yaparsınız.

## Hosting yönetimi

En basit kısım siz eğer shared hosting kullanıyorsanız birşey yapmayacaksınız. Siteniz kapalımı ticket at, 5-10 dakikaya sorunu halederler. Sorun halen devam mı ediyor ikinci ticketı at o zaman halletmiş olurlar işte. Başka durumlar varsa onu bilmem.

## Hosting güvenliği

Güvenlik belki sitenizi ayakta tutmaktan önce yer alır. Siz eğer iyi bir şirket ile çalışmasanız her türlü olay başınıza gelir. Mesela, z<strong>e</strong>.com sitemiz de Joomla! kullanıyoruz ki ben de Joomla! bilmediğim için güvenlik optimizasyonları yapamıyoruz ve bu yüzden sitemize tanımadığımız kullanıcılar eklemişler. Ben de hemen Joomla! yı kaldırdım ve başka bir CMS kurdum (güvenlik nedeni ile yazamıyorum). Ama bu bana bir tecrübe kazandırdı o da şu SSL bir nimet ve o nimetten herkesin faydalanması gerek. Tabi ki daha 2-3 tane daha tecrübe var ama o da bana kalsın :)

## Son söz -cidden-

Hosting yönetimi eğer sunucu ile yaparsanız -bence- en zevklisi ve kişiye en çok tecrübe katan yer olur. Ama başlangıç olarak asla tavsiye etmem. Bir cPanel, CloudLinux yanına bir de güzel bir şirket kim istemez.
