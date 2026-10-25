---
title: Linux-常用命令
type: cheatsheet
tags:
  - 速查
  - 语言/Linux
---

# Linux-常用命令

> [!note] 平台说明
> 本篇命令基于 Ubuntu 26.04 LTS（也适用于大多数 Debian 系发行版）。你笔记本是 Ubuntu + KDE，绝大多数命令通用。

## 目录与文件浏览

> [!example]+ 最常用写法
> ```bash
> pwd                  # 显示当前目录
> ls                   # 列出当前目录
> ls -l                # 长格式：权限、大小、时间
> ls -a                # 显示隐藏文件（. 开头）
> ls -lh               # 人类可读的大小（K/M/G）
> cd /path/to/dir      # 切换目录
> cd ~                 # 回主目录
> cd ..                # 上一级
> ```

**用途**：查看当前位置、列出文件、切换目录。

**易错点**：
- Linux 用 `/` 分隔路径，Windows 是 `\`。
- 隐藏文件以 `.` 开头，`ls` 默认不显示，要加 `-a`。
- 文件名区分大小写，`File` 和 `file` 是两个文件。

**版本/平台**：Ubuntu 26.04 / GNU coreutils。

**来源**：GNU Coreutils 手册（https://www.gnu.org/software/coreutils/manual/ ），2026-10-25 访问。

## 文件操作

> [!example]+ 最常用写法
> ```bash
> touch file.txt       # 新建空文件（或更新时间戳）
> mkdir dir            # 建目录
> mkdir -p a/b/c       # 递归建多级目录
> cp src dst           # 复制文件
> cp -r dir1 dir2      # 递归复制目录
> mv old new           # 移动 / 重命名
> rm file.txt          # 删除文件
> rm -r dir            # 递归删除目录
> ```

**用途**：创建、复制、移动、删除文件与目录。

**易错点**：
- `rm` 删除不可恢复，没有回收站，慎用；删目录要 `-r`。
- `cp` 复制目录必须加 `-r`，否则报错。
- `mv` 既是移动也是重命名（同目录下移动即改名）。

**版本/平台**：Ubuntu 26.04 / GNU coreutils。

**来源**：GNU Coreutils 手册（同上），2026-10-25 访问。

## 查看文件内容

> [!example]+ 最常用写法
> ```bash
> cat file.txt         # 一次性输出全部（适合小文件）
> less file.txt        # 分页查看，q 退出，/ 搜索
> head -n 20 file      # 前 20 行
> tail -n 20 file      # 后 20 行
> tail -f log.txt      # 实时跟踪日志（Ctrl+C 退出）
> ```

**用途**：查看文件内容。

**易错点**：
- 大文件别用 `cat`，用 `less`。
- `tail -f` 会一直跟随输出，退出按 `Ctrl+C`。

**版本/平台**：Ubuntu 26.04 / GNU coreutils。

**来源**：GNU Coreutils 手册（同上），2026-10-25 访问。

## 搜索与查找

> [!example]+ 最常用写法
> ```bash
> grep "关键词" file.txt       # 在文件中搜关键词
> grep -r "关键词" dir/        # 递归搜目录
> grep -i "word" file          # 忽略大小写
> find . -name "*.py"          # 按文件名找
> find . -type f -mtime -7     # 找最近 7 天修改的文件
> ```

**用途**：`grep` 搜内容，`find` 找文件。

**易错点**：`grep` 默认区分大小写，忽略大小写加 `-i`；`find` 的 `-name` 模式要用引号包住。

**版本/平台**：Ubuntu 26.04。

**来源**：GNU grep / find 手册（https://www.gnu.org/software/grep/manual/ ），2026-10-25 访问。

## 管道与重定向

> [!example]+ 最常用写法
> ```bash
> ls -l | grep ".txt"          # 管道：把前一个输出传给后一个
> echo "hi" > file.txt         # 覆盖写入文件
> echo "hi" >> file.txt        # 追加写入文件
> cmd 2>&1                     # 把错误输出也合并到标准输出
> ```

**用途**：组合命令、把输出保存到文件。

**易错点**：
- `>` 会**覆盖**原文件，`>>` 是**追加**，别写反。
- 只想看错误信息时用 `2>` 重定向标准错误。

**版本/平台**：Bash（Ubuntu 默认 shell）。

**来源**：GNU Bash 手册 · Redirections（https://www.gnu.org/software/bash/manual/ ），2026-10-25 访问。

## 查看帮助

> [!example]+ 最常用写法
> ```bash
> man ls              # 查看命令手册，q 退出
> ls --help           # 简要帮助
> which python        # 查看命令的路径
> ```

**用途**：查命令用法。

**易错点**：`man` 里按 `/` 搜索、`q` 退出；记不住参数先 `命令 --help` 最快。

**版本/平台**：Ubuntu 26.04。

**来源**：GNU Bash 手册（同上），2026-10-25 访问。

## 相关链接

- [[Linux-文件与权限]]
- [[Linux-进程管理]]
- [[Linux-包管理]]
