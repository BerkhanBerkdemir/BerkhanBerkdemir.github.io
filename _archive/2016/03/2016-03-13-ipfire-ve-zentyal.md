---
title: IPFire ve Zentyal
date: 2016-03-13 TRT
layout: post
---

Merhaba arkadaşlar,

Ben aslında makale yazmayı tercih edeceğim bu konu hakkında. Aslında iki distro da farklı. Biri Firewall, diğeri sbs. Aslında bu iki distro bir şirkette kullanıldığında 1000-2000 $ lık lisanlardan kurtulmuş oluyorsunuz. Linux zaten bunun için var diyebilirim.

İlk önce IPFire ile başlayayım. IPFire adından da anlaşılacağı gibi firewall yazılımı. İlk adı IPCop du. Aslında ikisi arasında en büyük farklardan biri web arayüz değişikliği. Ben IPFire ı eğer çok özel bir kurum değilseniz evinizde bile rahatlıkla kullanabileceğiniz bir yazılım. Aşırı basit kurulum ve yönetimi var. Aynı zamanda pakfire yönetimi sayesinde güncel kalmış oluyorsunuz. Bunun yanında Pakfire ile örneğin bir apache web sunucusu kurabiliyorsunuz. Yani sadece firewall olarak kullanmak zorunda değilsiniz. IPFire herşeyi ile ücretsiz olması aslında linux'cuların hoşuna giden birşey. Tek sıkıntısı 64 Bit sürümü bulunmuyor. Sadece ARM ve 32 Bit sürümü var. Herhangi bir donanım kısıtlaması bulumuyor herzaman ki gibi. IPFire 'a alternatif olarak Endian Firewall (EFW) veya pfSense olabilir. Endian belli bir yere kadar ücretsiz. Sonrasında paralı uygulamalar var. Onlarıda ödemek zorunda kalıyorsunuz. IPFire gibi bir tek ürün bence pfSense var. Onda daha fazla özellik var ama kullanımı biraz karışık.

Zentyal ise Small Business Server alternatifi bir sistem. Ubuntu üzerine kurulu, web arayüz yönetimli bir sistem. Bunun yanında MS SBS de ki gibi bunda da küçük işletmeler için en gerekli paketler var. Bu paketler arasında en sevdiğim basit bir firewall ve exchange mail hizmet protokolü. Tabiki MS Exchange bir tutmaz ama alternatifi olarak işinizi göreceğine inanıyorum. Samba ile printer server veya file server olarak da kullanabilirsiniz. LDAP, MS AD alternatifidir (kısaca telefon rehberi :)). Mail server için spam ve antivirus (spam assasin ve clamav). Webmail özelliği ile illa client kullanmanıza gerek kalmayacak. Mobil versiyonunda webmail biraz sıkıntılı. fakat mail sunucu alternatifi olarak bence ilk sıralarda olabilir. Elbette şuan ben clearos da tavsiye ediyorum sbs için. 2-3 kurcalamdan sonra paralı bir sistem olduğunu anlmam geç oldu. O yüzden ben herşeyi ile bedava sistem istiyorum diyorsanız (aynı benim gibi) zentyal önerilerim arasında.

Zentyal ile IPFire aslında birlikte kullanıldığında gidip MS'e binlerce dolar yatıracağınza burada kendiniz bile rahatlıkla kurabilirsiniz. Linux zaten özgürlüktür denmiyor boşbouna.

[IPFire](http://www.ipfire.org) alternatif: [Endian Firewall](http://www.endian.com), [pfSense](http://www.pfsense.org), [Untangle](http://www.untangle.com)

Zentyal alternatif: [ClearOS](http://www.clearos.com), [NethServer](http://www.nethserver.org), [Univention Corporate Server (UCS)](http://www.univention.com/products/ucs/)
