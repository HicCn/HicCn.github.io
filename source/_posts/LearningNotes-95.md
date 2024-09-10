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
                    "build",
                    "${workspaceFolder}/GodotHello.csproj",
                    "-c", "Debug",
                    "-o", "${workspaceFolder}/bin/Debug/net7.0"
                ],
                "problemMatcher": [],
                "group": {
                    "kind": "build",
                    "isDefault": true
                }
            }
        ]
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

