---
title: window批处理脚本踩坑记录
tags: 编程
categories: 学习笔记
date: 2023-01-05 13:20:22
---
## 引子
常常会遇上批量修改文件名的需求，平时对于一些简单的需求，比如更换下后缀之类的简单功能，网上copy的代码就能轻松解决，但只要要求稍微复杂点，copy来的代码就基本不能正常完成任务
这次也是为帧动画批量的修改文件名，因为是帧动画的原因，所以需要保证原来的图片顺序是不变。
由此，大概简单浏览了下bat的语法，用法。

## 使用的代码
    echo off
    set a=0
    ::设置前缀
    set qianzui=ts
    setlocal EnableDelayedExpansion
    for %%n in (*.png) do (
    set /a a+=1
    ren "%%n" "%qianzui%-!a!.png"
    echo "!a! :|re|----|%%n|-------|%qianzui%-!a!.png|"
    echo ____________________________________________________________
    )
    pause

## 关键字
### setlocal enabledelayedexpansion
- 启动变量延迟
### echo 打印
- echo off 关闭回显--冗余的显示部分
- echo "内容" 引号不能省略，并且会输出
### set 声明变量
- 使用变量延迟后，使用时需!变量名!
- /a 等待该语句变为数字表达式
### for
- 格式 for %%n(变量名) in (*.png)(遍历对象)(
    (执行语句)
    )
### ren 重命名文件
### pause 暂停
## 问题
- 因为*的遍历顺序，使用遍历时顺序为1，10，11，12，其他数字类比，并不能保证顺序一致
- 莫名其妙的重复执行一次遍历过的对象，第一个文件被修改后，在最后还会被修改一次，而且是随机的
- 如果不深入了解，代码和文件名的命名规则绑定性极高，难复用<span class= "heimu" >最后也是这样解决的</span>

## 有效链接
- https://zhuanlan.zhihu.com/p/125033413
- http://www.bathome.net/index.php


## 结语
直奔python
