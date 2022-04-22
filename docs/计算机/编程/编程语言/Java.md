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

+ 实例变量（Instance Variables）（非静态字段，Non-Static Fields），技术上讲，对象存储其个体状态在“非静态字段”中，即，那些没有以 static 关键字声明的字段。非静态字段也称为实例变量，因为它们的值对每一个类中的实例（也就是对象）是唯一的（unique），一辆自行车的 currentSpeed 跟另一辆自行车的currrentSpeed 是独立的。
+ 类变量（Class Viriables）（静态字段，Static Fields）类变量是用 static 修饰符（modifier）声明的任意字段，这会告诉编译器无论类实例化多少次，这个变量实际上只存在一个副本（copy），特定种类的自行车档数可以用 static 标记，因为概念上来讲，这个档数将被应用到所有的实例，代码`static int numGears = 6` 将会创建这样的静态字段。此外，也可以使用 `final` 关键字表明该档数永远不会被修改。
+ 局部变量（Local Variables）和对象如何在字段中存储其状态类似，一个方法将会将其临时状态存储在局部变量中，声明一个局部变量的语法（syntax）和声明一个字段类似
+ 参数（Parameters）例如，public static void main(String[] args)中，args 就是 main 方法的参数，最重要的一点是，参数总被归为变量，而不是字段。这同样适用于其他支持参数的结构（比如构造函数和异常处理程序）

尽管如此，本教程的其余部分在讨论字段和变量时使用以下一般准则。如果我们讨论的是 "一般的字段"（不包括局部变量和参数），我们可以直接说 "字段"。如果讨论适用于 "上述所有"，我们可以简单地说 "变量"。如果上下文要求进行区分，我们将酌情使用特定的术语（静态字段、局部变量等）。你可能偶尔也会看到 "成员（member） "这个术语。一个类型的字段、方法和嵌套类型被统称为其成员。


### 命名（Naming）：
+ 大小写敏感，可以是以字母，美元符号，或下划线开头的无限长的 Unicode letter 和数字序列。按照惯例，变量名应当总是以字母开头，而不是`$` 或 `_`此外，按照惯例，永远不要使用美元符号，你可能发现某些情况下自动生成的变量名包含了美元符号（dollar sign），但是你的变量命名应该永远避免使用它。下划线字符也有类似的约定；虽然从技术上讲，用`_` 作为变量名称的开头是合法的，但这种做法是不可取的。此外，变量名中使用空格是不合法的。
  
+ 后续的字符可以是字母、数字、美元符号或下划线字符。惯例（和常识）也适用于这个规则。当为你的变量选择名称时，请使用全称，而不是隐晦的缩写。这样做会使你的代码更容易阅读和理解。在许多情况下，这也会使你的代码自文档化（self-documenting）；例如，命名为 `cadence`、`speed` 和 `gear` 的字段，比缩写的版本，如 s、c 和 g，要直观得多。

+ 如果你选择的名字只由一个词组成，请用所有小写字母拼出该词。如果它由一个以上的词组成，请将后面每个词的第一个字母大写。gearRatio和currentGear这两个名字就是这种惯例的典型例子。如果你的变量存储了一个常量值，比如 static final int NUM_GEARS = 6，那么惯例会稍有改变，每个字母都要大写，并且用下划线字符来分隔后面的单词。根据惯例，下划线字符永远不会在其他地方使用。

