---
title: Python-虚拟环境与pip
type: cheatsheet
tags:
  - 速查
  - 语言/Python
---

# Python-虚拟环境与pip

## 为什么用虚拟环境

**用途**：每个项目一套独立的依赖，避免不同项目间的包版本冲突，也避免污染系统 Python。

**易错点**：不要把所有包都 `pip install` 到全局，不同项目可能要求同一个包的不同版本。

**版本/平台**：Python 3.3+ 内置 `venv`。

**来源**：Python 官方文档 · venv（https://docs.python.org/3/library/venv.html ），2026-10-25 访问。

## 创建与激活虚拟环境

> [!example]+ 最常用写法
> ```bash
> # 创建（Windows 与 Linux 命令相同）
> python -m venv .venv
>
> # 激活：Windows (cmd)
> .venv\Scripts\activate
>
> # 激活：Linux / macOS
> source .venv/bin/activate
>
> # 退出
> deactivate
> ```

**用途**：建一个叫 `.venv` 的独立环境并进入。

**易错点**：
- Windows 激活脚本在 `Scripts\activate`，Linux/macOS 在 `bin/activate`，路径不同。
- 激活后命令行提示符前会出现 `(.venv)`，说明已生效。
- `activate` 是 PowerShell 下要用 `activate.ps1`；PowerShell 执行策略限制时可能需先 `Set-ExecutionPolicy`。

**版本/平台**：Python 3.3+，Windows/Linux/macOS。

**来源**：Python 官方文档 · Creating virtual environments（https://docs.python.org/3/tutorial/venv.html ），2026-10-25 访问。

## pip 安装与管理包

> [!example]+ 最常用写法
> ```bash
> pip install requests            # 安装
> pip install requests==2.31.0    # 安装指定版本
> pip uninstall requests          # 卸载
> pip list                        # 查看已装包
> pip show requests               # 查看某包详情
> pip install -U pip              # 升级 pip 自己
> ```

**用途**：安装、卸载、查看第三方包。

**易错点**：
- 先激活虚拟环境再 `pip install`，否则装到全局。
- 国内可用镜像加速：`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 包名`。

**版本/平台**：pip 随 Python 3.4+ 自带。

**来源**：Python 官方文档 · Installing Packages（https://packaging.python.org/tutorials/installing-packages/ ），2026-10-25 访问。

## requirements.txt

> [!example]+ 最常用写法
> ```bash
> pip freeze > requirements.txt      # 导出当前环境所有包及版本
> pip install -r requirements.txt    # 按清单批量安装
> ```

**用途**：记录并复现项目依赖，团队协作、部署必备。

**易错点**：`freeze` 导出的是**全部**包（含间接依赖），可能很多；也可手写只列直接依赖。

**版本/平台**：pip。

**来源**：pip 官方文档 · Requirements Files（https://pip.pypa.io/en/stable/user_guide/#requirements-files ），2026-10-25 访问。

## 相关链接

- [[Python-常用库]]
- [[Python-基础语法]]
- [[Linux-包管理]]
