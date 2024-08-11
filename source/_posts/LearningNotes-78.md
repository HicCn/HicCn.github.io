---
title: Unity中的刚体、碰撞器与碰撞检测
date: 2024-03-25 11:16:38
categories: 学习笔记
tags:
    - unity
---
## unity的物理系统
    刚体与碰撞器都是Unity的物理引擎下的组件，
## [刚体](https://docs.unity.cn/cn/2021.3/ScriptReference/Rigidbody.html)

## [碰撞器](https://docs.unity.cn/cn/2021.3/ScriptReference/Collider.html)

### 碰撞回调


### isTrigger
isTrigger默认为false表示该物体的碰撞效果会被unity的物理引擎影响，依据速度，质量等因素产生移动，而当isTrigger被设置为true时，碰撞体将不会产生物理碰撞效果，而是会触发触发器事件。当其他物体进入或离开碰撞体的触发器范围时，可以通过编写脚本来检测并响应这些事件。
