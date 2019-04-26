---
title: Automated CentOS Installation with Kickstart
date: 2018-01-12
updated: 2017-03-25
layout: post
tags: CentOS
---
Hello guys,

Today I am gonna write about automated CentOS installation. Every single amateur sysadmin trying
these installation

> Use virtual machine. Because they have clone system. Install the system after that just
clone it. That's it.

This is not such a good idea. Why?

When you clone the whole OS, basically you have to change hostname, or static ip...

> Use container system. You can create an OS really fast way to.

Hey brother, we are talking about Operating System, not container. You have to create a Bare-Metal system for Docker or rkt.

## Solution?

### Kickstart!

What a magical word, right?

This is really magical tool, you can install 1 to 10000 server in same time without type anything. Maybe, you heard **Anaconda**. You can see this word when you install CentOS, Fedora or Red Hat.

Anyway, I want to show, how?

## Kick-Start

![](https://78.media.tumblr.com/abf002eddc7020efcebd19ff4b98955b/tumblr_nxnf12WWtx1tq4of6o1_500.gif)

First of all, I will use CentOS 7.4.1708 minimal version, but you can find this feature at Fedora or Red Hat Enterprise Linux.

### What should you do right now?

I will give you the file, you just copy it. That's it.

> This is just a boilerplate

```
# ks.cfg

#version=DEVEL

# System authorization information
auth --enableshadow --passalgo=sha512

# Use CDROM installation media
cdrom

# Use text install
text

# It is not run the Setup Agent on first boot
# I don't recommended this 'firstboot --enable'
# This one set the setting after that waiting your command for install.
#firstboot --enable
ignoredisk --only-use=sda

# Keyboard layouts
keyboard --vckeymap=us --xlayouts='us'

# System language
lang en_US.UTF-8

# Network information
network --bootproto=dhcp --device=enp0s3 --ipv6=auto --activate
network --hostname=<HOSTNAME>.example.com

# Root password
rootpw <ROOT_PASSWORD>

# System services
services --enabled="chronyd"

# System timezone
timezone America/Los_Angeles --isUtc

# System bootloader configuration
bootloader --append=" crashkernel=auto" --location=mbr --boot-drive=sda

# Partition clearing information
clearpart --none --initlabel

# Disk partitioning information
# This partitioning for 8GB Harddisk
part /boot --fstype="xfs" --ondisk=sda --size=476
part pv.198 --fstype="lvmpv" --ondisk=sda --size=7715
volgroup centos --pesize=4096 pv.198
logvol swap --fstype="swap" --size=953 --name=swap --vgname=centos
logvol / --fstype="xfs" --size=6271 --name=root --vgname=centos
logvol /home --fstype="xfs" --size=476 --name=home --vgname=centos

%packages
@^minimal
@core
chrony
kexec-tools

%end

%addon com_redhat_kdump --enable --reserve-mb='auto'

%end

%anaconda
pwpolicy root --minlen=6 --minquality=1 --notstrict --nochanges --notempty
pwpolicy user --minlen=6 --minquality=1 --notstrict --nochanges --emptyok
pwpolicy luks --minlen=6 --minquality=1 --notstrict --nochanges --notempty
%end
```

After that,

you have to upload this file (ks.cfg) to FTP, HTTP or NFS server. I will use PHP Built-in Server.

`php -S 0.0.0.0:4444 ks.cfg`

Now, PARTY TIME!!!

Insert CentOS disk to your Bare-Metal/Virtual server, don't press to *Install CentOS 7*. Just press *tab*.

![kickstart-1](https://i.imgur.com/EY2OsTo.png)

like this, after that, delete whole content and write those content to there

`vmlinuz initrd=initrd.img inst.ks=http://<IPADDR>:<PORT>/path/to/ks/file`

![pff](https://media.giphy.com/media/EOpZ7XsVfTN2E/giphy.gif)

![kickstart-2](https://i.imgur.com/HI4kZsR.png)

after that you will see this output, this means successfully will start the installation

![kickstart-3](https://i.imgur.com/eqq1WXh.png)

When done the installation, just press enter. Don't forget the remove CentOS installation CD. Reboot it. Than

![kickstart-4](https://i.imgur.com/KeLBBfT.png)

TA-DAA

![YAAAY](https://media.giphy.com/media/11sBLVxNs7v6WA/giphy.gif)

## Conclusion

Nowadays sysadmins use different automation tool but this tool can save your time. Also it is easy to use and has easy to read cfg file.
