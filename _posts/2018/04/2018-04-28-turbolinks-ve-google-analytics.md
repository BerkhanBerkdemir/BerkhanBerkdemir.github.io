---
layout: post
title: Turbolinks ve Google Analytics
author: Berkhan Berkdemir
date: 2018-04-28
---

İki gündür beni deli edirten bir Google Analytics sorunu var. Aslında pek hani hata çıktısı veren bir değil o yüzden daha sinir bozucu gidersin trace tree yi okursun bulursun sorunu.

Neyseki sorunun çözümü biraz sonrasında buldum.

## Sorun

Google Analytics'in kendi "Universal" scriptini kullandığınız zaman kullanıcı hareketleri doğru gelmiyor. Örneğin kullanıcı daha root path de ise Google Analytics (daha doğrusu analytics.js) değiştiğinin ruhu bile duymayacak ve kullanıcı belki de o sırada user login sayfasına giricek ama dashboard da siz halen root path da duran bir kullanıcı göreceksiniz sonrasında o kullanıcı bir anda disappear olucak.

Bu sorunun Turbolinks olduğunu aslında dün sabah fark ettim ve girdim araştırmaya bir sürü tread okudum, Medium da yazı okudum yok arkadaş sanki hepsi anlaşmışlar hatalı şeyler paylaşalım da.

Sonunda buldum. Bugün. Az önce. Birazcık "oha bu kadar basit mi idi?!??!?!?!?" durumuna girdim. Ama code u (adamın anlattıklarını değil) okuyunca anladım olayı.

## Çözüm

```erb
<!-- app/view/layout/application.html.erb -->
<script>
<% if Rails.env.production? %>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('require', 'linkid');
  ga('create', 'UA-XXXXXXXX-X', 'auto');
<% else %>
  function ga() { console.log("Google Analytics"); }
<% end %>
</script>
```

```javascript
// app/assets/javascripts/analytics.js
$(document).on('turbolinks:load', function() {
  ga('send', 'pageview', window.location.pathname);
});
```

> Eğer uygulamanızda ki Turbolinks sürümü 2.x ise kodda ki `turbolinks:load` u `page:change` olarak değiştirin. Kısaca bu kod 5.x de sorunsuz çalışıyor ki ben kendim kullanıyorum şuan.

Unutmadan, bu JavaScript parçası jQuery istiyor. O yüzden emin olun jQuery bu JS parçasından önce yüklenmesi gerek. Eğer bir JS ci el atarsa bu parçanın sadece JS veya Coffee'li sürümü güzel olur. Buyrun bu da nerden buldum bu parçayı [linki](http://nithinbekal.com/posts/turbolinks-google-analytics/)
