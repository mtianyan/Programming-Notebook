面向对象的三大特征: 继承，封装，多态。

封装:

将类的某些信息隐藏在类内部, 不允许外部程序直接访问;通过该类提供的方法来实现对隐藏信息的操作和访问;

隐藏对象的信息 同时 留出访问的接口

生活中的案例:

ATM机，我们可以通过它存取款、转账、余额查询操作。钞票是ATM内的重要信息，但我们在外部是无法直接看到的，这就是ATM机对于钞票这个重要信息的隐藏。但是ATM拥有操作屏, 插卡口,取钞口等，用户通过简单的操作就可以实现隐藏钞票的操作。

特点:

  1. 只能通过规定的方法访问数据
  2. 隐藏类的实例细节,方便修改和实现

### 封装的代码实现(上)

private 加在属性上，表明这个属性只能在当前类内被访问。

实现步骤: 修改属性的可见性,设为private; 创建getter/setter方法，设为public，用于属性的读写;在getter/setter方法中加入属性控制语句(对属性值的合法性进行判断:性别只能是男和女啊，年龄只能是正值啊)

宠物猫的年龄应该是正数。

1. 修改属性的可见性

```java
    private String name;
    private int age;
    private float weight;
    private String species;
```

private表示这个属性只能在Cat类内部进行访问。

