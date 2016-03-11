---
layout: post
title:  "关于Chaos Monkey Test在超复杂系统中的应用"
date:   2016-03-11
categories: 系统测试

---

* content
{:toc}


## 前言
第一次接触到Chaos Monkey在软件领域的应用是在13或者14年左右，当时是在Android的测试中，由于智能机都是触摸屏的，用户触摸屏幕激发页面中的功能，可能行比较多，这样对于客户端软件的健壮性要求比较高，如何能够更加贴近的模拟呢？然后就引入类似猴子胡乱点击的思路，叫做Chaos Monkey的方式来做健壮性的测试。

## Chaos Monkey的思路分布式环境中的应用
+ 分布式环境，目前随着互联网架构以及云设施的普及，云端以及分布式，成为越来越多应用系统构建的思路，在支持高并发以及大数据上，分布式环境展现出很好的优势，但是物理环境的复杂度也随之上升，那也导致了稳定性以及健壮性的复杂，在做功能测试的时候，健壮的问题一般会被忽略掉，如果引入Chaos monkey的思路，那就是说分布式环境中的各种措施随意破坏，之后观察系统的功能是否可以正常使用。
+ 在15年的纽约的Velocity大会上，Netfilx介绍了他们的Monkey系列软件，跑在AWS上的，能够故意把云环境中的服务搞挂，以此来探测健壮性。试想，这样的软件一旦经常跑，那稳定性的隐患点，应该都能够慢慢发现，但是这也是一种比较悲观的系统思路，认为一切都是不可靠的。

## Netfilx的系列Monkey软件
+ Janitor Monkey
  
  在AWS上运行，寻找那些需要被清理掉的资源，Janitor Monkey认为，任何资源都应该有一定的资源回收或者清理规则。整体工作分为三个步骤，标记、通知然后删除。这样运行之后，应该可以有效的避免云环境中的资源浪费。
 
+ Conformity Monkey
   
  Conformity Monkey是确保云环境中的实例的配置是最佳的，配置的最优达到使用的最优，Conformity Monkey会监测，如果发现一些实例的配置不是最优的，就会发邮件给到实例的owner。
 
 + Chaos Monkey
   
   Chaos Monkey的作用是识别云环境中的服务，然后随机的对他们进行关闭。由于避免对于线上有过大的影响，这个运行的时候一般是特定的时间点和特定的时间段。 可以采取的破坏性措施，例如关闭特定服务接口，关闭特定缓存服务，关闭特定DB服务，增加网络丢包率，增大网络延迟等。


## 相关引用
+ https://github.com/Netflix/SimianArmy/wiki/Chaos-Monkey  
+ http://conferences.oreilly.com/velocity/devops-web-performance-ny-2015/public/schedule/proceedings
+ https://github.com/Netflix/SimianArmy/wiki/The-Chaos-Monkey-Army

## one more thing
后续博文持续在微信的公众账号的第一时间维度，欢迎关注。

![](http://dl2.iteye.com/upload/attachment/0115/7181/a26e120b-b9ce-3a93-addc-24d3044cc56e.jpg)
