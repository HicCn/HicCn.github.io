---
title: 简单了解Unity
tags: 
    - 编程
    - Unity
categories: 学习笔记
date: 2022-11-16 04:10:00
---
## unity的特殊文件夹
> [官方文档](https://docs.unity3d.com/cn/current/Manual/SpecialFolders.html)
>https://docs.unity3d.com/cn/current/Manual/AssetDatabase.html
>https://docs.unity3d.com/cn/current/Manual/ScriptCompileOrderFolders.html

### Assets
Unity工程中所用到的所有Asset都放在该文件夹中，是资源文件的根目录，很多API都是基于这个文件目录的，查找目录都需要带上Assets，比如AssetDatabase。

### Library
Unity会把Asset下支持的资源导入成自身识别的格式，以及编译代码成为DLL文件，都放在Library文件夹中。

### ProjectSettings
编辑器中设置的各种参数

下面都是存在Assets目录下的文件的了。

### Editor
为Unity编辑器扩展程序的目录，可以在根目录下，也可以在子目录下，只要名字叫“Editor”，而且数量不限。Editor下面放的所有资源文件和脚本文件都不会被打进包中，而且脚本只能在编辑器模式下使用。一般会把扩展的编辑器放在这里，或只是编辑器程序用到的dll库，比如任务编辑器、角色编辑器、技能编辑器、战斗编辑器……以及各种小工具。

### Editor Default Resources
名字带空格，必须在Assets目录下，里面放编辑器程序用到的一些资源，比如图片，文本文件等。不会被打进包内，可以直接通过EditorGUIUtility.Load去读取该文件夹下的资源。

### Gizmos
Gizmos.DrawIcon在场景中某个位置绘制一张图片，该图片必须是在Gizmos文件夹下。
void OnDrawGizmos() {
Gizmos.DrawIcon(transform.position, “0.png”, true);
}
OnDrawGizmos是MonoBehaviour的生命周期函数，但是只在编辑器模式下每一帧都会执行。Gizmos类能完成多种在场景视图中绘制需求，做编辑器或调试的时候经常会用到，比如在场景视图中绘制一条辅助线。（用Debug.DrawLine，Debug.DrawRay也可以绘制简单的东西）

### Plugins
该文件夹一般会放置几种文件，第三方包、工具代码、sdk。
plugin分为两种：Managed plugins and Native plugins
Managed plugins：就是.NET编写的工具，运行于.NET平台（包括mono）的代码库，可以是脚本文件，也可以本身是DLL。NGUI源码就放在该文件夹下面的。
Native plugins：原生代码编写的库，比如第三方sdk，一般是dll、so、jar等等。
该文件夹下的东西会在standard compiler时编译（最先编译），以保证在其它地方使用时能找到。

### Resources
存放资源的特殊文件夹，可以在根目录下，也可以在子目录下，只要名字叫“Resources”就行，比如目录：/xxx/xxx/Resources 和 /Resources 是一样的，而且可有多个叫Resources的文件夹。Resources文件夹下的资源不管用还是不用都会被打包进.apk或者.ipa，因为Unity无法判断脚本有没有访问了其中的资源。需要注意的是项目中可以有多个Resources文件夹，所以如果不同目录的Resources存在同名资源，在打包的时候就会报错。
Resources中全部资源会被打包成一个缺省的AssetBundle（resources.assets）。
在该文件夹下的资源，可以通过Resources类进行加载使用。API地址

### Standard Assets
存放导入的第三方资源包。

### StreamingAssets
该文件夹也会在打包的时候全部打进包中，但它是“原封不动”的打包进去（直接拷贝到的包里）。游戏运行时只能读不能写。
不同的平台最后的路径也不同，可以使用unity提供的Application.streamingAssetsPath，它会根据平台返回正确的路径，如下：
Mac OS or Windows：path = Application.dataPath + “/StreamingAssets”;
IOS：path = Application.dataPath + “/Raw”;
Android：path = “jar:file://” + Application.dataPath + “!/assets/”;
我们一般会把初始的AssetBundle资源放在该文件夹下，并且通过WWW或AssetBundle.LoadFromFile加载使用。

### Hide Assets
隐藏文件夹和文件
以".“开头
以”~“结尾
名字为"cvs”
扩展名为".tmp"