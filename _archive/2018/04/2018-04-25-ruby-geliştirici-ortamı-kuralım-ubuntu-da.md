---
layout: post
title: Ruby geliştirici ortamı kuralım Ubuntu'da
author: Berkhan Berkdemir
date: 2018-04-25
update: 2018-04-28
---

Merhaba arkadaşlar,

Bilirsiniz ki bir geliştirme ortamı (dev-env) kurulumu kadar basit birşey olamaz. Tabiri caizse next-next-next. Şaka yapıyorum. Cidden doğru kurulması gereken birşey. Ben 2 sene de şunu öğrendim. Basit diye bir kavram yok bilgisayarda. `Hello, World!` ü 300 farklı şekilde de yazarsın, sadece sana basit olanı gösterirler. Bende işte bu yazımda basit olanı göstericem. Endişelenme, uzun olabilir ama aradaki hikayeleri atlamak "up to you".

Ben bu yazımda spesifik olarak Ruby (ozellikle Rails), Docker (alt yapı icin) gibi araçlar kullanacağım. Aynı zamanda GitHub entegrasyonu ile bazı Atom editör tweakleri yapacağız.

Musadeniz ile başlıyalım.

Bi saniye, başlamadan önce birkaç parçaya ihtiyacınız varki bunları Tahtakale'den bulamazsınız, yine internetten bulacaksınız ki şükürler olsunlar bedavalar.

* Herhangi Ubuntu flavor ve versiyon (Ben burada düz 17.10 kullanıcam ama 16.04 e kadar uyumlu olacaktır bu yazdıklarım (umuyorum))
* GitHub account

## Atom editör'ü indirelim.

Atom'u seviyorum ve açık kaynak kodlu projelerimde sadece Atom kullanıyorum. Atom hakkında kısaca özetlemek gerekirsek bir Hack-Tool. Öyle dediğime bakmayın, herhangi bir "hack" yeteneği yok bildiğiniz notepad. Bunun özelliği bu yazılımı hamur gibi şekilden şekile sokabiliyorsunuz (yazdığım yazılar Atom ile yazıyorum).

GitHub entegrasyonu cok basit oldugundan da kullanmayı seviyorum. Elbette JetBrains'de de bu ozellik var hatta dahası ama parantez açarak belirtmek isterim. JetBrains'in ürünleri IDE dir. Atom ise text-editor.

Çok renkli bir packages sistemi var Atom'un. Göz atmak isterseniz buyrun [linki](https://atom.io/packages)

> Öncelikle hatırlatmakta fayda var. Ubuntu, Debian üzerde gelişmiş bir Linux flavor'dır (bunun Türkçesi pek bir yerinde olmuyor). Yani bazı şeyleri yüklerken veya configure ederken Debian wikileri de işinizi görücektir ama şuan işimiz yok bunlar ile. Sadece küçük bir bilgi.

Bu yazıyı yazarken Atom versiyon 1.26.0. Betası ise 1.27 li birşey. Ben burada stable versiyon kurucam ama dilerseniz ki beta sürümünü indirerek Atom ekibine feedback verebilirsiniz.

Buyrun Atom'un [linki](https://atom.io/)nide şuraya sıkıştırıyım.

Buradan iki tip indirme seçeneğiniz var. Ya Source Code indirip iki dakikalığına kendinizi Haçkır hisederseniz ya da en akıllıca seçim olan paketlenmiş sürümü indirirsiniz. Ayrıca Source Code indirseniz dediğim şaka. Ciddiye almayın. Linçlemeyin. Şurada iki shell in belini kırıyoruz dimi.

Pekala indirdikde, bu nasıl çalışır? Bataryası dahil mi? Elbette dahil. Yoksa nasıl popüler olucak bu kadar dimi.

### Deb package

MS Windows alışkanlığınız Ubuntu da yine devam edebilir nasıl mı? Sadece yapmanız gerek DEB package i indirmek ve çift tıklamak. Gerisini Ubuntu (veya Debian) hallediyor.

### Source Code

