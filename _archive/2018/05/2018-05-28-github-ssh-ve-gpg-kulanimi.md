---
layout: post
title: "GitHub'da SSH ve GPG kullanımı"
author: Berkhan Berkdemir
date: 2018-05-28
---

GitHub'da SSH veya GPG kullanmanın zorunlu olmadığını belirtmek isterim. Öncelikle hangi koşullar anltında SSH veya GPG'nin kullanılması gerektiğini belirtmek istiyorum.

# GitHub HTTPS mi yoksa SSH mı?

Eğer yeni başladıysanız kesin kez HTTPS kullanmanızı öneriyorum çünkü herhangi bir setup ile uğraşmadan direkt olarak `git` komutlarını çalıştırabilirsiniz ama bir müdetten sonra bir aksiyon istiyorsanız -benim gibi- sizi SSH kısmına davet ediyorum.

## Peki SSH'ın avantajları neler?

HTTPS'de her seferinde credentials detayları girmek gibi bir zulümden kurtulursunuz. Düşünün benim gibi bir kullanıcı adınız olduğunu; her seferinde 16 karakter girmek...

Tabiki bu durumda `git`in de sihirli marifetleri olduğunu söyleyeceğim

```bash
git config --global credential.helper "cache --timeout=3600" # 1 saatlik credential caching
```

Bu satır ile bulunduğunuz Repository'nin credential bilgilerini caching yapıp her pull veya push da bu zulümden yine kurtuluyorsunuz ama bir noktaya dikkatinizi çekmek isterim

*Bulunduğunuz Repository*

Evet bu durum biraz can sıkıcı olabilir eğer ki birdan fazla Repository üzerinde çalışıyorsanız. Bu yüzden size önerim SSH ile çalışmanız olucak.

# GPG'de nedir?

Tam Wiki açıklaması yapamayacağım çünkü detaylı olarak kullandığım ve bildiğim birşey değil ama GPG'nin asıl kullanım alanı birşeyi onaylatmak.

GitHub'da commit history'e baktığınız zaman yanlarda birkaç tane "Verified" yazar aynı aşağıda ki görsel gibi

