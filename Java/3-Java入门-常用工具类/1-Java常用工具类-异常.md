除了自定义类，java中还为我们提供了一系列的工具类。我们会为大家介绍6种最常用的工具类。

如何进行应用异常处理程序中的问题？(系统介绍)

如何通过包装器类实现基本数据类型的对象化处理

String、StringBuilder是如何进行字符串信息操作的

常用集合框架及实现类使用

如何使用Java输入输出流进行文件读写

如何使用多线程实现数据并发通信(难度从上向下依次递增)

### 异常课程介绍

什么是异常？如何处理异常？

try-catch-finally;throw;throws;自定义异常;异常链

### 什么是异常？

异常: 意外、例外。异常本质上是程序上的错误。

错误在我们编写程序的过程中会经常发生,包括编译期间和运行期间的错误。

括号没有正常的配对; 语句结束后少写了分号;关键字编写错误 前面这几种都是编译期间的错误。通常这种错误编译器会帮助我们一起进行修订

但是运行期间的错误，编译器就无能为力了。

前面我们遇到的程序中的异常:

使用空的对象引用调用方法

```java
String str=null;
System.out.println(str.length());
```

数组访问时下标越界

```java
int[] ary={1,2,3};
for(int i=0;i<=3;i++){
  System.out.println(ary[i]);
}
```

算术运算时除数为0

```java
int one =12;
int two=0;
System.out.println(one/two);
```

类型转换时无法正常转型

```java
class Animal {
}
class Dog extends Animal {
}
class Cat extends Animal{
}

public class Test {
  public static void main(String[] args) {
      Animal a1 = new Dog();
      Animal a2 = new Cat();
      Dog d1 = (Dog)a1;
      Dog d2 = (Dog)a2;
}
```

以上都是运行期间的错误。以上这些代码在编译时是没有错误提示的。

在程序运行过程中,意外发生的情况,背离我们程序本身的意图的表现,都可以理解为异常。

错误执行 & 执行到崩溃

如何针对程序运行期间产生的异常进行合理的处理?

Java中有强大的异常处理机制。

### 异常分类

异常可以理解为一种事件，当它发生时会影响正常的程序运行流程。

Java中通过Throwable来进行各种异常信息的描述。

