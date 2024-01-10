---
title: unity工具开发
tags: 
    - 编程
    - unity
categories: 学习笔记
date: 2022-12-09 11:28:00
---

## 需求
因为需要调整项目中的重复资源，需要工具查找资源的引用，需要开发一个unity工具。

## Editor文件夹
unity中有一些特殊的文件夹
- Editor
- Plug-ins
- Resources
- StreamingAssets
- ...（[完整目录](https://docs.unity3d.com/cn/current/Manual/SpecialFolders.html)）

在Unity中，Editor文件夹通常用于存储项目中用于编辑器扩展的脚本。这些脚本可以提供自定义工具来帮助您管理游戏项目或更改编辑器的外观和行为。

## 创建启动菜单项

    using UnityEngine;
    using UnityEditor;

    public class test : MonoBehaviour
    {
        [MenuItem("MyMenu/Do Debug")]
        static void DoDebug()
        {
            Debug.Log("测试");
        }
    }

### 分析：
- [MenuItem("MyMenu/Do Debug")]，这个Attribute需要引用UnityEditor的命名空间。用处是，给菜单栏提供一个自定义的选项。
- "MyMenu/Do Debu"是菜单的路径，当然你也可以添加到默认的菜单中如"Component/UnitEditor"
- static void DoDebug(){...}为点击该选项后的调用函数，需注意一点，该函数必须是静态的。

## 效果

{%  image
    url="/images/post/post40-1.png"
    title="菜单效果"
%}
{%  image
    url="/images/post/post40-2.png"
    title="点击效果"
%}

### 补充
[MenuItem("MyMenu/Do Debug")]也可以指定某一文件夹
如[MenuItem("Assets/Do Debug")]
{% image
    url = "images/post/post40-2.png"
    title = "菜单效果"
%}

## meta文件
每个资源都会生成一个对应的meta资源

### meta资源的作用
1. 是用于辅助管理Unity资源文件的文件，Unity根据meta里记录的GUID来区分项目中的不同资源；
2. meta还记录了一些对应资源的非常重要的信息，比如：各个资源Inspector的信息等。

### 理解
在游戏场景中引用一个游戏资源，Unity并不直接按照文件路径和名称，而是使用一个独一无二的GUID来指向工程里的该资源文件。这个GUID储存在Unity工程为每个资源和文件夹生成的Meta文件里。 

使用GUID的好处就是，即使你移动、重命名或者修改资源的内容，这个资源仍然可以通过GUID来被引用（只要GUID不变，资源就能够被引用）。

缺点是你必须明确的意识到Meta文件是被关联到特定的资源上的，如果你删除了一个meta文件，Unity会认为原始的资源文件已经被删除，然后为这个“新的”资源文件生成一个新的GUID。这就是游戏场景中的资源引用中断的最常见原因。 

除了GUID，meta文件还存储了有关资源导入的信息。例如，贴图资源在导入时可以当作标准贴图、法线贴图、GUI贴图、cookie或者光线贴图。这些导入设置都会被存储在meta文件里。 


### GUID
在 Unity 中，meta 文件中的 GUID 是一个字符串，它用于标识一个游戏资源的唯一性。通常，每个游戏资源都会有一个唯一的 GUID，它由 Unity 自动生成，并存储在该资源的 meta 文件中。

GUID 有多种用途。首先，它可以用于标识游戏资源的唯一性。例如，如果你有多个相同的模型，你可以通过查看它们的 GUID 来区分它们。此外，GUID 还可以用于管理游戏资源之间的依赖关系。例如，如果一个脚本依赖于另一个脚本，那么它们之间的依赖关系就会存储在 meta 文件中，并使用 GUID 来标识相关的脚本。

所以我们可以通过 AssetDatabase.LoadAssetAtPath 的方法来根据资源的 GUID 加载指定的游戏资源，而不需要手动指定资源的路径。



## unity工具类

### Selection
Selection 是 Unity 中的一个静态类，它提供了一组方法和属性，用于处理选择的对象。通常，开发人员会使用 Selection 类来获取选择的对象的信息，并执行特定的操作。[官方文档](https://docs.unity.cn/cn/current/ScriptReference/Selection.html)

利用Selection.assetGUIDs我们可以通过选中获得所选资源的GUID。

### AssetDatabase
AssetDatabase是一个静态类，用于提供对Unity项目中的资源的访问和操作。它提供了一系列方法，可以用来查找、加载和保存项目中的资源，还可以用来对项目进行重新导入和构建。[官方文档](https://docs.unity.cn/cn/2018.4/Manual/AssetDatabase.html)

我们可以通过AssetDatabase.GetAllAssetPaths()来获得unity中所有资源的路径，通过比对输出引用了被查找资源的资源。

## 完整思路

1. 我们先通过Selection.assetGUIDs得到返回所选资源的 GUID。
1. 调用AssetDatabase.GetAllAssetPaths()得到项目中全部资源的路径。
1. 对全部资源逐个处理，如果是目标类型的文件，通过File.ReadAllText读取文件内容，通过IndexOf判断文件中是否出现对应GUID，如果是则输出路径。

