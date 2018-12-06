---
layout: post
title: Open an email client when Ubuntu starts
image: /images/2018/09/5-Screenshot from 2018-09-28 22-55-18.png
date: 2018-09-28 23:36 -0700

tags: Ubuntu
---

This is an old habit from Microsoft Office Outlook which sets as startup
application by default. It is very handy if you don't have regular time for
reading email. However, Mozilla Thunderbird doesn't come with same solution.

![Search result of "Startup Applicat" on Ubuntu 18.04](/images/2018/09/5-Screenshot from 2018-09-28 22-55-18.png)

In this tip, I will use *Startup Apllications Preferences* which is GUI for
startup programs on Ubuntu. When you download for full version of Ubuntu 18.04,
it comes by default. However, I'm not sure about minimal installation.

> Pictures say a lot.

## Add startup program

![](/images/2018/09/6-Screenshot from 2018-09-28 23-22-54.png)

Click *Add*, and you will see a window that has *Name*, *Command* and *Comment*
inputs. You need to fill name and command, but you don't need to worry about
comment.

| Attribute | Value                              |
| --------- | ---------------------------------- |
| Name      | Mozilla Thunderbird - Email client |
| Command   | `thunderbird %F`                   |

When you save, you will see the record which it will be like this

![](/images/2018/09/7-Screenshot from 2018-09-28 23-23-15.png)

Your Thunderbird is ready to go. All you need to is log out and log in. After
that, you will see the email client.
