---
title: 有限状态机笔记
tags: 
    - 编程
categories: 学习笔记
date: 2022-12-06 09:17:56
---
## 什么是有限状态机
状态机是有限状态自动机的简称，是现实事物运行规则抽象而成的一个数学模型，状态机有四个基本的属性：状态、事件、动作、变化。对于状态机来说，应该有初始状态和有限的状态与有限的事件。

>Allow an object to alter its behavior when its internal state changes. The object will appear to change its class. 
>
>当一个对象的内在状态改变时，允许它修改自己的行为。这个对象看起来像是改变了类

### 有限的含义
理论上任何事物都可以抽象出有限的状态。比如一杯水的温度可以算作它的状态，理论上温度的值是无限的，比如我可以说水的温度从 30° 升到了 30.0001° 也算是状态变化，但是我们在普遍场景下，对水的温度精度并不会要求很高。同样的，我们虽然可以按照常识将人的运动状态划分出了站立，跳跃，下蹲等，但同样进行了一定程度的抽象。

## 为什么要使用状态机
状态机简单来说就是对状态的管理，保证状态能正确流畅的切换。
## 状态机图
状态机可以抽象成一张有向图

{%  image
    url="/images/post/post35-1.jpg"
    title="状态机例图"
%}

以站立作为初始状态举例，我们可以抽象的理解为

站立（状态）+ 按下【↑】（事件） = 跳跃（状态）+ 跳跃事件（事件）
## 实现思路

>简单实现，仅供参考，应依据业务环境设计

对于状态机来说，它需要实现以下功能

- 改变状态
- 执行事件
- 获得当前状态

对于状态，需要满足

- 事件的内容 

### 代码部分

状态机

    class StateMode
        {
            private StateBase State;

            //构造，设置初始状态
            public StateMode(StateBase beginState)
            {
                this.State = beginState;
            }
            //获取当前状态
            public StateBase GetState()
            {
                return this.State;
            }
            //改变状态
            public void changeState(StateBase change)
            {
                this.State = change;
            }

            public void doEvent(){
                this.State.doEvent();
            }
        }

状态基类

    interface StateBase
    {
        public void doEvent();
    }

状态实例

    public class stopState : StateBase
    {
        public void doEvent()
        {
            Console.WriteLine("对象停止");
        }
    }
    public class moveState : StateBase
    {
        public void doEvent()
        {
            Console.WriteLine("对象运动");
        }
    }

测试

    static void Main(string[] args){
        stopState stop = new stopState();
        moveState move = new moveState();
        StateMode obj = new StateMode(stop);
        obj.doEvent();
        obj.changeState(move);
        obj.doEvent();
    }

输出结果

    对象停止
    对象运动
    
对于状态复杂的对象，我们可以利用一个字典对状态进行存储，扩展状态接口使其实现切换状态时的判断条件从而实现对象对自身状态的管理。