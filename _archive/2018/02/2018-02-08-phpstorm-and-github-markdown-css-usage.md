---
title: PHPStorm and GitHub markdown CSS usage
date: 2018-02-08
updated: 2018-03-25
layout: post
---

Hello guys,

You know, nowadays developer can prefer note editor or IDE. I prefer IDE for PHP but you can use note editor like atom or sublime.

I'm using JetBrains PHPStorm which most most powerful IDE I ever use. It has a lot feature. This not just PHP IDE. You can write node or SQL also Angular or VueJS. Anyway, I wanna show you one PHPStorm feature. Markdown editor.

PHPStorm has two type Markdown editor (engine) preview;
 - Default (In official document doesn't show the name)
 - JavaFX

I started using JavaFX and I feel sorry but I didn't find any changes. Maybe you can say what it is different than default ones.

If you looked/enabled JetBrains markdown editor, you can see really basic stuff. You can see bold text, or italic but not table.

That's why, I searched and I found one solution.

**Add CSS rule to our markdown editor**

Let's start.

## Change your preview mode to JavaFX
You can find this setting under the `Settings` > `Language & Frameworks` > `Markdown`

Also you can use `CTRL` + `ALT` + `S`. This is PHPStorm default settings shortcut

After that, you will see this settings.

![PHPStorm default preview settings](https://i.imgur.com/eN9Y6V9.png)

## Enable JavaFX and add your CSS rules

I don't need to say anything JavaFX, but I will show you how to find CSS rules in online, or I'll share with you what I am using for my IDE.

[GitHub Markdown CSS rules](https://github.com/sindresorhus/github-markdown-css)

You can use this link, I used. Thank you [sindresorhus](https://github.com/sindresorhus)

![PHPStorm JavaFX enabled, also it is using GitHub CSS rules](https://i.imgur.com/nra1MuH.png)

## Let's look at

![PHPStorm and GitHub markdown CSS rules](https://i.imgur.com/6Qgndu5.png)

Wow, it is too easy. Right. It was to easy and that's it.

## Conclusion

JetBrains' IDEs are awesome. Those are has a lot feature and we used just one plugin which markdown editor. See you my next blog.
