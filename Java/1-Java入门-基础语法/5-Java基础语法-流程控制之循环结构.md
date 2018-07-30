## 循环结构

顺序结构,从_上往下依次执行;选择结构,根据条件执行对应的内容

为什么要使用循环结构?

问题一:反复输入数字,判断输出对应是星期几。问题二:求1到100的累加和

主要内容:

while循环;do-while循环;for循环;循环嵌套;break语句;continue语句

### while 循环

语法格式:

```java
while(循环条件){
  语句;
}
```

如果循环体只有一条语句，大括号可以省略。为避免死循环,小括号后面不要加分号

执行流程: 将小于5的整数打印输出。

```java
int n=1;
while(n<5){
  //輸出n的値
  n++;
}
```

1. n的值必须先进行初始化
2. 循环变量n的值必须被改变（死循环）

执行流程分析:

![](http://myphoto.mtianyan.cn/20180729170026_bGtvLk_Screenshot.jpeg)

### 案例: 求1到5的累加和

```java
package cn.mtianyan.flow2;

public class PlusDemo {
    public static void main(String[] args) {
        // 求1到5的累加和
        // 1+2+3+4+5
        int n = 1;
        int sum = 0; //sum存放和变量
        while (n <=5 ){
            sum = sum +n;
            n++; // 这句不能少
        }
        System.out.println("sum="+sum);
    }
}
```

![](http://myphoto.mtianyan.cn/20180729172405_sBSScx_Screenshot.jpeg)

执行过程:

![](http://myphoto.mtianyan.cn/20180729172532_lxACjM_Screenshot.jpeg)

求1+3+5+7+...+15

```java
sum +=n;
n +=2; //替换n++ 可以实现跳值计算
```

### 案例: 循环输出26个英文字母,分两行输出

```java
package cn.mtianyan.flow2;

public class CharDemo {
    public static void main(String[] args) {
        // 循环输出26个英文小写字母，分两行输出
        char ch = 'a';
        int count=1; // 13个字母时换行
        while (ch <= 'z'){
            System.out.print(ch+"");
            if(count%13 == 0){
                System.out.println();
            }
            count++;
            ch++;
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729195222_iYBvRc_Screenshot.jpeg)

#### 编程练习

使用while循环求1到5的平方和。效果图:

![](http://myphoto.mtianyan.cn/20180729195440_VLFJXI_Screenshot.jpeg)

任务
  1. 定义整型变量n作为循环变量，并初始化
  2. 定义整型变量sum存放和,并初始化
  3. 使用while循环求1到5的平方和
  4. 输出平方和

```java
package cn.mtianyan.flow2;

public class LoopDemo {
    public static void main(String[] args) {
        int n = 1;
        int sum = 0;
        while (n<=5){
            sum +=(n*n);
            n++;
        }
        System.out.println("1到5的平方和为:"+sum);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729195819_VVXMmW_Screenshot.jpeg)

### do-while循环

语法格式

```java
do{
语句;
} while(循环条件);
```

注意事项: do-while循环至少执行一次；循环条件后的分号不能丢

```java
int n= 1;
do
{
  //輸出n的値
  n++;
} while(n< 5);
```

局部变量使用前必须被初始化

![](http://myphoto.mtianyan.cn/20180729201508_0llst9_Screenshot.jpeg)

求1到5的累加和

```java
package cn.mtianyan.flow2;

public class DoWhileDemo {
    public static void main(String[] args) {
        // 求1到5的累加和
        int n=1;
        int sum=0;
        do {
            sum +=(n*n);
            n++;
        }while (n<=5);
        System.out.println("1到5的平方和为:"+sum);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729201842_VdYjm1_Screenshot.jpeg)

### 案例:猜字游戏

猜字游戏。要求猜一个介于1到10之间的数字。然后将猜测的值与实际值进行比较,并给出提示,以便能更接近实际值,直到猜中为止。

程序分析:
  1. 给定要猜测的数字
  2. 使用循环结构
  3. 循环进行的条件:猜测的数据和实际值不相等
  4. 循环体的内容:输入实际值,及进行判断
  5. 输出猜到的值

```java
package cn.mtianyan.flow2;

import java.util.Scanner;

public class GuessDemo {
    public static void main(String[] args) {
        // 设置要猜的数
        int number = 6;
        int guess;
        System.out.println("猜一个介于1到10之间的数");
        do {
            System.out.println("请输入您猜测的数:");
            Scanner scanner = new Scanner(System.in);
            guess = scanner.nextInt();
            if(guess >number){
                System.out.println("您猜大了");
            }else{
                System.out.println("您猜小了");
            }
        }while (number != guess);
        System.out.println("您猜中了!答案为: "+number);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729202945_bqQORx_Screenshot.jpeg)

将要猜的数设为随机数:

Math.random()得到[0,1)之间的随机数

```java

         // Math.random()*10+1 表示[0,10)+1:[1,11)之间的随机数。强制类型转换int之后就是1-10了
        int number = (int) (Math.random()*10+1);
```

### for循环应用及局部变量作用范围

```java
int n=1;
while(n<5)
  //輸出n的値
  n++;
```

for循环语法格式:

```java
for(表达式1;表达式2;表达式3)
{
  语句;
}
```

```java
for(int n=1;n<5;n++)
{
  //输出语句;
}
```

分号不可省略，可以省略表达式1,2,3。

使用for循环,求1到5的累加和。

```java
package cn.mtianyan.flow2;

public class ForDemo {
    public static void main(String[] args) {
        int sum=0;
        for (int n=1;n<=5;n++){
            sum +=n;
        }
        // System.out.println(n); // 局部变量的作用范围
        System.out.println("sum="+sum);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729221822_PZ3elE_Screenshot.jpeg)

int n= 1;在循环体中只执行一次

![](http://myphoto.mtianyan.cn/20180729221807_sVhOKl_Screenshot.jpeg)

局部变量，主方法中定义的都是局部变量。局部变量只在定义它的大括号内有效!

### for循环的注意事项

三个表达式都是可以省略

```java
for(表达式1;表达式2;表达式3)
{
 语句;  
}
```

将10以下的整数打印输出:

```java
package cn.mtianyan.flow2;

public class ForDemo1 {
    public static void main(String[] args) {
        for (int i=0;i<=10;i++){
            System.out.print(i+" ");
            // 循环结束时i值为11
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729223734_j1m56c_Screenshot.jpeg)

省略表达式:

```java
package cn.mtianyan.flow2;

public class ForDemo1 {
    public static void main(String[] args) {
        int i=0;
        // for(;;){
        while(true){
            System.out.print(i+" ");
            // 循环结束时i值为11
            if(i>=10){
                break;
            }
            i++;
        }
    }
}
```

循环输入数字1-10并输出,如果输入0则跳出循环:

```java
package cn.mtianyan.flow2;

import java.util.Scanner;

public class InputZeroBreak {
    public static void main(String[] args) {
        System.out.println("请输入你需要打印的数字，输入0时退出");
        Scanner scanner = new Scanner(System.in);
        int n;
        while(true){
            n = scanner.nextInt();
            if(n==0){
                System.out.println("接收到0输入，已退出");
                break;
            }
            System.out.println("n="+n);
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729224739_6VIzqO_Screenshot.jpeg)

```java
package cn.mtianyan.flow2;

public class ForExercise {
    public static void main(String[] args) {
        int i;
        int j;
        for (i=0,j=1;j<5;j+=3){
            i = i+j;
        }
        System.out.println("i="+i);
        System.out.println("j="+j);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729230928_6oBN9d_Screenshot.jpeg)

请注意记住执行顺序如下:

![](http://myphoto.mtianyan.cn/20180729230942_OmGt92_20180729221807_sVhOKl_Screenshot.jpeg)

#### 编程练习

编写一个程序,求出200到300之间的数,且满足条件:它们三个数字之积为42 ,三个数字之和为12。

效果图:

![](http://myphoto.mtianyan.cn/20180729231136_IdQENC_Screenshot.jpeg)

任务
  1. 循环遍历 200到300之间的整数
  2. 分别取出个位、十位和百位上的数
  3. 求三个数字的和与积
  4. 判断三个数字的积是否为42 ,三个数字的和是否为12 ,如果满足条件则输出该数

```java
package cn.mtianyan.flow2;

public class LoopDemoExercise {
    public static void main(String[] args) {
        for (int i=200;i<=300;i++){
            // 个位 十位 百位
            int hundreds = i / 100;
            int ten = (i-hundreds*100)/ 10;
            int single = i-hundreds*100-ten*10;

            if(hundreds*ten*single == 42 && (hundreds+ten+single)==12){
                System.out.println(i);
            }
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729232119_6whk9s_Screenshot.jpeg)

### 嵌套的while循环应用

```java
while(循环条件)
{
  while(循环条件){
  }
}
```

一个循环内部还有另外一个循环，二重循环；允许多层循环嵌套; 外层循环和内层循环。循环嵌套可以混搭。

```java
do{
  ......
  while(循环条件){
    ......
  }
}while(循环条件);
```

```java
for(表达式1;表达式2;表达式3)
{
  ......
  for(表达式1;表达式2;表达式3){
    ......
  }
  ......
}
```

例: 使用嵌套while循环输出4行4列的星号

```java
package cn.mtianyan.flow2;

public class StarDemo {
    public static void main(String[] args) {
        int i=1; // 外重循环的循环变量
        int j=1; // 内重循环的循环变量
        System.out.println("输出4行4列的星号");
        while (i <= 4) {
            while (j <= 4) {
                System.out.print("*");
                j++;
            }
            System.out.println();
            i++;
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180729234442_NbTFve_Screenshot.jpeg)

程序运行流程分析:

![](http://myphoto.mtianyan.cn/20180729234257_K2NEj4_Screenshot.jpeg)

>可以看到内层的j执行完自己的第一轮之后，下次的i符合条件，j执行的轮中，i已经无法满足条件了。因此要在每一个大轮中重置内层的循环变量。

```java
package cn.mtianyan.flow2;

public class StarDemo {
    public static void main(String[] args) {
        int i=1; // 外重循环的循环变量
        int j; // 内重循环的循环变量
        System.out.println("输出4行10列的星号");
        // 外层控制有几行，内层控制每行有几列
        while (i <= 4) {
            j=1;
            while (j <= 10) {
                System.out.print("*");
                j++;
            }
            System.out.println();
            i++;
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180729235122_jU3KeS_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180729235220_kOMRaM_Screenshot.jpeg)
![](http://myphoto.mtianyan.cn/20180729235251_49mFc7_Screenshot.jpeg)

程序进阶: 输出三角形怎么处理?

程序每行输出多少个是由内层控制的，因此对于内层进行改造。

改为与外层联动`n<=4 改为n<=m` 第一次时输出一个星，输出两个星;

```java
while (j <= i) 
```

运行结果:

![](http://myphoto.mtianyan.cn/20180730000145_MpA1lP_Screenshot.jpeg)

```java
package cn.mtianyan.flow2;

public class StarDemoFor {
    public static void main(String[] args) {
        int i;
        int j;
        for(i=1;i<=4;i++){
            for(j=3;i<=j;j--){
                System.out.print("-");
            }
            for(j=1;j<=i;j++){
                System.out.print("*");
            }
            for(j=1;j<i;j++){
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180730005312_qdxCPy_Screenshot.jpeg)

### 阶乘的累加和

求1!+2!+3!+...+ 10!

嵌套循环，外层循环进行和运算，内层进行阶乘运算。

```java
package cn.mtianyan.flow2;

public class FactorialDemo {
    public static void main(String[] args) {
        int s,sum=0;
        for (int i=1;i<=4;i++){
            s = 1; // s值每个循环内重新置1
            for (int j=1;j<=i;j++){
                 s = s*j; // s存放阶乘计算的结果
            }
            sum +=s;
        }
        System.out.println("1!+2!+3!+4!="+sum);
    }
}
```

![](http://myphoto.mtianyan.cn/20180730010304_n4HKBI_Screenshot.jpeg)

```java
for (int i=1;i<=10;i++)
```

![](http://myphoto.mtianyan.cn/20180730010649_ONg4RR_Screenshot.jpeg)

```java
for (int i=1;i<=50;i++)
```

![](http://myphoto.mtianyan.cn/20180730010720_xmKCgH_Screenshot.jpeg)

可以看到此时int已经装不下了，发生了溢出，因此我们该使用长整型。

```java
 long s,sum=0;
```

而长整型还无法容纳的数据。

```java
package cn.mtianyan.flow2;

import java.math.BigInteger;

public class FactorialDemo {
    public static void main(String[] args) {
        BigInteger sum = new BigInteger("1");
        BigInteger s;
        for (int i=1;i<=50;i++){
            s = new BigInteger("1"); // s值每个循环内重新置1
            for (int j=1;j<=i;j++){
                BigInteger num = new BigInteger(String.valueOf(j));
                s = s.multiply(num);
            }
            sum = sum.add(s);
        }
        System.out.println("1!+2!+3!+50!="+sum);
    }
}
```

![](http://myphoto.mtianyan.cn/20180730012203_kkPuGo_Screenshot.jpeg)

#### 编程练习

用星号输出一个梯形,如下图所示: ( 使用嵌套for循环完成)

![](http://myphoto.mtianyan.cn/20180730012310_EJ3Z6X_Screenshot.jpeg)

任务:
  1. 外重循环控制输出行数
  2. 第一个内重循环控制输出的空格数,依次递减
  
  注意:由于星号和空格在屏幕上所占的空间不同,所以可以适当调整空格的输出,比如毎次
  循环都输出两个空格.这样输出来的图形会更加接近梯形
  
  3. 第二个内重循环控制毎行输出的星号数
  4. 输出完一行的星号和空格后换行

```java
package cn.mtianyan.flow2;

public class StarDemoExercise {
    public static void main(String[] args) {
        // 输出五行
        for(int i=1;i<=5;i++){

            for (int j=4;i<=j;j--){
                System.out.print("-");
            }
            for (int j=1;j<=i+1;j++){
                System.out.print("*");
            }
            for (int j=1;j<=i;j++){
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180730014900_DxfCId_Screenshot.jpeg)

>这里分为三部分画出。

```java
package cn.mtianyan.flow2;

public class StarExercise2 {
    public static void main(String[] args) {
        for(int i=1;i<=5;i++){
            for (int j=4;i<=j;j--){
                System.out.print("-");
            }
            for (int j=1;j<=(2*i+1);j++){
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180730015738_aH0FD8_Screenshot.jpeg)

分两部分画出，则需要看出行号和该行星星之间的关系。

### break语句

break语句可以结束当前循环的执行

执行完break语句后,循环体中位于break语句后面的语句就不会被执行

在多重循环中, break语句只向外跳一层

```java
public static void main(String[]args){
  Scanner sc=new Scanner(System.in);
  int n;
  while(true){
      n= sc.nextInt();
      if(n == 0)break;
      System.out.println(n);
  }
}
```

多重循环:

```java
public static void main(String[] args){
    int k = 0;
    for(int i=1;i<5;i++){
        for(int j=1;j<5;j++){
            k=i+j;
            if(j==3)break;
        }
    }
    System.out.println("k="+k);
}
```

![](http://myphoto.mtianyan.cn/20180730111837_wif0M8_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180730020744_7ZpciR_Screenshot.jpeg)

注意写表查看值得变化情况，脑补脑力不足很费劲。

break语句的使用;break语句的作用:跳出当前循环结构;break语句一旦被执行, 循环体中break语句后面的代码将不再被执行

注意: break语句是跳出当前循环.**只跳出了内层循环，不会影响到外层循环的继续执行**

### continue语句

continue语句只能用在循环里

continue语句可以结束当前循环的执行,但是要继续下一次循环的执行

求1+3+5+7+9

```java
public static void main(String[] args){
    int sum=0;
    for(int i=1;i<=9;i++){
        if( i%2 == 0)continue;
        sum =sum+i;
    }
    System.out.println("sum="+sum);
}
```

循环变量每次加2就可以实现。使用continue语句的情况如下

```java
public static void main(String[] args){
    int sum=0;
    for(int i=1;i<=9;i++){
        if(i%2 == 0)continue; // 偶数不加进sum
        sum=sum+i;
    }
    System.out.println("sum="+sum);
}
```

![](http://myphoto.mtianyan.cn/20180730110437_j5KtGv_Screenshot.jpeg)

双重循环问题:

```java
    public static void main(String[] args){
        int k=0;
        for(int i=1;i<=5;i++){
            for(int j=1; j<5; j++){
                if(j%2 == 0)continue;
                k=k+j;
            }
        }
        System.out.println("k="+k);
    }
```

自己分析输出结果:

![](http://myphoto.mtianyan.cn/20180730111928_FUBgpI_Screenshot.jpeg)

**只能在循环体内和switch语句体内使用break；**

### 程序Debug

![](http://myphoto.mtianyan.cn/20180730112207_RQmEWQ_Screenshot.jpeg)

调试的作用:
让程序员能看清程序每一步的效果,在需要查看结果的时候,使用debug查看实际结果是否与预期结果一致。

阶乘中s=1;的重置操作很容易遗漏。调试例子(1到5的累加和)

```java
package cn.mtianyan.flow2;

public class ForDemo {
    public static void main(String[] args) {
        int sum=0;
        for (int n=1;n<=5;n++){
            sum +=n;
        }
        System.out.println("sum="+sum);
    }
}
```

断点，让程序停到这

![](http://myphoto.mtianyan.cn/20180730112623_pNusXs_Screenshot.jpeg)

设置断点，让程序停在这。此时开始运行调试。

![](http://myphoto.mtianyan.cn/20180730112709_8juYcH_Screenshot.jpeg)

右键点debug，而不是run。

![](http://myphoto.mtianyan.cn/20180730112828_y0BikC_Screenshot.jpeg)

然后我们开始单步调试。

![](http://myphoto.mtianyan.cn/20180730112949_SNJUIX_Screenshot.jpeg)

step over 是单步调试， Step into 是进入函数内部，使用step over可以看到sum 和 n 一直在变化。

### Debug多断点调试

![](http://myphoto.mtianyan.cn/20180730113940_lVEiMr_Screenshot.jpeg)

多个断点时从当前断点之间执行完，跳到下个断点停住。注意: 对于for循环来说，一个断点可以当做循环次数个断点，直到循环结束，才会到下一个断点。

快捷键，各个平台不一样，自己根据英文名来找自己的快捷键。

### 流程控制总结

流程控制语句:顺序、选择、循环

选择语句

  - if语句
  - if-else语句
  - 多重if-else语句
  - 嵌套if-else语句
  - switch语句(常量表达式，整型字符型)

循环结构

  - while循环
  - do-while循环
  - for循环
  - 嵌套循环（任意的组）
  - break语句和continue语句(break使用在switch和循环结构当中，continue语句只能使用在循环结构当中)
  
  break是结束当前循环的执行，continue是结束当前循环的执行，会继续下一次循环执行。多重循环这两个都只跳出一层。

如何进行调试? 单步 继续执行到下个断点

如何存储相同数据类型的多个数据呢?数组将为我们解决这个问题。
在下集中,将为大家带来一维数组的使用,增强型for循环,以及冒泡排序!





















 

