---
date: '2008-03-15 18:18:00'
layout: post
slug: make-xmms-show-chinese-font-correctly
status: publish
title: Make XMMS show chinese font correctly.
wordpress_id: '183'
categories:
- OS
tags:
- Ubuntu
---

Below is the steps that work for me, which is Ubuntu7.10.

1. Create a .gtkrc.mine file with following content:

    
    # $(gtkconfigdir)/gtkrc.zh_CN## This file defines the fontsets for Chinese language (zh) using# the simplified chinese standard GuoBiao as in mainland China (CN)## 1999, Pablo Saratxaga #
    
    style "gtk-default-zh-cn" {fontset = "-adobe-helvetica-medium-r-normal--12-*-*-*-*-*-iso8859-1,-*-*-medium-r-normal--16-*-*-*-*-*-gb2312.1980-0,*-r-*"}class "GtkWidget" style "gtk-default-zh-cn"


2. sudo apt-get install xmms-mpg123-ja

3. Set the XMMS font as:

    
     -adobe-helvetica-medium-r-normal--12-*-*-*-*-*-iso8859-1,           -*-*-medium-r-normal--16-*-*-*-*-*-gb2312.1980-0,*-r-*


Reference:
1. [http://forum.ubuntu.org.cn/about10340-0.html](http://forum.ubuntu.org.cn/about10340-0.html)
