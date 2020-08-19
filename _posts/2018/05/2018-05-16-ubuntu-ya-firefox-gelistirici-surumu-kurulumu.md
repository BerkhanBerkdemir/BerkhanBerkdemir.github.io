---
layout: post
title: "Ubuntu'ya Firefox geliştirici sürümü kurulumu"
author: Berkhan Berkdemir
date: 2018-05-16
---

Birkaç ay öncesinden Mozilla ekibi yeni Firefox Quantum'u tanıttılar ve birçok geliştirici gibi çıldıranlar arasında bende vardım.

> İyi de bir "web browser" için neden böyle birşey yapılır
>
> Anonim

diye sorabilirsiniz. Haklılık payınızda var ama bir noktayı kaçırıyorsunuz. Firefox'u sıfırdan inşa ettiler diye düşünün bu güncellemeyi çünkü kendi dilleri olan Rust ile kendi tarayıcı motorlarını oluşturdular ve buna Quantum olarak adlandırdılar.

Sonuç ise muazzam. Kendi yaptıkları performans testlerinde *iki katdan fazla* performans aldıklarını öne sürüyorlar eski Firefox sürümüne göre.

Elbette olay sadece performans ile de kalmadı. Firefox artık daha oyun hamuru kıvamına geldiğini ve web geliştiricilerin artık sadece Google Chrome takılı kalmasına sebep bulmayacak bazı küçük oyuncaklar geliştirdi.

Bunlardan biriside [**Firefox Developer Edition**](https://www.mozilla.org/firefox/developer/)

Benim Dev. Edition'a geçmemde ki sebep kesinlikle ismi değil. Sonuçta aynı tool seti (DevTools, View-source, Web-IDE) normal Firefox'ta da var.

Peki neden geçtim?

1. Merak
2. Gelişmelere daha yakın olmak

Yeni parçaları denemek hoşuma gidiyor heleki açık kaynak kodlu ise. Amacım ila contribution da bulunmakta değil. Diğer ki kısım ise şöyle; Ubuntu'nun kendi deposunda yine Firefox var ama bu sürüm stable sürüm ki benim istediğim şeyi alamıyorum. Elbette normal kullanıcılar için normal ama yaptığım şey normal değil durumunu da göze alarak Beta yazılımlarını kullanmayı seviyor oldum.

## Firefox Dev'i indirelim

> Öncelikte hatırlatmakta fayda var. Ben burada eski Firefox sürümünü (bu tarih ile 60) komple silicem. Kısaca şunu demek istiyorum, eski bookmarklarınızı, pluginleriniz nasıl backuplarsınız bilmiyorum. Yani o işlemleri burada görmeyeceksiniz.

İlk önce eski Firefox sürümümüzü sakince kaldıralım

```shell
sudo apt remove -y firefox
sudo apt autoremove
sudo apt autoclean
```

Ve yeni Firefox'un tar.bz2 dosyasını indirelim `wget` komutu ile.

> [Firefox'un FTP sunucusunda](https://ftp.mozilla.org) 2004 yılına ait 1.0 sürümünü bile bulabilirsiniz.

```shell
mkdir /tmp/download # Geçici bir klasör yapalım, sonrasında gerekmeyecek çünkü
cd /tmp/download
wget "https://ftp.mozilla.org/pub/devedition/releases/61.0b5/linux-x86_64/en-US/firefox-61.0b5.tar.bz2"
mv firefox-61.0b5.tar.bz2 f.tar.bz2 # Daha okunaklı birşey olsun
tar -xf f.tar.bz2 # Bu komut ses çıkarmaz ama -v eklerseniz çıktıyı görebilirsiniz.
sudo mv firefox /opt # Ben bu yazıda /opt a yolluyorum isterseniz /usr/local yapabilirsiniz
```

Buraya kadar yorumlari okuyarak geldiyseniz güzel. Sırada Firefox'u Gnome'da kullanmak üzere hazırlıklara girişelim. Tek ihtiyacımız olan şey `firefox.desktop`.

```
[Desktop Entry]
Name=Firefox Developer
GenericName=Firefox Developer Edition
Exec=/opt/firefox/firefox %U
Terminal=false
Icon=/opt/firefox/browser/chrome/icons/default/default128.png
Type=Application
Categories=Application;Network;X-Developer;
Comment=Firefox Developer Edition Web Browser.
StartupWMClass=Firefox Developer Edition
```

Yukarida paylaştığım küçük .desktop şeysini kopyalayın ve `/usr/share/applications/firefox.desktop`'a yapıştırı verin.

Birde eğer terminalde clicklenebilir bir URL'e gelirseniz küçük bir hack yapmanız gerek `.bashrc`'de. En son kısma şunları eklerseniz sorunuzu çözecektir.

```bash
# For sensiable-browser
export BROWSER=/opt/firefox/firefox
```

Şimdi ise tek bir adım kaldı. O da open source tabanlı bir web browser'ın tadını çıkartmak.

![Firefox Developer Edition first run](https://i.imgur.com/7zx0cUG.png)
