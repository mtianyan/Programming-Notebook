流程控制;流程控制语句:

顺序、选择、循环

什么是顺序？

```java
package cn.mtianyan.flow;

public class OctalOutput {
    public static void main(String[] args) {
        //定义一一个整型变量n ,值为123
        int n;
        n = 123;
        System.out.println("n=" + n);
        //定义一个整型变量,存放八进制数
        int octal = 037;
        System.out.println("octal=" + octal); // 输出结果为十进制
        System.out.println("octal=" + Integer.toOctalString(octal)); // 输出结果为八进制对应字符串
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729122606_ypyCnV_Screenshot.jpeg)

顺序结构，一句一句按着顺序执行。

选择结构: if if-else

```java
if(条件)
{
<语句块>
}
if(条件){
<语句块>
}
else{
<语句块>
}
```

根据条件，选择执行if还是执行else后面的语句。

比如之前用户输入一个数，判断计数还是偶数，不想每次都重新运行。希望可以一直输入，就要用到循环结构。循环设置终止条件。

三大流程控制语句:顺序、选择、循环

学习的主要内容:

选择结构: if结构;if-else结构;多重if;嵌套if;switch结构

循环结构 while;do-while;for;循环嵌套

### 多重if结构

选择结构

```java
if(条件)
语句;

if(条件){
语句;
}
```

只有一条语句，大括号可以省略。条件小括号后面没有分号。

```java
if(条件)
语句1;
else
语句2;

if(条件){
语句1;
}else{
语句2;
}
```

案例需求描述:编写一个程序,根据考试成绩,输出相应的评定信息。
  - 成绩大于等于90分,输出“优”
  - 成绩大于等于80分且小于90分,输出“良”
  - 成绩大于等于60分小于80分,输出“中”
  - 成绩小于60分, 输出“不及格'

```java
package cn.mtianyan.flow;

import java.util.Scanner;

