---
title: 骨骼动画记录-Godot
date: 2024-11-14 19:40:03
tags: 动画
categories: 学习笔记
---
## 骨骼动画
骨骼动画是一种通过骨骼和关节来控制角色的动画技术，可以使用少量的美术素材完成角色的基本动作。基本上，可以理解成是皮影戏并且套用相关的技巧。

目前骨骼动画的软件有不少，本来在考虑是否需要使用spine,但是考虑到独立开发，使用引擎内自带的骨骼动画来实现基本的需求即可。

以下记录下使用Godot编辑器内的骨骼动画编辑来实现动画的基本步骤和关注点。

[骨骼动画说明](https://docs.godotengine.org/zh-cn/4.x/tutorials/animation/cutout_animation.html#doc-cutout-animation)
[官方文档](https://docs.godotengine.org/zh-cn/4.x/tutorials/animation/2d_skeletons.html#introduction)

## 素材要求
对应皮影戏的道具，基本区分为头部，躯干和四肢六个部分，有必要也可以在腰部将躯干分为两部分，另一方面，可以依赖骨骼动画中带有的权重达到分部位的效果
