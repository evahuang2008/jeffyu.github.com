---
date: '2005-06-13 10:46:24'
layout: post
slug: design-pattern-thinking
status: publish
title: Design Pattern Thinking
wordpress_id: '124'
categories:
- Chinese
- Thoughts
tags:
- Design Patterns
---



记得自己刚开始接触到设计模式的,是在2003年11月份的时候,最早看的是从jdon上面下载的<pattern in java>,后来在12月份看的是《Design pattern explained》(DDE),可以说这后面这本书对我的印象非常深刻.第1本书给我的感觉是,好像说的挺好玩的,挺有意思的.而后者给我的感觉就是说这本书会分析说我们为什么会有这些模式,这些模式是怎么解决我们的问题.

说说DDE这本书吧,我记得书里面有这么一段章节:
Find What Is Varying and Encapsulate It
In Design Patterns: Elements of Reusable Object -Oriented Software, the Gang of Four suggests the following:
Consider what should be variable in your design. This approach is the opposite of focusing on the cause of redesign. Instead of considering what might force a change to a design, consider what you want to be able to change without redesign. The focus here is on encapsulating the concept that varies, a theme of many design pat-Using inheritance this way in design patterns terns.
Or, as I like to rephrase it, "Find what varies and encapsulate it."
These statements seem odd if you only think about encapsulation as data-hiding. They are much more sensible when you think of encapsulation as hiding classes using abstract classes.

找出你可能需要改变的,或者说存在改变的地方,把他封装起来.不让外界知道更多的详细信息.这里的封装并不仅仅是封装数据,行为等,可以说封装一切.

设计模式其实也就是主要针对各个不同变化的类型,采取了不同的解决方案的总和.
我个人比较推荐这本书,特别是对像我这种设计模式的初学者,里面写的很好,我每次看,都有些不同的感觉.

.................(待续)


