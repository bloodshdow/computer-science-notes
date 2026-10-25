---
title: 环境配置-Docker
type: cheatsheet
tags:
  - 速查
  - 主题/环境配置
  - 工具/Docker
---

# 环境配置-Docker

> [!note] 定位
> Docker 让你把应用连同环境打包成"容器"，到哪都能跑。你 Linux 小电脑想学，这里从概念到安装到常用命令。装服务器部署时也会用到（见 [[Server-Nginx基础]]）。

## Docker 是什么（先理解再动手）

### 逻辑

Docker 解决"在我电脑上能跑，换个环境就崩"的问题。它把**应用 + 依赖**打包成一个镜像（image），运行时变成容器（container）。

三个核心概念：

| 概念 | 类比 | 说明 |
|---|---|---|
| 镜像 image | 安装包/模板 | 只读，打包了程序和依赖 |
| 容器 container | 运行中的程序 | 从镜像启动的实例，互相隔离 |
| 仓库 registry | 应用商店 | 存放镜像，默认是 Docker Hub |

一句话：**"镜像 → 运行 → 容器"**，类似"程序 → 运行 → 进程"。

### 易错点（逻辑层面）

- 容器是**临时的**：删了容器，容器里改的东西就没了（持久化要挂载数据卷）。
- 容器很轻（共享内核），不像虚拟机那么重。

## Ubuntu 26.04 安装 Docker

> [!example]+ 步骤（官方 apt 仓库）
> ```bash
> # 1. 更新并装依赖
> sudo apt update
> sudo apt install ca-certificates curl
>
> # 2. 加 Docker 官方 GPG 密钥
> sudo install -m 0755 -d /etc/apt/keyrings
> sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
> sudo chmod a+r /etc/apt/keyrings/docker.asc
>
> # 3. 加 Docker 软件源
> sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
> Types: deb
> URIs: https://download.docker.com/linux/ubuntu
> Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
> Components: stable
> Architectures: $(dpkg --print-architecture)
> Signed-By: /etc/apt/keyrings/docker.asc
> EOF
>
> # 4. 安装
> sudo apt update
> sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
>
> # 5. 验证
> sudo docker run hello-world
> ```

**用途**：用官方源装最新稳定版 Docker（含 Compose 插件）。

**易错点**：
- 装完默认要 `sudo` 才能用 docker，想免 sudo 把用户加进 docker 组（见下节）。
- 验证出现 "Hello from Docker!" 就装成功了。

**版本/平台**：Ubuntu 26.04 / Docker Engine。

**来源**：Docker 官方文档（https://docs.docker.com/engine/install/ubuntu/ ），2026-10-25 访问。

## 免 sudo 用 docker（推荐）

> [!example]+ 最常用写法
> ```bash
> sudo usermod -aG docker $USER   # 把当前用户加入 docker 组
> newgrp docker                   # 立即生效（或注销重新登录）
> docker ps                       # 验证：不再报权限错误
> ```

**用途**：不加 docker 组的话每条命令都要 `sudo`，很麻烦。

**易错点**：加组后要**重新登录**（或 `newgrp docker`）才生效；docker 组权限相当于 root，只加自己的账号。

**版本/平台**：Docker。

**来源**：Docker 官方文档 · Linux post-install（https://docs.docker.com/engine/install/linux-postinstall/ ），2026-10-25 访问。

## 常用命令

> [!example]+ 最常用写法
> ```bash
> docker images          # 列出本地镜像
> docker pull nginx      # 下载镜像
> docker run -d -p 8080:80 nginx   # 后台运行容器，映射 8080 端口到容器的 80
> docker ps              # 列出运行中的容器
> docker ps -a           # 列出所有容器（含停止的）
> docker stop 容器ID     # 停止容器
> docker rm 容器ID       # 删除容器
> docker rmi 镜像名      # 删除镜像
> docker logs 容器ID     # 看容器日志
> ```

**用途**：Docker 最常用的日常命令。

**易错点**：
- `docker run` 每次会**新建**容器；重复 run 会造出一堆容器。
- `-p 本机端口:容器端口` 是端口映射，别写反。
- `-d` 后台运行，不加会在前台占用终端。

**版本/平台**：Docker。

**来源**：Docker 官方文档 · CLI reference（https://docs.docker.com/reference/cli/docker/ ），2026-10-25 访问。

## 相关链接

- [[Server-Nginx基础]]
- [[Linux-包管理]]
- [[环境配置-Python]]
