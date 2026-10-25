---
title: Linux-进程管理
type: cheatsheet
tags:
  - 速查
  - 语言/Linux
---

# Linux-进程管理

## 查看进程

> [!example]+ 最常用写法
> ```bash
> ps aux               # 列出所有进程的详细信息
> ps aux | grep nginx  # 配合 grep 找某个进程
> top                  # 实时查看 CPU/内存占用，q 退出
> htop                 # 更友好的 top（需安装）
> ```

**用途**：查看系统里运行了哪些进程、占用多少资源。

**易错点**：
- `ps` 只显示某一瞬间快照，`top` 是实时刷新。
- `ps aux | grep xxx` 会把自己（grep 进程）也列出来，别误当结果。

**版本/平台**：Ubuntu 26.04。

**来源**：ps / top 手册页（`man ps`、`man top`），2026-10-25 访问。

## 结束进程 kill

> [!example]+ 最常用写法
> ```bash
> kill 1234            # 按 PID 发终止信号（SIGTERM）
> kill -9 1234         # 强制杀（SIGKILL），最后手段
> killall nginx        # 按进程名结束
> pkill -f "pattern"   # 按命令行匹配结束
> ```

**用途**：结束失控的进程。

**易错点**：
- 先用 `kill`（优雅终止），进程不响应再用 `kill -9`。
- PID 从 `ps` 或 `top` 的第二列获取。
- `kill -9` 不给程序清理机会，可能丢数据，慎用。

**版本/平台**：Ubuntu 26.04。

**来源**：kill 手册页（`man kill`），2026-10-25 访问。

## 前后台与 jobs

> [!example]+ 最常用写法
> ```bash
> command &            # 命令结尾 & 让它在后台运行
> jobs                 # 列出后台任务
> fg %1                # 把 1 号任务调到前台
> bg %1                # 把暂停的任务放到后台继续
> Ctrl+Z               # 暂停当前前台任务
> Ctrl+C               # 终止当前前台任务
> ```

**用途**：在后台跑长任务、暂停和恢复任务。

**易错点**：
- `Ctrl+Z` 是**暂停**不是结束，暂停后可用 `bg` 放后台或 `fg` 调回。
- 后台任务用 `jobs` 查看编号，`%1` 表示 1 号任务。

**版本/平台**：Bash（Ubuntu 默认 shell）。

**来源**：GNU Bash 手册 · Job Control（https://www.gnu.org/software/bash/manual/ ），2026-10-25 访问。

> [!note]- 进阶：nohup 让任务退出终端后继续
> ```bash
> nohup command > output.log 2>&1 &   # 退出终端也不中断
> ```

## 相关链接

- [[Linux-常用命令]]
- [[Linux-服务与systemd]]
