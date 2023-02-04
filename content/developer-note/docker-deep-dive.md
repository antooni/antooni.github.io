---
title: "Docker deep dive"
date: 2023-02-04
tags: ["docker", "codecrafters"]
draft: false
---

# Motivation
There are two main reasons for writing this article: 
- need to set up dev environment in docker
- recent finding of coding tutorial [Build your own docker](https://codecrafters.io/)

In addition I would like to understand docker in depth, because currently I know the concept, can use it as a black box, but nothing more. I am personally very curious about inner work of this tool.

# Pre-existing knowledge
> I would describe myself as a docker "advanced-beginner"

- understand the use case of this technology and facilitate it with the help of copy pasting from the internet
- have some awareness about its inner work: that it creates system inside my system, with its own memory scope, stripped out of everything beyond essentials
- wrote a `Dockerfile` and know how crucial (and useful) it is for automatization
- wrote a `docker-compose` and run it, also understand use-case of this tool
- wrote `Jenkins pipeline` using docker images
- created working dev environment in docker, consisting of ubuntu image and postgres database, deployed with `docker-compose`, to which I connect via SSH

Especially during this last point (dev-env), I felt inner need to better understand it, how Dockerfile file works, how it rebuilds, how docker-compose uses Dockerfile, is it rebuilt every time, how to write efficient tooling with it, and finally how it all works under the hood.

