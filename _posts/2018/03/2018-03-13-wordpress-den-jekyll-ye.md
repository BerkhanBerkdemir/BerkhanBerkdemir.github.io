---
layout: post
title: WordPress den Jekyll e Migrasyon
author: Berkhan Berkdemir
date: 2018-03-13
---

Tekrar hoşgeldiniz, bu biraz devam niteliğinde olacak. Teknik konular içerebilir. Elinizde bir adet Google un bulunması iyi olur. Keyifli okumalar

# Hikayesi

Aslında anlattım bir önceki yazımda. Ana sebebim yeni bir blog yazma ve eksi blog a domain olarak 'old.' subdomain e almak ile nedeni açık. Yep yeni bir sayfadan başlamak denebilir buna.

Ayrica hosting firmasına domain dışında bir para ödemek istememem de ayrı bir şekilde eklemek isterim.

# Hadi, ısınma turuna çıkalim

CDN olarak Cloudflare kullanıyorum. Bu yuzden büyük değişikliklerden önce yanlışıkla cache alınmasın (Always-On feature veya) diye bir maintance moduna girelim. Ayni zamanda eger Cloudflare ssl kullanıyorsanız mutlaka kapatın. Çünkü ben bunun yüzden 1 saatimi kafa yiyerek geçirdim (disqus ve jekyll exporter çalışmadı).

Nasıl mı? Hadi göstereyim.

## Cloduflare bakım moduna gecmek

