---
layout: post
title:  "How to choose a service"
date:   2016-02-20 22:33:00 +0800
categories: service
tags: [service]
---

Micro-Service 的關係，現在建置一個系統常會用到各種現成的組合，例如Message Queue server,Eip,Mail Service,Log service,... 
紀錄目前為止的評選要點

1. Containize
2. Open Source 
3. 本身RESTful Service 的齊全度
4. 本身Api的支援度

Containize 攸關DevOpts的媒合度及Service的可操作性、可複製性。一個Containize的Service可以在最方便及最短的時間內被啟動。並且最可能直接被雲端服務支援。
最好在Docker hub有出現相關的Image。

Open Source現今的成熟度及方便性已經遠超過好幾年前的情況，相同性質的服務，一個成熟的OpenSource專案更容易得到比商業專案更多的支援。

RESTful Service 的 支援度則有關該系統與其它系統的整合性。
