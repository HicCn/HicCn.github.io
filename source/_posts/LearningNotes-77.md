---
title: Unity Editor 拓展Inspector面板
date: 2024-03-22 16:16:53
categories: 学习笔记
tags:
    - Unity
---
[官方文档入口](https://docs.unity.cn/cn/2021.1/Manual/UsingTheInspector.html)
## 脚本上的常规标签
1. `[Header("Label")]`：在 Inspector 窗口中为字段或方法添加一个标题，用于更好地组织和描述相关内容。
2. `[HideInInspector]`：隐藏字段或方法，在 Inspector 窗口中不显示该项内容。
3. `[SerializeField]`：将私有字段序列化，使其可以在 Inspector 窗口中显示和编辑。通常用于需要在脚本中访问但又不希望公开为公共字段的变量。
4. `[Space(n)]`：在 Inspector 窗口中添加指定数量的空白行，用于分隔不同的字段或方法。
5. `[Tooltip("Description")]`：在 Inspector 窗口中为字段或方法添加一个工具提示，用于显示额外的描述信息。
6. `[Range(min, max)]`：指定一个数值范围，用于创建滑动条控件，并在 Inspector 窗口中允许用户在指定范围内选择值。
7. `[TextArea(rows, columns)]`：创建一个多行文本输入框，用于在 Inspector 窗口中输入多行文本内容。
8. `[ExecuteInEditMode]`:使脚本在编辑模式下运行，而不仅仅在播放模式下运行。
9. `[RequireComponent(typeof(SomeComponent))]`:自动添加指定类型的组件到游戏对象上，确保所需的组件存在。
10. `[CustomEditor(typeof(SomeComponent))]`:创建自定义的 Inspector 编辑器，以便更灵活地展示和编辑组件或脚本的属性。

## EditorGUILayout 

## [UIElements](https://docs.unity.cn/cn/2019.4/Manual/UIElements.html)

