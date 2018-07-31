什么是方法？

首先会想到的应该是我们最常使用到的主方法

```java
class HelloJava{
  public static void main(String[] args){
    System.out.println("Hello,Java!");
  }
}
```

main方法是程序的入口

```java
Scanner sc = new Scanner(System.in);
sc.nextInt();
sc.next();
```

类，Scanner是一个类，sc是它实例化出的对象。nextInt()是从键盘获取一个整型值的方法，next()是从键盘获取一个字符串类型值的方法。这两个都是使用对象名去调用，在方法部分,只使用对象名调用方法(但其实还有可以通过类调用的方法，后面学)

```java
System.out.println();
```

所谓方法，就是用来解决一类问题的代码的有序组合，是一个功能模块。

现在我们看到的这些方法基本都是jdk为我们提供的内置方法。但是为了满足我们更多的需求，我们需要自定义方法

主要内容: 方法的声明和调用;方法的重载

语法格式:

```java
访问修饰符 返回类型 方法名(参数列表){
  方法体
}
```

```java
  public static void main(String[] args){
    System.out.println("Hello,Java!");
  }
```

public属于访问修饰符的内容,static表明这是一个静态方法; 返回类型(void); 方法名(main);参数列表(字符串数组类型的args);方法体;

访问修饰符是方法允许被访问的权限范围。其他三种访问修饰符: 什么都不写，protected,private。

返回类型: void 表示无返回值;返回值可以是void以及任何数据类型。 方法名命名规则和变量名命名规则一致，如果只有一个单词，单词小写，如果有两个单词及以上，第二个开始大写首字母。比如,myMethod

方法名之后的括号是不可以省略的，但是参数列表是可以省略的。可以是无参。

根据方法是否带参数、是否返回值,可分为四类:
  
  - 无参无返回值方法
  - 无参带返回值方法
  - 带参无返回值方法
  - 带参带返回值方法

### 无参无返回值方法

例: 一行打印输出一串星号

实现的效果图:

