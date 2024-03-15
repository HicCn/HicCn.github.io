---
title: 迭代器模式与C#中的迭代器
tags: 
    - 编程
    - C#
categories: 学习笔记
date: 2022-11-27 01:45:15
---

## 迭代器模式

简单来说，迭代器模式提供一种方法顺序访问一个聚合对象中各个元素, 而又无须暴露该对象的内部表示。对于使用者不用关心其类型是array，list，linked list或者是其他什么数据结构。

迭代器模式是一种广泛运用的模式，基于此，在.NET中，迭代器模式被IEnumerator和IEnumerable及其对应的泛型接口所封装。如果一个类实现了IEnumerable接口，那么就能够被迭代；调用GetEnumerator方法将返回IEnumerator接口的实现，它就是迭代器本身。迭代器类似数据库中的游标，他是数据序列中的一个位置记录。迭代器只能向前移动，同一数据序列中可以有多个迭代器同时对数据进行操作。

## Enumerator接口
IEnumerator接口可以理解为一个迭代的计数器。它定义了一个成员Current，记录当前位置。拥有两个方法，MoveNext()即移动到下一个位置，Reset()即重新计数。

    namespace System.Collections
    {
        //
        // 摘要:
        //     Supports a simple iteration over a non-generic collection.
        public interface IEnumerator
        {
            //
            // 摘要:
            //     Gets the element in the collection at the current position of the enumerator.
            //
            // 返回结果:
            //     The element in the collection at the current position of the enumerator.
            object Current { get; }

            //
            // 摘要:
            //     Advances the enumerator to the next element of the collection.
            //
            // 返回结果:
            //     true if the enumerator was successfully advanced to the next element; false if
            //     the enumerator has passed the end of the collection.
            //
            // 异常:
            //   T:System.InvalidOperationException:
            //     The collection was modified after the enumerator was created.
            bool MoveNext();
            //
            // 摘要:
            //     Sets the enumerator to its initial position, which is before the first element
            //     in the collection.
            //
            // 异常:
            //   T:System.InvalidOperationException:
            //     The collection was modified after the enumerator was created.
            void Reset();
        }
    }


## IEnumerable接口
IEnumerable接口可以理解为是一个可迭代的声明，实现了IEnumerable就可以找到IEnumerator，才可以使用foreach遍历。

    namespace System.Collections
    {
        //
        // 摘要:
        //     Exposes an enumerator, which supports a simple iteration over a non-generic collection.
        public interface IEnumerable
        {
            //
            // 摘要:
            //     Returns an enumerator that iterates through a collection.
            //
            // 返回结果:
            //     An System.Collections.IEnumerator object that can be used to iterate through
            //     the collection.
            IEnumerator GetEnumerator();
        }
    }

## 迭代器类图

{% image
    url = "/assets/images/post/post32-1.png"
    title = "迭代器类图"
%}

## 关于foreach
foreach是C#提供的原生迭代函数,foreach的实现其实很简单，如设计模式中所示，对集合调用GetEnumerator方法获取迭代器，然后使用while循环，直到迭代器的MoveNext方法返回false，当MoveNext方法返回的值不为false时，可以对迭代器调用Current属性，获取迭代器当前所对应的值。

        public static void Foreach<T>(this IEnumerable<T> list, Action<T> action)
        {
            var it = list.GetEnumerator();
            while (it.MoveNext())
            {
                action(it.Current);
            }
        }

调用

        int[] numbers = {1,2,3,4,5,6};
        numbers.Foreach(i => {
            Console.WriteLine(i + "\t");
        });    


## yield语句

C#2.0中的迭代器的实现代码相较于C#1.0有了很大幅度的减少，之所以会这样这主要就是引入了yield关键字。yield关键字其实质就是在编译器对代码进行编译时，遇到yield关键字时就是在提示编译器这是实现一个迭代器块的方法。也就是将本来应该由我们创建嵌套类实现IEnumerator的工作，让编译器帮我们做了而已。但是这样的确使我们为实现迭代器减少了很大的工作量，使我们能更好的运用迭代器这一工具。

### 拓展：unity协程中的常见用法
- yield return new WaitForSeconds(3.0f); // 等待3秒，然后继续从此处开始，常用于做定时器。
- yield return null; // 这一帧到此暂停，下一帧再从暂停处继续，常用于循环中。
- yield return 1; // 这一帧到此暂停，下一帧再从暂停处继续。这里return什么都是等一帧，后面的返回值没有特殊意义。所以返回0或1或100都是一样的。参考：http://blog.csdn.net/nanggong/article/details/48421053
- yield return new WaitForEndOfFrame(); // 等到这一帧的cameras和GUI渲染结束后再从此处继续，即等到这帧的末尾再往下运行。这行之后的代码还是在当前帧运行，是在下一帧开始前执行，跟return null很相似。
- yield return new WaitForFixedUpdate(); // 在下一次执行FixedUpdate的时候继续执行这段代码，即等一次物理引擎的更新。
- yield return www; // 等待直至异步下载完成。
- yield break; // 直接跳出协程，对某些判定失败必须跳出的时候，比如加载AssetBundle的时候，WWW失败了，后边加载bundle没有必要了，这时候可以yield break跳出。
- yield return StartCoroutine(methodName); // 等待另一个协程执行完。这是把协程串联起来的关键，常用于让多个协程按顺序逐个运行。