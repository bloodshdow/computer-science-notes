---
title: Python-常用库
type: cheatsheet
tags:
  - 速查
  - 语言/Python
---

# Python-常用库

> [!note] 定位
> 只列最常用的标准库，每个给一个最小示例。第三方库安装见 [[Python-虚拟环境与pip]]。

## os 与 sys

> [!example]+ 最常用写法
> ```python
> import os, sys
> os.getcwd()              # 当前工作目录
> os.path.join("a", "b")   # "a/b"（跨平台拼路径）
> os.path.exists("x.txt")  # 判断文件是否存在
> os.makedirs("a/b")       # 递归建目录
> sys.argv                 # 命令行参数列表，argv[0] 是脚本名
> sys.exit(0)              # 退出程序
> ```

**用途**：操作系统交互（路径、文件、目录）与解释器信息。

**易错点**：
- 拼路径用 `os.path.join`，别手写 `/` 或 `\`，跨平台才稳。
- `sys.argv` 第一个元素是脚本名，真正的参数从 `argv[1]` 开始。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · os / sys（https://docs.python.org/3/library/os.html ），2026-10-25 访问。

## pathlib

> [!example]+ 最常用写法
> ```python
> from pathlib import Path
> p = Path("a") / "b.txt"   # 用 / 拼路径，更现代
> p.exists()                # 是否存在
> p.read_text()             # 读文本
> p.write_text("hi")        # 写文本
> p.suffix                  # ".txt"
> ```

**用途**：面向对象的路径处理，比 `os.path` 更推荐（Python 3.4+）。

**易错点**：`Path` 对象不是字符串，需要字符串时用 `str(p)`。

**版本/平台**：Python 3.4+。

**来源**：Python 官方文档 · pathlib（https://docs.python.org/3/library/pathlib.html ），2026-10-25 访问。

## json

> [!example]+ 最常用写法
> ```python
> import json
> json.dumps({"a": 1})          # '{"a": 1}'，对象→字符串
> json.loads('{"a": 1}')        # {'a': 1}，字符串→对象
> json.dump(obj, open("x.json", "w"))   # 写文件
> obj = json.load(open("x.json"))       # 读文件
> ```

**用途**：JSON 序列化与反序列化，接口交互、配置读写必备。

**易错点**：
- `dump`/`load` 是读写**文件**，`dumps`/`loads` 是处理**字符串**，别混。
- Python 的 `tuple` 会被序列化成 JSON 数组，反序列化回来是 `list`。
- 中文默认转义，用 `json.dumps(x, ensure_ascii=False)` 保留可读中文。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · json（https://docs.python.org/3/library/json.html ），2026-10-25 访问。

## re 正则表达式

> [!example]+ 最常用写法
> ```python
> import re
> re.search(r"\d+", "abc123")      # 找到第一个数字串，返回 Match 或 None
> re.findall(r"\d+", "a1b22")      # ['1', '22']，找全部
> re.sub(r"\s+", " ", "a  b")      # "a b"，替换
> m = re.match(r"(\w+)@(\w+)", "x@y")
> m.group(1)                       # "x"，取捕获组
> ```

**用途**：字符串的模式匹配、提取、替换。

**易错点**：
- 用原始字符串 `r"..."`，避免 `\` 被转义。
- `match` 只从**开头**匹配，`search` 在**任意位置**找，`findall` 找全部。
- `search` 找不到返回 `None`，调用 `.group()` 前要判空。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · re（https://docs.python.org/3/library/re.html ），2026-10-25 访问。

## datetime

> [!example]+ 最常用写法
> ```python
> from datetime import datetime
> now = datetime.now()                 # 当前时间
> now.strftime("%Y-%m-%d %H:%M:%S")    # 格式化成字符串
> datetime.strptime("2026-01-01", "%Y-%m-%d")   # 字符串→时间
> ```

**用途**：日期时间的获取、格式化与解析。

**易错点**：`strftime` 是格式化输出，`strptime` 是解析输入，两个方向别搞反。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · datetime（https://docs.python.org/3/library/datetime.html ），2026-10-25 访问。

## math 与 random

> [!example]+ 最常用写法
> ```python
> import math, random
> math.sqrt(16)          # 4.0
> math.floor(3.7)        # 3
> math.ceil(3.2)         # 4
> random.randint(1, 10)  # 1~10 随机整数（含两端）
> random.choice([1, 2, 3])  # 随机选一个
> ```

**用途**：数学运算与随机数。

**易错点**：`random.randint(a, b)` 是**闭区间**，含 a 和 b；`random.random()` 返回 `[0,1)` 浮点。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · math / random（https://docs.python.org/3/library/math.html ），2026-10-25 访问。

## collections

> [!example]+ 最常用写法
> ```python
> from collections import Counter, defaultdict, deque
> Counter("aab").most_common(1)      # [('a', 2)]，计数
> d = defaultdict(list)              # 访问不存在的键自动给默认值
> q = deque([1, 2]); q.appendleft(0) # 两端操作高效
> ```

**用途**：增强版容器。`Counter` 计数、`defaultdict` 免判键、`deque` 双端队列。

**易错点**：`defaultdict` 要传一个**工厂函数**（如 `list`），不是值（不是 `[]`）。

**版本/平台**：Python 3.x。

**来源**：Python 官方文档 · collections（https://docs.python.org/3/library/collections.html ），2026-10-25 访问。

## 相关链接

- [[Python-基础语法]]
- [[Python-虚拟环境与pip]]
- [[Python-函数]]
