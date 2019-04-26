---
layout: post
title: "Neden Middleman'den Wordpress'e geçtim?"
author: Berkhan Berkdemir
date: 2018-05-25
---

Wordpress hep sevdiğim bir Content Management System oldu, oluyorda. Özellikle son zamanlarda kendisini ileriye atan bir ekibi varken Twitter'da "vay be, adamlar yapıyor" tarzında yorumlara giriyorum. Bilirsiniz ki şu sıralar birde GPDR konusu meydana geldi ki bence şuan Avrupa'da ki bütün websitelerinde, sistemlerde çılgınlar gibi bu konuda çalışma sürüyor ve bugün de o gün zaten. Koskoca 43 tane yazıyı, resimleri (bir çoğu şükürler olsun cloud'da tutuyorum) herşeyi bir anda taşımak dilerseniz ki zor hele ki bunu el ile yapmak bence daha da zor ama beni bu işi yapmam için sürükliyen birkaç konu oldu ve bu yazımda bunlara değineceğim.

Belirtmem'de fayda var bu siteyi ilk açtığımda farklı bir <a href="https://linuxkafasi.org">domainde</a> açmıştım ve Wordpress kullanıyordum (2015). Uzun bir süre yazı yazmayınca bende Jekyll'e geçtim çünkü hem Ruby ve Rails öğrenmeye başladım diye hemde o sıralarda hosting sağlayıcım beni delirticek şekilde saçma çökmelere sebep olduğu için. Kısa bir süre önce de Türkçe blogumda ki içerikler ile İngilizce olanınkini birleştirmek istedim ama Jekyll'de düzgün bir plugin bulamadığım için Middleman (bir static site generator framework aslında) geçtim çok kısa sürede iki dil üzerinden çalışabildiğim bir statik bir sitem oldu ama birşeyler eksikti.
<ul>
 	<li>Blog yazmaktan çok sitemin templatine fix veya featureları ile uğraşıyordum.</li>
 	<li>Feedback sistemim çok kulanışlı değildi ve anonim yazanlar sıkıntı yaşıyordu aynı zamanda limitli bir formum vardı.</li>
 	<li>Google Analytics ve CDN artık kullanmayacağıma karar verdim.</li>
 	<li>Telefonumdan veya bilgisayarımdan sorun yaşamadan, gözümü ağrıtmadan yazı yazmak istiyordum.</li>
 	<li>Wordpress'in "Post formats" özelliğini birkaç templatede görünce kullanmak istedim.</li>
 	<li>Guttenberg projesi beni her seferinde heyecanlandırıyordu.</li>
</ul>
Kısaca beni SSG'ye iten birçok olay sonrasında aslında gerek yok düşüncesine çekti. Bunun ile birlikte fark ettim ki SSG sistemler <em>SEO konusunda</em> çok başarılı değil. İyi hatırlıyorum ki ilk WordPress blog sitemi açtığımda Yoast SEO vardı (halen varlar ve iyi iş yapıyorlar) ve çok kısa bir sürede Google'da search edilebilir hale getirdi yazıları kendisi.

Şunu da eklemek isterim, birçok sistemi, yazılımı veya dili denemeyi seven birisi olarak bu benim en sevdiğim huy olduğunu söyliyebilirim çünkü bunu küçük yaşta fark ettim; gerçekten o şeyin içinde yaşamam gerekiyor ki onu öğreniyim.

Bu konuda örnek vermem gerekirse Docker'ı öğrenmeye başladığım zamanı (2016) ele alabilirim. O zamanlarda Oracle Virtualbox ile birçok işlemi yapıyordum ve düşündüğünüz gibi işleri yapmak zordan çok uzundu. Her seferinde yeni sistem kurmak veya o sistemin klonunu almak sonrasında en basitinden IP değiştirmek gereksiz vakit kayıplarıydı. Sonrasında gerçek senaryolarım üzerinden PHP, MySQL ve Docker'ı kullanmaya basladım. Şu an çok iyi bir şekilde kullandığımı söyliyemem ama anlatabilecek kadar kullanabiliyorum.

Diğerki önemli nokta ise geçişim hakkında yeni bir hosting sağlayıcısına geçtim. Ne kadar kendileri ilk başlarda <a href="https://twitter.com/BerkhanBerkdemi/status/999624872488665088">beni çıldırtsalarda</a> geçmiş bulundum.

Sonuç olarak geldim işte ve şu an kullanıyorum. Nerden bilebilirsiniz belki 2 ay sonra yine değiştiricem belki sonraki durak Joomla!? Bilemeyiz.
