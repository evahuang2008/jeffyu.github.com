---
date: '2005-08-11 06:11:28'
layout: post
slug: '%e5%9c%a8linux%e5%92%8cwindows%e4%b8%8a%e5%ae%89%e8%a3%85cvs'
status: publish
title: 在Linux和Windows上安装CVS
wordpress_id: '109'
categories:
- Chinese
- Others
---




在Linux上安装CVS,关键要看这么几个文件:




在/etc/service文件中是否有:
cvspserver      2401/tcp                        # CVS client/server operations
cvspserver      2401/udp                        # CVS client/server operations
到/etc/xinetd.d/目录下建立这么个文件,文件名随便.里面包含这些:




service cvspserver
{
disable         = no
socket_type     = stream
wait            = no
user            = root
server          = /usr/bin/cvs
server_args     = -f --allow-root=/home/cvsroot pserver
log_on_success  += USERID
log_on_failure  += USERID
flags           = REUSE
}
加个cvsroot的用户,而后执行:




cvs -d /home/cvsroot init
service xinetd restart
最后,执行
netstat -l | grep cvspserver
如果能看到
tcp 0 0 *:cvspserver *:* LISTEN




表明成功!

详细: [http://www.linuxfans.org/nuke/modules.php?name=Forums&file=viewtopic&t=92177](http://www.linuxfans.org/nuke/modules.php?name=Forums&file=viewtopic&t=92177) 

Windows上安装cvsnt,只需在他的consol pannel里的repository里面设置你要放的目录和ip地址,就可以了.