![](http://myphoto.mtianyan.cn/20180731174123_LoqgEn_Screenshot.jpeg)

重复行为包装到方法。

冒泡排序问题: 将排序的实现代码单独的写在一个sort方法里面

```java
public void sort(int[] a){
  int temp;
  for(int i=0;i<a.length;i++){
    for(int j=0;j<a.length-1-i;j++){
      if(a[j]>a[j+1]){
          temp=a[j];
          a[j]=a[j+1];
          a[j+1]=temp;
      }
    }
  }
}
```

然后我们在使用的时候，只需要去调用这个方法就可以。

```java
SortDemo ad= new SortDemo();
int[] a={34,53,12,32,56,17};
int[] b={85,73,25,56,34,48};
// 对数组a进行排序
ad.sort(a);
// 对数组b进行排序
ad.sort(b);
```

方法的主要作用是减少代码量。下面是不使用方法的实现:

```java
package cn.mtianyan.method;

public class MethodDemo {
    public static void main(String[] args) {
        System.out.println("***********************");
        System.out.println("    欢迎来到java世界");
        System.out.println("***********************");
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731174832_bxqyBg_Screenshot.jpeg)

```java
package cn.mtianyan.method;

public class MethodDemo {
    public static void main(String[] args) {
        // 创建一个MethodDemo类的对象methodDemo
        MethodDemo methodDemo = new MethodDemo();
        // 使用对象名.方法名()去调用方法
        methodDemo.printStar();
        System.out.println("    欢迎来到java世界");
        methodDemo.printStar();
    }
    // 打印输出星号的方法
    public void printStar(){
        System.out.println("***********************");
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731175115_PPCCiT_Screenshot.jpeg)

注意:方法在类的内部定义! printStar和main方法并列; 按照习惯性应该写在主方法前面。

### 无参有返回值方法

求长方形的面积

```java
public int area(){}
```

Scanner类 中的next()方法没有参数,返回值是String类型。

提示: 初学时,会给出方法的定义形式。

```java
package cn.mtianyan.method;

public class Rectangle {
    // 求长方形面积方法
    public int area(){
        int length =10;
        int width = 5;
        int intArea = length * width;
        return intArea; // 返回值类型和方法定义返回类型要一致。
        // 变量名和方法名一致不报错。但是我们还是最好不要混淆。
    }
    public static void main(String[] args) {
        Rectangle rectangle = new Rectangle();
        int result = rectangle.area();
        System.out.println("Area="+result);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731180433_JqRGyC_Screenshot.jpeg)

### 有参无返回值方法

定义一个求两个float类型数据最大值的方法,在方法中将最大值打印输出。

```java
public void max(float a,float b){}
```

```java
package cn.mtianyan.method;

public class MaxDemo {
    public void max(float a,float b){
        float max=0;
        if(a>b){
            max = a;
        }else if(a == b){
            max = a;
            System.out.print("相等:");
        }else{
            max = b;
        }
        System.out.println("两个数"+a+"和"+b+"的最大值为: "+ max);
    }
    public static void main(String[] args) {
        MaxDemo maxDemo = new MaxDemo();
        maxDemo.max(5,3);
        maxDemo.max(5,5);
        maxDemo.max(3,5);

    }
}

```

运行结果:

![](http://myphoto.mtianyan.cn/20180731181330_cRK36j_Screenshot.jpeg)

局部变量的定义范围就是在定义它的大括号内有效，之前只学过选择结构和循环结构，变量在结构内有效。

```java
for(int i=0;i<=10;i++){}
```

i就只在for循环内有效。类似的a和b只在max方法内有效。

```java
        float m =5.6f,n=8.9f;
        maxDemo.max(m,n);
```

![](http://myphoto.mtianyan.cn/20180731181954_oHhnCI_Screenshot.jpeg)

方法传入的既可以是变量，也可以是字面值。只要和参数列表匹配就可以了。可以传递精度更低的，不能传递精度更高的，如double

#### 编程练习

定义一个方法,根据商品总价，计算出对应的折扣并输出。折扣信息如下:

  1. 总价<100 ,不打折
  2. 总价在100到199之间,打9.5折
  3. 总价在200以上,打8.5折

效果图:

![](http://myphoto.mtianyan.cn/20180731182309_sHaOvu_Screenshot.jpeg)

任务:

  1. 定义一个方法,根据商品总价输出折后总价
  2. 在主方法中定义对象
  3. 使用对象调用定义的方法

提示:商品总价为150时,可得到如效果图所示
的结果

```java
package cn.mtianyan.method;

public class DisCountDemo {
    public float money(float price){
        if (price<100){
            return price;
        }else if (price <=199){
            return price*0.95f;
        }else{
            return price*0.85f;
        }
    }
    public static void main(String[] args) {
        DisCountDemo disCountDemo = new DisCountDemo();
        float price = disCountDemo.money(150);
        System.out.println("折后商品总价为: "+price);
    }
}
```

![](http://myphoto.mtianyan.cn/20180731183335_xikZSq_Screenshot.jpeg)

### 带参有返回值方法

定义一个求n! 的方法，然后再求1!+2!+3!+4!+5!

```java
public int fac(int n){}
```

方法定义在类里面，是不能定义在另一个方法里的，也就是方法不能嵌套定义。比如: 主方法里面不能再嵌套一个方法。

```java
package cn.mtianyan.method;

public class FacDemo {
    public int fac(int n){
        int s =1;
        for (int i=1;i<=n;i++){
            s *=i;
        }
        return s;
    }
    public static void main(String[] args) {
        FacDemo facDemo = new FacDemo();
        // int fac = facDemo.fac(3);
        // System.out.println("3！= "+fac);
        // 求1! + 2! +3! +4! +5!
        int sum = 0;
        for (int i=1;i<=5;i++){
            sum +=facDemo.fac(i);
        }
        System.out.println("1!+2!+3!+4!+5! 和为： "+sum);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731185313_80tBDM_Screenshot.jpeg)

### 数组作为方法参数

例:定义方法,打印输出数组元素的值。

```java
public void printArray(int[] arr){}
```

main方法是String类型数组，这里是int类型数组。

```java
package cn.mtianyan.method;

public class ArrayMethod {
    public void printArray(int[] arr){
        for (int n :arr) { System.out.print(n+" "); }
        System.out.println(); // 方法是被调用多次的，所以最后加上换行。
    }
    public static void main(String[] args) {
        ArrayMethod arrayMethod = new ArrayMethod();
        int[] arr = {1,3,5,7,9};
        arrayMethod.printArray(arr);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731190041_oeWHgz_Screenshot.jpeg)

#### 编程练习

编写方法，求数组元素的平均值。

效果图:

![](http://myphoto.mtianyan.cn/20180731190304_p3F4Ko_Screenshot.jpeg)

任务

  1. 定义一个方法,求数组的平均值
  2. 在主方法中定义对象,并初始化一个float类型的数组,调用方法求数组元素的平均值，并将平均值打印输出

提示: 当数组元素的内容为: 78.5, 98.5, 65.5, 32.5和75.5时,可得到效果图所示的结果

```java
package cn.mtianyan.method;

public class ArrayExercise {
    public void arrAvg(float[] arr){
        float sum = 0;
        for (float n:arr) {
            sum += n;
        }
        float avg = sum/arr.length;
        System.out.println("数组的平均值为: "+avg);
    }
    public static void main(String[] args) {
        ArrayExercise arrayExercise = new ArrayExercise();
        float [] arr = {78.5f,98.5f,65.5f,32.5f,75.5f};
        arrayExercise.arrAvg(arr);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731190920_5SPsda_Screenshot.jpeg)

### 数组作为方法参数(下)

例子: 查找数组元素的值: 方法参数为:数组、要查找的元素;返回值: boolean类型

```java
public boolean search(int n,int[] arr){}
```

```java
package cn.mtianyan.method;

import java.util.Scanner;

public class ArraySearch {
    public boolean searchArray(int n,int[] arr){
        for (int i=0;i<arr.length-1;i++){
            if (arr[i] == n){
                System.out.println("数值为"+n+"的数的下标为:"+i);
                return true;
            }
        }
        System.out.println("没找到");
        return false;
    }
    public static void main(String[] args) {
        ArraySearch arraySearch = new ArraySearch();
        int[] arr = {3,10,11,13,17};
        System.out.println("请输入要查找的数据");
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        arraySearch.searchArray(n,arr);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731192149_vq7ZXz_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180731192205_dXYpjJ_Screenshot.jpeg)

### 方法重载

方法名相同,参数列表不同,被称为方法的重载。

为什么要有方法的重载？

之前的求最大值的例子中，我们求的是两个float类型的最大值。传参的时候可以传float类型，也可以传整型的值。传double类型值是不允许的。

我们此时想传double类型的值，不需要重新想方法名，只需要新添加一个

```java
public void max(double a,double b)
```

判断下列哪些方法是重载的方法

```java
public void hello(){}
public int hello(){} // 不构成重载，参数相同
public void hello(String s){}
public void hello(int n){}
public void hello(float f1,float f2){}
public void hello1(){} // 不构成重载，方法名都不同 
```

上面的3 4 5行代码均构成重载。参数不同，既可以是数量不同，也可以是类型不同。

定义三个方法,实现int、double和数组类型和的问题

```java
package cn.mtianyan.method;

public class MathDemo {
    // 求两个int类型数的和
    public int add(int a,int b){
        return a+b;
    }
    public double add(double a,double b){
        return a+b;
    }
    public double add(double[] arr1,double[] arr2){
        double arr1Sum=0,arr2Sum=0;
        for (double m:arr1) {
            arr1Sum +=m;
        }
        for (double n:arr2) {
            arr2Sum +=n;
        }
        return arr1Sum+arr2Sum;
    }
    public static void main(String[] args) {
        MathDemo mathDemo = new MathDemo();
        System.out.println("1加2的和为: "+mathDemo.add(1, 2));
        System.out.println("1.23+2.34的和为: "+mathDemo.add(1.23, 2.34));
        double[] arr1 = {1.2,1.3,1.4,1.5};
        double[] arr2 = {2.8,2.7,2.6,2.5};
        System.out.println("arr1+arr2= "+mathDemo.add(arr1, arr2));
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731211429_u6fDuA_Screenshot.jpeg)

这里注意类型的一致，否则会出现神奇的bug，比如你将`double arr1Sum=0,arr2Sum=0;`改为int，那么结果会是12。

#### 编程练习

定义两个重载的方法,分别求圆和长方形的面积。效果图:

![](http://myphoto.mtianyan.cn/20180731211952_nNMjk7_Screenshot.jpeg)

任务

  1. 定义两个求面积的重载方法,圆周率可以用Math.PI表示
  2. 在主方法中调用方法并将结果输出。

注意:当圆的半径为4.5 ,长方形周长分别为8和5时，可得到如效果图所示的结果

```java
package cn.mtianyan.method;

public class AreaDemo {
    // 求圆形面积
    public double area(double radius){
        return Math.PI*radius*radius;
    }
    // 求长方形面积
    public double area(double width,double height){
        return width*height;
    }
    public static void main(String[] args) {
        AreaDemo areaDemo = new AreaDemo();
        System.out.println("圆面积: "+areaDemo.area(2.0));
        System.out.println("长方形面积: "+areaDemo.area(3.0, 4.0));
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731212802_JL6FTj_Screenshot.jpeg)

### 基本数据类型的传值

参数的传递问题; 例: 对两个变量的值进行交换并打印输出。

方法调用前和方法调用后，主方法中传给方法的参数值是否发生了变化。传值问题。

```java
package cn.mtianyan.method;

public class ExchangeDemo {
    public void swap(int a,int b){
        int temp= 0;
        System.out.println("交换前: a="+a+" b="+b);
        temp = a;a = b;b = temp;
        System.out.println("交换后: a="+a+" b="+b);
    }
    public static void main(String[] args) {
        ExchangeDemo exchangeDemo = new ExchangeDemo();
        int m =5,n=3;
        exchangeDemo.swap(m,n);
        System.out.println();
        System.out.println("main中的m: "+m);
        System.out.println("main中的n: "+n);
    }
}

```

运行结果:

![](http://myphoto.mtianyan.cn/20180731215306_zL9IS1_Screenshot.jpeg)

交换前和交换后，main中的值并没有发生变化。

![](http://myphoto.mtianyan.cn/20180731215351_jNMkYF_Screenshot.jpeg)

m和n开辟了内存空间。

![](http://myphoto.mtianyan.cn/20180731215436_vnSRcr_Screenshot.jpeg)

传值时将m,n传给a,b只是将4和5这两个字面值传给了a,b;并不是把m,n的地址传过去。

![](http://myphoto.mtianyan.cn/20180731215603_eOJ2KT_Screenshot.jpeg)

只是a和b当中的值换成了5,4 但是m和n中的并没有发生变化。

主方法中调用自定义函数和其他自定义方法调用自定义方法是有区别的。主方法中必须实例化一个对象出来，而自定义方法中不需要实例化对象可直接通过名字调用(在一个类中)。

```java
package cn.mtianyan.method;

public class ExchangeDemo {
    public void swap(int a,int b){
        int temp= 0;
        System.out.println("交换前: a="+a+" b="+b);
        temp = a;a = b;b = temp;
        System.out.println("交换后: a="+a+" b="+b);
    }
    public void swapTest(){
        int m =5,n=3;
        swap(m,n);
        System.out.println("main中的m: "+m);
        System.out.println("main中的n: "+n);
    }
    public static void main(String[] args) {
        ExchangeDemo exchangeDemo = new ExchangeDemo();
        // exchangeDemo.swap(m,n);
        exchangeDemo.swapTest();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731220221_dJfQMr_Screenshot.jpeg)

经验: 通常我们会将各种功能模块的代码进行封装，最后主方法里只放几行调用语句。

在方法内对于传入的值进行改变，查看main中的值是否发生了变化。

```java
package cn.mtianyan.method;

public class ExchangeDemo1 {
    public void add(int n){
        n++;
        System.out.println("方法中n="+n);
    }
    public static void main(String[] args) {
        int n=10;
        System.out.println("方法调用前n的值: "+n);
        ExchangeDemo1 exchangeDemo1 = new ExchangeDemo1();
        exchangeDemo1.add(n);
        System.out.println("方法调用后n的值: "+n);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731220704_0wdyAB_Screenshot.jpeg)

普通类型是传值，只有传递对象时才是传递引用(地址)会修改main中的值，后面会讲到。

### 数组的传值

数组作为方法参数的传值问题

```java
package cn.mtianyan.method;

public class ArrayPassValue {
    // 定义方法用于修改某个数组元素的值
    public void  updateArray(int[] a){
        a[0] = 99;
        System.out.println("方法中arr值:");
        for (int n :a) {
            System.out.print(n+" ");
        }
    }
    public static void main(String[] args) {
        int[] arr = {1,3,4};
        ArrayPassValue arrayPassValue = new ArrayPassValue();
        arrayPassValue.updateArray(arr);
        System.out.println();
        System.out.println("main中修改后arr值");
        for (int n:arr) {
            System.out.print(n +" ");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731224124_WYJfAW_Screenshot.jpeg)

可以看到数组作为方法参数时，数组的值会被方法内部修改掉。

arr 会开辟一段连续的内存空间，然后arr指向数组中的第一个元素arr[1]; 调用方法传值时，是将a也指向了数组的第一个元素arr[1];a和arr指向同一块内存。

数据类型分为基本数据类型和引用数据类型。基本数据类型传的是值，引用数据类型传的是引用(地址指向)，对象作为参数也会影响;

### 可变参数列表

可变参数就是参数的数量是不确定的，它可以随时变化。

例:

```java
public void sum(int... n){}
```

求和方法中的应用。

```java
package cn.mtianyan.method;

public class VariableArgsDemo {
    // 求和(可变)
    public void sum(int... n){
        int sum =0;
        for (int i:n) {
            sum +=i;
        }
        System.out.println("sum:"+sum);
    }
    public static void main(String[] args) {
        VariableArgsDemo variableArgsDemo = new VariableArgsDemo();
        variableArgsDemo.sum(1,2,3);
        variableArgsDemo.sum(3,4,5,10);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731230801_3BUAhk_Screenshot.jpeg)

可变参数列表和数组有点像，后面我们会介绍它们之间的区别和联系。

代码示例: 可变参数中的查找问题

```java
package cn.mtianyan.method;

public class VariableArgsDemo1 {
    public void search(int n,int... a){
        boolean flag =false;
        for (int i=0;i<a.length-1;i++){
            if(n == a[i]){
                System.out.println("找到了值为"+n+"的数，其下标为"+i);
                flag = true; break;
            }
        }
        if(flag){
            System.out.println();
        }else{
            System.out.println("没找到");
        }
    }
    public static void main(String[] args) {
        VariableArgsDemo1 variableArgsDemo1 = new VariableArgsDemo1();
        variableArgsDemo1.search(1,2,1,3,4);
        variableArgsDemo1.search(3,12,2,3,6);
        variableArgsDemo1.search(10,12,2,3,6);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731235058_SsUur9_Screenshot.jpeg)

 注意: 参数列表中如果有两个以上的参数,可变参数一定是在最后的!

```java
        int[] arr1 = {1,2,3,4};
        variableArgsDemo1.search(2,arr1);
```

![](http://myphoto.mtianyan.cn/20180731235253_FY0bu1_Screenshot.jpeg)

结论: 可以将数组传递给可变参数列表

![](http://myphoto.mtianyan.cn/20180731235423_Mb5Q1o_Screenshot.jpeg)

可以看到，在方法定义中,认为当前的两个search方法重复定义,而不是重载!

但是数组作为参数时，是不能将多个值传递给数组的!

**因为要把可变参数放到参数的末尾，所以一个方法中只能有一个可变参数** 可变参数列表有时又称可变参数类型

### 可变参数列表作为方法参数的重载问题

```java
package cn.mtianyan.method;

public class VariableArgsDemo2 {
    public int add(int a,int b){
        System.out.println("不带可变参数的方法被调用");
        return a+b;
    }
    public int add(int... a){
        System.out.println("带可变参数的方法被调用");
        int sum =0;
        for (int n:a) {
            sum +=n;
        }
        return sum;
    }
    public static void main(String[] args) {
        VariableArgsDemo2 variableArgsDemo2 = new VariableArgsDemo2();
        System.out.println(variableArgsDemo2.add(1, 2));
        System.out.println(variableArgsDemo2.add(1, 2, 3));
    }
}

```

虽然两个方法都符合当前两个整型参数的要求，但是不带可变参数的方法被优先执行了。
可变参数列表所在的方法是最后被访问的。

单行注释 & 多行注释 & 文档注释

```java
// 单行注释

/* 第一行代码
   第二行代码
   第三行代码
   多行注释  */
```

```java
可以生成程序的帮助文档，通过javadoc命令。
```

```java
/**
 * 关于可变参数列表和重载问题
 * @author mtianyan
 * @version 0.1
 */
```

命令: `javadoc -d doc VariableArgsDemo2.java`  就会生成文档目录，index.html打开。

![](http://myphoto.mtianyan.cn/20180801001339_WnCIWs_Screenshot.jpeg)

### 如何进行方法的调试

和普通的调试没大的区别，就是设置断点，单步调试等;重点在于进入方法的内部。

```java
package cn.mtianyan.method;

public class Rectangle {
    // 求长方形面积方法
    public int area(){
        int length =10;
        int width = 5;
        int intArea = length * width;
        return intArea; // 返回值类型和方法定义返回类型要一致。
        // 变量名和方法名一致不报错。但是我们还是最好不要混淆。
    }
    public static void main(String[] args) {
        Rectangle rectangle = new Rectangle();
        int result = rectangle.area();
        System.out.println("Area="+result);
    }
}
```

![](http://myphoto.mtianyan.cn/20180801001630_MdlLKJ_Screenshot.jpeg)

14行设置断点，点击debug，可以看到值窗口内的main方法参数和rectangle对象。

![](http://myphoto.mtianyan.cn/20180801001733_AxfSlK_Screenshot.jpeg)

进行单步调试，StepOver。

![](http://myphoto.mtianyan.cn/20180801001830_UwBgiF_Screenshot.jpeg)

可以看到直接为我们计算出来具体的Area值，这里我们想进入方法内部。断点不变，重新点击Debug

然后点击Run->StepInto进入方法内部。

![](http://myphoto.mtianyan.cn/20180801002144_MXauRI_Screenshot.jpeg)

可以看到蓝色为我们正在运行到的行，已经进入了函数内部。此时如果我们发现方法太长了不想看了这类情况，可以点击StepOut再回到刚才的14行,由方法内部返回调用处。

### 作业

需求:定义一个类,对数组中的数据进行管理，增删改查。

菜单项:

  1. 插入数据
  2. 显示所有数据
  3. 在指定位置处插入数据
  4. 查询能被3整除的数据
  0. 退出
  
![](http://myphoto.mtianyan.cn/20180801003042_xJfvkR_Screenshot.jpeg)

注意: 添加到数组中的数据不能为0;插入数据时不能把原来的数据覆盖，演示的时候给的是在下标9处插入数据,思考一下如果是3怎么办?如果没有能被3整除的数据应给出提示信息。如果输入0-4以外的数字要给出错误提示

方法: 

```java
public int[] insertData() { } // 插入数据
int[] data = 对象名.insertData(); //调用

public void showData(int[] a, int length) {}  // 显示所有数据,length控制要显示多少个数据
public void insertAtArray(int[] a, int n, int k) {} // 在数组的索引为k位置插入数据n
public void divThree(int[] a) { } // 查询能被3整除的数据
public void notice(){} // 显示提示信息的方法
```

主方法业务逻辑，1,2,3,4 switch结构.

### 总结

方法声明的语法格式

```java
访问修饰符 返回类型 方法名(参数列表){
  方法体
}
```

访问修饰符有: public private protected 和什么都不写的默认default;除过这四个还可以是static

返回值类型可以是void或者任何数据类型。

参数列表可以为空，可以为基本，引用数据类型。

方法的调用:

```java
Demo d = new Demo();
d.show();
```

方法的重载: 方法名相同,参数列表不同

可变参数列表: 可变参数一定是方法中的最后一个参数;数组可以传递给可变参数的方法,反之不行;在重载中,含有可变参数的方法是最后被选中的;

方法的传值问题

  - 基本数据类型传值: 方法中对参数的修改,不会对主方法中传来的数组产生影响。仅仅是传值。
  - 引用数据类型传值: 方法中对数组的改变,会影响主方法中传来的数组。

方法的调试

从下次课开始,将全面进入面向对象环节!首先为大家展示面向对象的基础知识,包括什么是类和对象,构造方法的定义和使用,以及单一职责原则的原理和应用!













































 













