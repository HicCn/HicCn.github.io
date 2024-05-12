---
title: unity-资源加载简介
tags: 
    - 编程
    - unity
categories: 学习笔记
date: 2022-12-06 11:38:37
---

## Unity中常见的资源加载方式
### [Resources](https://docs.unity.cn/cn/2020.2/ScriptReference/Resources.html) 文件夹：
Resources是一种比较简单的资源加载方式，只需要将资源放入Resources文件夹，就可以通过路径进行加载。但是Resources 需要在游戏开始时将资源加载进内存，这往往需要一定的加载时间，并造成内存浪费，所以Resources适合于小型的项目或一些原型demo，对于大型项目来说是灾难的。

### [AssetBundle](https://docs.unity.cn/cn/2021.1/Manual/AssetBundlesIntro.html)：
AssetBundle 实际上是一个压缩文件，包含了资源的二进制数据和元数据信息，Unity 在加载 AssetBundle 时会解压缩并加载其中的资源。
AssetBundle以数据包为单元动态的加载资源（需要注意的是，数据包直接往往会出现复杂的相互引用，同样会导致大量不需要的ab包加载进内存，所以往往需要严格的隔离不同包中的数据，有时可能出现相同资源在不同数据包中各一份的情况）

### 通过网络：
对于某些应用场景需要用到网络对资源进行更新，如网络游戏中场景的热更新或者是展示玩家的UGC内容等。

