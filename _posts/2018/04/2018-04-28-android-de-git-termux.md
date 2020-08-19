---
layout: post
title: Android'de git - Termux
author: Berkhan Berkdemir
date: 2018-04-28
---

Android bilirsiniz ki arka planı Linux Kernel üzerine kurulu ve bu size çok güzel bir oyun alanı sunuyor ama bu oyun alanında biraz fazla kural ile çok kısıtlı oyun oynuyorsunuz. Çok sıkıcı değil mi.

Örneğin terminal e erişim sağlamak için klasik bir yönetimin olmayıp piyasada ki bir çok APK nın kullanışsız olması...

Bu durumda ben bir çözüm buldum. Termux.

Kendisi bir "Linux terminal emulator" Android için. Bu APK size BusyBox paketini de sunuyor ve cidden Linux cihaz kullanıyor konforunu veriyor. Hatta daha güzeli kendi paket yöneticisi sistemi var. Aynı APT veya YUM gibi.

Biz işte bu paket yöneticisi kullanarak git indireceğiz. Hadi başlıyalım

## Termux'u indirelim

Android Playstore dan [link](https://play.google.com/store/apps/details?id=com.termux)de ki Termux'u indirelim.

> Termux, Android version 5 sonrası için destek veriyor.

## git kurulumu

```shell
packages install -y git # veya apt install -y git
git config --global user.name "BenimMukemmelKullaniciAdim"
git config --global user.email "benimmukemmel@email.adresim"
```

Ve bu kadar. Artik Android cihazınız ile bir git projesini rahatlıkla klonyalabilirsiniz.

### Peki eğer bir GitHub, GitLab hesabınız varsa nasıl olacak?

`user.name` kısmına kullandığınız sistemde ki kullanıcı adınızı, `user.email` kısmına da yine kullandığınız sistemde ki email adresinizi yazıcaksınız.

## Bazı hayat kurtaran kısa yollar

> CTRL tuşu eğer ki klavyenizde yok ise önce `Ses arttırma + Q` çalıştırın

| Kısa yol           | Açıklama          |
| ------------------ | ----------------- |
| `CTRL + D`         | Terminalden çıkış |
| `CTRL + L`         | Terminali siler   |
| `CTRL + C`         | İşlemi durdur     |
| `Ses arttırma + P` | Page Up           |
| `Ses arttırma + N` | Page Down         |
| `Ses arttırma + Q` | Ekstra tuşlar     |
| `Ses arttırma + E` | ESC               |
| `Ses arttırma + T` | Tab               |
| `Ses arttırma + W` | Yukarı karakteri  |
| `Ses arttırma + S` | Aşağı karakteri   |
| `Ses arttırma + A` | Sol karakteri     |
| `Ses arttırma + D` | Sağ karakteri     |
