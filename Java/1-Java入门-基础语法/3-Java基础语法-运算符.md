运算符就是我们接触到的如：加减乘除之类的符号

表达式 & 运算符: 表达式由运算符和操作数组成

如：

![](http://myphoto.mtianyan.cn/20180728205747_By6uSa_Screenshot.jpeg)

>上面三个都是表达式，说明运算符是可选的。第三个表达式中的加号就是运算符。

![](http://myphoto.mtianyan.cn/20180728205903_w00qlE_Screenshot.jpeg)

也可以有多个运算符和操作数。`sum =num1+num2;` 加法运算，赋值运算，sum也是操作数。

算术运算符 & 赋值运算符 & 关系运算符 & 逻辑运算符 & 条件运算符 & 位运算符

### 赋值运算符

```java
int n=5;

int n;
n=5;
```

格式: 变量 = 表达式;

例子:

```java
int n=3; //将3赋值给变量n 
```

注意:赋值运算符是从右往左运算!

```java
double d=123.4;
double d1=d; //变量之间互相赋值
```

错误的写法: 

```java
double d;
123.4=d;
```

注意:赋值运算符的左边不能是常量!

复合赋值运算符

|运算符|表达式|计算|结果(假设x=15)|
|------|------|----|--------------|
|+=|x+=5|x=x+5|20|
|-=|x-=5|x=x-5|10|
|`*=`|`x*=5`|`x=x*5`|75|
|/=| x/=5 |x=x/5|3|
|%=| x%=5|x=x%5|0|

### 自增自减运算符

++ 自增1 int n=3; n++;-- 自减1 int n=4; ++n

|表达式|执行方式|结果(num1=1)|
|------|--------|------------|
| num2= ++num1;|num1= num1+1; num2= num1;|num1=2; num2=2;|
|num2= num1++;|num2= num1; num1= num1+1;|num1=2;num2=1;|
|num2= --num1;|num1= num1-1;num2= num1;| num1=O;num2=0;|
|num2= num1--;|num2= num1;num1 = num1-1;|num1=O;num2=1;|

先执行赋值还是先执行减减，加加这是个问题。

```java
package cn.mtianyan;

public class MathDemo1 {

    public static void main(String[] args) {

        // x++
        int x =4;
        int y=(x++)+5;

        System.out.println("x=" +x);
        System.out.println("y=" +y);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728231717_GXpBi9_Screenshot.jpeg)

```java
        // ++x
        x = 4;
        y = (++x)+5;
        System.out.println("x=" +x);
        System.out.println("y=" +y);  
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728232159_CUVPbI_Screenshot.jpeg)

```java
        // x--
        x = 4;
        y =(x--)+5;
        System.out.println("x=" +x+",y="+y);

        // --x
        x = 4;
        y = (--x)+5;
        System.out.println("x=" +x+",y="+y);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180728232429_bXpsTm_Screenshot.jpeg)

单目运算符 & 双目运算符: 对于几个操作数进行操作

下面代码的输出结果为? (选择一项)

```java
int m=5,n=6;
int x=(m++)+n;
int y=(--m)+n;
System.out.print( "x="+x+",");
System.out.println("y="+y);
```

x=11,y=10 错误！！！ 没有考虑到在y这一行m已经变成了6了; 因此x=11;y=11;是对的。

### 算术运算符

算术运算符主要用于进行基本的算术运算,如加法、减法、乘法和除法等。

|算术运算符|名称|举例|
|----------|----|----|
|+|加法|5+10=15|
|-|减法|10-5=5|
|`*`|乘法|`3*6=18`|
|/|除法|36/4=9|
|%|求余数|13%3=1|
|++|自增1|int n=3;n++;|
|--|自减1|int n=4;--n;|

新建一个包 cn.mtianyan.operator

```java
package cn.mtianyan.operator;

public class MathDemo {
    public static void main(String[] args) {
        int num1 =10,num2=5;
        int result; //存放结果

        // 加法
        result = num1 + num2;
        System.out.println(num1+"+"+num2+"="+result);

        // 字符串连接
        System.out.println(num1 +num2);
        System.out.println(""+num1 +num2);

        // 减法
        result = num1-num2;
        System.out.println(num1+"-"+num2+"="+result);

        // 乘法
        result = num1*num2;
        System.out.println(num1+"*"+num2+"="+result);

        // 除法
        result = num1/num2;
        System.out.println(num1+"/"+num2+"="+result);
        System.out.println("13/5="+13/5); // 整型数除法会舍弃
        System.out.println("13.0/5="+13.0/5);

        // 求余数
        result = 13%num2;
        System.out.println("13%"+num2+"="+result);
        System.out.println("13.5%5="+(13.5%5));
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729004210_wyx0Dk_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180729004120_2nAb3r_Screenshot.jpeg)

### 编程练习

根据任务要求完成本题。效果图:

![](http://myphoto.mtianyan.cn/20180729004435_oXX83s_Screenshot.jpeg)

任务:
  1. 定义整型变量m并初始化为10
  2. 定义整型变量n并初始化为5
  3. 将变量m的值加3 , n的值加5
  4. 求m和n的平均值,并将结果存于变量p中
  5. 将m的平方乘以n的平方, 并将结果存于变
  量q中
  6. 将p和q的值打印输出

```java
package cn.mtianyan.operator;

public class MathExercise {
    public static void main(String[] args) {
        int m =10;
        int n =5;
        m +=3;
        n +=5;
        float p = (m+n)/2;
        float q = (m*m)*(n*n);
        System.out.println("m和n的平均值为:"+p);
        System.out.println("m的平方乘以n的平方为:"+q);
    }
}
```

运行结果:
![](http://myphoto.mtianyan.cn/20180729005027_zO29hP_Screenshot.jpeg)

### 关系运算符

判断购物价格够不够满减(应用)

![](http://myphoto.mtianyan.cn/20180729005146_pQOOrR_Screenshot.jpeg)

比较运算符用于判断两个数据的大小,如大于;比较的结果是一个布尔值

|运算符|名称|表达式|结果|
|----|------|----|-----|
|>|大于|5>3|true|
|<|小于|5<3|false|
|>=|大于等于|5>=3|true|
|<=|小于等于|5<=3|false|
|==|等于|5==3|false|
|!=|不等于|5!= 3|true|

=是赋值，==是比较。注意:运算符必须在英文输入法状态下输入。

例:

  - 'A' > 'B’ 结果为false,比较的是两个字符的ASCII值.顺着排下来的，A肯定不如B大。
  - 5 != 6 结果为true ,比较两个数值是否相等
  - true == false 结果为false ,两个布尔值不相等
  - float f= 5.0f; long l=5;f==l;结果为true ,**浮点数与整数进行比较,只要值相等就返回true**

```java
package cn.mtianyan.operator;

public class RelateDemo {
    public static void main(String[] args) {
        int a=3,b=5;
        System.out.println("a<b="+(a<b));
        System.out.println("a>b="+ (a>b));
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729010627_34u1Zz_Screenshot.jpeg)

### if条件结构

数据比较: 关系运算符主要用于条件和循环语句中的判断条件;本次课介绍简单条件结构及如何编码

条件结构就是根据不同的条件去执行不同的操作。

现实中的成绩: 分数>60分一及格; 分数<60分一不及格;商场打折，满多少减多少。

简单if语句的格式:

```java
if(条件){
  <语句块>
}
```

if后面只有一条语句可以省略括号，后面有多条语句不可以省略括号。

例:商场打折,如果两件商品的总价大于100则减20,并把原价和折后价格分别输出。

```java
package cn.mtianyan.operator;

public class ConditionDemo1 {
    public static void main(String[] args) {
        double price1,price2;
        price1= 80;
        price2= 55;
        // 计算两件商品的总价格
        double sum= price1 + price2;
        System.out.println("原价为:"+sum);
        if (sum >100) {
            sum -=20; // sum=sum-20;
        }
        System.out.println("折后价格为:"+sum);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729011618_Kmliv7_Screenshot.jpeg)

### if-else条件结构

不满足条件也要进行操作

if-else语句的形式：

```java
if(条件为true){
<语句块>
}
else{
<语句块>
}
```

例:判断一个整数是奇数还是偶数,并将结果打印输出。

```java
package cn.mtianyan.operator;

import java.util.Scanner;

public class ConditionDemo2 {
    public static void main(String[] args) {
        // 从键盘接收数据
        System.out.println("请输入一个整数: ");
        Scanner s = new Scanner(System.in);
        int n = s.nextInt();

        // 定义一个变量存放数据
        // int n =10;
        if(n%2==0){
            System.out.println(n+"是偶数");
        }else{
            System.out.println(n+"是奇数!");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729012436_nlcPwJ_Screenshot.jpeg)

从键盘接收输入的语句如下，先记住就行了。

```java
        Scanner s = new Scanner(System.in);
        int n = s.nextInt();
```

#### 编程练习

使用if-else语句完成:根据x的值,输出y的值。
效果图:

![](http://myphoto.mtianyan.cn/20180729012711_GsPGKo_Screenshot.jpeg)

任务
  1. 定义整型变量x和y ,并进行赋值
  2. 如果x>0,则y=2*x+1 ,否则y=x+5
  3. 输出x和y的值

```java
package cn.mtianyan.operator;

public class IfDemo {
    public static void main(String[] args) {
        int x=-2,y;
        if(x>0){
            y=2*x+1;
        }else{
            y=x+5;
        }
        System.out.println("x="+x);
        System.out.println("y="+y);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729043758_ysHZp6_Screenshot.jpeg)

### 逻辑运算符

逻辑运算符用来连接一个或多个条件,判断这些条件是否成立;运算符的结果是布尔类型;什么时候使用逻辑运算符

![](http://myphoto.mtianyan.cn/20180729044020_cSzB9t_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180729044032_MvtCml_Screenshot.jpeg)

判断是学神还是学渣等时。

|名称|运算符|表达式|
|----|------|------|
|与|&&或&|operator1&&operator2|
|或|`||`或`|`|operator1`||`operator2|
|非|!|!operator|

注意:逻辑运算符的操作数,都是布尔类型的。

逻辑“与”运算符

问题:升学考试,英语、数学、C语言三门总成绩大于等于230, 并且英语成绩大于等于60 ,才能升学。

![](http://myphoto.mtianyan.cn/20180729044545_zjwZ52_Screenshot.jpeg)

三门总成绩大于等于230 ,表示为: sum >= 230
英语成绩大于等于60 ,表示为 en >= 60;

![](http://myphoto.mtianyan.cn/20180729044833_EyPaBz_Screenshot.jpeg)

&运算符 int n=3; boolean b=(3>7)&((n++)<2) 问: b= ?, n= ?

b=false,n=4。

&&透算符 int n=3; boolean b=(3>7)&&(n++)<2) 问:b= ? , n=?

b = false,n=3。

&&运算符又叫短路运算符,如果第一个表达式的值就能决定表达式最后的结果,运算符右边的表达式就不再计算了

### 逻辑或运算符

- 付款问题: 可以使用现金或银行卡

|现金|现金(布尔)|银行卡|银行卡(布尔)|结果|
|----|----------|------|------------|----|
|可以支付|true|可以支付|true|可以支付|
|可以支付|true|无法支付|false|可以支付|
|无法支付|false|可以支付|true|可以支付|
|无法支付|false|无法支付|false|无法支付|

`|`运算符

int n=3;boolean b=(3<7)|((n++)<2)问: b= ?,n=?

b=true,n=4;

`||`送算符

int n=3;boolean b=(3<1)||(n++)<2)向: b= ? ,n=?
b=true,n=3;

`||`运算符又叫短路运算符,如果第一个表达式的值就能决定表达式最后的结果,运算符右边的表达式就不再计算了。

### 逻辑非运算符

!运算符对原条件进行取反

例: !(3<5) ,结果为false

例:输入一个数,判断是否能被3整除,并输出相应的提示信息。

```java
package cn.mtianyan.operator;

import java.util.Scanner;

public class LogicDemo {
    public static void main(String[] args) {
        // 输入一个整数
        System.out.println("请输入一个整数: ");
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        if(!(n%3 == 0)){
            System.out.println(n+"不能被3整除");
        }else{
            System.out.println(n+"能被3整除");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729112002_RrARB5_Screenshot.jpeg)

### 条件运算符

Java中的条件运算符是三目运算符

前面学到的++是单目运算符 + - * /是双目运算符

语法: 布尔表达式?表达式1:表达式2

当布尔表达式的值为true ,则返回表达式1的值,否则返回表达式2的值。

例子: 求两个数的最大值并输出。

```java
package cn.mtianyan.operator;

public class ConditionThreeEye {
    public static void main(String[] args) {
        int a = 4;
        int b = 7;
        int max;
        if(a>b){
            max = a;
        }else{
            max = b;
        }
        System.out.println("max:"+max);
        max = a>b?a:b;
        System.out.println("max:"+max);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729112524_tpuhfa_Screenshot.jpeg)

后面的两个表达式可以是具体功能的表达式

```java
        boolean result = a>b?(3<6):(true == false);
        System.out.println(result);
```

![](http://myphoto.mtianyan.cn/20180729112711_pXC7GR_Screenshot.jpeg)

### 运算符的优先级

算术运算符 关系运算符 逻辑运算符

当这些运算符出现在一起，先算哪个呀？

```java
n= x * y +(x%2)-(x/y) I
```

|运算符|描述|
|------|----|
|()|圆括号|
|!, ++, --|逻辑非,自增,自减|
|*, /, %|乘法,除法,取余|
|+, -|加法,减法
|<, <=, >, >=|小于,小于等于,大于,大于等于|
|== !=|等于,不等于|
|&&|逻辑与|
| `||` |逻辑或|
|=, +=, *=, /=, %=, -=|赋值运算符,复合赋值运算符|

表格从上到下优先级从高到低，也就是小括号优先级最高。赋值运算符优先级最低。多加括号，解决优先级不明确问题。

已知 

```java
int x=4,y=6;
n= x*y +(x%2)-(x/y) 
// n=24
```

### 综合案例1 闰年问题

用if-else语句判断输入的年份是否为闰年。

闰年的判断规则:能被4整除但不能被100整除的年份,或者能被400整除的年份。

```java
package cn.mtianyan.operator;

import java.util.Scanner;

public class LeapYearDemo {
    public static void main(String[] args) {
        System.out.println("请输入年份:");
        Scanner scanner = new Scanner(System.in);
        int year = scanner.nextInt();
        if(year%400==0 | (year%4==0 & year%100!=0)){
            System.out.println(year+"年是闰年");
        }else {
            System.out.println(year+"年不是闰年");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729114442_Tc0tpd_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180729114523_WgdREV_Screenshot.jpeg)

### 课程总结

表达式 运算符(主要部分)

什么是表达式? 5;a;m+3;sum=a+b;n=x*y+(x%2)-(x/y);

表达式由一系列的运算符和操作数组成。

运算符:

![](http://myphoto.mtianyan.cn/20180729114833_9FwFQA_Screenshot.jpeg)

算术运算符 赋值运算符 关系运算符 逻辑运算符 条件运算符

在除法运算中,如果除数和被除数都是整数,则做整除运算;加加减减，前后数值不同。

a+=b 相当于 a=a+b; 与或非中的短路运算符 

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

如果if或else语句后面只有一条语句,可以不加大括号,否则必须加大括号。if后面小括号中的表达式结果必须是布尔值。

![](http://myphoto.mtianyan.cn/20180729115254_mdrrzD_Screenshot.jpeg)

在下一集中我们会学习流程控制中的选择结构，包括多重和嵌套的if-else结构以及switch结构!













