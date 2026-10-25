---
title: Linux-文件与权限
type: cheatsheet
tags:
  - 速查
  - 语言/Linux
---

# Linux-文件与权限

## 理解权限表示

> [!example]+ 最常用写法
> ```bash
> ls -l file.txt
> # -rw-r--r-- 1 user group 123 Oct 25 13:00 file.txt
> ```

**用途**：`ls -l` 第一列是权限，共 10 位：第 1 位是类型（`-` 普通文件、`d` 目录、`l` 链接），后 9 位分三组 `rwx`（读/写/执行）分别对应**属主、属组、其他**。

**易错点**：
- `r=4 读`、`w=2 写`、`x=1 执行`，三组相加得三位八进制数字（如 `755`）。
- `-rw-r--r--` 对应 `644`：属主读写，其他只读。
- 目录的 `x` 权限代表"能否进入该目录"。

**版本/平台**：Ubuntu 26.04。

**来源**：Ubuntu 官方文档 · File Permissions（https://ubuntu.com/server/docs/security-users ），2026-10-25 访问。

## 修改权限 chmod

> [!example]+ 最常用写法
> ```bash
> chmod 755 script.sh      # 数字法：属主 rwx，属组/其他 r-x
> chmod +x script.sh       # 符号法：给所有用户加执行权限
> chmod u+x script.sh      # 只给属主加执行
> chmod -R 755 dir/        # 递归改整个目录
> ```

**用途**：修改文件/目录的读写执行权限。

**易错点**：
- `chmod +x` 给所有用户加执行，常用在让脚本可运行。
- 数字法要一次写全 3 位（属主/属组/其他），如 `755`，别只写 `7`。
- 递归 `-R` 要小心，可能误改大量文件。

**版本/平台**：Ubuntu 26.04。

**来源**：chmod 手册页（`man chmod`），2026-10-25 访问。

## 修改属主与属组 chown

> [!example]+ 最常用写法
> ```bash
> sudo chown user file.txt          # 改属主
> sudo chown user:group file.txt    # 同时改属主和属组
> sudo chown -R user:group dir/     # 递归
> ```

**用途**：改变文件属于哪个用户、哪个组。

**易错点**：改属主通常需要 `sudo` 权限；改属组可用 `chgrp group file`。

**版本/平台**：Ubuntu 26.04。

**来源**：chown 手册页（`man chown`），2026-10-25 访问。

## sudo 提权

> [!example]+ 最常用写法
> ```bash
> sudo apt update          # 需要管理员权限的操作加 sudo
> sudo -i                  # 切到 root 交互式 shell（慎用）
> ```

**用途**：临时以管理员（root）身份执行命令。

**易错点**：
- 只有加入 `sudo` 组的用户才能用 `sudo`。
- `sudo -i` 会进入 root shell，容易误操作，能不用就不用。
- 输入密码时屏幕不显示（正常现象，不是卡住）。

**版本/平台**：Ubuntu 26.04。

**来源**：Ubuntu 官方文档 · sudo（https://ubuntu.com/server/docs/security-users ），2026-10-25 访问。

## 相关链接

- [[Linux-常用命令]]
- [[Linux-进程管理]]
- [[Linux-包管理]]
