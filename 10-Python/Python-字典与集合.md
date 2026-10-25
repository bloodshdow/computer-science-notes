---
title: Python-字典与集合
type: cheatsheet
tags:
  - 速查
  - 语言/Python
---

# Python-字典与集合

## 字典的创建

> [!example]+ 最常用写法
> ```python
> d = {"name": "Alice", "age": 20}
> d = dict(name="Alice", age=20)     # 关键字方式
> d = dict([("name", "Alice")])      # 由键值对列表构造
> d = {"a": {"x": 1}}                # 可以嵌套
> ```

**用途**：存储键值对（key → value），按键快速查找，键必须唯一且不可变。

**易错点**：
- 键必须**不可变**（字符串、数字、元组可以；列表不行）。
- `dict` 也是内置名，别当变量名用。

**版本/平台**：Python 3.x（3.7+ 字典保持插入顺序）。

**来源**：Python 官方文档 · dict（https://docs.python.org/3/library/stdtypes.html#dict ），2026-10-25 访问。

## 访问与修改

> [!example]+ 最常用写法
> ```python
> d = {"a": 1}
> d["a"]            # 1，用键访问；键不存在抛 KeyError
> d.get("b", 0)     # 0，键不存在返回默认值
> d["b"] = 2        # 新增或修改
> del d["a"]        # 删除键值对
> ```

**用途**：按键读、写、删。

**易错点**：
- `d[key]` 键不存在会抛 `KeyError`；不确定是否存在用 `d.get(key, 默认值)`。
- 赋值 `d[key] = v` 键存在是"改"，不存在是"增"。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · dict（同上），2026-10-25 访问。

## 删除与取出

> [!example]+ 最常用写法
> ```python
> d = {"a": 1, "b": 2}
> d.pop("a")        # 1，删除并返回；不存在抛 KeyError
> d.pop("x", 0)     # 0，不存在返回默认值
> d.popitem()       # ('b', 2)，删除并返回最后一项（键值对元组）
> d.clear()         # 清空
> ```

**用途**：删除时拿到被删的值。

**易错点**：`popitem` 返回的是 `(key, value)` 元组；空字典调用会报 `KeyError`。

**版本/平台**：Python 3.x（3.7+ `popitem` 删最后插入项）。

**来源**：Python 官方文档 · dict（同上），2026-10-25 访问。

## 键、值、项与遍历

> [!example]+ 最常用写法
> ```python
> d = {"a": 1, "b": 2}
> d.keys()       # dict_keys(['a', 'b'])
> d.values()     # dict_values([1, 2])
> d.items()      # dict_items([('a', 1), ('b', 2)])
>
> for k in d:            # 默认遍历键
>     print(k, d[k])
> for k, v in d.items(): # 同时拿键和值，最常用
>     print(k, v)
> "a" in d               # True，判断键是否存在
> ```

**用途**：遍历字典、判断键是否存在。

**易错点**：
- `for k in d` 遍历的是**键**，不是值。
- 要同时拿键和值用 `d.items()`。
- `x in d` 检查的是**键**，不是值。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · dict（同上），2026-10-25 访问。

## 字典推导式

> [!example]+ 最常用写法
> ```python
> d = {x: x * x for x in range(3)}   # {0:0, 1:1, 2:4}
> ```

**用途**：一行构造字典。

**易错点**：推导式里 `:` 左边是键、右边是值。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · dict displays（https://docs.python.org/3/reference/expressions.html#dictionary-displays ），2026-10-25 访问。

## 集合的创建

> [!example]+ 最常用写法
> ```python
> s = {1, 2, 3}
> empty = set()          # 空集合必须用 set()，{} 是空字典
> s = set([1, 2, 2, 3])  # {1, 2, 3}，自动去重
> ```

**用途**：存放**无序、不重复**的元素，常用于去重、成员判断。

**易错点**：
- `{}` 是空**字典**，空集合要用 `set()`。
- 集合元素也必须不可变（列表不能放进去）。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · set（https://docs.python.org/3/library/stdtypes.html#set ），2026-10-25 访问。

## 集合的增删

> [!example]+ 最常用写法
> ```python
> s = {1, 2}
> s.add(3)              # {1, 2, 3}，添加单个
> s.update([3, 4])      # 批量添加
> s.remove(2)           # 删除，不存在抛 KeyError
> s.discard(9)          # 删除，不存在也不报错
> x = s.pop()           # 随机删除一个并返回
> s.clear()             # 清空
> 2 in s                # True，判断是否存在
> ```

**用途**：集合元素增删与成员判断。

**易错点**：
- `remove` 不存在会报错，`discard` 不会。
- 集合无序，`pop` 删的是"某个"元素，不保证顺序。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · set（同上），2026-10-25 访问。

## 集合运算

> [!example]+ 最常用写法
> ```python
> a = {1, 2, 3}
> b = {2, 3, 4}
> a | b             # {1,2,3,4}，并集
> a & b             # {2,3}，交集
> a - b             # {1}，差集（a 有 b 无）
> a ^ b             # {1,4}，对称差（只在一方出现）
> a.issubset(b)     # False，a 是否 b 的子集
> a.issuperset(b)   # False
> a.isdisjoint(b)   # False，是否无交集
> ```

**用途**：集合间的并、交、差、对称差运算。

**易错点**：
- 运算符版（`|` `&` `-` `^`）要求两边都是集合；方法版（`union`/`intersection` 等）接受可迭代对象。
- `a - b` 是"a 有而 b 没有"，方向别搞反。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · set types（https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset ），2026-10-25 访问。

> [!note]- 进阶：方法版运算
> ```python
> a.union(b)                 # 并集，返回新集合
> a.intersection(b)          # 交集
> a.difference(b)            # 差集
> a.symmetric_difference(b)  # 对称差
> ```

## 集合推导式

> [!example]+ 最常用写法
> ```python
> s = {x * x for x in range(5)}   # {0, 1, 4, 9, 16}
> ```

**用途**：一行构造集合，同时自动去重。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · set displays（https://docs.python.org/3/reference/expressions.html#set-displays ），2026-10-25 访问。

## 不可变集合 frozenset

> [!example]+ 最常用写法
> ```python
> fs = frozenset([1, 2, 3])
> ```

**用途**：不可变的集合，可作为字典键或放进另一个集合。

**易错点**：`frozenset` 没有 `add`/`remove` 等修改方法。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · frozenset（https://docs.python.org/3/library/stdtypes.html#frozenset ），2026-10-25 访问。

## map 函数

> [!example]+ 最常用写法
> ```python
> nums = list(map(int, input().split()))   # 一行输入按空格拆成数字列表
> list(map(str.upper, ["a", "b"]))         # ['A', 'B']
> ```

**用途**：对可迭代对象的每个元素套同一个函数。`map(函数, 可迭代对象)` 返回迭代器，常用 `list()` 包一层。

**易错点**：`map` 返回的是迭代器，直接打印看不到内容，要 `list(...)` 转出来。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · map（https://docs.python.org/3/library/functions.html#map ），2026-10-25 访问。

## 相关链接

- [[Python-列表与元组]]
- [[Python-字符串]]
- [[Python-基础语法]]
- [[数据结构-散列表]]
- [[数据结构-查找算法]]
