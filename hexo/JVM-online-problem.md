---
title: JVM线上问题快速排查
date: 2017-09-29 21:15:00
description: "JVM线上问题快速排查"
categories: [Java]
tags: [Java,JVM]
---

## 找到最耗CPU的线程 ##

----------


### 步骤一:找到最耗CPU的进程

 - 执行top -c, 显示进程运行信息列表
 - 输入 P(大写p), 进程按照CPU使用率排序


### 步骤二:找到最耗CPU的线程

 - top -Hp `pid`,显示一个进程的线程运行信息列表
 - 输入 P(大写p), 进程按照CPU使用率排序

### 步骤三:将线程PID转化为16进制
```shell
printf "%x\n" 1234
4d2
```
*之所以要转化为16进制，是因为堆栈里，线程id是用16进制表示的*

### 步骤四:查看堆栈，找到线程在干嘛
```shell
jstack 11183 | grep '4d2' -C19 --color
```


----------
## 找到最耗内存对象 ##
```shell
jmap -histo:live 11183 | more 
```

 - #instances 实例数
 - #bytes 所占内存大小
 - class name 类名


----------
## 查看内存分配 ##
```shell
jmap -heap 11183
```


----------
