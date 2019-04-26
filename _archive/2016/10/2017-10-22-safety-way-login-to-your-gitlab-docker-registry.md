---
title: Safety way login to your GitLab Docker registry
date: 2017-10-22
updated: 2018-03-24
layout: post
tags: Docker, GitLab
---

Hello Guys,

I am going to write about GitLab CI problem with docker login to the registry

`WARNING! Using --password via the CLI is insecure. Use --password-stdin.`

Because I spend hours this problem. Solution, so simple.

```
# Dockerfile
image: docker:stable-git

services:
  - docker:dind

stages:
  - build

before_script:
  - echo $CI_BUILD_TOKEN | docker login --username=gitlab-ci-token --password-stdin registry.gitlab.com # Normal --password="" for CLI use. You can't use in GitLab CI becaue is not safety way. You need to use STDIN, so just added your script this line everthing for login to registry.

after_script:
  - docker logout registry.gitlab.com

build:docker:
  stage: build
  script:
    - cd /builds/<username/groupname CASE SENSITIVE>/<reponame> # Enter your Git sources
    - docker build -t registry.gitlab.com/<username/groupname NO CASE SENSITIVE>/<reponame>/master:docker . # If you have Dockerfile in source root. You can build the image. If you don't have you need to change dot to your Dockerfile path
    - docker push registry.gitlab.com/<username/groupname NO CASE SENSITIVE>/<reponame>/master:docker # You need to push your container for after use.
```

If you Google it this problem, and you can see many solved problem (didn't work with GitLab CI), but I didn't solve my problem. I found this solution than I tried and everything fine right now.

Anyway, just you need Docker Login 's row for that problem. If you have problem already just contact with me.

Have a good day
