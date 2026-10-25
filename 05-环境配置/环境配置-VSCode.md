---
title: 环境配置-VSCode
type: cheatsheet
tags:
  - 速查
  - 主题/环境配置
  - 工具/VSCode
---

# 环境配置-VSCode

> [!note] 定位
> 你的主力编辑器（Windows 大电脑和 Linux 小电脑都用它）。这里是装好后最常用的配置。

## 安装 VSCode

> [!example]+ 步骤
> ```text
> Windows：官网 code.visualstudio.com 下载安装包，双击装
> Ubuntu 26.04：下载 .deb 包后 sudo apt install ./code.deb
>     （或用 snap：sudo snap install code --classic）
> ```

**用途**：装编辑器本体。

**易错点**：Ubuntu 装 `.deb` 用 `sudo apt install ./code.deb`（注意 `./`），见 [[Linux-包管理]]。

**版本/平台**：VSCode（Windows/Linux 通用）。

**来源**：VSCode 官方文档（https://code.visualstudio.com/docs ），2026-10-25 访问。

## 必备扩展（按语言装）

> [!example]+ 最常用写法
> ```text
> 左侧扩展图标（或 Ctrl+Shift+X）搜索安装：
> - Python：装 "Python"（微软官方）+ "Pylance"
> - C/C++：装 "C/C++"（微软官方）
> - 中文界面：装 "Chinese (Simplified)"
> - 代码格式化：装 "Prettier"（前端用）
> ```

**用途**：VSCode 本身是空壳，功能靠扩展。装对应语言的扩展才能有补全、调试。

**易错点**：扩展名要认准**微软官方**的那个（发布者带勾/微软标记），同名山寨扩展很多。

**版本/平台**：VSCode。

**来源**：VSCode 官方文档 · Marketplace（https://code.visualstudio.com/docs/editor/extension-marketplace ），2026-10-25 访问。

## 最常用的快捷键

> [!example]+ 最常用写法
> ```text
> Ctrl+Shift+P     命令面板（万能入口，记不住功能就先按它）
> Ctrl+P           快速打开文件
> Ctrl+`           打开/关闭终端
> Ctrl+B           开关侧边栏
> Ctrl+Shift+X     扩展面板
> Ctrl+,           打开设置
> ```

**用途**：核心是 `Ctrl+Shift+P` 命令面板——几乎所有操作都能从里面搜到。

**易错点**：记不住具体功能时，直接 `Ctrl+Shift+P` 搜关键词（如 "interpreter"、"format"）。

**版本/平台**：VSCode。

**来源**：VSCode 官方文档 · Keyboard shortcuts（https://code.visualstudio.com/docs/getstarted/keybindings ），2026-10-25 访问。

## 配置终端

> [!example]+ 最常用写法
> ```text
> 1. Ctrl+` 打开终端
> 2. 右上角下拉可选终端类型（Windows 可选 PowerShell、cmd、Git Bash、WSL）
> 3. 想默认用 WSL 或 Git Bash：Ctrl+Shift+P → "Terminal: Select Default Profile"
> ```

**用途**：在编辑器里直接跑命令。

**易错点**：Windows 下用 WSL 写 C++ 时，把默认终端设成 WSL，编译命令就和 Linux 一致。

**版本/平台**：VSCode。

**来源**：VSCode 官方文档 · Integrated Terminal（https://code.visualstudio.com/docs/terminal/basics ），2026-10-25 访问。

## 选 Python 解释器

> [!example]+ 最常用写法
> ```text
> Ctrl+Shift+P → "Python: Select Interpreter" → 选带 .venv 的那一项
> ```

**用途**：让 VSCode 用你项目的虚拟环境，而不是全局 Python。

**易错点**：忘记选会导致 `import` 找不到虚拟环境里装的包。详见 [[环境配置-Python]]。

**版本/平台**：VSCode + Python 扩展。

**来源**：VSCode 官方文档 · Python（https://code.visualstudio.com/docs/python/environments ），2026-10-25 访问。

## 相关链接

- [[环境配置-Python]]
- [[环境配置-C与Cpp]]
- [[环境配置-WSL]]
