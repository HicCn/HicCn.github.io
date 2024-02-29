---
title: Unity Shader类概述
tags: 
    - unity
    - 编程
categories: 学习笔记
date: 2022-11-16 14:04:04
---
>关联文章[Unity Shader入门精要基础篇笔记](/2022/11/11/LearningNotes-11/)
## 什么是Shader
shader是运行在GPU上的程序，常用的着色器语言有HLSL、GLSL、CG

### shader和材质
材质可以理解成贴图+shader,通过不同的shader可以让同一张贴图有不同的效果。
### ShaderLab
在unity中，所有的unity Shader都是用ShaderLab来编写的，是unity为shader提供的一层抽象，其主要提供表面着色器（Surface Shader）和 顶点片段着色器（Vertex And Fragment Shader）。
{%  image
    url="/images/post/post29-1.png"
    title="unity shader入门精要中的描述"
%}

### Surface Shader 表面着色器
表面着色器（Surface Shader）是Unity提出的一个概念。编写着色器与光照的交互是复杂的，光源有很多类型，不同的阴影选项，不同的渲染路径(正向和延时渲染)，表面着色器将这一部分简化。Unity建议使用表面着色器来编写和光照有关的Shader。

### Vertex And Fragment Shader 顶点片段着色器
顶点片段着色器（Vertex And Fragment Shader）和OpenGL，Direct3D中的顶点着色器和片段着色器没有什么区别。顶点片段着色器比表面着色器使用更自由也更强大，当然光照需要自行处理。Unity也允许在里面编写几何着色器，一般用得不多。

## 简介
在 Unity 中，当您使用的着色器属于图形管线 的一部分，通常用到 Shader 类的实例。我们将一个<code> Shader </code>类的实例称为 Shader 对象。

Shader 对象是 Unity 使用着色器程序的特定方式；它是着色器程序和其他信息的封装器。它允许您在同一个文件中定义多个着色器程序，并告诉 Unity 如何使用它们。

## unity中基本的着色器模板
- 标准表面着色器/SurfaceShader
- 无关照着色器/Unlit Shader
- 图像效果着色器/Image Effect Shader 
- 图像效果着色器/Image Effect Shader 
- 计算着色器/Compute Shader



## unity shader代码结构

    Shader "Custom/NewSurfaceShader"
    {
        Properties
        {...}
        SubShader
        {...}

        //额外的内容
        FallBack "Diffuse"
        CustomEditor "EditorName"
    }

其中subShadedr为必备的部分，其余的部分均可以省略。

- Properties 属性
    - Properties是一个可以由外部定义的参数列表。在Properties中定义的属性会在材质的面板中暴露。

- SubShaders 子着色器
    - SubShaders中包含了当前shader的核心代码，并可以定义多个SubShader，在加载Shader时，Unity将遍历所有SubShader列表，并最终选择其中与用户设备兼容的子着色器执行。

- FallBack 备选方案
    - 如果没有任何子着色器能够在此硬件上运行，则尝试使用另一个着色器中的子着色器
- CustomEditor 自定义编辑器


## 小结
这部分内容只是简单的对unity shader有一个印象，具体的内容也没有展开，需要在后续的学习中具体的学习。
