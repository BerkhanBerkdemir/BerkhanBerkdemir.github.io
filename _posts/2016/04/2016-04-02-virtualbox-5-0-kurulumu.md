---
title: VirtualBox 5.0 kurulumu
date: 2016-04-02 TRT
layout: post
---

Merhaba arkadaşlar,

Bügün Oracle şirketine ait sanallaştırma yazılımı VirtualBox'dan bahsedeceğim.
Oracle bilirsiniz ki linux alt yapısı ile çalışan -büyük bir kısmı- genelde ücretli ürünleri olan desteği redhat veya ibm gibi gelişmiş, alt yapısına (sistemlerinin alt yapısı) güvenen Amerika menşeli bir şirkettir.

Oracle'ın biz VirtualBox yazılımından bahsedeceğiz. VirtualBox öyle Xen veya vSphere ESXi gibi "Bare Metal Hypervisor" değildir. Kendisi bir işletim sistemi üzerinde barındırılarak (Örneğin Windows 7, Ubuntu 14.04, CentOS 7 vb.) yeni "Guest Host" lar oluşturuyorsunuz. VirtualBox kurumsal anlamda kullanıldığını görmedim ki tavsiye de etmem. VirtualBox bir de php dili ile web sunucundan web panel kurabiliyorsunuz. Ben burada GUI arayüz ile Windows da kuracağım. Sonrasında Fedora veya OpenSuSE üzerinden web ui olarak kurarım.
Şimdi bize gerekli olan malzemeleri önce hazırlayalım.

* İntel'de VT-x, AMD'de AMD-V sanallaştırma özellikleri
* En az dual core 2GHz üstü tavsiye ederim
* 2 GB üstü RAM
* Bir tane linux, windows, unix veya başka işletim sistemi iso, img dosyası

Ama ben Pentium 4 530 hatta Pentium 4 2.8GHz -northwood- ile de kullandım ama hiç verimli değil. Zorunda olmadıkça kullanmanızı da önermem.

Şimdi malzemeler hazır ise başlayabiliriz. Ben MS Windows 7 Starter -32bit- de yapacağım. (işlemcim Atom N455 ve VT-x desteklemiyor)

Ben size [link](https://www.virtualbox.org/)'i vereyim de. Bu satırları yazarken virtualbox sitesinden yeniden yapım çalışmaları var. O yüzden sizi Oracle'ın FTP sunucusuna yönlendirecekler -Ardından "Download Server" linkine basın-. Buradan en son sürüm olan -bu satırlar yazılırken sürüm 5.0.16- indireceksiniz. Aynı zamanda yanında Vbox Extension indirirseniz VirtualBox ürününe ekstra özellikler eklersiniz (HDD şifreleme, uzak masaüstü vb.). Toplam 120MB lık bir kurulum dosyanız olacak.

Şimdi kuruluma gelelim. Standart windows mantığında "next > next > next" yaparak da geçebilirsiniz ama kurulumu sindirerek kurmanınızı öneririm. Nelere "next" dediğinizi en azından bilmeniz ileride gerekebilir.

Şimdi fotoğraflar ile anlatacağımdan biraz rahatım :)

## VirtualBox'u için başlıyalım dansa

![](2016/04/linux_kafasi_001.png)

Gerekli olan dosyaları hazır edelim ve öncelikle VBox'un kurulumuna başlayalım

![](2016/04/linux_kafasi_002.png)
![](2016/04/linux_kafasi_003.png)

Aynı benim gibi yaparsanız (yani bütün sürücüleri kurarsanız) iyi yaparsınız. Çünkü bir kurulumda eğer "tüh be keşke local network için host-only kursaydım" dememek için.

![](2016/04/linux_kafasi_004.png)

Burası size kalmış. Ben rahat görmek için ilk ikisini seçiyorum. Register file associantions kesinlikle kurulu olsun.

![](2016/04/linux_kafasi_005.png)

Network driver'larını kuracağından bağlantı kopabilir uyarısını veriyor. O yüzden sunucu'ya kuracaksanız (-ki niye kurasanız hyper-v ne güne var) mutlaka kullanıcıları uyarın.

![](2016/04/linux_kafasi_006.png)

Kuruluma başlıyoruz artık. Install dediğinizde bağlantıda kopmalar meydana gelebilir. Bu sırada mutlaka bilgisayar başında olun çünkü -windows için diyorum :)- vac uyarısı gelecek. İzin vermeniz lazım. Aksi takdirde kurulum olmaz. Peki VAC ile mi kalıyor. Hayır ayrıca driver'ları kurmanız için de izin isteyecek. Siz ama Oracle kaynaklı uygualamara izin ver derseniz sıkıntı olmaz -kurulum sırasında göreceksiniz-.

![](2016/04/linux_kafasi_007.png)

Kurulumu başlattık ve,

![](2016/04/linux_kafasi_008.png)

Devam ederken,

![](2016/04/linux_kafasi_009.png)

Bitti bu kısım. Benim size nacizane önerim bir yeniden başlatın sistemi. Sistemi biraz rahatlatın :)

## Tiny Core Linux kurulumu

![](2016/04/linux_kafasi_010.png)

VBox'ın arayüzü bu kadar sade. Ama bir o kadar da kullanışlı işte. Basit bir "lab" kurulumu için çok bile.

![](2016/04/linux_kafasi_011.png)

Şimdi ben Tiny Core Plus kurulumu yapacağım VBox'ın üzerine. Elimde ki TC versiyonu 4.2.9 kernel'i üzerine inşa edilmiş. O yüzden ben linux'un altından 4.x.x (32bit) seçiyorum.

![](2016/04/linux_kafasi_012.png)

