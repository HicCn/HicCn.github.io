---
title: Unity Profiler性能检测
tags: 
    - Unity
    - 编程
categories: 学习笔记
date: 2022-11-10 23:57:36
---
## 性能指标
对性能的评估是一个科学的过程，要判断性能的好坏首先就是要确定性能指标。一般的我们可以关注内存用量，CPU使用率，GPU使用率，并发数目等项目，确定设备的最大化的支持数，分析数据以确认性能瓶颈。对于游戏的性能瓶颈，多半是由CPU过载、运行时峰值、内存访问速度慢、内存碎片、垃圾回收、GPU填充速率差或者内存带宽造成的。
</br>
在游戏开发中，我们一般期望游戏帧数能保持在60帧以上。

## 基本性能分析模块
|性能分析器模块	|功能|
|---|---|
|CPU Usage|	概要显示应用程序在哪些方面花费最多时间（涉及物理、脚本、动画和垃圾收集等多个方面）。该模块包含有关应用程序的大量性能分析信息，您可以使用这些信息来决定进一步使用哪些其他模块来调查应用程序中的更具体问题。该模块始终处于激活状态（即使您将其关闭）。请参阅 [CPU Usage Profiler 模块](https://docs.unity.cn/cn/2019.4/Manual/ProfilerCPU.html)|
|GPU Usage|	显示与图形处理有关的信息。默认情况下，此模块处于非激活状态，因为它的开销较大。请参阅 [GPU Usage Profiler 模块](https://docs.unity.cn/cn/2019.4/Manual/ProfilerGPU.html)。|
|渲染	|显示有关 Unity 如何在应用程序中渲染图形的信息，包括有关静态和动态批处理、SetPass 和 Draw 调用、三角形和顶点的信息。请参阅 [Rendering Profiler 模块](https://docs.unity.cn/cn/2019.4/Manual/ProfilerRendering.html)。|
|Memory	|显示有关 Unity 如何在应用程序中分配内存的信息。这尤其适合用于查看脚本分配 (GC.Alloc) 如何引起垃圾收集或者是应用程序的资源内存使用量随时间变化的趋势。请参阅 [Memory Profiler 模块](https://docs.unity.cn/cn/2019.4/Manual/ProfilerMemory.html)。|
|Audio	|显示应用程序中的音频相关信息，例如何时播放音频源以及播放的音频源数量、音频系统需要的 CPU 使用率以及 Unity 为其分配的内存量。请参阅 [Audio Profiler 模块](https://docs.unity.cn/cn/2019.4/Manual/ProfilerAudio.html)。|
|Video	|显示应用程序中的视频相关信息。请参阅 [Video Profiler 模块](https://docs.unity.cn/cn/2019.4/Manual/profiler-vide-profiler-module)。|
|Physics	|显示应用程序中物理引擎已进行的物理处理的相关信息。请参阅 [Physics Profiler 模块](https://docs.unity.cn/cn/2019.4/Manual/ProfilerPhysics.html)。|
|Physics (2D)	|与 Physics Profiler 模块类似，此模块显示应用程序中物理引擎已进行的 2D 物理处理的相关信息。|
|Network Messages|（已弃用）	显示有关多玩家高级 API 发送或接收的较低级数据包和消息的信息。注意：多玩家高级 API 已被弃用。|
|Network Operations|（已弃用）	显示有关多玩家高级 API 发送和接收的消息中含有哪些类型或操作的详细信息，例如已传输的 SyncVar 或命令的数量。注意：多玩家高级 API 已被弃用。|
|UI	|显示有关 Unity 如何为应用程序处理 UI 批处理的信息，包括 Unity 为何以及如何对项目进行批处理。请参阅 [UI Profiler 模块](https://docs.unity.cn/cn/2019.4/Manual/ProfilerUI.html)。|
|UI Details|	与 UI 模块类似，此模块的图表添加有关批处理和顶点计数的数据，以及标记（包含有关触发 UI 变化的用户输入事件的信息）。|
|Global Illumination	|显示有关 Unity 在应用程序中的全局光照 (Global Illumination) 光照子系统中花费的 CPU 资源的信息。请参阅 [Global Illumination Profiler 窗口](https://docs.unity.cn/cn/2019.4/Manual/ProfilerGI.html)。|

## 性能分析模块自身的性能开销
某些性能分析器模块具有大量的数据收集开销，例如 GPU、UI 和 Audio Profiler 模块。为了防止这些模块影响应用程序的性能，可以通过在 Profiler Module 下拉选单中取消选择这些模块来将它们停用。这样可从窗口删除模块，让性能分析器停止收集该模块的数据，并减少性能分析器的开销。

这不适用于 CPU Usage 模块，该模块始终会收集数据（即使该模块处于非激活状态），因为其他模块依赖这些数据。

要添加模块，请选择 Profiler Module 下拉选单，然后选择要激活的性能分析器。从下拉选单选择性能分析器模块后，这个模块开始收集数据，但是在非激活时段内不显示任何数据。

## 具体的使用
当我们单击波形图上的任意一点时，游戏会暂停下来，并且为我们显示这一帧所执行的内容。
有三种显示方式

|视图	|功能|
|---|---|
|Timeline|	显示特定帧的时间细分信息，以及该帧长度的时间轴。只有在此视图模式中才可以一次性查看所有线程上的时间以及在帧内运行线程的时间，因此可以关联各个线程的时间（例如作业系统工作线程在主线程上的系统调度这些线程之后启动）。|
|Hierarchy|	按时间数据的内部层级结构对这些数据分组。此选项以降序列表格式显示应用程序调用的元素，默认按花费的时间排序。还可以按分配的脚本内存量 (GC Alloc) 或调用次数对信息进行排序。要更改用于对表进行排序的列，请单击该表列的标题。|
|Raw Hierarchy	|以类似于发生计时的调用栈的层级结构显示时间数据。Unity 在此模式中单独列出每个调用栈，而不是像在 Hierarchy 视图中一样将它们合并。|

### profiler的脚本控制
我们可以通过静态的Profiler类在脚本代码中控制Profiler。具体的方法可以查阅[unity Profiler说明文档](https://docs.unity.cn/cn/2020.3/ScriptReference/Profiling.Profiler.html)但最重要的方法就是
|方法|功能|
|---|---|
|BeginSample|开始使用自定义标签分析一段代码。|
|EndSample	|结束当前的性能分析样本。|

### Deep Profiling
使用Unity Profiler开启DeepProfile模式以后，可以看到很多函数的具体消耗和GC情况，包括调用栈这些信息，有了这些信息再对症下药的话优化的效果是很明显的。但是在Editor下开启DeepProfile模式采集到的的数据通常是不准确的，一般我们要在真机上开启DeepProfile模式采集数据。

## 真机调试
待更