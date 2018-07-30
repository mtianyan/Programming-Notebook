## 二维数组

所谓二维数组，可以简单的理解为是一种“特殊”的一维数组，它的每个数组空间中保存的是一个一维数组。

那么如何使用二维数组呢，步骤如下：

1. 声明数组并分配空间

```java
数据类型[][] 数组名= new 数据类型[行的个数][列的个数];
```

或者分为两步:

```java
数据类型[][] 数组名;
数组名= new 数据类型[行的个数] [列的个数];
```

具体到实际例子:

```java
//定义一个两行三列的二维数组
int[][] num=new int[2][3];
```

2. 赋值

二维数组的赋值，和一维数组类似，可以通过下标来逐个赋值，注意索引从 0 开始

```java
数组名[行的索引] [列的索引] = 值;
```

也可以在声明数组的同时为其赋值

```java
数据类型[][] 数組名={ {值1,值2...}, {值11,值22...}, {值21,值22...} };
```

具体到实际的例子:

```java
//给第1行第1列的元素赋值
num[0][0]=12;
```

3. 处理数组

二维数组的访问和输出同一维数组一样，只是多了一个下标而已。在循环输出时，需要里面再内嵌一个循环，即使用**二重循环**来输出二维数组中的每一个元素。如：

```java
package cn.mtianyan;

public class ArrayTwo {
    public static void main(String[] args) {
        // 定义一个两行三列的二维数组并赋值
        int[][] twoArray = {{1,2,3},{4,5,6}};
        for (int i=0;i<twoArray.length;i++){
            // 每行的元素
            for (int j=0;j<twoArray[i].length;j++){
                System.out.print(twoArray[i][j]);
            }
            System.out.println();
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180731005006_sccgk5_Screenshot.jpeg)

需要了解的：在定义二维数组时也可以只指定行的个数，然后再为每一行分别指定列的个数。如果每行的列数不同，则创建的是不规则的二维数组，如下所示：

```java
package cn.mtianyan;

public class ArrayTwoIrregular {
    public static void main(String[] args) {
        int[][] irregularArray = new int[2][]; //这里的2是数组容量
        // irregularArray[0] = new int[2];
        // irregularArray[1] = new int[3];
        // irregularArray[0][1] = 3;

        irregularArray[0] = new int[]{1, 2};
        irregularArray[1] = new int[]{1, 2, 3};
        for (int i=0;i<irregularArray.length;i++){
            for (int j=0;j<irregularArray[i].length;j++){
                System.out.print(irregularArray[i][j]);
            }
            System.out.println();
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180731005923_aRmZr2_Screenshot.jpeg)

#### 编程任务

功能要求：定义一个两行三列的二维数组 names并赋值，使用二重循环输出二维数组中的元素。

运行结果：

![](http://myphoto.mtianyan.cn/20180731010020_BUMt6g_Screenshot.jpeg)

package cn.mtianyan;

public class ArrayTwoExercise {
    public static void main(String[] args) {
        // 定义两行三列的二维数组并赋值
        String [][] names={{"tom","jack","mike"},{"zhangsan","lisi","wangwu"}};
        for (int i=0;i<names.length;i++){
            for (int j=0;j<names[i].length;j++){
                System.out.println(names[i][j]);
            }
            System.out.println();
        }
    }
}

运行结果:

![](http://myphoto.mtianyan.cn/20180731010245_IS4eyQ_Screenshot.jpeg)

### 数组总结

一维数组: 声明 创建 初始化 元素的引用 长度 数组的应用

注意的问题: 
  - 数组是引用数据类型(不同类型数组有其初始的默认值); -
  - 创建数组时,会开辟连续的内存空间;
  - 数组长度使用length属性获取;
  - 数组元素的下标从0开始
  - 数组下标越界问题

下集预告:

我们将学习到java1基础部分一个非常重要的部分，包括方法的创建和调用，方法的重载和传值问题，什么是可变参数列表，最后来看一下方法如何进行调试！



