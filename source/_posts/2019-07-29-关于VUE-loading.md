---
title: 关于VUE-loading
date: 2019-07-29 20:02:14
updated: 2019-08-26 23:30:33
categories:
- 光鲜的前端
- VUE
tags:
- loading
---
想在路由中做一个加载中的动画。  
想了想啊，路由加载能花多长时间，主要是页面加载呐。页面打开时显示加载中，页面加载完成关闭加载中遮罩层。

<!--more-->

方案一：
使用NProgress。
方案二：
使用ElementUI。
考虑到不希望安装新的插件，使用ElementUi。
