---
layout: post
title: AWS Lambda, Serverless, and DynamoDB
image: /public/images/2018/09/2-serverless-application-architecture.png
date: 2018-09-06 08:45 -0700
updated: 2019-04-24 15:10 -0700

categories:
  - microservices
tags: [AWS, Lambda, DynamoDB, Serverless]
---

A few years ago, microservices was one of the revolutionary development
technique, and tech companies had moved to this architecture because of the
ease of maintain. Furthermore, Docker, Kubernetes, and other cool open-source
projects are thanked this architecture because they were built on top of
it.

Well, let's see why they prefer to move this magic development technique.

## Idea of a microservices

Before we dive into microservices, we need to know what is a monolith
application; then, we will talk about microservices.

[![Monolith vs microservices](/public/images/2018/09/1-monolith-vs-microservices.png)](https://aws.amazon.com/microservices#Monolithic_vs._Microservices_Architecture)

As in the figure, the monolith architecture acts like one application with user
service, or posts service. However, microservices architecture has different
services, and it makes the architecture scalable since you can add an additional
service like "Search Service". Although, microservices is not a "must". Like
every other architecture, **it is a solution that resolves a problem**.

In this case, AWS Lambda, API Gateway, and other cool AWS technologies give
developers a ready-to-serve microservices architecture.

So, what will you achieve with AWS Lambda, API Gateway, DynamoDB?

1. Pay only what you have used
2. Scale a service, or function from 1 to 1000000 users
3. Just write your code. There is no managing your infrastructure

## Serverless microservices architecture

![Serverless application architecture](/public/images/2018/09/2-serverless-application-architecture.png "Serverless application architecture")

When we talk about *serverless*, it does not mean that there is no servers. We
still need them to serve these information with client, but in this case, we
will not manage it; therefore, it is called *serverless*.

### How does this architecture work?

Let's discuss what is going on this serverless application architecture.  
You will see that we have an user who wants to vote something with smartphone
via an application. We already know that mobile applications have to use API
back-end because nothing will store on user phone. The gateway will route the
request to Lambda which is piece of code that will write the record to DynamoDB.
DynamoDB will trigger second Lambda, so it will recalculate, and S3 will have
the static HTML content.

The user who voted before can check out the result of the voting via website
which is static HTML, and it is served by S3.

## Conclusion

Microservices architecture gives a chance to developers easy to maintain, and
scalable architecture. Furthermore, AWS Lambda gives cost-effective, secure,
code-first system.
