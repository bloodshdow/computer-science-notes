---
title: CSharp-集合与LINQ
type: cheatsheet
tags:
  - 速查
  - 语言/CSharp
---

# CSharp-集合与LINQ

> [!note] 版本说明
> 基于 C# 12 / .NET 8。LINQ 是 C# 最强大的特性之一，用类 SQL 的语法查询集合。

## 集合：List / Dictionary

> [!example]+ 最常用写法
> ```csharp
> using System.Collections.Generic;
>
> List<int> list = new List<int>();
> list.Add(1);            // 添加
> list.Add(2);
> list[0];                // 下标访问
> list.Count;             // 大小（注意是 Count 不是 Length）
> list.Contains(1);       // 是否包含
>
> Dictionary<string, int> map = new Dictionary<string, int>();
> map["apple"] = 5;       // 添加/修改
> map.ContainsKey("apple");   // 是否有键
> map["apple"];           // 取值
> ```

**用途**：`List` 动态数组、`Dictionary` 键值对，最常用的两个集合。

**易错点**：
- `List` 的大小是 `Count`（不是 `Length`，那是数组的）。
- `Dictionary` 用 `map[key]` 取不存在的键会抛 `KeyNotFoundException`，先 `ContainsKey` 或用 `TryGetValue`。

**版本/平台**：C# 12 / .NET 8。

**来源**：Microsoft Learn · List / Dictionary（https://learn.microsoft.com/zh-cn/dotnet/api/system.collections.generic.list-1 ），2026-10-25 访问。

## LINQ：集合查询

> [!example]+ 最常用写法
> ```csharp
> using System.Linq;
>
> var nums = new List<int> { 1, 2, 3, 4, 5 };
>
> var even = nums.Where(x => x % 2 == 0);       // 过滤：[2,4]
> var doubled = nums.Select(x => x * 2);        // 映射：[2,4,6,8,10]
> var sum = nums.Sum();                         // 求和：15
> var first = nums.First(x => x > 3);           // 第一个 >3：4
> var sorted = nums.OrderByDescending(x => x);  // 降序排序
> ```

**用途**：LINQ 用函数式风格查询集合，`Where`（过滤）、`Select`（映射）最常用，替代手写循环。

**易错点**：
- LINQ 返回的是**惰性查询**，`ToList()` 才真正执行并转成列表。
- `First` 找不到会抛异常；不确定时用 `FirstOrDefault`（返回默认值）。

**版本/平台**：C# 12 / .NET 8。

**来源**：Microsoft Learn · LINQ（https://learn.microsoft.com/zh-cn/dotnet/csharp/linq/ ），2026-10-25 访问。

## 遍历集合

> [!example]+ 最常用写法
> ```csharp
> foreach (var item in list) {
>     Console.WriteLine(item);
> }
>
> foreach (var kv in map) {   // 遍历字典
>     kv.Key;   kv.Value;
> }
> ```

**用途**：`foreach` 遍历所有集合。

**易错点**：`foreach` 遍历时不能修改集合（会抛异常），要改就收集起来再改。

**版本/平台**：C# 12。

**来源**：Microsoft Learn · foreach（https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/statements/iteration-statements ），2026-10-25 访问。

## 相关链接

- [[CSharp-基础语法]]
- [[CSharp-面向对象]]
