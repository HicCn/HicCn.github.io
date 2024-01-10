---
title: Unity动画使用备忘
tags: unity
categories: 学习笔记
date: 2023-02-28 09:50:38
---
## 创建动画

选中需要添加Animation的对象，通过ctrl+6打开创建面板，创建动画。

## 

## 常用类

- Animator：动画控制器，控制Mecanim动画系统的接口，用来管理多个动画；

- Animation：用于播放动画，老版中单独的一个Animation也可以完成动画的播放和切换，不过状态切换之类的需要程序猿代码控制。在新版中，状态管理部分交给了Animator；

- AnimationClip：动画剪辑片段，储存基于关键帧的动画，是用于Animation来播放动画；

- AnimationState：动画状态，用来改变单一动画的播放速度、权重、时间、层级、播放Mode，以及混合模式；

- AnimationEvent：动画事件，用于某种条件下触发自定义函数；

- StateMachineBehaviour： 动画状态机管理器拓展类，脚本继承了该类之后，绑定到Animator上某State上面。当状态发生变化，可以重载响应函数。类似 触发器的响应函数；

>单独使用Animation（老版）可以移动位置等，但是就是不能播放sprite，但是使用Animator就可以播放Sprite。这应该是Unity的bug。