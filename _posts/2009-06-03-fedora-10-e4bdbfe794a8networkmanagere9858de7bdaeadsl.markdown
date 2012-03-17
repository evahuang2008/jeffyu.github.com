---
date: '2009-06-03 18:34:00'
layout: post
slug: fedora-10-%e4%bd%bf%e7%94%a8networkmanager%e9%85%8d%e7%bd%aeadsl
status: publish
title: Fedora 10 使用NetworkManager配置ADSL
wordpress_id: '228'
categories:
- Chinese
- OS
tags:
- Fedora
---

在Fedora 10 下使用 NetworkManager 来配置ADSL.



	
  1. su -c NetworkManager (启动NetworkManager)

	
  2. 点击NetworkManager的图标, 看到VPN Connections, 选择Configure VPN

	
  3. Go to DSL Tab,

	
  4. Add DSL, 输入: username, password etc


然后重启 NetworkManager, 使用 DSL 来连接即可.
