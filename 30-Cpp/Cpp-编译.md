---
title: Cpp-编译
type: cheatsheet
tags:
  - 速查
  - 语言/Cpp
---

# Cpp-编译

> [!note] 版本说明
> 本篇基于 Ubuntu 26.04 上的 g++（GCC）。你笔记本是 Ubuntu，可直接用；Windows 用 MinGW 或 MSVC。

## 编译单个文件

> [!example]+ 最常用写法
> ```bash
> g++ main.cpp -o main     # 编译成可执行文件 main
> ./main                   # 运行
> ```

**用途**：把 `.cpp` 编译成可执行文件。

**易错点**：
- 不加 `-o` 默认生成 `a.out`。
- 编译错误看报错里的 `行号` 和提示，从第一个错误开始改。

**版本/平台**：Ubuntu 26.04 / g++（GCC 11+）。

**来源**：GCC 官方文档（https://gcc.gnu.org/onlinedocs/ ），2026-10-25 访问。

## 编译标准与常用选项

> [!example]+ 最常用写法
> ```bash
> g++ -std=c++17 main.cpp -o main   # 指定 C++17 标准
> g++ -Wall -Wextra main.cpp -o main # 打开警告
> g++ -g main.cpp -o main           # 带调试信息（供 gdb）
> g++ -O2 main.cpp -o main          # 优化（发布用）
> ```

**用途**：指定语言标准、开启警告、调试、优化。

**易错点**：
- 教学建议 `-std=c++17`，明确版本。
- `-Wall -Wextra` 能提示很多隐患，养成开启习惯。
- `-g`（调试）和 `-O2`（优化）通常不同时用。

**版本/平台**：g++（GCC 11+）。

**来源**：GCC 官方文档 · Invoking G++（https://gcc.gnu.org/onlinedocs/gcc/Invoking-G_002b_002b.html ），2026-10-25 访问。

## 多文件编译

> [!example]+ 最常用写法
> ```bash
> g++ main.cpp utils.cpp -o main     # 多个 .cpp 一起编译
> ```

**用途**：项目拆多个源文件时一起编译。

**易错点**：头文件 `.h` 用 `#include "utils.h"`（自定义用双引号，标准库用尖括号）。

**版本/平台**：g++。

**来源**：GCC 官方文档（同上），2026-10-25 访问。

## 常见编译报错速查

> [!example]+ 最常用写法
> ```text
> error: expected ';' before ...      # 少分号
> error: 'x' was not declared ...     # 变量/函数没声明
> error: undefined reference to 'f'   # 声明了但没定义/没链接
> error: 'cout' was not declared      # 少 #include <iostream>
> ```

**用途**：快速定位常见错误原因。

**易错点**：`undefined reference` 是**链接错误**，通常是函数只声明没实现，或漏编译某个 `.cpp`。

**版本/平台**：g++。

**来源**：GCC 官方文档（同上），2026-10-25 访问。

> [!note]- 进阶：Makefile 基础
> ```makefile
> main: main.o utils.o
> 	g++ main.o utils.o -o main
> main.o: main.cpp utils.h
> 	g++ -c main.cpp
> utils.o: utils.cpp utils.h
> 	g++ -c utils.cpp
> clean:
> 	rm -f main *.o
> ```
> 运行 `make` 自动增量编译，`make clean` 清理。

## 相关链接

- [[Cpp-基础语法]]
- [[Cpp-类与对象]]
- [[Linux-常用命令]]
- [[环境配置-C与Cpp]]
