字符串处理类。

常用的:  String类和StringBuilder类

Java中字符串是被作为一个String类型的对象来处理的。这节课我们就来了解这个类的其他方法和特性。

### 主要内容

如何创建String对象; String对象的常用方法; ==和equals方法的区别;String对象的特性不可变性

### String常用方法简介

为什么要学习字符串

比如我们要上传一个图片，要求必须是图片格式(jpg gif等),对于上传的文件名称进行判断，看是否是图片格式。

注册用户要求提供邮箱，正确的邮箱，邮箱格式校验。

创建String对象的方法:

创建String对象的方式不止三种,这里先介绍 常用的

```java
String s1= "mtianyan";
```

>创建一个字符串对象mtianyan ,名为s1

```java
String s2=new String();
```

>创建一个空字符串对象,名为s2

```java
String s3=new String("mtianyan");
```

>创建一个字符串对象mtianyan,名为s3

String中的常用方法:

|方法|说明|
|----|----|
|int length()|返回当前字符串的长度|
|int indexOf(int ch)|查找ch字符在该字符串中第一次出现的位置|
|int indexOf(String str)|查找str子字符串在该字符串中第一次出现的位置|
|int lastIndexOf(int ch)|查找ch字符在该字符串中最后一次出现的位置|
|int lastIndexOf(String str)|查找str子字符串在该字符串中最后一次出现的位置|
|String substring(int beginIndex)|获取从beginIndex位置开始到结束的子字符串|
|String substring(int beginIndex, int endIndex)|获取从beginIndex位置开始到endIndex位置的子字符串|
|String trim()|返回去除了前后空格的字符串|
|boolean equals(Object obj)|将该字符串与指定对象比较，返回true或false|
|String toLowerCase() |将字符串转换为小写|
|String toUpperCase() |将字符串转换为大写|
|char charAt(int index)|获取字符串中指定位置的字符|
|String[] split(String regex, int limit) |将字符串分割为子字符串，返回字符串数组|
|byte[] getBytes()|将该字符串转换为byte数组|

### String常用方法(上）

```java
package cn.mtianyan.string;

public class StringDemo1 {

	public static void main(String[] args) {
		// 定义一个字符串"JAVA 编程 基础"
		String str="JAVA 编程 基础";
		// 打印输出字符串的长度
		System.out.println("字符串的长度是："+str.length());

		// 取出字符'程'并输出
		System.out.println(str.charAt(6));
		
		// 取出子串"编程 基础"并输出
		System.out.println(str.substring(5));
		
		// 取出子串"编程"并输出
		System.out.println(str.substring(5, 7));
	}

}
```

字符串长度是包括空格的。

关于字符串索引

