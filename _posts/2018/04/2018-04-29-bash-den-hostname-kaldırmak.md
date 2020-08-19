---
layout: post
title: Bash'den hostname kaldırmak
author: Berkhan Berkdemir
date: 2018-04-29
---

Bilirsiniz ki Ubuntu da standart olan bir parça varsa o da Bash. Bash aslında bir shell ve bir programlama dilidir. Ben bu yazımda azıcık hacklediğim birşeyi göstermek istiyorum.

Bunu yapmamda ki sebep hostname olduğu zaman cidden 80 columns olan alanın zaten yarısı gidiyor ki bu da hoş birşey değil. Amacım `username:pathname($/#)` şeklinde gözükmesi

Aslında bu alışkanlığı zsh da iken buldum. Oh-My-Zsh ile çok tembelleştim diye tekrar Bash'a geri döndüm.

Neyse ki çözümü var ve amaç burada `PS1` değişkenini değiştirmekten ibaret.

Yapacağımız ilk şey favori text-editörümüz ile `.bashrc` dosyasını editlemek olacak. Bu dosyayı sizin kendi home directorynizde bulabilirsiniz.

Pekala nasıl mı emin olacaksınız home dirde olduğunuzu?

Eğer command promptun yanında `~` (tile) varsa bu denemetir ki siz o kullanıcı olarak home dirdesiniz.

Ben direkt paylaşmak istiyorum eski ve yeni kodları. Burada geriye kalan kısım `PS1` değişkenini bulmak o kadar.

```bash
if [ "$color_prompt" = yes ]; then
    OLD_PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
    PS1='\[\033[01;32m\]\u\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    OLD_PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
    PS1='\u:\w\$ '
fi
```

if statement ın içinde ki değer tahmin edebileceğiniz (okuyabileceğiniz) gibi Bash'a color support veriyor ki o yüzden bu kadar uzun bir code çıkarttı.

Burada bazı değişkenleri anlatmak isterim

| Değiken adı | Açıklama               |
| ----------- | ---------------------- |
| `\u`        | Kullanı adı            |
| `\h`        | Hostname               |
| `\w`        | Buldunuğunuz directory |
| `\$`        | $ veya # yerleştirir   |

Bu işlemi yaptıktan sonra yapmanız gereken terminalden komple çıkmak çünkü `.bashrc` üzerinde bir işlem yaptık.

Peki nasıl görünüyor du eskisi?

![Before bash](https://i.imgur.com/jQPd1a5.png)

![After bash](https://i.imgur.com/pUeajqr.png)
