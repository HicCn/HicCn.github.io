---
title: Web端游戏
date: 2024-04-30 14:58:41
tags:
    - 开发通识
---

## 浏览器基本认识

### 浏览器内核

- 渲染引擎：负责将HTML、CSS、JS代码渲染成最终的图像，并展示在屏幕上
- JS引擎：负责解析和执行JS代码


## web端如何渲染游戏画面
1. Canvas API：

- Canvas是HTML5提供的一种绘图API，允许通过JavaScript来绘制2D图形和动画。
游戏开发者可以使用Canvas API在HTML文档中创建一个画布元素，然后通过JavaScript在画布上绘制游戏场景、角色和动画。
- Canvas虽然能够实现简单的游戏，但对于复杂的游戏可能性能和渲染效果会受到限制。
WebGL：

2. WebGL是一种基于OpenGL ES的JavaScript API，用于在浏览器中渲染3D图形。
- 游戏开发者可以使用WebGL来创建复杂的3D游戏，利用GPU加速来实现更高的渲染性能。
WebGL可以直接访问GPU，因此可以在浏览器中实现更复杂的游戏画面和效果，例如实时光影、粒子效果等。