![](http://myphoto.mtianyan.cn/20180806161613_ThSo3d_Screenshot.jpeg)

运行结果:

![](http://myphoto.mtianyan.cn/20180806161829_gQSep6_Screenshot.jpeg)

substring两个参数时，第二个参数是下一个字符的index值。

### String常用方法(下)

indexOf() 和 lastIndexOf方法

```java
package cn.mtianyan.string;

public class StringDemo2 {

	public static void main(String[] args) {
		// 定义一个字符串"JAVA编程基础，我喜欢java编程"
		String str=new String("JAVA编程基础，我喜欢java编程");
		
		// 查找字符'A'在字符串中第一次出现的位置
		System.out.println("字符'A'在字符串中第一次出现的位置"+str.indexOf('A'));

		// 查找子串"编程"在字符串中第一次出现的位置
		System.out.println("子串\"编程\"在字符串中第一次出现的位置"+str.indexOf("编程"));
		
		// 查找字符'A'在字符串中最后一次出现的位置
		System.out.println("字符'A'在字符串中最后一次出现的位置"+str.lastIndexOf('A'));
		
		// 查找子串"编程"在字符串中最后一次出现的位置
		System.out.println("子串\"编程\"在字符串中最后一次出现的位置"+str.lastIndexOf("编程"));
		
		// 在字符串index值为8的位置开始，查找子串"编程"第一次出现的位置
		System.out.println("在字符串index值为8的位置开始，查找子串\"编程\"第一次出现的位置"+str.indexOf("编程", 8));
	}

}
```

字符串中出现双引号要转义。

运行结果:

![](http://myphoto.mtianyan.cn/20180806163207_IZUpCT_Screenshot.jpeg)

#### 编程练习

使用String类常用方法完成字符串处理。任务
  
    1. 定义一个字符串”abcdefg"
    2. 取出子串cde并转换为大写
    3. 将DE替换为MM
    4. 最后得到结果CMM

```java
package cn.mtianyan.string;

public class Exercise {
    public static void main(String[] args) {
        String one = new String("abcdefg");
        String two = one.substring(2,5).toUpperCase();
        System.out.println(two);
        two =two.substring(0,1)+"MM";
        System.out.println(two);
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180806164155_QrL5Zz_Screenshot.jpeg)

### 字符串与bytes数组间的相互转换

String类中getBytes方法使用。

实际开发中，数据传输到网络上，网络上传输的数据是二进制字节型的，我们需要把字符串转换成二进制进行传输。同样，接收到数据之后，我们需要把字节数据转换为字符串。

```java
package cn.mtianyan.string;

import java.io.UnsupportedEncodingException;

public class StringDemo3 {

	public static void main(String[] args) throws UnsupportedEncodingException {
		// 字符串和byte数组之间的相互转换
		// 定义一个字符串
		String str=new String("JAVA 编程 基础");
		// 将字符串转换为byte数组，并打印输出
		byte[] arrs=str.getBytes();
		for(int i=0;i<arrs.length;i++){
			System.out.print(arrs[i]+" ");
		}
	}

}
```

打印输出的都是一些二进制的字节的数据。1(byte)=8位(bit) 这些数据是与编码有关的。

运行结果:

![](http://myphoto.mtianyan.cn/20180806165144_NoGRpr_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180806165050_v2sbyF_Screenshot.jpeg)

```java
		System.out.println();
		// 将byte数组转换为字符串
		String str1=new String(arrs);
		System.out.println(str1);
```

此时运行结果:

![](http://myphoto.mtianyan.cn/20180806165305_D5Imcx_Screenshot.jpeg)

此时我们的编码和解码使用的编码格式是一致的，都是默认不填的值。

```java
package cn.mtianyan.string;

import java.io.UnsupportedEncodingException;

public class StringDemo3 {

	public static void main(String[] args) throws UnsupportedEncodingException {
		// 字符串和byte数组之间的相互转换
		// 定义一个字符串
		String str=new String("JAVA 编程 基础");
		// 将字符串转换为byte数组，并打印输出
		byte[] arrs=str.getBytes();
		for(int i=0;i<arrs.length;i++){
			System.out.print(arrs[i]+" ");
		}

		System.out.println();
		// 将byte数组转换为字符串
		String str1=new String(arrs,"GBK");
		System.out.println(str1);
	}
}
```

UnsupportedEncodingException为不支持编码异常,在字符编码有问题时触发。

运行结果:

![](http://myphoto.mtianyan.cn/20180806165527_AduabO_Screenshot.jpeg)

可以看到此时中文出现了乱码情况，解决方案: 将两者编码保持一致

```java
	public static void main(String[] args) throws UnsupportedEncodingException {
		// 字符串和byte数组之间的相互转换
		// 定义一个字符串
		String str=new String("JAVA 编程 基础");
		// 将字符串转换为byte数组，并打印输出
		byte[] arrs=str.getBytes("GBK");
		for(int i=0;i<arrs.length;i++){
			System.out.print(arrs[i]+" ");
		}

		System.out.println();
		// 将byte数组转换为字符串
		String str1=new String(arrs,"GBK");
		System.out.println(str1);
		
	}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180806165623_Cest95_Screenshot.jpeg)

小结:

字符串和byte数组间的相互转换;编码问题: GBK编码和UTF-8编码

### 等于运算符与equals方法的区别

```java
package cn.mtianyan.string;

public class StringDemo5 {

	public static void main(String[] args) {
		// ==和equals方法的区别
		// 定义三个字符串，内容都是mtianyan
		String str1="mtianyan";
		String str2="mtianyan";
		String str3=new String("mtianyan");
		System.out.println("str1和str2的内容相同？"+(str1.equals(str2)));
		System.out.println("str1和str3的内容相同？"+(str1.equals(str3)));
		
		System.out.println("str1和str2的地址相同？"+(str1==str2));
		System.out.println("str1和str3的地址相同？"+(str1==str3));
	}
}
```

![](http://myphoto.mtianyan.cn/20180806170008_gVHF0a_Screenshot.jpeg)

equals是字符串内容相同就可以。new 开辟新的内存空间。 ==指地址是否相同。

内存空间，有栈存放类的引用，常量池存放字符串常量，堆里存放new创建的字符串对象

![](http://myphoto.mtianyan.cn/20180806170422_EuxDjb_Screenshot.jpeg)

当我们执行语句

```java
		String str1="mtianyan";
		String str2="mtianyan";
```

栈中就有了一个str1的引用,常量池中生成一个mtianyan，并且str1的引用指向常量池中"mtianyan"；
当str2语句执行，同样是栈中生成str2引用，常量池生成"mtianyan" 这时候发现常量池已经有了，不会在常量池中新增。将str2也指向mtianyan

str3即使有一条相同的语句str4(new)。都会在栈中有str3和4的引用，堆中生成两个String对象，地址不同。

### 字符串的不可变性

```java
package cn.mtianyan.string;

public class StringDemo6 {

	public static void main(String[] args) {
		// String的不可变性
		// String对象一旦被创建，则不能修改，是不可变的
		// 所谓的修改其实是创建了新的对象，所指向的内存空间不变
		String s1="mtianyan";
		String s2="hello,"+s1;
		// s1不再指向mtianyan所在的内存空间，而是指向了"hello,mtianyan"
		System.out.println("s1="+s1);
		System.out.println("s2="+s2);

		String s3=new String("hello,mtianyan!");
		System.out.println("子串:"+s3.substring(0,5));
		System.out.println("s3="+s3);
	}

}
```

new String会在堆中生成实例化String对象，而substring的结果会在常量池中生成。因为String是不可变的，所以我们必须要有临时变量来重新指向它改变后的值。

### StringBuilder

String和StringBuilder的区别: String具有不可变性,而StringBuilder不具备。

建议: 当频繁操作字符串时,使用StringBuilder。

>因为String是不可变的，中间变量多余。

StringBuilder和StringBuffer二者基本相似:

StringBuffer是线程安全的, StringBuilder则没有,所以性能略高，后面我们会学到线程。字符串处理一般都是单线程，我们使用StringBulider就行了。

java.lang包中包含

即使我们使用默认的无参构造方法，仍然会开辟一个16字节的内存空间。与String类一样可以传入字符数组。

append方法，在末尾增加内容。delete删除内容。insert插入内容。length返回字符串长度，replace方法替换。

### StringBuilder常用方法

```java
public class StringBuilderDemo1 {

	public static void main(String[] args) {
		// 定义一个字符串"你好"
		StringBuilder str=new StringBuilder("你好");
		// 在"你好"后面添加内容，将字符串变成"你好，mtianyan!"
		   str.append(',');
	   	 str.append("mtianyan!");
	     System.out.println("str="+str);
	     System.out.println("str="+str.append(',').append("mtianyan!"));
	}
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180806182350_odau3J_Screenshot.jpeg)

```java
		// 将字符串变成"你好,MTIANYAN ！"
		// 两种方式：
		// 1. 使用delete方法删除mtianyan，然后再插入MTIANYAN
		System.out.println("替换后："+str.delete(3,str.length()).insert(3, "MTIANYAN!"));
		// 2. 使用replace方法直接替换
		System.out.println("替换后："+str.replace(3,str.length(),"MTIANYAN!"));
		
		// 在字符串"你好，MTIANYAN!"中取出"你好"并输出
		System.out.println(str.substring(0,2));
		System.out.println(str);
```

运行结果:
 
![](http://myphoto.mtianyan.cn/20180806182856_YkJrnc_Screenshot.jpeg)

小结:

```java
StringBuilder append(String str)
StringBuilder delete(int start, int end)
StringBuilder insert(int offset, String str)
StringBuilder replace(int start, int end, String str)
```

### 课程总结

String和StringBuilder StringBuffer

介绍了这两个类的常用方法

在String中介绍了 == 和 equals() 方法的区别

介绍了String和StringBuilder的区别,主要是String的不可变性

通过学习，进一步掌握java文档的使用

下集预告: 我们将学习Java中的集合。































