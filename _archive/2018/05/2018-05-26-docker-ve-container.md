---
layout: post
title: Docker ve Container
author: Berkhan Berkdemir
date: 2018-05-26
---

Docker'ın tarihçesini anlatmak istemem ama 2014 yılından çıkan <a href="https://github.com/docker/docker-ce">açık kaynak kodlu</a> birçok bölümü Go, Python dilleri ile yazılmış bir proje olduğunu da belirtmek isterim. İlk çıktığında amacı hantal sanal makinalar yerine daha çok uygulama bazlı taşınabilir parçacıklar haline getirmekti. Aynı zamanda sanal bir makina üzerinde bir donanım ataması yaptığınız zaman o donanım parçası tamamı ile veya en azından çoğu o sanal makinaya ait oluyor bu da gereksiz bir şekilde donanımızın harcanmasına neden oluyor.

Docker ile birlikte taşınabilir bir formata getirildi uygulamalar ve bu uygulamaların adına Container dendi. Containerlar temelinde Linux kerneli ile çalışan işletim sistemlerinde oluştuğundan herhangi bir servisi çalıştırabilir. Örneğin <a href="https://hub.docker.com/_/httpd/">Apache HTTPd</a>; <a href="https://hub.docker.com/r/library/httpd/tags/">Alpine Linux</a> versiyonu tam tamına 29 Megabyte.

Özetlemek gerekirsek Docker bize containerlarımızı yönetmemizi sağlayan bir motor. Peki nasıl bir şeye benziyor?

<img class="aligncenter wp-image-225 size-full" src="http://blog.berkhanberkdemir.com/wp-content/uploads/2018/05/containers-vs-virtual-machines.jpg" alt="Containers VS Virtual Machines" width="548" height="352" />

Geleneksel sanal makinalara ilk önce bakarsak (sol) önce her bir uygulamanın bir misafir işletim sistemi var. Bu da demek oluyor ki biz <em>A</em> uygulamasından bir tane daha oluşturmamız için (yani <em>A'</em>) misafir işletim sisteminin tamamının klonunu almamız lazım. Burada da şu tip sorunlar ile karşılaşabilirsiniz.
<ul>
 	<li>Kısa zamanda birden fazla aynı uygulama ihtiyacınız olması</li>
 	<li>Uygulama veya işletim sistemi güncelemesi uygulanması</li>
</ul>
Diğer elden Docker'a bakıcak (sağ) olursak herhangi bir işletim sistemi ile uğraştığımızı söyliyemeyiz çünkü biz burada her bir uygulamızı bir container ile temsil ediyoruz.
<blockquote>Containerlar birbirinden bağımsız; ama işletim sistemlerini ve yazılım kütüphanelerini paylaşırlar.</blockquote>
Böylelikle çok küçük bir donanım veya alan ile birden fazla uygulama ve o uygulamanın birden fazla kopyasını çalıştırmamız mümkün olucak.
