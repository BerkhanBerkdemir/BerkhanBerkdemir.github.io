---
layout: post
title: How to Update ThinkPad T460's BIOS on any Linux OS
description: >-
  Update ThinkPad T460's on Ubuntu 18.04, or any type of Linux distro that can
  run some Perl script
date: 2019-03-19 17:32 -0700
updated: 2019-04-23 15:24 -0700
---

## TL;DR

I contacted with Lenovo support over *Twitter*, and they told me that there is
no way to update ~~Lenovo~~ ThinkPad T460's BIOS. So, here is a guide that you
can update the BIOS &mdash; but with a disclaimer; **please make sure that you
know what you are doing** because **you can do something wrong**. Also, I use
Ubuntu 18.04, and the BIOS version was 1.10 which was released March 23, 2016.

![Output of dmidecode](/public/images/2019/3/2-screenshot-from-2018-10-02-18-16-26.png "Output of dmidecode")
*The screenshot was taken on 2 October, 2018*

## Required tools and steps to apply the update

I got an USB driver, and wiped it to make it ready the drive. At the same time,
I downloaded [the update][bios-update], BIOS, from ~~Lenovo~~'s support. Also,
wanted to read the `README.txt` because they can add important information for
the hardware owners.

Next step is that downloading some utilities to work with that `r06uj66d.iso`
since we won't able to flash that ISO into the USB drive.

> Psst. I think you don't run Ubuntu. That's why you consider some other options
> to use that tool. Here is [the source code][geteltorito]

```bash
sudo apt install -y genisoimage
```

> As a sysadmin advice, keep the ISO image on your archive. You may need it for
> latter. Trust me.

Convert the ISO (CD image) to IMG (aka. floppy disk format)

```bash
geteltorito -o bios.img r06uj66d.iso
```

Flash the USB. If you don't know how to find your USB's device path, please
search it.

```bash
sudo dd if=bios.img of=/dev/sdb
```

So, yeah. We have some todos like applying the update. Don't unplug the USB, and
safely reboot the system. When you see the vendor logo, press F12 then choose
the USB driver to boot.

Now, you can see some weird things, so no worry. It'll be so easy, and it takes
only less than 10 minutes; therefore, please follow each instructions.

When pops up the BIOS update, go "system update", and like we said earlier,
follow **each instructions**. The system will reboot *itself* a few times.

## The result

So, I updated to 1.40 from 1.10 :tada:

![the output of dmidecode with the 1.40 BIOS](/public/images/2019/3/3-screenshot-from-2019-03-19-16-56-30.png "the output of dmidecode with the 1.40 BIOS")

## Thanks

I need to thank for this two [awesome][cyberloginit] [articles][workaround]!

[geteltorito]: https://userpages.uni-koblenz.de/~krienke/ftp/noarch/geteltorito/
[bios-update]: https://support.lenovo.com/us/en/downloads/ds112123
[cyberloginit]: https://cyberloginit.com/2017/10/14/update-thinkpad-bios-with-usb-drive.html
[workaround]: https://workaround.org/article/updating-the-bios-on-lenovo-laptops-from-linux-using-a-usb-flash-stick/
