## 数组

为什么要使用数组？

学生成绩排序问题

![](http://myphoto.mtianyan.cn/20180730122104_35chOE_Screenshot.jpeg)

如果没有数组，我们得定义30个变量。

数组是**相同类型的**数据**按顺序组成的**一种**引用数据类型**

要学习的内容:

  - 一维数组: 声明 创建 初始化 元素的引用 长度 数组的应用
  
### 数组的概念

数组声明语法格式:

```java
数据类型[] 数组名;
数据类型 数组名[]; //和c等一致的形式

int[] myIntArray;
int myIntArray[];
char[] ch;
String[] strArray;//字符串是一个类，这是对象数组。
```

变量声明的语法格式:

```java
数据类型 变量名;
```

数据类型后加上了中括号。命名规范上第一个单词首字母小写，之后单词首字母大写。

数组的创建:

语法格式一:先声明后创建

```java
数据类型[] 数组名;
数组名 = new 数据类型[数组长度]; // new是在创建一个对象，这里是创建一个数组
int[] arr;
arr= new int[10]; // 创建一个长度为10的整型数组
```

语法格式二:声明的同时创建数组

```java
数据类型[] 数组名= new 数据类型[数组长度];
int[] arr= new int[10]; // 创建长度为10的整型数组arr
```

注意:数组创建时长度必须指定

#### 数组在内存中的存储

数组会被分配连续的内存空间

```java
int[] a=new int[5];
```

![](http://myphoto.mtianyan.cn/20180730123211_IfQRFs_Screenshot.jpeg)

默认值都为0。数组名是一个对象，指向数组中的第一个元素。

![](http://myphoto.mtianyan.cn/20180730123254_37KImI_Screenshot.jpeg)

局部变量和数组的默认值问题: 局部变量是没有默认值的，如果没有初始化，是内存中的随机值。而数组是有默认值的0的,因为数组本身是对象。

数组的初始化: 声明数组的同时给数组赋值,叫做数组的初始化。

例子:

```java
int[] arr={1,2,3,4,5,6,7,8,9,10};
```

数组的长度就是初始化时所给数组元素的个数

数组元素的引用

语法格式:

```java
数组名[下标];
```

注意:下标从0开始

```java
int[] arr={1,2,3,4,5,6,7,8,9,10};
```

![](http://myphoto.mtianyan.cn/20180730144444_pnIZDX_Screenshot.jpeg)

连续的内存空间当中存储数组的值

![](http://myphoto.mtianyan.cn/20180730144529_lfn963_Screenshot.jpeg)

变量名 和 变量值的关系

数组的长度:

```java
int[] arr={1,2,3,4,5,6,7,8,9,10};
// 属性length表示数组的长度,如a.length
```

### 一维数组的应用

```java
package cn.mtianyan.array;

public class ArrayDemo {
    public static void main(String[] args) {
        // 声明数组
        int[] intArray;
        String strArray[];

        // 创建数组
        intArray = new  int[5];
        strArray = new String[10];

        // 声明数组的同时进行创建
        float[] floatArray = new float[4];

        // 初始化数组
        char[] ch = {'a','b','c','d'};
        System.out.println("ch数组的长度为: "+ch.length);

        // 数组默认值
        char[] charArray = new char[5];
        System.out.println("intArray数组的第二个元素为: "+intArray[1]);
        System.out.println("strArray数组的第五个元素为: "+strArray[4]);
        System.out.println("floatArray的最后一个元素为:"+floatArray[floatArray.length-1]);
        System.out.println("charArray的第一个元素为: "+charArray[0]+"End");
    }
}
```

![](http://myphoto.mtianyan.cn/20180730145611_HEStUI_Screenshot.jpeg)

所有对象数组都像strArray一样在创建时默认值为null;使用循环对整型数组赋值。

```java
        // 循环为整型数组赋值
        for (int i=0;i<5;i++){
            intArray[i] = i+1;
        }
        System.out.println("整型数组intArray的元素为: ");
        for (int i=0;i<5;i++){
            System.out.print(intArray[i]+" ");
        }
```

![](http://myphoto.mtianyan.cn/20180730145953_YG4i1h_Screenshot.jpeg)

数组下标越界，会报出异常。ArrayIndexOutOfBoundsException（运行时异常） 数组下标越界异常。

### 求数组元素的累加和

定义一个整型数组，从键盘接收输入值，然后求累加和。

```java
package cn.mtianyan.array;

import java.util.Scanner;

public class ArrayAddDemo {
    public static void main(String[] args) {
        int[] intArray = new int[5];
        System.out.println("请输入五个数组的元素,输入0为计算前面几个输入值，只输入0退出程序:");
        Scanner scanner = new Scanner(System.in);
        int sum=0;
        while (true) {
            sum = 0;
            for (int i = 0; i < 5; i++) {
                intArray[i] = scanner.nextInt();
                if (intArray[i] == 0) break;
                sum = sum + intArray[i];
            }
            if (sum==0) break;
            System.out.println("sum:" + sum);
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180730151636_faar37_Screenshot.jpeg)

```java
package cn.mtianyan.array;

import java.util.Scanner;

public class ArrayDemo1 {
    public static void main(String[] args) {
        int[] a = new int[5];
        Scanner scanner = new Scanner(System.in);

        for (int i=0;i<a.length;i++){
            System.out.print("请输入第"+(i+1)+"个元素: ");
            a[i] = scanner.nextInt();

        }
        System.out.println();
        System.out.println("数组元素的内容为: ");
        for (int i=0;i<a.length;i++){
            System.out.print(a[i]+" ");
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180730152248_Uwrrqc_Screenshot.jpeg)

```java
        int sum=0;
        for (int i=0;i<a.length;i++){
            sum +=a[i];
        }
        System.out.println("数组累加和为: "+sum);
```

![](http://myphoto.mtianyan.cn/20180730152552_XAjVTC_Screenshot.jpeg)

#### 编程练习

求数组中能被3整除的元素并打印输出。

效果图:

![](http://myphoto.mtianyan.cn/20180730153616_mtZkJe_Screenshot.jpeg)

任务:
  1. 定义一个整型数组a并初始化
  2. 循环遍历数组,找出能被3整除的元素并打印输出

```java
package cn.mtianyan.array;

public class ArrayExercise {
    public static void main(String[] args) {
        int[] a ={1,2,6,12,15,16,17};

        System.out.println("能被3整除的数组元素为:");
        for (int i=0;i<a.length;i++){
            if (a[i] % 3==0){
                System.out.println(a[i]);
            }
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180730154033_gOBCih_Screenshot.jpeg)

### 求数组元素的最大值

```java
package cn.mtianyan.array;

public class ArrayMaxDemo {
    public static void main(String[] args) {
        // 求数组元素最大值
        int[] a ={1,2,6,12,35,16,17};
        int max = 0;
        for (int i=0;i<a.length;i++){
            if(a[i]>max){
                max = a[i];
            }
        }
        System.out.println("max:" +max);
    }
}
```

![](http://myphoto.mtianyan.cn/20180730154321_JxCQpF_Screenshot.jpeg)

优化: max 之间等于a[0] 然后循环就可以从1开始了，少了一次比较。

```java
 public static void main(String[] args) {
        // 求数组元素最大值
        int[] a ={34,23,78,56,31};
        int max = a[0];
        for (int i=1;i<a.length;i++){
            if(a[i]>max){
                max = a[i];
            }
        }
        System.out.println("max:" +max);
    }
```

![](http://myphoto.mtianyan.cn/20180730161301_JwcBaF_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180730154618_wX13nh_Screenshot.jpeg)

### 增强型for循环

和数组结合起来使用会更加方便

又叫foreach循环, foreach循环应用:

```java
        System.out.println();
        System.out.println("使用foreach输出数组内容:");
        for (int n:a) {
            System.out.print(n+" ");
        }
```

![](http://myphoto.mtianyan.cn/20180730173738_vcjxFP_Screenshot.jpeg)

如何对变量a,b的值进行交换

```java
int a=3,b=5;
int temp;
temp=a;a=b;b=temp;
```

### 冒泡排序

对一组整数按照由小到大的顺序进行排序。

![](http://myphoto.mtianyan.cn/20180730224225_66HPV4_Screenshot.jpeg)

假设存放着这样一组整数，如何将它们从小到大进行排序。

>对数组中元素从头到位对相邻的元素进行大小比较。

过程: 对34和53进行比较，发现34和53相比，53大的在右边是正常的，什么都不用做，12和53相比发现53是大的，53向上浮一位。53和32进行比较，53比32大，再次上浮。52和56比，很正常。然后56和17比，56上浮。

![](http://myphoto.mtianyan.cn/20180730225111_mw3yLV_Screenshot.jpeg)
![](http://myphoto.mtianyan.cn/20180730233605_CcEpQu_Screenshot.jpeg)

这就是冒泡排序.

```java
package cn.mtianyan.array;

public class SortDemo {
    public static void main(String[] args) {
        // 冒泡排序
        int[] a ={34,53,12,32,56,17};
        System.out.println("排序前的数组元素为: ");
        for (int n:a){
            System.out.print(n+" ");
        }
        System.out.println();
        int temp;
        // 外层控制趟，内层冒泡
        for(int i=0;i<a.length-1;i++){
            // 内层循环控制每趟排序,越到后边的趟，需要排的越少。
            for (int j=0;j<a.length-1-i;j++){
                // 前一个数大于后一个数，交换位置
                if(a[j] > a[j+1]){
                    temp = a[j];
                    a[j] = a[j+1];
                    a[j+1] = temp;
                }
            }
        }
        System.out.println("从小到大排序排序后的数组元素为: ");
        for (int n:a) {
            System.out.print(n+" ");
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731001701_pEEnn9_Screenshot.jpeg)

```java
package cn.mtianyan.array;

public class SortReverseDemo {
    public static void main(String[] args) {
        // 冒泡排序
        int[] a ={34,53,12,32,56,17};
        System.out.println("排序前的数组元素为: ");
        for (int n:a){
            System.out.print(n+" ");
        }
        System.out.println();
        for (int i=0;i<a.length-1;i++){
            for (int j=0;j<a.length-1-i;j++){
                if(a[j] < a[j+1]){
                    int temp = 0;
                    temp = a[j];
                    a[j] = a[j+1];
                    a[j+1] = temp;
                }
            }
        }
        System.out.println("从大到小排序后的数组元素为: ");
        for (int n:a){
            System.out.print(n+" ");
        }

    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731002445_kFUbqG_Screenshot.jpeg)

在下一集中,将为大家带来数组家族的另外一个成员:二维数组!在课程中会通过实例演示维数组的声明、创建、初始化以及应用!