> 注：不要以为 letter 是英文字母，它包括中文！包括 `_￥` ， `中文` 和 `𝜃` 在内的变量名都是合法的，尽管这么干容易被同事打死
> 
> 关于判断一个 Unicode 字符 是否为 Unicode letter， 参考 [这个地址](http://xahlee.info/comp/unicode_letter_character.html)

### 基本数据类型（Primitive Data Types）

Java编程语言是静态类型的（statically-typed），必须首先声明。这包括说明变量的类型和名称，正如你已经看到的。

```
int gear = 1;
```

这样做会告诉你的程序，有一个名为 `gear` 的字段存在，持有数值型数据（numerical），初始值为1，一个变量的数据类型决定了它可能包含哪些值，以及哪些运算符可以被用于这个变量。除了 int 类型（整型） 以外，Java 编程语言还支持其他其中基本数据类型，一个基本数据类型由语言预定义，并用保留关键字（reserved keyword）来命名。基本数据类型的值之间不共享状态，Java 编程语言支持以下 8 种基本数据类型。

+ Byte 类型 是 8 位有符号二进制补码整数（ 8-bit signed two's complement integer），最小值 -128，最大值为 127。字节数据类型对于在大数组中节省内存是很有用的，这种情况下节省的内存是很重要的需求。它们也可以用来代替int，因为它们的限制有助于阐述你的代码；一个变量的范围被限制的事实可以作为一种文档形式。
+ short 数据类型标识 16 位带符号二进制补码整数，其最小值为 -32768，最大值为 32767（包括32767）。和字节一样，同样的准则也适用：你可以在大数组中使用short来节省内存，在这种情况下，节省的内存实际上很重要。
+ int：默认情况下，int数据类型是一个32位有符号的二进制补码整数，它的最小值为2^31-1，最大值为2^31-1。在Java SE 8及以后的版本中，你可以使用int数据类型来表示一个无符号的32位整数，它的最小值为0，最大值为2^32-1。使用Integer类来使用int数据类型作为无符号整数。更多信息请参见 "Number类 "一节。静态方法如compareUnsigned, divideUnsigned 等已经被添加到Integer 类中，以支持无符号整数的算术操作。
+ long。long数据类型是一个64位的二进制。有符号的long的最小值为-2^63，最大值为2^63-1。在Java SE 8及以后的版本中，你可以使用long数据类型来表示一个无符号的64位long，它的最小值为0，最大值为2^64-1。当你需要一个比int提供的数值范围更宽的数值时，可以使用这种数据类型。Long 类还包含一些方法，如 compareUnsigned, divideUnsigned 等，以支持无符号long 的算术操作。
+ float。float数据类型是一个单精度的32位IEEE 754浮点。它的取值范围超出了本文的讨论范围，但在《Java语言规范》的浮点类型、格式和值部分有规定。如同对byte和short的建议一样，如果你需要在大的浮点数数组中节省内存，请使用浮点数（而不是double）。这种数据类型绝不应该用于精确的数值，例如货币。对于这一点，你需要使用java.math.BigDecimal类来代替。***Numbers and Strings***一书涵盖了BigDecimal和其他由Java平台提供的有用的类。
+ double。double数据类型是一个双精度的64位IEEE 754浮点。它的取值范围超出了本文的讨论范围，但在《Java语言规范》的浮点类型、格式和值部分有规定。对于十进制值，这种数据类型通常是默认选择。如上所述，这种数据类型绝不应该用于精确的值，如货币。
+ boolean。布尔数据类型只有两个可能的值：真和假。将这种数据类型用于跟踪真/假条件的简单标志。这种数据类型代表一位信息，但它的 "大小 "并不是精确定义的。
+ char。char数据类型是一个单一的16位Unicode字符。它的最小值为'\u0000'（或0），最大值为'\uffff'（或65,535（包括））

#### 1.默认值
当一个字段被声明时，并不总是需要赋值。已声明但未初始化的字段将被编译器设置为一个合理的默认值。一般来说，这个默认值将是零或空，这取决于数据类型。然而，依赖这样的默认值，通常被认为是不好的编程风格。

下面的图表总结了上述数据类型的默认值。

| 数据类型 | 默认值（对于字段） |
|--------|-----------------|
|  byte  |        0        |
|  short |        0        |
|  int   |        0        |
|  long  |        0L       |
|  float |        0.0f     |
| double |        0.0d     |
|  char  |    '\u0000'     |
|  String (or any object)  |        null        |
|boolean |       false     |

局部变量略有不同；编译器永远不会给未初始化的局部变量分配一个默认值。如果你不能在声明的地方初始化你的局部变量，请确保在你试图使用它之前给它赋值。访问一个未初始化的局部变量将导致一个编译时错误。

#### 2. 字面量（literal）
你可能已经注意到了 new 关键字不呢个用于初始化一个基本类型变量。基本类型是编程语言内置的特殊数据类型。它们并不是由类创建的对象，一个字面量是一个固定值的源码表示，它在你的代码是直接表示而无需计算。

```
boolean result = true;
char capitalC = 'C';
byte b = 100;
short s = 10000;
int i = 100000;
```

#### 整数字面量（Integer Literals）
如果一个整数字面量以 `L` 或 `l` 结尾，则其为 long 类型，否则为 int 类型。推荐使用大写 L 因为 小写的 l 极易与数字 1 混淆。

整数字面量的值，byte short int 的值可由 int 字面量创建， 超出 int 范围的 long 类型的值可由 long 字面量创建，整数字面量可以用 10 进制 16 进制 或 二进制数制系统表示

0x 表示十六进制数 0b 表示二进制数

#### 浮点字面量（Floating-Point Literals）
一个浮点字面量是如果以 F 或 f 结尾是 float 类型，否则为 double 类型（可选以 D 或 d 结尾）

浮点类型也可以用 E 或 e 表示（用于科学计数法（scientific notation）），F 或 f （32位 float 字面量） 以及 D 或者 d（64位 double 字面量，默认的，而且通常省略不写）

```
double d1 = 123.4;
// same value as d1, but in scientific notation
double d2 = 1.234e2;
float f1  = 123.4f;
```

#### 字符和字符串字面量（Character and String Literals）
字符和字符串类型的字面量可能包含任何 Unicode (UTF-16) 字符。如果你的编辑器和文件系统允许，你在代码中直接使用这些字符，如果不行，你可以使用 “Unicode 转义字符（Unicode escape）” 例如 `'\u0108'` `"S\u00ED Se\u00Flor"` (西班牙语的 Sí Señor)。永远对字符字面量单引号（single quotes），对字符串字面量使用双引号（double quotes）Unicode 转义序列也可以用于程序的其他地方（比如字段名）而不只是字符或字符串字面量


