### 欢迎大家来到java世界

>带领大家领略编程的奥秘。

人与人沟通需要语言。计算机世界的沟通语言。

- Java语法结构，使用循环和选择流控制结构，了解方法和数组的使用。

### Java简介

Java是一门编程语言，先了解语法结构。

主要内容:

  - Java简介
  - 开发第一个Java程序(命令行)
  - 使用Eclipse进行Java开发

Java重大事件:
  
  - Java是一门面向对象的程序设计语言
  - 1995年由sun公司发布,是咖啡的名字;Java: 好喝的咖啡。
  - 2010年sun公司被Oracle公司收购了
  - 当前课程的JDK版本是8.0（目前最新的是java10系列）

![](http://myphoto.mtianyan.cn/20180728021918_MU5aPS_Screenshot.jpeg)

JVM:
  - JVM(Java Virtual Machine) Java虚拟机简称
  - JVM是Java平台无关性实现的关键。

一般高级语言要在不同平台运行，通常要进行编译目标机器代码。

Java程序执行过程

![](http://myphoto.mtianyan.cn/blog/180721/A6KjI89mgg.png?imageslim)

>由源文件`.java`，通过**编译器**进行编译生成`.class`的字节码文件，字节码文件交给解释器来执行。

解释执行由java虚拟机完成，将字节码文件解释为具体平台上的机器指令。实现**一次编译，到处运行**

JDK:

  - JDK ( Java Development Kit ) Java语言的软件开发工具包
  - 两个主要的组件: javac -编译器,将源程序鞋成字节码;java - 运行编译后的java程序(.class后綴的)

JRE:

  - JRE(Java Runtime Environment)
  - 包括Java虚拟机( JVM )、Java核心类库和支持文件
  - 如果只需要运行Java程序，下载并安装JRE即可（给用户的运行环境下）

如果要开发Java软件，需要下载JDK;在JDK中附带有JRE的。

JDK,JRE和JVM三者的关系:

![](http://myphoto.mtianyan.cn/20180728022747_ExosPD_Screenshot.jpeg)

>JRE=JVM+JavaSE标准类库;JDK=JRE+开发工具集(例如Javac编译工具等)

Java平台
  
  - Java SE 面向桌面程序 Java标准版
  - Java EE 面向Web程序 Java企业版
  - Java ME 移动设备 Java微型版
  
### Java程序的运行流程

首先我们使用记事本编写一个java程序

HelloMtianyan 既是类的名字，同时也是我们保存成`.java`文件的文件名

```java
class HelloJava{
    public static void main(String[] args)
    {
      System.out.println("Hello java,mtianyan!");
    }
}
```

将上述代码保存为HelloJava.java,然后cd到保存的目录，执行。

```java
javac HelloJava.java
```

如果提示javac命令不存在，环境变量中加入javac所在路径。

命令成功执行，没有任何输出。此时会多出一个HelloJava.class文件。运行下面命令

```java
java Hellojava // 此处不能加class,否则提示如下报错。

// 错误: 找不到或无法加载主类 HelloJava.class
// 原因: java.lang.ClassNotFoundException: HelloJava.class
```

`String[] args`这个参数是必要的，否则java会提示：

```java
错误: 在类 HelloJava 中找不到 main 方法, 请将 main 方法定义为:
public static void main(String[] args)
```

![](http://myphoto.mtianyan.cn/20180728030013_M05i0X_Screenshot.jpeg)

### 带命令行参数的Java程序

记事本写一段程序:

```java
class ArgsDemo{
    public static void main(String[] args){
      // 输入从键盘输入的内容; args是命令行输入的参数数组
      System.out.println(args[0]);
      System.out.println(args[1]);
    }
}
```

![](http://myphoto.mtianyan.cn/20180728031104_AqCwoH_Screenshot.jpeg)

>这里注意java，后面后缀几个参数，就依次是这几个。

```python
import sys

print '参数个数为:',len(sys.argv), '个参数。'
print '参数列表:', str(sys.argv)
```

![](http://myphoto.mtianyan.cn/20180728031528_8Smu4m_Screenshot.jpeg)

>Python中文件名会被作为第一个参数。

注意: 传了几个值就只能取几个值，否则会产生越界错误。

### Java程序结构

```java
class HelloJava{
    public static void main(String[] args){
      System.out.println("Hello java,mtianyan!");
    }
}
```

类中包含main方法，大括号是嵌套关系的层次表示。

class 之后是类名，前面也可以加上修饰符, 如`public class HelloJava`

println是输出语句，main函数是程序的入口。

### 使用Eclipse开发java程序(推荐使用IDEA)

首先，下载IDEA，都2018年了，大清亡了这么多年了，别用Eclipse了。

### 创建程序。

先创建工程(Project)，再创建Package。

点击创建Project -> CreateProjectFromTemplate -> 填写信息

![](http://myphoto.mtianyan.cn/20180728033120_rTX07b_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180728033746_ruhERD_Screenshot.jpeg)

新建好的工程如上图所示，src为源代码目录，下面的cn.mtianyan是包名; Main是类名同时也是入口类的文件名。

- 自行新建包: src右键New Package

![](http://myphoto.mtianyan.cn/20180728034357_reNBC3_Screenshot.jpeg)

- 自行新建类,daishushu下右键New Java Class

![](http://myphoto.mtianyan.cn/20180728034513_oX5U8q_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180728034959_TIGeCi_Screenshot.jpeg)

>这里可以看到IDEA中的报名cn.mtianyan对应到文件夹其实是对应两层文件夹的cn/mtianyan的。

### 课程总结

Java的诞生和发展;JDK,JRE和JVM;

JRE= JVM + JavaSE标准类库;JDK=JRE+幵岌工具集(例如Javac编译工具等)

Java平台: Java SE , Java标准版;Java EE , Java企业版;Java ME 为移动设备提供了基于Java坏境的开发与应用平台

Java程序的执行流程: .java .class -> Program

Java程序的结构: 类 嵌套方法 main方法入口

下集预告:

在下一集中，将为大家带来Java中的常量和变量的定义及使用。除此之外,还包括标识符、关键字、字面
值和数据类型等相关的概念。



