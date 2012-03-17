---
date: '2009-07-08 19:42:00'
layout: post
slug: fedora-environment-setting
status: publish
title: Fedora environment setting.
wordpress_id: '231'
categories:
- OS
tags:
- Fedora
---

I still recalled that when I used the Ubuntu, I put all of my environment variables, like JAVA_HOME et al in the .bash_profile file, and if I want to make it effect, I am running the:

source .bash_profile

But in Fedora, I couldn't make it effect unless I do the logout & login.
And then searched on the google, it turns out the people would do as following:

put all of environment setting in the .bashrc file, and then if you update it, try to

source .bash_profile

It will make all of updates effective.

I tried it, it works as it was told. So, now I changed my habit, put the environment setting to the .bashrc file.
