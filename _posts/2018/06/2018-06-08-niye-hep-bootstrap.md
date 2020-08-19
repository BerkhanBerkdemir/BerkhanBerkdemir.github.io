---
title: Niye hep Bootstrap?
date: 2018-06-08 22:08 PDT
tags: 
---

Niye her open-source projem de kulanıyorum bu doğa harikası CSS framework'ünü. Birkaç kısımda anlatmak istiyorum

## Rails ve ben

Evet doğru, cidden çok sevmeye başladım Ruby *ve* Rails'i. Sebebi aslında Ruby'nin DSL yani Domain-Specific language olmasından dolayı ve daha da anlaşılır bir şekilde söylemek istersem; okuduğum gibi yazıyorum veya yazdığım gibi okuyorum. Her ne ise, keyifli bir geliştirme oluyor o sırada.

Ama peki Bootstrap'ın rolü nerede? Aslında dostum gerçeği söylemek gerekirse Bootstrap bir Twitter projesi - şuan karmaşık. Bilirsinki Twitter'ın arka planı Ruby on Rails'e dayanıyor. Evvet, tahmin edebileceğin gibi

```
Bootstrap <3 Ruby on Rails
```

Sadece bu nedenden mi? Hayır.

## Basit. *Klişe* olan değil

Ciddi anlamda benim gibi front-end kavramlarına uzak birisi için tek yaptığım CDNJS'den çekiyorum ve kullanıyorum. Elbette bunu küçük çaplı open-source projelerimde yapıyorum. Şuan çalıştığım o büyük projem de gem olarak yüklü Bootstrap ve tahmin edebilirsiniz ki hiç sorun yaşatmadan çalışıyor.

Diğerki frameworklere nazaran bana göre daha şöyle *business* duruyor. Elbette bu benim görüşüm ve amacım burada framework yüceltmek değil hele ki bu framework artık yürüyen bir canlıya dönmüş ise.

Ayrıca biraz fazla vakit harcadığım için kendisi ile -2015- artık birçok şeyi otomatik yapıyorum mesela benim klasik birşeyi hemen ortaya al snipeti

```html
<div class="row">
  <div class="col-md-6 mx-auto">
    ...
  </div>
</div>
```

Bu tarzda şeyleri artık düşünmeden yazmaya başladım - elbette çok basit örnek. Sonrasında merak edip nasıl oluyoru araştırdım ve SCSS ile basit seviyede CSS ögrendim - GitHub'da ki bir [CSS framework](http://github.com/siimple) grubuna girecek kadar.

Ben ve Bootstrap bu kadar. Bu da benim GitHub repolarımda bulunan; UI'ya sahip %95'in neden Bootstrap olmasının yazısı idi.

