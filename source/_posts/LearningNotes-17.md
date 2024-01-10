---
title: C#编译过程与Mono运行环境 
tags: 
    - C#
    - 编程
    - unity
categories: 学习笔记
date: 2022-11-16 03:21:55
---
>[CLR](https://learn.microsoft.com/zh-cn/dotnet/standard/clr)


## 运行时与编译时
>https://blog.lishunyang.com/2021/07/compile-time-and-runtime.html
>https://www.zhihu.com/question/20607178
运行时与编译时是一种概念
- 运行时编译：运行时编译是一种延迟编译，它把代码翻译成机器指令在应用程序运行时才发生。

- 编译时编译：编译时编译是一个早期的准备步骤，它会在应用程序被部署之前就将代码转换成机器指令。

## C#的编译过程
>https://www.cnblogs.com/May-day/p/6594574.html

{%  image
    url="/images/post/pos17-1.png"
    title="C#编译流程"
%}


## Momo
>https://www.cnblogs.com/zhangchui/articles/4086042.html

   Mono是一个软件平台，设计用来允许开发者轻松地创建跨平台应用程序。他是微软.Net框架的开源实现，基于C#的ECMA标准和公共语言运行时（CLR）。我们认为通过一个优秀的标准的软件开发平台，可以降低在Linux环境下开发优秀程序的门槛。

### unity和Momo

## CoreCLR 关于unity未来的.NTE开发
[说明](https://developer.unity.cn/projects/62bbc040edbc2a7848d45ae8)
[社区论坛讨论](https://forum.unity.com/threads/unity-future-net-development-status.1092205/)

### IL2CPP
[官方文档](https://docs.unity.cn/cn/2019.4/Manual/IL2CPP.html)
