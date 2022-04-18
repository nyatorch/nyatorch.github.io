# Java 学习笔记
> 参考 [Oracle Java Tutorial](https://docs.oracle.com/javase/tutorial/)   
> 后来发现该书已经被出版社翻译过，国内译本为《Java 语言导学》


## Java 有何特点
+ 简单
+ 面向对象
+ 分布式
+ 多线程
+ 动态
+ 体系结构中立
+ 可移植
+ 高性能
+ 健壮（鲁棒）
+ 安全
  
以上词语可以在 The Java Language Environment 这本白皮书里面找到

## Java 编程语言
Java 在 `.java` 后缀的文件中以纯文本（plain text）编写代码，源代码将会被`javac`编译器编译成`.class`后缀的字节码（bytecodes）文件，这是 java 虚拟机（JVM）的机器码文件，而不是你处理器的原生（native）的机器码。`java`启动工具则会通过一个JVM虚拟机实例运行你的应用程序。通过不同操作系统上的 JVM 虚拟机，java提供了跨平台运行的能力，此外，像 Java SE HotSpot 这样的虚拟机还可以提供查找性能瓶颈，将使用频率高的代码重新编译为本地代码等功能。

## Java 平台
平台（platform）是程序运行的硬件或软件环境。大多数平台指的是操作系统级和其依赖的硬件的结合。但是 Java 平台是一个仅包括软件的平台，运行于硬件基础平台的上层。

它包括两个部分：

+ Java 虚拟机（Java Virtual Machine, JVM）
+ Java 应用程序编程接口（Java Application Programming Interface, API）

API 是现成的软件组件，提供了许多有用的功能。他被归入相关类和接口的库（libraries）中。这些库也被称为包（packages）
API 和 Java 虚拟机将程序与其依赖的硬件(underlying hardware)隔离（insulate）开

作为平台无关（platform-independent）的环境，Java 平台可能比原生的机器码（native code）慢一点。但是编译器和虚拟机的高级技术可以让其性能接近于原生代码且无需威胁到可移植性（portability）



## Java 技术可以做什么

+ 开发工具：javac 编译器， java 启动器，javadoc 文档工具
+ 应用程序编程接口（API）：API提供了java编程语言的核心功能，从基础的对象到网络和安全，到XML生成和数据库访问。核心API非常多，可以阅读Java文档进行学习
+ 开发技术：JDK 提供了标准的构件，例如Java Web Start和Java Plug-in 让你部署应用到最终用户
+ 用户界面工具：JavaFX，Swing 和 Java 2D工具创建图形用户界面
+ 集成库（Integration Libraries）：Java IDL API，JDBC API， Java Naming and Directory Interface（JNDI）API, Java RMI, Java Remote Method Invoation over Internet Inter-ORB Protocol Technology(Java RMI-IIOP Technology)提供了远程的数据库对象访问和操作


## Hello World

```
class HelloWorldApp{
    public static void main(String[] args){
        System.out.println("Hello World"); // Display the string
    }
}
```

这个应用可以分为三个部分：

+ HelloWorldApp 类定义
+ main 方法
+ 源代码注释

```
/* 文本注释 */
/** 文档注释 */
// 单行文本注释
```
### 类定义
```
class name{

}
```
### main 方法

```
public static void main(String[] args){
    System.out.println("Hello World!");
}
```

`String args[]` 用于传递命令行参数

调用 System 类打印 `Hello World!` 


## 面向对象

### 什么是对象
对象具有状态（state）和行为（behavior）
如狗有名字，颜色，品种等状态，具有叫，抓东西，摇尾巴的行为

软件对象同样具有状态和行为，软件对象使用字段（field，有些语言称为变量，variable）存储状态，并将其行为通过方法（method，有些程序语言称为函数，function）暴露出来。

方法可以操作对象内部状态，也是对象与对象之间沟通的途径。

将内部状态隐藏起来，并要求所有的交互都要通过对象的方法进行，被称为**封装（encapsulation）**，这是面向对象编程的基础概念之一

将代码构建成独立的对象提供了许多好处：
+ 模块化
+ 信息隐藏
+ 代码复用
+ 可插拔和易于调试


## 类（Class）
显示中许多独立的对象都有相同的类型。
例如上千辆的自行车有着相同的制作工艺，模型，图纸，因此包含相同的组件。在面向对象的术语中，我们的你自己的自行车是对象（也就是所有的自行车）类的实例。。类是创建个体对象的蓝图。

定义 Bicycle 类
```
class Bicycle {
    int cadence = 0;
    int gear = 0;
    int gear = 1；
    void change Cadence (int newValue){
        cadence = newValue;
    }  
    void changeGear(int newValue){
        gear = newValue;
    }
    void speedUp(int increment){
        speed = speed + increment;
    }
    void applyBrakes(int decrement){
        speed = speed - decrement;
    }
    void printStates(){
        System.out.println("cadence:" +
         cadence + " speed:" + 
         speed + " gear:" + gear);
    }
}
```
该类并没有包含 main 方法，类并不是完整的应用程序，仅仅是程序可能用到的自行车蓝图，创建和使用 Bicycle 新对象的任务由其他类完成。
BicycleDemo 类创建了两个独立的 Bicycle 对象并调用它们的方法

```
class BicycleDemo {
    public static void main(String[] args) {
        //Create two different
        //Bicycle objects
        Bicycle  bike1 = new Bicycle();
        Bicycle bike2 = new Bicycle();

        //Invoke methods on
        //those objects
        bike1.changeCadence(50);
        bike1.speedUp(10);
        bike1.changeGear(2);
        bike1.printStates();

        bike2.changeCadence(50);
        bike2.speedUp(10);
        bike2.changeGear(2);
        bike2.chnageCadence(40);
        bike2.speedUp(10);
        bike2.changeGear(3);
        bike2.printStates();
    }
}
```

## 继承
不同的对象也由相同的地方
类可以集成其他类常用的状态和行为。