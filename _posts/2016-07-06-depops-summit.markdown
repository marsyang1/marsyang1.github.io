---
layout: post
title:  "Devops Summit 2016心得"
date:   2016-07-06 23:22:00 +0800
categories: summit
tags: [summit]
---

心得:
有時候看著台人的人開心的演講 ， 真的是滿羨慕的 。 畢竟台中有這樣的環境跟能接受這樣文化的機會實在很少。
要推動一些內部優化的工作也是困難重重....

Kubernetes講者非常熟練的在台上非常炫Demo了一輪 ， 雖然Kubernetes本身不太好安裝 ， 但顯然
所提供的各種功能的確是滿貼近Production會遇到的各種狀況 ，畢竟Production本來就什麼事情都有可能發生.
有一個可以支持各種狀況的Service是還滿重要的.另外講者順便Demo了MicroService的部分也是很受用.

從限制理論看Devops也是非常有趣的題目，如同上面所說，推動Devops或者Agile之類的 ， 最容易遇到的是
文化的衝擊跟工具的選擇 。 工具的選擇好解決 ， 但文化的衝擊...人跟人之間的問題往往是最難處理的。

ELK平台的部分就已經聽過滿多次了 ，只是想說加減聽聽別人怎用的  ， 另外聽到搭配RabbitMQ也是不錯的Idea.

Agile的推動直接舉實例說明也是滿不錯的 ， 但這也是有文化的衝擊問題.

Monitoring的部分也滿重要的 , 其實在玩過container之後 , 還滿明顯的可以提會到.
Monitor不太可能再依賴單一語言提供的解決方案 , 會需要可以吃進支援各種Ap Server來源 ,
並且還要夠彈性的方案. 不過我之前評估到後來是先用icinga2就是了 , 因為比較簡單也好架.

https://www.icinga.org/products/icinga-2/

Debug by counter 也是滿有趣的.
講者提到其實國外滿多Production Code裡面也埋滿多Debug Code 來handle各種錯誤.
Production的好壞跟Code Robust有關係.如果Production可以應付各種Exception的話,
使用者的體驗會比較好.所以如果在effort不大的情況增加Code Robust是滿重要的議題.

----

以下為筆記

Kubernetes

* 盲人摸象
* Google - SRE - Site Reliabity Engineering
	* 50% on Engineering Work
	* Automation
	* Create tool for developer
* config.properties to Google Work Master , code to Repo , work Master to deploy
* Kubernetes
	* like Google work master.
	* config to Kubernetes.
	* Guestbook UI => HelloService (deploy)
	*    |         => GuestBook Service (deploy)
	*   redis            |
	*                  MySQL
* saturnism/spring-boot:1.2.3
* gcp push to google
* kubectl run .....
* kubectl scale deployment ....
* kubectl delete pod
* pod 共生死
* kubectl expose deployment  ==> Service HA
* Rolling update
	* kubectl edit deployment
	* kubectl rollout history
* 可結合 Jenkins 作部署 and rolling update
* fabric8
	* auto setup jenkins ... e.g. depopts service

ELK

* logstash => E => K
           => StatD => G
           => E Watch
* 60G log => 8台 * 1台24G  , 5台RabbitMQ
* 滿吃記憶體
* 可搭配RabbitMQ作第一道收集
* log 留2個月 , 超過存到S3 用 AWS
* 跑Program 排成刪除
* 還滿多人用的......
* 真的有人遇到掉包問題.....用RabbitMQ可以解決掉包

Docker file vs CM

* Docker file
	* Easy to use , hard to maintain , extend
* Packer
	* tool for createing image
	* https://www.packer.io
* Kubernetes 難設定 , 可用GCP比較快
* AWS 可新增Tag KubernetesCluster
* Jenkins Job DSL -> Seed DSL設定  => Jenkins Job

Monitoring

* 風險管臉用

大陸

* shadowsocks
* shadowsocks-rss => docker
* 80 , 8080 , 443預設封鎖 , 要申請備案
* 公信部
* 一般備案個人拿台胞證也可以申請
* domain 一定要有ICP證書
* 經營式網站 => 需要線上付錢 => 要企業 , 中資100萬RMB
* 公安部

Counter

* 用Counter可以解決95%的問題
* 自行定義warn error的界線
* Code簡單
* 國外很多產品也埋很多counter
* 比單純用log 的effort來得小
