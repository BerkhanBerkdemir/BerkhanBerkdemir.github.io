---
layout: post
title: WordPress den Jekyll macerasi
author: Berkhan Berkdemir
date: 2018-03-13
---

Uzun zaman oldu, resmen ilk göz ağrım blogumu tozlu storagelar da bıraktım. Bu Türkçe blog yazmayı bırakalı çok fazla sey oldu. Sonrasında anlatıcam ama önce şu WordPress macerami anlatmak istiyorum

<blockquote class="twitter-tweet" data-cards="hidden" data-lang="en"><p lang="tr" dir="ltr">&quot;Oha, websitemi çökerttim.&quot;<a href="https://twitter.com/hashtag/jekyll?src=hash&amp;ref_src=twsrc%5Etfw">#jekyll</a> &#39;e geçiş yapıyordum, <a href="https://twitter.com/hashtag/wordpress?src=hash&amp;ref_src=twsrc%5Etfw">#wordpress</a> elimde kaldı. Güzel vakit gecirdik kendisi ile, güzel blog deneyimi sundu tesekkür ederim. <a href="https://t.co/3hEVokPaAI">pic.twitter.com/3hEVokPaAI</a></p>&mdash; Berkhan Berkdemir (@BerkhanBerkdemi) <a href="https://twitter.com/BerkhanBerkdemi/status/973436023530078208?ref_src=twsrc%5Etfw">March 13, 2018</a></blockquote><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Yani, ilk adam akıllı birşeyler yazmaya başladığım ve bana çok sey katan WordPress ve WordPress ekibi/topluğuna teşekkür ediyorum.

# Yahu ne oldu?

Şimdi, yeni [blogum](https://blog.berkhanberkdemir.com)a bakan bilir. Kisaca o blogun ozelligi su

| Yazilim Adi | Neden kullaniyorum            |
| ----------- | ----------------------------- |
| Hexo        | Static content yaratmak icin  |
| Gitlab      | Hosting                       |
| Cloudflare  | CDN, DNS ve Traffic Analytics |
| Imgur       | Image hosting                 |
| Google Analytics | Website search analytics |
| Disqus      | Comment system                |

Eee, ne olmus??

Hepsi __bedava__ servisler dostum. Sadece domain registration icin para oduyorum. Bunun disinda hepsinin bedava hizmetlerini kullanıyorum ve bu da benim işimi görüyor.

Neden gidip de para mi Turkiye de ki hosting firmalarina savurayim? Hemde WordPress de tonlarca security eklentisine, backup veya anti-spam eklentisine de ekstradan CPU/RAM/I-O vermek...

Yil 2018. Insanlar internetten daha fazla bilgi bulup hemen kullanmak istiyor degil mi? Peki websiteleri buna hazir mi?

Bu soruyu sorduktan sonra (bugun) hemen benim linuxkafasi.org a hiz testi yaptim. Tatmin edici. Ama sorun _ne_ ki Static Content Generator a geçtim? Aylık shared hosting'e $12 ödüyorum. Gereksiz bir para. Mail addresimi kullanmıyorum, bana bir katkısı yok stress yaratmasından ötürü. IO sorunu var şu aralar. Eklenti güncellediğim gibi %100 e çakilyor. Bende tam zamanı diyip yapıştırdım cloudflare de maintance modunu, başladım çalişmaya (Sonraki yazi da nasil yaptigimi anlatacağim)

Şimdi, iki blog a ayiracagim. Birisi old.linuxkafasi.org olacak. Diğerkisi (yani bu), benim ana blogum olacak. Old yapmamin sebebi ise orada cidden amator olarak yazdığım şeyleri saklamak istedim. Çunku cidden bana gelişmemi gösteriyor. Onu Google da indexlemeyeceğim ama websitelerimden oraya link verebilirim.

Çok hikaye anlattim şimdi ise

> Talk is cheap. Show me the code.

Tamam, simdi code a gecelim.

# Neden Jekyll, Hexo niye değil?

Ruby 've' Rails'e çok yeni basladim (Şubat 15 inde baslamışım) ve cidden cok sevdigim bir dil ve framework haline geldi. İngilizce blogumu Hexo (JS tabanlı) ile kullanıyorum. Hexo ile basladi çünkü çok çok basitti (Jekyll i görmeden dedim bunu). Tatlı idi ama sorun benim javascript e bir türlü alışamayıp anlayamamam. Eklenti veya Template geliştirememem (rahat duramıyorum birşey katkıda bulunamazsam).

Sonra fark ettim ki bi şans tani [birinciye](https://www.staticgen.com/).

## Sebep 1: Ruby tabanli
Cidden Ruby tabanlı. Bu yuzden digerki blogumu da Jeklly e degisitircem. Koskoca `Gemfile` da sadece 3 tane dependcy var. Jekyll kendisi, feed plugin ve template. Bu kadar basit ve anlasilir.

## Sebep 2: Template engine
Vallahi kusura bakmayin ama ben eski kafa PHP li olabilirim ama o embedded PHP öldürüyordu beni. Sonrasinda twig ile tanıştım. Cidden çok güzeldi. Hayat bu kadar basitleştirilmez. Sonra Hexo ile EJS i gördüm.

Bence on yargi olustu (JS yüzünden) ve EJS i anlamadim. Cidden. Belki de arka planda ki mantiği farkli idi de o yuzden. Bu template engine twig e cidden benziyor. Anliyorum bem olley be..

## Sebep 3: Github <3 Jekyll
Default github pages jekyll kullaniyor. Bunun sebebinin (benim dusuncem bu) Ruby based olmasi. Elbette baska sebebleri de olabilir.

# Sonuc mu?

Cidden bu benim düşüncem, WordPress, baslangic seviyesinde ki bir blogger in baslamasi gerken nokta. Ama sonrasinda, ozellikle programcilar, yeni mecralar ariyorlar cunku wordpress in o kadar toollari veya feature/pluginsleri bir yerden sonra gereksiz kaliyor. Cunku artik neyin gerekli olup olmadigini biliyorsun.

Sonraki yazımda hemen bunun ardindan yazacagim. Konusu mu

__Wordpress den Jekyll e gidis__
