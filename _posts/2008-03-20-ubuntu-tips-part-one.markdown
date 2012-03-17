---
date: '2008-03-20 03:50:00'
layout: post
slug: ubuntu-tips-part-one
status: publish
title: Ubuntu Tips - Part one
wordpress_id: '188'
categories:
- OS
tags:
- Ubuntu
---

1. You need to set the ubuntu environment in /etc/profile, such as JDK setting and so on. putting other settings that need to be initialized firstly in the .bashrc.

2. Install software in the /usr/local/share/applications

3. Install packages in the /opt/ folder.

4. start or stop vsftp server
sudo  /etc/init.d/vsftpd [start | stop | restart]

5. Install printer from window-shared.
* install the samba
* System -> Administration -> Printing -> New Printer

6.  Accessing Windows shared files. (samba server is required)
Open nautilus，CTRL+L，in the location input smb://192.168.100.x .

7.  Use xchm to open the chm file.

8. Using du -sh File to show the File size. such as:
du -sh /opt/downloads

9. Press "CTRL + H" to show the hidden files in the nautilus.

10. Show what kind of process occupy the "sound"
lsof  /dev/snd/controlC0

11. Create a soft link:
ln -s source target

12. Remove a link:
unlink linkName

13. for the bz2 archive, use
bunzip2 fileName.bz2 to extract the archive.
