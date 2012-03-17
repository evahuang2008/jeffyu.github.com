---
date: '2008-03-25 13:53:00'
layout: post
slug: fedora8-installation
status: publish
title: Fedora8 installation
wordpress_id: '190'
categories:
- OS
tags:
- Fedora
---

Because I need to use fedora in my company, below are some install instruction.

1. Input chinese input.
1) running: yum groupinstall chinese-support
2) System -> Preference -> Personal -> InputMethod: Tick enable input method feature option.

2. Polish the chinese font.
1) Copy the fonts from Windows system.
cd /usr/share/fonts
mkdir windows
cp all windows font on it.
fc-cache /usr/share/fonts/windows
fc-cache -fv
2) restart Xwindow
3) Update the System font and firefox fonts accordingly.

Reference:
[1] [http://sandajian.googlepages.com/fedora8-chinese](http://sandajian.googlepages.com/fedora8-chinese)
[2] [http://www.5istudy.cn/system/unix-linux/Fedora7-332.html](http://www.5istudy.cn/system/unix-linux/Fedora7-332.html)
