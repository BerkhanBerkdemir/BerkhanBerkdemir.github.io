---
layout: post
title: Using rbenv
image: /public/images/2019/4/2-adi-goldstein-671017-unsplash.jpg
date: 2019-04-25 17:38 -0700
---

![Everyone Can Code](/public/images/2019/4/2-adi-goldstein-671017-unsplash.jpg "Everyone Can Code")
*Photo by [Adi Goldstein](https://unsplash.com/photos/mDinBvq1Sfg) on
[Unsplash](https://unsplash.com/search/photos/codet)*

I was using default Ruby version (2.5.1) which comes by default on Ubuntu 18.04,
and I did not need to run multiple version of Ruby &mdash; or latest one.

Today, I needed to work with Ruby 2.6.3 on Project
[Mağara](https://github.com/magara/magara).

## Is this your first time with Ruby?

Well, I need to say that I really do not remember the dependencies of Ruby on
Ubuntu, so I did quick search on the Internet.

```
sudo apt install libssl-dev libreadline-dev zlib1g-dev autoconf bison \
  build-essential libyaml-dev libreadline-dev libncurses5-dev libffi-dev \
  libgdbm-dev
```

## Remove everything about previous Ruby

I was using default Ruby, so I need to delete before take an action

```
sudo rm -rf /usr/bin/bundle*
sudo rm -rf /usr/lib/ruby
sudo apt remove ruby*
```

Before get start, please reboot your system; otherwise, you can get unexpected
errors, which I got some of them, for example when rbenv tries to build
`eventmachine`, you'll get an error.

## Installing rbenv

I used `rbenv-installer` because who wants manual way when they have automated
script?

```
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash
```

I installed the rbenv, but it complains about something *doctor*. After that I
go to bottom of the `.bashrc` with Vim editor

```
vi ~/.bashrc
```

add the `PATH` variable and save when you exit

```bash
export PATH="$PATH:$HOME/.rbenv/bin"
eval "$(rbenv init -)"
```

Close the terminal and open new one. I was excited, and I want to download
2.6.3, and I did with

```
rbenv install 2.6.3
```

However, I got an error about missing libraries

```
berkhan:~$ rbenv install 2.6.3
Downloading ruby-2.6.3.tar.bz2...
-> https://cache.ruby-lang.org/pub/ruby/2.6/ruby-2.6.3.tar.bz2
Installing ruby-2.6.3...

BUILD FAILED (Ubuntu 18.04 using ruby-build 20190423)

Inspect or clean up the working tree at /tmp/ruby-build.20190424185613.10421
Results logged to /tmp/ruby-build.20190424185613.10421.log

Last 10 log lines:
installing capi-docs:               /home/berkhan/.rbenv/versions/2.6.3/share/doc/ruby
The Ruby openssl extension was not compiled.
The Ruby readline extension was not compiled.
ERROR: Ruby install aborted due to missing extensions
Try running `apt-get install -y libssl-dev libreadline-dev` to fetch missing dependencies.

Configure options used:
  --prefix=/home/berkhan/.rbenv/versions/2.6.3
  LDFLAGS=-L/home/berkhan/.rbenv/versions/2.6.3/lib
  CPPFLAGS=-I/home/berkhan/.rbenv/versions/2.6.3/include
```

and, I go back and run what rbenv says

```
sudo apt install -y libssl-dev libreadline-dev
```

I think we can run it again, right?

```
rbenv install 2.6.3
```

Voilà

```
berkhan:~$ rbenv install 2.6.3
Installing ruby-2.6.3...
Installed ruby-2.6.3 to /home/berkhan/.rbenv/versions/2.6.3

berkhan:~$ ruby --version
ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-linux]
```

## Updating Bundler

I use Bundler 2.x and rbenv brings 1.x, so UPDATE TIME!

```
berkhan:~$ gem update
...
berkhan:~$ bundler --version
Bundler version 2.0.1
```

Be careful about which version of bundler bundled your Gemfile.lock. If the
lock file bundled with 1.x, you will see 1.x with `bundler --version`.
