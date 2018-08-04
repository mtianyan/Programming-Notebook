多态: 多种形态，面向对象的核心，封装和继承都是为多态而服务的。

位于最后也是最重要的。

本次课程围绕: 什么是多态? 多态在程序设计中的优势? 在Java中如何实现多态?

### 多态的概念

![](http://myphoto.mtianyan.cn/20180804024909_f6NKyM_Screenshot.jpeg)

猫，狗，兔子都会吃，都会叫。但它们吃的东西是不同的，叫声也是不一样的。

敲键盘的f1键，当前位于不同的软件窗口，也会做出不同的反应;同一种行为在不同的对象上作用，会产生不同的结果。

多态意味着允许不同类的对象对同一消息做出不同的响应。

广泛意义分类: 

  - 编译时多态(设计时多态，通过方法重载实现) 编译器在编译状态就可以进行不同行为的区分。
  - 运行时多态 程序运行时动态决定调用哪个方法
  
Java中的多态一般指运行时多态。

实现多态的必要条件: 满足继承关系;父类引用指向子类对象

### 案例场景描述及实体类编写

程序中的继承: 猫，狗都继承动物类 动物都能吃东西(猫狗重载eat:猫吃鱼，狗吃肉）

```java
package cn.mtianyan.poly;

public class Animal {
    private String name;
    private int month;

    public Animal() {
    }

    public Animal(String name, int month) {

        this.name = name;
        this.month = month;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getMonth() {
        return month;
    }

    public void setMonth(int month) {
        this.month = month;
    }

    public void eat(){
        System.out.println("动物都有吃东西的能力");
    }
}
```

```java
package cn.mtianyan.poly;

public class Cat extends Animal{
    private double weight;

    public void run(){
        System.out.println("小猫快乐的奔跑");
    }

    public Cat(String name, int month, double weight) {
        super(name, month);
        this.weight = weight;
    }

    public double getWeight() {
        return weight;
    }

    public void setWeight(double weight) {
        this.weight = weight;
    }

    public Cat() {

    }

    @Override
    public void eat() {
        System.out.println("猫吃鱼~~~");
    }
}
```

```java
package cn.mtianyan.poly;

public class Dog extends Animal{
    private String sex;

    public void sleep(){
        System.out.println("小狗有午睡习惯");
    }

    public Dog() {
    }

    public Dog(String name, int month, String sex) {

        super(name, month);
        this.sex = sex;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    @Override
    public void eat() {
        System.out.println("狗爱吃肉~~~");
    }
}
```

```java
package cn.mtianyan.poly;

public class Test {
    public static void main(String[] args) {
        Animal one = new Animal();
        Animal two = new Cat();
        Animal three = new Dog();

        one.eat();
        two.eat();
        three.eat();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804030818_ILbXiZ_Screenshot.jpeg)

分别调用的是自己的方法，虽然都是Animal类型的引用，但是根据实例化对象的不同，执行不同的具体实现方法。

`Animal two = new Cat()` 将一个子类对象转型为一个父类对象，这叫做向上转型,隐式转型，自动转型。

代码中的具体表现就是: 父类引用指向子类实例,可以调用子类重写父类的方法以及父类派生的方法,无法调用子类独有方法。

子类所自己独有的方法无法调用。

### 向下转型

![](http://myphoto.mtianyan.cn/20180804032430_BaZgL0_Screenshot.jpeg)

向下转型、强制类型转换。子类引用指向父类实例，其实我们之前就用过的，重写Object类的equals方法时，就将父类Object强制转换了。
转换之后可以调用子类特有的方法。

```java
        System.out.println("============");
        Cat temp = (Cat) two;
        temp.eat();
        temp.run();
        temp.getMonth();
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804033318_dDBgcC_Screenshot.jpeg)

```java
        Dog temp2 = (Dog) two;
        temp2.eat();
```

没有运行时，是不会报错的。

```java
Exception in thread "main" java.lang.ClassCastException: cn.mtianyan.poly.Cat cannot be cast to cn.mtianyan.poly.Dog
	at cn.mtianyan.poly.Test.main(Test.java:19)
```

向下转型并不是可以随便转换的，要满足一定的转换条件。

### instanceof 运算符

怎样确定是否满足这个转换条件呢？

![](http://myphoto.mtianyan.cn/20180804033727_p8H2V2_Screenshot.jpeg)

作用: 判断左边对象是否是右边类的实例,如果是就返true;不是就返回false

这个运算符可以用来判断一个对象是否满足某个类的实例特征。

![](http://myphoto.mtianyan.cn/20180804033901_GnfNlj_Screenshot.jpeg)

```java
        System.out.println("============");
        if (two instanceof Cat){
            Cat temp = (Cat) two;
            temp.eat();
            temp.run();
            temp.getMonth();
            System.out.println("two 可以转换为Cat类型");
        }
        if (two instanceof Dog){
            Dog temp2 = (Dog) two;
            temp2.eat();
            System.out.println("two 可以转换为Dog类型");
        }else {
            System.out.println("two 不能转换为Dog类型");
        }
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804034144_u9o4KT_Screenshot.jpeg)

通过instanceof 运算符来提高向下转型的安全性。

```java
        if(two instanceof Animal){
            System.out.println("Animal");
        }
        if (two instanceof Object){
            System.out.println("Object");
        }
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804034431_4flw45_Screenshot.jpeg)

two中是具有Animal的实例特征也具有Object的实例特征的。运算符右侧不管写自己，还是父类，还是爷爷类。返回值都是true

### 类型转换总结

向上转型: 父类引用指向子类对象。也就是小变大。儿子要和爸爸说话得向上抬起头。

向下转型: 子类引用指向父类对象。也就是大变小。爸爸要和儿子说话的向下低下头。

```java
    // Animal类中
    public static void say(){
        System.out.println("动物打招呼");
    }
    
    // Cat类中
    @Override
    public void eat() {
        say();
        System.out.println("猫吃鱼~~~");
    }
```

![](http://myphoto.mtianyan.cn/20180804140332_v4tYqu_Screenshot.jpeg)

可以看到Cat中是可以使用父类的say()方法的。

```java
    public static void say(){
        System.out.println("小猫碰胡须");
    }
```

是允许有和继承自父类的static方法重名的方法存在的。此时可以eat中的say调用的就是类内的该方法

![](http://myphoto.mtianyan.cn/20180804140701_Tq3IJS_Screenshot.jpeg)

但是该方法并不与Animal中的方法构成重写。也就是父类中static修饰的方法允许被子类使用，但是不允许被子类重写。

```java
    @Override // 报错
    public static void say(){
        System.out.println("小猫碰胡须");
    }
```

![](http://myphoto.mtianyan.cn/20180804140935_d3k7zM_Screenshot.jpeg)

Cat中的say方法可以定位为Cat所独有的方法。

注意:父类中的静态方法无法被子类重写，所以向上转型之后，只能调用到父类原有的静态方法。如果此时要用子类中的，只能通过向下转型。

```java
Cat cat = (Cat)two;
cat.say();
```

### 类型转换案例(上)

新建Master类:喂宠物 喂猫咪: 吃完东西后，主人会带着去玩线球;喂狗狗:吃完东西后,主人会带着狗狗去睡觉。

```java
package cn.mtianyan.poly;

public class Master {
    public void feed(Cat cat){
        cat.eat();
        cat.playBall();
    }
    public void feed(Dog dog){
        dog.eat();
        dog.sleep();
    }
}
```

```java
    // Cat中添加playBall();
    public void playBall() {
        System.out.println("玩线球");
    }
```

```java
package cn.mtianyan.poly;

public class MasterTest {
    public static void main(String[] args) {
        Master master = new Master();
        Cat cat = new Cat();
        Dog dog = new Dog();
        master.feed(cat);
        master.feed(dog);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804142658_E9hXqM_Screenshot.jpeg)

这样已经满足了我们上面的需求，可是问题来了如果我们养的动物很多呢？所以说我们得写一大堆方法。

```java
    // 方案二
    public void feed(Animal animal){
        if (animal instanceof Dog){
            Dog dog = (Dog) animal;
            dog.eat();
            dog.sleep();
        }else if (animal instanceof Cat){
            Cat cat = (Cat) animal;
            cat.eat();
            cat.playBall();
        }
    }
```

方案1: 编写方法，传入不同类型的动物，调用各自的方法

方案2: 编写方法传入动物的父类，方法中通过类型转换，调用指定子类的方法。后期在维护中只需要增加新的else if

```java
        Master master = new Master();
        Cat cat = new Cat();
        Dog dog = new Dog();
        master.feed(cat);
        master.feed(dog);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804143512_TvqlBi_Screenshot.jpeg)

可以看到，两种方案的运行结果是一致的。

```java
    public void feed(Animal animal){
        animal.eat();
        if (animal instanceof Dog){
            Dog dog = (Dog) animal;
            dog.sleep();
        }else if (animal instanceof Cat){
            Cat cat = (Cat) animal;
            cat.playBall();
        }
    }
```

可以将其中的eat方法抽取到判断之前,不影响最终的结果。 职责单一原则将吃东西和睡觉觉，玩线球分开。

### 类型转换案例(下)

饲养何种宠物? 空闲时间多:养狗狗; 空闲时间不多:养猫咪

```java
    // Master类中
    public Dog hasManyTime(){
        System.out.println("主人休闲时间比较充足，适合养狗狗");
        return new Dog();
    }
    public Cat hasLittleTime(){
        System.out.println("主人休闲时间比较不足,适合养猫咪");
        return new Cat();
    }
```

```java
        // MasterTest
        System.out.println("===============");
        boolean isManyTime = true;
        Animal temp;
        if (isManyTime){
            temp = master.hasManyTime();
        }else {
            temp = master.hasLittleTime();
        }
        System.out.println(temp);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804144653_i3Yq7v_Screenshot.jpeg)

```java
    public Animal raise(boolean isManyTime){
        if (isManyTime){
            System.out.println("主人休闲时间比较充足，适合养狗狗");
            return new Dog();
        }else {
            System.out.println("主人休闲时间比较不足,适合养猫咪");
            return new Cat();
        }
    }
```

```java
        System.out.println("-------------------");
        isManyTime = false;
        temp = master.raise(isManyTime);
        System.out.println(temp);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804144955_7xAuSV_Screenshot.jpeg)

### 抽象类

```java
Animal pet = new Animal ("花花",2);
pet.eat(;
```

这样的Animal就没有它实际的具体意义，太过宽泛。语法是没有问题，但实例化Pet没有意义.

可不可以直接写出符合程序逻辑的代码? (也就是如何避免这种太宽泛没有实际意义的类被实例化);Java中使用抽象炎,限制实例化

```java
public abstract class Animal{ // abstract public  class Animal
  
}
```

被这个关键字修饰的类被我们称之为抽象类。

![](http://myphoto.mtianyan.cn/20180804145729_IH5YLC_Screenshot.jpeg)

Test中提示我们Animal是一个抽象类，无法被实例化。

```java
Animal two = new Cat();
Animal three = new Dog();
```

如上两句代码是没有问题的，可以通过向上转型，指向子类实例。

应用场景: 某个父类只是知道其子类应该包含怎样的方法,但无法准确知道这些子类如何实现这些方法。

父类中只限制了动物都有吃东西的能力，但每个具体的动物怎么吃，由子类自己决定。

![](http://myphoto.mtianyan.cn/20180804150116_5gSpja_Screenshot.jpeg)

避免子类没有章法的设计随意性，又避免了无意义父类的实例化。

### 抽象方法

在父类中只是为了规定子类拥有该项能力，但具体实现并无意义的方法应该设置为抽象方法。

```java
public abstract void eat();
```

抽象方法是不允许有方法体，连花括号都不能有。此时子类是**必须**实现父类的抽象方法的。

![](http://myphoto.mtianyan.cn/20180804150459_9f5lE1_Screenshot.jpeg)

抽象方法:不允许包含方法体;子类中需要重写父类的抽象方法。假如我在子类中既不想实现该抽象方法，我又不想报错，那么我此时可以把这个子类也加上abstract变成抽象类，然后把实现抽象方法的任务交给孙子辈执行。

为什么要使用抽象方法,抽象类?他们的应用场景和特点是什么?

实际业务中不一定要抽象类，父类中确实有一些方法是为了限制子类必须有这种能力，而且这种能力在每个子类中实现不同。1. 父类中的实现没有意义，2. 你也必须提醒子类是必须要去自己实现自己的这个方法的。

后期子类变多了之后，你新建一个类只要继承了抽象的父类，IDE会自动提醒你实现父类中的抽象方法的。

抽象类 & 抽象方法使用规则:

    1. abstract定 义抽象类
    2. 抽象类不能直接实例化,只能被继承,可以通过向上转型完成对象实例
    3. abstract定义抽象方法 ,不需要具体实现也不能有具体实现，花括号都不能有。
    4. 包含抽象方法的类必须是抽象类。

作为一个抽象类是可以没有抽象方法的。当一个类继承抽象类，是必须实现类中的抽象方法的，如果不重写，可以将该子类也变为抽象类，由孙子类实现。

static final private 是否允许和abstract同时出现的，答案: 这是不允许的。(static final private不能与abstract并存)

>抽象方法是要在子类中进行重写的，所以private只能在当前类被访问，final方法不允许被子类重写，static静态的不允许被子类重写。

#### 编程练习

定义一个抽象类图形Shape类,由该派生出两个子类圆Circle类和矩形Rectangle类。Shape里声明了抽象方法area(),该方法分别在两个子类里得到实现。程序参考运行效果图如下:

![](http://myphoto.mtianyan.cn/20180804154456_VqSXkc_Screenshot.jpeg)

```java
package cn.mtianyan.shape;

public abstract class Shape {
    public abstract double area();
}
```

```java
package cn.mtianyan.shape;

public class Rectangle extends Shape {
    private double length;
    private double width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    public double getLength() {

        return length;
    }

    public void setLength(double length) {
        this.length = length;
    }

    public double getWidth() {
        return width;
    }

    public void setWidth(double width) {
        this.width = width;
    }

    @Override
    public double area() {
        return length*width;
    }
}
```

```java
package cn.mtianyan.shape;

public class Circle extends Shape {
    private double PI = Math.PI;
    private double r;

    public double getR() {
        return r;
    }

    public void setR(double r) {
        this.r = r;
    }

    public Circle(double r) {
        this.r = r;
    }

    @Override
    public double area() {
        return PI*r*r;
    }
}
```

```java
package cn.mtianyan.shape;

public class Test {
    public static void main(String[] args) {
        Circle circle = new Circle(3.5);
        System.out.println("圆的面积为 "+circle.area());
        Rectangle rectangle = new Rectangle(6,5);
        System.out.println("矩形的面积为 " + rectangle.area());
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804155441_GM6WVq_Screenshot.jpeg)

### 问题引发的思考

java中只支持单继承，也就是一个子类只有一个唯一的直接父类（满足A is a B）

![](http://myphoto.mtianyan.cn/20180804155530_D53Uxa_Screenshot.jpeg)

如何解决一个类型中需要兼容多种类型特征的问题？以及多个不同类型具有相同特征的问题呢?

对于手机的发展史这样一个场景我们该如何进行合理的代码实现呢？

```java
package cn.mtianyan.phone;

/**
 * 原始手机
 */
public class Telephone {
    private String brand;
    private int price;

    public Telephone() {
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }

    public void call(){
        System.out.println("手机可以打电话");
    }
}
```

```java
package cn.mtianyan.phone;

public class SecondPhone extends Telephone {
    public void message(){
        System.out.println("手机可以发短信");
    }
}
```

```java
package cn.mtianyan.phone;

public class ThirdPhone extends SecondPhone {
    public void video(){
        System.out.println("手机可以看视频");
    }
    public void music(){
        System.out.println("手机可以听音乐");
    }
}
```

```java
package cn.mtianyan.phone;

public class FourthPhone extends ThirdPhone {
    public void photo(){
        System.out.println("手机可以拍照");
    }
    public void internet(){
        System.out.println("手机可以上网");
    }
    public void game(){
        System.out.println("手机可以玩游戏");
    }
}
```

```java
package cn.mtianyan.phone;

public class PhoneTest {
    public static void main(String[] args) {
        FourthPhone fourthPhone = new FourthPhone();
        fourthPhone.call();
        fourthPhone.message();
        fourthPhone.music();
        fourthPhone.video();
        fourthPhone.internet();
        fourthPhone.photo();
        fourthPhone.game();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804160757_pcti8X_Screenshot.jpeg)

可以看到对于我们目前的需求是可以满足的，但是如果来了一些新的设备。

![](http://myphoto.mtianyan.cn/20180804160852_zJyylL_Screenshot.jpeg)

比如，相机可以拍照，电脑可以看视频、听音乐、打游戏。智能手表也可以打电话，

![](http://myphoto.mtianyan.cn/20180804161013_FV9TxS_Screenshot.jpeg)

它们并不能提取出一个公共的父类。此时我们采取愚蠢的实现就是，每个类硬编码写死自己的能力。

```java
public class Camera {
    public void photo(){
        System.out.println("相机可以拍照");
    }
}
```

虽然不能抽取出一个父类，但是它们之间是有相同的行为能力的联系的，我们是否可以根据这种行为能力进行关联。

Java中通过接口实现行为能力的关联。

### 定义接口并测试

```java
public interface Iphoto {
    public void photo();
}
```

![](http://myphoto.mtianyan.cn/20180804161550_z9xrac_Screenshot.jpeg)

接口抽象方法不允许有方法体。虽然我们没有添加abstract关键字，但是接口中的必然是抽象方法。

```java
public class Camera implements Iphoto{
    @Override
    public void photo() {
        System.out.println("相机可以拍照");
    }
}
```

```java
public class FourthPhone extends ThirdPhone implements Iphoto{
    @Override
    public void photo() {
        System.out.println("手机可以拍照");
    }
}
```

```java
        System.out.println("============");
        Iphoto iphoto = new FourthPhone();
        iphoto.photo();
        iphoto = new Camera();
        iphoto.photo();
```

![](http://myphoto.mtianyan.cn/20180804171754_pAQklk_Screenshot.jpeg)

当通过接口指向具体的实现对象时，只能调用接口中规定的方法，不能调用对象独有的方法。

```java
((FourthPhone) iphoto).game();
```

如果想要使用对象具有的非接口方法，是要进行强制转换的。

### 接口成员: 抽象方法&常量

接口定义了某一批类所需要遵守的规范;接口不关心这些类的内部数据,也不关心这些类里方法实现细节,它只规定这些类里必须提供某些方法。

接口的命名推荐使用I开头,因为接口限定一组规范由具体类实现，通常设置为public和默认。protected是不允许修饰接口的。

```java
package cn.mtianyan.phone;

public interface INet {
    // 接口中抽象方法可以不写abstract关键字
    // 不写public，子类继承也会直接有public修饰符
    public void network();
    void connection();

    // 接口中可以定义常量: 默认会加上public static final
   int TEMP = 20;
}
```

```java
package cn.mtianyan.phone;

public class Computer implements INet {
    @Override
    public void network() {
        System.out.println("电脑可以上网");
    }

    @Override
    public void connection() {
        System.out.println("电脑可以进行连接");
    }
}
```

当类实现接口时，需要去实现接口中的所有抽象方法，否则需要将该类设置为抽象类

```java
        System.out.println("---------------");
        System.out.println(INet.TEMP);
```

![](http://myphoto.mtianyan.cn/20180804173039_owH5QG_Screenshot.jpeg)

```java
package cn.mtianyan.phone;

public class SmartWatch implements INet{

    @Override
    public void network() {
        System.out.println("智能手表可以上网");
    }

    @Override
    public void connection() {
    }
}
```

```java
        System.out.println("---------------");
        System.out.println(INet.TEMP);

        System.out.println("===============");
        INet net = new SmartWatch();
        System.out.println(net.TEMP);
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804185626_OQBzpP_Screenshot.jpeg)

接口中有一个公开的静态的最终的常量等于20，而实现接口的SmartWatch类中如果也定义一个同名常量。

```java
    // SmartWatch中
    public static final int TEMP = 30;
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804190013_DwBKaT_Screenshot.jpeg)

此处打印出来的依然是20，如果接口中和实现类中有同样的信息，当使用接口指向实现类时，该数据成员值为接口中定义的。

```java
        System.out.println("***************");
        SmartWatch smartWatch = new SmartWatch();
        System.out.println(smartWatch.TEMP);
```

使用该实现类的自己的对象当然打印出的是自己里面的成员值30.

![](http://myphoto.mtianyan.cn/20180804190241_aVrscm_Screenshot.jpeg)

### 接口成员: 默认方法 & 静态方法

SmartWatch实现了Inet接口之后，就得被迫实现两个抽象方法network和connection，要么自己变成抽象类(两个方法一个都不要)，要么就必须得把两方法都接收了。我们是否可以选择性的实现一部分对自己有意义的呢？

是否可以像之前类的重写，有一个默认的实现。如果我不需要自定义，也可以保持原样不用管它，只针对性的重写我需要的方法。

JDK1.8之后针对这种需求提供了一种默认方法。

```java
    default void connection(){
        System.out.println("我是接口中的默认连接");
    };
```

default: 默认方法可以带方法体

```java
public class Computer implements INet {
    @Override
    public void network() {
        System.out.println("电脑可以上网");
    }
}
```

此处Computer即使不实现接口类中的connection方法也不会报错。JDK1.8中除了默认方法 还提供静态方法。

```java
    // 静态方法: 也是可以带方法体的。
    static void stop(){
        System.out.println("我是接口中的静态方法");
    }
```

此时Computer中不重写接口中的该方法也不会报错。在调用时:

```java
        System.out.println("===============");
        INet net = new SmartWatch();
        net.connection();
        INet.stop();
```

![](http://myphoto.mtianyan.cn/20180804224633_el5w4w_Screenshot.jpeg)

connection可以通过父类引用调用到该默认方法，stop只能通过INet接口名来调用。

默认方法实际上虽然初始的目的是满足那些不被我们关注的方法实现，但是它也是可以被实现类所重写的。

```java
    @Override
    public void connection() {
        // INet.super.connection(); // 调用接口中默认的方法
        System.out.println("智能手表可以连接");
    }
```

```java
        System.out.println("===============");
        INet net = new SmartWatch();
        net.connection();
        INet.stop();
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804225028_bs1izm_Screenshot.jpeg)

通过INet.只能调用当前接口的静态成员。必须加上super才能访问到INet中定义的方法。

类当中的静态方法只能被子类继承而无法重写，同理接口的实现类也无法重写该静态方法。

default: 默认方法可以带方法体jdk1. 8后新增, 可以在实现类中重写，并可以通过接口的引用调用。

static:静态方法可以带方法体jdk1. 8后新增, 不可以在实现类中重写，可以同接口名调用。

### 关于多接口中重名默认方法处理的解决方案

在Java中, 一个类可以实现多个接口。

```java
public class SmartWatch implements INet, Iphoto{
}
```

```java
        System.out.println("----------------");
        INet net2 = new SmartWatch();
        net2.connection();
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804232155_E3YBft_Screenshot.jpeg)

如果照相能力的接口也定义了默认方法。

```java
public interface Iphoto {
    public void photo();
    default void connection(){
        System.out.println("我是照相接口中的默认连接");
    }
}
```

![](http://myphoto.mtianyan.cn/20180804232422_AhOmer_Screenshot.jpeg)

如果此时的SmartWatch中没有自己的connection方法实现，就会导致报错，两个实现接口中的该方法不知道该用哪一个？

解决方案也很简单，哪个都不用。自己只要拥有自己的connection实现就可以了，会使用自己的。

```java
    @Override
    public void connection() {
        System.out.println("SmartWatch 中的connection");
    }
```

```java
        System.out.println("----------------");
        INet net2 = new SmartWatch();
        net2.connection();
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804232831_fI9FpI_Screenshot.jpeg)

```java
        System.out.println("----------------");
        INet net2 = new SmartWatch();
        net2.connection();

        Iphoto ip2 = new SmartWatch();
        ip2.connection();
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804232933_9gW24Y_Screenshot.jpeg)

子类可以在继承父类的同时实现接口(可以同时实现多个接口)

```java
public class FourthPhone extends ThirdPhone implements Iphoto,INet
```

接口的implements 应该写在继承的后面。

![](http://myphoto.mtianyan.cn/20180804233655_NyjW3B_Screenshot.jpeg)

上面我们说的是一个类实现的两个接口中有同名的默认方法connection，此时我们只需要在该类中重写一个自己的connection实现就行了，那如果如上图所示，除过两个接口，继承过来的父类中也有connection方法。

```java
    public void connection(){
        System.out.println("我是三代手机的连接");
    }
```

在四代手机继承的三代手机类中添加一个connection方法。

此时四代手机即使没有connection方法，也不会报错。

```java
        System.out.println("...............");
        INet net3 = new FourthPhone();
        net3.connection();

        Iphoto ip3 = new FourthPhone();
        ip3.connection();
```

运行结果:

![](http://myphoto.mtianyan.cn/20180804234512_3ik8Ow_Screenshot.jpeg)

此时的情况是，父类中有connection方法，实现的两个接口中也有默认的connection方法（不是默认的connection，也不会报错接口方法未实现）。可以看到此时以父类的connection方法为准。

而当四代手机中自己也有了connection方法之后，

```java
    @Override
    public void connection() {
        System.out.println("我是四代手机中的connection");
    }
```

```java
        System.out.println("...............");
        INet net3 = new FourthPhone();
        net3.connection();

        Iphoto ip3 = new FourthPhone();
        ip3.connection();
```

此时调用的就是四代机自己的connection方法。

![](http://myphoto.mtianyan.cn/20180804234958_d6Zpa7_Screenshot.jpeg)

### 关于多接口中重名常量处理的解决方案

```java
package cn.mtianyan.phone;

interface One{
    static int x=11;
}
interface Two{
    final int x=22;
}
public class VarDemo implements One,Two{
    public void test(){
        // System.out.println(x); //报错
        System.out.println(One.x);
        System.out.println(Two.x);
    }
    public static void main(String[] args) {
        new VarDemo().test();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805000837_A0qUAD_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180805000902_SI8KxQ_Screenshot.jpeg)

直接使用x会提示，匹配的x值有两个不知道取哪一个。

```java
package cn.mtianyan.phone;

interface One{
    static int x=11;
}
interface Two{
    final int x=22;
}
class Three{
    public static int x=33;
}
public class VarDemo extends Three implements One,Two{
    public void test(){
//        System.out.println(x); //报错
        System.out.println(One.x);
        System.out.println(Two.x);
        // System.out.println(x); // 继承three依然报错
        System.out.println(Three.x);
    }
    public static void main(String[] args) {
        new VarDemo().test();
    }
}
```

此时即使继承了Three，并不能像上节方法中以父类的方法优先那样不再报错。而是依然提示多个匹配，不知道该用哪个。

运行结果:

![](http://myphoto.mtianyan.cn/20180805001419_lidz9e_Screenshot.jpeg)

```java
public class VarDemo extends Three implements One,Two{
    public int x=44;
    public void test(){
//        System.out.println(x); //报错
        System.out.println(One.x);
        System.out.println(Two.x);
        // System.out.println(x); // 继承three依然报错
        System.out.println(Three.x);
        System.out.println(x);
    }
    public static void main(String[] args) {
        new VarDemo().test();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805001519_HrVW3Y_Screenshot.jpeg)

只有在类中自己定义了x常量，才能直接通过x访问到值。也就是父类的常量并不像方法那样具有其较高的优先级。

```java
package cn.mtianyan.phone;

interface IA{
    int TEMP =10;
}
interface IB extends IA{
    String TEMP = "temp";
}

public class TempTest implements IA,IB{
    public static void main(String[] args) {
        IA a = new TempTest();
        IB b = new TempTest();
        System.out.print(a.TEMP);
        System.out.println(b.TEMP);
    }
}
```

接口之间也可以进行继承。父类的变量并不会优先于接口本身。

![](http://myphoto.mtianyan.cn/20180805002412_n5JxrU_Screenshot.jpeg)

### 接口的继承

接口也可以实现继承，并且可以继承多个父接口。定义一个接口的父类IFather接口。

```java
package cn.mtianyan.phone;

public interface IFather {
    void say();
}
```

```java
package cn.mtianyan.phone;

public interface IFather2 {
    void fly();
}
```

```java
package cn.mtianyan.phone;

public interface ISon extends IFather,IFather2 {
    void run();
}
```

```java
package cn.mtianyan.phone;

public class InterfaceInheritDemo implements ISon {
    @Override
    public void run() {

    }

    @Override
    public void say() {

    }

    @Override
    public void fly() {

    }
}
```

假如此时Ison中继承的两个父接口中都有一个默认的connection方法实现。

```java
package cn.mtianyan.phone;

public interface IFather {
    void say();

    default void connection(){
        System.out.println("IFather中的connection");
    }
}
```

```java
package cn.mtianyan.phone;

public interface IFather2 {
    void fly();
    default void connection(){
        System.out.println("IFather2中的connection");
    }
}
```

此时作为ISon已经傻了，两个爹都有一个默认方法，算了两个都别要，创建一个自己的connection方法。

```java
package cn.mtianyan.phone;

public interface ISon extends IFather,IFather2 {
    void run();

    @Override
    default void say() {

    }

    @Override
    default void connection() {
        
    }

    @Override
    default void fly() {

    }
}
```

#### 编程练习

使用接口的知识，定义接口IFly,创建三个类Plane类、Bird类、Balloon类 ,分別重写接口中的fly()方法，然后再测试类中进行调用。

程序运行参考效果如图所示:

![](http://myphoto.mtianyan.cn/20180805012913_71hpwW_Screenshot.jpeg)

```java
package cn.mtianyan.bird;

public interface IFly {
    void fly();
}
```

```java
package cn.mtianyan.bird;

public class Plane implements IFly {
    @Override
    public void fly() {
        System.out.println("飞机在天上飞");
    }
}
```

```java
package cn.mtianyan.bird;

public class Bird implements IFly {
    @Override
    public void fly() {
        System.out.println("小鸟在天空翱翔");
    }
}
```

```java
package cn.mtianyan.bird;

public class Balloon implements IFly {
    @Override
    public void fly() {
        System.out.println("气球飞上天空");
    }
}
```

```java
package cn.mtianyan.bird;

public class Test {
    public static void main(String[] args) {
        IFly plane = new Plane();
        plane.fly();
        IFly bird = new Bird();
        bird.fly();
        Balloon balloon = new Balloon();
        balloon.fly();

    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805013341_4hRaYA_Screenshot.jpeg)

### 内部类概述

在Java中,可以将一个类定义在另一个类里面或者一个方法里面,这样的类称为内部类;与之对应,包含内部类的类被称为外部类。

```java
// 外部类:人
public class Person{
  int age;//年龄
  public Heart getHeart(){
      return new Heart();
  }
  //内部类:心脏
  class Heart{
    public String beat(){
      return "心脏在跳动";
    }
  }
}
```

为什么要将一个类定义在另一个类里面呢?

>内部类隐藏在外部类之内,更好的实现了信息隐藏。

内部类的分类:

    - 成员内部类
    - 静态内部类
    - 方法内部类
    - 匿名内部类
  
### 成员内部类

内部类中最常见的就是成员内部类,也称为普通内部类。

```java
// 外部类:人
public class Person{
  int age;//年龄
  public Heart getHeart(){
      return new Heart();
  }
  //内部类:心脏
  class Heart{
    public String beat(){
      return "心脏在跳动";
    }
  }
}
```

这就是一个成员内部类的代码，Heart直接定义在了Person的内部。

```java
package cn.mtianyan.people;

// 外部类:人
public class Person{
    int age;//年龄

    public Heart getHeart(){
        return new Heart();
    }

    //内部类:心脏（成员内部类）
    class Heart{
        public String beat(){
            return "心脏在跳动";
        }
    }
}
```

```java
package cn.mtianyan.people;

public class PersonTest {
    public static void main(String[] args) {
        Person person = new Person();
        person.age = 12;

        // 获取内部类对象实例，方式1: new 外部类.new 内部类
        Person.Heart heart1 = new Person().new Heart();
        System.out.println(heart1.beat());

        // 获取内部类对象实例，方式2: 外部类对象.new 内部类
        Person.Heart heart2 = person.new Heart();
        System.out.println(heart2.beat());

        // 获取内部类对象实例，方式3: 外部类对象.获取内部类方法(返回值为内部类对象)
        Person.Heart heart3 = person.getHeart();
        System.out.println(heart3.beat());
    }
}
```

可以看到三种获取内部类实例对象的方法，注意第三种是因为我们的编程习惯，为内部类准备一个get方法。

![](http://myphoto.mtianyan.cn/20180805014959_xJFQaL_Screenshot.jpeg)

内部类的访问修饰符，可以任意，但是访问范围会受到影响.比如Heart什么都不加是默认等级是不支持跨包调用内部类的。

内部类可以直接使用外部类的成员属性和成员方法的。

```java
package cn.mtianyan.people;

// 外部类:人
public class Person{
    int age;//年龄

    public Heart getHeart(){
        return new Heart();
    }
    public void eat(){
        System.out.println("人会吃东西");
    }

    //内部类:心脏（成员内部类）
    class Heart{
        public String beat(){
            eat();
            return age+"岁的心脏在跳动";
        }
    }
}
```

![](http://myphoto.mtianyan.cn/20180805015159_47B2rR_Screenshot.jpeg)

0岁是因为我们的new Person()之后没有对于age进行赋值。

假设我们的Heart内部类中有一个和外部类同名的属性age

```java
    //内部类:心脏（成员内部类）
    class Heart{
        int age = 99;
        public String beat(){
            eat();
            return age+"岁的心脏在跳动";
        }
    }
```

运行结果：

![](http://myphoto.mtianyan.cn/20180805015400_oXX1a5_Screenshot.jpeg)

可以看到，内部类自身的属性值优先级最高。内部类可以直接访问外部类的成员;如果出现同名属性，优先访问内部类中定义的

问题来了，如果我此时就想访问外部类当中的这个该怎么办？

```java
    //内部类:心脏（成员内部类）
    class Heart{
        int age = 99;
        public String beat(){
            eat();
            return Person.this.age+"岁的心脏在跳动";
        }
    }
```

Person.this.age 访问Person类对象的成员属性。可以使用外部类.this.成员的方式，访问外部类中同名的信息

![](http://myphoto.mtianyan.cn/20180805015943_p6Fg4W_Screenshot.jpeg)

在Eclipse中，内部类会被编译为Person$Heart的class文件。而IDEA中则不会。

外部类中想要使用内部类的属性，是要先实例化出内部类的对象才能访问其属性。

```java
package cn.mtianyan.people;

// 外部类:人
public class Person{
    int age;//年龄

    public Heart getHeart(){
        new Heart().temp = 13;
        return new Heart();
    }
    public void eat(){
        System.out.println("人会吃东西");
    }

    //内部类:心脏（成员内部类）
    class Heart{
        int age = 99;
        int temp = 12;
        public String beat(){
            eat();
            return Person.this.age+"岁的心脏在跳动";
        }
    }
}
```

外部类访问内部类信息，需要通过内部类实例，无法直接访问。内部类编译后. class文件命名:外部类$内部类.class(Eclipse中)

思考问题: 内部类中是否可以包含与外部类相同方法签名的方法？如果不报错，内部类方法中调用的eat谁更优先。

```java
package cn.mtianyan.people;

// 外部类:人
public class Person{
    int age;//年龄

    public Heart getHeart(){
        new Heart().temp = 13;
        return new Heart();
    }
    public void eat(){
        System.out.println("人会吃东西");
    }

    //内部类:心脏（成员内部类）
    class Heart{
        public void eat(){
            System.out.println("心脏会吃空气");
        }
        int age = 99;
        int temp = 12;
        public String beat(){
            eat();
            return Person.this.age+"岁的心脏在跳动";
        }
    }
}
```

>答案是可以包含，不报错，其中当然是内部类自己的eat方法更优先。

运行结果:

![](http://myphoto.mtianyan.cn/20180805020711_DTOus3_Screenshot.jpeg)

此时如果我们想调用外部类的eat()

```java
        public String beat(){
            Person.this.eat();
            return Person.this.age+"岁的心脏在跳动";
        }
```

![](http://myphoto.mtianyan.cn/20180805021525_EI1Tze_Screenshot.jpeg)

### 静态内部类 

看到名字我们就应该知道这是由static修饰的内部类。回顾一下我们前面讲过的静态成员的特点: **类共享的**

静态内部类对象可以不依赖于外部类对象,直接创建

```java
    //内部类:心脏（静态内部类）
    static class Heart{

        int age = 99;
        int temp = 12;
        public String beat(){
            // eat();  // 要搭配外部类是static修饰的eat
            new Person().eat();
            // Person.this.eat();
            return Person.this.age+"岁的心脏在跳动"; // 报错
        }
    }
```

静态内部类中，只能直接访问外部类的静态方法，如果需要调用非静态方法，可以通过对象实例

```java
return new Person().age+"岁的心脏在跳动";
```

如果需要调用非静态成员（包括方法和属性），可以通过对象实例

```java
        // 获取内部类对象实例，方式3: 外部类对象.获取内部类方法(返回值为内部类对象)
        Person.Heart heart3 = person.getHeart();
        System.out.println(heart3.beat());

        // 获取静态内部类对象实例
        Person.Heart myStaticHeart = new Person.Heart();
        System.out.println(myStaticHeart.beat());
```

对于静态内部类而言，上面这两种方法都是可以进行实例化的，这里我们可以看到getHeart的好处。即使内部类从成员内部类变成了静态内部类，仍然是可以正常工作的。

静态内部类中添加静态的成员属性和静态的方法是没有问题的。

```java
        // 静态内部类中的静态成员
        public static int age = 13;
        public static void say(){
            System.out.println("hello");
        }
```

```java
        System.out.println("--------------");
        System.out.println(Person.Heart.age);
        Person.Heart.say();
```

![](http://myphoto.mtianyan.cn/20180805023223_gZ5Ez7_Screenshot.jpeg)

静态内部类对象实例化时，可以不依赖于外部类对象;可以通过外部类.内部类.静态成员的方式，访问内部类中的静态成员

想要访问外部类的成员属性，如果该外部类属性不是静态的，要通过实例化外部类对象.属性访问，如果是静态的，只需要外部类.属性就可以。

```java
return new Person().age+"岁的心脏在跳动"; // 非静态
return Person.age+"岁的心脏在跳动"; // 静态
```

当内部类属性与外部类属性同名时，默认直接调用内部类中的成员;如果需要访问外部类中的静态属性，则可以通过`外部类.属性`的方式;
如果需要访问外部类中的非静态属性，则可以通过new 外部类().属性的方式;

### 方法内部类

定义在外部类方法中的内部类,也称局部内部类。既然定义在方法里，就可以按照方法内成员的使用规则来使用。

方法内定义的局部变量只能在方法里使用; 方法内不能定义静态成员; 不能通过public,private,protected进行访问修饰符的限定。

![](http://myphoto.mtianyan.cn/20180805024753_bqlsAV_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180805024937_0noZPO_Screenshot.jpeg)

可以看到提示: 方法内部类是不可以包含静态方法成员的。

```java
package cn.mtianyan.people;

// 外部类:人
public class Person{
    int age;//年龄

    public Object getHeart(){
        //内部类:心脏（方法内部类）
        class Heart{

            int temp = 12;
            public  int age = 13;
            public  void say(){
                System.out.println("hello");
            }
            public String beat(){
                // eat();  // 要搭配外部类是static修饰的eat
                new Person().eat();
                // Person.this.eat();
                return new Person().age+"岁的心脏在跳动";
            }
        }
        return new Heart().beat();
    }
    
    public void eat(){
        System.out.println("人会吃东西");
    }
}
```

```java
        Person person1 = new Person();
        System.out.println(person1.getHeart());
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805025451_pJ50DD_Screenshot.jpeg)

因为这个类在方法内部，所以即使返回了该类的对象，在方法之外也无法调用它的方法。所以一般直接返回该类的方法。

![](http://myphoto.mtianyan.cn/20180805025657_newWJY_Screenshot.jpeg)

方法内部类编译后生成的class文件。此处纠正前面说的Eclipse中没有生成文件的错误。是生成了的，要打开文件夹查看，而不是IDE中查看。

方法内部类:

    - 定义在方法内部，作用范围也在方法内
    - 和方法内部成员使用规则一样，class前面不可以添加public、private、protected. static
    - 类中不能包含静态成员
    - 类中可以包含final、abstract修饰的成员

### 匿名内部类(上)

匿名内部类就是没有名字，隐藏名字的意思。

之前我们使用类与对象都是如下：

```java
class类名{
}

类名 对象名 = new 构造方法();
```

但有时候在程序中我们对于某个类的实例只会使用一次，此时这个类的名字对于整个程序是可有可无的。

此时我们可以将类的定义与类的创建，放到一起完成,简化程序的编写。

通常使用匿名内部类简化对于接口实现和抽象类的操作。

```java
package cn.mtianyan.anonymous;

public abstract class Person {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Person() {

    }

    public abstract void read();
}
```

```java
package cn.mtianyan.anonymous;

public class Man extends Person {
    @Override
    public void read() {
        System.out.println("男生喜欢看科幻书籍");
    }
}
```

```java
package cn.mtianyan.anonymous;

public class Women extends Person{
    @Override
    public void read() {
        System.out.println("女生喜欢言情小说");
    }
}
```

```java
package cn.mtianyan.anonymous;

public class Test {
    // 根据传入的不同的人的类型，调用对应的read方法

    // 方案1:
    public void getRead(Man man){
        man.read();
    }
    public void getRead(Women women){
        women.read();
    }

    public static void main(String[] args) {
        Test test = new Test();
        Man one = new Man();
        Women two = new Women();

        test.getRead(one);
        test.getRead(two);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805031241_m19UrC_Screenshot.jpeg)

```java
    // 方案2:
    public void getRead(Person person){
        person.read();
    }
```

此时将方案一注释掉，方案2也是可以正常运行的。运行结果:

![](http://myphoto.mtianyan.cn/20180805031417_PvzYbw_Screenshot.jpeg)

开始启用匿名内部类实现，将Man和Women中的类定义都注释掉。将main方法中原来的注释掉。

```java
package cn.mtianyan.anonymous;

public class Test {

    public void getRead(Person person){
        person.read();
    }

    public static void main(String[] args) {

        Test test = new Test();
        test.getRead(new Person() {
            @Override
            public void read() {
                System.out.println("男生喜欢看科幻类书籍");
            }
        });
    }
}
```

![](http://myphoto.mtianyan.cn/20180805031953_pM0Ufp_Screenshot.jpeg)

在实例化对象的同时完成对象方法的编写。没有名字包括没有类名，以及实例名。

### 匿名内部类(下)

![](http://myphoto.mtianyan.cn/20180805032340_ypfhNd_Screenshot.jpeg)

可以看到匿名内部类编译过后的class文件。

    - 匿名内部类没有类型名称、实例对象名称;
    - 编译后的文件命名:外部类$数字. class;
    - 无法使用private、public、protected. abstract、 static修饰。既然无法使用这些修饰，当然也是不允许有抽象方法的。
    - 无法编写构造方法 (匿名内部类中初始化可以使用构造代码块)
    - 不能出现静态成员
    - 匿名内部类可以实现接口也可以继承父类，但是不可兼得
    
    ![](http://myphoto.mtianyan.cn/20180805033742_pWYBRj_Screenshot.jpeg)

#### 编程练习

分别通过成员内部类、方法内部类、匿名内部类完成接口Ball ,在测试类BallTest中的调用。

程序参考运行效果图如下:

![](http://myphoto.mtianyan.cn/20180805034053_oWanba_Screenshot.jpeg)

```java
package cn.mtianyan.ball;

public interface Ball {
    void play();
}
```

```java
package cn.mtianyan.ball;

public class BallTest {
    void playBall(){
        class Inner_f implements Ball{

            @Override
            public void play() {
                System.out.println("方法内部类：");
                System.out.println("打乒乓球");
                System.out.println("**********");
            }
        }
        new Inner_f().play();
    }
    // 成员内部类
    class Inner_m implements Ball {

        @Override
        public void play() {
            System.out.println("成员内部类:");
            System.out.println("打篮球");
            System.out.println("**********");
        }
    }
}
```

```java
package cn.mtianyan.ball;

public class Test {
    void playBall(Ball ball){
        ball.play();
    }
    public static void main(String[] args) {
        BallTest.Inner_m one = new BallTest().new Inner_m();
        one.play();
        BallTest ballTest = new BallTest();
        ballTest.playBall();
        Test test = new Test();
        test.playBall(new Ball() {
            @Override
            public void play() {
                System.out.println("匿名内部类:");
                System.out.println("打排球");
            }
        });
    }

}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180805035609_3DfLBk_Screenshot.jpeg)

### 总结

多态的分类:

  1. 编译时多态(设计时多态) : 方法重载。
  2. 运行时多态: JAVA运行时系统根据调用该方法的实例的类型来决定选择调用哪个方法则被称为运行时多态。

我们平时说得多态,多指运行时多态

向上类型转换( Upcast) : 将子类型转换为父类型。 隐式/自动类型转换,是小类型到大类型的转换

向下类型转换( Downcast) : 将父类型转换为子类型。强制类型转换,是大类型到小类型

通过instanceof运算符,来解决引用对象的类型,避免类型转换的安全性问题,提高代码的强壮性。

抽象类应用场景:

>某个父类只是限定其子类应该包含怎样的方法,但不需要准确知道这些子类如何实现这些方法。

Java中使用抽象类,限制实例化:

```java
public abstract class Animal{
}
```

abstract也可用于方法一抽象方法

```java
public abstract void eat();
```

注意:
    1、抽象类不能直接实例化
    2、子类如果没有重写父类所有的抽象方法,则也要定义为抽象类
    3、抽象方法所在的类一定是抽象类
    4、抽象类中可以没有抽象方法
    
接口:

接口定义了某一批类所需要遵守的规范;接口不关心这些类的内部数据,也不关心这些类里方法的实现细节,它只规定这些类里必须提供某些方法

```java
语法: [修饰符] interface 接口名 [ extends 父接口1,父接口2 ...]
{
  零个到多个常量定义...
  零个到多个抽象方法的定义...
  零个到多个默认方法的定义... ( jdk1.8新增) // 
  零个到多个静态方法方法的定义... ( jdk1.8新增)// 后两种允许有方法体
}
```

接口可以实现多继承，即一个子接口可以同时继承多个父接口;实现接口的类如果不能实现所有接口中待重写的方法,则必须设置为抽象类

一个类可以继承自一个父类,同时实现多个接口

内部类:

在Java中,可以将一个类定义在另一个类里面或者一个方法里面,这样的类称为内部类;与之对应,包含内部类的类被称为外部类。

内部类的分类: 成员内部类;静态内部类;方法内部类;匿名内部类

优势: 内部类提供了更好的封装,可以把内部类隐藏在外部类之内,不允许同一个包中的其他类访问该类,更好的实现了信息隐藏。

注意内部类的访问规则，尤其是匿名内部类的写法。

在下一集中,将带领大家一起来认识一下什么是异常以及在Java中如何进行合理的异常处理。

































































































