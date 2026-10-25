---
title: Python-列表与元组
type: cheatsheet
tags:
  - 速查
  - 语言/Python
---

# Python-列表与元组

> [!warning] 变量名建议
> 课堂笔记里常用 `list` 当变量名，但 `list` 是内置函数名。覆盖它之后 `list("abc")` 会报错。建议改用 `lst`、`nums` 等。

## 列表的创建

> [!example]+ 最常用写法
> ```python
> lst = [1, 2, 3]
> lst = list("abc")                    # ['a', 'b', 'c']，把可迭代对象转成列表
> lst = [i for i in range(2, 5)]       # 列表推导式：[2, 3, 4]
> ```

**用途**：创建有序、可变的序列，是 Python 最常用的容器。

**易错点**：
- `list` 是内置函数名，不要用它当变量名。
- `list(5)` 会报错，因为 `list()` 需要可迭代对象（整数不可迭代）。

**版本/平台**：Python 3.x（3.10+）。

**来源**：Python 官方文档 · Built-in Types — Lists（https://docs.python.org/3/library/stdtypes.html#lists ），2026-10-25 访问。

## 索引与切片

> [!example]+ 最常用写法
> ```python
> lst = [0, 1, 2, 3, 4]
> lst[0]        # 0，索引从 0 开始
> lst[-1]       # 4，倒数第一个
> lst[1:3]      # [1, 2]，end 不包含
> lst[::-1]     # [4, 3, 2, 1, 0]，步长 -1 即倒序
> ```

**用途**：按下标取单个元素，或用 `[start:end:step]` 取子序列。

**易错点**：
- 切片 `lst[1:3]` 的 `end` 不包含，只取到下标 2。
- `step` 为负数时 `start`、`end` 方向要反过来，如 `lst[-1:-3:-1]`。
- 越界索引会报 `IndexError`；但切片越界不会报错，只会返回空或截断。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Common Sequence Operations（https://docs.python.org/3/library/stdtypes.html#typesseq-common ），2026-10-25 访问。

## 修改列表

> [!example]+ 最常用写法
> ```python
> lst = [1, 2, 3, 4]
> lst[0] = 200            # 按下标改：[200, 2, 3, 4]
> lst[1:3] = [20, 30]     # 切片批量改：[200, 20, 30, 4]
> lst += [5]              # 原地追加，等于 lst.extend([5])
> lst = lst + [6]         # 生成新列表再赋值，原列表不变
> ```

**用途**：通过索引、切片或运算符增改元素。

**易错点**：
- `lst + [1]` 是"新建列表"，`lst += [1]` 是"原地扩展"，行为不同。
- 列表没有"减法"运算符，`lst - [1]` 会报错，删除请用 `del` 或 `remove`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Mutable Sequence Types（https://docs.python.org/3/library/stdtypes.html#mutable-sequence-types ），2026-10-25 访问。

## 常用增删方法

> [!example]+ 最常用写法
> ```python
> lst = [2, 3, 4, 5]
> lst.append(6)           # 末尾添加：[2,3,4,5,6]
> lst.extend([7, 8])      # 批量添加：[2,3,4,5,6,7,8]
> lst.insert(0, 1)        # 指定位置插入：[1,2,3,...]
> lst.remove(3)           # 删除第一个等于 3 的值
> x = lst.pop()           # 删除并返回末尾元素；pop(i) 删除下标 i
> del lst[0]              # 删除指定下标
> lst.clear()             # 清空
> ```

**用途**：列表元素的添加与删除。

**易错点**：
- `remove(x)` 只删第一个匹配值；不存在会报 `ValueError`。
- `pop()` 无参删末尾；`pop(i)` 删下标 `i`，越界报 `IndexError`。
- `append` 只加一个元素，`extend` 才批量加，别混用。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Lists（https://docs.python.org/3/tutorial/datastructures.html ），2026-10-25 访问。

## 排序与反转

> [!example]+ 最常用写法
> ```python
> lst = [3, 1, 2]
> lst.sort()              # 原地升序，返回 None
> new = sorted(lst)       # 返回新列表，原列表不变
> lst.sort(reverse=True)  # 降序
> lst.reverse()           # 直接反转顺序，不排序
> ```

**用途**：排序与逆序。

