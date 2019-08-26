---
title: Spring整合Quartz动态任务
date: 2019-07-20 15:01:45
categories:
- 后端的坚持
- 学习笔记
tags:
- Quartz
---
案例一：https://segmentfault.com/a/1190000016554033
案例二：https://www.cnblogs.com/dauber/p/9466502.html
案例二CODE：https://github.com/zt1115798334/springboot-quartz.git
<!--more-->
### Quartz基本概念
1. Job 表示一个工作，要执行的具体内容。此接口中只有一个方法，如下：
```java
void execute(JobExecutionContext context) 
```
2. JobDetail 表示一个具体的可执行的调度程序(与Scheduler是N:1关系，与Trigger是N:Nguanxi )，Job 是这个可执行程调度程序所要执行的内容，另外 JobDetail 还包含了这个任务调度的方案和策略。   
3. Trigger 代表一个调度参数的配置，什么时候去调(与Scheduler是N:1关系)。 
4. Scheduler 代表一个调度容器(基本单位1)，一个调度容器中可以注册多个 JobDetail 和 Trigger。当 Trigger 与 JobDetail 组合，就可以被 Scheduler 容器调度了。   
### Quartz动态调度
案例:https://blog.csdn.net/xiang__liu/article/details/82389210
### 我的Demo
代码：https://github.com/kaola-horde/TeaHouse/tree/master/SpringBoot/QuartzDemo
笔记：还没总结




9466502.html
案例二CODE：https://github.com/zt1115798334/springboot-quartz.git
<!--more-->
### Quartz基本概念
1. Job 表示一个工作，要执行的具体内容。此接口中只有一个方法，如下：
```java
void execute(JobExecutionContext context) 
```
2. JobDetail 表示一个具体的可执行的调度程序(与Scheduler是N:1关系，与Trigger是N:Nguanxi )，Job 是这个可执行程调度程序所要执行的内容，另外 JobDetail 还包含了这个任务调度的方案和策略。   
3. Trigger 代表一个调度参数的配置，什么时候去调(与Scheduler是N:1关系)。 
4. Scheduler 代表一个调度容器(基本单位1)，一个调度容器中可以注册多个 JobDetail 和 Trigger。当 Trigger 与 JobDetail 组合，就可以被 Scheduler �