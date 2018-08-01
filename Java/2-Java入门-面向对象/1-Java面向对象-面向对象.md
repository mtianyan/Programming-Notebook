通过前面的学习我们对于java的语法结构有了一定的认识，掌握了分支结构，循环结构等常用的程序逻辑，也能运用这些知识解决一些简单问题。

以前我们面向过程，现在我们面向对象。这是从盖小房子走向盖摩天大楼的第一步。

面向对象 : 程序的稳定性 可扩展性 可重用性 都有非常大的优势。

本次学习我们将学习如何通过java语言实现面向对象的三大特征: 继承 封装 多态; 编写具有面向对象思想的java程序。

### 类和对象
学习内容:

  1. 什么是对象
  2. 什么是面向对象
  3. 什么是类
  4. 类和对象的关系

对象: 万物皆对象，现实中存在的事物都可以看成一个对象。

面向对象: 人关注对象; 人关注事物信息

遵循现实生活中的场景，比如想养一只猫: 小点的,可爱的,不容易掉毛的。店员提供的猫:

![](http://myphoto.mtianyan.cn/20180801093621_Af0IB1_Screenshot.jpeg)

这就是一个面向对象的过程。

![](http://myphoto.mtianyan.cn/20180801093710_jgmbSw_Screenshot.jpeg)

我的描述是一个抽象的虚拟的特征，而店员带我看的两只猫就是满足特征的实物。

![](http://myphoto.mtianyan.cn/20180801093824_xsdWU5_Screenshot.jpeg)

类是模子，确定对象将会拥有的特征(属性)和行为(方法); 对象是类的实例表现;类是对象的类型;对象是特定类型的数据

属性和方法: 属性:对象具有的各种静态特征，对象有什么”; 方法:对象具有的各种动态行为,对象能做什么”

类: 类，抽象的概念; 是一个模板 & 对象:是一个看得到、摸得着的具体实体。

### 创建类

![](http://myphoto.mtianyan.cn/20180801094220_v6Vjsw_Screenshot.jpeg)

名的推荐命名规范: 英文字母小写;域名的倒序

猫的属性: 昵称、年龄、体重、品种; 方法:跑动、吃东西

```java
package cn.mtianyan.animal;

/**
 * 宠物猫类
 * @author mtianyan
 */
public class Cat {
    // 猫的成员属性: 昵称、年龄、体重、品种;
    String name;
    int age;
    float weight;
    String species;

    // 方法:跑动、吃东西
    public void run(){
        System.out.println("小猫在跑");
    }
    public void eat(){
        System.out.println("小猫吃鱼");
    }
}
```

### 实例化对象

```java
package cn.mtianyan.animal;

public class CatTest {

    public static void main(String[] args) {
        Cat oneCat = new Cat();
        oneCat.run();
        oneCat.eat();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801095359_hq0iW2_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180801095501_H4vkNu_Screenshot.jpeg)

普通的变量如果没有初始化是不能被打印输出的。而对象的成员变量则可以之间打印，因为它们有默认值。

```java
        System.out.println(oneCat.age);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801095649_eYxiL0_Screenshot.jpeg)

```java
        System.out.println("年龄: "+ oneCat.age);
        System.out.println("昵称: "+ oneCat.name);
        System.out.println("体重: " + oneCat.weight);
        System.out.println("品种: " + oneCat.species);
```

![](http://myphoto.mtianyan.cn/20180801095939_W7TVH3_Screenshot.jpeg)

可以看到字符串类型的是null，int型是0，float型是0.0

```java
        oneCat.name = "花花";
        oneCat.age = 2;
        oneCat.weight = 1000;
        oneCat.species = "中华田园猫";
        
        System.out.println("年龄: "+ oneCat.age);
        System.out.println("昵称: "+ oneCat.name);
        System.out.println("体重: " + oneCat.weight);
        System.out.println("品种: " + oneCat.species);
```

![](http://myphoto.mtianyan.cn/20180801100214_MON7LO_Screenshot.jpeg)

类实例化对象，对象使用属性和方法。方法带参数，重载run方法。

```java
    public void run(String name){
        System.out.println(name+"在跑");
    }

// CatTest中调用    
oneCat.run(oneCat.name);
```

![](http://myphoto.mtianyan.cn/20180801100601_UrwiBd_Screenshot.jpeg)

### 单一职责原则

问题来了，我们为什么要把Cat类和包含main方法的CatTest类进行分离呢？

单一职责原则(单一功能原则) 一个类应该有且只有一个引起功能变化的原因。

一个类应该只干一件事不能太累。

如果在一个类当中,承担的功能越多.交融，耦合性就越高，被复用的可能性就越低。特别是因为耦合度高，可能因为一个职责的变化，引起其他职责的变化，进而影响整个程序的运行。

![](http://myphoto.mtianyan.cn/20180801101137_8nHG1s_Screenshot.jpeg)

在程序设计中我们建议将不同的职责放到不同的类当中来实现,把不同的引发变化的原因封装进不同的类。

面向对象的设计原则不止这一个，还有:里氏替换原则;依赖倒置原则;开闭原则;迪米特法则;组合/聚合复用原则;接口隔离原则。其他这些我们都会学习到。

### new关键字

实例化对象的过程可以分为两部分: 声明对象 Cat one;实例化对象 new Cat();

![](http://myphoto.mtianyan.cn/20180801101629_UpBVn7_Screenshot.jpeg) 

声明对象时，是在栈中开辟了一块内存空间，此时还不是一个有效的对象，因为此时one的空间里是空的。如果此时用它进行属性的方法和调用是不被允许的。

```java
        Cat twoCat;
        twoCat.run();
```

![](http://myphoto.mtianyan.cn/20180801101858_9fmgyz_Screenshot.jpeg)

实例化对象是在堆空间开辟一块空间，完成了具体对象相关信息的初始化操作。

![](http://myphoto.mtianyan.cn/20180801102105_NU1VU2_Screenshot.jpeg)

也就是声明对象和实例化对象是在内存中的不同空间完成的，通过赋值操作，将两者关联。具体的关联就是将堆中具体对象的内存地址存放是在one中。

![](http://myphoto.mtianyan.cn/20180801102321_pAQVCv_Screenshot.jpeg)

```java
package cn.mtianyan.animal;

public class CatTest {

    public static void main(String[] args) {
        Cat oneCat = new Cat();

        oneCat.name = "花花";
        oneCat.age = 2;
        oneCat.weight = 1000;
        oneCat.species = "中华田园猫";

        System.out.println("年龄: "+ oneCat.age);
        System.out.println("昵称: "+ oneCat.name);
        System.out.println("体重: " + oneCat.weight);
        System.out.println("品种: " + oneCat.species);

        System.out.println("-----------------------");

        Cat twoCat=new Cat();
        twoCat.name = "花花";
        twoCat.age = 2;
        twoCat.weight = 1000;
        twoCat.species = "中华田园猫";
        System.out.println("年龄: "+ twoCat.age);
        System.out.println("昵称: "+ twoCat.name);
        System.out.println("体重: " + twoCat.weight);
        System.out.println("品种: " + twoCat.species);
    }
}
```

![](http://myphoto.mtianyan.cn/20180801102612_ygEWcU_Screenshot.jpeg)

两只猫的相关信息一模一样，但是实际它们指向的是堆中两块不同的内存。修改two的信息是不会对one产生影响的。

![](http://myphoto.mtianyan.cn/20180801102846_1dgxQq_Screenshot.jpeg)

```java
twoCat.name = "欢欢";
twoCat.species = "英国短毛猫";
```

![](http://myphoto.mtianyan.cn/20180801103002_cVJ6tt_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180801103036_rjZHUW_Screenshot.jpeg)

老王，老张有一套一模一样户型的房子，但是各自有各自的钥匙，老王对房子做的个性化装修，不会对老张的房子造成影响。

我们可不可以一套房子有两把钥匙呢？

```java
Cat twoCat=oneCat;
```

将one赋值给two，one里装的是啥呢？

![](http://myphoto.mtianyan.cn/20180801103400_ZKpWJ5_Screenshot.jpeg)

装的是堆中one对象的地址，也就是one家的钥匙，把钥匙给了two;那么two也将能操作one的房间。此时的one two都有钥匙，对房子都可进行操作（同一间房子）

```java
package cn.mtianyan.animal;

public class CatTest {

    public static void main(String[] args) {
        Cat oneCat = new Cat();

        oneCat.name = "花花";
        oneCat.age = 2;
        oneCat.weight = 1000;
        oneCat.species = "中华田园猫";

        System.out.println("年龄: "+ oneCat.age);
        System.out.println("昵称: "+ oneCat.name);
        System.out.println("体重: " + oneCat.weight);
        System.out.println("品种: " + oneCat.species);

        System.out.println("-----------------------");

        Cat twoCat=oneCat;
        twoCat.name = "欢欢";
        twoCat.age = 2;
        twoCat.weight = 1000;
        twoCat.species = "英国短毛猫";
        System.out.println("年龄: "+ oneCat.age);
        System.out.println("昵称: "+ oneCat.name);
        System.out.println("体重: " + oneCat.weight);
        System.out.println("品种: " + oneCat.species);
    }
}
```

可以看到对Two的操作，One中的也变了。栈当中存储的其实是堆中对象地址的引用

#### 编程练习

编写自定义Person类

程序运行参考效果图如下:
![](http://myphoto.mtianyan.cn/20180801105828_oV5GRS_Screenshot.jpeg)
任务:
创建Person类, 属性:名字(name),年齢(age),成绩(grade); 

方法:
  1. 无参无返回値的student方法,描述为: 我是一名学生!
  2. 带参数(性別sex)的方法,描述为我是一个**孩!(其中，**为传入参数)
  3. 无参无返回値的mySelf方法,介紹自己的姓名、年齢、年级(参数参考效果囹)

创建测试类:实例化対象,传入参数,调用无参无返回値的student和mySelf方法及带参方法sex

```java
package cn.mtianyan.person;

public class Person {
    String name;
    int age;
    String grade;

    public void student(){
        System.out.println("我是一名学生!");
    }

    public void sex(String sex){
        System.out.println("我是一个"+sex+"孩！");
    }
    public void mySelf(){
        System.out.print("我叫"+name+",");
        System.out.printf("今年"+age+"岁了,");
        System.out.printf("读小学"+grade+"年级了。");
    }
}
```

```java
package cn.mtianyan.person;

public class PersonTest {
    public static void main(String[] args) {
        Person one = new Person();
        one.name ="李明";
        one.age = 10;
        one.grade = "五";

        one.student();
        one.sex("男");
        one.mySelf();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801110534_bom13g_Screenshot.jpeg)

### 构造方法: 无参构造方法

构造方法也称为: 构造函数,构造器。使用构造方法完成对象初始化相关设置。

构造方法的调用必须配合new关键字，不能被对象单独的调用。

语法结构:

构造方法与类同名(必须相同)且没有返回值

```java
public 构造方法名(){
  //初始化代码
}
```

![](http://myphoto.mtianyan.cn/20180801110948_vUHhGJ_Screenshot.jpeg)

方法名后面的括号中可以加参数也可以不加参数。只能在对象实例化的时候调用。

之前我们的一贯模式: 方法先声明再调用。而我们之前没有声明过构造方法啊，它是怎么实例化出来的呢？

当没有指定构造方法时,系统会自动添加无参的构造方法;当有指定构造方法,无论是有参、无参的构造方法,都不会自动添加无参的
构造方法;-个类中可以有多个构造方法

```java
    // 构造方法
    public Cat(){
        System.out.println("我是无参构造");
    }
    
    // 调用
    Cat oneCat = new Cat();
    oneCat.run();
```

![](http://myphoto.mtianyan.cn/20180801111637_0GV0qA_Screenshot.jpeg)

```java
    public Cat(String name){
        System.out.println("我是有参构造");
    }
    
    Cat oneCat = new Cat();    
```

```java
Error:(6, 22) java: 无法将类 cn.mtianyan.animal.Cat中的构造器 Cat应用到给定类型;
  需要: java.lang.String
  找到: 没有参数
  原因: 实际参数列表和形式参数列表长度不同
```

### 构造方法:有参构造方法

```java
public Cat(String name,int age,float weight,String species){
this.name = name;
this.age = age;
this.weight = weight;
this.species = species;
}

// 调用
Cat fourArgsCat = new Cat("花花",10,1000,"中华田园猫");

System.out.println("年龄: "+ fourArgsCat.age);
System.out.println("昵称: "+ fourArgsCat.name);
System.out.println("体重: " + fourArgsCat.weight);
System.out.println("品种: " + fourArgsCat.species);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801112724_wV0rM5_Screenshot.jpeg)

```java
name = name; // 构造方法中
```

![](http://myphoto.mtianyan.cn/20180801112924_r94WQp_Screenshot.jpeg)

这里传入的name并没有赋值给对象的name。调试状态下可以看到:

![](http://myphoto.mtianyan.cn/20180801113128_vu7ZCA_Screenshot.jpeg)

程序里的就近原则，会先找同一个作用范围内的，找不到才会去类里找。

```java
public Cat(String newName,int age,float weight,String species){
        name = newName;
}
```

将参数改为不与类的属性成员同名的，可以解决这个问题。

有一种方法既减少工作量(不需要人为的修改参数名与属性名保持不一致)又能让程序知道我们是给属性赋值!

>使用this关键字，显式告诉编译器我们是要赋值给当前对象的属性。

![](http://myphoto.mtianyan.cn/20180801114343_N166Zg_Screenshot.jpeg)

可以看到一个隐式的参数，this对象。

### 构造方法调用(番外)
前面我们说了构造方法不能有返回值，必须与类名一致，而如果此时有一个和类名同名的有返回值的普通方法呢？

```java
public void Cat(){
  System.out.println("我只是一个普通方法，恰好方法名与类名相同了");
}
// 调用
Cat fourArgsCat = new Cat("花花",10,1000,"中华田园猫");
fourArgsCat.Cat();
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801114936_uPerDz_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180801115023_PU2tGf_Screenshot.jpeg)

语法虽然没有什么问题，但是并不推荐大家这样去写。构造方法只能配合new来调用。

类内的普通方法可以直接调用其他类内普通方法

```java
    // 方法:跑动、吃东西
    public void run(){
        eat(); // this.eat()
        System.out.println("小猫在跑");
    }
```

构造方法不能被普通方法所调用。

```java
Error:(33, 9) java: 找不到符号
  符号:   方法 Cat()
  位置: 类 cn.mtianyan.animal.Cat
```

```java
    public Cat(String name,int age,float weight,String species){
        this(); // 在构造方法内调用构造方法
        this.name = name;
        this.age = age;
        this.weight = weight;
        this.species = species;
    }
// 调用
Cat fourArgsCat = new Cat("花花",10,1000,"中华田园猫");
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801115503_oJKv84_Screenshot.jpeg)

同一个类的多个构造方法，可以通过`this()`来调用。

```java
this("哈哈");
```

![](http://myphoto.mtianyan.cn/20180801115652_Mdzxt0_Screenshot.jpeg)

#### 编程练习

编写自定义猴子类.

程序参考运行效果图如下:

![](http://myphoto.mtianyan.cn/20180801115757_gZCIjo_Screenshot.jpeg)

任务

  1. 创建Monkey类,属性:名称(name)和特征(feature);方法:1-无参构造方法(默认初始化name和feature的属性值，属性值参考效果图)
  2. 带参构造方法，接收外部传入的参数，分别传递给name和feature

```java
package cn.mtianyan.monkey;

public class Monkey {
    String name;
    String feature;

    public Monkey(){
        System.out.println("我是使用无参构造产生的猴子: ");
        this.name = "长尾猴";
        this.feature = "尾巴长";
    }
    public Monkey(String name,String feature){
        System.out.println("我是使用带参构造产生的猴子: ");
        this.name = name;
        this.feature = feature;
    }
}
```

```java
package cn.mtianyan.monkey;

public class MonkeyTest {
    public static void main(String[] args) {
        Monkey one = new Monkey();
        System.out.println("名称: " + one.name);
        System.out.println("特征: " + one.feature);
        System.out.println("=====================");
        Monkey two = new Monkey("白头叶猴","头上有白毛，喜欢吃树叶");
        System.out.println("名称: " + two.name);
        System.out.println("特征: " + two.feature);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801120607_GF1nxR_Screenshot.jpeg)

### 课程总结

java是一个面向对象的语言

关注现实存在的事物的各方面的信息,从对象的角度出发,根据事物的特征进行程序设计

对象:用来描述客观事物的一个实体（真实存在）; 类:具有相同属性和方法的一组对象的集合（抽象模板，应该有什么，可以做什么）

![](http://myphoto.mtianyan.cn/20180801120815_i9XRSu_Screenshot.jpeg)

属性通常称为成员属性; 方法称为成员方法。

定义类的基本语法:

```java
public class类名{
  //定义属性部分
  [访问修饰符]数据类型 属性名;
  
  //定义方法部分
  [访问修饰符] 返回类型 方法名(参数){
  }
}
```

创建并引用对象,语法格式:

```java
类名 对象名= new 构造方法();

对象名.属性
对象名.方法名()
```

局部变量没有初值，必须初始化。而成员变量是有其默认值的。

成员属性的初始值:

|基本类型| 默认值|
|--------|-------|
|byte| 0|
|short| 0|
|int| 0|
|long| 0L|
|float| 0.0f|
|double| 0.0d
|char |'\u0000'|
|boolean |false|

引用类型对象的初始值null, 如String默认值。

实例化对象的过程可以分为两部分: 声明对象 `Cat one;` 实例化对象 `new Cat();`

声明对象是在栈空间中进行的，实例化对象是在堆中进行，最后通过赋值运算符`Cat one= new Cat();`将两者绑定。

构造方法:

构造方法与类同名且没有返回值

![](http://myphoto.mtianyan.cn/20180801121724_RCWWF0_Screenshot.jpeg)

只能在对象实例化的时候调用;一个类中可以有多个构造方法-构造方法重载;当没有指定构造方法时,系统会自动添加无参的构造方法;

当有指定构造方法,无论是有参、无参的构造方法都不会自动添加无参的构造方法。建议在添加自定义构造方法的时候也添加一个无参的构造。

带参构造进行实例化时，为了避免赋值错误。

this: 当前对象的默认引用; this的使用:调用成员属性,解决成员属性和局部变量同名冲突。调用成员方法。

**调用重载的构造方法。**只能通过this来调用。

![](http://myphoto.mtianyan.cn/20180801122132_NhqDKI_Screenshot.jpeg)

通过this()调用构造方法,必须放在方法体内第一行。

![](http://myphoto.mtianyan.cn/20180801122224_mvFYRc_Screenshot.jpeg)

在下一集中,面向对象的重要特性-封装,即将粉墨登场,我们会一起来研究,什么是封装以及如何在Java程序中实现封装。





































