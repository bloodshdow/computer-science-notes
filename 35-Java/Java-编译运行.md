---
title: Java-编译运行
type: cheatsheet
tags:
  - 速查
  - 语言/Java
---

# Java-编译运行

> [!note] 版本说明
> 基于 Java 21 LTS。Java 是"编译成字节码 + JVM 运行"的两步模型，和 C/C++ 直接编译成本地机器码不同。

## 编译与运行

> [!example]+ 最常用写法
> ```bash
> javac Hello.java       # 编译，生成 Hello.class（字节码）
> java Hello             # 运行（注意不带 .class 后缀）
> ```

**用途**：`javac` 编译成字节码，`java` 在 JVM 上运行。

**易错点**：
- 运行命令是 `java Hello`，**不是** `java Hello.class`。
- 文件里有 `public class Hello` 时，文件名必须叫 `Hello.java`。
- 跨平台的关键：`.class` 字节码在任意装了 JVM 的系统都能跑。

**版本/平台**：Java 21 / JDK。

**来源**：Oracle Java 文档（https://docs.oracle.com/en/java/javase/21/ ），2026-10-25 访问。

## 装 JDK

> [!example]+ 步骤
> ```bash
> # Linux（Ubuntu 26.04）
> sudo apt install openjdk-21-jdk
> java -version    # 验证
> javac -version
> ```
> ```text
> # Windows：到 adoptium.net（免费）下载 JDK 21 安装包，装完配好 PATH
> ```

**用途**：装 Java 开发工具包（JDK），含 `java` 和 `javac`。

**易错点**：写代码要装 **JDK**（含编译器），只装 JRE（运行环境）不能编译。

**版本/平台**：JDK 21。

**来源**：Adoptium 文档（https://adoptium.net/ ），2026-10-25 访问。

## 常见编译错误

> [!example]+ 最常用写法
> ```text
> error: class Hello is public, should be declared in Hello.java
>     → 文件名和 public 类名不一致
> error: cannot find symbol
>     → 变量/方法名拼错，或没 import
> error: ';' expected
>     → 少分号
> ```

**用途**：快速定位编译错误。

**易错点**：Java 报错信息一般很清楚，看 `error:` 后面第一行 + 行号即可。

**版本/平台**：javac。

**来源**：Oracle Java 文档（同上），2026-10-25 访问。

## 相关链接

- [[Java-基础语法]]
- [[环境配置-Git]]
- [[Linux-包管理]]
