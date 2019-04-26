---
title: Netlify vs Gitlab Pages
date: 2018-04-01
update: 2018-12-01
layout: post
---

Hello guys,

This part is part of the [next generation blogging]({% post_url 2018-04-01-next-generation-blogging-with-static-site-generators %}). I will compare 3 different system.

*Netlify* vs *Gitlab pages* vs *Gitlab pages + Cloudflare*

I sait in my previous blog about why I am using Gitlab pages for static content hosting because they are successful (not only Pages. Features, support etc.)

![Netlify vs Gitlab pages vs Gitlab pages + Cloudflare](https://i.imgur.com/UV9eVYC.png)

I just wanna share this image because it tells everything. As you can see, Netlify won. Only Gitlab pages has some problem. Missing css.

![404 main.css](https://i.imgur.com/Uk1AEbk.png)

Also it is quiet slow than others. Total pages size low because we have one missing css, that's why this is not really good comparison.

Let's look for Cloudflare. It has good load time score. 0.7s too close for Netlify and better than only Gitlab pages, but Cloudflare offers some feature, so they add some JS files (for example email protection).

## PageSpeed

![PageSpeed comparison](https://i.imgur.com/SMYUSCB.png)

Google says, those results are perfect. Yes, it is. We don't need to think about too much.

## YSlow

But, I don't know why, like Yahoo says "I won't crawl that" :smiley:. Maybe, you want to look it up, that's why, I shared with you.

## Let's move to Netlify

I am using Cloudflare as DNS and CDN solution and Gitlab as hosting service, but why I don't want to use just 1 system for everything also with new features?

I really like to use new system and feature, that's why this is test drive. Maybe, I can use for really one. If I like :grin:.

### Change your NS address with Netlify one

It doesn't matter which DNS provider you use because DNS is DNS. So, I don't need to say "I'll use this X provider blah blah blah..."

Just replace your old nameserver with Netlify nameservers (they have 4 NS)

This process can take 1 hour to 2 days (with old experience...)

### Add DNS record other than main website

> Before you start this process make sure you have live Netlify website

Well, you just need to sign up with your GitHub, GitLab or BitBuckett account. After that, they will ask you website repository. Maybe, you have GitHub pages. Just give them permission for access your repositories. They will handle it all of things. You don't need to worry about that. Also, you don't do any extra action for build system. Netlify has auto-build system.

#### Fail!

![Fail deploy](https://i.imgur.com/OWWMaY4.png)

It just happened auto-build, they built 1 hour after

![Success deploy](https://i.imgur.com/0ANk3i9.png)

#### Add your domain

![Add your A rule](https://i.imgur.com/UhnSJmn.png)

Wait for a few hours because DNS system cannot change your old IP address with new one right away. This update took one and half hour for me. It may change for you this period.

#### Create Let's Encrypt SSL

![One click Let's Encrypt installation](https://i.imgur.com/eHHf54Q.png)

You just need to click one button, that's it

> Your DNS has to host in their nameservers. Otherwise, you cannot use Let's Encrypt.

![Let's encrypt ready to go](https://i.imgur.com/sgTSbTu.png)

DONE!

![Details from Netlify SSL dashboard](https://i.imgur.com/COMUG17.png)

Here it is some detail from the dashboard.

##### Force HTTPS

![Force HTTPS with Netlify](https://i.imgur.com/mnSD0mJ.png)

Maybe, you want to use only HTTPS for security reason.

They have a solution for that situation. One click. That's it. Ready to use, but it takes few minutes for effect.

## Conclusion

I liked their system, so I changed my all blogs with Netlify. It didn't take too much time, also it worth it. Now, I just use one dashboard for DNS, building, versioning etc. I can write one more blog about Netlify.

Thank you.
