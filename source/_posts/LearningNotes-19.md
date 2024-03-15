---
title: Unity中脚本的生命周期
tags:
  - unity
categories: 学习笔记
date: 2022-11-16 04:01:16
---

## MonoBehaviour类
>[unity介绍文档](https://docs.unity.cn/cn/2021.1/Manual/class-MonoBehaviour.html)
>[unity细节文档](https://docs.unity.cn/cn/2021.1/ScriptReference/MonoBehaviour.html)

MonoBehaviour是Unity中用于实现游戏对象行为的组件基类，所有游戏对象的行为都是派生自MonoBehaviour的子类，该类包含多个内建函数可用于实现对象的行为。

## 执行顺序
>[unity文档](https://docs.unity3d.com/cn/current/Manual/ExecutionOrder.html)

{%  image
    url="/assets/images/post/pos19-1.png"
    title="脚本生命周期流程图"
%}