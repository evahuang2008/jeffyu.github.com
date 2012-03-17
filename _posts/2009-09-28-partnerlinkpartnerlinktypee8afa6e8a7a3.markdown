---
date: '2009-09-28 03:04:00'
layout: post
slug: partnerlinkpartnerlinktype%e8%af%a6%e8%a7%a3
status: publish
title: PartnerLink,PartnerLinkType详解
wordpress_id: '255'
categories:
- BPM
- Chinese
tags:
- BPEL
---

记得我在看BPEL的时候,总是对PartnerLink和PartnerLinkType概念比较混淆,特别是里面的partnerRole, myRole属性的疑惑,后通过查阅资料,觉得理解得差不多,特分享自己的学习笔记.

BPEL的出现,最主要是想提供一个业务流程(process)的语法,从另外一个方面,也就是想对已有的服务(这里限定于发布成web service的服务)进行一系列的编制(orchestration),然后变成一个新的服务(默认也是发布成web service). 这从一方面来说,也算是重复利用了已有的服务.

BPEL Process主要包括了Activity的概念,里面有包括最基本的Receive,Invoke, Reply等primitive Activity,也包括了strcture activity,比如sequence, flow, case等. 那既然我们定义了这些activity,又是怎么跟外部的已有服务进行联系上呢. 那么就是通过我们所要讲的PartnerLink, PartnerLinkType来关联.

我们先来看下PartnerLinkType. 我比较赞同把PartnerLinkType比喻成通道{Note: 来自于reference[2]的文章}. 可以这么想, BPEL Process是一个web service,这个服务是通过什么方法来与其他已经存在的另外一些web service(s)进行关联呢?PartnerLinkType就是定义这样的一个通道.

先看下PartnerLinkType的例子.

[xml]
<plnk:partnerLinkType name="AuctionHouse_SellerLT">
<plnk:role name="AuctionHouse" portType="tns:sellerPT" />
<plnk:role name="Seller" portType="tns:sellerAnswerPT" />
</plnk:partnerLinkType>
[/xml]

注意这里定义的role可以有1个或者2个,在这个例子当中,我们看到的是2个,代表着需要两个portType(类似Java的Interface)来完成这个通道.这种情况一般是属于异步(Asynchronous)的情况. 我们也可以看做是2个的叫做双向,1个的叫做单向. 1个的一般直接是同步(Synchronous)的,可以直接获取到结果的,不用向异步那样需要一个回调方法(callback).

介绍完PartnerLinkType,可以把PartnerLink想做是PartnerLinkType的实例化.但有点不同的是,在上面我们讲到PartnerLinkType是有单向和双向的,在双向的情况下,那到底是哪个方向呢?比方说,到底是从A ->B 还是从 B -> A呢? PartnerLink的定义就会明确规定了这个方向,比如说:

[xml]
<partnerLink name=”seller”
   partnerLinkType=”AuctionHouse_SellerLT”
   myRole=”AuctionHouse” partnerRole=”Seller”>
</partnerLink>
[/xml]

注意到这里的myRole和partnerRole的属性,这两个属性指明了PartnerLinkType的方向. 这里, MyRole是指BPEL Process, partnerRole是指外部的we service. 那么,这个例子当中就是,这个通道是从bpel process流向exernal web service.也就是有个请求发送到bpel process,然后bpel process通过这个通道,调用到外面的web service,然后外部的web service再传递结果给bpel process.

这里,我们还得看下单向的情况(也就是在定义PartnerLinkType时,只有一个role的). 比方下面的这个例子.

[xml]
<plnk:partnerLinkType name="loanPartnerLT">
<plnk:role name="loanService" portType="tns:loanServicePT" />
</plnk:partnerLinkType>
<plnk:partnerLinkType name="loanApprovalLT">
<plnk:role name="approver" portType="tns:loanApprovalPT" />
</plnk:partnerLinkType>
[/xml]

再看PartnerLink的定义.

[xml]
<partnerLink  name="customer"
partnerLinkType="lns:loanPartnerLT"
myRole="loanService" />

<partnerLink name="approver"
partnerLinkType="lns:loanApprovalLT"
partnerRole="approver" />
[/xml]

在这里,第一个customer的partnerLink定义,说明这个管道是从bpel process这个方向开的,也就是说Request的message应该是发到 Bpel Process. 相反的,第二个approver是属于partnerRole,也就是说这个Request Message应该是BPEL Process发给 partner (也就是外部真正提供服务的web service).

可以推知，凡是partnerLink中定义了myrole的地方，都是外界要调用bpel process的地方，必然对应receive操作.

注意,因为这个PartnerLinkType是WSDL的一个扩展点,所以很多时候,对于这个PartnerLinkType就直接定义在WSDL文件里,而不放在.bpel文件中.

[Reference]
0. [WSBPEL 2.0 specification](http://docs.oasis-open.org/wsbpel/2.0/OS/wsbpel-v2.0-OS.html)
1. [PartnerLinks and PartnerLinkTypes](http://infocenter.activevos.com/infocenter/ActiveVOS/v60/index.jsp?topic=/com.activee.bpel.doc/html/UG8-2.html)
2. [BPEL中的PartnerLink和PartnerLinkType](http://www.zhaoxiangpeng.com/articles/bpel%E4%B8%AD%E7%9A%84partnerlink%E5%92%8Cpartnerlinktype.html)
