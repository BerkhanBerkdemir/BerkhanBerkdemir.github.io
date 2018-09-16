---
layout: post
title: Remove Hostname From Terminal
image: /images/2018/09/4-after-hostname-edit.png
#date: 2018-09-06 08:45 -0700
#categories: [microservices]
tags: Ubuntu
---

Developers use terminal all the time because it is effective than graphical
user interfaces (GUI). Therefore, I spend my time on my lovely terminal, but
the problem is length of hostname. I use default size which is 80x24.
`berkhans-thinkpad-t460` has 22 characters... Now, you can imagine that is why
important for me.

[
![Before hostname change](/images/2018/09/3-before-hostname-edit.png)
](/images/2018/09/3-before-hostname-edit.png)

I will just share simple snippet that will help you to remove that hostname
part.

```bash
if [ "$color_prompt" = yes ]; then
    PS1='\[\033[01;32m\]\u\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='\u:\w\$ '
fi
```

All you need to do that add this snippet before
`unset color_prompt force_color_prompt`.

After you restart your terminal, you will have this

[
![After hostname change](/images/2018/09/4-after-hostname-edit.png)
](/images/2018/09/4-after-hostname-edit.png)
