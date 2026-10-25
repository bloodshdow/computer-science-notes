---
title: Python-字符串
type: cheatsheet
tags:
  - 速查
  - 语言/Python
---

# Python-字符串

> [!warning] 两个易拼错的方法名
> 课堂笔记里写的是 `startwith` / `endwith`，正确拼写是 **`startswith`** / **`endswith`**（都有 `s`）。查前后缀判断时别拼错。

## 创建字符串

> [!example]+ 最常用写法
> ```python
> s1 = 'hello'
> s2 = "world"
> s3 = '''多行
> 字符串'''
> s4 = str(123)        # '123'
> ```

**用途**：单引号、双引号、三引号都能建字符串；`str()` 把对象转成字符串。

**易错点**：三引号 `'''...'''` 可跨多行；`str()` 转数字是常用写法。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Text Sequence Type — str（https://docs.python.org/3/library/stdtypes.html#textseq ），2026-10-25 访问。

## 索引与切片

> [!example]+ 最常用写法
> ```python
> s = "hello"
> s[0]        # 'h'
> s[-1]       # 'o'
> s[1:3]      # 'el'，end 不包含
> s[::-1]     # 'olleh'，倒序
> ```

**用途**：与列表相同，按 `[start:end:step]` 取子串。

**易错点**：字符串**不可变**，`s[0] = 'H'` 会报 `TypeError`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Text Sequence Type — str（同上），2026-10-25 访问。

## 常用运算符

> [!example]+ 最常用写法
> ```python
> s = "hello"
> len(s)             # 5，长度
> "ell" in s         # True，是否包含
> s + " world"       # "hello world"，拼接
> s * 2              # "hellohello"，重复
> ```

**用途**：长度、成员判断、拼接、重复。

**易错点**：`in` 判断子串是否存在；`+` 只能拼字符串，`"a" + 1` 会报错。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · Common String Operations（https://docs.python.org/3/library/string.html ），2026-10-25 访问。

## 大小写转换

> [!example]+ 最常用写法
> ```python
> s = "hello World"
> s.upper()       # "HELLO WORLD"
> s.lower()       # "hello world"
> s.capitalize()  # "Hello world"，仅首字母大写
> s.title()       # "Hello World"，每个单词首字母大写
> s.swapcase()    # 交换大小写
> s.casefold()    # 更彻底的小写，适合不区分大小写比较
> ```

**用途**：大小写转换。做不区分大小写的比较用 `casefold` 比 `lower` 更稳。

**易错点**：这些方法都**返回新字符串**，不修改原字符串。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · String Methods（https://docs.python.org/3/library/stdtypes.html#string-methods ），2026-10-25 访问。

## 查找与统计

> [!example]+ 最常用写法
> ```python
> s = "hello world"
> s.find("o")      # 4，第一个匹配下标；找不到返回 -1
> s.rfind("o")     # 7，从右边找
> s.index("o")     # 4，同 find 但找不到抛 ValueError
> s.count("o")     # 2，统计出现次数
> ```

**用途**：查找子串位置、统计次数。

**易错点**：
- `find` 找不到返回 `-1`；`index` 找不到抛异常，注意区分。
- 判断是否"包含"优先用 `"sub" in s`，比 `find != -1` 更直观。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · String Methods（同上），2026-10-25 访问。

## 前后缀判断

> [!example]+ 最常用写法
> ```python
> s = "hello.txt"
> s.startswith("he")     # True
> s.endswith(".txt")     # True
> ```

**用途**：判断开头/结尾，常用于文件扩展名、URL 判断。

**易错点**：方法名是 `startswith` / `endswith`，末尾的 `s` 容易漏。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · String Methods（同上），2026-10-25 访问。

## 判断类方法

> [!example]+ 最常用写法
> ```python
> "abc".isalpha()      # True  是否全是字母
> "123".isdigit()      # True  是否全是数字
> "abc123".isalnum()   # True  是否字母或数字
> "  ".isspace()       # True  是否全是空白
> "abc".islower()      # True  是否全是小写
> "ABC".isupper()      # True  是否全是大写
> ```

**用途**：判断字符串内容性质（字母/数字/空白/大小写）。

