### 案例简介

通过一个简单的案例具体的实现一下封装。

![](http://myphoto.mtianyan.cn/20180801223043_e2R6Rp_Screenshot.jpeg)

通过java语言和面向对象的思想，模拟一个场景的实现。

 案例: 学校开设了计算机科学与应用这个专业,专业编号: J0001;学制年限: 4年;
 
 现在有三个学生报名了该学校。
 
 ![](http://myphoto.mtianyan.cn/20180801223259_4e281E_Screenshot.jpeg)

实现的效果图:

![](http://myphoto.mtianyan.cn/20180801223342_bOvPGG_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180801223353_QJF9NS_Screenshot.jpeg)

```java
package cn.mtianyan.computer;

public class Subject {
    public Subject(String name, String code, int year){
        this.setName(name);
        this.setCode(code);
        this.setYear(year);
    }
    public void showInfo(){
        System.out.println("专业信息如下:");
        System.out.println("专业名称: " + this.name);
        System.out.println("专业编号: " + this.code);
        System.out.println("学制年限: " + this.year +"年");
        System.out.println("=====================");
    }
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getCode() {
        return code;
    }

    public void setCode(String code) {
        this.code = code;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    private String code;
    private int year;
}
```

```java
package cn.mtianyan.computer;

public class Student {
    public Student(String name,String studentID, String sex,int age,Subject subject){
        this.setName(name);
        this.setStudentID(studentID);
        this.setAge(age);
        this.setSex(sex);
        this.subject = subject;
    }
    public void showInfo(){
        System.out.println("==================");
        System.out.println("姓名: "+name);
        System.out.println("学号: "+studentID);
        System.out.println("性别: "+sex);
        System.out.println("年龄: "+age);
        System.out.println("所报专业名称: "+ subject.getName());
        System.out.println("学制年限: "+ subject.getYear());
    }
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getStudentID() {
        return studentID;
    }

    public void setStudentID(String studentID) {
        this.studentID = studentID;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    private String studentID;
    private String sex;
    private int age;
    private Subject subject;
}
```

```java
package cn.mtianyan.computer;

public class Test {
    public static void main(String[] args) {
        Subject subject = new Subject("计算机科学与应用","J0001",4);
        subject.showInfo();
        Student student1 = new Student("张三","S01","男",18, subject);
        student1.showInfo();
        Student student2 = new Student("李四","S02","女",17, subject);
        student2.showInfo();
        Student student3 = new Student("王五","S03","男",18, subject);
        student3.showInfo();
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180801225809_5W9om4_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180801225829_at0zu4_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180801225843_2aaw7j_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180801225852_px4NJh_Screenshot.jpeg)

上面是我个人的实现.

### 综合案例

计算机科学与应用是一个对象。 三个学生是三个对象。学科专业类 & 专业类

类:

  1. 专业: 专业名称、编号、学制年限
  2. 学生: 姓名、学号、性别、年龄

### 编写Subject类

啊啊啊，英语真季二茶，Get到了。Subject是学科。

分包存储: cn.mtianyan.model cn.mtianyan.test

```java
package cn.mtianyan.model;
/**
 * 专业类
 * @author mtianyan
 */
public class Subject {
	// 成员属性：学科名称、学科编号、学制年限、报名选修的学生信息、报名选修的学生个数
	private String subjectName;
	private String subjectNo;
	private int subjectLife;
	private Student[] myStudents; // 专业学生数组
	private int studentNum;
	
	// 无参构造方法
	public Subject() {

	}

	// 带参构造，带参构造，实现对全部属性的赋值
	public Subject(String subjectName, String subjectNo, int subjectLife) {
		// this.subjectName=subjectName;
		this.setSubjectName(subjectName);
		this.setSubjectNo(subjectNo);
		this.setSubjectLife(subjectLife);
	}
	
	public void setSubjectName(String subjectName) {
		this.subjectName = subjectName;
	}

	public String getSubjectName() {
		return this.subjectName;
	}

	public String getSubjectNo() {
		return subjectNo;
	}

	public void setSubjectNo(String subjectNo) {
		this.subjectNo = subjectNo;
	}

	public int getSubjectLife() {
		return subjectLife;
	}

	// 设置学制年限，限制必须>0
	public void setSubjectLife(int subjectLife) {
		if (subjectLife <= 0)
			return;
		this.subjectLife = subjectLife;
	}

	/**
	 * 获取选修专业的学生信息 如果保存学生信息的数组未被初始化，则，先初始化长度200
	 * @return 保存学生信息的数组
	 */
	public Student[] getMyStudents() {
		if(this.myStudents==null)
			this.myStudents=new Student[200];
		return myStudents;
	}

	public void setMyStudents(Student[] myStudents) {
		this.myStudents = myStudents;
	}

	public int getStudentNum() {
		return studentNum;
	}

	public void setStudentNum(int studentNum) {
		this.studentNum = studentNum;
	}

	/**
	 * 专业介绍的方法
	 * @return 专业介绍的相关信息，包括名称、编号、年限
	 */
	public String info() {
		String str = "专业信息如下：\n专业名称：" + this.getSubjectName() + "\n专业编号：" + this.getSubjectNo() + "\n学制年限："
				+ this.getSubjectLife() + "年";
		return str;
	}
	
	public void addStudent(Student stu){
		/*
		 * 1、将学生保存到数组中
		 * 2、将学生个数保存到studentNum
		 * */
		//1、将学生保存到数组中
		for(int i=0;i<this.getMyStudents().length;i++){
			if(this.getMyStudents()[i]==null){
				stu.setStudentSubject(this);
				this.getMyStudents()[i]=stu;
				//2、将学生个数保存到studentNum
				this.studentNum=i+1;
				return;
			}
		}
	}
}
```

这里我们的info方法在设计的时候返回String而不是直接在方法内打印，体现了单一职责原则，这样的设计使得这些字符串如果后期不是在控制台打印，而是做其他处理更方便。

### 编写Student类

```java
package cn.mtianyan.model;

public class Student {
	// 成员属性：学号、姓名、性别、年龄、专业
	private String studentNo;
	private String studentName;
	private String studentSex;
	private int studentAge;
	private Subject studentSubject;
	
	// 无参构造方法
	public Student() {

	}
	//多参构造方法，实现对学号、姓名、性别、年龄的赋值
	public Student(String studentNo, String studentName, String studentSex, int studentAge) {
		this.setStudentNo(studentNo);
		this.setStudentName(studentName);
		this.setStudentSex(studentSex);
		this.setStudentAge(studentAge);
	}
	// 多参构造方法，实现对全部属性的赋值
	public Student(String studentNo, String studentName, String studentSex, int studentAge,Subject studentSubject) {
		this.setStudentNo(studentNo);
		this.setStudentName(studentName);
		this.setStudentSex(studentSex);
		this.setStudentAge(studentAge);
		// this.studentAge=studentAge;
		this.setStudentSubject(studentSubject);
	}

	public String getStudentNo() {
		return studentNo;
	}

	public void setStudentNo(String studentNo) {
		this.studentNo = studentNo;
	}

	public String getStudentName() {
		return studentName;
	}

	public void setStudentName(String studentName) {
		this.studentName = studentName;
	}

	public String getStudentSex() {
		return studentSex;
	}

	public void setStudentSex(String studentSex) {
		// 限制性别只能是“男”或者“女”，反之，强制赋值为“男”
		if(studentSex.equals("男") | studentSex.equals("女")){
			this.studentSex = studentSex;
		}else {
			this.studentSex = "男";
		}

	}

	public int getStudentAge() {
		return studentAge;
	}

	/**
	 * 给年龄赋值，限定必须在10--100之间，反之赋值为18
	 * 
	 * @param studentAge
	 *            传入的年龄
	 */
	public void setStudentAge(int studentAge) {
		if (studentAge < 10 || studentAge > 100)
			this.studentAge = 18;
		else
			this.studentAge = studentAge;
	}

	/**
	 * 获取专业对象，如果没有实例化，先实例化后再返回
	 * @return 专业对象信息
	 */
	public Subject getStudentSubject() {
		if(this.studentSubject==null)
			this.studentSubject=new Subject();
		return studentSubject;
	}

	public void setStudentSubject(Subject studentSubject) {
		this.studentSubject = studentSubject;
	}

	/**
	 * 学生自我介绍的方法
	 * 
	 * @return 自我介绍的信息，包括姓名、学号、性别、年龄
	 */
	public String introduction() {
		String str = "学生信息如下：\n姓名：" + this.getStudentName() + "\n学号：" + this.getStudentNo() + "\n性别："
				+ this.getStudentSex() + "\n年龄：" + this.getStudentAge()+ "\n所报专业名称：" + this.getStudentSubject().getSubjectName() + "\n学制年限："
						+ this.getStudentSubject().getSubjectLife();
		return str;
	}

	/**
	 * 学生自我介绍的方法
	 * @param subjectName 所学专业名称
	 * @param subjectLife 学制年限
	 * @return 自我介绍的信息，包括姓名、学号、性别、年龄、所学专业名称、学制年限
	 */
	public String introduction(String subjectName, int subjectLife) {
		String str = "学生信息如下：\n姓名：" + this.getStudentName() + "\n学号：" + this.getStudentNo() + "\n性别："
				+ this.getStudentSex() + "\n年龄：" + this.getStudentAge() + "\n所报专业名称：" + subjectName + "\n学制年限："
				+ subjectLife;
		return str;
	}

	/**
	 * 学生自我介绍的方法
	 * @param mySubject 所选专业的对象
	 * @return自我介绍的信息，包括姓名、学号、性别、年龄、所学专业名称、学制年限
	 */
	public String introduction(Subject mySubject){
		String str = "学生信息如下：\n姓名：" + this.getStudentName() + "\n学号：" + this.getStudentNo() + "\n性别："
				+ this.getStudentSex() + "\n年龄：" + this.getStudentAge() + "\n所报专业名称：" + mySubject.getSubjectName() + "\n学制年限："
				+ mySubject.getSubjectLife()+"\n专业编号："+mySubject.getSubjectNo();
		return str;
	}
}
```

对于参数很多的构造方法，可以选择右键生成构造方法，然后选择上所要涵盖的参数。

![](http://myphoto.mtianyan.cn/20180801232218_ORd9pQ_Screenshot.jpeg)

如何实现字符串内容是否相等的判断?

可以通过`equals()`方法进行字符串内容的判断,如果内容相等返回值为true，反之为false。如:当str代表用户性别时,可以通过如下代码判断性别为男还是女

```java
if (str.equals("男"))
  System.out.println("性别为男")
else
  System.out.println("性别为女")
```

### 通过方法实现学生与专业关联

方案1: 在方法中添加两个参数,分别表示专业名称和学制年限。

```java
	public String introduction(String subjectName, int subjectLife) {
		String str = "学生信息如下：\n姓名：" + this.getStudentName() + "\n学号：" + this.getStudentNo() + "\n性别："
				+ this.getStudentSex() + "\n年龄：" + this.getStudentAge() + "\n所报专业名称：" + subjectName + "\n学制年限："
				+ subjectLife;
		return str;
	}
```

前往 Editor -> General 中 Other 部分，选中 show quick documentation on mouse move 设置多少毫秒会显示。 

![](http://myphoto.mtianyan.cn/20180802102635_5Nk27f_Screenshot.jpeg)

这样可以看到文档注释的优点所在。

### 通过方法实现学生与专业关联-方案2

这里我们添加的两个参数和我们Subject类中的属性造成了数据冗余。在方法中添加1个专业对象作为参数,通过其属性获得相关信息

```java
	/**
	 * 学生自我介绍的方法
	 * @param mySubject 所选专业的对象
	 * @return自我介绍的信息，包括姓名、学号、性别、年龄、所学专业名称、学制年限
	 */
	public String introduction(Subject mySubject){
		String str = "学生信息如下：\n姓名：" + this.getStudentName() + "\n学号：" + this.getStudentNo() + "\n性别："
				+ this.getStudentSex() + "\n年龄：" + this.getStudentAge() + "\n所报专业名称：" + mySubject.getSubjectName() + "\n学制年限："
				+ mySubject.getSubjectLife()+"\n专业编号："+mySubject.getSubjectNo();
		return str;
	}
```

### 通过方法实现学生与专业关联-方案3

因为大学生是一定有一个专业信息的，在类中添加专业对象作为成员属性,通过其属性获得相关信息。

```java
	private Subject studentSubject; // 对象默认值是null
	// 构造函数添加参数
	// 增加set 和 get方法
```

类除了我们需要用到的有参构造，应该准备一个无参构造，保证程序特殊情况的正常运行。

```java
	public Subject getStudentSubject() {
		if(this.studentSubject==null)
			this.studentSubject=new Subject();
		return studentSubject;
	}
```

```java
"\n学制年限："+ this.getStudentSubject().getSubjectLife();
```

先获取到专业对象，再通过对象获取到专业年限

### 通过方法实现学生与专业关联-方案分析

方案1 :在方法中添加两个参数,分别表示专业名称和学制年限 优点: 容易理解 缺点: 参数列表长

方案2 :在方法中添加1个专业对象作为参数,通过其属性获得相关信息。 优点: 更加简单 获取参数方便 学生与专业关联性不强

方案3 ;在类中添加专业对象作为属性,通过其属性获得相关信息.  优点: 关联性更强

方法中传入对象，传递的是一个对象的引用。在方法中通过对象作为参数,传递的是它的引用可以通过引用获取该对象所有信息。

这样是很不安全的。

```java
	public String introduction(Subject mySubject){
	  mySubject.setSubjectName("mtianyan学科");
		String str = "学生信息如下：\n姓名：" + this.getStudentName() + "\n学号：" + this.getStudentNo() + "\n性别："
				+ this.getStudentSex() + "\n年龄：" + this.getStudentAge() + "\n所报专业名称：" + mySubject.getSubjectName() + "\n学制年限："
				+ mySubject.getSubjectLife()+"\n专业编号："+mySubject.getSubjectNo();
		return str;
	}
```

```java
Subject sub1=new Subject("计算机科学与应用","J0001",4);
Student stu3=new Student("S03","王五","男",18);
System.out.println(stu3.introduction(sub1));
System.out.println("=====================");
System.out.println(sub1.info());
```

![](http://myphoto.mtianyan.cn/20180802112010_CXqw12_Screenshot.jpeg)

可以看到学生类中的自我介绍修改专业，会将sub1都修改掉。这里如何对于传入的对象进行保护，后面再讲。目前先记住这个问题。

### 新增需求及分析

计算机科学与应用专业有多少个学生进行了报名?如何实现？

用什么样的容器装学生？

![](http://myphoto.mtianyan.cn/20180802113542_vInzHQ_Screenshot.jpeg)

使用数组来放学生，最后一个学生的下标加1就是学生人数。

1. 先修改我自己个人的垃圾版本代码以满足该需求

```java
  	private Student[] myStudents;
	  private int studentNum;
	
	  public int getStudentsNum() {
        return studentsNum;
    }

    public void setStudentsNum(int studentsNum) {
        this.studentsNum = studentsNum;
    }
        public Student[] getStudents() {
        return students;
    }

    public void setStudents(Student[] students) {
        this.students = students;
    }
```

添加两个成员变量，并为其生成get set方法。构造方法中添加数组和学生数量初始化内容。这里的studentsNum定义成static的类属性更好。

```java
    public Subject(String name, String code, int year){
        this.setName(name);
        this.setCode(code);
        this.setYear(year);
        this.studentsNum = 0;
        this.students = new Student[100];
    }
```

编写学生报到或叫做添加学生的方法:

```java
    public void addStudent(Student student){
        int stuNum = this.getStudentsNum();
        this.getStudents()[stuNum] = student;
        this.setStudentsNum(++stuNum); //这里set的必须是前置加加
    }
```

```java
    public void showStudents(){
      int stuNum = this.getStudentsNum();
        for (int i=0;i<stuNum;i++) {
            System.out.println(this.name+"专业学生信息: ");
            System.out.println(students[i].getName());
        }
    }
```

```java
        System.out.println("----------");
        subject.addStudent(student1);
        subject.showStudents();
        System.out.println("----------");
        System.out.println("已有"+subject.getStudentsNum()+"人报名！");
```

运行结果:

![](http://myphoto.mtianyan.cn/20180802115937_QEMoS1_Screenshot.jpeg)

#### 官方实现

数组无论里面存放的是什么，它都是引用类型。

```java
	private Student[] myStudents;
	private int studentNum;
	
	public int getStudentNum() {
		return studentNum;
	}

	public void setStudentNum(int studentNum) {
		this.studentNum = studentNum;
	}
		public Student[] getMyStudents() {
		if(this.myStudents==null)
			this.myStudents=new Student[200];
		return myStudents;
	}
  public void setStudents(Student[] students) {
        this.students = students;
    }
```

![](http://myphoto.mtianyan.cn/20180802120622_Xd21X7_Screenshot.jpeg)

数组的容量和当前放置了多少元素的长度是两个不同的值。因此我们既要定义数组，又要定义当前用了的长度，后面我们会学到集合，将这两步操作合二为一。

```java
	public void addStudent(Student stu){
		/*
		 * 1、将学生保存到数组中
		 * 2、将学生个数保存到studentNum
		 * */
		//1、将学生保存到数组中
		for(int i=0;i<this.getMyStudents().length;i++){
			if(this.getMyStudents()[i]==null){
				stu.setStudentSubject(this);
				this.getMyStudents()[i]=stu;
				//2、将学生个数保存到studentNum
				this.studentNum=i+1;
				return;
			}
		}
	}
```

添加时遍历数组，寻找到第一个为null的位置填入，我觉得是不如我的填入策略的。

```java
package cn.mtianyan.test;

public class FloatTest {
    private static float [] f = new float[2];

    public static void main(String[] args) {
        System.out.println("f[0]="+f[0]);
    }
}
```

数组是对象，对象实例化之后都是有默认值的

![](http://myphoto.mtianyan.cn/20180802163823_hd89oH_Screenshot.jpeg)

### 解析: 数组未实例化造成的空指针异常

接下来我们针对案例实现中的两个常见问题进行一下讲解!

测试将学生数组实例化操作注释后的运行

```java
	public Student[] getMyStudents() {
//		if(this.myStudents==null)
//			this.myStudents=new Student[200];
		return myStudents;
	}
```

```java
Exception in thread "main" java.lang.NullPointerException
	at cn.mtianyan.model.Subject.addStudent(Subject.java:92)
	at cn.mtianyan.test.SchoolTest.main(SchoolTest.java:24)
```

会报出空指针异常。

方案一: 我在声明的时候就顺便进行初始化，或者在构造函数进行该值的初始化。
方案二: 用到的时候再进行创建。

这里方案一和方案二都是可行的。方案二在这个操作如果是一个耗时操作的时候更合适一点。















