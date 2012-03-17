---
date: '2008-06-17 01:32:00'
layout: post
slug: fedora8-in-lenovo-t61p-with-projector
status: publish
title: Fedora8 in Lenovo T61P with Projector
wordpress_id: '205'
categories:
- OS
tags:
- Fedora
---

As you might know projectors often do not work well with widescreen laptop, which installed Fedora. So my T61P does not work with the projector in my office.
Today, I've found a way to fix that. (Actually it was told by my colleague Denny). By that reducing the screen resolution and using the "Dual Head" functionality in the Display.

The steps are:

System -> Administration -> Display -> Dual Head tab.

Checked the "Use dual head" option.
And then select the resolution as "1280X1024".  (Remember to save your original one as a backup in case of the change doesn't work for you and cause your xwindow broken.)

And then reboot the system. Hopefully it works for you too.
