---
layout: post
title: Sorry, but I won't run Ubuntu anymore
date: 2019-03-04 17:53 -0800
---

I'm not hacked or nobody holds a gun to my head. I, literally, do not want to
run Ubuntu anymore. Well, I have reasons for that; however, you can learn more
about **detailed why** with [this YouTube link](https://youtu.be/Xy7v5tdfSZM).

> When I started to think about my problem, I saw that I'm not the only one
> having the same problem, in that YouTube video.

## Background

When I was 8 years old, I saw [BackTrack Linux][backtrack-linux] on my dad's
IBM ThinkPad R51, and it was running with a CD. That was cool because I had
Windows XP, and it needs to boot the system for ten minutes or so. But the
coolest thing is that that CD just boots the system in 1-2 minutes. That was the
first time I saw Linux. Another important mention is that graphical user
interface. That wasn't just like Windows, it was different than others because
of that it felt me special.

In 2014-2015, my dad invited to me to Dell Sonicwall firewall showcase &mdash; I
was using Windows system BTW. I had heard firewall systems use Linux, but I had
no idea about **why**? If we look at my age, 15, it is just normal for me to
don't understand anything about Linux because at that time, I don't have any
background of how computer works. So, I didn't find the answer of *why*?

> Many of my friends know that I'm fan of IBM servers because I grew up with one
> of them: IBM eServer xSeries 205 aka. x205
>
> That was not the perfect server that I've ever met, but that was an awesome
> experience for 15 years old child.

After that day I checkout what is a firewall, or how they work, and finally
I found a distro on [DistroWatch][distrowatch] which is named **IPCop**.

> There is no link for IPCop because it's been discontinued project. I'll give
> newer versions (forked) of IPCop later on. Just keep going to read.
>
> Oh, I found their *old* [SourceForge](https://sourceforge.net/projects/ipcop)
> site.

I downloaded an ISO image and burned a CD. I had no idea about virtualization or
any other fancy technologies that I can easily spin up an instance of IPCop. So,
I got the CD, and ran on my x205. Then, I saw the splash screen[^1]. That
was not the most beautiful thing, but yeah, you know.

![I was like that](https://media.giphy.com/media/SjuHQhR9RTdzq/giphy.gif)

I set a Linux firewall ~~with my 15 years old experience~~. Well, we didn't run
in the production, but that was unbelievably beautiful experience for me.

## Finding Distributions and Trying Them in VirtualBox

When I was looking for firewall Linux *operating systems*, I didn't know that
was called a **distribution**, I found a few distributions like Fedora, CentOS,
OpenSuSE[^2] and Ubuntu. I downloaded them, I ran all of them on
[VirtualBox][virtualbox], I think that was 4.3 something, on my Pentium 4 HT
@ 3.00GHz, 2GB RAM Windows XP computer.

I didn't do anything fancy. I ran them, and I played with them for a while
inside of their virtual machines. All of them running as smooth as a baby's
bottom, but something that I find in Ubuntu was different. I was like hooked on
that, and I decided to **nuke** Windows XP, and run Ubuntu 14.04.

![](https://media.giphy.com/media/cRBRQf8syLUyY/giphy.gif)

But, I didn't because my MOBO[^3] doesn't support USB boot, so I need to burn
a CD-R to install Ubuntu 14.04, or even worse, put Ubuntu in floppy drivers
:fearful:

I burned a CD-R to install, and every single my setup was crashed. So, I didn't
set up a U14.04, and I burned 10-15 CD-R &mdash; I think my DVD reader wasn't
OK, but anyway.

So, I moved back, and installed Ubuntu 12.04 without any error. I used for 1
month without any problem, but I had to move back to Windows because of my
brother :triumph:

I didn't do anything unusual like compiling a Kernel, writing a program. I did
what I do in Windows XP except playing video games. After that moment, I always
had VirtualBox installed.

## Moving to The US

Moved to US in August 2017 for Santa Monica College to transfer to University of
California, Los Angeles or University of California, Berkeley, which are top
universities for computer science. I have to have a notebook because I don't
have one, so I got the notebook: ThinkPad T430. It is heavy because of its
9-cell battery, very thick case and old Intel 3rd Generation I5, but I prefer
ThinkPad over any of brands because I know how to fix, I know how to upgrade
&mdash; thanks to R51.

Day one, I installed Windows 7 since it has a key, and also, I use **stable**
software over cutting edge one. After 3 months, I was still using Windows 7, and
I suddenly changed the OS to Ubuntu 16.04 in November.

That was perfect OS because I write PHP (Symfony), use MySQL and I do some
remote SysAdmin stuffs. With that, I learned many things with Linux operating
system. I started learning shortcuts of Unity[^4] desktop environment. Actually,
I didn't learn them. When I press long the supper button, aka. Windows logo,
I can see the all shortcuts.

Then I started to learn Docker *natively*, Kubernetes, cloud computing with
changing an operating system completely. I think there was a magic that I didn't
see before. That is the reason I fell in love with Ubuntu because I'm learning
new technologies with it.

## Ubuntu 18.04 and Before & After

I was so exited about Ubuntu 18.04 because first time I was curious about an
new release of operating system before that I wanted to install Ubuntu 17.10,
but that was.. that was.., sorry but, that sucks! I didn't even run my
development environment without any error.

> I deleted my Twitter account in August 2018, but I saw that it wasn't deleted.
> Tweets are shared from my archive.

> @ubuntu community please fix this battery bar before release 18.04. It says 10
> hour for full charge from %96...
>
> &mdash; Berkhan Berkdemir April 13, 2018

or

> @ubuntu @gnome I found that bug in 17.10 #ubuntu #gnome #bug #nautilus
> ![Nautilus bug on Ubuntu 17.10](/images/2019/3/1-nautilus-bug-on-ubuntu-17-10.jpg)
>
> &mdash; Berkhan Berkdemir May 15, 2018

OK. it is my bad also because I didn't report their issue board. I just post
a tweet. Anyway, I installed Ubuntu 18.04.

Well, did I see something fancy? Yeah, they dropped the support of **their**
Unity and support Gnome, started to force user to install snap packages because
in the Gnome app store you make an effort to find non-snap application. For
example, I used to have Spotify, and I didn't download Snap application and I
downloaded Spotify via APT tool.

I lost my feelings about Ubuntu after that moment because they started to have
different vision. They don't have the same passion when I using. They are
started to force user to a packing system with a few reason.

## Ubuntu 19.04...

This is the first time that they didn't release an *alpha* release to test
Ubuntu. Why? Why did you not release an *alpha* release? What are you hiding?
Why are you removed some of cool features, such as GSconnect, from U19.04?

They'll release an beta release 21 days before the final release. Well, it is
not a LTS[^5], but it the only reason that I lost my passion for Ubuntu. There
is **no fancy** things going on anymore.

## The Last Words

I learned many things about Linux with Ubuntu, and I need to say thank you.
But I need to use something stable because I want a system that
Just Works&trade;.

So, I'll move to Red Hat Enterprise Linux, developer edition, CentOS or
OpenSuSE. Yeah, I know that moving from cutting-edge solutions to enterprise
Linux system will be hard, but I don't want to see Snap application or
no-new-feature releases when you have tons of.

---

[backtrack-linux]: https://www.backtrack-linux.org
[distrowatch]: https://distrowatch.com
[virtualbox]: https://www.virtualbox.org

[^1]: Splash screen: An introduction page of BIOS, program or an operating
      system

[^2]: If your background comes from old days (or with somebody's experience),
      you could say SuSE because the name of distribution was that. However, you
      won't be wrong if you call them SUSE. Also, SuSE stands for *Software und
      System-Entwicklung*, Software and System Development

[^3]: Motherboard

[^4]: An user interface what makes Ubuntu, Ubuntu

[^5]: Long-Term Support
