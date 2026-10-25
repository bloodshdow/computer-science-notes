---
title: 环境配置-C与Cpp
type: cheatsheet
tags:
  - 速查
  - 主题/环境配置
  - 语言/Cpp
---

# 环境配置-C与Cpp

> [!note] 定位
> 装好能编译运行 C/C++ 的环境。你的情况：Linux 小电脑直接用 gcc/g++；Windows 大电脑靠 WSL（或以后换 Visual Studio）。三种方式都列出来。

## Linux（Ubuntu 26.04）装 gcc/g++

> [!example]+ 最常用写法
> ```bash
> sudo apt update
> sudo apt install build-essential   # 一次装齐 gcc、g++、make 等
> gcc --version    # 验证 C 编译器
> g++ --version    # 验证 C++ 编译器
> ```

**用途**：`build-essential` 是编译 C/C++ 的必备元包，装上它编译器、make、头文件全齐。

**易错点**：只装 `gcc` 不够，C++ 要 `g++`；直接装 `build-essential` 最省心。

**版本/平台**：Ubuntu 26.04 / GCC。

**来源**：Ubuntu 官方文档（https://help.ubuntu.com/community/CompilingEasyHowTo ），2026-10-25 访问。

## Windows 直接装 MinGW-w64

> [!example]+ 步骤
> ```text
> 1. 到 winlibs.com 或 mingw-w64 官网下载 MinGW-w64（选 64 位、含 g++ 的包）
> 2. 解压到 C:\mingw64（或任意无空格路径）
> 3. 把 C:\mingw64\bin 加到系统 PATH
> 4. 验证：新开终端输入 g++ --version
> ```

**用途**：Windows 原生编译 C/C++，不依赖 WSL。

**易错点**：
- 装完要把 `bin` 目录加到 PATH，否则命令行找不到 `g++`。
- 路径最好**不含空格和中文**，避免编译脚本出错。
- 更省事的替代：用 MSYS2（`pacman -S mingw-w64-x86_64-gcc`）。

**版本/平台**：Windows 10/11 / MinGW-w64。

**来源**：MinGW-w64 文档（https://www.mingw-w64.org/ ），2026-10-25 访问。

## 用 WSL 编译（你大电脑的方式）

> [!example]+ 最常用写法
> ```bash
> # 在 WSL 的 Linux 里，和真机 Linux 完全一样
> sudo apt install build-essential
> # 在 WSL 里编译
> g++ main.cpp -o main
> # 从 Windows 访问 WSL 文件：资源管理器地址栏输 \\wsl$
> ```

**用途**：WSL 就是 Windows 里的 Linux，编译环境和真机 Linux 一致，装了就能直接 `g++`。

**易错点**：
- WSL 里装包走 `apt`，命令和 Linux 完全相同（见上节）。
- WSL 的编译结果在 WSL 里运行，不是 Windows 原生 exe。
- WSL 安装配置见 [[环境配置-WSL]]。

**版本/平台**：WSL2 / Ubuntu。

**来源**：微软 WSL 文档（https://learn.microsoft.com/zh-cn/windows/wsl/ ），2026-10-25 访问。

## 以后用 Visual Studio（完整 IDE）

> [!note]- VS 和 VSCode 的区别
> - **VSCode**：轻量编辑器，装插件才能编译，灵活但需自己配。
> - **Visual Studio**（注意没有 "Code"）：微软的完整 IDE，装 C++ 工作负载后开箱即用，但重、只支持 Windows。
> - 你要写 C++ 且想要"点一下就能编译调试"，VS 更省心。安装时勾选 **"使用 C++ 的桌面开发"** 工作负载即可。

## 相关链接

- [[环境配置-WSL]]
- [[环境配置-VSCode]]
- [[Cpp-编译]]
- [[Cpp-基础语法]]
