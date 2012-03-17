---
date: '2009-10-22 03:22:00'
layout: post
slug: openfire-jwchat-tomcat-realtime-collaboration
status: publish
title: Openfire + jwchat + Tomcat = Realtime collaboration
wordpress_id: '258'
categories:
- Chinese
- Java
tags:
- jwchat
- Openfire
---

If you are building a web application, you might need customers use IM client to get to you easily, and can communicate with you on real time. Then I would recommend the [Openfire](http://www.igniterealtime.org/projects/openfire/index.jsp) (IM server) +[ jwchat](http://blog.jwchat.org/jwchat/) (web IM) to build your real time collaboration. All of these two are open source. Openfire also has its enterprise edition.

Following are two links about how to setup these two. (both of them are written in Chinese).

1. [构建 基于openfire + jwchat 的 WEB IM](http://www.javaeye.com/topic/154697?page=1)
2. [Openfire+jwchat linux 下安装记录](http://www.cnblogs.com/bluespot/archive/2008/07/17/1243164.html)

I am using the Openfire 3.6.4. But the steps are the same as before.

Update (Oct-24-2009), if you want to build your own web IM to communicate with Jabber server, then you'd better check out the [JSJAC library](http://blog.jwchat.org/jsjac/). One common issue due to the XMLHttpRequest is that is unable to get resource across the domain. Good news is that you could either [use the Apache mod_proxy or url rewrite to do so](http://www.enavigo.com/2008/10/14/setting-up-jsjac-with-openfire-352/), or you deploy a JHB servlet like what jwchat war did.