public class ScoreAssess {
    public static void main(String[] args) {
        System.out.println("请输入成绩: ");
        Scanner scanner = new Scanner(System.in);
        int score = scanner.nextInt();
        if(score >=90) {
            System.out.println("优");
        }
        if (score>=80 & score<90){
            System.out.println("良");
        }
        if(score >=60 & score<80){
            System.out.println("中");
        }
        if (score <60){
            System.out.println("不及格");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729154549_TNFL4G_Screenshot.jpeg)

这是我们通过简单的多个if的实现，可以看到>=90和<90就是一种取反的范围。

多重if结构语法格式:

```java
if(表达式1)
  语句1;
else if(表达式2)
  语句2;
else if(表达式3)
  语句3;
else
  语句n;
```

```java
package cn.mtianyan.flow;

import java.util.Scanner;

public class ScoreAssess {
    public static void main(String[] args) {
        System.out.println("请输入成绩: ");
        Scanner scanner = new Scanner(System.in);
        int score = scanner.nextInt();
        if(score >=90) {
            System.out.println("优");
        }
        else if (score>=80){ // 相当于score>=80 & score<90
            System.out.println("良");
        }
        else if(score >=60){
            System.out.println("中");
        }
        else{
            System.out.println("不及格");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729154959_JeaHxk_Screenshot.jpeg)

这里应该注意其中包含的隐含条件。else if 是上句if的取反范围加上自己的if条件。

```java
package cn.mtianyan.flow;

public class IfChoose {
    public static void main(String[] args) {

        int a = 5, b = 4, c = 3, d = 2;
        if (a > b && b > c) {
            System.out.println(d);
        } else if ((c - 1 >= d) == 1) {
            System.out.println(d + 1);
        } else {
            System.out.println(d + 2);
        }
    }
}
```

Error:(9, 33) java: 不可比较的类型: boolean和int

```java
else if ((c - 1 >= d) == true) // boolean只能与布尔值进行比较
```

#### 编程练习

根据下面数学函数,编写程序根据x的值,计算y的值,最后输出x和y的值。(使用多重if-else结构完成)

![](http://myphoto.mtianyan.cn/20180729155744_dl6Zoi_Screenshot.jpeg)

任务

  1. 定义整型变量x并初始化为-5
  2. 定义整型变量y并初始化0
  3. 根据所给条件,使用多重if-else结构求y的値
  4. 输出x和y的値

```java
package cn.mtianyan.flow;

public class IfElseDemo {
    public static void main(String[] args) {
        int x = -5;
        int y = 0;
        if(x<0){
            y=-1;
        }else if(x==0){
            y=0;
        }else{
            y=1;
        }
        System.out.println("x="+x+",y="+y);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729160209_5mC7Ae_Screenshot.jpeg)

### 嵌套if结构

将整个if块插入另一个if块中

```java
if(表达式1)
  if(表达式2)
    if(表达式3)
        语句;
else
  语句;
```

有多个if，要注意跟哪个else对齐。

案例: 从键盘输入两个整数,经过判断输出他们的关系(大于,小于，等于)

```java
package cn.mtianyan.flow;

public class IntCompare {
    public static void main(String[] args) {
        int x = 5,y=15;
        // 判断x和y是否相等
        if (x != y){
            if (x >y ){
                System.out.println(x+"大于"+y);
            }else{
                System.out.println(x+"小于"+y);
            }
        }else {
            System.out.println(x+"和"+y+"相等");
        }

        if (x != y)
            if (x >y )
                System.out.println(x+"大于"+y);
        else
            System.out.println(x+"和"+y+"相等"); // else语句与离它最近的进行匹配，对应到x>y这个了
    }
}
```

![](http://myphoto.mtianyan.cn/20180729161033_nna2fM_Screenshot.jpeg)

大括号要加，else与最近的if匹配。

### Switch结构

if和switch的区别

if结构:
  - 判断条件是布尔类型,判断条件是一个范围(成绩大于60)
  
switch结构:
  - 判断条件是常量值

```java
switch(表达式){
  case 常量表达式1:
      语句1; break;
  case 常量表达式2:
      语句2;break;
  default:
  语句3;
}
```

遇到break，会跳出。default可以省略，表达式值与常量表达式匹配。JDK6.0以前这个表达式最终结果只能是int类型(等价的char等)。

JDK 7.0以后表达式的值可以是基本数据类型的byte,short,int,char ,以及**String类型**。

案例 从键盘输入1-7之间的任意数字,分别输出对应的信息。

1一星期一;2一星期二;3一星期三;4一星期四;5-星期五;6一星期六;7一星期日;

```java
package cn.mtianyan.flow;

import java.util.Scanner;

public class WeekDemo1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入1-7之间的数字: ");
        int n = scanner.nextInt();

        switch (n){
            case 1:
                System.out.println("星期一");
            case 2:
                System.out.println("星期二");
            case 3:
                System.out.println("星期三");
            case 4:
                System.out.println("星期四");
            case 5:
                System.out.println("星期五");
            case 6:
                System.out.println("星期六");
            case 7:
                System.out.println("星期日");
            default:
                System.out.println("该数字超出了1-7的范围！");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729163233_vpFaCQ_Screenshot.jpeg)

如果不加break; 从和n匹配的一直执行到最后去。

```java
package cn.mtianyan.flow;

import java.util.Scanner;

public class WeekDemo1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入1-7之间的数字: ");
        int n = scanner.nextInt();

        switch (n){
            case 1:
                System.out.println("星期一");break;
            case 2:
                System.out.println("星期二");break;
            case 3:
                System.out.println("星期三");break;
            case 4:
                System.out.println("星期四");break;
            case 5:
                System.out.println("星期五");break;
            case 6:
                System.out.println("星期六");break;
            case 7:
                System.out.println("星期日");break;
            default:
                System.out.println("该数字超出了1-7的范围！");
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180729162924_PGNUkV_Screenshot.jpeg)

改写程序为字符串的输入

```java
package cn.mtianyan.flow;

import java.util.Scanner;

public class WeekDemo2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入表示星期的英文单词: ");
        String week = scanner.next();
        week = week.toUpperCase(); // 把字符串中字符全部改为大写
        switch (week){
            case "MONDAY":
                System.out.println("星期一");break;
            case "TUESDAY":
                System.out.println("星期二");break;
            case "WEDNESDAY":
                System.out.println("星期三");break;
            case "THURSDAY":
                System.out.println("星期四");break;
            case "FRIDAY":
                System.out.println("星期五");break;
            case "SATURDAY":
                System.out.println("星期六");break;
            case "SUNDAY":
                System.out.println("星期日");break;
            default:
                System.out.println("单词输入错误！");
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180729163947_fdWcl2_Screenshot.jpeg)

将字符全部转换为大写。

在下一集中,我们将来学习流程控制中的循环结构,包括while、do-while和for三种循环结构,以及循环的嵌套等。同时,我们还将首次接触程序调试!





