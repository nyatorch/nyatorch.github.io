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

Java 规定每个应用程序都必须有一个 main 方法

```
public static void main(String[] args){
    System.out.println("Hello World!");
}
```

`public static` 的顺序无关紧要，但习惯上使用 `public static` 而不是 `static public` （后者同样可以正常编译运行）

`String args[]` 用于传递命令行参数，参数名可以自己定义，但是多数程序员会选择 `args` 或者 `argv`

调用 System 类打印 `Hello World!` 


## 面向对象编程（Object-Oriented Programming）

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


### 类（Class）
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

### 继承（Inheritance）
不同的对象也有相同的地方
类可以继承（inherit）其他类常用的状态和行为。在这个例子中，Bicycle 成为 MountainBike，RoadBike 和 TandemBike 的超类（superclass）。

Java 语言允许每个类有一个直接超类，每个超类可以有无穷多个潜在的子类（subclass）

创建子类要用到 extends 关键字，后面接要继承的类名

```
class MountainBike extends Bicycle {

    // new fields and methods defining 
    // a mountain bike would go here

}
```

子类将得到与超类相同的字段和方法，这样编写代码时只用关注子类中独有的特性，这提高了代码的可读性，

然而，你必须注意正确文档化每个超类定义的状态和行为，因为这些代码不会出现在每个子类的源文件中。

### 接口（Interface）
正如之前所学，对象通过其暴露的方法，定义它们与外界的交互。方法构成了对象与的接口。比如，电视机盒前面板上的按钮就是你与盒子里面电路交互的接口。你可以通过电源键来开关电视。

最常见的情况，一个接口时一组空方法体的相关的方法。如果给自行车定义一个接口，大概会像这样

```
interface Bicycle {

    //  wheel revolutions per minute
    void changeCadence(int newValue);

    void changeGear(int newValue);

    void speedUp(int increment);

    void applyBrakes(int decrement);
}
```

为了实现（implement）这个接口，你的类名需要进行修改（变为某个特定品牌的自行车，比如 ACMEBicycle），并且你应该在类声明中使用 `implements` 关键字：

```
class ACMEBicycle implements Bicycle {

    int cadence = 0;
    int speed = 0;
    int gear = 1;

   // The compiler will now require that methods
   // changeCadence, changeGear, speedUp, and applyBrakes
   // all be implemented. Compilation will fail if those
   // methods are missing from this class.

    void changeCadence(int newValue) {
         cadence = newValue;
    }

    void changeGear(int newValue) {
         gear = newValue;
    }

    void speedUp(int increment) {
         speed = speed + increment;   
    }

    void applyBrakes(int decrement) {
         speed = speed - decrement;
    }

    void printStates() {
         System.out.println("cadence:" +
             cadence + " speed:" + 
             speed + " gear:" + gear);
    }
}
```


实现（implement）一个接口可以使一个类对它所承诺提供的行为变得更加形式化。接口在类和外部世界之间形成了一个契约（contract），这个契约在编译时被强制执行。如果你的类声称要实现一个接口，那么在该类成功编译之前，该接口定义的所有方法必须出现在其源代码中。

> 注意：要实际编译ACMEBicycle类，你需要在实现的接口方法的开头添加 public 关键字。你将在后面的 "类与对象 "和 "接口与继承 "课程中了解到这样做的原因。



### 包（Package）
包是一个命名空间（namespace），它组织了一系列相关的类和接口。

从概念上来说你可以认为包和你电脑上不同的文件夹类似。

你可以在一个目录里面放着 HTML 页面，在另一个目录放图片，脚本和应用又放到一个不同的文件夹里面。

由于 Java 编写的程序可以有成百上千个独立的类组成，通过将相关的类和接口放入包中来保持组织性是有意义的。

Java平台提供了一个巨大的类库（一组包），适合在你自己的应用程序中使用。这个库被称为 "应用编程接口"，或简称为 "API"。它的包代表了最常见的与通用编程相关的任务。例如，

String对象包含字符串的状态和行为；

File对象允许程序员轻松地创建、删除、检查、比较或修改文件系统上的文件；

Socket对象允许创建和使用网络套接字；

各种GUI对象控制按钮和复选框以及其他与图形用户界面有关的东西。

有数以千计的类可以选择。这使你这个程序员能够专注于设计你的特定应用程序，而不是使其运行所需的基础设施。


[Java 平台 API 规范](https://docs.oracle.com/javase/8/docs/api/index.html)包含了Java SE平台提供的所有包、接口、类、字段和方法的完整清单。在你的浏览器中加载该页面并将其加入书签。作为一个程序员，它将成为你唯一最重要的参考文档。


## 语言基础

### 变量（Variables）

正如之前所学，对象将其状态（state）存储在字段（fields）中

```
int cadence = 0;
int speed = 0;
int gear = 1;
```

在 什么是对象 的部分已经介绍了字段，但你可能还有疑惑：命名一个字段的规则和惯例是什么，除了 int 还有哪些数据类型，如果字段没有被明确初始化，是否会被分配一个默认值？我们将在本课中探讨这些问题的答案，但在这之前，你必须先了解一些技术上的区别。在Java编程语言中，"字段 "和 "变量 "这两个词都被使用；这在新的开发者中是一个常见的混淆源，因为这两个词似乎都是指同一件事。

Java 编程语言定义了如下种类的变量：

+ 实例变量（Instance Variables）（非静态字段，Non-Static Fields）
+ 类变量（Class Viriables）（静态字段，Static Fields）
+ 局部变量（Local Variables）
+ 参数（Parameters）