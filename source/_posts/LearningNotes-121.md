---
title: 虚幻基本认识
date: 2025-09-22 20:03:46
tags:
    - 工具记录
categories:
    - 学习笔记
---
[虚幻文档](https://dev.epicgames.com/documentation/zh-CN/unreal-engine)
## 虚幻引擎简介
虚幻引擎（Unreal Engine）是一款由Epic Games开发的游戏引擎，广泛应用于游戏开发、电影制作、建筑可视化等领域。虚幻引擎以其强大的图形渲染能力、高度的可扩展性和灵活性而闻名，被广泛用于开发高质量的3D游戏和视觉效果。
## 基本认识
### 文件夹结构（4.27）
- Config
  - 项目配置目录，存放全局配置文件
- Content
  - 核心资源目录，存放项目中所有可编辑的资源（引擎会自动索引该目录下的资源），是开发者日常操作最频繁的文件夹。
- [DerivedDataCache](https://dev.epicgames.com/documentation/zh-cn/unreal-engine/using-derived-data-cache-in-unreal-engine)
  - 引擎缓存目录，存放项目运行 / 编辑过程中自动生成的临时数据，可安全删除（引擎会重新生成）。
- Intermediate
  - 中间文件目录，存放项目运行 / 编辑过程中自动生成的临时数据，可安全删除（引擎会重新生成）。
- Saved
  - 运行时生成文件目录，存放项目运行 / 编辑过程中自动生成的临时数据，可安全删除（引擎会重新生成）。
### 其他
- 左手坐标系
### 蓝图
[基础蓝图节点](https://www.bilibili.com/video/BV1bx4y1x7h8)
[文档](https://dev.epicgames.com/documentation/zh-cn/unreal-engine/specialized-blueprint-visual-scripting-node-groups-in-unreal-engine)
## 设计哲学
[虚幻的GamePlay框架](https://dev.epicgames.com/documentation/zh-cn/unreal-engine/gameplay-framework-in-unreal-engine?application_version=5.6)
[虚幻引擎GamePlay框架理解与应用](https://www.bilibili.com/video/BV1ED4y1D7Sf)
### Actor 
- 具体的逻辑载体
  - 可以拥有组件
- 可互相嵌套
- 网络同步能力
  - 能确保不同客户端间的状态一致
### 组件
- 模块化功能单元
  - 通过组合得到复杂效果


### 其他
- 虚幻的开发范式更强调继承而Unity的开发范式更强调组合
  - 虚幻的核心类型体系是基于继承的，而Unity的基础框架本身就是基于组合的。
  - 虚幻的结构是带有约束感的，但也很大程度上避免了重复造轮子的问题。而unity相反，unity的结构让上手门槛变得很低，但也带来了很多重复造轮子的问题。

## 其他
### Chaos物理系统

### 热更

### UnLua

### VS Code 配置

## 实例 实现FPS Demo
### 需求
1. 基础的角色控制
   1. 移动
   2. 跳跃
   3. 瞄准
   4. 射击
2. 基础的GamePlay交互
   1. 武器切换
   2. 武器开火
   3. 武器装填
   4. HP系统
3. 基础的场景与敌人
   1. 场景
   2. 敌人
      1. 敌人ai
      2. 生成敌人
4. 基础UI
   1. GameePlay UI
      1. 血条
      2. 弹药
      3. 武器
      4. HUD
         1. 准星
         2. 提示文本
   2. 常规UI
      1. 开始菜单
      2. 暂停菜单