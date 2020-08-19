---
layout: post
title: Para ödemeden blog sahibi olmak mümkün mü?
author: Berkhan Berkdemir
date: 2018-04-28
update: 2018-04-28
---

Bilirsiniz ki blog sitesi kurmak şu zamanlarda çok da zor birşey değil hele ki azcık da olsa programlama bilginiz varsa hiçbir şey. Ben bu yazımda birazcık hayal olan birşeyi anlatacağım (veya okudukça nasıl da zor olmadığını anlayacaksınız).

## Sorun

Şimdi yıl 2018. Elinizde ki internet birkaç 20, 50, 100 mbps oldu. Herkes bir hız peşinde, sizinde yazdıklarınız o hızla okunacak ama okunmadan öncesinde bir sorununuz var.

> Websitesi 2 saniyeden fazla zamanda görüntü oluşturmuyorsa çöp - Berkhan Berkdemir

Bunun çözümü basit diye düşünebilirsiniz. Eğer ki eski sisteminiz PHP tabanlı bir CMS ise (örneğin WordPress, Joomla vb.) hemen cache plugin ekleyip işin altından kalkabilirsiniz veya ki 10.000 kulanıcılı bir blogunuz var ve o kadar çok query transaction oluyor ki bir cache sistemi kullanmanız gerek. O zamanda memcached, redis gibi cache sistemleri kullanmanız gerekicek.

Ayrıca hatırlatmakta da fayda var. Olay sadece computing de değil daha ötesi. Mesela siteniz Afrika'nın bir yerinden erişim süresi ne kadar uzunlukta veya siteniz 1 Mbit/s (yani regular 2G) erişimi ne kadar sürüyor. Bunlar önemli çünkü bu sebeplerden dolayı websitenize olan ziyaretçileri daha DOM yüklenmeden kapatmalarına neden olabilsiniz.

Tamam biz ne yapacağız veya kullanacağız?

* SSG olarak - Jekyll
* Code hosting - GitHub
* CDN, DNS, Form ve Deployment - Netlify
* Resim hosting - Imgur
* Yorum sistemi - Disqus
* Analitik - Google Analytics

> DİKKAT:
>
> Burada fark ettiyseniz DNS derken domain den bahsetmiyorum çünkü domaini satın almak **zorundasınız**. Bedavaya getirmek istiyorsaniz subdomain kullanabilirsiniz ama benim size verebileceğim nacizene tavsiyeme uyup yıllık $1 lık olanlardan başlayın derim çünkü ileride keşke demenize neden olabilir.

## Çözüm

Takipte kalın. Bir video gelecek.
