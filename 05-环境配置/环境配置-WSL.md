---
title: 环境配置-WSL
type: cheatsheet
tags:
  - 速查
  - 主题/环境配置
  - 语言/Linux
---

# 环境配置-WSL

> [!note] 定位
> WSL（Windows Subsystem for Linux）让你在 Windows 里直接跑 Linux。你大电脑就是靠它写 C++。这里是安装和常用操作。

## 安装 WSL

> [!example]+ 最常用写法
> ```powershell
> # 在 Windows 的 PowerShell 或管理员终端里，一条命令装好（含 Ubuntu）
> wsl --install
> ```

**用途**：自动装好 WSL2 + 默认 Ubuntu 发行版，重启后设个用户名密码即可用。

**易错点**：
- 需要 Windows 10 2004+ 或 Windows 11。
- 装完会要求**重启**；重启后首次进入 Ubuntu 会要你设 Linux 用户名和密码。
- 如果 `wsl --install` 没装发行版，用 `wsl --install -d Ubuntu` 指定。

**版本/平台**：Windows 10/11 / WSL2。

**来源**：微软官方文档（https://learn.microsoft.com/zh-cn/windows/wsl/install ），2026-10-25 访问。

## 常用命令

> [!example]+ 最常用写法
> ```powershell
> wsl --list --verbose      # 查看装了哪些发行版、状态（缩写成 wsl -l -v）
> wsl --shutdown            # 关闭 WSL（释放内存）
> wsl -d Ubuntu             # 启动指定发行版
> ```

**用途**：管理 WSL 的启动和发行版。

**易错点**：`wsl` 单独运行会进入默认发行版的 shell；`wsl 命令` 能在不进入 shell 的情况下直接跑一条 Linux 命令。

**版本/平台**：WSL2。

**来源**：微软官方文档（https://learn.microsoft.com/zh-cn/windows/wsl/basic-commands ），2026-10-25 访问。

## 文件互通

> [!example]+ 最常用写法
> ```text
> # 从 Windows 访问 WSL 文件：资源管理器地址栏输入
> \\wsl$
>
> # 从 WSL 访问 Windows 文件：挂载在 /mnt 下
> ls /mnt/c/Users/你的用户名/Downloads
> ```

**用途**：两边文件互相访问。

**易错点**：
- Windows 的盘符在 WSL 里是 `/mnt/c`、`/mnt/d`。
- **性能**：在 WSL 里操作 `/mnt/c`（Windows 文件）很慢；编译项目尽量放 WSL 自己的 `~` 目录下。

**版本/平台**：WSL2。

**来源**：微软官方文档（https://learn.microsoft.com/zh-cn/windows/wsl/filesystems ），2026-10-25 访问。

## WSL 里装开发环境

> [!example]+ 最常用写法
> ```bash
> sudo apt update
> sudo apt install build-essential    # C/C++ 编译器
> sudo apt install python3 python3-pip python3-venv  # Python
> sudo apt install git                # Git
> ```

**用途**：WSL 里就是真 Linux，装环境用 apt，和 Linux 笔记本命令完全一致。

**易错点**：装完记得先 `sudo apt update`；详细见 [[环境配置-C与Cpp]] 和 [[环境配置-Python]]。

**版本/平台**：WSL2 / Ubuntu。

**来源**：微软官方文档（同上），2026-10-25 访问。

## 相关链接

- [[环境配置-C与Cpp]]
- [[环境配置-Python]]
- [[环境配置-VSCode]]
- [[Linux-常用命令]]