RAM ataması yaparken dinamik ram olarak hesaplanacak. o yüzden öyle uçuk ramler atamanızı önermiyorum. TC için 64-128MB ram yeterli -hatta fazla- ama siz başka rakamlar atayabilirsiniz.

![](2016/04/linux_kafasi_013.png)

vHDD'yi nereden alacağını belirtin. Hazır bir vHDD'niz de olabilir veya sonradan hazırlamak istersiniz. Benim hazırlmam gerek.

![](2016/04/linux_kafasi_014.png)

Size önerim VDI biçiminde yapın. VirtualBox'un orjinal vHDD uzantısıdır. VDMK vSphere ESX için, VHD Hyper-V için gibi gibi. Sizin burada yapacağınız bu diski sonradan başka bir sistem de kullanacak mısınız bu soruya cevap verip burayı işaretleyin -ekstradan şunu da yazmam gerek convert edebilirsiniz ama benim size önerim convertten önce buna hazır olmanız bir sıkıntı olursa ne olacak mesala?-

![](2016/04/linux_kafasi_015.png)

Değişken boyut -dynamic, dinamik- örneğin 30Gb vHDD ayarladınız, işletim sistemini kurdunuz ve toplam işletim sistemi boyutu 3GB. Siz eğer vHDD yi yerinden oynatacaksınız mutlaka dinamik yapın. Yok sabit kalacak ama performans olsun derseniz -forumlarda geçen laf bu yoksa ben performansını halen göremedim- Statik yapın.

![](2016/04/linux_kafasi_016.png)

Boyut size kalmış.

NOT: Statik olarak ayarladıysanız ve vHDD boyutunu çok yüksek bir rakam yaptıysanız (örneğin 300GB) 10GB başına 1-2 dakika kurulum için bekleyeceksiniz ve o zaman kadar HDD kullanımı %100 olacaktır. O yüzden bu işlemi yaparken bilgisayarınızı veya sunucunuzu düşünerek yapın.

![](2016/04/linux_kafasi_017.png)

Tabi ki ben 512MB olarak statik bir şekilde ayarladım o yüzden çok hızlı bir şekilde bitti :)

![](2016/04/linux_kafasi_018.png)

Şimdi buraya kadar basitti değil mi? Tabi ki. Ama 3. Bölüm daha basit.

## Küçük dokunuşlar

Şimdi VM'e/lere optimizasyon yapacağız. Ama önce ayarlar kısmına girin

![](2016/04/linux_kafasi_019.png)

Ardından Sistem kısmından Disketi kapatın (disket kurulumu yapmayacağız ama gerekli ise açık kalsın.

![](2016/04/linux_kafasi_020.png)

Ve 3 geri alalım ki CD ve HDD den önce okunmasın.

![](2016/04/linux_kafasi_021.png)

CD nizin iso veya img formatını buraya tanıtın aynen;

![](2016/04/linux_kafasi_022.png)

böyle yapın sonra "aç" derseniz cd aynı gerçekte dvd okuyucuya takmış gibi olacaksınız :)

![](2016/04/linux_kafasi_023.png)

Şimdi "ağ" kısmına gelin ve oradan hangi (sizde köprü bağdaştırıcı farklı gözükebilir ben wifi kullanıyorum şu an için) köprü bağdaştırcağınızı seçin. En altta da hangi driver'ı tanıtsın guest os'a diye de (yani ethernet kartını) gösteriyor ben genelde İntel mt sunucu yaparım ama siz de farklıları deneyebilirsiniz.

![](2016/04/linux_kafasi_024.png)

buna benzeyecek arayüzünüz. (benzemesi zorunda değil ayrıca belirtiyim)

## Tiny Core Linux kullanımı

![](2016/04/linux_kafasi_027.png)

Aynen böyle başlayacaktır.

NOT: Ben TC Plus kullanıyorum siz illa bunu kullanacaksınız diye bir şey yok. Ubuntu'da kurabilirsiniz Fedora'da, Server 2012R2'de.

![](2016/04/linux_kafasi_028.png)

Ve live cd başlatılıyor. Bu siyah ekran dan sonra size GUI hazırlanacak ve orada isterseniz vHDD'ye cidden kurabilirsiniz isterseniz livecd olarak kalabilir.

## vbox extension kurulumu -OPSIYONEL-

![](2016/04/linux_kafasi_029.png)

En başta da belirtiğim gibi vbox extension opsiyonel bir seçenektir. Ama benim size önerim kurun. Belki gerekebilir ilerde. Önce Terchiler'e girin

![](2016/04/linux_kafasi_030.png)

Uzantılar kısmına girin yanda ki küçük sarı (tanımlayamıyorum) cisimciğe basın :)

NOT: Vbox extension ayrıca yüklü olması gerek sonra ben bunu nereden bulacağım demeyin :)

![](2016/04/linux_kafasi_031.png)

Seçin ve "aç" 'a tıklayın. Ardında size,

![](2016/04/linux_kafasi_032.png)

bu paketin içinde neler olduğunu gösteren bir diyalog çıkar. Burada "yükle" derseniz size,

![](2016/04/linux_kafasi_033.png)

lisans sözleşmesini gösterir. Burada en aşağıya kadar gelip "KABUL EDİYORUM" seçeneği aktif hale gelir ve,

![](2016/04/linux_kafasi_034.png)

kurulum başlar.

![](2016/04/linux_kafasi_035.png)

Kurulum bittiğinde size haber verir bu sırada VAC gibi gerekli işlerm olmaz.

![](2016/04/linux_kafasi_036.png)

ve başarılı olduğunu yanında ki tik den anlayabilirsiniz.

Aslında her bilgisayar kurdu için gerekli bir ürün. Her gün normal hardiskinize yapacağınız soft formattansa buradan yani sanal ortam da gayet başarılı işler çıkarabilirsiniz.
