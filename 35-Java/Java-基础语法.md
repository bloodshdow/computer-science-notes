---
title: Java-基础语法
type: cheatsheet
tags:
  - 速查
  - 语言/Java
---

# Java-基础语法

> [!note] 版本说明
> 基于 Java 21 LTS（当前教学主流，JDK 25 是最新 LTS）。Java 是静态类型、面向对象语言，所有代码都在类里。

## 第一个程序

> [!example]+ 最常用写法
> ```java
> public class Hello {
>     public static void main(String[] args) {
>         System.out.println("Hello, Java");
>     }
> }
> ```

**用途**：Java 程序入口。`main` 方法签名是固定的，`System.out.println` 打印并换行。

**易错点**：
- **文件名必须和 public 类名一致**（`Hello.java`）。
- `main` 方法必须 `public static void main(String[] args)`，一个都不能少。
- 每条语句末尾要分号 `;`。

**版本/平台**：Java 21 LTS。

**来源**：Oracle Java 文档（https://docs.oracle.com/en/java/javase/21/ ），2026-10-25 访问。

## 变量与基本类型

> [!example]+ 最常用写法
> ```java
> int a = 10;            // 整数
> double b = 3.14;       // 浮点
> char c = 'A';          // 字符（单引号）
> boolean flag = true;   // 布尔
> String s = "hi";       // 字符串（引用类型，双引号）
> final int MAX = 100;   // final 常量
> ```

**用途**：声明变量。Java 有 8 种基本类型（int/double/char/boolean 等），`String` 是引用类型。

**易错点**：
- 字符单引号 `'A'`，字符串双引号 `"A"`。
- `final` 修饰的变量是常量，不能再赋值。
- Java 是强静态类型，变量类型声明后固定。

**版本/平台**：Java 21。

**来源**：Oracle Java 文档 · Primitive types（https://docs.oracle.com/javase/specs/jls/se21/html/jls-4.html ），2026-10-25 访问。

## 控制流

> [!example]+ 最常用写法
> ```java
> if (x > 0) {
>     // ...
> } else if (x == 0) {
>     // ...
> } else {
>     // ...
> }
>
> for (int i = 0; i < 10; i++) { }
> for (int x : arr) { }          // 增强 for，遍历数组/集合
> while (cond) { }
> ```

**用途**：分支与循环，语法和 C/C++ 几乎一样。

**易错点**：
- 判断相等用 `==`（基本类型）；**字符串比较用 `equals` 不是 `==`**（见下）。
- 增强 for 遍历只读，不能修改集合元素。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程 · Control flow（https://docs.oracle.com/javase/tutorial/java/nutsandbolts/flow.html ），2026-10-25 访问。

## 字符串比较（高频坑）

> [!example]+ 最常用写法
> ```java
> String a = "hello";
> String b = new String("hello");
> a.equals(b)          // true，比较内容（正确做法）
> a == b               // false，比较的是引用地址（错误）
> a.length()           // 长度
> a + " world"         // 拼接
> ```

**用途**：`equals` 比较内容，`==` 比较引用。

**易错点**：
- **这是 Java 最经典的坑**：比较字符串内容永远用 `equals`，用 `==` 会得到错误结果。
- `length()` 是**方法**（带括号），不像数组的 `length` 是属性。

**版本/平台**：Java 21。

**来源**：Oracle Java 文档 · String（https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/String.html ），2026-10-25 访问。

## 数组

> [!example]+ 最常用写法
> ```java
> int[] arr = {1, 2, 3};          // 直接初始化
> int[] arr2 = new int[5];        // 定长，默认全 0
> arr[0] = 10;                    // 下标访问
> arr.length                      // 数组长度（是属性，不是方法）
> ```

**用途**：定长数组。长度固定，创建后不能变。

**易错点**：
- 数组长度用 `arr.length`（无括号），和字符串的 `s.length()`（有括号）不同。
- 越界访问抛 `ArrayIndexOutOfBoundsException`。
- 需要动态长度用 `ArrayList`（见 [[Java-集合框架]]）。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程 · Arrays（https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html ），2026-10-25 访问。

## 类型转换

> [!example]+ 最常用写法
> ```java
> int a = (int) 3.14;         // 强制转换（可能丢精度）
> String s = String.valueOf(123);   // 数字转字符串
> int b = Integer.parseInt("123");  // 字符串转数字
> ```

**用途**：类型之间转换。

**易错点**：字符串转数字用 `Integer.parseInt`（失败抛异常）；数字转字符串用 `String.valueOf` 或 `"" + 123`。

**版本/平台**：Java 21。

**来源**：Oracle Java 文档（同上），2026-10-25 访问。

## 相关链接

- [[Java-面向对象]]
- [[Java-集合框架]]
- [[Java-编译运行]]
