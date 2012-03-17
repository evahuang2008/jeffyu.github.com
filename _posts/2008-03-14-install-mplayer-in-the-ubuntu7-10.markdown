---
date: '2008-03-14 22:08:00'
layout: post
slug: install-mplayer-in-the-ubuntu7-10
status: publish
title: Install Mplayer in the Ubuntu7.10
wordpress_id: '182'
categories:
- OS
tags:
- Ubuntu
---

1. sudo apt-get install mplayer mplayer-fonts mozilla-mplayer
2. Download the win32codec from [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html), Choose the "Binary Codec Packages" title, the file name is sort of "linux x86 ...".
3. Extract the win32codec from the package in the /usr/lib/win32. (create it if it doesn't exist).
4. Start the Mplayer, it should be all set.

Q: Can play the sound ok, but without having any images.
A: running: sudo apt-get install libstdc++5 in the Shell.

Reference:
1. [Install MPlayer](http://wiki.ubuntu.org.cn/%E5%AE%89%E8%A3%85MPlayer)
2. [http://forum.ubuntu.org.cn/viewtopic.php?t=108805](http://forum.ubuntu.org.cn/viewtopic.php?t=108805)
