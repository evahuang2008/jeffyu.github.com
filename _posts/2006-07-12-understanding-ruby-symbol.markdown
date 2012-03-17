---
date: '2006-07-12 16:58:08'
layout: post
slug: understanding-ruby-symbol
status: publish
title: Understanding Ruby Symbol
wordpress_id: '48'
categories:
- Ruby
---

在用Rails的时候,经常会碰到Symbol的用法,比如:




  `link_to("View Article", :controller => "articles", :action => "index")`




`其实Symbol跟字符串很类似,不同的是:`一般来说，symbol是interned名字或字符串 ，使用它的话，可以避免相同字符串的多个拷贝，节省内存....




详细的请参见:




([http://glu.ttono.us/articles/2005/08/19/understanding-ruby-symbols](http://glu.ttono.us/articles/2005/08/19/understanding-ruby-symbols))