![GitHub'da verified commit](2018/05/github-ssh-ve-gpg-kullanimi.png)

Bu durumda bu commit sizin bilgisayarınız'dan çıktığını kanıtlamış oluyorsunuz.

Tekrardan hatırlatmak isterim bu yapıcağımız işlemlerin hiçbiri zorunlu değil. Ben sadece burada nasıl kullanılacağınızı göstereceğim. Aynı zamanda platformum olarak Ubuntu 18.04 kullanıyorum. Yani MS Windows veya Mac OS X kullanıyorsanız durumlarda değişiklik gösterebilir ama baz aldığım dökümantasyon [şurada](https://help.github.com/categories/authenticating-to-github/) ve her üç büyük içinde detaylı bilgi bulunmakta.

# GitHub ile SSH kullanımı

> Eğer öncesinde SSH sistemini AWS, Azure veya Heroku gibi sistemlerde kullandıysanız yapmanız gereken değişiklikler dışında birkaç işlem daha olabilir. Bu konu hakkında kapsamlı bir SSH blog/dökümantasyon'u okumanız iyi olucaktır çünkü burada o noktalara değinmeyeceğim.

Öncelikle terminalimizi açalım ve hemencik bir SSH anahtarı oluşturalım.

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Dökümantasyon belirtmiyor o yüzden bir birşey diyemiyeceğim, eğer ki şifrenizi publice gizlediyseniz. Yani demem o ki burada GitHub'a login olurken ki mail adresinizi girmeniz gerekiyor.

Üst taraftaki komutu çalıştırdığınız zaman terminal sizden birkaç sorunuza yanıt bekliyor olucak. Öncelikle yeni anahtarın nereye kayıt olacağı. Bu kısmı Enter'a basıp geçebilirsiniz ama uyarmakta fayda var -aynı zamanda ssh-keygen de uyarıcak- eğer eski bir `id_rsa` varsa bu silinecek.

İkinci sorusu ise bu key için şifre girmeniz olucak. Bu kısım genel anlamda bir şifreden bahsediyor olucak, hesap şifreniz değil.

## SSH anahtarı ssh-agent'a tanıştırmak

Öncelikle arka planda `ssh-agent`'ı çalıştıralım.

```bash
eval "$(ssh-agent -s)"
Agent pid 59566 # pID olarak random bir rakam alıcaksınız
```

ve en yapıcağımız işlem bu anahtarı ssh-agent'a gösterelim.

```bash
ssh-add ~/.ssh/id_rsa
```

Bilgisayarımızda yapacağımız işlemler bu kadar. Şimdi'de GitHub hesabımıza girelim ve şu path'ı takip edelim

Settings > SSH and GPG keys > New SSH key

Burada title kısmına yararlı birşeyler girmeniz iyi olucaktır çünkü ileride "yahu bu kimin anahtarı" demenize gerek kalmasın. Mesela "Mutfak PC" - tam bir Windows örneği oldu.

Key kısmını nerede mi bulucaksınız? Elbette local bilgisayarınızda `~/.ssh/id_rsa.pub` dosyasında. Bundan iki tane olucak birisi .pub olan ve olmayan. Bu dosyanın içinde ki verilerin hespini kopyalaın ve GitHub'ın içine atın.

Şimdi mi? Hazırsınız SSH'ı kullanmaya!

# GitHub ile GPG kullanımı

> GPG hakkında derin bir bilgim olmadığını söylemek istiyorum. Eğer bir yerden yanlış bir işlem yapıyorsam söyleyin ama dökümantasyon olarak yukarıda da belirtiğim gibi [şurayı](https://help.github.com/categories/authenticating-to-github/) takip ediyorum

```bash
gpg --full-generate-key
```

`RSA and RSA` kullanmamız gerekicek o yüzden enter ile default'u seçelim. Sonraki kısımda ise anahtar uzunluğu olarak en yüksek değer olan 4096 yu girelim ve Enter'layalım. Şimdi ise kimlik bilgileriniz gelicek. Bu kısıma kullanıcı adınızı girin. Email kısmına ise GitHub'da kullandığınız değeri giriceksiniz. Dikkat edelim, eğer GitHub ile kullandığınız mail adresiniz Private ise bu değer Settings > Email kısmında bulucaksınız.

> Comment kısmına takılmanıza gerek yok. O bilgi sadece sonrasında onun ne olduğunu hatırlatmak için. Ama ben bu durumda `GitHub GPG` dedim

Yine bir password giriceğiz. Bu değer GitHub ve SSH key şifreniz ile farklı olabilir ama unutmayın bu değer her commit sırasında kullınacağız.

```
gpg --list-secret-keys --keyid-format LONG
/home/berkhan/.gnupg/pubring.kbx
--------------------------------
sec   rsa4096/2473423C5BC3527D 2018-05-28 [SC]
      76*C*9****4E4B5***B14*9******23C5***5*7D
uid                 [ultimate] BerkhanBerkdemir (GitHub GPG) <********+BerkhanBerkdemir@users.noreply.github.com>
ssb   rsa4096/*******38*67***A 2018-05-28 [E]
```

Yıldızlar haricinde bir çıktı alıcaksınız. Bu çıktıdan `rsa4096/` yanında ki değeri bir yerde saklayın çünkü bunu kulanıcağız nasıl mı?

> Herkes de bu değerler farklılık gösterebilir. Rakamlara takılmayın. Sadece yaptığımız kısma odaklanın.

```bash
gpg --armor --export 2473423C5BC3527D
```

dediğimiz zaman uzunca bir çıktı alıcağız ve bu yazının başında `-----BEGIN PGP PUBLIC KEY BLOCK-----` ve `-----END PGP PUBLIC KEY BLOCK-----` yazmalı.

Şimdi sıra bu GPG değerini GitHub'ın içine atma

Settings > SSH and GPG keys > New GPG key

burada tek bir kısım görüceksiniz o da sadece GPG anahtarımızı koyucağımız yer. Az önce bir output almıştık terminalden bu değeri buraya yapıştıralım ve onaylıyalım.

Ve en son sihir. git programına haber verelim bu GPG anahtarı hakkında. Az önce kopyaladığımız değeri hatrlarsınız, 2473423C5BC3527D.

```bash
git config --global user.signingkey 2473423C5BC3527D
echo 'export GPG_TTY=$(tty)' >> ~/.bashrc
```

Buraya kadar tamamız. Peki ben Commit veya Tag işlemlerini nasıl onaylarım? Sorunun cevabı basit. Eğerki Commit'lerinizi default olarak verify yapmak istiyorsanız buyrun komutu burada

```bash
git config --global commit.gpgsign true # Default Commit verify
```

Ama dilerseniz ki her seferinde el ile yapmak istiyorum

```bash
git commit -S -m "Hello, World!"
```

Yani `-S` flagı sorunuza cevap olucak. Aynı şekilde tag oluşturmakda öyle

```bash
git tag -s "v0.1.0"
```

Bu kısımda ise `-s` flagını kullanacağız.

# Son söz

Biraz komplike gözükebilir ama sonuçta bunu birkez yapıcağınız ve belkide bir daha hiç kurcalayamacağınız için bence değer.
