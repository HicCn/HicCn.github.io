---
title: C#中多态的实现
tags: 
    - 编程
    - C#
categories: 学习笔记
date: 2022-11-10 23:46:07
---
## 定义
简单对多态进行定义，即一个行为具有多种表达。

## 函数重载
重载是多态的一种基本方法，对于相同名称的函数，通过不同的参数类型，参数个数使其有不同的表达。
## 虚拟成员
虚拟成员是官方的定义，具体的我们可以理解为允许基类中派生类重新定义的修饰方法，仅当基类成员声明为<code>virtual</code>或<code>abstract</code>时，派生类才可以重写基类的对应成员。对应的，派生类需要声明对应成员为<code>override</code>或<code>abstract</code>。

### virtual与abstract

|说明|virtual|abstract|
|---|---|---|
|基类创建时|必须实现|没有实现|
|基类的实例化|允许|不允许|
|子类重写|可以不重写|必须实现|
|子类的重写修饰|方法前加<code>override</code>|方法前加<code>abstract</code>|

### 接口
接口是一种特殊的抽象类，同样可以实现多态的表达。
### 具体细节
- 如果需要派生类的子类停止重写虚方法，可以使用<code>sealed</code>停止该类的派生类重写虚方法。
- 通过 <code>base</code> 关键字访问基类的该方法或属性

## New关键字
使用<code> new </code>关键字可以隐藏基类成员，使派生类具有与基类中的成员同名的成员。
###  Override 和 New 
<code>new</code>是隐藏，<code>override</code>为覆盖。举一个例子

    class BaseClass
    {
        public virtual void outTs(){
            Console.WriteLine("基类方法");
        }
    }

    class DerivedClass_A : BaseClass
    {
        public new void outTs(){
            Console.WriteLine("子类方法");
        }
    }

    class DerivedClass_B : BaseClass
    {
        public override void outTs(){
            Console.WriteLine("子类方法");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            BaseClass newTS = new DerivedClass_A();
            BaseClass overrideTS = new DerivedClass_B();

            newTS.outTs();
            overrideTS.outTs();
        }
    }
这时的输出结果为

    基类方法
    子类方法

可以说明使用<code>new</code>时，在多态性调用时 原类型的方法不会被覆盖。

## 引申
### base 关键字
- 调用基类上已被其他方法重写的方法。
- 创建派生类时，会先调用一次基类的构造方法。
### 构造顺序
- 对于基类，即不包含继承关系时
    1. 静态字段
    2. 静态构造方法
    3. 实例字段
    4. 实例构造方法
- 对于派生类，即包含继承关系
    1. 子类的静态字段
    1. 子类的静态构造方法
    1. 子类的实例字段
    1. 父类的静态字段
    1. 父类的静态构造方法
    1. 父类的实例字段
    1. 父类的实例构造方法
    1. 子类的实例构造方法