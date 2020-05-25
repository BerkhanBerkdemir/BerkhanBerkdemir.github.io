---
layout: post
title: How to NOT install NVIDIA driver in Linux
image: /public/images/2019/7/1-christian-wiediger-3GUW88tRmv8-unsplash.jpg
date: 2019-07-24 16:35 -0700
---

> In this post, you'll not find a script that **magically** installs NVIDIA
> driver; however, that will help you to understand what is going behind the
> close-source driver. Also, I am not the developer but SysAdmin who closely
> works with Linux systems.

We decided to use NVIDIA graphic cards to train deep learning models because
AWS uses NVIDIA cards in p2 and p3 instances and our software was
written in CUDA. So, obviously, we have to use a NVIDIA graphic card.

I know installing NVIDIA graphic card driver is a *mess* in Linux, but should
NOT hard to install in +6 hours.

## Understand the requirements and read the documentation before the action

NVIDIA says:

> Installation instructions: Once you have downloaded the driver, change to the
> directory containing the driver package and install the driver by running, as
> root, `sh ./NVIDIA-Linux-x86_64-430.34.run`
>
> One of the last installation steps will offer to update your X configuration
> file. Either accept that offer, edit your X configuration file manually so
> that the NVIDIA X driver will be used, or run `nvidia-xconfig`
>
> &mdash; nvidia.com [July 24, 2019][1]

What I did I jumped into the [`README`][2] file because I'm SysAdmin. I can read
a Tolstoy in a minute, but that wasn't the case. It was the worst experience
I've ever done because I had no idea where to start and titles don't point out
the action you want.

I already know that we are using Linux Kernel 4.18.0, GCC 7.4.0 and X.Org server
1.19.6. There is no additional dependencies we downloaded after the Linux setup.
Also, I know that we have a card which is NVIDIA GeForce 900 series.

The documentation doesn't state anything about hard-requirements, so I tough we
would be fine with default settings. Nevertheless, that didn't work very well.

## Unix/Linux does NOT like reboot

Yes, these systems are not like *winfos*, and they do not like reboot. Despite,
NVIDIA installer loads some modules to the Linux Kernel. So, you **must** reboot
the system, then, you can see the result.

Also, the installer uses [DKMS][3], and we used it as well because if you don't
use DKMS, you would want to `CTRL + C` the installer, really.

## Do NOT say yes to strangers

As a SysAdmin, I have to know every single dependency I download to the system
&mdash; that's why I'm getting paid. In this case, I have no clue what NVIDIA
does

```
An incomplete installation of libglvnd was found. All of the essential
libglvnd libraries are present, but on or more optional components are missing.
Do you want to install a full copy of libglvnd? This will overwrite
any existing libglvnd libraries.
```

That is an example of *friendly remainder*, and I love and appreciate whom does
that. So, I said **Install and overwrite** instead of **Don't install**.
However, I had to delete the system completely and reinstall again and said
**Don't install**. Now, I have no problem, *for now*.

## They don't care the user, but community cares

I hate to be a search-engine-admin, but I had to turn to the search engine to
find the main issue and there is **NO single answer** for it. My friend and I
started to try every single answer we see because we have no clue even worse I
have no clue.

## Conclusion

NVIDIA doesn't care about the open-source community, their users and SysAdmins.
Due to the lack of UX and meaningful errors make hard to understand installer
needs; therefore, we had to delete the system 3 times and install a few times
the installer. I hope they can solve the problem with **money** they earn from
high-end, expensive, *insufficient* documented cards.

[1]: https://www.nvidia.com/Download/driverResults.aspx/148589/en-us
[2]: http://us.download.nvidia.com/XFree86/Linux-x86_64/430.34/README/index.html
[3]: https://en.wikipedia.org/wiki/Dynamic_Kernel_Module_Support
