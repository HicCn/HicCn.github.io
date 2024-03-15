---
title: Unity Shader 简单实例代码说明
tags: 
    - 编程
    - unity
    - shader
categories: 学习笔记
date: 2023-01-09 11:58:38
---
## 说明
这是一个初级的笔记，通过一个unity Shader实例来了解unity中shader的使用

{% image
    url=""/assets/images/post/post49-1""
    title="效果展示"
%}

## 完整代码
>https://www.cnblogs.com/spiderljx/p/10923121.html

    Shader "TS/TsShader"
    {
        Properties
        {
        }
        SubShader
        {
            Tags{"Queue" = "transparent"  "RenderType" = "transparent"  "IgoreProjector" = "true" }
            Blend  SrcAlpha  oneMinusSrcAlpha     
            Pass
            {
                CGPROGRAM
                #pragma vertex vert
                #pragma fragment frag

                #include "UnityCG.cginc"
                
                struct v2f       
                {
                    float4 pos : POSITION;
                    float4 uv   : TEXCOORD;
                    float4 col :COLOR;
                };

                v2f vert(appdata_base v)   
                {
                    v2f  o;
                    o.pos = UnityObjectToClipPos(v.vertex);  
                    o.uv = v.texcoord;
                    o.col.xyz = v.normal*0.5+0.5;   
                    o.col.w = 1.0;
                    return o;
                }
                half4 frag(v2f i) :COLOR 
                {
                    half4 h = i.col;   
                    return h;
                }
                ENDCG
            }
        }
    }

## CG
>https://www.jianshu.com/p/cca54d6e3cf0
>[CG官方文档](https://developer.download.nvidia.cn/cg/Cg_language.html)
### 数据类型
- float 32位浮点数据，一个符号位。浮点数据类型被所有的图形接口支持；

- half  16位浮点数据；

- int   32位整形数据

- fixed 12位定点数，

- bool  布尔数据，被所有的图形接口支持；

- sampler*  纹理对象的句柄，分为sampler、sampler1D、sampler2D、sampler3D、samplerCUBE和samplerRECT。

## 说明
### #pragma vertex
顶点着色器声明
### #pragma fragment
片元着色器声明
### 
### appdata_base
