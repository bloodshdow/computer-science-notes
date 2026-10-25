---
title: CSharp-面向对象
type: cheatsheet
tags:
  - 速查
  - 语言/CSharp
---

# CSharp-面向对象

> [!note] 版本说明
> 基于 C# 12 / .NET 8。C# 的面向对象和 Java 高度相似，重点看区别。

## 类与对象

> [!example]+ 最常用写法
> ```csharp
> public class Person {
>     public string Name { get; set; }   // 自动属性
>     public int Age { get; set; }
>
>     public Person(string name, int age) {
>         Name = name;
>         Age = age;
>     }
>
>     public void SayHi() {
>         Console.WriteLine($"Hi {Name}");
>     }
> }
>
> var p = new Person("Alice", 20);
> p.SayHi();
> ```

**用途**：类封装数据和行为。`{ get; set; }` 是 C# 的自动属性，省去手写 getter/setter。

**易错点**：
- **属性（Property）** 是 C# 特色，比 Java 的 getter/setter 简洁（`p.Name` 直接访问）。
- 构造函数名和类同名、无返回值。

**版本/平台**：C# 12 / .NET 8。

**来源**：Microsoft Learn · 类（https://learn.microsoft.com/zh-cn/dotnet/csharp/fundamentals/types/classes ），2026-10-25 访问。

## 属性 vs 字段

> [!example]+ 最常用写法
> ```csharp
> public class Person {
>     private string name;                 // 字段（私有）
>     public string Name {                 // 属性（对外）
>         get { return name; }
>         set { name = value; }
>     }
>     // 简写：public string Name { get; set; }
> }
> ```

**用途**：字段存数据（private），属性对外暴露访问（get/set）。

**易错点**：属性本质是方法，`value` 是 set 里的隐式参数。自动属性 `{ get; set; }` 是最常用简写。

**版本/平台**：C# 12。

**来源**：Microsoft Learn · 属性（https://learn.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/properties ），2026-10-25 访问。

## 继承与多态

> [!example]+ 最常用写法
> ```csharp
> public class Animal {
>     public virtual void Speak() { Console.WriteLine("?"); }
> }
>
> public class Dog : Animal {          // 冒号继承（对应 Java 的 extends）
>     public override void Speak() { Console.WriteLine("Woof"); }
> }
>
> Animal a = new Dog();
> a.Speak();    // "Woof"，多态
> ```

**用途**：继承和重写。C# 用 `: 基类` 表示继承，`virtual`/`override` 实现多态。

**易错点**：
- 基类方法要 `virtual`，子类重写要 `override`（和 Java 默认虚方法不同）。
- C# 单继承，接口用 `: I接口` 实现（多接口逗号分隔）。

**版本/平台**：C# 12。

**来源**：Microsoft Learn · 继承（https://learn.microsoft.com/zh-cn/dotnet/csharp/fundamentals/object-oriented/inheritance ），2026-10-25 访问。

## 接口

> [!example]+ 最常用写法
> ```csharp
> interface IFlyable {
>     void Fly();
> }
>
> class Bird : IFlyable {
>     public void Fly() { Console.WriteLine("flying"); }
> }
> ```

**用途**：接口定义契约，C# 接口名习惯 `I` 开头（如 `IFlyable`）。

**易错点**：接口命名规范是 `I` 前缀；类和接口都用 `:` 连接（继承类放前面）。

**版本/平台**：C# 12。

**来源**：Microsoft Learn · 接口（https://learn.microsoft.com/zh-cn/dotnet/csharp/fundamentals/types/interfaces ），2026-10-25 访问。

## 相关链接

- [[CSharp-基础语法]]
- [[CSharp-集合与LINQ]]
