---
title: Java-面向对象
type: cheatsheet
tags:
  - 速查
  - 语言/Java
---

# Java-面向对象

> [!note] 版本说明
> 基于 Java 21 LTS。Java 是纯面向对象语言，几乎一切都是类。

## 定义类与对象

> [!example]+ 最常用写法
> ```java
> public class Person {
>     // 成员变量（字段）
>     private String name;
>     private int age;
>
>     // 构造方法：名字和类同名，无返回值
>     public Person(String name, int age) {
>         this.name = name;
>         this.age = age;
>     }
>
>     // 成员方法
>     public void sayHi() {
>         System.out.println("Hi " + name);
>     }
> }
>
> // 使用
> Person p = new Person("Alice", 20);
> p.sayHi();
> ```

**用途**：类封装数据（字段）和行为（方法），`new` 创建对象。

**易错点**：
- 构造方法名必须和类名相同、**没有返回类型**。
- `this` 指当前对象，用于区分成员变量和参数同名。
- 没有写构造方法时，编译器会给一个无参构造；写了有参构造后无参构造就没了。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程 · Classes（https://docs.oracle.com/javase/tutorial/java/javaOO/classes.html ），2026-10-25 访问。

## 访问修饰符与封装

> [!example]+ 最常用写法
> ```java
> public class Person {
>     private String name;     // 私有，只能类内部访问
>
>     // getter / setter 暴露访问
>     public String getName() { return name; }
>     public void setName(String name) { this.name = name; }
> }
> ```

**用途**：`private` 隐藏字段，通过 getter/setter 访问，即封装。

**易错点**：
- `private`（类内）/ `public`（外部）/ `protected`（子类）是访问级别。
- 字段通常 `private`，用 getter/setter 控制访问，是 Java 惯例。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程 · Access control（https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html ），2026-10-25 访问。

## 继承

> [!example]+ 最常用写法
> ```java
> public class Animal {
>     public void eat() { System.out.println("eating"); }
> }
>
> public class Dog extends Animal {   // 用 extends 继承
>     public void bark() { System.out.println("woof"); }
> }
>
> Dog d = new Dog();
> d.eat();    // 继承来的方法
> d.bark();
> ```

**用途**：子类复用父类，Java **单继承**（一个类只能 extends 一个父类）。

**易错点**：
- Java 只支持单继承，但可通过**接口（interface）**实现多继承效果。
- 子类构造时会自动调用父类无参构造（`super()` 隐式）。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程 · Inheritance（https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html ），2026-10-25 访问。

## 方法重写与多态

> [!example]+ 最常用写法
> ```java
> class Animal {
>     public void speak() { System.out.println("?"); }
> }
> class Dog extends Animal {
>     @Override
>     public void speak() { System.out.println("Woof"); }
> }
>
> Animal a = new Dog();   // 父类引用指向子类对象
> a.speak();              // "Woof"，动态绑定，调用子类实现
> ```

**用途**：`@Override` 重写父类方法；父类引用调用时执行子类实现，即多态。

**易错点**：
- 重写加 `@Override` 注解，拼错方法名编译器会报错。
- 方法重写（override，子类改父类实现）和方法重载（overload，同名不同参数）是两个概念。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程 · Polymorphism（https://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html ），2026-10-25 访问。

## 接口 interface

> [!example]+ 最常用写法
> ```java
> interface Flyable {
>     void fly();    // 接口方法默认 public abstract
> }
>
> class Bird implements Flyable {
>     public void fly() { System.out.println("flying"); }
> }
> ```

**用途**：接口定义"能做什么"的契约，类用 `implements` 实现，可多实现。

**易错点**：
- 类能 `implements` 多个接口（弥补单继承）。
- 接口里只有方法声明（Java 8+ 可有 default 方法）。

**版本/平台**：Java 21。

**来源**：Oracle Java 教程 · Interfaces（https://docs.oracle.com/javase/tutorial/java/IandI/createinterface.html ），2026-10-25 访问。

## 相关链接

- [[Java-基础语法]]
- [[Java-集合框架]]
- [[Java-异常]]
