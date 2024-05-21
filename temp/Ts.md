## TypeScript
### javaScript与面向对象[参考文档](https://web.nodejs.cn/en-us/docs/web/javascript/inheritance_and_the_prototype_chain/)
#### 动态类型
JavaScript 中的变量不直接与任何特定值类型相关联，并且可以为任何变量分配（和重新分配）所有类型的值：
#### 弱类型
JavaScript 中允许隐式类型转换，而不是抛出类型错误。
#### 设计理念
 - [原型继承模型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain):查找属性或方法时，会在对象的**原型**上查找，直到找到为止。[参考](https://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)

#### 具体设计
- 在Javascript语言中，new命令后面跟的不是类，而是构造函数。
- prototype属性： 它是一个对象，包含了可以由特定类型的所有实例共享的属性和方法。
- 原型：每个JavaScript对象都有一个内置的属性叫做__proto__，这个属性指向它的原型对象。原型对象也可能有自己的原型，这样就形成了一个链式的继承结构。
- 类：在JavaScript中类实际上是“特殊的 functions”，就像定义 函数表达式 和 函数声明 一样，类可以通过两种方式定义：类表达式```XXX = class{}``` 或 类声明 ```class XXX{}```。
### 基本类型[官方文档](https://www.tslang.cn/docs/handbook/basic-types.html)
1. `number`：表示数字，可以是整数或浮点数。
2. `string`：表示字符串，使用单引号或双引号定义。
3. `boolean`：表示布尔值，值为 `true` 或 `false`。
4. `null`：表示空值或不存在的值。
5. `undefined`：表示未定义的值。
6. `object`：表示复杂数据类型。
7. `array`：表示数组，可以使用 `[]` 或 `Array<elementType>` 声明。
8. `tuple`：表示元组，固定长度和各自类型的数组。
9. `enum`：表示枚举类型。
10. `any`：表示任意类型，可以动态改变类型。
11. `void`：表示没有返回值。
12. `never`：表示永不存在的值的类型（例如函数返回错误或无限循环）。


### 基本语法[官方文档](https://www.tslang.cn/docs/home.html)

1. 声明变量并指定类型[中文文档](https://www.tslang.cn/docs/handbook/variable-declarations.html)
    ~~~ 
    let message: string = "Hello, TypeScript!";
    var number: number = 10;
    const isDone: boolean = false;
    ~~~ 
    - let 作用域：块作用域（函数体，IF语句等）
    - var 作用域：包含它的函数，模块，命名空间或全局作用域内部任何位置被访问，它不在乎你声明多少次；你只会得到1个（var坑众多，这只是其一，谨慎使用）
    ~~~
    //这是合法的
    function f(x) {
        var x;
        var x;

        if (true) {
            var x;
        }
    }
    ~~~
    - const 作用域：块作用域下的常量


2. 函数声明与类型注解
    ~~~ 
    function greet(name: string): string {
        return "Hello, " + name;
    }
    ~~~ 
3. 复杂数据结构：接口
    ~~~ 
    interface Person {
        name: string;
        age: number;
    }
    ~~~ 

4. 类与继承
    - 传统
    ~~~ 
    class Animal {
        name: string;
        constructor(name: string) {
            this.name = name;
        }

        makeSound(): void {
            console.log('Animal is making sound');
        }
    }

    class Dog extends Animal {
        breed: string;
        constructor(name: string, breed: string) {
            super(name);
            this.breed = breed;
        }

        bark(): void {
            console.log('Bark, bark!');
            this.makeSound(); // 调用父类方法
        }
    }
    ~~~ 
    - Mixins通过可重用组件创建类
    ~~~
    export function Mixin<T1, T2>(
        t1Type: new (...args: any[]) => {},
        t2Type: {},
    ): new (...args: any[]) => T1 & T2 {
        class T1SubClass extends t1Type {}
        ApplyMixins(T1SubClass, [t2Type]);
        return T1SubClass as unknown as new (...args: any[]) => T1 & T2;
    }
    ~~~
5. 类型转换
    - 类型断言
    ~~~ 
    let someValue: any = "this is a string";
    let strLength: number;
    strLength: number = (someValue as string).length;// 使用as关键字
    strLength: number = (<someValue>someValue).length;// 使用尖括号语法
    ~~~
    - 类型转换
    ~~~
    let numStr: string = "123";
    let num: number = Number(numStr); // 将字符串转换为数字
    ~~~
6. 泛型
    ~~~
    function identity<T>(arg: T): T {
        return arg;
    }

    let output = identity<string>("myString");  // type of output will be 'string'
    ~~~
7. 遍历
    - 循环
    ~~~
    let list = [4, 5, 6];

    // for 循环
    for (let _i = 0; _i < list.length; _i++) {
        let num = list[_i];
        console.log(num);
    }
    // while 循环
    let _j: number = 0;
    while (_j < list.length) {
        let num = list[_j];
        console.log(num);
        i++;
    }
    ~~~

    - 迭代（对象需要实现Symbol.iterator）
    ~~~
    let list = [4, 5, 6];
    // for..in 关注迭代对象的key
    for (let i in list) {
        console.log(i); // "0", "1", "2",
    }
    // for..of 关注迭代对象的value
    for (let i of list) {
        console.log(i); // "4", "5", "6"
    }
    ~~~
1. 模块解析
    - 模块与类：模块注重的是代码的复用而类作为一种面向对象的概念，是用来创建具有特定结构和行为的对象的。
1. 解构赋值
    
1. 类型参数

1. 泛型

### 基本概念
1. 语句块

1. 对象字面量
~~~
let obj = {
    name: '张三',
    age: 20,
    gender: '男'
    getAge(): number{
        return age; // 方法需要有一个返回值
    }
}
~~~

### 特殊机制 
#### Promise
 Promise 是 JavaScript 中用于异步编程的一种重要机制。在 TypeScript 中，Promise 是一种具有 then 和 catch 方法的对象，它表示一个异步操作的最终完成（或失败）及其结果值。

一个 Promise 有以下三种状态：
- pending：初始状态，既不是成功，也不是失败状态。
- fulfilled：意味着操作成功完成。
- rejected：意味着操作失败。

Promise 的基本用法：
~~~
let promise = new Promise((resolve, reject) => {
    // 异步操作...
    if (/* 异步操作成功 */) {
        resolve("成功的结果");
    } else {
        reject("失败的原因");
    }
});
promise.then(result => {
    console.log("成功:", result);
}).catch(error => {
    console.log("失败:", error);
});
~~~
在上述代码中，resolve 函数用于在异步操作成功时将 Promise 的状从 pending 变为 fulfilled，并设置成功的结果值。reject 函数用在异步操作失败时将 Promise 的状态从 pending 变为 rejected，并置失败的原因。
Promise 的 then 方法接受两个参数，第一个参数是当 Promise 状态为 fulfilled 时执行的回调函数，第二个参数是当 Promise 状态变为rejected 时执行的回调函数。

## typeScript 与传统的OOP语言（java/C#）有和区别
[参考](https://www.tslang.com.cn/zh/docs/handbook/typescript-in-5-minutes-oop.html)

### 类型系统
1. 在TypeScript中，申明与使用不需要一一对应，TypeScript的类型只是一个集合，是高度动态的。
    1. 在C#或Java中，可以将运行时类型与其编译时声明之间视为一一对应的。
        在TypeScript中，最好将类型视为共享某些共性的值的集合。因为类型只是集合，一个特定的值可以同时属于多个集合。

        一旦开始将类型视为集合，某些操作变得非常自然。例如，在C#中，传递一个值，该值可能是string或int，会比较别扭，因为不存在代表这种值的单一类型。

        在TypeScript中，一旦你意识到每种类型只是集合，这个问题就变得非常自然。如何描述一个值，它要么属于string集合，要么属于number集合？它 simply 同时属于这两个集合的并集：string | number。

        TypeScript提供了一系列集合论方式处理类型的机制，如果你将类型视为集合，这些机制会变得更加直观。

    
    2. TypeScript中的对象并不是单一类型。例如，如果我们构造一个满足接口的对象，即使两者之间没有声明性关系，我们也可以在需要该接口的地方使用该对象。即只要调用方能满足输入条件即是一次正确的调用。
        
        再比如，定义一个空类型```class Empty {}```，声明函数的入参为```function fn(arg: Empty) {// do something?}```，那么对于任意对象，都是可以调用该方法的。这同样体现了TypeScript中的类型系统所代表的是一种集合，这种集合是可以向下兼容的。TypeScript中将这种特性成为**擦除的结构类型**。

        另一个体现这一思想的设计是 implements 子句仅仅是一个检查，用于判断类是否可以被视为接口类型。它***完全**不会改变类或其方法的类型。

    3. 结构相同的对象可以互相兼容
    ~~~
    class Car {
        drive() {
            // hit the gas
        }
    }
    class Golfer {
        drive() {
            // hit the ball far
        }
    }
    // No error?
    let w: Car = new Golfer();
    ~~~
    4. 泛型
    
        TypeScript的类型系统是结构性的，不是命名性的：我们可以使用具有x和y属性的对象作为Pointlike，因为它们都是数字。类型之间的关系由它们所包含的属性决定，而不是它们是否以某种特定的关系声明。

        TypeScript的类型系统也是不可知的：没有任何东西在运行时告诉我们Pointlike是。实际上，类型运行时是不存在的。

        回到将类型视为集合的概念，我们可以认为Pointlike既是values集合的成员，也是values集合的成员。

        结构类型化的后果 面向对象的程序员通常会对结构类型化的两个特定方面感到惊讶。

        子类型关系可能不如预期明显。在Java或C#中，如果有一个BaseClass和一个DerivedClass，那么DerivedClass是BaseClass的子类型。但在TypeScript中，如果两个类型具有相同的结构，那么它们就是等价的，不区分子类型关系。

        类型检查可能比预期更严格。在Java或C#中，如果有一个方法接受一个string参数，那么传递一个非string类型的值通常会在运行时引发错误。但在TypeScript中，类型检查是在编译时进行的，如果在代码中存在类型不匹配，那么在编译时就会引发错误。

        总之，结构类型化在TypeScript中引入了一些新的概念，面向对象的程序员可能需要一些时间来适应。