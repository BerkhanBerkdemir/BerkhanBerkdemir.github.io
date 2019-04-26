---
title: Citrix Xen Server 6.5 local de ISO kütüphanesi hazırlanması
date: 2016-09-26 TRT
author: Berkhan Berkdemir
layout: post
---

Bu yazım aslında bilgilendirme amaçlı olacaktır ve konusu Citrix Xen Server 6.5, 6.5 SP1 hatta 7 üzerine rahatlıkla uygulayabileceğiniz bir fonksiyondan bahsedebiliriz.

Hazırlanması kadar kullanımıda çok basit olacaktır. Aslında neden ihtiyaç duyduğunuda size bahsetsem güzel olacaktır.

## ISO Kütüphanesi hazırlanması

Aslında Xen Server'a geçen çoğu kişi VMWare ESXi gibi bir sistemden geçtiğinden dolayı *local iso library* arayışında bulunmuyor değil insan. *New SR*'a baktığınızda ise sadece Remote olarak bağlanmanız sizi hemen üzmesin.

Biraz araştırma ile zaten buraya geldiniz. Ben hemen size istediğiniz satırları vereyim

```
mkdir -p /var/opt/xen/ISO_Kutuphane
```

Bu satır ile siz `/var/opt/xen` in altında `ISO_Kutuphane` adında boş bir klasör elde etmiş oluyorsunuz. Bu ilk kısımdı. Şimdi burası en önemli yer,

```
xe sr-create name-label="ISO Kütüphanem" type=iso device-config:location=/var/opt/xen/ISO_Kutuphane device-config:legacy_mode=true content-type=iso
```

satırı ile sisteminiz hazır. Şu an sunucunuz üzerinde local bir iso kütüphaneniz bulunmakta.

### Wget ile dosya çekme

aslında wget in bazı fonksiyonlarıda anlatmak isteyeceğim bu satırlarımda. Ama en basit kullanımı ile başlayacağım.

```
wget www.isodunyalari.com/opensuse/opensuse13.2/opensuse13.2_amd64.iso
```

ve enter'a bastıktan sonra dosya bitene kadar ekranınızda kalacak. Buda sunucu yöneticilerinin pek istemediği olayki onun da en basit kullanımı

```
wget -bcq www.isodunyalari.com/opensuse/opensuse13.2/opensuse13.2_amd64.iso
```

Aslında burada biraz da linux veya terminal kullanımı ile uygulamalarda ki fonksiyonlarına da birazcık değişmiş oldum denebilirim.
Sırası ile `-b` : background çıktı verir ama bilgilendirme çıktılarıdır `-c` : continue bağlantı kopsa dahi tekrardan devam etmesi `-q` : quite ise sistemin ses çıkartmadan devam etmesi diyebilirim.

> `-b` : size *PID* kodu verir. Sistemi durdurmak isterseniz PID kodu ile kill yapmanız gerek uygulamayı
> `-c` : continue bağlantı kopsa dahi tekrardan devam etmesi
> `-q` : quite wget hiçbir şekilde çıktı vermez

Vereceğim bilgilerim bunlar. Umarım işinize yaradı. Sorularınızı yorumlardan veya bana iletişim formunu doldurarak yaparsanız sevinirim..
