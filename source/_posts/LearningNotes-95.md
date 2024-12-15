---
title: Godot 环境配置
date: 2024-09-09 01:14:18
tags:
    - 工具记录
categories:
    - 开发笔记
---
## Godot 简介
### 目录结构
Godot 没有严格的目录结构规范，一个空项目包(c#)含，默认文件创建在根目录下
- .godot
  - editor
  - imported
  - mono
  - shader_cache
  - .gdignore
  - global_script_class_cache.cfg
  - uid_cache.bin
- icon.svg
- icon.svg.import
- project.godot
## Godot C# 环境
- [配置编辑器](https://docs.godotengine.org/zh-cn/4.x/tutorials/scripting/c_sharp/c_sharp_basics.html)
  - 在 Godot 的 Editor(编辑器) → Editor Settings(编辑器设置) 菜单中：

  设置 Dotnet(.NET) -> Editor(编辑器) -> External Editor(外部编辑器) 为 Visual Studio Code 。

- Godot支持使用命令行[命令行教程](https://www.osgeo.cn/godot/getting_started/editor/command_line_tutorial.html)

### vsCode 环境搭建
- 插件
  - C#
  - C# Tools for Godot
  - code-translate 翻译插件
- 设置控制台编码格式
  - 
  
### Godot 断点
- launch.json文件
  官方文档中的program项输入的是"${env:GODOT4}",应该是需要配置环境变量，但我直接使用了路径。
    ~~~
    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "Play",
                "type": "coreclr",
                "request": "launch",
                "preLaunchTask": "build",
                "program": "你的Godot.exe路径",
                "args": [],
                "cwd": "${workspaceFolder}",
                "stopAtEntry": false,
            }
        ]
    }
    ~~~

- tasks.json文件

    ~~~
    {
        "version": "2.0.0",
        "tasks": [
            {
                "label": "build",
                "command": "dotnet",
                "type": "process",
                "args": [
                    "build"
                ],
                "problemMatcher": "$msCompile",
                "presentation": {
                    "echo": true,
                    "reveal": "silent",
                    "focus": false,
                    "panel": "shared",
                    "showReuseMessage": true,
                    "clear": false
                }
            }
        ]
    }
    ~~~


## Godot Hello
测试脚本

```
using Godot;
using System;

namespace HelloWorldProject
{
    public partial class HelloWorld : Node2D
    {
        public override void _Ready()
        {
            GD.Print("Hello World!");
        }
    }
}
```

## API查询
- [Godot API](https://docs.godotengine.org/zh-cn/4.x/classes/index.html)

## Godot 基本认识
- [推荐教程](https://www.bilibili.com/video/BV1kC4y1677m/)
- [设计理念](https://docs.godotengine.org/zh-cn/4.x/getting_started/introduction/godot_design_philosophy.html)
- 所有对象都是Node的子类
- 节点树
- 不区分场景和预制体
- 不区分节点和组件
  - 节点即组件
- 信号
  - ![alt text](image.png)

## C#版本接入luban
- 使用.net版本的luban
- 将对应的luban核心代码放入项目
- 配置外部工具
