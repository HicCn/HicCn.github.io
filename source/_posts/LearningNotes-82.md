---
title: laya 基本认识
date: 2024-04-30 13:06:29
categories: 学习笔记
tags:
    - laya
    - 工具记录
---
[官方文档](https://layaair.layabox.com/#/doc)
## laya 基本说明
- 开源的3D游戏引擎
- LayaAir支持ActionScript3、TypeScript、JavaScript三种语言
  - 3.0只支持TypeScript
- 发布可在浏览器，小游戏平台或在安卓与ios上运行的游戏

## 环境配置
### 安装 Node.js 
Node.js 是一个免费的、开源的、跨平台的 JavaScript 运行时环境。
### 安装 TypeScript
TypeScript 是由微软开发的开源编程语言。它是 JavaScript 的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。
### 浏览器选择 与 编辑器
- 浏览器：Chrome、、Edge
- 编辑器：VSCode

## 基本使用

### 目录结构
- assets
  - 所有的场景与资源都在assets目录，IDE对项目资源的管理，都是来自于该目录
- src
  - 脚本目录
- editor-widgets
  - 插件目录，真实路径为LayaAirIDE\resources
- engine
  - 引擎库的声明文件
- bin

### 节点


### 场景
#### UI 运行时
UI组件脚本只能添加在Scene2D节点或2D预制体根节点的属性设置面板上的Runtime入口。如果添加在Scene2D上，它的父类就继承于Laya.Scene；如果添加在2D预制体的根节点，它的父类就继承于UI小部件的类（根据2D预制体根节点的节点类型而定）。因此，UI组件脚本就是UI运行时，也叫做 Runtime 类，可以对场景或预制体内部所有UI组件进行方便的管理。

##### 与组件间的区别
本质上是设计抽象上的区别

runtime脚本是不可复用的，并且一个界面通常只有唯一的逻辑脚本，所以laya将UI界面用场景来规划，这是唯一的。对于可复用的脚本则是组件归于ECS架构。

[参考官方文档](https://layaair.layabox.com/3.x/doc/IDE/uiEditor/runtime/readme.html)

>在UI开发过程中，我们会使用Image，Box，Tab等等这些LayaAir 提供的UI组件。对于一套相对复杂的UI界面来说，大量的UI组件，用自定义组件脚本的方式管理并不方便，需要每个组件都拖拽到自定义属性中，繁琐而费力。因此我们建议开发者，使用UI组件脚本来管理UI组件，后面我们再说UI组件脚本和自定义组件脚本的区别。UI组件脚本设计的目的就是在场景或者是预制体的根节点创建，能对其内部所有的组件进行更加方便的管理。
### 脚本生命周期
[官方文档](https://layaair.layabox.com/3.x/doc/basics/common/Component/readme.html)

| 名称         | 条件                                                                                                                       | 执行顺序 |
| ------------ | -------------------------------------------------------------------------------------------------------------------------- | -------- |
| onAdded      | 被添加到节点后调用，和Awake不同的是即使节点未激活onAdded也会调用                                                           | 1        |
| onReset      | 重置组件参数到默认值，如果实现了这个函数，则组件会被重置并且自动回收到对象池，方便下次复用。如果没有重置，则不进行回收复用 | 2        |
| onAwake      | 组件被激活后执行，此时所有节点和组件均已创建完毕，此方法只执行一次                                                         | 3        |
| onEnable     | 组件被启用后执行，比如节点被添加到舞台后                                                                                   | 4        |
| onStart      | 第一次执行onUpdate之前执行，只会执行一次                                                                                   | 5        |
| onUpdate     | 每帧更新时执行，尽量不要在这里写大循环逻辑或者使用getComponent方法                                                         |6        |
| onLateUpdate | 每帧更新时执行，在onUpdate之后执行，尽量不要在这里写大循环逻辑或者使用getComponent方法                                     | 7        |
| onPreRender  | 渲染之前执行                                                                                                               | 8        |
| onPostRender | 渲染之后执行                                                                                                               | 9        |
| onDisable    | 组件被禁用时执行，比如从节点从舞台移除后                                                                                   | 10        |
| onDestroy    | 手动调用节点销毁时执行                                                                                                     | 11       |

## Editor 环境
[官方文档](https://layaair.layabox.com/3.x/doc/IDE/layapackage/plug-in/readme.html)

### meta文件
仅有uuid
 
### Electron框架
laya IDE 使用Electron开发，Electron是一个使用 JavaScript、HTML 和 CSS 构建桌面应用程序的框架。

### 脚本隔离机制
编辑器实现脚本隔离的机制是将脚本编译成三个js，bundle.js包含可以在预览环境，也就是在浏览器可以运行的版本；bundle.editor.js是在UI进程运行的脚本；bundle.scene.js是在Scene进程的脚本。这个机制是自动的，但开发者需了解这个机制的运作方式：

1、所有含有@Laya.regClass装饰器的脚本会编译进bundle.js和bundle.scene.js。注意，这里指的“所有”，仅限于Debug版本。在release版本的bundle.js里，只会包含有被场景引用的脚本。bundle.scene.js不会出现在发布版本中。

2、所有含有@IEditorEnv.regClass装饰器的脚本会编译进bundle.scene.js。这个js只在编辑器内部运行，可以放心使用node能力。

3、所有含有@IEditor.xxx装饰器的脚本会编译进bundle.editor.js。这个js只运行在UI进程，可以放心使用node能力，但如果引用Laya的类会报错。

虽然这种识别机制能够解决标记不同脚本使用用途的问题，但还是建议开发者自行用目录方式进行隔离。例如将UI进程运行的脚本放入到editor名称的目录，将只在编辑器内运行的脚本放入到scene名称的目录，这样维护起来会更清晰。
