---
layout: post
title:  "JavaEE , Spring take a look at 2016-01"
date:   2016-01-28 12:25:00 +0800
categories: javaee
tags: [javaee, spring]
---

So , 先前工作的關係 , JavaEE跟Spring兩邊都有接觸到 , 所以會比對一下兩邊的狀況.

2015的狀況

* JavaEE
    * 非常仰賴Ap Server.
    * Ap Server 升到JavaEE 7 變多了 , 但Open Source方案依舊是Glassfish,WildFly,Payara沒有被認證但也可以算 [Oracle的列表](http://www.oracle.com/technetwork/java/javaee/overview/compatibility-jsp-136984.html)
    * 台灣用的人依舊不是很多 , 如果要用docker包成micro service也的確有點大.(也許可以用payara micro包看看)
     [Docker build payara micro](http://blog.payara.fish/docker-build-scripts-images-now-available-for-payara-server)
* Spring
    * Spring Boot 的出現解決了Spring 多而繁雜的各種設定 , 也解決了各種版本相依卻不一致的問題.
	
----

其實就兩邊都用到IOC , Web MVC , ORM Framework的狀況下 , 打包成War(or Jar file)的Size都不是很小.