![](https://i.imgur.com/vWk3K5Y.jpg)

Sadece tek bir tık ile Cloudflare artık cache modunda calışmayacak ve bütün trafiği direk sizin asıl işrate ettiğiniz sunucuya gidecek.

Bu durumun bir avantaji bir de dezavntaji var

### Avantaj
Eğer herhangi bir major değisiklik yapacaksaniz cidden yapmanız gerek. Şunu düşünün. Elinizde yeni bir template var. Siz bunu eğer public e açarsanız herkes de hemen sonuç alamazsınız eğer doğru cache expires ayarlamaz iseniz (veya hashlanmış (Okunus: Heshlenmiş, patates olan değil.) CSS JS kullanmazsanız). Ben burada cidden major un major unu yapiyorum. Yen bir sisteme geciyorum, eski sistemi yeni bir domain e aliyorum ayni zamanda komple template degisiyor.

Kesin kes boyle baslamam benim icin iyi bir durum

### Dezavantaj
Siteniz cok fazla trafik altinda ise ve bunu yaparsaniz ve Wordpress gibi server side bagimlisi bir siteniz varsa backup veya migration scriptleriniz yavas calisabilir hatta hata alabilir. Bu durum beni cok etkilemedi. Sonucta gunde 30-40 kisi ziyaret ediyor ve benim o anki hizimi cok fazla yavaslatmadi.

## Cloudflare flexiable SSL/ full SSL i kapatmak

Diceksiniz sacmalama niye kapatiyoruz mis gibi HTTPS yuruyoruz surada. Oyle demeyin. Ben Disqus ve Jeklly-Exporter i çalıştırana kadar anam ağladı. Şimdiden kapatin merak etmeyin canınızı yakmayacak.

İlk fotoğrafta da görüceginiz gibi off da. Cidden yapin. Sonrasinda açarsınız. On/Off dügmesi orada işte.

# Basliyoruz

Oncelikle bu blog u yazarken `ruby 2.3` surumunu kullandigimi ve tarihin 2018-03-13 oldugunu belirtmek isterim. Guncel bir blog olup olmadigi kendi tarihinize gore karsilastirin.

Ayrica sisteminde (Ubutnu 16.04) hali hazirda, `gcc`, `ruby`, `ruby-dev` ve daha nice development tool bulunmaktadir. O yuzden sizden onerim bilgisayarinıza nasil ruby indireceginiz hakkinda ruby nin dokumantasyonunun altini ustue getirin. (Windows ve Mac kurulumu bilmiyorum ama linux icin yardim ederim. Distro fark etmez, en kotu soruce dan hallederiz)

[Ruby Official Documentation](https://www.ruby-lang.org/en/documentation/)

## Sira Jekyll de

### Jekyll yi indirelim, YAAYY

[Jekyll](https://jekyllrb.com/) nin orjinal sayfasina bakarsaniz su kodlari goreceksiniz

{% highlight bash %}
gem install jekyll bundle
jekyll new my-awesome-site
cd my-awesome-site
jekyll serve
{% endhighlight %}

### Jekyll nin `_config.yml` na bir goz atalim

En başta göze çarpan anahtar kelimeler `title`, `email`...

Doldurabildiğiginiz doldurun. Bir fikriniz olmayanları ellemeyin. Veya elinizde github hesabı yok ise `False` veya `nil` (Ruby de null karaterine eşit) yazın.

## WordPress kısmı

### Jekyll-Exporter'ı çalıştıralım.
![](https://i.imgur.com/oDkVoyX.jpg)

Geliştiricisi: Ben Balter olan exporter'ı indirin ve etkinleştirin.

__Dikkat__: "Export to Jekyll" dediğiniz gibi sistem kaynaklarının hepsini kullanacak. Amman dikkat edin export sırasında hostig provider canınızı sıkmasın.

> Bakınız: ![](https://imgur.com/9fsCKT2.jpg)

### Yorumlarımızı alalım

Ben yorum yöneticisi olarak Disqus kullanacağım. Çünkü şu ana kadar oraya yedekledim bilgilerimi. Peki nasıl (questıon mark)

![](https://imgur.com/8kdBXlk.jpg)

Şimdi ise WordPress için yazılmış Disqus'ı indirin ve etkinleştirin. Sonraki adım için şurayı bir takip edin derim. Çünkü ben oraya değinmeyeceğim.

![](https://imgur.com/vA9JLUd.jpg)

### Sihirli zipcik

![](https://imgur.com/HxnNu7u.jpg)

Exporter'ı çalıştırdıysanız kısa (bende uzun sürdü) bir süre içinde zip'i alıcaksınız.

Ama sorunlarımız var.

#### Bazı WordPress tagleri

![](https://imgur.com/jhVpJ3j.jpg)

#### HTML uyuşmazlığı

![](https://imgur.com/mpANJZx.jpg)

### Çözüm

El ile hepsini silin. Şahsen daha da kullanmayacağım için öyle yaptım. Ama sorun çözümü bulursanız (Birincisi için değil) [github](https://github.com/benbalter/wordpress-to-jekyll-exporter) da ki repo suna bir PR çakı verin.

## git (push --force)^1000

Sıra en sevdiğim kısımda. Kodu uzak repoya atmakta. Hadi onu da yapalım.

Öncelikle ben GitLab kullanıyorum. Belki sen Bitbucket veya GitHub yahut X-bilmem-git-firması kullanıyor olabilirsin. O yüzden de değişiklik gösterebilir.

GitLab da hemen bir uzak repo oluşturalim. Ben yanlışıkla normal domain adını giriyorum. O yüzden ileride değiştirecem adını.

İlk bir local de message ımızı yapıştıralım.

![](https://imgur.com/UEhYUwP.jpg)

Şimdi GitLab tarafı
![](https://imgur.com/VZ9jhDd.jpg)

![](https://imgur.com/7zxqRj0.jpg)

![](https://imgur.com/i1q39p0.jpg)

![](https://imgur.com/7gQTHgh.jpg)

# Son vuruş - CII.. (Continuous Integration Integration Int..), ne abarttım.

![](https://imgur.com/i0tlSIC.jpg)

> Kusura bakmayın GIMP editlemesi bana ait. Bu yüzden front-end hiç düşünmedim

![](https://imgur.com/Ci6Bnd2.jpg)

![](https://gph.is/1UB39zl)

# Son sözüm

Yani azcık sıkıntı idi wordpress exporter ama total de güzel sonuç cıkardı. Unutmadan değerli Cloudflare imizin SSL ve Cache özelliklerini unutmadan açalım.

Umarım keyifli bir yazı çıkarmişimdir ve bunu bana beğeniniz ile bildirirseniz sevinirim. Aynı zamanda önerilere açıgım bana bir disqus, 100kB kadar yakınlıktasınız.

Şimdi sizi PHP ve MySQL iniz ile başbaşa bırakıyım

__Dipnot:__ PHP den de MySQL den de vazgeçemem. Severim o bitirim ikiliyi.
