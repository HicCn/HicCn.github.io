---
title: 数据类型的基类与其一般方法
tags: 
    - 编程
    - Unity
categories: 学习笔记
date: 2023-01-03 09:17:30
---
## object
>[object文档](https://learn.microsoft.com/zh-cn/dotnet/api/system.object?view=net-7.0)
C#中的object是一种基本数据类型，它是所有其他类型的根类型，可以存储任何类型的值，包括值类型和引用类型。它可以用于定义变量，方法参数和返回值，以及作为参数传递给方法。


- Equals(Object)	
    - 确定指定对象是否等于当前对象。

- Equals(Object, Object)	
    - 确定指定的对象实例是否被视为相等。

- Finalize()	
    - 在垃圾回收将某一对象回收前允许该对象尝试释放资源并执行其他清理操作。

- GetHashCode()	
    - 作为默认哈希函数。

- GetType()	
    - 获取当前实例的 Type。

- MemberwiseClone()	
    - 创建当前 Object 的浅表副本。

- ReferenceEquals(Object, Object)	
    - 确定指定的 Object 实例是否是相同的实例。

- ToString()	
    - 返回表示当前对象的字符串。

### GetHashCode
[GetHashCode文档](https://learn.microsoft.com/zh-cn/dotnet/api/system.object.gethashcode?view=net-7.0#system-object-gethashcode)
[博客园对象哈希码](https://www.cnblogs.com/GreenLeaves/p/7827963.html)

GetHashCode方法是用于比较两个对象是否相等的重要方法。

### Equals
[Equals文档](https://learn.microsoft.com/zh-cn/dotnet/api/system.iequatable-1.equals?view=net-7.0)
GetHashCode方法也是用于比较两个对象是否相等。GetHashCode是用来获取对象的哈希码，而Equals是用来比较两个对象是否相等，它们是不同的概念。


## System.ValueType
[ValueType文档](https://learn.microsoft.com/zh-cn/dotnet/api/system.valuetype?view=net-6.0)

System.ValueType是一种特殊的类型，它是object的派生类，是一种特殊的类型，表示值类型，而object是一种通用类型，它表示引用类型。System.ValueType可以用来表示基本数据类型，如整数、浮点数、布尔值等，而object可以用来表示任何类型的对象，包括值类型和引用类型。

### 对比object
System.ValueType的基本方法包括Equals、GetHashCode、GetTypeCode和ToString，而object的基本方法包括Equals、GetHashCode、GetType和ToString。两者的不同之处在于，System.ValueType的基本方法中多了一个GetTypeCode方法，而object的基本方法中没有这个方法。

