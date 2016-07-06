---
layout: post
title:  "Devops Summit 2016心得"
date:   2016-07-06 23:22:00 +0800
categories: service
tags: [service]
---


以下為筆記

----

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