**易错点**：
- `isdigit` 只认十进制数字字符，`"²".isdigit()` 为 True 但 `"²".isdecimal()` 为 False。
- `isnumeric` 范围 > `isdigit` > `isdecimal`，后者最严格。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · str.isdigit 等（https://docs.python.org/3/library/stdtypes.html#str.isdigit ），2026-10-25 访问。

> [!note]- 进阶：isnumeric / isdecimal / isidentifier / isprintable
> ```python
> "12".isnumeric()       # True，范围比 isdigit 更广
> "12".isdecimal()       # True，只认十进制数字，最严格
> "abc".isidentifier()   # True，是否合法标识符
> "a\n".isprintable()    # False，是否可打印（换行符不可打印）
> ```

## 清理空白与替换

> [!example]+ 最常用写法
> ```python
> "  hello  ".strip()          # "hello"，去两端空白
> "xxhixx".strip("x")          # "hi"，去两端指定字符
> "hello".replace("l", "L")    # "heLLo"
> "hello".replace("l", "L", 1) # "heLlo"，只替换 1 次
> ```

**用途**：去空白、去指定字符、替换子串。

**易错点**：
- `strip(chars)` 是"删掉两端出现在 chars 里的所有字符"，不是删完整子串。
- `replace` 默认全部替换，第三个参数限制次数。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · String Methods（同上），2026-10-25 访问。

> [!note]- 进阶：lstrip / rstrip / expandtabs
> ```python
> "  hi  ".lstrip()        # "hi  "，只去左边
> "  hi  ".rstrip()        # "  hi"，只去右边
> "a\tb".expandtabs(4)     # "a   b"，把 \t 展开成空格
> ```

## 拆分与合并

> [!example]+ 最常用写法
> ```python
> "a,b,c".split(",")       # ['a', 'b', 'c']
> "a b  c".split()         # ['a', 'b', 'c']，无参按任意空白拆
> "a,b,c".split(",", 1)    # ['a', 'b,c']，最多拆 1 次
> "-".join(["a", "b"])     # "a-b"
> "a,b,c".partition(",")   # ('a', ',', 'b,c')，切成三元组
> ```

**用途**：拆字符串成列表、把列表拼成字符串。

**易错点**：
- `split()` 无参会把连续空白当一个分隔符；`split(" ")` 则保留空串。
- `join` 是"连接符.join(可迭代对象)"，元素必须是字符串，数字要先 `str()`。
- `partition` 固定返回三元组 `(左边, 分隔符, 右边)`，只切第一次。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · str.split / str.join（https://docs.python.org/3/library/stdtypes.html#str.split ），2026-10-25 访问。

> [!note]- 进阶：rsplit / rpartition / splitlines
> ```python
> "a,b,c".rsplit(",", 1)     # ['a,b', 'c']，从右边拆
> "a,b,c".rpartition(",")    # ('a,b', ',', 'c')
> "a\nb\r\nc".splitlines()   # ['a', 'b', 'c']，按行拆，识别 \n \r \r\n
> "a\nb\n".splitlines(True)  # ['a\n', 'b\n']，保留换行符
> ```

## 格式化

> [!example]+ 最常用写法
> ```python
> name = "Alice"
> f"{name}!"                    # "Alice!"，f-string 最推荐
> "{} {}".format("a", "b")      # "a b"
> "{name}".format(name="Alice") # "Alice"
> ```

**用途**：把变量插进字符串。优先用 f-string（`f"..."`）。

**易错点**：f-string 需要 Python 3.6+；`format` 是旧写法但兼容性广。

**版本/平台**：Python 3.6+（f-string）。

**来源**：Python 官方文档 · Formatted string literals（https://docs.python.org/3/reference/lexical_analysis.html#f-strings ），2026-10-25 访问。

## 编码与解码

> [!example]+ 最常用写法
> ```python
> b = "你好".encode("utf-8")   # b'\xe4\xbd\xa0\xe5\xa5\xbd'
> b.decode("utf-8")            # '你好'
> ```

**用途**：字符串 ↔ 字节串转换，网络传输、文件读写常用。

**易错点**：`encode` 得到的是 `bytes` 类型（前面有 `b`）；`decode` 的编码必须和 `encode` 一致，否则报 `UnicodeDecodeError`。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · str.encode（https://docs.python.org/3/library/stdtypes.html#str.encode ），2026-10-25 访问。

## 相关链接

- [[Python-列表与元组]]
- [[Python-字典与集合]]
- [[Python-基础语法]]
