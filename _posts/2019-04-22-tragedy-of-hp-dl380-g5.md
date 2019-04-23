---
layout: post
title: Tragedy of HP ProLiant DL380 G5
date: 2019-04-22 15:32 -0700
---

We bought second-hand DL380 G5 to run our master Citrix XenServer, and it works
without any problem. Except latest version of firmware updates...

> Tragedy (from the Greek: τραγῳδία, tragōidia) is a form of drama based on
> human suffering that invokes an accompanying catharsis or pleasure in
> audiences.
>
> Tragedy, https://en.wikipedia.org/w/index.php?title=Tragedy&oldid=893388704
> (last visited Apr. 22, 2019).

I am 20 years old and not a senior system administrator which we can say that
due to lack of experience. This is third time to work with a bare-metal system.
Moreover, my father and I did not work with HP before; however, we decided to
buy a HP server. It came with Intel Xeon E5405, 32GB DDR2 RAM and 6 146GB 10K
SAS. That is awesome since the hardware works with no error, and we started to
work with.

1 day after the purchase, I wanted to update all firmwares. I started with the
easy one: iLO. Upload the image to iLO and you are ready to go. It will restart
itself a few times and you can work with after that moment.

The second move was safely updating the BIOS. The latest version of the BIOS
published at September 30, 2015. **But**, we cannot access the latest one
because Hewlett Packard Enterprise changes their downloadable firmware policy.

> This went into effect today (February 1, 2014). Neither HP nor our HP reseller
> notified us of this change. So if you have some out-of-warranty server-related
> equipment that you want to keep up to date, you're out of luck unless you pay
> up.
>
> &mdash; CannonBall7 [February 1, 2014][hp-blocks-fw-updates-without-warranty]

Well, I bought this server in December 2018, and I **was thinking** that the
vendor does not block the firmware from their costumers, but they do.

I can access any firmware which published before February 1, 2014.

---

*P.S. If I update the BIOS, I'll add a guide in here. So, subscribe with RSS*

[hp-blocks-fw-updates-without-warranty]: https://www.reddit.com/r/sysadmin/comments/1wrake/hp_now_blocks_firmware_updates_for_products/
