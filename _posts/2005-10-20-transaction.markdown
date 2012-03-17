---
date: '2005-10-20 00:29:52'
layout: post
slug: transaction
status: publish
title: Transaction...
wordpress_id: '94'
categories:
- Java
---

  今天早上来demo,来的比较早,闲来无事,就看看TSS,有个帖子是问Transaction的问题,是这样的:([http://www.theserverside.com/news/thread.tss?thread_id=37173](http://www.theserverside.com/news/thread.tss?thread_id=37173))




   当我们新建一个Connection时候,设置它的connection.setAutoCommit(false),那么如果我们到最后的时候,直接关闭掉Connection,他会执行commit 还是rollback呢? (很多人可能会说,代码不能写. ok,我也知道,但关键是我们要探讨在这种情况下,数据库会怎么处理呢?)  
  在TSS看完这个问题后,我也稍微看了下些comments,不大去关心这个问题,只觉得,以后一定要显式调用commit or rollback,在后来用FeedDemon收了Gavin King的Blog,发现他就这个问题写了篇Blog([http://blog.hibernate.org/cgi-bin/blosxom.cgi/2005/10/19#popquiz_connectionclose](http://blog.hibernate.org/cgi-bin/blosxom.cgi/2005/10/19#popquiz_connectionclose)),写的很详细,虽然我对他本人不是很喜欢,(或者是因为之前跟Rod的争吵,让我感觉到他没什么风度),但是他的数据库知识和Java的知识,这还是应该不在我之下的..(嘿,我说,谁的西红柿和臭鸡蛋.),这篇Blog解释的很详细.  
  回到问题,那么,数据库到底是会执行commit or rollback呢? 答案是: it depends, 要看vendor实现,就比如说Oracle,他是执行commit的,但不同的厂商,有不同的实现,因为Jdbc的specification对这个没有明确规定,所以oracle执行commit也是没有违反规则的...  
 当然了,从这篇文章,我们只能说如果自己以后设置connection的autoCommit为false的时候,自己切记,一定要显示(explicity)执行rollback or commit.




  
