---
title: Java-异常
type: cheatsheet
tags:
  - 速查
  - 语言/Java
---

# Java-异常

> [!note] 版本说明
> 基于 Java 21 LTS。Java 用异常机制处理错误，比 C 的返回值判断更系统。

## try-catch-finally

> [!example]+ 最常用写法
> ```java
> try {
>     int x = 10 / 0;          // 会抛 ArithmeticException
> } catch (ArithmeticException e) {
>     System.out.println("出错了: " + e.getMessage());
> } finally {
>     System.out.println("无论是否异常都执行");
> }
> ```

**用途**：捕获并处理异常，`finally` 块总是执行（常用于关闭资源）。

**易错点**：
- `finally` 无论有无异常、是否 return 都会执行。
- 捕获具体异常类型，别一上来就 `catch (Exception e)` 吞掉所有异常。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程 · Exceptions（https://docs.oracle.com/javase/tutorial/essential/exceptions/ ），2026-10-25 访问。

## throws 声明与 throw 抛出

> [!example]+ 最常用写法
> ```java
> public void readFile() throws IOException {
>     // 方法签名声明可能抛出的受检异常
>     if (出错) {
>         throw new IOException("文件不存在");
>     }
> }
> ```

**用途**：`throws` 在方法签名声明"可能抛异常"，`throw` 在方法体里主动抛。

**易错点**：
- `throw` 是抛出一个异常**对象**（`throw new Xxx()`），`throws` 是声明（在方法括号后）。
- 两者拼写像但意思完全不同，别混。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程（同上），2026-10-25 访问。

## 受检异常 vs 运行时异常

> [!note]- 两类异常的区别
> - **受检异常（Checked）**：如 `IOException`，编译器强制你处理（try-catch 或 throws），否则编译不过。
> - **运行时异常（Runtime）**：如 `NullPointerException`、`ArrayIndexOutOfBoundsException`，不强制处理，多为程序 bug。
> - 常见运行时异常：`NullPointerException`（空指针）、`IndexOutOfBoundsException`（越界）、`ClassCastException`（类型转换错）。

## 相关链接

- [[Java-基础语法]]
- [[Java-面向对象]]
