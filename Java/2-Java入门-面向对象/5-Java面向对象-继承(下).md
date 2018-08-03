前面我们学习了继承的概念和特点;继承的代码实现;方法重写;访问修饰符的分类及作用;super关键字的使用;继承的初始化顺序

课程简介:

认识继承体系的老祖宗: Object类

当我们不希望某些类被继承，某些方法被重写，某些数据被修订时，final关键字登场。

注解的简介

### Object类介绍

Object类时所有类的父类

```java
class Dog extends Animal{
  
}
```

一个类没有使用extends关键字明确标识继承关系,则默认继承Object类(包括数组);Java中的每个类都可以使用Object中定义的方法;

前往oracle官网查看官方的api文档

https://docs.oracle.com/javase/8/docs/api/

Object类是存放在java.lang这个包里的。这个包里我们之前用到的System String Math等类都在这个包里。这个包是系统默认会为我们直接加载的。

```java
equals(Object obj)
Indicates whether some other object is "equal to" this one.
```

两个对象是否指向同一块内存。object中的equals和双等于是同一个效果，因此经常要被我们重写。

```java
equals(Object anObject)
Compares this string to the specified object.
```

字符串中重写了equals方法，实现了字符串内容的比较。

修改我们的Animal双参构造函数，让其将传入的参数赋给成员变量。

```java
    public Animal(String name,int month)
    {
        this.setName(name);
        this.setMonth(month);
        System.out.println("我是父类的有参构造方法");
    }
```

```java
package cn.mtianyan.inherit;

public class TestThree {
    public static void main(String[] args) {
        Animal one = new Animal("花花",10);
        Animal two = new Animal("花花",10);

        System.out.println(one.equals(two));
    }
}
```

