设计模式的官方解释: 一套被反复使用，经过分类编目，多数人知晓的，代码设计经验的总结。

设计模式是软件开发人员在软件开发过程中面临的一般问题的解决方案。

对于建一栋房子，只要类型确定了，对于设计师来说都有其可以套用的模板，但是这些模板都是经过行业考验，是经验的总结。

![](http://myphoto.mtianyan.cn/20180804004729_HbqHTV_Screenshot.jpeg)

软件过程中遇到的开发场景，难题。设计模式有很多种，通常认为这23种是其他设计模式的基础。

![](http://myphoto.mtianyan.cn/20180804004945_vei4o4_Screenshot.jpeg)

作用分类: 关注对象创建过程，类和对象组合，对象之间的通信过程。

![](http://myphoto.mtianyan.cn/20180804005124_krGpld_Screenshot.jpeg)

如何学好设计模式？

设计模式是基于场景的解决方案，所以学习时要针对设计模式针对的真实场景来学习。

如果某个新场景的解决方案被认可,那我们就可以定义一个新的设计模式

### 单例模式的定义和作用

一山不容二虎

计算机系统中，我们只需要他有一个唯一的实例在工作。无论一个电脑连接了多少台打印机，但是它的后台处理程序只有一个唯一的实例在工作，这样才不会出现混乱的交错情况

![](http://myphoto.mtianyan.cn/20180804005514_zzhsjS_Screenshot.jpeg)

驱动程序，线程池，缓存，日志等等，在实际的软件应用中很多时候都会要求有且只有一个实例。

目的: 使得类的一个对象成为该类系统中的唯一实例

定义: 一个类有且仅有一个实例,并且自行实例化向整个系统提供

要点: 1. 某个类只能有一个实例; 2. 必须自行创建实例; 3. 必须自行向整个系统提供这个实例

![](http://myphoto.mtianyan.cn/20180804005853_BsStE5_Screenshot.jpeg)

实现:

  1. 只提供**私有**的构造方法(private是访问限制能力最强的修饰符，只能在当前类内被访问，经过private修饰，该类的对象在类外无法通过new关键字直接实例化，限制类实例化产生的渠道);
  2. 含有一个该类的**静态**私有对象()（有且仅有一个实例，static修饰的静态成员恰好满足该类有且仅有一个，无论有多少对象都共享这一个）;
  3. 提供一个静态的公有方法用于创建、获取静态私有对象(向外部系统提供唯一的对象实例)

Java中实现单例模式的代码实现方案有两种:

![](http://myphoto.mtianyan.cn/20180804010403_WfKalg_Screenshot.jpeg)

饿汉式和懒汉式: 饿汉式是在类中私有对象创建的过程中就即刻去完成它的实例化操作。不管你用不用我先放在这。

懒汉式: 对象创建时并不直接实例化，而是在静态公有方法中进行实例化。只有在用到的时候，才会去进行实例化的操作。

### 饿汉式代码实现

```java
package cn.mtianyan.singleton;

// 饿汉式:创建对象实例的时候直接初始化,饿的时候都比较着急
public class HungryMan {
    // 1. 创建私有构造方法
    private HungryMan(){

    }

    // 2. 创建该类型的私有静态实例
    private static HungryMan instance = new HungryMan();
    // 饿汉模式: 创建静态实例的时候直接进行实例化。

    // 3. 创建公有静态方法返回静态化实例对象
    public static HungryMan getInstance() {
        return instance;
    }
}
```

```java
package cn.mtianyan.singleton;

public class Test {
    public static void main(String[] args) {
        // HungryMan hungryMan = new HungryMan();
        HungryMan one = HungryMan.getInstance();
        HungryMan two = HungryMan.getInstance();

        System.out.println(one == two);
        System.out.println(one);
        System.out.println(two);
    }
}
```

![](http://myphoto.mtianyan.cn/20180804014320_xh3QTO_Screenshot.jpeg)

对于饿汉式是一种典型的空间换时间的方式，在类进行加载时，我们静态实例对象就完成了实例化操作。操作时因为加载时已经实例化过了，操作速度会变快。但是因为类加载时这个对象就已经存在了，它的生命周期较长，占用空间。

![](http://myphoto.mtianyan.cn/20180804014420_icBLnj_Screenshot.jpeg)

#### 编程练习

某公司研发星球维护系统,请使用饿汉式单例模式的实现思想,设计编写地球类。

程序运行参考效果图如下:

![](http://myphoto.mtianyan.cn/20180804014700_yNfiKf_Screenshot.jpeg)

```java
package cn.mtianyan.singleton;

public class Earth {
    private Earth() {
    }

    private static Earth instance = new Earth();

    public static Earth getInstance() {
        return instance;
    }
}
```

```java
package cn.mtianyan.singleton;

public class EarthTest {
    public static void main(String[] args) {
        System.out.println("第一个地球创建中。。。。");
        Earth one = Earth.getInstance();
        System.out.println("第二个地球创建中。。。。");
        Earth two = Earth.getInstance();
        System.out.println("第三个地球创建中。。。。");
        Earth three = Earth.getInstance();

        System.out.println("问: 三个地球是同一个么？");
        System.out.println(one);
        System.out.println(two);
        System.out.println(three);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804015216_jQcgCv_Screenshot.jpeg)

### 懒汉式单例模式

```java
package cn.mtianyan.singleton;
// 懒汉式: 类内实例对象创建时并不直接初始化，直到第一次调用get方法时，才完成初始化操作
public class LazyMan {
    private LazyMan() {

    }

    private static LazyMan instance =null;

    public static LazyMan getInstance() {
        if(instance == null){
            instance = new LazyMan();
        }
        return instance;
    }
}
```

懒汉式: 类内实例对象创建时并不直接初始化，直到第一次调用get方法时，才完成初始化操作

```java
package cn.mtianyan.singleton;

public class Test {
    public static void main(String[] args) {
      
        LazyMan one1 = LazyMan.getInstance();
        LazyMan two1 = LazyMan.getInstance();

        System.out.println(one1 == two1);
        System.out.println(one1);
        System.out.println(two1);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804015722_ulPLgA_Screenshot.jpeg)

时间换空间，操作没有饿汉式快，因为调用时才实例化。

### 编程练习

请使用懒汉式单例模式的实现思想,设计编写皇帝类。

程序运行参考效果图如下:

![](http://myphoto.mtianyan.cn/20180804015924_DxBdht_Screenshot.jpeg)

```java
package cn.mtianyan.singleton;

public class Emperor {
    public static int EmperorNum = 1;
    private Emperor(){
    }
    private static Emperor instance = null;

    public static Emperor getInstance() {
        System.out.println("创建"+EmperorNum+"号皇帝对象");
        EmperorNum++;
        if(instance == null){
            instance = new Emperor();
        }
        return instance;
    }
}
```

```java
package cn.mtianyan.singleton;

public class EmperorTest {
    public static void main(String[] args) {
        Emperor one = Emperor.getInstance();
        Emperor two = Emperor.getInstance();
        Emperor three = Emperor.getInstance();
        System.out.println("三个皇帝对象依次是: ");
        System.out.println(one);
        System.out.println(two);
        System.out.println(three);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804020616_aHqFJo_Screenshot.jpeg)

### 饿汉式 PK 懒汉式

![](http://myphoto.mtianyan.cn/20180804020740_p24tHe_Screenshot.jpeg)

饿汉式，该类的实例在第一次使用时速度是比较快的。懒汉式，第一次使用才实例化。

![](http://myphoto.mtianyan.cn/20180804020851_MMljT0_Screenshot.jpeg)

多线程场景: 同一时刻干多件事。边走路边打电话。

饿汉式，类加载时进行了对象的实例化创建，即使多个进程并发操作，访问的实例也是唯一的，饿汉式线程安全。

懒汉式，第一次使用才会实例化，多个线程并发操作时，由于时间片的切换，可能导致线程风险。

![](http://myphoto.mtianyan.cn/20180804021204_kQ7BRG_Screenshot.jpeg)

>后面我们会介绍多线程的知识，以及如何规避风险。

可以通过关键字Synchronized实现线程的锁定。可以通过静态内部类和枚举保证操作时的线程唯一。

![](http://myphoto.mtianyan.cn/20180804021409_s68PlJ_Screenshot.jpeg)

>1. 同步锁 2. 双重校验锁 3. 静态内部类 4. 枚举

### 单例模式的特点及适用场景

单例模式的优点:

1. 在内存中只有一个对象,节省内存空间; 2. 避免频繁的创建销毁对象, 提高性能; 3. 避免对共享资源的多重占用

缺点:

1. 扩展比较困难; 2. 如果实例化后的对象长期不利用,系统将默认为垃圾进行回收,造成对象状态丢失

使用场景:

  1. 创建对象时占用资源过多,但同时又需要用到该类对象
  2. 对系统内资源要求统一读写,如读写配置信息
  3. 当多个实例存在可能引起程序逻辑错误,如号码生成器
  
每一种设计模式都是针对场景，针对某种具体问题的。具体场景具体分析。

在下一集中,我们将来学习面向对象思想的最后一个重要特性-多态。什么是多态?如何在Java中实现多态?在下面的课程中,将向大家详细介绍。









