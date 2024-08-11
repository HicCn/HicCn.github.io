---
title: 单元测试基本概念
date: 2024-05-27 01:30:06
categories: 学习笔记
tags:
    - 编程
---
## 怎么做
1. 确定单元：分割最小单元，可以是一个函数、几个函数
1. 编写用例：为每个单元编写一组测试用例，以确保其正常工作。
1. 确认结果：检查测试结果，确保每个测试用例都能通过。

## 测试工具
- Python：unittest、pytest
- C/C++：GoogleTest
- JavaScript/TypeScript：Jest、Mocha
- C#：xUnit
- Lua：LuaUnit
- Go：GoConvey
- Ruby：RSpec
- PHP：PHPUnit
- Kotlin：JUnit
- Rust：test
- Scala：ScalaTest
- Perl：Test::Simple
- Haskell：HUnit
- Java：JUnit

## 非侵入式测试

## 延申 [白盒测试](https://cloud.tencent.com/developer/techpedia/1936)
>它是一种测试程序内部结构和逻辑的方法，通过检查程序的内部结构、设计、代码实现、算法等来验证程序的正确性和完整性。白盒测试通常由开发人员或专业测试人员进行，需要对程序的源代码进行详细的分析，以确定哪些代码需要进行测试，并编写测试用例来检查代码的正确性。

### 白盒测试的要求有哪些？
 - 语句覆盖测试（Statement Coverage Testing）:测试人员通过测试用例覆盖到每一个可执行语句，以验证程序的每一个语句都能够被正确执行。

- 判定覆盖测试（Decision Coverage Testing）
测试人员通过测试用例覆盖到程序中的每一个判断语句，以验证程序的每一个判断条件都能够被正确执行。

 - 条件覆盖测试（Condition Coverage Testing）
测试人员通过测试用例覆盖到程序中每一个判断语句的所有条件，以验证程序的每一个条件都能够被正确执行。

 - 路径覆盖测试（Path Coverage Testing）
测试人员通过测试用例覆盖到程序中的每一条可能的执行路径，以验证程序的每一个路径都能够被正确执行。

 - 分支覆盖测试（Branch Coverage Testing）
测试人员通过测试用例覆盖到程序中每一个分支语句，以验证程序的每一个分支都能够被正确执行。

 - 函数覆盖测试（Function Coverage Testing）
测试人员通过测试用例覆盖到程序中每一个函数，以验证程序的每一个函数都能够被正确执行。

## 延申 [Jest编写测试用例](https://www.jianshu.com/p/eec5e34ff0c2)