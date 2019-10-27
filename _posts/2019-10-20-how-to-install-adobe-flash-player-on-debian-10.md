---
layout: post
title: How to Install Adobe Flash Player on Debian 10
date: 2019-10-20 19:45 -0700
---

I had had bad times while installing Flash Player on this beautiful Linux
distribution. I understand concern of Debian community, and I strongly agree
that close-source codes need to be away from these distributions.

If you have needed to run Adobe Flash Player on any kind of Debian distribution,
you can use this post to install Flash Player, but I want to remind you that you
should not use Adobe Flash Player after December 31, 2020 because it will
**not** get any security patches[^1].

Also, I want to remind you that I am using Firefox ESR version 60.9.0 while
writing this post.

> Firefox 68 ESR released, and this post can still be applied for it

## Installation of Adobe Flash Player

> Before get started, `cd(1)` to either `/tmp` or some type of temporary
> directory. In this post, I use `/tmp`.

We need to download Flash Player from its source. The downloaded file is a
gziped tarball

```bash
wget https://fpdownload.adobe.com/get/flashplayer/pdc/32.0.0.270/flash_player_npapi_linux.x86_64.tar.gz
```

Now, we need to extract with `tar(1)`

```bash
tar -xf flash_player_npapi_linux.x86_64.tar.gz libflashplayer.so
```

Create a directory to place `libflashplayer.so`  file. I will `mkdir` the
directory under `/usr/lib` as `flashplugin-nonfree`. This is because I want to
easily update without messing with system libraries. Also, I can place a
`README` about procedures I need to take in order to update Flash Player
version

```bash
mkdir /usr/lib/flashplugin-nonfree
```

We can `mv(1)` `libflashplayer.so` under `/usr/lib/flashplugin-nonfree`
directory. Also, I would remind you that do not forget change owner and file
permisions

```bash
mv libflashplayer.so /usr/lib/flashplugin-nonfree

chmod 644 /usr/lib/flashplugin-nonfree/libflashplayer.so
chown root:root /usr/lib/flashplugin-nonfree/libflashplayer.so
```

Here is the interesting part because I had not used `update-alternatives(1)`
before, and when I used in this installation, I found its magic. I always use
`ln(1)` to create symlinks, but `update-alternatives(1)` provides an "User
Interface" to control, create and manage symlinks

```bash
update-alternatives --quiet --install \
   /usr/lib/mozilla/plugins/flash-mozilla.so \
   flash-mozilla.so \
   /usr/lib/flashplugin-nonfree/libflashplayer.so 50
```

You can list symlinks that are created by `update-alternatives(1)` with
`--list` flag

```bash
update-alternatives --list flash-mozilla.so
```

Now, all you need is to restart your Firefox and you **should** see the changes
immediately. If not, restart the system. Otherwise, I don't know; *it worked on
my machine*.

## Conclusion

If you have a situation like mine, having Flash Player just for an old system,
you will likely install it with **pain**, but this post may help you in this
road. I would thank for Patrick[^2] and Greg[^3] for their explanation.

[^1]: https://helpx.adobe.com/shockwave/shockwave-end-of-life-faq.html
[^2]: https://unix.stackexchange.com/a/388266
[^3]: https://lists.debian.org/debian-user/2019/10/msg00837.html
