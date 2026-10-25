---
title: Python-函数
type: cheatsheet
tags:
  - 速查
  - 语言/Python
---

# Python-函数

> [!note] 本篇定位
> 函数定义、参数、返回值的基础写法见 [[Python-基础语法#函数定义]]。本篇聚焦 lambda、作用域、常用内置高阶函数等进阶内容。

## lambda 匿名函数

> [!example]+ 最常用写法
> ```python
> f = lambda x: x * 2
> f(5)                     # 10
> sorted(lst, key=lambda x: x[1])   # 按第二项排序
> ```

**用途**：写一次性、短小的函数，常作 `sorted`/`map`/`filter` 的 `key`。

**易错点**：lambda 只能写**一个表达式**，不能包含语句或赋值。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · lambda（https://docs.python.org/3/reference/expressions.html#lambda ），2026-10-25 访问。

## 作用域与 global

> [!example]+ 最常用写法
> ```python
> x = 10
> def f():
>     x = 5          # 这是局部变量，不影响外面的 x
>     return x
>
> def g():
>     global x       # 声明要修改全局变量
>     x = 99
> ```

**用途**：理解变量查找顺序（局部 → 闭包 → 全局 → 内置），即 LEGB。

**易错点**：
- 函数内直接 `x = 5` 创建的是**局部变量**，不会改全局。
- 要改全局变量必须先写 `global x`。
- 只**读**全局变量不需要 `global`，只有赋值才需要。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Naming and binding（https://docs.python.org/3/reference/executionmodel.html#naming-and-binding ），2026-10-25 访问。

## 内置高阶函数

> [!example]+ 最常用写法
> ```python
> list(map(int, ["1", "2"]))         # [1, 2]
> list(filter(lambda x: x > 0, [-1, 2]))  # [2]
> ```

**用途**：`map` 对每个元素套函数；`filter` 按条件过滤；`sorted` 的 `key` 指定排序依据。

**易错点**：`map`/`filter` 返回**迭代器**，要 `list()` 才能直接看结果。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · map / filter（https://docs.python.org/3/library/functions.html#map ），2026-10-25 访问。

## 相关链接

- [[Python-基础语法]]
- [[Python-列表与元组]]
- [[Python-字典与集合]]
