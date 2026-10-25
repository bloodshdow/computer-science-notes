---
title: Python-基础语法
type: cheatsheet
tags:
  - 速查
  - 语言/Python
---

# Python-基础语法

## 变量与基本类型

> [!example]+ 最常用写法
> ```python
> x = 10            # int 整数
> y = 3.14          # float 浮点数
> name = "Alice"    # str 字符串
> flag = True       # bool 布尔
> n = None          # NoneType 空值
> ```

**用途**：Python 变量无需声明类型，赋值即创建；类型是动态的。

**易错点**：
- Python 是强类型，`"a" + 1` 会报 `TypeError`（不会自动拼接）。
- `None` 表示"空值"，判断用 `x is None` 而不是 `x == None`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · 内置类型（https://docs.python.org/3/library/stdtypes.html ），2026-10-25 访问。

## 基本运算符

> [!example]+ 最常用写法
> ```python
> 7 / 2    # 3.5  真除法，结果是 float
> 7 // 2   # 3    整除（向下取整）
> 7 % 2    # 1    取余
> 2 ** 10  # 1024 幂运算
> ```

**用途**：算术运算。`/`、`//`、`%`、`**` 是 Python 特有或易混点。

**易错点**：
- `/` 永远返回浮点数，整数除要用 `//`。
- `//` 是向下取整，负数时注意：`-7 // 2 == -4`。
- `**` 是幂运算（不是 `^`，`^` 是按位异或）。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Numeric Types（https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex ），2026-10-25 访问。

## 条件判断

> [!example]+ 最常用写法
> ```python
> x = 10
> if x > 0:
>     print("正数")
> elif x == 0:
>     print("零")
> else:
>     print("负数")
> ```

**用途**：分支判断。Python 用缩进表示代码块，没有大括号。

**易错点**：
- 分支条件是 `elif`，不是 `else if`。
- 缩进必须是 4 个空格（或一致的 Tab），混用会报 `IndentationError`。
- `elif` 和 `else` 结尾要加 `:`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · if 语句（https://docs.python.org/3/tutorial/controlflow.html#if-statements ），2026-10-25 访问。

## 循环

> [!example]+ 最常用写法
> ```python
> for i in range(5):        # 0,1,2,3,4
>     print(i)
> for item in [1, 2, 3]:    # 直接遍历元素
>     print(item)
> while x > 0:              # 条件循环
>     x -= 1
> ```

**用途**：`for` 遍历可迭代对象；`while` 按条件循环。

**易错点**：
- `range(5)` 是 0 到 4，**不含** 5。
- `range(start, stop, step)` 的 `stop` 不包含。
- 循环体内 `break` 跳出、`continue` 跳过本次。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · for 语句 / range（https://docs.python.org/3/tutorial/controlflow.html#for-statements ），2026-10-25 访问。

## 函数定义

> [!example]+ 最常用写法
> ```python
> def add(a, b):
>     """返回两数之和。"""
>     return a + b
>
> def greet(name="world"):   # 默认参数
>     return f"hello {name}"
> ```

**用途**：用 `def` 定义函数，`return` 返回值。

**易错点**：
- 没有 `return` 的函数返回 `None`。
- 默认参数要放在非默认参数后面。
- 可变默认参数（如 `def f(x=[])`）有坑，见进阶。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Defining Functions（https://docs.python.org/3/tutorial/controlflow.html#defining-functions ），2026-10-25 访问。

> [!note]- 进阶：可变默认参数陷阱
> ```python
> def f(x, items=[]):      # 错误：[] 只创建一次，多次调用会累积
>     items.append(x)
>     return items
> # 正确写法：
> def f(x, items=None):
>     if items is None:
>         items = []
>     items.append(x)
>     return items
> ```

## 参数传递

> [!example]+ 最常用写法
> ```python
> def f(a, b, c=0, *args, **kwargs):
>     print(a, b, c, args, kwargs)
> f(1, 2, 3, 4, 5, x=6)   # 1 2 3 (4, 5) {'x': 6}
> ```

**用途**：位置参数、默认参数、`*args` 收集多余位置参数、`**kwargs` 收集关键字参数。

**易错点**：`*args` 收集成**元组**，`**kwargs` 收集成**字典**；顺序必须是 位置 → 默认 → `*args` → `**kwargs`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · More on Defining Functions（https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions ），2026-10-25 访问。

## 列表推导式

> [!example]+ 最常用写法
> ```python
> [i * 2 for i in range(5)]            # [0, 2, 4, 6, 8]
> [i for i in range(10) if i % 2 == 0] # [0, 2, 4, 6, 8]，带条件
> ```

**用途**：一行生成列表，比显式 for 循环更简洁。

**易错点**：条件写在 `for` 后面（`if` 过滤）；想写 if/else 分支则要放前面：`[x if x>0 else 0 for x in lst]`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · List Comprehensions（https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions ），2026-10-25 访问。

## 异常处理

> [!example]+ 最常用写法
> ```python
> try:
>     x = 1 / 0
> except ZeroDivisionError as e:
>     print("出错了:", e)
> else:
>     print("没出错才执行")
> finally:
>     print("无论怎样都执行")
> ```

**用途**：捕获并处理异常，避免程序崩溃。

**易错点**：
- `except` 尽量捕获具体异常类型，别裸用 `except:`（会吞掉所有异常）。
- `finally` 无论是否异常都会执行，常用于关闭文件/连接。
- 主动抛出用 `raise ValueError("...")`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Errors and Exceptions（https://docs.python.org/3/tutorial/errors.html ），2026-10-25 访问。

## 输入输出

> [!example]+ 最常用写法
> ```python
> name = input("请输入名字: ")      # 返回字符串
> age = int(input("年龄: "))        # 手动转成整数
> print("a", "b", sep=",", end="")  # 控制分隔符和结尾
> ```

**用途**：`input()` 读一行输入，`print()` 输出。

**易错点**：`input()` 返回的永远是**字符串**，数字运算前要 `int()`/`float()` 转换。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · input / print（https://docs.python.org/3/library/functions.html#print ），2026-10-25 访问。

## 类型转换

> [!example]+ 最常用写法
> ```python
> int("42")      # 42
> float("3.14")  # 3.14
> str(123)       # "123"
> list("abc")    # ['a', 'b', 'c']
> ```

**用途**：在数字、字符串、容器之间转换。

**易错点**：`int("abc")` 会抛 `ValueError`；`int("3.14")` 也不行，要先 `float`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · 内置函数（https://docs.python.org/3/library/functions.html ），2026-10-25 访问。

## 相关链接

- [[Python-列表与元组]]
- [[Python-字符串]]
- [[Python-字典与集合]]
- [[Python-函数]]
