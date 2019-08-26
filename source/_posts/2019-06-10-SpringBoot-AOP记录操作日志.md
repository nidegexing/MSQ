---
title: SpringBoot-AOP记录操作日志
date: 2019-06-10 19:47:18
categories:
- 后端的坚持
- SpringBoot
tags:
- 记录日志
- AOP
toc: true
---
## AOP面向切面
我们可以用AOP来做什么？
1 记录重要的操作日志：不用每个方法都要写一遍相同的代码
2 异常的统一处理：同样的，不用对每个类做相同的异常处理，一次就搞定了。
<!--more-->
## SpringBoot中实现AOP记录日志的两个例子
1 配置切点，自定义切点行为
摘自：https://blog.csdn.net/u010096717/article/details/82221263
摘要:
```
@Pointcut("execution(* com.springboot.controller.*.*(..))")
public void Pointcut() {
}
//@Around：环绕通知
@Around("Pointcut()")
public Object Around(ProceedingJoinPoint pjp) throws Throwable {
}
```
2 自定义注解，自定义切点调用注解
摘自：https://blog.csdn.net/textalign/article/details/83863475
摘要：
```
/**
 * 定义切入点，切入点为com.example.aop下的所有函数
 */
@Pointcut("@annotation(com.springboot.aop.MyLog))")
public void myLog() {
}
@Around("myLog()")
public Object doBefore(ProceedingJoinPoint pjp) throws Throwable {
// 计时并调用目标函数
long start = System.currentTimeMillis();
Object result = pjp.proceed();      //真正调用方法
Long usedTime = System.currentTimeMillis() - start;
log.info("USED :" + usedTime);
return result;
}
```
## 后记
采用第一种方法还是第二种方法呢？
本来作为一个偏执者，我采用的是第一种的方式，所有的controller都会自动加入日志，多帅！！
实际上在使用上发现诸多不便：很多请求并不需要记录日志，比如说初始化加载的参数。更多的时候，我们只希望记录重要的日志。
在这样的情况下，使用@Mylog的情况下更自由，我们认为哪个需要记录日志，加一个@Mylog注解就可以了。酷不酷。s/83863475
摘要：
```
/**
 * 定义切入点，切入点为com.example.aop下的所有函数
 */
@Poi