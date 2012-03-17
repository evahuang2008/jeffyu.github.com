---
date: '2008-06-18 17:28:00'
layout: post
slug: install-firefox3-in-fedora8
status: publish
title: Install Firefox3 in Fedora8.
wordpress_id: '207'
categories:
- OS
tags:
- Fedora
---

Today is a big day for [Firefox](http://www.mozilla.com/en-US/firefox/), it just released its [firefox3.GA](http://www.spreadfirefox.com/en-US/worldrecord), with more than 15,000 improvements over firefox2.x.

So, I just can't wait to give that a try, but it seems that Fedora 9 shipped with the firefox3, as for Fedora8, it still sticks to the firefox2.x. Then I look for a firefox3 rpm package for F8, here comes the [i86 rpm](http://mirror.yandex.ru/fedora/tigro/8/i386/firefox3-3.0-1.fc8.i386.rpm), it is from this thread.[1]:

After you download the rpm, simply run: (Before installing firefox3, remember to keep a backup for your bookmark)

rpm -i firefox3....(your rpm filename).

Note: It doesn't work when I am running "yum localinstall ...", it seems failed in the GPG key check.

Once you finish the installation, simply open a shell, run: firefox3, make sure you have closed all the firefox browser, otherwise, it will still runs the firefox as same as what you are using now.
Your firefox3 and firefox2.x can be co-existed in your Fedora, but it just can be used one version at a time, it depends on which version you are firstly opened!

Although I know it is not a good/easy way for us to install software by using rpm, it is better to use the yum, so that we can make sure that the library dependencies get right, but currently, I haven't found the firefox3 in the F8 repository. Hopefully someone will upload it there.

Update: Ahh.... just found we can download the tar file from mozilla directly, extract and run the "./firefox" in your console. but need to make sure you have closed all the firefox web browser, otherwise, it won't get it updated. That is when I thought this approach might not work. :(

[Reference]
1: [http://forums.fedoraforum.org/showthread.php?t=192028](http://forums.fedoraforum.org/showthread.php?t=192028)
