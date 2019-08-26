---
title: Kafka-Zookeeper搭建流数据处理平台
date: 2018-11-04 16:15:26
categories:
- 后端的坚持
- 后端框架
tags:
- Kafa
- ZooKeeper
---
<div>
    <img src="http://bmob-cdn-20430.b0.upaiyun.com/2018/07/13/baa79f934052c05380c9a6246138655b.jpg"
     height="100%" width="100%" title="颜值就是正义" alt="颜值就是正义">
</div>
美女是第一驱动力，我也驱动下我的粉丝儿。
<!--more-->
# 平台适应性说明
这个平台可以用来做什么呢？首先是消息的处理，可以作为通信通道。其次是集群管理，收到消息后，可以自定义负载均衡策略，调用不同的server进行不同的服务处理。
优点是Kafka的高吞吐量，以及离线处理策略。同时zookeeper的服务管理也很易用高效。

## Kafa介绍
Kafka是由Apache软件基金会开发的一个开源流处理平台，由Scala和Java编写。Kafka是一种高吞吐量的分布式发布订阅消息系统，它可以处理消费者规模的网站中的所有动作流数据。
<font color=blue>PS:
概括来说，作为消息队列来使用。消息数据基于文件，消费者上线后可以收到离线的消息。
遗憾的是，查询队列的命令没有搞定。</font>
</br>
## Kafa环境搭建
大牛的笔记：[Kafka_Win教程](https://www.cnblogs.com/alvingofast/p/kafka_deployment_on_windows.html)
1.启动
.\bin\windows\kafka-server-start.bat .\config\server.properties
2.创建Topic：test
kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic testDemo
3.打开一个Producer
kafka-console-producer.bat --broker-list localhost:9092 --topic testDemo
4.打开一个Consumer
kafka-console-producer.bat --broker-list localhost:9092 --topic testDemo
0.90版本之后启动消费者的方法：
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic testDemo --from-beginning
kafka-console-consumer.sh --bootstrap-server mini1:9092 --topic testDemo

## ZooKeeper介绍
ZooKeeper是一个分布式的，开放源码的分布式应用程序协调服务，是Google的Chubby一个开源的实现，是Hadoop和Hbase的重要组件。它是一个为分布式应用提供一致性服务的软件，提供的功能包括：配置维护、域名服务、分布式同步、组服务等。
<font color=blue>PS:
1.作为Kafka环境的基础。
2.管理服务。每个集群启动后，到zookeeper上注册，这样zookeeper就知道谁活着呢。
从而实现集群的管理。需要注意集群间的数据共享问题。</font>
</br>
## ZooKeeper环境搭建
大牛笔记：[Zookeeper_Win教程](https://www.cnblogs.com/xuxiuxiu/p/5868481.html)
1.下载地址
下载地址http://mirrors.cnnic.cn/apache/zookeeper/
2.解压后即可使用
修改/conf目录下的zoo_simple.cfg为zoo.cfg。
3.启动zookeeper
windows下：执行zookeeper-3.4.6\bin >zkServer.cmd
linux下：ookeeper-3.4.6\bin >zkServer.sh start启动
查看是否成功运行：bin/zkServer.cmd  status

[集群](https://blog.csdn.net/my_bai/article/details/68490632)
[Java集成Kafka](https://blog.csdn.net/sgy86/article/details/80497183)
[Java集成ZooKeeper](https://blog.csdn.net/maguanghui_2012/article/details/54583371)
[Spring+ZooKeeper+Kafka](https://blog.csdn.net/qq_37555579/article/details/78944486)
[zookeeper集群](https://blog.csdn.net/u011308691/article/details/51970868)
[真正的Kafka集群](https://www.cnblogs.com/likehua/p/3999538.html)
<font color=blue>PS:
如何搭建集群呢，其实是这样：搭建zookeeper集群作为一个整体。然后每个Kafka的服务的zookeeper.server是集群（3个）。</font>
</br>
[Kafka杂谈](https://blog.csdn.net/wws921104/article/details/72637050/)
https://blog.csdn.net/qq_37555579/article/details/78915088
https://blog.csdn.net/qq_37555579/article/details/78944486
https://blog.csdn.net/jrn1012/article/details/77009025
https://blog.csdn.net/wu18296184782/article/details/80164190

根据Spring框架的API描述，有以下四种方法配置applicationContext.xml文件路径
1. /WEB-INF/applicationContext.xml
2. com/config/applicationContext.xml
3. file:C:/javacode/springdemo/com/config/applicationContext.xml
4. classpath:com/config/applicationContext.xml

[图文并茂的博客](https://blog.csdn.net/L_201607/article/details/81176439)
### 幸运的你
我已经做好了Demo,基于SpringBoot和SpringMvc的都有，请我吃糖果哦，hi hi hi//www.cnblogs.com/likehua/p/3999538.html)
<font color=blue>PS:
如何搭建集群呢，其实是这样：搭建zookeeper集群作为一个整体。然后每个Kafka的服务的zookeeper.server是集群（3个）。</font>
</br>
[Kafka杂谈](https://blog.csdn.net/wws921104/article/details/72637050/)
https://blog.csdn.net/qq_37555579/article/details/78915088
https://blog.csdn.net/qq_37555579/article/details/78944486
https://blog.csdn.net/jrn1012/article/details/77009025
https://blog.csdn.net/wu18296184782/article/details/80164190

根据Spring框架的API描述，有以下四种方法配置applicationContext.xml文件路