![](http://myphoto.mtianyan.cn/20180805134916_S0QvMt_Screenshot.jpeg)

Error是程序无法处理的错误，表示运行应用程序中较严重问题。Java虚拟机问题(虚拟机错误 VirtualMachineError;内存溢出OutOfMemoryError;线程死锁 ThreadDeath);它们在应用程序的控制和处理能力之外,而且绝大多数是程序运行时不允许出现的状况。对于设计合理的应用程序来说,即使确实发生了错误,本质上也不应该试图去处理它所引起的异常状况。

Exception是程序本身可以处理的异常。异常处理通常指针对这种类型异常的处理。

Exception可以分为两大类: 非检查异常(Unchecked Exception); 检查异常(Checked Exception)

非检查异常是编译器不要求强制处置的异常，它包括RuntimeException以及它的子类: 空指针异常 NullPointerException;数组下标越界异常 ArrayIndexOutOfBoundsException;算数异常 ArithmeticException;类型转换异常 ClassCastException;

java程序在编译阶段是不会去检查上面这些runtime异常的

![](http://myphoto.mtianyan.cn/20180805135549_8W4STf_Screenshot.jpeg)

检查异常，编译器要求必须处置的异常。如: IO异常 IOException; SQL异常 SQLException

### 异常处理分类

在Java应用程序中,异常处理机制为: 抛出异常;捕捉异常

异常要先被抛出，然后才能被捕获。

抛出异常指的就是当一个方法当中出现异常，方法会去创建异常对象，并去交付给运行时系统来进行处理。

异常对象: 异常类型以及异常出现时的程序状态等

当运行时系统捕获到这个异常，此时会去寻找合适的处理器，如果找到了，就会执行处理器的相关逻辑；如果始终没找到，运行就会终止

对于运行时异常、错误或可查异常, Java技术所要求的异常处理方式有所不同。

Java规定: 对于可查异常（检查异常(Checked Exception)）必须捕捉、或者声明抛出

允许忽略不可查的RuntimeException(含子类)和Error(含子类)。

对于抛出异常和捕获异常，Java中通过5个关键字来实现: try catch finally throw throws

![](http://myphoto.mtianyan.cn/20180805140509_lTBUWd_Screenshot.jpeg)

其中try catch finally是一组，是用来捕获异常的。try 执行可能产生异常的代码; catch 捕获异常;finally 无论是否发生异常代码总能执行;

![](http://myphoto.mtianyan.cn/20180805140653_rbjQIN_Screenshot.jpeg)

throws 声明可能要抛出的异常; throw 手动抛出异常

### try-catch-finally简介

```java
public void method(){
    try {
          //代码段1
          //产生异常的代码段2
        }catch (异常类型 ex) {
          //对异常进行处理的代码段3
        }finally{
          //代码段4
        }
}
```

try块后可接零个或多个catch快,如果没有catch块则必须跟一个finally块。简单来讲就是try要和catch或finally组合使用，不可单独存在。catch和finally如果没有try的加入，也是无法起作用的。

```java
package cn.mtianyan.exception;

import java.util.Scanner;

public class TryDemo {
    public static void main(String[] args) {
//        // 定义两个整数，输出两数之商
//        int one = 12;
//        int two = 2;
//        System.out.println("one/two="+one/two);

        // 用户输入不可控
        System.out.println("====运算开始====");
        Scanner scanner = new Scanner(System.in);
        System.out.print("请输入第一个数字: ");
        int one = scanner.nextInt();
        System.out.print("请输入第二个数字: ");
        int two = scanner.nextInt();
        System.out.println("one/two="+one/two);
        System.out.println("====运算结束====");
    }
}
```

注释部分是我们在程序写死的数字逻辑，是可以正常运行的。但一旦我们将这些变量交给了用户，那么用户输入的不可控因素就会给程序带来异常。

```java
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at cn.mtianyan.exception.TryDemo.main(TryDemo.java:19)
```

![](http://myphoto.mtianyan.cn/20180805142406_a3Sxcl_Screenshot.jpeg)

```java
Exception in thread "main" java.util.InputMismatchException
	at java.base/java.util.Scanner.throwFor(Scanner.java:939)
	at java.base/java.util.Scanner.next(Scanner.java:1594)
	at java.base/java.util.Scanner.nextInt(Scanner.java:2258)
	at java.base/java.util.Scanner.nextInt(Scanner.java:2212)
	at cn.mtianyan.exception.TryDemo.main(TryDemo.java:16)
```

![](http://myphoto.mtianyan.cn/20180805142446_alpmzx_Screenshot.jpeg)

### try-catch结构进行异常处理

将可能出现异常的代码放在try块里。

```java
package cn.mtianyan.exception;

import java.util.Scanner;

public class TryDemo {
    public static void main(String[] args) {

        // 用户输入不可控
        System.out.println("====运算开始====");
        try {
            Scanner scanner = new Scanner(System.in);
            System.out.print("请输入第一个数字: ");
            int one = scanner.nextInt();
            System.out.print("请输入第二个数字: ");
            int two = scanner.nextInt();
            System.out.println("one/two=" + one / two);
        }catch (Exception e){
            System.out.println("程序出错啦");
        }
        System.out.println("====运算结束====");
    }
}
```

![](http://myphoto.mtianyan.cn/20180805142915_cBrOaZ_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180805142930_u52mBu_Screenshot.jpeg)

有没有办法可以提示我是哪里出错，出的什么错呢？

```java
catch (Exception e){
            System.out.println("程序出错啦");
            e.printStackTrace();
        }
```

![](http://myphoto.mtianyan.cn/20180805143152_qy32Fa_Screenshot.jpeg)

printStackTrace输出的格式有些诡异。错误栈应该是倒着看，最后一行是我们自己代码中的位置。

```java
finally {
            System.out.println("====运算结束====");
        }
```

finally块保证一定会被执行。

### 使用多重catch结构处理异常

针对不同的异常有不同的处理方式该如何做到？

```java
catch (ArithmeticException e){
            System.out.println("除数不可以为0");
            e.printStackTrace();
        }catch (InputMismatchException e){
            System.out.println("请输入整数");
            e.printStackTrace();
        }catch (Exception e){
            System.out.println("程序出错了");
        } 
```

![](http://myphoto.mtianyan.cn/20180805143855_Z00Gaw_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180805143915_OV0m9z_Screenshot.jpeg)

推荐最后使用Exception兜底，必须放在最后一个。

```java
package cn.mtianyan.exception;

public class TestExercise {
    public static void main(String args[]) {
        try {
            int a = 1 - 1;
            System.out.println("a = " + a);
            int b = 4 / a;
            int c[] = {1};
            c[10] = 99;
        } catch (ArithmeticException e) {
            System.out.println("除数不允许为0");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("数组越界");
        }
    }
}
```

上述代码的运行结果为:

![](http://myphoto.mtianyan.cn/20180805144448_dYj8vD_Screenshot.jpeg)

第一次发生异常被捕获之后，程序去执行了catch块中的语句，不会再去执行首次出现异常行之下的try中代码

### 终止finally执行方法

通常情况，finally块是一定会执行的。

```java
catch (ArithmeticException e){
            System.exit(1);
            System.out.println("除数不可以为0");
            e.printStackTrace();
        }
```

![](http://myphoto.mtianyan.cn/20180805174948_stIzJJ_Screenshot.jpeg)

System.exit(1);终止当前虚拟机运行。程序无条件终止运行。

0代表正常退出,非0代表非正常退出。如果程序按照正常逻辑执行需要退出时,调用System.exit(O)。如果发生异常而退出,比如在catch块使用,则调用System.exit(1);

### return关键字在异常处理中的作用

之前的学习中我们知道return关键字可以用于方法返回值的带回。

```java
package cn.mtianyan.exception;
import java.util.Scanner;

public class TryDemoReturn {
    public static void main(String[] args) {

        System.out.println("one/two="+add());

    }
    public static int add(){
        // 用户输入不可控
        System.out.println("====运算开始====");
        try {
            Scanner scanner = new Scanner(System.in);
            System.out.print("请输入第一个数字: ");
            int one = scanner.nextInt();
            System.out.print("请输入第二个数字: ");
            int two = scanner.nextInt();
            return one/two;
        }catch (ArithmeticException e){
            System.out.println("除数不可以为0");
            return 0;
        } finally {
            System.out.println("====运算结束====");
            return -9999;
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805220938_Aa6LgK_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180805221117_cgsYcM_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180805221200_UHHjdf_Screenshot.jpeg)

可以看到，不管有多少个return在前面，都会以最后一个finally中的return为准作为返回值。

删除掉finally中的return语句，程序就可以按照我们预期的状态运行。

![](http://myphoto.mtianyan.cn/20180805221403_9Xld5Q_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180805221422_NZW4lF_Screenshot.jpeg)

```java
package cn.mtianyan.exception;

public class TestExerciseTwo{
    public static int test(int b){
        try{
            b+=10;
            return b;
        }catch(Exception e){
            return 1;
        }finally{
            b+=10;
            return b;
        }
        }
    public static void main(String[] args) {
        int num =10;
        System.out.println(test(num));
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805222000_psSlqP_Screenshot.jpeg)

### 使用throws声明异常类型

可以通过throws声明将要抛出何种类型的异常,通过throw将产生的异常抛出。

如果一个方法可能会出现异常,但没有能力处理这种异常,可以在方法声明处用throws子句来声明抛出异常。谁调用了这个方法，谁就该去处理这样的异常。

throws语句用在方法定义时声明该方法要抛出的异常类型。

```java
public void method() throws Exception1,Exception2,...,ExceptionN {
    //可能产生异常的代码
}
```

当方法抛出异常列表中的异常时,方法将不对这些类型及其子类类型的异常作处理,而抛向调用该方法的方法,由他去处理。

```java
    public static int add() throws ArithmeticException {
        // 用户输入不可控
        System.out.println("====运算开始====");
        Scanner scanner = new Scanner(System.in);
        System.out.print("请输入第一个数字: ");
        int one = scanner.nextInt();
        System.out.print("请输入第二个数字: ");
        int two = scanner.nextInt();
        System.out.println("====运算结束====");
        return one / two;
    }
```

上面的代码在方法中声明可能抛出的异常，去除掉方法自己的异常处理，交给上层处理。可以采取快捷键来生成try catch包裹(生成时会自动检查异常类型)。

```java
        try {
            System.out.println("one/two=" + add());
        } catch (ArithmeticException e) {
          
            e.printStackTrace();
        }
```

![](http://myphoto.mtianyan.cn/20180805223435_Ca7sf7_Screenshot.jpeg)

通过throws抛出异常时，针对可能出现的多种异常情况，解决方案:

    1. throws后面接多个异常类型,中间用逗号分隔
    2. throws后面接Exception，直接Exception的时候，编译器会提示你test方法可能会产生异常，因为Exception是父类包含了出现检查异常的情况。

![](http://myphoto.mtianyan.cn/20180805224724_IbZo5p_Screenshot.jpeg)

而我们只写几个具体的异常类型(非检查型异常时)时是不会有提示的，如果想要提醒别人注意添加异常处理，可以添加文档注释。

```java
    /**
     * 两数字相加的方法
     * @return
     * @throws ArithmeticException
     * @throws InputMismatchException
     */
```

![](http://myphoto.mtianyan.cn/20180805225208_kOtW3h_Screenshot.jpeg)

### throw抛出异常对象

throw用来抛出一一个异常。

例如: `throw new IOException();`

throw抛出的只能够是可抛出类Throwable或者其子类的实例对象。

例如: `throw new String("出错啦");` 是错误的

```java
public void method(){
  try {
    //代码段1
  throw new 异常类型();
  } catch(异常类型 ex){
    //对异常进行处理的代码段2
  }
}
```

方案一: 自己抛出的异常自己进行异常处理。

方案二: 在抛出异常处通过throws关键字标明异常类型。

```java
public void method() throws 异常类型{
  //代码段1
    throw new 异常类型();
}    
```

1. 规避可能出现的风险; 2. 完成一些程序的逻辑

场景: 要求:如果入住人员年龄在18岁以下或者80岁以上，必须由亲属陪同入住,不能单独入住。

```java
public static void testAge() {

		try {
			System.out.println("请输入年龄：");
			Scanner input = new Scanner(System.in);
			int age = input.nextInt();
			if (age < 18 || age > 80) {
				throw new Exception("18岁以下，80岁以上的住客必须由亲友陪同");
			} else {
				System.out.println("欢迎入住本酒店");
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
```

```java
	public static void main(String[] args) {
			testAge();
	}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805230619_COd1Dp_Screenshot.jpeg)

throw抛出异常对象的处理方案：
  
    1. 通过try..catch包含throw语句-自己抛自己处理
  	2. 通过throws在方法声明出抛出异常类型-谁调用谁处理-调用者可以自己处理，也可以继续上抛,此时可以抛出与throw对象相同的类型或者其父类

```java
	public static void testAge() throws Exception {
		System.out.println("请输入年龄：");
		Scanner input = new Scanner(System.in);
		int age = input.nextInt();
		if (age < 18 || age > 80) {
			throw new Exception("18岁以下，80岁以上的住客必须由亲友陪同");
		} else {
			System.out.println("欢迎入住本酒店");
		}
	}
```

```java
		try {
			testAge();
		} catch (Exception e) {
			e.printStackTrace();
		}
```

![](http://myphoto.mtianyan.cn/20180805231750_jle777_Screenshot.jpeg)

### 关于throw抛出异常类型问题的逼叨叨

```java
	public static void testAge() throws Throwable {
		System.out.println("请输入年龄：");
		Scanner input = new Scanner(System.in);
		int age = input.nextInt();
		if (age < 18 || age > 80) {
			throw new Exception("18岁以下，80岁以上的住客必须由亲友陪同");
		} else {
			System.out.println("欢迎入住本酒店");
		}
	}
```

```java
		try {
			testAge();
		} catch (Throwable e) {
			e.printStackTrace();
		}
```

因为Throwable是Exception异常的父类。throws后面不能是Exception的子类。

![](http://myphoto.mtianyan.cn/20180805232249_RnY314_Screenshot.jpeg)

此时可以抛出与throw对象相同的类型或者其父类(不能是子类)

```java
	public static void testAge(){
		System.out.println("请输入年龄：");
		Scanner input = new Scanner(System.in);
		int age = input.nextInt();
		if (age < 18 || age > 80) {
			throw new ArithmeticException();
//			throw new Exception("18岁以下，80岁以上的住客必须由亲友陪同");
		} else {
			System.out.println("欢迎入住本酒店");
		}
	}
```

非检查异常，不做强制处理。

```java
			testAge(); //无提示
```

throw抛出异常时是不推荐抛出非检查异常的。

### 自定义异常

使用Java内置的异常类可以描述在编程时出现的大部分异常情况。

也可以通过自定义异常描述特定业务产生的异常类型。

所谓自定义异常,就是定义一个类,去继承Throwable类或者它的子类。

新建一个类: HotelAgeException 继承自Exception类

```java
package cn.mtianyan.exception;

public class HotelAgeException extends Exception{
    public HotelAgeException(){
        super("18岁以下，80岁以上的住客必须由亲友陪同");
    }
}
```

```java
	public static void testAge() throws HotelAgeException {
		System.out.println("请输入年龄：");
		Scanner input = new Scanner(System.in);
		int age = input.nextInt();
		if (age < 18 || age > 80) {
			throw new HotelAgeException();
		} else {
			System.out.println("欢迎入住本酒店");
		}
	}
```

因为是继承自Exception类的，会提醒throws。

```java
		try {
			testAge();
		} catch (HotelAgeException e) {
			System.out.println(e.getMessage());
			System.out.println("酒店前台工作人员不允许为其办理入住登记");
		} 
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805233217_Xxrwb8_Screenshot.jpeg)

当然后面可以多添加几个catch来捕获。

### 异常链

有时候我们会捕获一个异常后在抛出另一个异常

![](http://myphoto.mtianyan.cn/20180805233410_3gR2VH_Screenshot.jpeg)

后一个方法接收前一个方法抛出的异常对象。

```java
package cn.mtianyan.exception;

public class TryDemoFive {
    public static void main(String[] args) {
        try {
            testThree();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void testOne() throws HotelAgeException {
        throw new HotelAgeException();
    }
    public static void testTwo() throws Exception {
        try {
            testOne();
        } catch (HotelAgeException e) {
            throw new Exception("我是新产生的异常1");
        }
    }
    public static void testThree() throws Exception {
        try {
            testTwo();
        } catch (Exception e) {
            throw new Exception("我是新产生异常2");
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180805233751_Lv5qYD_Screenshot.jpeg)

最后只会获得最后一个方法调用时throw的异常，前面的异常都丢失了。如何解决这种异常的丢失情况，让异常链的情况为我们所知。

构造方法中添加上一层异常e，或者使用initCause(e)

```java
public static void testOne() throws HotelAgeException {
        throw new HotelAgeException();
    }
    public static void testTwo() throws Exception {
        try {
            testOne();
        } catch (HotelAgeException e) {
            throw new Exception("我是新产生的异常1",e);
        }
    }
    public static void testThree() throws Exception {
        try {
            testTwo();
        } catch (Exception e) {
            Exception e1 = new Exception("我是新产生异常2");
            e1.initCause(e);
            throw e1;
        }
    }
```

![](http://myphoto.mtianyan.cn/20180805234440_GsTqXo_Screenshot.jpeg)

顾名思义就是:将异常发生的原因一个传一个串起来,即把底层的异常信息传给上层,这样逐层抛出。

### 课程总结

程序中的异常

>在程序运行过程中,意外发生的情况,背离我们程序本身的意图的表现,都可以理解为异常。

利用Java中的异常机制,我们可以更好地提升程序的健壮性。

在Java中, 通过Throwable及其子类描述各种不同的异常类型。

![](http://myphoto.mtianyan.cn/20180806000117_GopCuL_Screenshot.jpeg)

检查异常，编译器强制要求进行异常处理。

异常处理: 

在Java应用程序中,异常处理机制为:抛出异常、捕捉异常

通过五个关键字来实现: try,catch,finally,throw,throws

![](http://myphoto.mtianyan.cn/20180806000320_7nHWbC_Screenshot.jpeg)

try中未发生异常：直接执行try catch块后的代码段

![](http://myphoto.mtianyan.cn/20180806000413_j9v4Sx_Screenshot.jpeg)

当try块中发生了异常,产生异常对象与catch中异常类型匹配

![](http://myphoto.mtianyan.cn/20180806000505_TExUxv_Screenshot.jpeg)

当try块中发生了异常,产生异常对象与catch中异常类型不匹配

![](http://myphoto.mtianyan.cn/20180806000547_ObFBL0_Screenshot.jpeg)

使用多重catch进行异常类型信息匹配

![](http://myphoto.mtianyan.cn/20180806000853_QTeRkG_Screenshot.jpeg)

无论是否执行catch块通常都能正常执行。
![](http://myphoto.mtianyan.cn/20180806001347_AWodDh_Screenshot.jpeg)

一旦加入了System.exit(1)会强制终止执行

![](http://myphoto.mtianyan.cn/20180806001431_4D4QW3_Screenshot.jpeg)

return关键字，一定是finally执行完成之后，才会去执行相应的代码。

![](http://myphoto.mtianyan.cn/20180806001717_S9vR2g_Screenshot.jpeg)

**实际应用中的经验与总结:**

  - 处理运行时异常时,采用逻辑去合理规避同时辅助try-catch处理
  - 在多重catch块后面,可以加一个catch(Exception)来处理可能会被遗漏的异常
  - 对于不确定的代码,也可以加上try-catch ,处理潜在的异常
  - 尽量去处理异常,切忌只是简单的调用printStackTrace()去打印输出
  - 具体如何处理异常,要根据不同的业务需求和异常类型去决定
  - 尽量添加finally语句块去释放占用的资源

### 关于方法重写时throws的注意事项

可以通过throws声明将要抛出何种类型的异常,通过throw将产生的异常抛出。

如果一个方法可能会出现异常,但没有能力处理这种异常,可以在方法声明处用throws子句来声明抛出异常,

抛出的异常有两种处理方案: 自己处理，抛出谁调用谁处理。

当子类重写父类抛出异常的方法时,声明的异常必须是父类方法所声明异常的同类或子类。

```java
package cn.mtianyan.exception;

public class FatherTest {
    public void test() throws HotelAgeException {
        throw new HotelAgeException();
    }
}
```

```java
package cn.mtianyan.exception;

public class SonTest extends FatherTest {
    @Override
    public void test() throws Exception { // 报错

    }
}
```

![](http://myphoto.mtianyan.cn/20180806002439_sZv8xs_Screenshot.jpeg)

```java
public class SonTest extends FatherTest {
    @Override
    public void test() throws RuntimeException {

    }
}
```

上面代码RuntimeException就不会报错。

```java
package cn.mtianyan.exception;

public class HotelAgeException extends Exception{
    public HotelAgeException(){
        super("18岁以下，80岁以上的住客必须由亲友陪同");
    }
}

class SubException extends HotelAgeException{

}
```

```java
package cn.mtianyan.exception;

public class SonTest extends FatherTest {
    @Override
    public void test() throws SubException {

    }
}
```

此时也是不会报错的。当子类重写父类抛出异常的方法时,声明的异常必须是父类方法所声明异常的同类或子类。

自定义异常: 可以通过自定义异常描述特定业务产生的异常类型。所谓自定义异常,就是定义一个类,去继承Throwable类或者它的
子类。

异常链: 当捕获一个异常后再抛出另一个异常时,如果希望将异常发生的原因一个传一个串起来 ,即把底层的异常信息传给上层,就形成了异常链。

构造方法带参数e或者initCause方式来实现。

在下一集中，我们将针对Java中包装类的相关知识进行学习,基本数据类型与其对应包装类的对应关系是怎样的呢?让我们来一一认识他们。



















































