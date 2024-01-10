---
title: C#中的可访问性
tags: 
    - 编程
    - C#
categories: 学习笔记
date: 2022-11-10 22:31:21
---
## 定义
首先引用官方定义对C#的访问级别有一个简单认识。
>
| 声明的可访问性 | 含义 |
| ----------- | ----------- |
| public  |	访问不受限制。|
| protected|	访问限于包含类或派生自包含类的类型。|
| internal	| 访问限于当前程序集。|
| protected internal	| 访问限于当前程序集或派生自包含类的类型。|
| private |	访问限于包含类。|
| private protected |	访问限于包含类或当前程序集中派生自包含类的类型。|
>

我们可以注意到有三个基本的作用范围-类、派生类、程序集，关键字围绕着三个基本单位，对程序的访问权限进行限制
我们可以不严谨的对C#中的可访问级别进行一个排序，并通过下表直观的看到关键字对应的可访问性。
- public > protected > internal protected > internal > private protected > private

|调用方的位置|	public|	protected internal	|protected	|internal	|private protected|	private|
| --- |  :----: |  :----: |  :----: |  :----: |  :----: |  :----: |  
|在类内|	✔️️	|✔️	|✔️	|✔️	|✔️	|✔️|
|派生类（相同程序集）	|✔️	|✔️	|✔️	|✔️|	✔️	|❌|
|非派生类（相同程序集）	|✔️	|✔️	|❌|	✔️|	❌|	❌|
|派生类（不同程序集）	|✔️	|✔️	|✔️	|❌|	❌|	❌|
|非派生类（不同程序集）	|✔️	|❌	|❌|	❌|	❌|	❌|

### 类
将类仅仅理解为class是不够准确的，类似的像struct也是可以被private修饰并且效果一致的。类不仅仅是类，更像是声明了一种仅限内部的访问。
### 派生类
派生类的就是子类，继承是通过使用派生来完成的，使用也叫派生类，可以理解为这是类和类之间的一种特殊光系。
### 程序集
程序集不同于命名空间，命名空间是对代码整合逻辑的梳理，而程序集是指编译之后生成的 .dll 或 .exe，基本上可以理解为可以由其他应用程序或程序集调用的API。
</br>

## 例子
- protected

        public class A
        {
            protected int x;
            static void F(A a, B b) {
                a.x = 1;        // Ok
                b.x = 1;        // Ok
            }
        }
        public class B: A
        {
            static void F(A a, B b) {
                a.x = 1;        // Error, must access through instance of B
                b.x = 1;        // Ok
            }
        }
    基本上，可以将protected理解为一个私有类型，你无法直接对其进行访问，但是可以通过派生类的实例进行访问。
- protected internal

        public class A
        {
            protected internal int x;
            static void F(A a, B b)
            {
                a.x = 1;        // Ok
                b.x = 1;        // Ok
            }
        }
        public class B : A
        {
            static void F(A a, B b)
            {
                a.x = 1;        // Ok
                b.x = 1;        // Ok
            }
        }
    对于protected internal我们要清楚其主体为internal，所以对于同一程序集内的类之间基本可以认为它是公开的，并且运行不同程序集中的派生类访问。
- private protected<br>
    通过对比private protected与protected，可以发现private修饰protected时，其修饰的部分是程序集，对于不同的程序集，限制之间的访问。
## 引申
### 程序域（AppDomain）
为了保证代码的键壮性CLR希望不同服务功能的代码之间相互隔离，这种隔离可以通过创建多个进程来实现，但操作系统中创建进程是即耗时又耗费资源的一件事，所以在CLR中引入了AppDomain的概念，AppDomain主要是用来实现同一进程中的各AppDomain之间的隔离，AppDomain可以用以下特征来描述它的全貌：

- AppDomain概念并不存在于操作系统，而只存在于.net中并且AppDomain不可脱离进程单独存在，它是属于某一CLR或寄宿着CLR的进程的。

- 一个进程中可以有多个AppDomain,并且每个之间相互隔离（只保证安全代码的隔离，不安全代码并不能保证）,此可以理解为AppDomain是.net程序中的"进程"，在一个AppDomain中创建的对象只属于本AppDomain，多个AppDomain之间的对象不能相互访问，除非遵循CLR的一些规则。

- .net程序启动时在进程中创建一个默认的AppDomain，入口代码将运行于此AppDomain，默认应用程序域只有在进程终止时才会被销毁，如果主动的调用Unload去卸载默认应用程序域，会抛出一个CannotUnloadAppDomainException。

- 每个AppDomain都单独的加载程序集，这意味着在A应用程序域中加载了的程序集，并不一定在B应用程序域中也被加载了。每个APPDomain有单独的Loader堆，互相不影响，每个Loader堆都记录了自AppDomain建立以后所访问过的类型，Loader堆中的每个类型对象都有一个方法表，这些方法表指向已经被JIT编译过的本地代码（前提是这些方法是已经被至少执行过一次的）。因为AppDomain是相互隔离的所以相同的一个类型中的方法，在A应用程序域中是被JIT编译过的，但不一定在B应用程序域中也是被JIT编辑过的，方法是否被JIT编辑过取决于些方法是否在本AppDomain被调用过。

- 当AppDomain被卸载时，此AppDomain中的程序集会被卸载，因为每个APPDomain加载的程序集都是独立的所以一个应用程序域被卸载并不会影响其它AppDomain中加载的程序集,另外本AppDomain的loader堆也会被回收，每个程序域的loader堆是独立的所以也不会影响到其它程序域的Loader堆，因为loader堆是独立的（静态字段是存在于类型对象上的），所以一个类型中的静态字段在不同应用程序域中也是不同的存在，所以静态字段也是不被影响的，唯一受影响的是线程，因为线程可以跨越应用程序域访问不同的应用程序域上的代码，后面我们会介绍当卸载一个应用程序域时如果对线程做处理。

- 有一种程序集可以被多个AppDomain使用，这种程序集叫做"AppDomain中立"的程序集，比如MSCorLib.dll，该程序集包含了System.Object,System.Int32以及其它的与.net framework密不可分的类型，这个程序集在CLR初始化时会自动加载，JIT会为这些程序集创建一个特殊的Loader堆，并且程序集中的方法被编译成的本地代码可被所有AppDomain共享，这种程序集不可被卸载只有当进程结束时这种程序集才会被卸载。

 ### 作为其他类型的成员的嵌套类型可以具有如下表所示的声明的可访问性
 |成员	|默认成员可访问性|	允许的成员的声明的可访问性|
 |---|---|---|
|enum|	public	|无|
|class	|private	|public、protected、internal、private、protected internal、private protected|
|interface	|public	|public、protected、internal、private*、protected、internal、private protected|
|struct	|private	|public、internal、private|