![](http://myphoto.mtianyan.cn/20180803120024_Q4KclD_Screenshot.jpeg)

可以看到即使Animal没有extends任何类，它也能调用Object类的方法，equals();而equals方法没有被重写的时候，就是双等于，是看两个对象是否指向同一块内存。

```java
        System.out.println(one == two);
```

![](http://myphoto.mtianyan.cn/20180803120244_vHw67a_Screenshot.jpeg)

可以看到，Object类中的equals和==是一样的。equals:继承Object中的equals方法时，比较的是两个引用是否指向同一个对象(内存)

```java
        String str1 = new String("hello");
        String str2 = new String("hello");
        System.out.println(str1.equals(str2));
        System.out.println(str1 == str2);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180803120534_k2ha8I_Screenshot.jpeg)

String类型重写了Object类的equals方法。

### Object类介绍中

```java
        Animal one = new Animal("花花",10);
        Animal two = new Animal("花花",10);
```

假如我们的目的是判断这两个对象的值是否相同，该怎么办呢？

>我们需要在Animal类中重写继承自Object类中的equals方法

```java
    // 重写Object中的equals方法
    public boolean equals(Object obj){
        if(obj == null){
            return false;
        }
        Animal temp = (Animal) obj;
        if (this.getName().equals(temp.getName()) && (this.getMonth()==temp.getMonth())){
            return true;
        }else {
            return false;
        }
    }
```

进行强制转换。有可能会出现潜在的异常

```java
        System.out.println(one.equals(two));
        System.out.println(one == two);
```

![](http://myphoto.mtianyan.cn/20180803171117_fe5t5M_Screenshot.jpeg)

```java
    // 重载equals方法
    public boolean equals(Animal obj){
        if(obj == null){
            return false;
        }
        if (this.getName().equals(obj.getName()) && (this.getMonth()==obj.getMonth())){
            return true;
        }else {
            return false;
        }
    }
```

equals测试: 1. 继承Object中的equals方法时，比较的是两个引用是否指向同一个对象;2. 子类可以通过重写equals方法的形式，改变比较的内容。这里equals中的参数为空的判断也是很重要的，否则可能因为传入的值为空，造成程序的异常。

由于通过Animal类型参数重载了equals()所以代码运行时自动定位类型匹配方法

### Object类介绍(下)

Object类中的toString方法是打印出类的字符串形式（类名+@+hash值）。

语句中输出对象名时，默认调用toString方法。

```java
        System.out.println(one.toString());
        System.out.println(one);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180803172317_BJjkgo_Screenshot.jpeg)

可以看到调用toString和直接打印一个类是一样的。输出对象名时，默认会直接调用类中的toString方法。

継承Object中的toString方法吋,输出対象的字符串表示形式:类型信息+@+地址信息

toString方法也经常被我们重写，String类就将这个进行了重写。

```java
        System.out.println(str1.toString());
        System.out.println(str1);
```

子类可以通过重写equals方法的形式，改变输出的内容以及表现形式

![](http://myphoto.mtianyan.cn/20180803205714_u1X4MQ_Screenshot.jpeg)

可以看到str1就本身已经相当于调用了toString方法了，如果再次调用就会提示重复调用。下面我们重写Animal中的toString方法。

```java
    public String toString() {
        return "昵称: " +this.getName()+";年龄: "+this.getMonth();

    }
```

```java
        System.out.println("================");
        System.out.println(one.toString());
        System.out.println(one);
```

![](http://myphoto.mtianyan.cn/20180803210332_h5Rrql_Screenshot.jpeg)

养成良好的查阅文档的习惯。

### final关键字的使用

通过继承关系大大提高了复用性和灵活性，但是有时候我们不希望这个方法被继承，或被重写,值不想它被修改。

```java
public final class Animal // final public class Animal
```

表示Animal这个类是最终的，是不允许有子类的。

![](http://myphoto.mtianyan.cn/20180803214359_VdeIs8_Screenshot.jpeg)

```java
public final class String
extends Object
implements Serializable, Comparable<String>, CharSequence
```

```java
public final class System
extends Object
```

java.lang下的我们用过的包，可以看到String和System都是final修饰的。

一个方法不希望被子类重写，要在返回值之前加final关键字

```java
    // 吃东西
    public final void eat(){
        System.out.println(this.getName()+"在吃东西");
    }
```

![](http://myphoto.mtianyan.cn/20180803215108_TgQeeH_Screenshot.jpeg)

不能被重写，但是子类仍然是可以调用这个方法的(不过用的是父类的实现）

final class: 该类没有子类public final class \ finalpublic class

final方法: 该方法不允许被子类重写，但是可以正常被子类继承使用

final还可以修饰变量。

```java
    public final void eat(){
        int temp =10; // 方法内的局部变量
        System.out.println(this.getName()+"在吃东西");
    }
```

方法内的局部变量作用范围，从该行开始到所在大括号结束。类的成员属性的作用范围取决于它前面的访问修饰符

![](http://myphoto.mtianyan.cn/20180803220240_QGX3G7_Screenshot.jpeg)

可以看到final关键字修饰过后的变量temp是不允许被再次修改的。

final 修饰的局部变量，不需要在定义的同时必须赋值，只要在使用之前赋一次值就可以了。

```java
        final int temp; // 方法内的局部变量
        temp = 12;
```

```java
    public final int temp =150; // 成员属性
```

```java
    public Animal(){
        temp = 20; // 报错
        System.out.println("我是父类的无参构造方法");
    }
```

![](http://myphoto.mtianyan.cn/20180803220652_piWoQY_Screenshot.jpeg)

被final修饰的成员属性如果在定义时没有被赋值，只有两个地方可以进行赋值: 1. 构造方法;2. 构造代码块

类中成员属性:赋值过程: 1. 定义直接初始化; 2. 构造方法; 3. 构造代码块; 三者只可选其一

```java
    public Animal(){
        temp = 10;
        System.out.println("我是父类的无参构造方法");
    }
    public Animal(String name,int month)
    {
        temp = 20;
        this.setName(name);
        this.setMonth(month);
        System.out.println("我是父类的有参构造方法");
    }
```

注意: **有多个构造方法时，final关键字修饰的成员变量需要在多个构造方法内都要进行赋值, 不同构造方法可以赋值不同**

### final 关键字使用(下)

java 数据类型分为基本数据类型 和 引用数据类型

![](http://myphoto.mtianyan.cn/20180803222648_gg19SZ_Screenshot.jpeg)

基本类型的数据是可以进行直接赋值的`int temp=15;`，引用类型的数据需要通过实例化来构造对象`Animal one= new Animal();`。

对于引用数据类型被final修饰后，引用地址是否可以发生改变?属性值是否可以发生改变呢?

```java
        final Animal animal = new Animal("花花",10);
        animal = new Animal(); // 报错
```

![](http://myphoto.mtianyan.cn/20180803223147_k8yK71_Screenshot.jpeg)

引用地址是不可以发生变化的，但是对象的属性值是允许被重新修改的。

```java
        final Animal animal = new Animal("花花",10);
        animal.month = 12;
        animal.name = "哈哈";
```

```java
    public static final int temp; // public final static int temp
    
    static {
        temp = 12;
        System.out.println("我是父类的静态代码块");
    }
```

对于我们的变量而言，如果我们既不希望它在程序中不被修改，同时希望它是作为全局变量来存在的。这种情况下使用static和final同时修饰。此时分步赋值应该在静态代码块中进行。

final:

修饰类表示不允许被继承; 修饰方法表示不允许被子类重写; final修饰的方法可以被继承;不能修饰构造方法

```java
final public Animal() // 报错
```

![](http://myphoto.mtianyan.cn/20180803223906_NdsRoZ_Screenshot.jpeg)

只有public，protected，private可以放在构造方法前面,当然什么都不加的默认情况也是不会报错的

```java
Animal(){}
```

修饰变量表示不允许修改: 

方法内部的局部变量 -> 在使用之前被初始化赋值即可

类中成员变量 -> 只能在定义时、构造方法、构造代码块中进行

基本数据类型的变量 -> 初始赋值之后不能更改;引用类型的变量 -> 初始化之后不能再指向另一个对象,但对象的内容是可变的

可配合static使用: 可以修饰方法和变量。通常应用于: 修饰配置信息(这类只需要加载一次，不需要后期改变的值)，

```java
public static final String MYBLOG = "https://www.jianshu.com/u/db9a7a0daa1f"
```

使用final修饰可以提高性能,但会降低可扩展性

```java
package cn.mtianyan.help;

public class Animal {
    public String name;
    public int month;

    public Animal() {
    }
    public void eat(){
        System.out.println(this.name+"在吃东西");
    }
    public void help(final Animal temp){
//        temp = new Animal(); // 出错
        temp.name = "牛牛";
        temp.eat();
    }
}
```

```java
package cn.mtianyan.help;

public class Test {
    public static void main(String[] args) {
        Animal one = new Animal();
        one.name = "花花";
        Animal two = new Animal();
        two.name = "凡凡";
        one.help(two);
    }
}
```

出错在传入的参数是final修饰的对象，不能重新指向其他对象，但是其内容是可以改变的。

运行结果:

![](http://myphoto.mtianyan.cn/20180803225446_trrY8h_Screenshot.jpeg)

### 注解介绍

之前我们介绍了子类的方法重写需要的条件

方法重写: 1. 有继承关系的子类中;2. 方法名相同,参数列表相同(参数顺序,个数,类型),方法返回值相同;3. 访问修饰符,访问范围需要大于等于父类的访问范围;4. 与方法的参数名无关

快速生成方法重写，并对于是否符合条件进行有效的验证

快捷键 -> ![](http://myphoto.mtianyan.cn/20180803230521_8VHprn_Screenshot.jpeg)

点击想要重写的方法会自动的为你产生:

```java
    @Override
    public void setMonth(int month) {
        super.setMonth(month); // 调用父类的实现方法，一般都会注释掉
    }
```

这个override删除了也没有问题，但是你加在其他不是重写父类方法的就会报错。

![](http://myphoto.mtianyan.cn/20180803230838_gHSMUg_Screenshot.jpeg)

称之为注解: JDK1.5版本引入的一个特性, 可以声明在包、类、属性、方法、局部变量、方法参数等的前面,用来对这些元素进行说明、注释。

注解相当于一种标记，为这个程序添加注解就相当于是打上了某种标记。为方法加上override的注解，就相当于为这个方法打上标签，告诉大家这是重写父类的一个方法。

![](http://myphoto.mtianyan.cn/20180803231105_w61472_Screenshot.jpeg)

>按照运行机制分: 源码注解;编译时注解;运行时注解

源码注解: 注解只在源码中存在,编译成.class文件就不存在了。

编译时注解: 注解在源码和.class文件中都存在。

运行时注解: 在运行阶段还起作用,甚至会影响运行逻辑的注解。比如spring框架，@Autowired依赖注入的这种注解，它实现的就是在程序运行的过程当中自动的将外部传入的信息加载进去,它就是一种可以影响程序运行逻辑的运行时注解。

![](http://myphoto.mtianyan.cn/20180803231643_N3czYp_Screenshot.jpeg)

按照来源来分: 来自JDK的注解; 来自第三方的注解; 我们自己定义的注解

元注解: 对注解进行注解。

```java
    // 父类Animal中
    public Animal create(){
        return new Animal();
    }
    // 子类中重写 可以返回子类类型，但是不可以返回Object类。向下兼容
    @Override
    public Dog create() {
        return new Dog();
    }
```

上述代码是不会报错，可以正常运行的。这说明我们之前要求的重写和父类返回值相同时不严谨的。方法返回值可以从父类类型变为子类类型

这里的兼容问题多态部分我们还会讲的。

#### 编程练习

请使用面向对象的思想,实现杨梅和仙人蕉的信息描述。

程序参考运行效果图如下:

![](http://myphoto.mtianyan.cn/20180803232544_c1xEtt_Screenshot.jpeg)

思路分析:

1. 根据杨梅和香蕉的共性,抽取父类水果(Fruits) 私有属性:水果的形状(shape)和口感(taste) 方法:
  
    - 带参构造函数(参数为shape和taste)
    - 创建无参无返回值得方法eat(描述内容为:水果可供人们食用!)
    - 重写equals方法,比较两个对象是否相等(比较shape,taste)

```java
package cn.mtianyan.fruits;

public class Fruits {
    private String shape;
    private String taste;

    public Fruits(String shape, String taste) {
        this.shape = shape;
        this.taste = taste;
    }
    public void eat(){
        System.out.println("水果可供人们食用!");
    }

    public String getShape() {
        return shape;
    }

    public void setShape(String shape) {
        this.shape = shape;
    }

    public String getTaste() {
        return taste;
    }

    public void setTaste(String taste) {
        this.taste = taste;
    }

    public Fruits() {
    }

    @Override
    public boolean equals(Object object){
        if (object == null){
            return false;
        }
        Fruits temp = (Fruits) object;
        if (this.getShape().equals(temp.getShape()) && this.getTaste().equals(temp.getTaste())){
            return true;
        }else {
            return false;
        }
    }
}
```

```java
package cn.mtianyan.fruits;

public class Banana extends Fruits{
    private String color;

    public Banana(String shape, String taste, String color) {
        super(shape, taste);
        this.color = color;
    }

    public String getColor() {

        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    @Override
    public String toString() {
        return "仙人蕉果形"+getShape()+","+getTaste()+"可供生食。";
    }
}
```

```java
package cn.mtianyan.fruits;

public class Waxberry extends Fruits {
    private String color;

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public Waxberry(String shape, String taste) {
        super(shape, taste);
    }

    public void face(){
        System.out.println("杨梅: "+getColor()+"、"+getShape()+",果味"+getTaste());
    }

    @Override
    public void eat() {
        System.out.println("杨梅"+getTaste()+"，非常好吃！");
    }

    public Waxberry(String shape, String taste, String color) {
        super(shape, taste);
        this.color = color;
    }

    @Override
    public String toString() {
        return "杨梅的信息: 果实为"+getShape()+"、"+getColor()+","+getTaste()+",非常好吃！";
    }
}
```

```java
package cn.mtianyan.fruits;

public class Test {
    public static void main(String[] args) {
        Fruits one = new Fruits("圆","甜");
        Fruits two = new Fruits("圆","甜");
        one.eat();
        System.out.println("fru1和fru2的引用比较: "+one.equals(two));

        System.out.println("---------------------------");
        Waxberry waxberry = new Waxberry("圆形","酸甜适中","紫红色");
        waxberry.face();
        waxberry.eat();
        System.out.println(waxberry);

        System.out.println("---------------------------");
        Banana banana = new Banana("短而稍圆","果肉香甜","黄色");
        System.out.println(banana);
        System.out.println("仙人蕉颜色为"+banana.getColor());
    }
}

```

运行结果:

![](http://myphoto.mtianyan.cn/20180804000811_Zbu7Br_Screenshot.jpeg)

### 总结

Object类: Object类是所有类的父类; Java中的毎个类都可以使用Object中定义的方法: equals / toString 都是经常被重写的方法。

final关键字:

    1. 修饰类表示不允许被继承
    2. 修饰方法表示不允许被子类重写
    3. 修饰变量表示不允许修改

final修饰的方法可以被继承使用的;引用类型的变量:初始化之后不能再指向另一个对象,但指向的对象的内容是可变的

可配合static使用，表示静态的不允许修改的信息，如配置信息

注解:

可以声明在包、类、属性、方法、局部变量、方法参数等的前面,用来对这些元素进行说明、注释。

![](http://myphoto.mtianyan.cn/20180804003436_cAe8AB_Screenshot.jpeg)

返回值类型与父类兼容，并不要求完全相同。

在下一集中,我们将来认识一个常用的设计模式-单例模式。























