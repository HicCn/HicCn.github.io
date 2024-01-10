---
title: 通过委托实现观察者模式
tags: 
    - 编程
    - C#
categories: 学习笔记
date: 2022-11-03 21:41:33
---

## 观察者模式

    在游戏开发的过程中，对象之间往往都有着复杂的依赖，比如我们的系统需要的玩家的操作做出反应，当玩家的操作出现失误，游戏的画面要对失误做出反应，玩家的血量需要进行扣除（如果有），或者是通过某个操作触发了成就，或者是完成了任务。这一系列的反应如果没有进行良好的处理，就会让程序的耦合程度越来越高。由此我们希望有一个方法能在某个关键节点做出改变时**通知**需要做出反应的对象，使其做出反应，观察者模式就是由此而来。

      观察者模式是一个在游戏开发中使用频率非常高的设计模式，一般来说它用于在对象间建立一种一对多的依赖关系。通知是观察者模式中的关键动作，所以观察者模式也叫做发布-订阅模式，它是一种对象行为模式。

### 通过委托的实现方式

####    什么是委托

     委托是一种**引用****类型**，在理解上，我们可以从很多的角度去理解委托，从委托的形式上，我们可以理解为委托是方法的数组，或者委托是一个方法的工厂，我们需要知道它大体上是生产哪类产品的（定义返回类型），需要知道生产前需要什么原料（声明参数列表），或者根据经验，委托可以理解成C中的函数指针。就结果而言，通过委托我们可以将方法作为一种变量来使用。

      最后通过一个实例来声明并使用一个委托。
````
 public delegate int testProgrm(int a , int b);//声明委托
 class Program
     {
         static void Main(string[] args)
         {
             funcClass FuncClass = new();
             testProgrm demo = FuncClass.add_1;//创建一个委托实例
             demo(10,20);//调用委托
             demo += FuncClass.add_2;//添加事件
             demo -= FuncClass.add_2;//移除事件
        }
     }
 
     class funcClass{
         public int add_1(int a,int b){
             return a+b;
         }
         public int add_2(int a,int b){
             return a+b;
         }
     }
````
     最后，还要了解下，基于委托出现的事件（Event）。事件是在委托的基础上出现的，但事件不是委托的实例，事件也不能简单的理解成一种特殊的委托，对于事件来说，事件对委托进行了封装使其只有add/remove方法，这样做使其不能对外开发，外部仅能进行订阅与取消的操作，所以二者的关系有些类似与字段与属性。通过事件对委托进行保护。

####    使用委托的观察者模式

从委托的形式我们就可以看出来，委托的使用方式就是一种发布-订阅模式，通过将方法注册到委托实例中，在调用时就会依次对实例中的方法进行调用。通过委托我们可以很轻松的实现观察者模式。

以下代码通过字典建立事件与方法间的联系，仅供参考。


    public delegate void EventDelegate(EventObject evn);//声明委托类型
    public abstract class EventObject { }//声明参数类型
    public class EventBus {
        readonly Dictionary<ushort, List<EventDelegate>> _dic; //用字典存储事件
        public EventBus()
        {
            _dic = new Dictionary<ushort, List<EventDelegate>>();
        }
        public void AddObserver(ushort EventID, EventDelegate evn)
        {
            try{
                _dic[EventID].Add(new EventDelegate(evn));
            }
            catch{
                List<EventDelegate> tL = new List<EventDelegate>();
                tL.Add(new EventDelegate(evn));
                _dic.Add(EventID,tL);
            }
        }
        public void RemoveObserver(ushort EventID,EventDelegate evn)
        {
            try{
             _dic.Remove(EventID);
            }catch{
            }
        }
        public void Notify(ushort EventID)
        {
            if (_dic[EventID].Count != 0)
            {
                foreach (var evn in _dic[EventID])
                {
                    evn.Invoke(null);
                }
            }
        }
        public void Notify(ushort EventID,EventObject Evn)
        {
            if (_dic[EventID].Count != 0)
            {
                foreach (var evn in _dic[EventID])
                {
                    evn.Invoke(Evn);
                }
            }
        }
    }