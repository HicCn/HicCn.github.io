---
title: 游戏的一致性
date: 2024-03-20 10:19:39
tags:
    - 游戏开发
---
## 为什么要重视一致性
重视一致性意味着在游戏开发初期对游戏已经具有了初步的全局思考。对于一个完整的游戏
应该做到：
- 玩法设计的一致性,盲目的缝合往往会让玩家出现主次不分明的游戏目标，与行为不一致的游玩思路。
- 美术风格的一致性
- 音乐音效的一致性
- 故事情节的一致性
- 开发脚手架与资源管理的一致性

## 素材的显示规则
- unity单位
  - Unity 项目中使用的单位大小。默认情况下，1 个 Unity 单位为 1 米（100像素）。要使用其他缩放比例，请在导入资源时在 Import Settings 中设置 Scale Factor 选项。
- 摄像机的Size
  - 对于正交摄像机，Size的大小就表示了屏幕高度的一半有多少个**unity单位**
- 素材的Pixels Per Unit(PPU)
  - 一个**unity单位**显示对应图片的多少像素
- UI：Canvas的RenderModel
  - Screen Space - Overlay（屏幕空间 - 覆盖）：在这种模式下，Canvas 会被渲染在屏幕上，并覆盖在场景中的其他元素之上。UI 元素将始终显示在最顶层，不会随着场景中相机的移动而改变位置。这种模式适用于大多数常见的 2D UI 布局，如菜单、按钮等。
  - Screen Space - Camera（屏幕空间 - 相机）：
    这种模式下，Canvas 会被渲染在屏幕上，但是会与一个指定的摄像机相对应。Canvas 的位置和尺寸会随着相机的视野变化而改变，可以通过设置 Canvas 的 Plane Distance 属性来调整 Canvas 和相机之间的距离。这种模式适用于需要 UI 元素随着相机移动或缩放而变化的情况。
  - World Space（世界空间）：
  在这种模式下，Canvas 会被视为场景中的一个普通 3D 对象，可以在场景中自由定位、旋转和缩放。UI 元素会随着 Canvas 的变换而改变位置，也会受到场景中光照和阴影的影响。这种模式适用于需要在 3D 空间中展示 UI 元素的情况，比如在游戏中的交互式 3D UI 或者虚拟现实场景中的 UI 呈现。
