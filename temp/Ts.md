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