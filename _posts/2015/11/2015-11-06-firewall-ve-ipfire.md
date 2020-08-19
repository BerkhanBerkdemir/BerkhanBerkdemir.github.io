---
title: Firewall ve IPFire
date: 2015-11-06 TRT
layout: post
---
Merhaba Linux meraklılar. Ben Berkhan. Bugünkü konumuz Firewall ve IPFire işletim sistemi. Öncelikle belirtmek isterim firewall konusunu tam kavramadan IPFire'ı anlamak hiç mümkün değil. 
Firewall Türkçesi güvenlik duvarı anlamına geliyor. Temel amacı çalışma ağını veya kullanıcıyı dış etkenlerden korumak. Firewalllar internet ağının en önünde bulunur ve duvar görevi alır. Burada birisi sizin ağınızı kontrol etmek isterse (ip scan gibi) firewall bu isteklere belli bir süre engelleyerek veya bu isteği reddederek yanıt verir. Firewalllar basit port engellemelerinde veya VPN çözümleri vardır. Tabi ki daha değişik özelliklere sahip birçok Firewall bulunuyor Linux dünyasında.

Bunlardan örneğim ise IPFire (ileride Endian FW, Untangle ve Zentyal ı işleyeceğiz). IPFire Linux tabanlı firewall ve router yazılımıdır. Bir önceki (sürümün) adı IPCop. Burada biraz daha fazla geliştirme, optimizasyon ve web ara yüzü değişikliği ile IPFire'ı elde ettiler. IPFire basit bir işletim sistemi aslında. VPN bağlantıları kurarak, Port kabul etmek/engellemek/reddetmek (allow /deny / reject), Proxy Server, DHCP Server, Mail Server ve Pakfire (Paket yönetimi) sayesinde OwnCloud 7 gibi bilindik filesync çözümleri de bulunuyor. Bence IPFire'ı basit hale getiren olay tek tık ile birçok veriyi elde etmeniz. Özellikle UTM'lerin bu aralar moda olduğu dönemde bence IPFire'da hak ettiği yerde olmalı diye düşnüyorum. Çünkü bir UTM'in verdiği her şeyi basit bir şekilde size de verebiliyor.

IPFire 4 temel renkten oluşuyor. 

* Kırmızı (Red) - Zararlı olan bölge. WAN ağı.
* Yeşil (Green) - İstemcilerinizin bulunduğu bölge.
* Mavi (Blue) - Kablosuz erişim sağlayan istemciler bulunur. Yeşil'e göre tehlikeli, Turuncu'ya 
    göre güvenli
* Turuncu (Orange) - DMZ alanı. Burada Mail sunucuları, Web sunucuları gibi hep dışarı ile
    haberleşen sunucular bulunur.

Elbette bu renkler sadece gruplandırma olayını basit hale getirmek için. IPFire da zorunlu bulunan tek renk kırmızıdır. Sonuçta WAN ağınız bulunmaz ise nasıl internet ile haberleşeceksiniz. En çok tercih edilen ikili ise Kırmızı – Yeşil.

İlk önce kurulum çok basittir. Türkçe dil desteği bulunuyor fakat bazı uygulamalarda olduğu gibi küçük eksikleri olacaktır. Önce Harddisk e kurulum yapıyor. Ve size https://domain:444 veya https://xxx.xxx.xx.xx:444 ile girmeniz gerektiğini söylüyor. Ama burada şöyle bir sıkıntı var daha ip atamadınız bile. IPFire'ı CD'sini sürücünden veya USB belleği çıkartın ve sistemin boot etmesini bekleyin. Burada size hangi Ethernet kartlarının ne renk olacağını hangi ip olacağını soracak size. Benim size önerim 3 kart kullanmanız (Kırmızı – Yeşil – Mavi). Çünkü küçük ve orta işletmeler mümkün mertebe bunları kullanmak zorunda kalacaklar. Şimdi size ilk önce root kullanıcısın (terminal) şifresini soracak. İkinci şifre ise web ara yüzün şifresi. En çok kullanacağınız şifredir. Ve kurulum için birkaç soru soracak olabilir ekstradan (en azından 2.17 Core 92 de ekstra soru yok).

**VIDEO EKLENECEK**

Ara yüzün de ilk sizi karşılayan pencere de hangi iplerin bulunduğu, anlık olarak yükleme ve indirme hızı gibi hızlı ulaşmanız gerek bilgiler hemen önünüzde. İlk sekme "system" sekmesi. Burada sistem üzerin de ki özellikleri değiştiriyorsunuz. Bunlara örnek sistemi yeniden başlatmak, sistem yedeği almak, sistem zamanı değiştirmek gibi basit işler var. İkinci sekme "status" sekmesi. Burada firewall durumunu grafiksel (işlemci yükü, açık olan servisler, takas alanı durumu gibi). Üçüncü sekme "network" adında. Burada Ağ da yapmak istediğiniz servisi açıyorsunuz. Bunlara örnek Squid Proxy, İçerik filtreleme, DHCP sunucu gibi özellikleri yapılandırıyorsunuz. Dördüncü sekme "services". Bu "status" sekmesinde ki gibi değil. "Status"da sadece durumlarını gösteriyor. "Services"da ise bu servisleri yönetiyorsunuz (OpenVPN, IPSec, IDS, Zaman sunucusu gibi). Beşinci sekme "firewall". Burada firewall'un o meşhur mu meşhur port engellemeleri izinleri yapılıyor hangi kullanıcılar veya gruba ne izinler vereceğiniz de ayarlayabileceksiniz.
 Bir sonra ki konu Zentyal ile küçük küçük alıştırmalar.
