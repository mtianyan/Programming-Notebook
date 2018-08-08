Java输入输出流

生活中无处不在，只要涉及到传输。复制粘贴操作;修改头像，将本地数据上传到网络服务器。

```java
System.out.println("mtianyan");
```

将字符串输出到屏幕上。

![](http://myphoto.mtianyan.cn/20180808165931_DXiuFN_Screenshot.jpeg)

字符从河流中依次通过，形成了字符流。

流就是指一连串流动的字符,以先进先出的方式发送信息的通道。

输出流: 屏幕，打印机等。

输入流: 从键盘接收数据。

![](http://myphoto.mtianyan.cn/20180808170056_8FrwCY_Screenshot.jpeg)

从键盘读取数据，输入到程序当中。文件，扫描仪都可以作为输入设备。

文件输入-读取 文件输出-写数据

#### 主要内容

File类的使用;字节流;字符流;对象的序列化与反序列化

### File类概述

什么是文件？

文件可认为是相关记录或放在一起的数据的集合;在Java中,使用java.io.File类对文件迸行操作。Windows分隔符和Linux分隔符的不同。

mkdirs 创建多级目录

```java
package cn.mtianyan.file;

import java.io.File;
import java.io.IOException;

public class FileDemo {
    public static void main(String[] args) throws IOException {
        File directory = new File("");
        String pathBase = directory.getAbsolutePath();
        // 创建File对象
//        File file1 = new File(pathBase+"/src/cn/mtianyan/file/hi.txt");
        File file = new File(pathBase);
        File file1 = new File(file,"/src/cn/mtianyan/file/hi.txt");
        System.out.println("是否是目录:"+file1.isDirectory());
        System.out.println("是否是文件:"+file1.isFile());


        // 创建单级目录
        File file2 = new File(pathBase,"Mtianyan");
        if (!file2.exists()){
            file2.mkdir();
        }
    }
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808171904_eS2CQs_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180808171839_4r1zNf_Screenshot.jpeg)

```java
        // 创建多级目录
        File file3 = new File(pathBase,"Mtianyan2/mtianyan");
        if (!file3.exists()){
            file3.mkdirs();
        }
```

![](http://myphoto.mtianyan.cn/20180808172017_rvE8sl_Screenshot.jpeg)

```java
        File file4 = new File(file,"/src/cn/mtianyan/file/error.txt");
        if (!file4.exists()){
            file4.createNewFile();
        }
```

![](http://myphoto.mtianyan.cn/20180808172317_i1ZoBg_Screenshot.jpeg)

### 字节流概述

字节输入流 InputStream

字节输出流 OutputStream

![](http://myphoto.mtianyan.cn/20180808172528_x3QbMU_Screenshot.jpeg)

重点介绍: File Buffer 对象

![](http://myphoto.mtianyan.cn/20180808172618_bjNJbN_Screenshot.jpeg)

### FileInputStream

从文件系统中的某个文件中获得输入字节

![](http://myphoto.mtianyan.cn/20180808172738_fhev5V_Screenshot.jpeg)

用于读取图像数据之类的原始字节流。

|方法名|描述|
|------|----|
|public int read()|从输入流中读取一个数据字节|
|public int read(byte[] b)|从输入流中将最多b.length个字节的数据读入一个byte数组中|
|public int read(byte[] b,int off, int len)|从输入流中将最多len个字节的数据读入byte数组中|
|public void close()|关闭此文件输入流并释放与此流有关的所有系统资源|

返回值为-1表示已经读到了文件的末尾。

### FileInputStream

```java
package cn.mtianyan.file;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class FileInputDemo1 {

	public static void main(String[] args) {
		File directory = new File("");
		String pathBase = directory.getAbsolutePath();
		//创建一个FileInputStream对象
		try {
			FileInputStream fis=new FileInputStream(pathBase+"/src/cn/mtianyan/file/hi.txt");
//			int n=fis.read();
			int n;
//			while(n!=-1){
//				System.out.print((char)n);
//				n=fis.read();
//			}
			while((n=fis.read())!=-1){
				System.out.print((char)n);
			}
			fis.close();
		}catch (FileNotFoundException e) {
			System.out.println("找不到文件");
			e.printStackTrace();
		} catch(IOException e){
			System.out.println("输入输出异常");
			e.printStackTrace();
		}
	}
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808181200_l8lxly_Screenshot.jpeg)

读取数据存放到字节数组

```java
package cn.mtianyan.file;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class FileInputDemo2 {

	public static void main(String[] args) {
		File directory = new File("");
		String pathBase = directory.getAbsolutePath();
		// 创建一个FileInputStream对象
		try {
			FileInputStream fis=new FileInputStream(pathBase+"/src/cn/mtianyan/file/hi.txt");
			byte[] b=new byte[15];
			fis.read(b,0,5);
			System.out.println(new String(b));
			fis.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808181934_sUN6ZQ_Screenshot.jpeg)

偏移量是5，所以只读出来了hello，如果不加偏移量可以全部读出来，这里String将bytes中全部连带空的部分都打印出来了。

### FileOutputStream

构造方法，追加，覆盖。

|方法名|描述|
|------|----|
|public void write(int b)|将指定字节写入此文件输出流|
|public void write(byte[] b)|将b.length个字节从指定byte数组写入此文件输出流中|
|public void write(byte[] b,int off,int len)|将指定byte数组中从偏移量off开始的len个字节写入此文件输出流|
|public void close()|关闭此文件输出流并释放与此流有关的所有系统资源|

```java
package cn.mtianyan.file;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputDemo {

	public static void main(String[] args) {
		FileOutputStream fos;
		FileInputStream fis;
		try {
			fos = new FileOutputStream("mtianyan.txt",true);
			fis=new FileInputStream("mtianyan.txt");
			fos.write(50);
			fos.write('a');
			System.out.println(fis.read());
			System.out.println((char)fis.read());
			fos.close();
			fis.close();

		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808182805_ybsTL0_Screenshot.jpeg)

存入50 a，读出来还是50 a。但由于编码问题，在文件里不是50a。

![](http://myphoto.mtianyan.cn/20180808182900_tT1sCW_Screenshot.jpeg)

### 文件的拷贝问题

```java
package cn.mtianyan.file;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputDemo1 {

	public static void main(String[] args) {
		// 文件拷贝
		try {
			FileInputStream fis=new FileInputStream("happy.gif");
			FileOutputStream fos=new FileOutputStream("happycopy.gif");
			int n=0;
			byte[] b=new byte[1024];
			while((n=fis.read(b))!=-1){
				fos.write(b,0,n);
			}
			fis.close();
			fos.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		}catch(IOException e){
			e.printStackTrace();
		}
		

	}

}
```

此时文件就被拷贝到同一个目录了

![](http://myphoto.mtianyan.cn/20180808183320_ahAQYG_Screenshot.jpeg)

拷贝之后的文件变大，最后一次写数据写多了。使用`fos.write(b,0,n);`解决

### 缓冲流

缓冲输入流BufferedInputStream;缓冲输出流BufferedOutputStream

缓冲区满了，会自动flush;不满时需要我们标明flush，否则出现

```java
java.io.IOException: Stream Closed
	at java.io.FileOutputStream.writeBytes(Native Method)
	at java.io.FileOutputStream.write(FileOutputStream.java:326)
	at java.io.BufferedOutputStream.flushBuffer(BufferedOutputStream.java:82)
	at java.io.BufferedOutputStream.flush(BufferedOutputStream.java:140)
	at java.io.FilterOutputStream.close(FilterOutputStream.java:158)
	at cn.mtianyan.file.BufferedDemo.main(BufferedDemo.java:27)
```

```java
package cn.mtianyan.file;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class BufferedDemo {

	public static void main(String[] args) {
		try {
			FileOutputStream fos=new FileOutputStream("mtianyan.txt");
			BufferedOutputStream bos=new BufferedOutputStream(fos);
			FileInputStream fis=new FileInputStream("mtianyan.txt");
			BufferedInputStream bis=new BufferedInputStream(fis);
			long startTime=System.currentTimeMillis();
			bos.write(50);
			bos.write('a');
			bos.flush();
			System.out.println(bis.read());
			System.out.println((char)bis.read());
			long endTime=System.currentTimeMillis();
			System.out.println(endTime-startTime);
			fos.close();
			bos.close();
			fis.close();
			bis.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		}catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808183910_Aack1s_Screenshot.jpeg)

close方法，会强制清空缓冲区写入。

```java
long startTime=System.currentTimeMillis();
```

加上系统时间记录，取的时间差。

### 字符流概述

字符输入流Reader 字符输出流 Writer

![](http://myphoto.mtianyan.cn/20180808184444_fQrPVN_Screenshot.jpeg)

![](http://myphoto.mtianyan.cn/20180808184550_lmwnDJ_Screenshot.jpeg)

一串字符 转换为字节 字节转为字符,网络聊天。

字节字符转换流: InputStreamReader;OutputStreamWriter;

```java
package cn.mtianyan.charstream;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class ReaderDemo {

	public static void main(String[] args) {
		try {
			FileInputStream fis=new FileInputStream("mtianyan.txt");
			InputStreamReader isr=new InputStreamReader(fis);
			BufferedReader br=new BufferedReader(isr);
			int n=0;
			char[] cbuf=new char[10];
// 读取代码
		    while((n=isr.read())!=-1){
		    	   System.out.print((char)n);
		    }
//			while((n=isr.read(cbuf))!=-1){
//				String s=new String(cbuf,0,n);
//				System.out.print(s);
//			}

			fis.close();
			isr.close();
			br.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		}
		catch (IOException e) {
			e.printStackTrace();
		}
	}

}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808192227_iMGlp3_Screenshot.jpeg)

```java
package cn.mtianyan.charstream;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class ReaderDemo {

	public static void main(String[] args) {
		try {
			FileInputStream fis=new FileInputStream("mtianyan.txt");
			InputStreamReader isr=new InputStreamReader(fis,"GBK");
			BufferedReader br=new BufferedReader(isr);
			FileOutputStream fos=new FileOutputStream("mtianyan1.txt");
			OutputStreamWriter osw=new OutputStreamWriter(fos,"GBK");
			BufferedWriter bw=new BufferedWriter(osw);
			int n;
			char[] cbuf=new char[10];
			while((n = (br.read(cbuf)))!=-1){
				bw.write(cbuf,0,n);
				bw.flush();
			}
			fis.close();
			fos.close();
			isr.close();
			osw.close();
			br.close();
			bw.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		}
		catch (IOException e) {
			e.printStackTrace();
		}
	}

}
```

![](http://myphoto.mtianyan.cn/20180808192257_ydCWgF_Screenshot.jpeg)

### 其他字符流

加入缓冲输入输出，加快速度。

```java
BufferedReader br=new BufferedReader(isr);
BufferedWriter bw=new BufferedWriter(osw);
```

### 对象序列化

把收到的信息发给另一个人。发送一个对象过去。

步骤: 创建一个类,继承Serializable接口; 创建对象;将对象写入文件;从文件读取对象信息

对象输入流ObjectInputStream
对象输出流ObjectOutputStream

```java
package cn.mtianyan.serial;

import java.io.Serializable;

public class Goods implements Serializable{
	private String goodsId;
	private String goodsName;
	private double price;
	public Goods(String goodsId,String goodsName,double price){
		this.goodsId=goodsId;
		this.goodsName=goodsName;
		this.price=price;
	}
	public String getGoodsId() {
		return goodsId;
	}
	public void setGoodsId(String goodsId) {
		this.goodsId = goodsId;
	}
	public String getGoodsName() {
		return goodsName;
	}
	public void setGoodsName(String goodsName) {
		this.goodsName = goodsName;
	}
	public double getPrice() {
		return price;
	}
	public void setPrice(double price) {
		this.price = price;
	}
	@Override
	public String toString() {
		return "商品信息 [编号：" + goodsId + ", 名称：" + goodsName 
				+ ", 价格：" + price + "]";
	}
	
}
```

```java
package cn.mtianyan.serial;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

public class GoodsTest {

	public static void main(String[] args) {
		// 定义Goods类的对象
		Goods goods1 = new Goods("gd001", "电脑", 3000);
		try {
			FileOutputStream fos = new FileOutputStream("goods.txt");
			ObjectOutputStream oos = new ObjectOutputStream(fos);
			FileInputStream fis = new FileInputStream("goods.txt");
			ObjectInputStream ois = new ObjectInputStream(fis);
			// 将Goods对象信息写入文件
			oos.writeObject(goods1);
			oos.writeBoolean(true);
			oos.flush();
			// 读对象信息
			try {
				Goods goods = (Goods) ois.readObject();
				System.out.println(goods);
			} catch (ClassNotFoundException e) {
				e.printStackTrace();
			}
			System.out.println(ois.readBoolean());

			fos.close();
			oos.close();
			fis.close();
			ois.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}

	}

}
```

![](http://myphoto.mtianyan.cn/20180808193135_A7oCcO_Screenshot.jpeg)

### 课程总结

流的概念 File类的使用 字节流 字符流 对象的序列化与反序列化

课程完结，后期有时间了添加一个综合应用知识的音乐播放器案例。

