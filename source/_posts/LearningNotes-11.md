---
title: Unity Shader入门精要基础篇笔记 ×
tags: 
    - unity
categories: 读书笔记
date: 2022-11-11 18:10:32
---
## 基础篇目录
1. 欢迎来到 Shader 的世界
2. 渲染流水线
3. Unity Shader 基础
4. 学习 Shader 所需的数学基础

## 基础概念
### 渲染图元
### 视锥体
### 顶点数据
## 渲染流水线
### 什么是渲染流水线
流水线是指将一个行为拆分成多个步骤，每个单元专注于处理某个具体的简单的步骤。对于渲染这一具体行为来说。因为具体步骤的复杂性，我们可以用阶段概况的描述每个阶段渲染流水线都做了些什么。<br>
在《Real-Rendering,Third Edition》中，将渲染流程概况为三个阶段
1. 应用阶段 -产出渲染图元
1. 几何阶段 -产出顶点数据
1. 光栅化阶段

### 应用阶段
这一阶段通常由CPU负责，并且由开发者所主导。这一阶段负责提供渲染过程中所需的数据、资源，并对其优化。具体的，我们需要觉得摄像机位置，场景内物品，视锥体，场景内光源等等。并且剔除掉场景中被遮挡或者因为阴影等原因不可见的物品。对于场景中的物品，我们还要确定它的渲染状态，即材质，纹理，shader等等。
### 几何阶段
这一阶段通常由GPU执行，几何阶段需要将顶点坐标变化到屏幕空间中，并计算相应位置的深度值、着色等相关信息。
### 光栅化
这一阶段同样由GPU执行,它决定了每个渲染图元的哪些像素应该被渲染在屏幕上，根据上一阶段的数据进行插值，逐像素的进行处理。

### CPU与GPU之间的通信
CPU与GPU之间的通信主要发生在应用阶段，这一阶段需要将产出的渲染图元传输给GPU。对于应用阶段，大体可以分为以下三个步骤
1. CPU将数据加载到显存当中
2. 设置渲染状态（调整渲染方法）
3. 调用Draw call