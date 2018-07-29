## 常量与变量
主要内容: 标识符 关键字 变量 数据类型 类型转换 常量

### 标识符

我们所认识的标识符: 类的名字，每一个字母是字符。

数字不能作为标识符的开头,标识符中间不能有空格。

标识符的命名规则

>标识符可以由字母、数字、下划线(_)和美元符($)组成,不
能以数字开头；标识符严格区分大小写；标识符不能是Java关键字和保留字

IDE中标红的都是关键字，IDEA中为橙色。

![](http://myphoto.mtianyan.cn/20180728042038_xNmD0F_Screenshot.jpeg)

标识符的命名最好能反映出其作用

_hello 合法; Void 合法(区分大小写，和void不一样); abc$123 合法; abc 123 非法(包含空格）

### 关键字

Java中关键字:

![](http://myphoto.mtianyan.cn/20180728043808_x3EYf6_Screenshot.jpeg)

不需要专门记忆，用到自然知道了。

保留字: goto

### 什么是变量？

接受语法结构，仿写，熟悉意义。

什么是变量 & 变量名的命名规则

![](http://myphoto.mtianyan.cn/20180728044123_hWlfYQ_Screenshot.jpeg)

比如我们使用计算机做题，其中的啊a.b想要运算，应该先存储下来。变量就是数据存储。

变量的三个元素:变量类型、变量名和变量值。

| 房间       | 变量   | 
| --------   | -----:  | 
| 入住的客人 | 变量值  | 
| 房间名字   | 变量名  |  
| 房间类型   | 变量类型|  

>房间与变量的类比如上:入住的客人对应变量值; 房间名字对应变量名;房间类型对应变量类型

变量名也是一个标识符，变量名的命名规则:
  
  - 满足标识符命名规则
  - 符合驼峰法命名规范: 单个单词全部小写，多个单词第一个单词小写，后面单词首字母大写。如: 年龄 age 学生姓名 stuName
  - 进来简单，做到见名知意
  - 变量名的长度没有限制
  
类的命名规范:

  - 満足Pascal命名法规范：一个单词构成首字母大写，多个单词构成，每个首字母都大写。类名单词首字母都得大写。
  
好处: 方便阅读。

### 数据类型

![](http://myphoto.mtianyan.cn/20180728045255_ZUD3Hq_Screenshot.jpeg)

>数据类型可分为两大类，基本数据类型 和 引用数据类型: 类( class ); 接口( interface ) ;数组

![](http://myphoto.mtianyan.cn/20180728045438_JCuylb_Screenshot.jpeg)

boolean的两个值为true和false，true代表真，false代表假。byte, short, int，long都是整数数据类型。

### 基本数据类型详解

|数据类型 |说明 |字节
| --------   | -----:  | :----:  |
|byte| 字节型 |1|
|short |短整型 |2|
|int| 整型| 4|
|long |长整型 |8|
|float| 单精度浮点型 |4|
|double| 双精度浮点型 |8|
|char| 字符型 |2|
|boolean |布尔型|1|

### 整型字面值及变量声明

整型字面值：

Java中有三种表示整数的方法:十迸制、八迸制、十六进制

进制表示:

八进制: 以0开头，包括0-7的数字，如037，056;十进制包含0-9数字；十六进制表示:以0x或0X开头,包括0-9的数字,及字母a-f , A-F;如：0x12，0xabcf，0XABCFF。

123(十进制) 023(八进制) 0x1357(十六进制) 0x1abcL（长整型,L或l结尾）

变量声明:

`格式:数据类型 变量名;`

例:

```java
int n; // 声明整型变量n
long count; // 声明长整型变量count
```

变量赋值:

使用"="运算符进行赋值;"="叫作赋值运算符,将运算符右边的值赋给左边的变量。

例:

```java
int n; // 定义int型变量n
n=3; //将3赋值给n
```

可以在定义变量的同时给变量赋值,即**变量的初始化**。
例子:

```java
int n=3;
int octal=037; // 定义int类型变量存放八进制数据
long longNumber=0xa2cdf3ffL; // 定义变量存放十六进制长整型数据
short shortNumber= 123; // 定义变量存放短整型数据
byte b=10; // 定义变量存放byte类型数据
```

![](http://myphoto.mtianyan.cn/20180728140834_oDHqam_Screenshot.jpeg)

>可以看到长整型已经不是合法的int型数据了，再次重申int型数据只有三种表示方法: 十进制，十六进制，八进制。

### 浮点型字面量

浮点型字面值默认情况下表示double类型,也可以在值后加d或D

如: 123.43d 或 123.43D

如表示float类型,则需要在字面值后加f或F

如: 23.4f 或 23.4F

### 浮点型案例

新建一个类 FloatDemo.java

```java
package cn.mtianyan;

public class FloatDemo {
    public static void main(string[] artgs){
        // 定义一个单精度浮点型变量,存放1234.328
        float f = 1234.328f; // 一个浮点型数据末尾什么都不写，是Double型的。
        System.out.println("f="+f);

        // 定义一个双精度浮点型变量，存放5623.456
        double d = 5623.465; //写d，写f后缀都是可以的，小可以变大。
        System.out.println("d="+d);
        
        double d1 = 123L; // Double类型范围最大
        System.out.println("d1="+d1);
        
        // 变量间赋值
        double d2 = d;
        System.out.println("d2="+d2);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728141818_6ajj0r_Screenshot.jpeg)

### 编程练习

分別定乂float、double、 int樸型的数据,并打印輸出。

输出效果图如下:

![](http://myphoto.mtianyan.cn/20180728141943_hyhPwt_Screenshot.jpeg)

任务:
  
  1. 定义一个float类型的变量f1 , 值为98.4
  2、定义一个float类型的变量f2 ,将f1的值赋值给f2
  3、定义一个整型变量n ,值为55
  4、定义一个double类型的变量d1 ,值为555.3

```java
package cn.mtianyan;

public class FloatExercise {
    public static void main(String[] args) {
        float f =98.4f;
        System.out.println("f="+f);
        float f2  = f;
        System.out.println("f2="+f2);
        int n = 55;
        System.out.println("n="+n);
        double d1 = 555.3;
        System.out.println("d1="+d1);
        d1 = n;
        System.out.println("赋值后的d1值为"+d1);

    }
}
```

![](http://myphoto.mtianyan.cn/20180728142422_UCKFdn_Screenshot.jpeg)

### 基本数据类型变量的存储

数据类型分为基本数据类型和引用数据类型；引用数据类型包括数组和类等；类定义的变量又叫对象

按照作用范围分为: 类级、 对象实例级、方法级、块级

>方法级的变量被叫做局部变量

![](http://myphoto.mtianyan.cn/20180728142655_xcLC0P_Screenshot.jpeg)

java中对于内存进行了细分，有栈，堆，常量池等。我们在主函数中定义的变量存储在栈区。

```java
int n = 100;
```

![](http://myphoto.mtianyan.cn/20180728142815_fykTAn_Screenshot.jpeg)

n就是存储了100的这块内存空间的别名。

### 字符型字面值

字符型字面值用单引号内的单个字符表示。如: 'a','b','$'

字符型字面值用单引号引起来。这里的单引号很重要，不能丢掉。单引号中必须只有一个字符。

如何定义字符型变量?

```java
char a = 'a';
char a = 65;
```

```java
package cn.mtianyan;

public class CharDemo {
    public static void main(String[] args) {
        char a = 'a';
        char b = 65;
        System.out.println("a="+a);
        System.out.println("b="+b);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728143331_FhXe89_Screenshot.jpeg)

65是一个大写的A

ASCII码: ASCII ( American Standard Code for Information Interchange , 美国标准信息交换代码)；信息传递的统一标准。

基于拉丁字母的一套电脑编码系统；主要用于显示现代英语和其他西欧语言

使用7位或8位二进制数组合来表示128或256种可能的字符。7位二进制数组合-标准ASCII码;8位二进制数组合(后128位)-扩展ASCII码

标准ASCII码表示大小写字母，标点符号，美式英语中的控制字符等。扩展ASCII码表示特殊符号,外来语言的字母等。

标准ASCII码 0-127

结论: 整型和字符类型是可以互相转换的，参考的转换依据是我们的ASCII码表。

char类型是两个字节表示，无符号的16位整数类型，表示范围0-65535范围。

![](http://myphoto.mtianyan.cn/20180728152223_CZ8u9z_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180728152246_uNtv7r_Screenshot.jpeg)

>可以看到，65535是没有任何提示的，65536会提示转换为int型。强制转换可能引起数据的丢失。

### Unicode编码

ASCII 码是美国标准信息交换码；ASCII码不能支持所有语言。

Unicode编码又称为统一码、万国码.Unicode编码的目标是支持世界上所有的字符集;

```java
char c = '\u005d'; // 005d四个16进制数

// Unicode表示法,在值前加前缀\u

char cOut = (char) 65536;
System.out.println("cOut=" +cOut);
// 定义变量存放unicode编码表示的字符
char uc = '\u005d'; //必须是16进制四个数，32位。
System.out.println("u=" +uc);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728155021_6W5GHc_Screenshot.jpeg)

### 布尔类型字面值

布尔值只能定义为true和false

例子:

```java
boolean b=true;
```

字符串字面值

```java
str1 = "Hello,mtianyan!"
System. outprintln("str="+str);
```

字符串不属于基本数据类型，它是类！

字符串的字面值如何表示？

>双引号引起来的0个或多个字符。

字符串的定义:

```java
package cn.mtianyan;

public class StringDemo {

    public static void main(String[] args) {
        // 定义一个空字符串
        String s1 = "";
        System.out.println("s1="+s1);

        String s2 = "Hello";
        System.out.println("s2="+s2);

        String s3 = "A\u005d\u005fB"; // A,B正常显示，普通与Unicode可以混在一个字符串里
        System.out.println("s3="+s3);

        String s4 = "Hello  mtianyan"; // 空格也是一个字符，字符串的长度也要算上空格。
        System.out.println("s4="+s4);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728172826_14xjCi_Screenshot.jpeg)

>字符串字面值必须用双引号，可以是空串啥都没有。

### 变量综合案例

![](http://myphoto.mtianyan.cn/20180728173101_6pV6bw_Screenshot.jpeg)

只进行声明，不进行初始化的变量是不能使用的。

```java
package cn.mtianyan;

public class VarDemo {
    public static void main(String[] args) {
        // 定义两个整型变量
        int x=3,y=5;
        // x=3,y=5; 形式是错误的
        System.out.println("x="+x);
        System.out.println("y="+y);
        // 换行问题
        System.out.printf(x+" "+y +'\n');
        // System.out.println(); // 换行
        System.out.printf(x+","+y);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728173533_I9ulT2_Screenshot.jpeg)

**转义字符**

|转义字符| 描述|
|--------|------|
|`\uxxxx`| 四位16进制数所表示的字符|
|`\'`| 单引号字符|
|`\"`| 双引号字符|
|`\\`| 反斜杠字符|
|`\r`| 回车|
|`\n`| 换行|
|`\t`| 横向跳格|
|`\b`| 退格|

回车和换行是不一样的，回车光标会回到光标的最开始，换行是换到当前光标位置的下一行。

```java
System.out.printf(x+"\t"+y +'\n');
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728183906_9666be_Screenshot.jpeg)

```java
        System.out.println('\t');
        System.out.println(x+'\t');
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728184112_yBvYtr_Screenshot.jpeg)

>将字符串转换为整数进行了运算

记得用双引号，或者前面加一个空串""

```java
        System.out.printf(x+","+y);
        System.out.printf("\n\'"+x+"\'");
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728184411_ZHV57A_Screenshot.jpeg)

java中是可以使用汉字作为变量名的，但是不建议使用

```java
        char ch = '天';
        System.out.println(ch);
        char 中文 = '涯';
        System.out.println(中文);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728184753_3Dovqk_Screenshot.jpeg)

用科学计数法表示浮点型数据

```java
        double d = 1.23E5; //科学计数法1.23*10^5
        float f = 1.23e5f;
        double d1 =.2; //代表0.2

        System.out.println("d=" +d);
        System.out.println("f=" +f);
        System.out.println("d1=" +d1);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728195837_DOuSYa_Screenshot.jpeg)

### 数据类型转换的基本概念

类型转换分为自动类型转换和强制类型转换

```java
long n=253;（int转）
```

char 65536 强制转换，可能引起数据丢失

```java
char cOut = (char) 65536;
```

自动类型转换(隐式类型)顺序

![](http://myphoto.mtianyan.cn/20180728200222_mKxzGP_Screenshot.jpeg)

>实线表示无信息丢失的数据类型转换; 虚线表示可能在转换时出现精度丢失。

强制类型转换:

如果A类型的数据表示范围比B类型大,则将A类型的值赋值给B类型,需要强制类型转换。

例子:

```java
double d= 123.4;
float f= (float)d;
```

强制数据类型转换的格式: (数据类型)数值

### 数据类型转换案例

```java
package cn.mtianyan;

public class TypeExchange {
    public static void main(String[] args) {
        // char类型和int类型之间的转换
        char c = (char) 65536;
        int n;
        n = c; // 隐式类型转换
        c = (char) n;

        // 整型和浮点型转换
        int x =100;
        long y = x;
        x = (int)y;
        float f = 1000000000000000L;
        System.out.println("f="+f);
        float f1 = 102312392189367L;
        System.out.println("f1="+f1); // 会发生数据丢失
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728201207_SdLrsI_Screenshot.jpeg)

可以看到确实丢失了一部分。

### 编程练习

定义各种数据类型的变量,按要求为它们赋值,并打印输出。

效果图:

![](http://myphoto.mtianyan.cn/20180728201311_Dd5Wsk_Screenshot.jpeg)

备注:由于编辑器环境的不同,第一行字符c的输出结果也会有所不同。

任务:

1、定义一个整型字面値67832,赋值姶char类型変量c,并将c的值輸出
2、定义一个整型変量n,初始化为65
3、定义一个字符型变量c1 ,赋值为n ,并输出c1的值。
4、定义一个长整型変量l, 值为987654321
5、定义一个整型変量i,赋值为,并输出i的値
6、定义一个float型変量f,将变量l的值赋值给f,并輸出f的値
7、将float的值f, 童新赋值给変量l, 并输出l的償

```java
package cn.mtianyan;

public class DataTypeExercise {
    public static void main(String[] args) {
        char c = (char) 67832;
        System.out.println("c="+c);
        int n = 65;
        char c1 = (char) n;
        System.out.println("c1="+c1);
        long l = 987654321;
        int i = (int) l;
        System.out.println("i="+i);
        float f = l;
        System.out.println("f="+f);
        l = (long) f;
        System.out.println("l="+l);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728202225_0EeeAl_Screenshot.jpeg)

### 常量

```java
final int n =5; // final 关键字定义常量
```

![](http://myphoto.mtianyan.cn/20180728202510_eQhcP8_Screenshot.jpeg)

>可以看到常量是不可以再被赋值的。

```java
        final double PI = 3.14; // 下面可以只更改一个地方
        final double MIN_VALUE = 0;
```

命名时，常量一般使用大写字母表示，多个单词字母大写，中间下划线隔开。

java中字面值也叫做常量，字面值是变量和常量的实际表示的数值。流程控制时，将字面值和final定义的，都统称为常量。

### 变量与常量总结

标识符的命名规则

  1. 必须由字母、数字、下划线(_)和美元符($)组成
  2. 首字母只能是字母、下划线(_)和美元符($),不能是数字。
  3. 不能是Java的关键字和保留字
  4. 严格区分大小写
  5. 要有意义

public是关键字，Public就是合格的标识符。

关键字（已经接触了的）:

![](http://myphoto.mtianyan.cn/20180728204432_rNS4Ay_Screenshot.jpeg)

数据类型:

数据类型分为基本数据类型和引用数据类型(字符串和数组类型)。

![](http://myphoto.mtianyan.cn/20180728204555_NO3LHV_Screenshot.jpeg)

变量的定义和初始化: `int n; n=5;` 初始化: `int n=5;`

![](http://myphoto.mtianyan.cn/20180728204736_eEKcQ5_Screenshot.jpeg)

ASCII码 和 Unicode编码

类型转换: 隐式类型转换 强制类型转换

字面值也是常量的一种

在下一集中,将为大家带来Java中运算符的使用,同时为了更好的进行学习,还介绍了简单条件语句!