Cidden hiç denemediğim, denemeye gerek duymadığım bir yöntem. Ama internet çöplüğünden bulanabilmesi zor olmayacak bir bilgi. Buyrun DuckDuckGo da yazmak ile uğraşmayın diye de query [linki](https://duckduckgo.com/?q=How+to+install+Atom+from+soruce+code&t=canonical&ia=web)

> Kendi orjinal dökümanları bulunmakta ayrıca ekliyim dedim [linki](https://flight-manual.atom.io/getting-started/sections/installing-atom/#installing-atom) de.

İndirdiyseniz sonraki seviye aşağıda.

---

Çalıştırmanız için yapmanız gerekşey `Terminal` i açarak

```shell
cd /home/projemin/yolu/tasdan
atom .
```

İlk kısım tamam. Şimdi biraz arka taraf için hazırlananalım

## _Git_ şeysi

Bi'kere kabul edelim, git ezdi geçti diğerki versiyon kontrol sistemlerini. Belki Subversion'cu sundur bilmem ama ben burada Git ve GitHub dan anlatacağım. Bu yüzden o bilgileri buradan bulamazsın dostum.

Güzeldir git, severiz kendisini.

Ubuntu 17.10 (aslında sadece bu versiyon değil bütün Linux flavorlarında artık) da çok basit bir şekilde indirebilirsiniz git i. Nasıl mı?

```shell
sudo apt install -y git
```

Herhangi komplike birşey yok indirme sırasında fark ettiğiniz gibi. Şimdi birkaç küçük dokunuş zamanı, aynı [Bob Ross](https://duckduckgo.com/?q=Old+painter+on+TV&t=canonical&ia=web) gibi.

```shell
git config --global user.name "LoremIpsum_DolorSitAmet"
git config --global user.email "lorem_ipsum_sit@gmail.com"
```

Şimdi niye böyle havali şeyler yazdınız diyebilirsiniz ama bilmeniz de fayda var alt tarafa koyucam neden böyle birşey var diye.

> "Lorem ipsum..." latince bir kavram olan eskiden matbaa da kullanılan bir örnek metin imiş. Digital zaman ile şimdi web geliştirileri kullanıyor. Şahsen işe yarıyor. Eğer merak ediyorsanız buyrun burada onun da [link](https://lipsum.com)i

Birinci kısma GitHub, GitLab veya BitBucket veya herhangi bir kendinize ait sistemde ki kullanıcı adınızı giriyorsunuz, ikinci kısmı ise aynı şekilde sizin siz olduğunuza kanıtlayacak (çünkü ileride bunu SSH keylerinde kullanacaksınız unutmayın) bir email adresi. Hatırlatmakta fayda var. Eğer üç büyükten (GitHub, GitLab, BitBucket) bir hesabınız varsa, mail kısmına oradakiler hesabınızın mail adresinizi girerek yapıcaksınız. Bu konuda eğer kafanızda birşey takıldıysanız disqusalım (hoş oldu) aşağıda.

### _Git_ şeysini SSH ile kullanalım (tamamı ile opsiyonel)

Bunu yapmanızı neden öneriyorum, çünkü iki commit arasında şifre sorulmaz derler. Yok öyle birşey. Şuan aklıma geldi. Neyse, asıl sebebi aslında gayet açık.

~~Güvenli~~. Yok daha neler. Öyle bir neden dolayı değil aslında. Sıkça şifrenizi girmek gibi sıkıcı birşey den uzak duruyorsunuz bu kadar. Eğer birden fazla sistem kullanıyorsanız hatırlatmakta fayda var. Ben şuan GitHub için olanı anlatacağım belki GitLab da farklılık göretebilir bu process. O yüzden bir search query yazmaktan zarar çıkmaz.

Hadi başlıyalım. (Bu kısım hacker yeteneği gerektirmez. Basbaya copy paste yap. Ama yazdıklarımıda bir göz at belki istemediğin birşey yapıyorsundur)

> Ayrica buyrun bu da orjinal [link](https://help.github.com/articles/connecting-to-github-with-ssh/)i GitHub tarafafından

```shell
ssh-keygen -t rsa -b 4096 -C "lorem_ipsum_sit@gmail.com" # Yeni bir sertifika oluşturalım. Bu sertifikada şu mail adresi adına olucak ve uzunluğuda 4096 olup, RSA tipinde olucak

...
Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
...
# Burayı enterlamanız yeterli eğer id_rsa zaten başka birşey tarafında kullanılıyorsa buraya hemen onu yaz.

...
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
...
# Nedenini bilmediğim bir şekilde benim araştırdığım iki üç yerde GitHub account password u kullanın diyor.

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa # SSH Agent a ekliyelim bu sertifikayı
reset # Temizleyelim etrafı. Clean de kullanabilirsin
cat ~/.ssh/id_rsa.pub # Şimdi burayı komple copy paste yap. Kullanıcaz bunu.
```

Şimdi kopyaladınız değil mi? Hafifçe GitHub hesabımızı açalım ve oradan Ayarlar kısmından SSH & GPG Keys kısmına gidelim. Bizim elimizde şuan SSH key var. Oradan yeni SSH key ekle kısmına tıkalyın ve Description kısmına mesela Ubu17.10-home yazabilirsiniz. Altta ki kısma ise panomuza kopyaladığımız şeyi yapıştıralım ve hazırız. Artık SSH ile git işlemlerinizi daha hızlı yapabilirsiniz.

> Ben size dedim şifre daha _az_ giriceksiniz diye, hiç demedim ama bu konuda çözümünüz var. Meslea bir daha sorma diyebilirsiniz git clone veya git push yaparken. Terminalcikte sormayacak bir daha.

Eğer herhangi bir kısım pek açık değilse düzelti veriyim

## Temiz bir NodeJS ve Yarn

Rails nedendir bilinmez (hızlı kabul edelim yani) Yarn kullanıyor JS dependencies için. Bizde NodeJS 9 ve Yarn 1.6 indiriceğiz. Aslında çok da marifetli şeyler yapmayacağız. Sadece copy paste.

```shell
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
sudo apt update && sudo apt install -y nodejs yarn
# Eğer kontrol etmek isterseniz sürümleri buyrun flagları
nodejs -v
yarn --version
```

## Ruby'i indirme zamanı geldi

Ben burada Ubuntu da default olarak bulunan Ruby sürümünü indiricem ki o da 2.3. Ama dilerseniz ki bir sürü yöntem ile latest veya development versiyonlarınıda indirebilirsiniz (Mesela rbven).

Ayrıca, ben değişen durumlara göre PostgreSQL, MySQL veya SQLite kullanabiliyorum ki bu neden ile ben 3 adaptörün dev packagesını indiricem.

> Gem paketi olan Nokogiri kurulumu cidden saç yolduran ne olduğunu anlamayacağınız birşey. Cidden ben bu dev envi kurana kadar 5-6 kere almişimdir eksik dev packages hatasını.

```shell
sudo apt install ruby-dev build-essential patch \
    libssl-dev libreadline-dev libyaml-dev \
    libsqlite3-dev sqlite3 \
    libmysqlclient-dev libpq-dev\
    libxml2-dev libxslt1-dev \
    libcurl4-openssl-dev libffi-dev \
    zlib1g-dev liblzma-dev
```

### Ruby'nin sihirli değneği - Bundler

Aslında Ruby ye yeni başladım o yüzden canınızı Bundler tarihçesini anlatmayacağım. Hadi yaşadınız. Direkt nasıl kurulacağını göstereceğim yani

Birde şuraya nokogiri yi ekliyim.

```shell
gem install bundler nokogiri
```

## Docker'ı seviyoruz, o da bizi

Docker'ı cidden çok seviyorum. Böylesine güzel hayatı kolaylaştıran tool görmedim. Benim gibi dev envini, infrastructure çöplüğü yapmak istemeyen, yeni teknolojileri deneme delisi (bknz. yazar) iseniniz şiddet ile öneriyorum. Yanında bir Compose aldınız mı tadında da yenmez ama ben burada Compose u gösterme niyetli değilim. Bildiğiniz dümdüz container run edicem.

Ama önce ubuntu ya nasıl kuruluru gösteriyim izniniz ile.

### Docker'ı Ubuntu ya kuralım

```shell
sudo apt install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88 # Kontrol edebilirsiniz bu command ile fingerprint i
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable" # Düşüncem o durki bilgisayarınızın architecture u classic x86, eğer
   # daha çılgınca architecturelar kullanıyorsanız lütfen sizi offical documentation
   # a davet ediyim. Burada da [link](https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository)i
sudo apt update && sudo apt install -y docker-ce
```

Şimdi sihir zamanı. Nasıl mı?

### Hadi architecture u ayağa kaldıralım

Öyle H tagine bakarak böyle büyük şeyler olucağını düşünmeyin. Aslında küçük olaylar sonrasında büyür. Ama neyse, felsefe yapmayalım.

Ben burada PostgreSQL, Redis, Elasticsearch indiricem. Özellikle Alpine sürümlerini kullanıyorum çünkü herhangi bir işlem yapmayacağım containerlar üzerinden.

Çünkü, DB containerı sadece DB görevini alır der [12 factor kuralı](https://12factor.net/). Bu yüzden ellemeye gerek yok olması gibi ihtiyacımda yok. Çok güzel çalışıyorlar.

Hadi biraz servis ayağa kaldıralım

```shell
docker run --name=my_project-postgres --env POSTGRES_USER=LoremIpsum --env POSTGRES_PASSWORD=L0reM<ipsuM --env POSTGRES_DB=my_project_development \
    -d -p 5432:5432 postgres:alpine
docker run --name=my_project-redis -d -p 6379:6379 redis:alpine
docker run --name=my_project-elasticsearch -d -p 9200:9200 -p 9300:9300 elasticsearch:alpine
```

Bu kadar. Koskoaca 3 tane servisi internet hiziniza bağlı olarak çok hızlı bir şekilde kurduk ve hazır çalışıyorlar. Nasıl mı öğreneceksiniz. `docker ps` bununu için var.

> Hatirlatma, eğer Docker'ı benim gibi non-root user üzerinden kurdu iseniz aklında bulunsun, Docker root user'ı ile çalışır. bu yüzden üstteki kodları eğer run edemediyseniz hata aldıysanız bir de `sudo` ile çalıştırın.

## Son söz

Bu kadar kısa olabileceğini düşünüyorsanız ~~yanılıyorsunuz~~ haklısınız. Bitti işte. Koskoca bir dev-env kurdunuz. Şimdi yapmanız gereken hemecik bir Rails indirmek, sinatra indirmek...

Docker ile hayat kolaylaşıyor ve bilgsayarınızda gereksiz conf dosyalarını barındırmaktan uzak duruyorsunuz. Aynı zamanda sanki gerçek bir prod-env kullanıyormuş gibi de Compose yazabilirsiniz.

Ama sonraki yazımda Docker hakkında birkaç birşey anlatmak isterim. Belki süpriz yapar video çekerim.

Konu hakkında sorularınız varsa bekliyorum alttarafta disqusalım.