**易错点**：
- `sort()` 是方法、原地改且返回 `None`；`sorted()` 是函数、返回新列表。别写成 `lst = lst.sort()`。
- `reverse=True` 是"排完序再倒过来"，不是"倒着排"；`reverse()` 只是反转顺序，完全不排序。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Sorting HOW TO（https://docs.python.org/3/howto/sorting.html ），2026-10-25 访问。

## 拷贝（浅拷贝与深拷贝）

> [!example]+ 最常用写法
> ```python
> import copy
> a = [1, 2, 3, [4, 5, 6]]
> b = copy.copy(a)        # 浅拷贝：只复制外层
> c = copy.deepcopy(a)    # 深拷贝：内层列表也复制
> a[3].append(99)
> print(b)                # [1, 2, 3, [4, 5, 6, 99]]，内层共享
> print(c)                # [1, 2, 3, [4, 5, 6]]，内层独立
> ```

**用途**：复制列表时区分"复制引用"和"复制值"。

**易错点**：
- 直接 `b = a` 是赋值，两个名字指向同一对象，改一个另一个也变。
- 浅拷贝 `copy.copy` 只复制外层，内层嵌套列表仍是共享的。
- 深拷贝 `copy.deepcopy` 会连内层一起复制，最彻底但更慢。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · copy 模块（https://docs.python.org/3/library/copy.html ），2026-10-25 访问。

## 元组的创建

> [!example]+ 最常用写法
> ```python
> t = (1, 2, 3)
> t = 1, 2, 3            # 括号可省略
> t = (1,)               # 单元素元组必须有逗号
> t = ()                 # 空元组
> t = tuple([1, 2])      # 从可迭代对象转换：(1, 2)
> ```

**用途**：创建不可变序列，常用于函数返回多个值、作为字典键。

**易错点**：
- 单元素必须写 `(1,)`，写成 `(1)` 会被当成数字 `1` 而不是元组。
- 元组不可增删改元素，但里面的可变对象（如列表）仍可改。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Tuples（https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences ），2026-10-25 访问。

## 元组的"改"操作

> [!example]+ 最常用写法
> ```python
> t = (1, 2, 3)
> t2 = t + (4, 5)              # 拼接：(1, 2, 3, 4, 5)
> t = t[:1] + (99,) + t[2:]    # 替换：得到 (1, 99, 3)
> t = t[:1] + t[2:]            # 删除：得到 (1, 3)
> ```

**用途**：元组本身不可变，这些操作本质是"生成新元组再赋值"。

**易错点**：
- 元组没有 `append`、`remove` 等原地方法，只能用拼接/切片构造新元组。
- `(99)` 不是元组，拼接时单元素要写 `(99,)`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Tuples（同上），2026-10-25 访问。

## 元组 ↔ 列表互转

> [!example]+ 最常用写法
> ```python
> t = (1, 2, 3)
> lst = list(t)        # (1,2,3) -> [1,2,3]
> lst[0] = 100
> t = tuple(lst)       # [100,2,3] -> (100,2,3)
> ```

**用途**：需要修改时先转列表，改完再转回元组。

**易错点**：转换生成的是新对象，原对象不变。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · list() / tuple() 构造器（https://docs.python.org/3/library/stdtypes.html ），2026-10-25 访问。

## 元组常用方法

> [!example]+ 最常用写法
> ```python
> t = (1, 2, 2, 3)
> t.count(2)    # 2，统计 2 出现次数
> t.index(2)    # 1，第一个 2 的下标
> ```

**用途**：计数与查找下标。

**易错点**：`index(x)` 找不到会报 `ValueError`（不像 `str.find` 返回 -1）。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Tuples（同上），2026-10-25 访问。

## 解包与交换

> [!example]+ 最常用写法
> ```python
> a, b, c = (1, 2, 3)     # 解包：a=1 b=2 c=3
> a, *b = (1, 2, 3, 4)    # 星号收集剩余：a=1 b=[2,3,4]
> a, b = b, a             # 交换变量，无需临时变量
> ```

**用途**：一次把序列元素赋给多个变量。

**易错点**：
- 解包时变量数量必须和元素数量一致，否则 `ValueError`。
- `*` 号把剩余元素收集成**列表**。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Tuples and Sequences（https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences ），2026-10-25 访问。

## 相关链接

- [[Python-字符串]]
- [[Python-字典与集合]]
- [[Python-基础语法]]
- [[数据结构-数组与动态数组]]
- [[Cpp-STL常用容器]]
- [[Java-集合框架]]
