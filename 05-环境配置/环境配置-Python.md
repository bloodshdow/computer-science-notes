---
title: 环境配置-Python
type: cheatsheet
tags:
  - 速查
  - 主题/环境配置
  - 语言/Python
---

# 环境配置-Python

> [!note] 定位
> 从零装好 Python 开发环境，Windows 和 Linux 对照。虚拟环境（venv）是重点，因为最容易被忘记。装好之后怎么用 pip 见 [[Python-虚拟环境与pip]]。

## Windows 安装 Python

> [!example]+ 步骤
> ```text
> 1. 到 python.org/downloads 下载 Windows 64 位安装包
> 2. 运行安装器，勾选底部的 "Add python.exe to PATH"（关键！）
> 3. 点 Install Now
> 4. 验证：命令行输入 python --version 能打印版本号
> ```

**用途**：装 Python 本体。

**易错点**：
- **一定要勾 "Add to PATH"**，否则命令行找不到 `python`，后面全乱。
- 装完新开一个终端再验证，旧终端可能没刷新环境变量。

**版本/平台**：Python 3.13（Windows 10/11）。

**来源**：Python 官方文档（https://docs.python.org/3/using/windows.html ），2026-10-25 访问。

## Linux（Ubuntu 26.04）安装 Python

> [!example]+ 最常用写法
> ```bash
> sudo apt update
> sudo apt install python3 python3-pip python3-venv   # 三个都要
> python3 --version          # 验证
> ```

**用途**：Ubuntu 通常自带 python3，但要补装 pip 和 venv。

**易错点**：
- Linux 上命令是 `python3` 而不是 `python`（`python` 可能指向旧版或不存在）。
- `python3-venv` 是虚拟环境模块，**不装的话 venv 命令会报错**，这是最常见的坑。

**版本/平台**：Ubuntu 26.04。

**来源**：Ubuntu 官方文档（https://help.ubuntu.com/community/Python ），2026-10-25 访问。

## 虚拟环境 venv（重点，容易忘）

### 逻辑

虚拟环境 = 每个项目一个**独立的 Python 环境**，装包互不干扰。为什么需要？因为不同项目可能要不同版本的同一个包，全装全局会打架。

### 创建与激活

> [!example]+ 最常用写法
> ```bash
> # 在项目目录下创建名为 .venv 的环境
> python -m venv .venv
>
> # 激活（Windows，cmd/PowerShell）
> .venv\Scripts\activate
>
> # 激活（Linux / macOS）
> source .venv/bin/activate
>
> # 激活成功后，命令行前面会出现 (.venv) 前缀
> # 退出
> deactivate
> ```

**用途**：每个项目一个独立环境，装包不会污染全局。

**易错点（都是高频坑）**：
- **激活路径两端不同**：Windows 是 `.venv\Scripts\activate`，Linux 是 `.venv/bin/activate`。
- 看到命令行前缀 `(.venv)` 才说明激活成功；没出现就是没激活，`pip install` 会装到全局。
- 每次新开终端都要**重新激活**（这不是永久的）。
- Windows PowerShell 下可能要用 `.venv\Scripts\Activate.ps1`，且执行策略限制时会报错。

### 在 VSCode 里用虚拟环境

> [!note]- VSCode 选解释器
> 1. 装好 `.venv` 后，`Ctrl+Shift+P` → 输入 "Python: Select Interpreter"。
> 2. 选择带 `.venv` 的那一项（路径里能看到 `.venv`）。
> 3. 之后 VSCode 的终端和运行都会自动用这个环境，不用手动 activate。

## pip 装包与镜像（已配置，仅提示）

> [!example]+ 最常用写法
> ```bash
> pip install 包名          # 装包（记得先激活虚拟环境）
> pip install -r requirements.txt   # 按清单装
> ```

**用途**：装第三方库。你已配好国内镜像源，正常 `pip install` 即可。

**易错点**：装包前先确认终端有 `(.venv)` 前缀，否则装到全局去。

**版本/平台**：pip。

**来源**：Python 官方文档（https://packaging.python.org/ ），2026-10-25 访问。

## 相关链接

- [[Python-虚拟环境与pip]]
- [[环境配置-VSCode]]
- [[环境配置-C与Cpp]]
- [[Python-基础语法]]
