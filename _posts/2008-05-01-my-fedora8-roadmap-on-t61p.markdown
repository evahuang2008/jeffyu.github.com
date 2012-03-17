---
date: '2008-05-01 15:51:00'
layout: post
slug: my-fedora8-roadmap-on-t61p
status: publish
title: My Fedora8 Roadmap on T61P
wordpress_id: '201'
categories:
- OS
tags:
- Fedora
---

1. firstly, you need to install the Fedora8 in "text mode", because the ndivia driver issue. (be patient, this issue will be resolve in next. ;-)

2. Add repositories.
1) [Livna](http://rpm.livna.org/livna-release-8.rpm): rpm -i http://rpm.livna.org/livna-release-8.rpm
2) [FreshRPMS](http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/7/freshrpms-release/freshrpms-release-1.1-1.fc.noarch.rpm): rpm -i http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/7/
freshrpms-release/freshrpms-release-1.1-1.fc.noarch.rpm

3. Two ways to solve the display/video problem.



	
  * 2.1 log in as a root, and then update the /etc/X11/xorg.conf by using "vesa" mode, it should be located in the "Dirver" section. basically, need to change from the "nv" to "vesa" in a refresh installation.

	
  * 2.2 using "yum install kmod-nvidia, xorg-x11-drv-nvidia", if it asks you to upgrade the kernel first, which is my case.  I need to run the "yum update kernel".
After you installed the drivers, and run the "startx" to log in the X window.


4. Install compiz packages, 3D effect.
Detail please see [this link](http://www.fedoraguide.info/index.php/Main_Page#Compiz-fusion_.283D_effects.29).

5. Install chinese-input & fonts
See my the other [blog entry here](http://jeffyuchang.blogspot.com/2008/03/fedora8-installation.html).

6. Update System.
"yum -y upgrade"

7. Other softwares.
yum install xchat,
stardict,
skype,
thunderbird,
xmms, xmms-mp3, xmms-wma,
mplayer,smplayer
......

8. Update the default level for initialization.
By default, the machine will run on Level 3, it means that it won't start the X window automatically, you can modify it in "/etc/inittab" file, around line 18.

[Reference]
1. [Fedora8 on ThinkPad T61P](http://www.thinkwiki.org/wiki/Installing_Fedora_8_on_a_ThinkPad_T61p)
2. [Gustavo's Fedora8 roadmap ](http://gka-linux.blogspot.com/2007/11/my-fedora-8-road-map.html)
3. [Fedora8 Guide](http://www.fedoraguide.info/index.php/Main_Page)