![](http://myphoto.mtianyan.cn/20180801150348_IuNL8y_Screenshot.jpeg)

可以看到此时这些属性已经无法再类外直接通过对象进行访问了。

访问修饰符: private public
  1. 还有什么呢?
  2. 访问权限是怎样的?

2. 设置公有的getter/setter方法隐藏; 在get/set方法中添加对属性的限定。

```java
public String getName() {
        return name;
    }

public void setName(String name) {
        this.name = name;
    }
```

可以通过快捷键: ![](http://myphoto.mtianyan.cn/20180801150755_foT1F0_Screenshot.jpeg) 进行快速的生成。

```java
public String getName() {
        return "我是一只名叫"+name+"小猫";
    }
```

里面可以加入自己的一些逻辑，包装。下面是封装之后的使用:

```java
        Cat oneCat = new Cat();
        oneCat.setAge(10);
        oneCat.setName("花花");
        oneCat.setSpecies("中华田园猫");
        oneCat.setWeight(1000);

        System.out.println("年龄: "+ oneCat.getAge());
        System.out.println("昵称: "+ oneCat.getName());
        System.out.println("体重: " + oneCat.getWeight());
        System.out.println("品种: " + oneCat.getSpecies());
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801151637_KmcJDc_Screenshot.jpeg)

### 封装代码实现下

注意只有getXXX方法的属性是只读属性;只有setXXX方法的属性是只写属性。下面我们在set方法中加入一些验证

```java
    public void setAge(int age) {
        if (age <0){
            System.out.println("猫的年龄必须大于0");
        }else{
            this.age = age;
        }
    }
  
  // 调用
  oneCat.setAge(-1);
```

![](http://myphoto.mtianyan.cn/20180801152417_Bbvc8D_Screenshot.jpeg)

可以通过异常处理优化程序,后面会详细介绍。如果在构造函数中不使用get set 而是直接赋值，可以正常运行，但是不推荐。因为写在get/set里的验证逻辑将不会被执行。

```java
public Cat(int age){
  this.age = age;
}

Cat oneCat = new Cat(-1);
System.out.println("年龄: "+ oneCat.getAge());
```

![](http://myphoto.mtianyan.cn/20180801152949_yFz1Eo_Screenshot.jpeg)

**因此推荐在构造方法中也同样使用get/set**

#### 编程练习

编写自定义类实现图书信息设置，运行参考效果如下所示:

![](http://myphoto.mtianyan.cn/20180801153232_PpIYGs_Screenshot.jpeg)

属性: 书名、作者、出版社、价格
方法: 信息介绍

```java
package cn.mtianyan.book;

public class Book {
    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getPulishingHouse() {
        return pulishingHouse;
    }

    public void setPulishingHouse(String pulishingHouse) {
        this.pulishingHouse = pulishingHouse;
    }

    public float getPrice() {
        return price;
    }

    public void setPrice(float price) {
        if(price < 10){
            System.out.println("图书价格最低10元");
            this.price =10;
        }else{
            this.price = price;
        }
    }

    private String title;
    private String author;
    private String pulishingHouse;
    private float price;

    public Book(String title,String author,String pulishingHouse,float price){
        this.setTitle(title);
        this.setAuthor(author);
        this.setPulishingHouse(pulishingHouse);
        this.setPrice(price);
    }
    public void info(){
        System.out.println("书名: " + this.getTitle());
        System.out.println("作者: " + this.getAuthor());
        System.out.println("出版社: " + this.getPulishingHouse());
        System.out.println("价格: " + this.getPrice());
    }
}
```

```java
package cn.mtianyan.book;

public class BookTest {
    public static void main(String[] args) {
        Book one = new Book("红楼梦","曹雪芹","人民文学出版社",6);
        Book two = new Book("小李飞刀","古龙","中国长安出版社",55.5f);
        one.info();
        System.out.println("===================");
        two.info();
    }
}
```

![](http://myphoto.mtianyan.cn/20180801154808_FUCuI4_Screenshot.jpeg)

### 使用包进行类管理

文件夹进行文件管理，同一个文件中可以存放多个不同的文件，同名的文件只能存放在不同的文件夹中。

在Java中如何进行不同类文件的管理呢：java中我们通过包来管理java文件，解决同名文件冲突。

Java中一个包里不能存在同名类

![](http://myphoto.mtianyan.cn/20180801171422_svdM0i_Screenshot.jpeg)

 域名倒序+模块+功能(域名全部小写)

```java
package cn.mtianyan.book;
```

包的定义必须放在Java源文件中的第一行，定义类时，我们应该遵循单一职责原则，因此在建立包的时候，建议每个包内存储信息功能单一。

如何实现跨包的类调用?有几种调用形式?我如何告诉编译器我要调用的是哪个包里的Cat呢?

```java
import cn.mtianyan.animal.*; // 加载包下的所有类
import cn.mtianyan.animal.cat; // 加载指定包下的指定类
```

建议采用 `import包名.类名` 的方式加载,提高效率

可以直接在程序代码中加载`cn.mtianyan.animal.cat`

```java
 cn.mtianyan.animal.Cat cat = new cn.mtianyan.animal.Cat();
```

加载类的顺序跟import导入语句的位置无关,具体包的指定，优先级大于通配符。

```java
import cn.mtianyan.*
```

`import包名.*` 只能访问指定包名下的类，无法访问子包下的类

包的作用:

  1. 管理Java文件
  2. 解决同名文件冲突

定义包:
  
  语法: package 包名;例: package cn.mtianyan.animal;

注意: 必须放在Java源文件中的第一行;-个Java源文件中只能有-个package语句;包名全部英文小写;命名方式:域名倒序+模块+功能

导入包语法:

import 包名.类名;

例:导入包中全部类: import cn.mtianyan.*;导入包中指定类: import cn.mtianyan.animal.Cat;

tips(常用系统包):

|包名| 内容|
|----|-----|
|java.lang| 包含Java语言基础的类,该包系统加载时默认导入 如:System、String、Math|
|java.util| 包含Java语言中常用工具 如: Scanner、Random|
|java.io| 包含输入、输出相关功能的类 如: File、InputStream|

#### 编程练习

编写自定义类实现用户信息类.

程序参考运行效果图如下:

![](http://myphoto.mtianyan.cn/20180801173658_yqA00J_Screenshot.jpeg)

任务

用户类: 属性(用户名、密码)
用户管理类: 方法(用户信息验证)

```java
package cn.mtianyan.user;

public class User {
    private String username;

    public User(String username, String password) {
        this.setUsername(username);
        this.setPassword(password);
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    private String password;
}
```

```java
package cn.mtianyan.user;

public class UserManage {
    public String checkUser(User one,User two){
        System.out.println("用户名: "+one.getUsername());
        System.out.println("密码: "+one.getPassword());
        System.out.println("用户名: "+two.getUsername());
        System.out.println("密码: "+two.getPassword());
        System.out.println("=================");
        if (one.getUsername().equals(two.getUsername())){
            return  "用户名一致";
        }else {
            return  "用户名不一致";
        }
    }
}
```

```java
package cn.mtianyan.user;

public class Test {
    public static void main(String[] args) {
        User one = new User("Lucy","123456");
        User two = new User("Mike","123456");
        UserManage userManage = new UserManage();
        System.out.println(userManage.checkUser(one,two));
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801175012_nV0s1q_Screenshot.jpeg)

### Static关键字（上）

![](http://myphoto.mtianyan.cn/20180801175056_cZuD35_Screenshot.jpeg)

static表示静态信息，它在Java程序中可以和喞些信息組合使用?用它修饰的信息具有哪些特征呢?

```java
public float price; //cat类中
```

```java
Cat one = new Cat();
one.price = 2000;

Cat two = new Cat();
two.price = 150;
```

上述代码的结果显然脑补都可以脑补到.但假如我们为价格添上static修饰

```java
public static int price; //售价
```

![](http://myphoto.mtianyan.cn/20180801175644_iFjEHz_Screenshot.jpeg) 

添加了static修饰之后，price变成了斜体。

![](http://myphoto.mtianyan.cn/20180801175837_ddMw5l_Screenshot.jpeg)

可以看到在main中取值时，提示我们静态的成员变量，应该以一种静态的访问方式访问。此时的运行结果中，两只猫的价格都变成了150。

Static表示的是一个静态的，修饰成员时叫做一个静态成员或类成员，它是属于这个类所有的。无论这个类实例化出多少的对象，它都会共用同一块内存空间。

![](http://myphoto.mtianyan.cn/20180801180156_R60V5c_Screenshot.jpeg)

后赋值的会将前面的内存中的内容覆盖掉; 类对象共享;类加载时产生,销毁时释放，生命周期长

```java
one.price = 2000;
Cat.price = 3000;
```

既可以通过对象名，也可以通过类名来访问。

### Static关键字中

Static 加在属性前面，被称为静态属性，类属性。同理，Static添加到方法前面就从普通方法，变成了类方法。

```java
public static void eat(){
        System.out.println("小猫吃鱼");
}
```

类方法的调用和我们的静态成员变量的访问时一样的，既可以通过类，也可以通过对象。

```java
        oneCat.eat();
        Cat.eat();
```

推荐调用方式：类名.静态成员

除了加在属性，方法，static还可以加在哪些地方呢？

![](http://myphoto.mtianyan.cn/20180801181018_EWrNSO_Screenshot.jpeg)

不能加载类名前，类名前仅仅允许添加: public abstract final; 因此static + 类 = 不存在的

方法中我们可以定义局部变量，

![](http://myphoto.mtianyan.cn/20180801181248_MMB5J0_Screenshot.jpeg)

但是局部变量的前面也是不允许加static的，局部变量仅仅被允许添加final

普通的成员方法是可以访问当前对象的成员变量和方法的。

```java
    public void run(){
        eat(); // 可以调用静态方法
        this.name = "妞妞";
        this.price = 200; // 普通方法也是可以访问静态成员的
    }
```

```java
    public static void eat(){
        run();
        age = 10;
        price = 200;
    }
```

![](http://myphoto.mtianyan.cn/20180801181746_gwf0Dn_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180801181802_aSeM1C_Screenshot.jpeg)

可以看到静态方法中是不能访问非静态成员方法和成员属性的，因为它缺少隐含的this参数。

如果非得在静态方法内来访问非静态成员方法呢？

```java
    public static void eat(){
        Cat cat = new Cat();
        cat.run();
        cat.age = 10;
        price = 200;
    }
```

静态方法中不能直接访问同一个类中的非静态成员，只能直接调用同一个类中的静态成员;非要访问，只能通过对象实例化后，对象.成员方法的方式访问非静态成员。

### static关键字(下）

关于代码块的相关知识，java中代码是由大括号括起来的。语句中出现大括号对就叫代码块。

当出现在方法里的时候，叫做普通代码块。普通代码块和一般语句的执行顺序是一样的。

```java
    public void run(){
        {
            System.out.println("我是普通代码块1");
        }
        System.out.println("小猫在跑");
        {
            System.out.println("我是普通代码块2");
        }
    }
```

普通代码块：顺序执行,先出现, 先执行

当代码块直接在类中定义,与成员方法，属性并列，就被称为是构造代码块。

```java
    {
        System.out.println("我是构造代码块1");
    }// 构造代码块
```

![](http://myphoto.mtianyan.cn/20180801183117_yE6DyA_Screenshot.jpeg)

可以看到，构造代码块比构造函数还先执行。构造代码块:创建对象时调用,优先于构造方法执行。不管构造方法块放在类里面的前后，它都会先于构造函数执行。

多个构造代码块之间有先后顺序，但都先于构造函数执行。

```java
    {
        System.out.println("我是构造代码块1");
    }
    // 中间吧啦吧啦一大堆
    {
        System.out.println("我是构造代码块2");
    }
```

![](http://myphoto.mtianyan.cn/20180801183446_Qg5PAT_Screenshot.jpeg)

在构造代码块前面加上static修饰，它就会变成静态代码块。

```java
    {
        System.out.println("我是构造代码块1");
    }
    // 中间吧啦吧啦一大堆
    static {
        System.out.println("我是位于后面的静态代码块");
    }
```

猜猜谁先执行呢?当时是先有类再有对象。静态的先执行。

![](http://myphoto.mtianyan.cn/20180801183804_SXK6wQ_Screenshot.jpeg)

```java
        Cat oneCat = new Cat(-1);
        Cat twoCat = new Cat(3);
```

![](http://myphoto.mtianyan.cn/20180801183943_0Q5Jku_Screenshot.jpeg)

可以看到，当实例化多个对象的时候，静态代码块只会执行一次，而构造代码块是实例化了多少个对象就执行多少次。

静态代码块: 类加载时调用,优先于构造代码块执行。一个类中也可以有多个静态代码块，它们的执行顺序显然是按照先后顺序了，就不举例子了。无论产生多少类实例,静态代码块只执行一次。

```java
    {
        name = "喵喵";// 非静态
        price = 100; // 静态
        System.out.println("我是构造代码块1");
    }
```

![](http://myphoto.mtianyan.cn/20180801184735_wurYYB_Screenshot.jpeg)

如图前面所学的一样，构造代码块中可以访问静态 & 非静态成员。静态代码块中只能访问静态成员。

仅希望执行一次的代码可以放在静态代码块中

#### 编程练习

请根据效果图以及任务要求完成代码。

程序参考运行效果图如下:

![](http://myphoto.mtianyan.cn/20180801185018_GpMOCL_Screenshot.jpeg)

任务

创建类Code,类中编写构造块、静态代码块以及构造函数; 创建CodeBlock,类中编写的构造块、静态代码块以及构造函数。
在主函数中测试他们的执行的优先顺序

```java
package cn.mtianyan.code;

public class Code {
    {
        System.out.println("Code的构造块");
    }
    public Code(){
        System.out.println("Code的构造方法");
    }
    static {
        System.out.println("Code的静态代码块");
    }
}
```

```java
package cn.mtianyan.code;

public class CodeBlock {
    {
        System.out.println("CodeBlock的构造块");
    }
    public CodeBlock(){
        System.out.println("CodeBlock的构造方法");
    }
    static {
        System.out.println("CodeBlock的静态代码块");
    }
    
    public static void main(String[] args) {
        CodeBlock codeBlock;
        System.out.println("CodeBlock的主方法");
        System.out.println("产生Code类实例对象");
        Code code = new Code();
        System.out.println("产生CodeBlock实例对象");
        codeBlock = new CodeBlock();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801185825_sGEyLs_Screenshot.jpeg)

### static关键字(续)

```java
    public void run(){
        {
            System.out.println("我是普通代码块1");
        }
        System.out.println("小猫在跑");
        {
            System.out.println("我是普通代码块2");
        }
    }
```

run方法里面有两个代码空间，代码块1和代码块2

![](http://myphoto.mtianyan.cn/20180801213930_I7qTl9_Screenshot.jpeg)

一个方法中是不能出现同名变量的，比如run中

```java
    public void run(){
        int temp =10;
        int temp =12;
    }
```

![](http://myphoto.mtianyan.cn/20180801214145_BUGQrK_Screenshot.jpeg)

```java
    public void run(){
//        int temp =10;
        {
            int temp = 11;
            System.out.println("我是普通代码块1");
        }
        System.out.println("小猫在跑");
        {
            int temp = 12;
            System.out.println("我是普通代码块2");
        }
    }
```

此时是正常的，两个代码块空间中允许有自己的变量值，不会重名造成冲突。但是不能在方法的全局域也就是注释的位置添加同名变量，会与两个变量都造成重复定义的问题。

![](http://myphoto.mtianyan.cn/20180801214703_hYgGkf_Screenshot.jpeg)

temp = 14是从它定义一直作用到结束的。

```java
    public void run(){
//        int temp =10;
        {
            int temp = 11;
            System.out.println("我是普通代码块1");
        }
        {
            int temp = 12;
            System.out.println("我是普通代码块2");
        }
        int temp = 13;
        System.out.println("小猫在跑");
    }
```

#### 编程实践

```java
package cn.mtianyan.ming;

public class Student {
    public String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public  int getAge() {
        return age;
    }

    public  void setAge(int age) {
        Student.age = age;
    }

    public static int age;

}

```

```java
package cn.mtianyan.ming;

public class StudentTest {
    public static void main(String[] args) {

        Student stu = new Student();
        stu.setName("小红");
        stu.setAge(13);
        Student stu1 = new Student();
        stu1.setName("小明");
        stu1.setAge(18);

        System.out.println(stu.getName()+"今年"+stu.getAge()+"岁了！");
        System.out.println(stu1.getName()+"今天"+stu.getAge()+"岁了！");
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801220004_FNnElz_Screenshot.jpeg)

### 总结

封装: 通过该类提供的方法来实现对隐藏信息的操作和访问;隐藏对象的信息 & 留出访问的接口

特点: 1. 只能通过规定的方法访问数据 & 2. 隐藏类的实例细节,方便修改和实现

合理的封装符合我们的使用习惯: 我们只需知道如何使用,并不需要深究它的内部实现构造。

java中三个步骤实现封装:

修改属性的可见性(设为private);创建getter/setter方法设为public用于属性的读写;在getter/setter方法中加入属性控制语句对属性值的合法性进行判断。

第一步是实现了内部重要信息的隐藏，二三步是留出了对外访问的接口。

包的作用: 1. 管理Java文件 2. 解决同名文件冲突

定义包: 语法 package 包名;

注意: 1. 必须放在Java源文件中的第一行  2. 一个Java源文件中只能有一个package语句  3. 包名全部英文小写4. 命名方式:域名倒序+模块+功能

跨包访问的语法: import 包名.类名;

例:

```java
// 导入包中全部类
import cn.mtianyan.*;

// 导入包中指定类:
import cn.mtianyan.animal.Cat;
```

通配符只能导入当前mtianyan包下的类，不能导入它的子包如(animal)的类。

**static**

1. static+属性  2. static+方法 3. static+类 4. static+方法内局部変量 5. static+代码块

静态属性、类属性 & 静态方法、类方法; 不存在静态类，不存在方法中的静态局部变量; 

{}来隔离一个代码块出来，存在于方法当中称之为普通代码块;存在于类当中时被称为构造代码块; 当构造代码块前面加上static关键字的时候就变成了静态代码块。

注意问题:

  1. 静态成员的生命周期： 类加载时产生,销毁时释放,生命周期长
  2. 静态方法中的成员调用：可以直接访问类内的静态成员，不可以直接访问类内的非静态成员。非得访问，只能在方法内实例化对象再通过对象访问。
  3. 各种代码块的执行顺序: 静态代码块只执行一次，构造代码块在每次对象构造的时候调用,普通代码块在调用方法时使用。

在下一集中,我们将通过一个综合案例,带领大家进一步学习“封装”在面向对象编程中的应用。















































































