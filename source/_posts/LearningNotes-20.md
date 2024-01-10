---
title: 多线程概述与unity中的协程
tags: 
    - 编程
    - unity
categories: 学习笔记
date: 2022-11-16 04:02:54
---


## 什么是线程
线程是CPU进行调度计算的基本单位

## 操作系统中的进程
进程是操作系统中一个正在执行的应用实体
### 时间片
操作系统虽然提供了多任务的能力，但对于CPU的运算来说，它仍然是单任务的，所以有了时间片这一概念
> 在时分操作系统中，系统分配给每一个运行中的进程在CPU中的一小段微观时间。

在宏观上：我们可以同时打开多个应用程序，每个程序并行不悖，同时运行。但是在微观上：由于只有一个CPU，一次只能处理程序要求的一部分，如何处理公平，一种方法就是引入时间片，每个程序轮流执行。
## 什么是多线程
多线程就是协调多个线程共同执行一个进程的能力。

## 为什么会有多线程
- 多线程能降低计算资源的浪费    
- 多线程是一种更好的分配任务的方式
- 对于程序的编写来说，多线程使程序的层次更加清晰


## 线程间的通信
对于操作系统来说，每个线程都有属于自己的栈空间，如果每个线程都是独立的工作，那就会造成资源的浪费，所以我们需要为线程之间制定好规则，而规则奏效的前提就需要线程间的相互通信。一般的我们可以有以下方式实现线程间的通信
- 共享内存
- 消息传递
- 管道流
## 进程间通信
应用实体的通信方式一般有以下几种
- socket
- 共享文件
- 消息队列
- 间接通信（如通过数据库或邮箱通信）

## 使用时的问题

1. 当A进程/线程在等待B进程/线程释放资源时，B进程/线程同样在等待A进程/线程。则在无外部作用的情况下，A/B两进程或线程都将永远无法进行下去。
    - 形成死锁的四个必要条件是什么
        |||
        |---|---|
        |互斥条件|线程(进程)对于所分配到的资源具有排它性，即一个资源只能被一个线程(进程)占用，直到被该线程(进程)释放|
        |请求与保持条件|一个线程(进程)因请求被占用资源而发生阻塞时，对已获得的资源保持不放。|
        |不剥夺条件|线程(进程)已获得的资源在末使用完之前不能被其他线程强行剥夺，只有自己使用完毕后才释放资源。|
        |循环等待条件|当发生死锁时，所等待的线程(进程)必定会形成一个环路（类似于死循环），造成永久阻塞|

## 协程与unity中的协程
协程完全由用户控制，可以理解为一种可以暂停的函数，基于这一概念，unity可以将一个任务分配到多个帧里去执行，即在主函数完成全部内容后暂停协程，在下一帧中继续执行。

### 原理
Unity协程的实现基本原理是利用了迭代器。