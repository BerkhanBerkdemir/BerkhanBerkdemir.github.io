---
title: Why did I move my blog from Hexo to Jekyll
date: 2018-03-25
layout: post
---

Hello guys,

Today I am going to write about my blog migration from Hexo. Why did I migrate my website?

Well, Hexo and Jekyll provide SSG (aka Static Site Generator). My hexo system worked fine but I don't have any idea for NodeJS or EJS etc.. So, I decided to move my Hexo to Jekyll.

I searched for importer. I found but they don't support Hexo directly. I need to use RSS as an importer. I did but it didn't work also I got an error.

However, I had wanted to move Jekyll and I will do.

I started manual migration by hand. It is sound crazy but you know. If you have just one chance you will try, right and I did.

Now, you are reading this page with Jekyll.

## Why I interested too much with Jekyll?

I had started to learn Ruby 'and' Rails, so I moved my all system to Ruby. In my philosophy,

> If you want to learn something for programming you need to live with it.

Maybe, you won't agree with this quote, but I learned PHP with this way. I had started blogging with WordPress, I learned Symfony and Silex. While I was learning Symfony, I looked at MySQL/Redis and so on...

This means not you have to; therefore, you don't need to migrate your blog to new system for learning purpose. If you feel comfortable just leave it.

## I really like Jekyll, but why?

Actually, this is in my perspective, so it can change for you. I liked Ruby. It is really beautiful language. It has really understandable syntax. You can read what you write like English. I want to share with you some block of code.

```ruby
redirect_to login_path unless logged_in?
```

It says,

> Redirect to login path unless logged in.

Yes, you got it :smiley:.

```php
if (logged_in) {
  redirect_to(login_path);
}
```

But, when you write with different language like PHP? Maybe you need to provide some comment.

**Warning:** This compression means not "PHP isn't understandable"! I am just writing about Ruby syntax close to English. Another word, you can write like

```ruby
if logged_in? == false
  redirect_to login_path
end
```

Seems like that I wrote with PHP.

That's enough, I think.

## Easy to develop

Just read these rows

```liquid
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  {%- seo -%}
  <link rel="stylesheet" href="{{ "/assets/main.css" | relative_url }}">
  {%- feed_meta -%}
  {%- if jekyll.environment == 'production' and site.google_analytics -%}
    {%- include google-analytics.html -%}
  {%- endif -%}
</head>
```

> If you don't have any idea with templating and you are little bit curious about that just follow the Wikipedia link about [Template Processor](https://en.wikipedia.org/wiki/Template_processor)

Well, I just shared this simple code piece. You can call "base template" or "base layout". For example, let's look for this `if` statement.

It says if Jekyll environment equals `production` and `google_analytics` variable available in your `_config.yml` include `google-analytics.html` file into this template.

Easy, right? I heard some "nuh"

## Conclusion

Jekyll, Ruby or Rails. Awesome parts for developing or writing your blog. Because they keep simple as they can do. That's why startups can prefer Ruby as a development language since it is simple and you can get result with few code.

If you have any question just add to Disqus. Comments are important for me.

Thank you.
