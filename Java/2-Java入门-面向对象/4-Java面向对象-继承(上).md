什么是继承?继承有哪些特点?我们在Java中如何实现继承?

程序中的继承（面向对象编程思想来源于生活）:

![](http://myphoto.mtianyan.cn/20180802170319_r2ObHf_Screenshot.jpeg)

解决重复代码的出现问题。抽取共性生成父类。

![](http://myphoto.mtianyan.cn/20180802170416_cT0dKf_Screenshot.jpeg)

此时猫和狗直接继承父类将可以直接使用父类的这些成员属性和方法。此时子类当中的方法就可以只写子类所特有的东西。

特点: 1. 利于代码复用;2. 缩短开发周期

继承是: -种类与类之间的关系; 使用已存在的类的定义作为基础建立新类。已存在的类称为父类(基类); 建立的新类称为子类(派生类)。

新类的定义可以增加新的数据或新的功能,也可以用父类的功能,**但不能选择性地继承父类**

满足 "A is a B"的关系就可以形成继承关系;

![](http://myphoto.mtianyan.cn/20180802170855_IxN5J9_Screenshot.jpeg)

### 继承的概念和特点

代码中是通过 `extends` 关键字实现继承的。

编写父类:

```java
class Animal{
  // 公共的属性和方法
}
```

编写子类，继承父类:

```java
class Dog extends Animal{
  //子类特有的属性和方法
}
class Cat extends Animal{
  //子类特有的属性和方法
}
```

java中只能继承一个父类(单继承)。子类可以访问父类非私有成员

```java
package cn.mtianyan.inherit;

public class Animal {
    private String name;
    private int month;
    private String species;

    public Animal(){

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

    public String getSpecies() {
        return species;
    }

    public void setSpecies(String species) {
        this.species = species;
    }
    // 吃东西
    public void eat(){
        System.out.println(this.getName()+"在吃东西");
    }
}
```

```java
package cn.mtianyan.inherit;

public class Cat extends Animal {
    private double weight; //体重

    public Cat(){

    }
    public double getWeight() {
        return weight;
    }

    public void setWeight(double weight) {
        this.weight = weight;
    }
    // 跑动的方法
    public void run(){
        System.out.println(this.getName()+"是一只"+this.getSpecies()+",它在快乐的奔跑");
    }
}
```

```java
package cn.mtianyan.inherit;

public class Dog extends Animal {
    private  String sex; //性别
    public void Dog(){

    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    // 睡觉的方法
    public void sleep(){
        System.out.println(this.getName()+"现在"+this.getMonth()+"个月大,它在睡觉");
    }
}
```

```java
package cn.mtianyan.inherit;

public class Test {
    public static void main(String[] args) {
        Cat one = new Cat();
        one.setName("花花");
        one.setSpecies("中华田园猫");
        one.eat();
        one.run();
        System.out.println("===============");
        Dog two = new Dog();
        two.setName("妞妞");
        two.setMonth(1);
        two.eat();
        two.sleep();
    }
}
```

![](http://myphoto.mtianyan.cn/20180802172532_pACr5e_Screenshot.jpeg)

可以看到子类继承了父类之后可以访问父类的非私有成员，但是父类的私有成员子类还是无法直接访问的，但可以通过父类暴露的公有方法实现间接访问。

![](http://myphoto.mtianyan.cn/20180802173625_bUCpim_Screenshot.jpeg)

当然父类对象也不可以访问到子类特有的方法或属性。父类不可以访问子类特有成员（那怕是公有的）

### 方法的重写

现在狗中的吃东西方法是父类的吃东西的方法，我希望狗有自己独立的吃东西的方法。虽然有父类吃东西的这个能力，但是表现形式是不一样的。

![](http://myphoto.mtianyan.cn/20180802173920_A7jcrG_Screenshot.jpeg)

可以通过方法重写来实现。我们之前学过方法重载的概念

方法重载: 1. 同一个类中; 2. 方法名相同，参数列表不同(参数顺序、个数、类型);3. 方法返回值、访问修饰符任意。4. 与方法的参数名无关

```java
    // 睡觉的方法
    public void sleep(){
        System.out.println(this.getName()+"现在"+this.getMonth()+"个月大,它在睡觉");
    }
    // 睡觉方法的重载方法
    private String sleep(String name){
        return "";
    }
    // 只要两个参数的类型顺序不同
    public void sleep(String name,int month){

    }
    public void sleep(int month,String name){

    }
    // 与方法的参数名无关,加上下面的代码会和上面的 sleep(int month,String name)造成重复定义
    public void sleep(int age,String month){
        
    }
```

### 方法的重写(下）

语法规则:

返回值类型;方法名;参数类型、顺序、个数; 前述要素都要与父类继承的方法相同

前提是有继承关系，子类来重写父类。

方法重写: 1.有继承关系的子类中; 2. 方法名相同，参数列表相同(参数顺序、个数、类型)，方法返回值相同;方法的访问修饰符是可以允许有变化的(有条件的)

这种条件性，讲解访问修饰符的时候再说。

```java
    // 狗类中 子类重写父类吃东西方法
    public void eat(){
        System.out.println(this.getName()+"最近没有食欲");
    }
```

当子类重写父类方法后,子类对象调用的是重写后的方法。

![](http://myphoto.mtianyan.cn/20180802175225_FYB4Fp_Screenshot.jpeg)

```java
    // 动物类中: 吃东西
    public void eat(){
        System.out.println(this.getName()+"在吃东西");
    }
```

```java
    // 狗类中 子类重写父类吃东西方法
    public void eat(String month){
        System.out.println(month+"最近没有食欲");
    }
```

狗类中重写父类的吃东西方法，我使用的是java10，即使参数列表不同也是可以重写的。（这里就不太清楚什么情况了）我测试这样的参数不同的重载，就不能在后面实现父类对象指向子类方法的多态了。后面具体学到再说

### 方法重写的碎碎念

不止可以定义同名的方法来重写父类的方法，还可以在子类中定义与父类同名的属性。

```java
    public int temp =150; // 动物类中
```

```java
    public int temp =300; // 猫类中
```

![](http://myphoto.mtianyan.cn/20180802180600_mqck3L_Screenshot.jpeg)

#### 编程联系

编程练习:请使用面向对象的思想,设计自定义类完成如下功能要求:

接收用户输入的信息,选择需要完成的工作任务。其中，可供选择的有:测试工作和研发工作。关于类型设定描述如下:

测试工作属性:工作名称、编写的测试用例个数、发现的Bug数量 方法:工作描述
研发工作属性:工作名称、有效编码行数、目前没有解决的Bug个数 方法:工作描述

![](http://myphoto.mtianyan.cn/20180802180942_Xnpso8_Screenshot.jpeg)

```java
package cn.mtianyan.bug;

public class Programmer {
    public String getWorkerName() {
        return workerName;
    }
    public Programmer(){

    }
    public Programmer(String workerName, int usefulCodeNum, int bugCodeNum) {
        this.workerName = workerName;
        this.usefulCodeNum = usefulCodeNum;
        this.bugCodeNum = bugCodeNum;
    }

    public void setWorkerName(String workerName) {
        this.workerName = workerName;
    }

    public int getUsefulCodeNum() {
        return usefulCodeNum;
    }

    public void setUsefulCodeNum(int usefulCodeNum) {
        this.usefulCodeNum = usefulCodeNum;
    }

    public int getBugCodeNum() {
        return bugCodeNum;
    }

    public void setBugCodeNum(int bugCodeNum) {
        this.bugCodeNum = bugCodeNum;
    }

    private String workerName;
    private int usefulCodeNum;
    private int bugCodeNum;
    public void workerInfo(){
        System.out.println("父类信息测试: 开心工作");
    }
}
```

```java
package cn.mtianyan.bug;

public class TestProgrammer extends Programmer {
    public TestProgrammer(){

    }
    public TestProgrammer(String workerName, int usefulCodeNum, int bugCodeNum) {
        this.setWorkerName(workerName);
        this.setUsefulCodeNum(usefulCodeNum);
        this.setUsefulCodeNum(bugCodeNum);
    }
    public void workerInfo(){
        System.out.print(this.getWorkerName()+"类测试: "+this.getWorkerName()+"的日报是: 今天编写了"+this.getUsefulCodeNum());
        System.out.printf("个测试用例，发现了"+this.getBugCodeNum()+"个bug");
    }
}
```

```java
package cn.mtianyan.bug;

public class DevelopProgrammer extends Programmer {
    public DevelopProgrammer(String workerName, int usefulCodeNum, int bugCodeNum) {
        this.setWorkerName(workerName);
        this.setUsefulCodeNum(usefulCodeNum);
        this.setUsefulCodeNum(bugCodeNum);
    }
    public void workerInfo(){
        System.out.print(this.getWorkerName()+"信息类测试: "+this.getWorkerName()+"的日报是: 今天编写了"+this.getUsefulCodeNum());
        System.out.printf("行代码，目前仍然有"+this.getBugCodeNum()+"个bug没有解决");
    }
}
```

```java
package cn.mtianyan.bug;

public class Test {
    public static void main(String[] args) {
        Programmer programmer = new Programmer();
        programmer.workerInfo();
        TestProgrammer testProgrammer = new TestProgrammer("测试工作",10,5);
        testProgrammer.workerInfo();
        System.out.println();
        DevelopProgrammer developProgrammer = new DevelopProgrammer("研发工作",1000,10);
        developProgrammer.workerInfo();
    }
}
```

这里子类中想要有带参构造函数，父类必须有一个默认构造函数(无参构造函数或全参全默认值构造函数）

### 访问修饰符

公有的: public; 私有的: private; 受保护的: protected; 默认

private:只允许在本类中进行访问，离开了当前类就不允许被访问了。

public:允许在任意位置访问

protected:允许在当前类，同包中的子类/非子类都可以，跨包子类调用。跨包的非子类不允许调用。

默认: 允许在当前类，跨包子类/非子类都不允许，同包子类/非子类都可调用，

|访问修饰符| 本类| 同包| 子类| 其他|
|----------|-----|-----|-----|-----|
|private|√||||
|默认|√|√|||
|protected|√|√|√||
|public|√|√|√|√|

自上而下，访问范围越来越小；自下而上，限制能力越来越强。

大家还记得之前提到的那个问题吗 方法的重写与访问修饰符的关系。

![](http://myphoto.mtianyan.cn/20180802184827_raazJl_Screenshot.jpeg)

### 访问修饰符对方法重写的影响

答案: 子类重写父类方法时，访问修饰符是允许改变的。要求是: 访问范围要求大于等于父类的访问范围。

如果父类是public 那么子类的也必须是public

![](http://myphoto.mtianyan.cn/20180802185101_3AyCVq_Screenshot.jpeg)

可以看到不遵守，就会报错。

面向对象程序来源于生活，父类当然希望子类比自己的交际范围更强更广。

### super关键字的使用(上)

子类可以继承父类的方法，也可以重写自己的方法。那么问题来了，如何判断子类的其他方法中调用的这个方法是父类的还是自己的。

```java
    //  Animal类 吃东西
    public void eat(){
        System.out.println(this.getName()+"在吃东西");
    }
    // 狗类中 子类重写父类吃东西方法
    public void eat(){
        System.out.println(this.getName()+"最近没有食欲");
    }
    
    // 狗类中的睡觉方法
    public void sleep(){
        eat();
        System.out.println(this.getName()+"现在"+this.getMonth()+"个月大,它在睡觉");
    }
```

```java
        Dog two = new Dog();
        two.setName("妞妞");
        two.sleep();
```

运行结果:

![](http://myphoto.mtianyan.cn/20180802224909_UnSQk0_Screenshot.jpeg)

可以看到调用的是子类中重写过后的方法。

`super`关键字是对父类对象的引用。

```java
    // 狗类中的睡觉方法
    public void sleep(){
        super.eat();
        System.out.println(this.getName()+"现在"+this.getMonth()+"个月大,它在睡觉");
    }
```

此时直接指明调用父类对象的eat方法。而且不止调用成员方法，也可以访问成员属性

```java
        super.temp = 10;
```

普通的成员方法都是可以通过super被子类访问到的，但是构造方法是不可以的。因为父类的构造方法是不允许被继承,不允许被重写。虽然它两个不允许，但是它的存在是非常必要的，子类对象的实例化要依赖于父类对象存在默认构造函数(无参或全参全默认值)

### 继承的初始化顺序

满足继承关系的子类对象是如何产生的?

认识子类对象的实例化过程: 

```java
package cn.mtianyan.inherit;

public class Animal {
    private String name;
    private int month;
    private String species;
    public int temp =150;

    private static int st1=22;
    public static int st2=23;

    static {
        System.out.println("我是父类的静态代码块");
    }

    {
        System.out.println("我是父类的构造代码块");
    }
    public Animal(){
        System.out.println("我是父类的无参构造方法");
    }
}
```

```java
package cn.mtianyan.inherit;

public class Cat extends Animal {
    private double weight; //体重
    // public int temp =300;
    public static int st3 =44;
    static {
        System.out.println("我是子类的静态代码块");
    }

    {
        System.out.println("我是子类的构造代码块");
    }
    public Cat(){
        System.out.println("我是子类的无参构造方法");
    }
}
```

```java
package cn.mtianyan.inherit;

public class TestTwo {
    public static void main(String[] args) {
        Cat cat = new Cat();
        System.out.println(cat.temp);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180802232723_sq4qns_Screenshot.jpeg)

继承后的初始化顺序： 

父类静态成员 -> 子类静态成员 -> 父类对象构造 -> 子类对象构造

问题: 访问修饰符影响成员加载顺序?静态成员优先于静态代码块执行?

访问修饰符不影响成员加载顺序,跟书写位置有关。如果把静态代码块写在静态变量的前面，那么先执行静态代码块。

### Super关键字的使用(下)

可以看到我们刚才的例子中子类执行了父类的默认无参构造方法，但是问题来了，子类是否有权利选取使用父类的哪个构造方法呢？

```java
    public Cat(String name,int month){
        System.out.println("我是子类的带参构造方法");
    }
```

```java
    public Animal(String name,int month){
        System.out.println("我是父类的有参构造方法");
    }
```

```java
package cn.mtianyan.inherit;

public class TestTwo {
    public static void main(String[] args) {
        Cat cat = new Cat("花花",2);
        System.out.println(cat.temp);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180803002858_iPFIAI_Screenshot.jpeg)

可以看到即使子类使用的带参构造函数，父类使用的依然是无参构造函数。调试过程中可以看到父类即使没有extends任何东西，还是继承自祖宗object的.

当我们在子类的构造方法中没有显示的标志的时候，默认调用的是父类的无参构造方法。 因此父类的无参构造很重要，否则会影响子类的实例化。

```java
    public Cat(String name,int month){
        super(name, month);
        System.out.println("我是子类的带参构造方法");
    }
```

通过super来调用父类的有参构造方法。

![](http://myphoto.mtianyan.cn/20180803004634_m8f77M_Screenshot.jpeg)

子类构造默认调用父类无参构造方法;可以通过super()调用父类允许被访问的其他构造方法;super()必须放在子类构造方法有效代码第一行;且只能放在构造方法里。

![](http://myphoto.mtianyan.cn/20180803004930_SZqO20_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180803004948_AsMJkJ_Screenshot.jpeg)

**super**

代表父类引用: 访问父类成员方法 super.print(); 访问父类属性 super.name; 访问父类构造方法 super();

子类的构造的过程中必须调用其父类的构造方法; 如果子类的构造方法中没有显式标注,则系统系默认调用父类无参的构造方法

如果子类构造方法中既没有显式标注,且父类中没有无参的构造方法,则编译出错

使用super调用父类指定构造方法,必须在子类的构造方法的第一行

### super pk this

super 父类对象 & this 当前对象

静态方法中不能使用this，因为没有传入隐藏的this对象引用.当然也不能调用super

```java
    public Cat(String name,int month){
        this();
        System.out.println("我是子类的带参构造方法");
    }
```

会同时执行同一个类中的无参构造方法。

![](http://myphoto.mtianyan.cn/20180803005947_UWFXzM_Screenshot.jpeg)

构造方法中super和this能并存么?如果可以，谁先谁后?

我觉得可以，先super后this。

![](http://myphoto.mtianyan.cn/20180803010113_uCNZ87_Screenshot.jpeg)

正确答案是: this和super都要求是第一行，这两个只能出现一个。

this: 当前类对象的引用;访问当前类的成员方法;访问当前类的成员属性;访问当前类的构造方法;不能在静态方法中使用

super: 父类对象的引用;访问父类的成员方法;访问父类的成员属性;访问父类的构造方法;不能在静态方法中使用

构造方法调用时, super和this不能同时出现（因为两者都要求自己是第一行）

#### 编程练习

编程练习:某公司要开发"XX车行管理系统”，请使用面向对象的思想,设计自定义类描述自行车、电动车和三轮车。

程序参考运行效果图如下:

![](http://myphoto.mtianyan.cn/20180803011704_Q5xyK5_Screenshot.jpeg)

任务分析:

第一步: 分析自行车，电动车和三轮车的共性都是非机动车，具有非机动车的基本特征都有运行的方法
第二步: 根据共性，定义非机动车属性:品牌、颜色、轮子(默认2个)、座椅(默认1个)

方法: 编写无参构造方法、双参构造方法和四参构造方法，其中，在双参构造方法中，完成对品牌和颜色的赋值;在四参构造方法中，完成对所有属性的赋值

```java
package cn.mtianyan.bike;

/**
 * 非机动车
 */
public class NonMotorVehicle {
    private String brand;
    private String color;
    private int numberOfWheels = 2;
    private int seatNumber = 1;

    public NonMotorVehicle(String brand, String color, int numberOfWheels, int seatNumber) {
        this.brand = brand;
        this.color = color;
        this.numberOfWheels = numberOfWheels;
        this.seatNumber = seatNumber;
    }

    public NonMotorVehicle(String brand, String color) {
        this.brand = brand;
        this.color = color;
    }

    public NonMotorVehicle() {

    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getNumberOfWheels() {
        return numberOfWheels;
    }

    public void setNumberOfWheels(int numberOfWheels) {
        this.numberOfWheels = numberOfWheels;
    }

    public int getSeatNumber() {
        return seatNumber;
    }

    public void setSeatNumber(int seatNumber) {
        this.seatNumber = seatNumber;
    }
    public void run(){
        System.out.print("父类信息测试: ");
        System.out.print("这是一辆"+this.getColor()+"颜色的,");
        System.out.print(this.getBrand()+"牌的非机动车,有");
        System.out.printf(this.getNumberOfWheels()+"个轮子,"+"有"+getSeatNumber()+"个座椅");
    }
}
```

```java
package cn.mtianyan.bike;

public class Bike extends NonMotorVehicle {
    public Bike(String brand, String color) {
        super(brand, color);
    }

    public void run(){
        System.out.print("自行车类测试: ");
        System.out.print("这是一辆"+this.getColor()+"颜色的,");
        System.out.print(this.getBrand()+"牌的自行车");
    }
}
```

```java
package cn.mtianyan.bike;

public class ElectricBike extends NonMotorVehicle {
    public ElectricBike(String brand){
        this.setBrand(brand);
    }
    public void run(){
        System.out.print("电动车类信息测试: ");
        System.out.print("这是一辆使用");
        System.out.print(this.getBrand()+"牌电池的电动车");
    }
}

```

```java
package cn.mtianyan.bike;

public class Tricycle extends NonMotorVehicle{
    public Tricycle(int numberOfWheels){
        this.setNumberOfWheels(numberOfWheels);
    }
    public void run(){
        System.out.print("三轮车类信息测试: ");
        System.out.print("三轮车是一款有"+this.getNumberOfWheels()+"个轮子的非机动车");
    }
}

```

```java
package cn.mtianyan.bike;

public class Test {
    public static void main(String[] args) {
        NonMotorVehicle nonMotorVehicle = new NonMotorVehicle("天宇","红",4,2);
        nonMotorVehicle.run();
        System.out.println();
        Bike bike = new Bike("捷安特","黄");
        bike.run();
        System.out.println();
        ElectricBike electricBike = new ElectricBike("飞鸽");
        electricBike.run();
        System.out.println();
        Tricycle tricycle = new Tricycle(3);
        tricycle.run();
    }

}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180803015858_X7fFil_Screenshot.jpeg)

### 总结

继承

概念: 1. 一种类与类之间的关系;2. 使用已存在的类的定义作为基础建立新类;3. 新类的定义可以增加新的数据或新的功能,也可以用父类的功能,但不能选择性地继承父类;4. 满足"A is a B"的关系

特点: 1. 利于代码复用 2. 缩短开发周期

语法: 1. 使用extends实现继承 2. 单一继承,只能有一个父类

```java
class Dog extends Animal{
    //子类特有的属性和方法 
}
```

继承后的初始化顺序:

![](http://myphoto.mtianyan.cn/20180803020233_vvklPX_Screenshot.jpeg)

super: 

  - 访问父类成员方法 `super.print();`
  - 访问父类属性 `super.name;`
  - 访问父类构造方法 `super();`

子类的构造的过程中必须调用其父类的构造方法,默认调用无参的构造方法。
如果子类构造方法中既没有显式标注,而父类又没有无参的构造方法,则编译出错。
使用super调用父类指定构造方法,必须在子类的构造方法的第一行。

![](http://myphoto.mtianyan.cn/20180803020454_nRoHKw_Screenshot.jpeg)

构造方法调用时, super和this不能同时出现

方法重写: 

  - 在满足继承关系的子类中
  - 方法名、参数个数、顺序、返回值与父类相同
  - 访问修饰符的限定范围大于等于父类方法(重点)

方法重载:

  - 在同一个类中
  - 方法名相同
  - 参数个数、顺序、类型不同
  - 返回值类型、访问修饰符任意

访问修饰符:

![](http://myphoto.mtianyan.cn/20180803020657_H152gk_Screenshot.jpeg)

在下一集中,我们将继续进行继承相关知识的学习,将会带领大家，一起来学习Object类、final关键字以及注解的相关知识。















































