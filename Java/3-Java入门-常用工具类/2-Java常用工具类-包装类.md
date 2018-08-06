Java是一门面向对象的编程语言

![](http://myphoto.mtianyan.cn/20180806012238_SdeivS_Screenshot.jpeg)

但家族却存在几个异类，它们不能像对象一样进行属性，方法的调用，以及相互之间的对象化处理(对象交互)

包装类的存在就是为了解决这些异类所存在的问题，让它们能够像对象一样进行交互。

课程目标:

什么是包装类;包装类与基本数据类型之间的对应关系;包装类的常用方法

### 课程简介

Java中数据类型分为基本数据类型和引用数据类型

![](http://myphoto.mtianyan.cn/20180806012556_ktRbTV_Screenshot.jpeg)

基本数据类型没有属性，方法，无法对象化交互。包装类的产生就是为了解决基本数据类型存在的这些问题。通过包装类可以让基本数据类型获取对象一样的特征，拥有属性方法，行使对象一样的权益，对象化交互。

包装类与基本数据类型之间的对应关系。

|基本类型|对应的包装类|
|--------|------------|
|byte| Byte |
|short|Short|
|int |Integer|
|long|Long|
|float|Float|
|double|Double|
|char|Character|
|boolean|Boolean|

大部分为首字母大写，int和char是两个特例。

### 包装类常用方法

所有的包装类存在于java.lang中

final 修饰，所有的包装类是没有子类的。 所有的数值型都是继承自Number的

![](http://myphoto.mtianyan.cn/20180806013233_5hBbrV_Screenshot.jpeg)

剩下的char 和 boolean是继承自Object类的。

Integer类实现了Comparable接口。有两个构造方法:

![](http://myphoto.mtianyan.cn/20180806013547_az8a1D_Screenshot.jpeg)

静态方法既可以通过类名调用，也可以通过对象进行调用。对于一个系统类，记住常用的方法就可以了。

![](http://myphoto.mtianyan.cn/20180806013800_wfKAyX_Screenshot.jpeg)

虽然方法很多，但是可以看到比如`*Value`方法都是将整型转换为某个数据类型。

### 基本数据类型和包装型之间的转换

对于这两种类型的转换，我们需要认识两个新的名词: 装箱 & 拆箱

![](http://myphoto.mtianyan.cn/20180806133318_1NM3UW_Screenshot.jpeg)

Java中装箱就是把基本类型的值转换为包装类对象。

![](http://myphoto.mtianyan.cn/20180806133356_toRisA_Screenshot.jpeg)

拆箱则是逆操作，将包装类转换为基本数据类型。

```java
package cn.mtianyan.wrapper;

public class WrapperTestOne {
    public static void main(String[] args) {
        // 装箱:把基本数据类型转换成包装类
        // 1.自动装箱
        // 2. 手动装箱
        int t1 =2;
        Integer t2 =t1;

        // 手动
        Integer t3 = new Integer(t1);

        // 测试
        System.out.println("int: "+t1);
        System.out.println("Interger: "+t2);
        System.out.println("Interger2: "+t3);

        System.out.println("==============");
        // 拆箱:把包装类转换成基本数据类型
        // 1. 自动拆箱
        int t4 = t2;
        // 2. 手动拆箱
        int t5 = t3.intValue();

        // 测试
        System.out.println("Interger: "+t2);
        System.out.println("自动拆箱:"+t4);
        System.out.println("手动intValue: "+t5);

        double t6 = t2.doubleValue();
        System.out.println("手动拆箱 double: "+t6);
    }
}
```

![](http://myphoto.mtianyan.cn/20180806134213_5Jmj3r_Screenshot.jpeg)

拆箱和装箱都有自动和手动两种。

### 基本数据类型和字符串之间的转换

```java
package cn.mtianyan.wrapper;

public class WrapperTestChar {
    public static void main(String[] args) {
        // 基本数据类型转换为字符串
        int t1=2;
        String t2 = Integer.toString(t1);

        // 测试
        System.out.println("int 类型转换为String类型对象t2="+t2);
        System.out.println("============");

        // 字符串转换为基本数据类型
        // 1. 包装类的parse方法
        int t3 = Integer.parseInt(t2);
        System.out.println("String类型转换为int变量 t3="+t3);

        // 2. valueOf 先将字符串转换为包装类，再通过自动拆箱完成基本类型转换
        int t4 = Integer.valueOf(t2);
        System.out.println("String类型转换为int变量 t4="+t4);
    }
}
```

可以通过toString方法完成基本数据类型转换为字符串。可以通过Parse和valueOf完成字符串转基本数据类型。其中valueOf是对Parse的封装。

### 需要知道的知识点(上)

包装类对象的初始值;包装类对象间的比较

前面讲过基本数据类型的初始值

|基本类型|默认值|
|--------|------|
|byte|0|
|short|0|
|int|0|
|long|OL|
|float|0.0f|
|double|0.0d|
|char|'\u0000'|
|boolean|false|

上表中的`\u`是指Unicode编码

思考: 定义了一个Integer类型对象one ,他的初始值是不是也等于0呢?

```java
package cn.mtianyan.wrapper;

public class Cat {
    // 成员属性
    String name;
    int month;
    double weight;
}
```

```java
package cn.mtianyan.wrapper;

public class CatTest {
    public static void main(String[] args) {
        // 实例化对象
        Cat one = new Cat();

        // 测试输出
        System.out.println("小猫昵称: "+one.name);
        System.out.println("小猫年龄: "+one.month);
        System.out.println("小猫体重: "+one.weight);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180806135809_qU92SR_Screenshot.jpeg)

```java
package cn.mtianyan.wrapper;

public class Cat {
    // 成员属性
    String name;
    Integer month;
    double weight;
}
```

![](http://myphoto.mtianyan.cn/20180806135852_I1mv6E_Screenshot.jpeg)

此时输出的年龄就不是0，是null了。很好理解，Integer和String一样是对象了，都为null。

```java
Double weight;
```

![](http://myphoto.mtianyan.cn/20180806140014_Y3FTAl_Screenshot.jpeg)

包装类对象之间的比较

### 包装类需要知道的几点知识点

```java
package cn.mtianyan.wrapper;

public class WrapperTestCompare {
    public static void main(String[] args) {
        Integer one = Integer.valueOf(100);
        Integer two = Integer.valueOf(100);

        System.out.println("valueOf创建的one==two 的结果: "+(one==two));

        Integer one1 = new Integer(100);
        Integer two1 = new Integer(100);
        System.out.println("Integer创建的one==two 的结果: "+(one1==two1));
    }
}
```

![](http://myphoto.mtianyan.cn/20180806142249_T369UJ_Screenshot.jpeg)

等号两步如果放的是对象名的话，是对象在内存中的引用，不仅仅是对象值的比较。因此可以看出one two 指向同一块内存。

我们可以试着改变其中一个的值，观察另一个。

```java
        one = 13;
        System.out.println(one);
        System.out.println(two);
```

![](http://myphoto.mtianyan.cn/20180806142630_o6H91g_Screenshot.jpeg)

并没有发生变化。根据源码查看，valueOf会自动缓存值。所以同样的值指向同一个内存。

![](http://myphoto.mtianyan.cn/20180806142743_n54XXR_Screenshot.jpeg)

两次new指向两个不同的空间。

```java
        Integer three = 100;
        System.out.println("three==100的结果: "+(three==100)); // 自动拆箱
```

![](http://myphoto.mtianyan.cn/20180806142924_12dX1h_Screenshot.jpeg)

```java
        Integer four = 100; // 自动拆箱操作等价于 Integer.valueOf(100);
        // 为了提高这个方法的效率，提供了一个缓存区(对象池)
        System.out.println("three==four的结果: "+(three==four));
```

![](http://myphoto.mtianyan.cn/20180806143247_4e24Vs_Screenshot.jpeg)

如果传入的参数在-128到127之间，就会直接在对象池中寻找是否已经有了，有了就直接产生。没有就调用new Integer

three已经被缓存下来了。four来的时候，会和three指向同一块内存。

```java
        Integer five = 200;
        System.out.println("five==200的结果: "+(five==200));
```

自动装箱，拆箱值当然相等。

```java
        Integer five = 200;
        System.out.println("five==200的结果: "+(five==200));

        Integer six = 200;
        System.out.println("six==five的结果: "+(six==five));
```

![](http://myphoto.mtianyan.cn/20180806143819_77mRrg_Screenshot.jpeg)

数值范围只能在-128 到 128之间才能从对象池取。

### 需要知道的几点知识下

![](http://myphoto.mtianyan.cn/20180806143921_KVJ5KD_Screenshot.jpeg)

在java的基本数据类型包装类中除了 float 和 double都是可以应用对象常量池概念的。

```java
        Double d1 = Double.valueOf(100);
        System.out.println("d1==100: "+(d1==100));
        
        Double d2 = Double.valueOf(100);
        System.out.println("d1==d2: "+(d1==d2));
```

![](http://myphoto.mtianyan.cn/20180806144212_hxyIgP_Screenshot.jpeg)

可以看到，Double类型的valueOf并不会进行缓存操作。

```java
    public static Double valueOf(double d) {
        return new Double(d);
    }
```

只是最简单new的调用

### 总结

包装类解决基本数据类型不具有对象化能力的问题。

![](http://myphoto.mtianyan.cn/20180806144956_jpGxpt_Screenshot.jpeg)

java.lang 装箱 拆箱 基本数据类型 和字符串转换。

在下一集中,将为大家带来字符串处理类String和StringBuilder。通过实例演示了常用方法的使用,以及二者的存储方式及区别





