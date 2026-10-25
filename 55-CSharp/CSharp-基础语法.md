---
title: CSharp-基础语法
type: cheatsheet
tags:
  - 速查
  - 语言/CSharp
---

# CSharp-基础语法

> [!note] 版本说明
> 基于 C# 12 / .NET 8（.NET 10 是最新 LTS）。C# 是微软的静态类型面向对象语言，语法和 Java 很像，跨平台（.NET 可在 Windows/Linux/macOS 运行）。

## 第一个程序

> [!example]+ 最常用写法
> ```csharp
> // Program.cs
> using System;
>
> Console.WriteLine("Hello, C#");
> ```

**用途**：C# 顶层语句让 `Main` 方法可以省略，直接写代码。`Console.WriteLine` 打印并换行。

**易错点**：
- 每条语句分号结尾。
- 早期 C# 需要显式 `Main` 方法；新版（.NET 6+）顶层语句简化了入口。

**版本/平台**：C# 12 / .NET 8。

**来源**：Microsoft Learn（https://learn.microsoft.com/zh-cn/dotnet/csharp/ ），2026-10-25 访问。

## 变量与类型

> [!example]+ 最常用写法
> ```csharp
> int a = 10;
> double b = 3.14;
> char c = 'A';
> bool flag = true;
> string s = "hi";
> var x = 10;              // var 自动推断类型
> const int MAX = 100;     // 常量
> ```

**用途**：声明变量。`var` 让编译器推断类型，写起来更简洁。

**易错点**：
- 字符单引号、字符串双引号，和 Java/C 一致。
- `var` 是编译期推断，类型仍然固定（不是动态类型）。

**版本/平台**：C# 12 / .NET 8。

**来源**：Microsoft Learn · 类型（https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/built-in-types ），2026-10-25 访问。

## 字符串处理

> [!example]+ 最常用写法
> ```csharp
> string s = "hello";
> s.Length;              // 长度
> s + " world";          // 拼接
> $"hello {name}";       // 字符串插值（$ 前缀）
> s.ToUpper();           // 转大写
> s.Contains("ell");     // 是否包含
> s.Substring(0, 2);     // 截取
> ```

**用途**：C# 字符串处理。`$"{变量}"` 插值是最常用特性。

**易错点**：
- 字符串插值用 `$"..."`，`{变量}` 里可直接放变量。
- 字符串在 C# 里是引用类型但比较内容用 `==`（和 Java 的 `equals` 不同）。

**版本/平台**：C# 12 / .NET 8。

**来源**：Microsoft Learn · string（https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/reference-types ），2026-10-25 访问。

## 可空类型与 null

> [!example]+ 最常用写法
> ```csharp
> int? x = null;          // ? 表示可空值类型
> string? s = null;       // 可空引用类型（编译器会警告）
> int y = x ?? 0;         // ?? 空合并：x 为 null 时用 0
> ```

**用途**：C# 严格区分"可空"和"非空"，减少空引用异常。

**易错点**：
- 值类型（`int`）默认不能为 null，要可空加 `?`。
- `??` 提供默认值，`?.` 安全访问（`obj?.Name` 为 null 时不报错）。

**版本/平台**：C# 8+ / .NET 8。

**来源**：Microsoft Learn · 可空类型（https://learn.microsoft.com/zh-cn/dotnet/csharp/nullable-references ），2026-10-25 访问。

## 控制流

> [!example]+ 最常用写法
> ```csharp
> if (x > 0) { } else { }
> for (int i = 0; i < 10; i++) { }
> foreach (var item in list) { }   // 遍历集合
> while (cond) { }
> ```

**用途**：分支和循环，语法和 Java 几乎一致。

**易错点**：C# 遍历集合用 `foreach`（对应 Java 的增强 for）。

**版本/平台**：C# 12 / .NET 8。

**来源**：Microsoft Learn · 控制流（https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/statements/ ），2026-10-25 访问。

## 相关链接

- [[CSharp-面向对象]]
- [[CSharp-集合与LINQ]]
- [[CSharp-编译运行]]
