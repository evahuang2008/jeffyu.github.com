---
date: '2008-05-05 15:44:00'
layout: post
slug: using-wireless-in-fedora8-for-t61p
status: publish
title: Using wireless in Fedora8 for T61P
wordpress_id: '202'
categories:
- OS
tags:
- Fedora
---

1. Go to System -> Administration -> Network
You will see the wireless was shown as: wlan0

2. Edit dialog, make sure the "Activate device when computer starts" unchecked
"Controlled by NetworkManager" checked. if you haven't installed the NetworkManager utility,
then use "yum install NetworkManager" command to install it.

3. Go to System -> Administration -> Services, Checked the "NetworkManager" and "NetworkManagerDispatcher", so that they can start automatically when you start your computer.

4. Reboot the system. (You can try to run: service network restart, but I just simply restarted it).

PS: you can use "iwconfig" to see your wireless device, and use the "iwlist wlan0 scan" to see your available wireless. here wlan0 is your wireless device name.
