---
title: Unity中的坐标系
date: 2024-03-15 14:01:48
categories: 学习笔记
tags:
    - unity
---
# Unity中的几种坐标系

在不同的情况下使用不同的坐标系更加方便，所以在Unity中有多种坐标系：

- 全局坐标系 World Coordinate System
- 局部坐标系 Local Coordinate System
- 屏幕坐标系 Screen Space
- 视口坐标系 ViewPort Space

## 全局坐标系

    全局坐标系是用于描述场景内所有物体位置的方向的基准，也称为世界坐标系。

    在Unity中创建的物体都是以全局坐标系中的坐标原点（0,0,0），来确定各自的位置的。

    可以使用transform.position来获取游戏对象的世界坐标。

## 局部坐标系

    局部坐标系也称为模型坐标系或物体坐标系。

    每个物体都有自身独立的物体坐标系。当物体移动或改变方向时，和该物体相关联的坐标系将随之移动或改变方向。

    模型Mesh保存的顶点坐标均为局部坐标系下的坐标。

## 本地坐标

    transform.localPosition（本地坐标）可以获得物体在父物体的局部坐标系中的位置点。

    父子关系，子物体以父物体的坐标点为自身的坐标原点。

    如果该游戏物体没有父物体，那么    transform.localPosition获得的依然是该物体在全局坐标系中的坐标。

    如果该物体有父物体，则获得是在其父物体的局部坐标系中的坐标。

    检视视图中显示的为localPosition的值。

## 屏幕坐标系

    屏幕坐标系是建立在屏幕上的二维坐标系。

    以像素来定义的，屏幕的左下角为（0,0），右    上角为（Screen.width, Screen.height），z轴的坐标是相机的世界坐标中z轴坐标的负值。

    鼠标位置坐标属于屏幕坐标，通过Input.mousePosition可以获得该位置的坐标。

    手指触摸屏幕也为屏幕坐标，Input.GetTouch(0).position可以获得单个手指触摸屏幕时手指的坐标。

## 视口坐标系

    视口坐标系是将Game视图的屏幕坐标系单位化，左下角（0,0），右上角（1,1）。z轴的坐标是相机的世界坐标中z轴坐标的负值。

# 坐标系之间的关联与相互转换

## 全局坐标系和局部坐标系

### 关联

    transform.Translate(translation:Vector3, relativeTo: Space = Space.Self);

沿着translation的方向移动|translation|的距离，其结果将应用到relativeTo坐标系中。如果relativeTo为空，则默认为局部坐标系。

### 转换

    Transform.TransformPoint(Vector3 position) :将一个坐标点从局部坐标系转换到全局坐标系。

    Transform.InverseTransformPoint(Vector3 position)：将坐标点从全局坐标系转换到局部坐标系。

    Transform.TransformDirection(Vector3 direction):将一个方向从局部坐标系转换到全局坐标系。

    Transform.InverseTransformDirection(Vector3 direction)：将一个方向从全局坐标系转换到局部坐标系。

    Transform.TransformVector(Vector3 vector):将一个向量从局部坐标系转换到全局坐标系。

    Transform.InverseTransformVector(Vector3 vector):将一个向量从全局坐标系转换到局部坐标系。

## 屏幕坐标系与全局坐标系

### 转换

    Camera.ScreenToWorldPoint(Vector3 position): 将屏幕坐标转换为全局坐标。

    Camera.WorldToScreenPoint(Vector3 position):将全局坐标转换为屏幕坐标。

Input.mousePosition：获得鼠标在屏幕坐标系中的坐标。

## 屏幕坐标系与视口坐标系

### 转换

    Camera.ScreenToViewportPoint(Vector3 position)：将屏幕坐标转换为视口坐标。

    Camera.ViewportToScreenPoint(Vector3 position)：将视口坐标转换为屏幕坐标。

## 全局坐标系与视口坐标系

### 转换

    Camera.WorldToViewportPoint(Vector3 position)：将全局坐标转换为视口坐标。

    Camera.ViewportToWorldPoint(Vector3 position)：将视口坐标转换为全局坐标。
