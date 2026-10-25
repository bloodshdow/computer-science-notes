---
title: Java-集合框架
type: cheatsheet
tags:
  - 速查
  - 语言/Java
---

# Java-集合框架

> [!note] 版本说明
> 基于 Java 21 LTS。集合框架（Collection Framework）是 Java 最常用的工具，掌握 List/Map/Set 三大接口即可。

## 集合总览

| 接口 | 特点 | 常用实现 |
|---|---|---|
| `List` | 有序、可重复、按索引访问 | `ArrayList`、`LinkedList` |
| `Set` | 无序、不重复 | `HashSet`、`TreeSet` |
| `Map` | 键值对 | `HashMap`、`TreeMap` |

## List：有序列表

> [!example]+ 最常用写法
> ```java
> import java.util.*;
>
> List<String> list = new ArrayList<>();
> list.add("a");            // 添加
> list.add("b");
> list.get(0);              // "a"，按下标取
> list.set(0, "A");         // 改下标 0 的值
> list.remove(0);           // 删下标 0
> list.size();              // 大小
> list.contains("a");       // 是否包含
> for (String s : list) { } // 遍历
> ```

**用途**：最常用的列表，`ArrayList` 是动态数组（随机访问快）。

**易错点**：
- 泛型 `List<String>` 指定元素类型，不能放其它类型。
- `ArrayList` 随机访问快；`LinkedList` 插入删除快但访问慢。

**版本/平台**：Java 21。

**来源**：Oracle Java 文档 · List（https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/List.html ），2026-10-25 访问。

## Set：不重复集合

> [!example]+ 最常用写法
> ```java
> Set<Integer> set = new HashSet<>();
> set.add(1);           // 添加（重复的会被忽略）
> set.add(2);
> set.add(1);           // 不会重复添加
> set.size();           // 2
> set.contains(1);      // 是否存在
> ```

**用途**：去重、成员判断。`HashSet` 基于哈希表，`TreeSet` 自动排序。

**易错点**：`Set` 不保证顺序（`HashSet`）；要排序用 `TreeSet`。

**版本/平台**：Java 21。

**来源**：Oracle Java 文档 · Set（https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Set.html ），2026-10-25 访问。

## Map：键值对

> [!example]+ 最常用写法
> ```java
> Map<String, Integer> map = new HashMap<>();
> map.put("apple", 5);        // 添加/修改
> map.get("apple");           // 5，取值
> map.getOrDefault("x", 0);   // 不存在返回默认值
> map.containsKey("apple");   // 是否有这个键
> map.remove("apple");        // 删除
>
> for (Map.Entry<String, Integer> e : map.entrySet()) {
>     e.getKey();   e.getValue();   // 遍历键值对
> }
> ```

**用途**：按键存取值。`HashMap` 基于哈希表，`TreeMap` 按键排序。

**易错点**：
- `get` 不存在的键返回 `null`，用 `getOrDefault` 更安全。
- 遍历键值对用 `entrySet()`，遍历键用 `keySet()`。

**版本/平台**：Java 21。

**来源**：Oracle Java 文档 · Map（https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Map.html ），2026-10-25 访问。

## 集合 vs 数组

> [!note]- 什么时候用哪个
> - **数组** `int[]`：大小固定、性能极致时用。
> - **List/Set/Map**：大小动态、功能丰富，日常开发优先用集合。
> - 集合不能存基本类型，要用包装类（`Integer` 而不是 `int`）。

## 相关链接

- [[Java-基础语法]]
- [[Java-面向对象]]
- [[数据结构-数组与动态数组]]
- [[数据结构-散列表]]
- [[数据结构-红黑树]]
- [[Cpp-STL常用容器]]
