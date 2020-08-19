---
title: Deploy an application to Heroku in GitLab CI
date: 2018-01-30
updated: 2018-03-25
layout: post
tags: Heroku, GitLab
---

If you are developer sometimes you can build a server, right? But, developers don't like this building stage because they don't need to know ip configuraiton, DNS zones, Redis conf files, MySQL default engine and so on.

That's why developers are using PaaS. If you want to know more about you can check my another blog. Here it is the [link](https://blog.berkhanberkdemir.com/2017/11/25/What-am-I-thinking-about-Heroku/index.html)

## What I will use

I will use example [symfony/demo](https://github.com/symfony/demo). Actually they have TravisCI, but if we are working with GitLab (like me), how we can solve this problem.

You have to have;
 - GitLab.com account
 - git

> WARNING: This blog not for production stage application. This is just experience. If you did something, you did.

Let's start

## Install demo app (optional)...
First of all, we have to get the application with git.

`git clone https://github.com/symfony/demo`

Now, you can enter to directory with

`cd demo`

If you type `ls`, you will see a lot of stuffs. Now, don't touch it also don't configure it.

> You can create your own Symfony application. I won't test it (phpunit) or build it (webpack). Just installing Heroku and deployment automation.

We are going to write `.gitlab-ci.yml` file.

## The CI

I love GitLab because you can find many tools/utility or functions in inside of GitLab. For example, service desk feature, CI/CD, Docker Registry and so on...

## Writing `.gitlab-ci.yml`

### Update Debian repositories

I am using PHP container which is official container from Docker. This container based on Debian. That's why we will use apt-get package management system. Next part we will update repositories with `apt-get update -yqq`.

-y flag means if apt-get would require something for confirm you will accept it.

-qq flag means I just see in `Dockerfile`. Few people prefer -qq flag but I am using -q=2 because you won't get an output from apt-get.

```yaml
images: php:7.1-cli
deploy:
    stage: deploy
    script:
        - apt-get update -y -q=2
```

### Download git on Debian

In Docker container doesn't have git. That's why we will install git.

```yaml
deploy:
    stage: deploy
    script:
        - apt-get update -y -q=2
        - apt-get install -y -q=2 git
```

## Basic CI template

This is template for us. Heroku is working with git version control system. We will use that. Like add it, push it. That's it.

But, if you have a Database system, you have to run `doctrine:schema:create` or `doctrine:database:create`. That's why, we will download Heroku Toolbent..

```yaml
deploy:
    stage: deploy
    script:
        - apt-get update -y -q=2
        - apt-get install -y -q=2 git
        - git remote add heroku https://heroku:$HEROKU_API_KEY@git.heroku.com/$HEROKU_APP_NAME.git
        - git push -f heroku master
```

## Download Heroku toolbent on Container

With these easy steps you will get Heroku. You must have `software-properties-common` and `apt-transport-https`. You can not install Heroku.

```yaml
deploy:
    stage: deploy
    script:
        - apt-get update -y -q=2
        - apt-get install -y -q=2 software-properties-common apt-transport-https
        - add-apt-repository "deb https://cli-assets.heroku.com/branches/stable/apt ./"
        - curl -L https://cli-assets.heroku.com/apt/release.key | apt-key add -
        - apt-get update -y -q=2
        - apt-get install -y -q=2 heroku
```

## Let's see the code

```yaml
deploy:
    stage: deploy
    variables:
        HEROKU_AUTH_KEY: aa-xx-bb-yy
        HEROKU_APP_NAME: heroku-symfony-4-demo
        HEROKU_API_KEY: xx-aa-yy-bb
        HEROKU_MAIL: xx@gmail.com
    script:
        - apt-get update -y -q=2
        - apt-get install -y -q=2 software-properties-common apt-transport-https
        - add-apt-repository "deb https://cli-assets.heroku.com/branches/stable/apt ./"
        - curl -L https://cli-assets.heroku.com/apt/release.key | apt-key add -
        - apt-get update -y -q=2
        - apt-get install -y -q=2 git heroku
        - git remote add heroku https://heroku:$HEROKU_API_KEY@git.heroku.com/$HEROKU_APP_NAME.git
        - git push -f heroku master
        - echo -e "\nmachine api.heroku.com\n    login ${HEROKU_MAIL}\n    password ${HEROKU_AUTH_KEY}\nmachine git.heroku.com\n    login ${HEROKU_MAIL}\n    password ${HEROKU_AUTH_KEY}" > $HOME/.netrc
        - heroku run "php bin/console cache:clear" --app $HEROKU_APP_NAME
        - heroku run "php bin/console cache:warmup" --app $HEROKU_APP_NAME
        - heroku run "php bin/console doctrine:database:drop --force" --app $HEROKU_APP_NAME
        - heroku run "php bin/console doctrine:database:create" --app $HEROKU_APP_NAME
        - heroku run "php bin/console doctrine:schema:create" --app $HEROKU_APP_NAME
        - rm -rf $HOME/.netrc
        - unset HEROKU_APP_NAME
        - unset HEROKU_API_KEY
        - unset HEROKU_AUTH_KEY
        - unset HEROKU_MAIL
```

WOOW!

What was that?!?

First of all you have to have ./.netrc for Heroku login. This is not such a good idea for store your authentication key in `.gitlab-ci.yml`. But if you have a private repo and just you are accessing to repo it is not problem.

## Conclusion

Heroku is simple PaaS I have ever used. That's why, I use a lot during development stage. It is masterpiece for me. Also, GitLab important place for my heart because it is saved my life many time. I recomended both services. You don't need to pay, just use it. That's it.
