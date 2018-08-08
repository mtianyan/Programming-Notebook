什么是线程？

要理解线程，我们得从进程说起。

进程的概念:

>进程是指可执行程序并存放在计算机存储器的一个指令序列,它是一个动态执行的过程。

![](http://myphoto.mtianyan.cn/20180808014048_HqW3h3_Screenshot.jpeg)

我们程序员边听音乐边写代码再挂着qq，这三个软件可以同时运行就是我们的进程在起作用。

Windows的任务管理可以看到进程。一个软件可以多个进程。

早期我们的计算机是单任务的，只能一个一个的运行，一个运行完了，才允许下一个的执行。

线程是比进程还要小的运行单位,一个进程包含多个线程。一个代码是由很多代码块组成，可以将代码块分到不同的线程执行。

线程可以看做一个子程序。程序的运行是靠cpu的，一个cpu情况下怎样才能保证程序的正常运行。

![](http://myphoto.mtianyan.cn/20180808112852_GhbSNg_Screenshot.jpeg)

将cpu的运行时间进行分片，时间片的轮转。

![](http://myphoto.mtianyan.cn/20180808112931_jp0XOF_Screenshot.jpeg)

什么是多线程？线程的创建(两种方式)，线程的状态和生命周期，线程调度，同步与死锁

### Thread和Runnable接口介绍

创建一个Thread类,或者一个Thread子类的对象。

创建一个实现Runnable接口的类的对象。

Thread是-个线程类,位于java.lang包下

|构造方法|说明|
|--------|----|
Thread()|创建一个线程对象|
Thread(String name)|创建一个具有指定名称的线程对象|
Thread(Runnable target)|创建一个基于Runnable接口实现类的线程对象|
Thread(Runnable target,String name)|创建一个基于Runnable接口实现类,并且具有指定名称的线程对象。

Thread类的常用方法

|方法|说明|
|----|----|
|public void run()|线程相关的代码写在该方法中，一般需要重写|
|public void start()|启动线程的方法|
|public static void sleep(long m)|线程休眠m毫秒的方法|
|public void join()|优先执行调用join()方法的线程

run方法中的代码可以被称为线程体。join抢占进程

Runnable接口 只有一个方法run();Runnable是Java中用以实现线程的接口;任何实现线程功能的类都必须实现该接口

### 通过Thread类创建线程

通过继承Thread类的方式创建线程类,重写run()方法。

```java
package cn.mtianyan.thread;
// 继承Thread，重写run 就是一个线程
class MyThread extends Thread{
	public void run(){
		System.out.println(getName()+"该线程正在执行！");
	}
}
public class ThreadTest {

	public static void main(String[] args) {
	    System.out.println("主线程1");
		MyThread mt=new MyThread();
		mt.start(); // 启动线程
        // 主方法本身主线程 和 My thread
//		mt.start(); // 线程只能启动一次
		System.out.println("主线程2");
	}

}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808114903_jGiOEt_Screenshot.jpeg)

### 通过Thread类创建线程下

```java
package cn.mtianyan.thread1;
class MyThread extends Thread{
	public MyThread(String name){
		super(name);
	}
	public void run(){
		for(int i=1;i<=10;i++){
			System.out.println(getName()+"正在运行"+i);
		}
	}
}
public class ThreadTest {

	public static void main(String[] args) {
		MyThread mt1=new MyThread("线程1");
		MyThread mt2=new MyThread("线程2");
		mt1.start();
		mt2.start();
	}

}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808115146_Ca3CM2_Screenshot.jpeg)

线程的具体运行顺序是随机的，有可能1先运行，有可能2先运行。

![](http://myphoto.mtianyan.cn/20180808115241_i7DVOb_Screenshot.jpeg)

有可能1，2交替运行。

### 实现Runnable接口创建线程

为什么要实现Runnable接口?

  - Java不支持多继承
  - 不打算重写Thread类的其他方法，这种方法更常用

```java
package cn.mtianyan.runnable;

class PrintRunnable implements Runnable {
	int i = 1; // 资源
	@Override
	public void run() {
		while (i <= 10)
			System.out.println(Thread.currentThread().getName() + "正在运行" + (i++));
	}

}

public class Test {

	public static void main(String[] args) {
		PrintRunnable pr = new PrintRunnable();
		Thread t1 = new Thread(pr);
		t1.start();
		// PrintRunnable pr1 = new PrintRunnable();
		Thread t2 = new Thread(pr);
		t2.start();

	} 

}
```

![](http://myphoto.mtianyan.cn/20180808143837_BU6wPN_Screenshot.jpeg)

此时i是t1 t2共享的资源，一共运行10次。

```java
	@Override
	public void run() {
		int i = 1; // 资源
		while (i <= 10)
			System.out.println(Thread.currentThread().getName() + "正在运行" + (i++));
	}
```

当资源在线程体内部时，则为该线程独占资源。会运行20次

![](http://myphoto.mtianyan.cn/20180808144041_F1cmBA_Screenshot.jpeg)

### 线程的状态和生命周期

新建(New)：创建一个Thread或Thread子类的对象时，进入新建状态。

可运行(Runnable)： 调用start方法进入可运行状态,就绪状态

正在运行(Running)： 一个Thread获取了cpu使用权就进入了正在运行状态。

阻塞(Blocked): 不再执行，缺少资源

终止状态(Dead)

![](http://myphoto.mtianyan.cn/20180808144740_5vHWoS_Screenshot.jpeg)

### sleep方法的使用

Thread类的方法

```java
public static void sleep(long millis)
```

作用在指定的毫秒数内让正在执行的线程休眠(暂停执行); 参数为休眠的时间，单位是毫秒

```java
package cn.mtianyan.sleep;

class MyThread implements Runnable{

	@Override
	public void run() {
		for(int i=1;i<=30;i++){
			System.out.println(Thread.currentThread().getName()+"执行第"+i+"次！");
			try {
				Thread.sleep(1000); // 一秒钟休眠一次
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}	
}
public class SleepDemo {

	public static void main(String[] args) {
		MyThread mt=new MyThread();
		Thread t=new Thread(mt);
		t.start();
		Thread t1=new Thread(mt);
		t1.start();
	}

}
```

运行结果: 每隔一秒刷新一次,共运行30次。

引入sleep作用: 计时，定期刷新数据。当休眠完成，线程并不能直接进入运行，只能进入就绪状态，等待cpu。

![](http://myphoto.mtianyan.cn/20180808150619_SkUa39_Screenshot.jpeg)

两个线程交替运行，因为一个休眠完可以立马接收另一个线程已经运行完的。总体来说还是有随机性的。

### join方法的使用

Thread类的方法

```java
public final void join()
```

作用:等待调用该方法的线程结束后才能执行，抢占资源优先执行。

```java
package cn.mtianyan.join;

class MyThread extends Thread{
	public void run(){
		for(int i=1;i<=5;i++)
		System.out.println(getName()+"正在执行"+i+"次！");
	}
}
public class JoinDemo {

	public static void main(String[] args) {
		MyThread mt=new MyThread();
		mt.start();
		try {
			mt.join(1);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		for(int i=1;i<=5;i++){
			System.out.println("主线程运行第"+i+"次！");
		}
		System.out.println("主线程运行结束！");
	}

}
```

因为mt使用了join方法抢占了主线程执行，因此一直都是Thread在前，主线程在后。

![](http://myphoto.mtianyan.cn/20180808151037_EbdvTW_Screenshot.jpeg)

Thread类的方法

```java
public final void join(long millis)
```

附带参数，毫秒。作用: 等待该线程终止的最长时间为millis毫秒。

![](http://myphoto.mtianyan.cn/20180808151258_ZzM982_Screenshot.jpeg)

可以看到，添加毫秒参数之后，主线程等待Thread运行了50次，一毫秒到期，就换主进程来执行了。

### 线程优先级

是否可以通过设置让某个线程优先执行呢?

Java为线程类提供了10个优先级;优先级可以用整数1-10表示,超过范围会抛出异常

主线程默认优先级为5 数字越大表示的优先级越高

优先级常量

MAX_PRIORITY :线程的最高优先级10 
MIN_PRIORITY :线程的最低优先级1 
NORM_PRIORITY :线程的默认优先级5 

改变获取线程优先级方法:

|方法|说明|
|----|----|
|public int getPriority()|获取线程优先级的方法|
|public void setPriority(int newPriority)|设置线程优先级的方法|

```java
package cn.mtianyan.priority;

class MyThread extends Thread{
	private String name;
	public MyThread(String name){
		this.name=name;
	}
	public void run(){
		for(int i=1;i<=10;i++){
			System.out.println("线程"+name+"正在运行"+i);
		}
	}
}
public class PriorityDemo {

	public static void main(String[] args) {
		// 获取主线程的优先级
		int mainPriority=Thread.currentThread().getPriority();
		System.out.println("主线程的优先级为："+mainPriority);
		MyThread mt1=new MyThread("线程1");
		MyThread mt2=new MyThread("线程2");
//		mt1.setPriority(10);
		mt1.setPriority(Thread.MAX_PRIORITY);
		mt2.setPriority(Thread.MIN_PRIORITY);
		mt2.start();
		mt1.start();
		System.out.println("线程1的优先级为："+mt1.getPriority());
	}

}
```

![](http://myphoto.mtianyan.cn/20180808153824_Gj5U9q_Screenshot.jpeg)

线程的执行和启动顺序，优先级大小，操作系统调度，当前资源等有大关系，具有很强随机性

### 线程同步

多线程运行问题

各个线程是通过竞争CPU时间而获得运行机会的;各线程什么时候得到CPU时间，占用多久,是不可预测的

一个正在运行着的线程在什么地方被暂停是不确定的

带来问题:

```java
package cn.mtianyan.bank;

public class Bank {
	private String account;		// 账号
	private int balance;		// 账户余额

	public Bank(String account, int balance) {
		this.account = account;
		this.balance = balance;
	}

	public String getAccount() {
		return account;
	}

	public void setAccount(String account) {
		this.account = account;
	}

	public int getBalance() {
		return balance;
	}

	public void setBalance(int balance) {
		this.balance = balance;
	}

	@Override
	public String toString() {
		return "Bank [账号：" + account + ", 余额：" + balance + "]";
	}

	// 存款
	public void saveAccount() {

		// 获取当前的账号余额
		int balance = getBalance();
		try {
			Thread.sleep(1000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		// 修改余额，存100元
		balance += 100;
		// 修改账户余额
		setBalance(balance);
		// 输出存款后的账户余额
		System.out.println("存款后的账户余额为：" + balance);
	}

	public void drawAccount() {
			// 在不同的位置处添加sleep方法

			// 获得当前的帐户余额
			int balance = getBalance();
			// 修改余额，取200
			balance = balance - 200;
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			// 修改帐户余额
			setBalance(balance);
			System.out.println("取款后的帐户余额：" + balance);

	}
}
```

```java
package cn.mtianyan.bank;
//取款
public class DrawAccount implements Runnable{
	Bank bank;
	public DrawAccount(Bank bank){
		this.bank=bank;
	}
	@Override
	public void run() {
		bank.drawAccount();
	}
	
}
```

```java
package cn.mtianyan.bank;
//存款
public class SaveAccount implements Runnable{
	Bank bank;
	public SaveAccount(Bank bank){
		this.bank=bank;
	}
	public void run(){
		bank.saveAccount();
	}
}
```

```java
package cn.mtianyan.bank;

public class Test {

	public static void main(String[] args) {
		// 创建帐户，给定余额为1000
		Bank bank=new Bank("1001",1000);
		// 创建线程对象
		SaveAccount sa=new SaveAccount(bank);
		DrawAccount da=new DrawAccount(bank);
		Thread save=new Thread(sa);
		Thread draw=new Thread(da);
		save.start();
		draw.start();
		try {
			
			draw.join();
			save.join();
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(bank);
	}

}
```

运行结果:

![](http://myphoto.mtianyan.cn/20180808154820_RRVmIX_Screenshot.jpeg)

可以看到由于线程执行顺序先后的不确定性，造成账号资金不一致情况。

存放还没有进行修改账户余额就被终止了，取款时以未增加之前的数字来取的。

为了保证在存款或取款的时候,不允许其他线程对帐户余额进行操作 需要将Bank对象进行锁定

使用关键字synchronized实现，确保共享对象，同一时刻只能被一个进程访问。这种机制称为线程同步，或者线程互斥。

synchronized关键字用在 成员方法 静态方法 语句块

```java
public synchronized void saveAccount(){}
public static synchronized void saveAccount(){}
synchronized(obj){......}
```

obj是我们需要锁定的对象

```java
	// 存款
	public synchronized void saveAccount() {

		// 获取当前的账号余额
		int balance = getBalance();
		try {
			Thread.sleep(1000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		// 修改余额，存100元
		balance += 100;
		// 修改账户余额
		setBalance(balance);
		// 输出存款后的账户余额
		System.out.println("存款后的账户余额为：" + balance);
	}

	public void drawAccount() {

		synchronized (this) {
			// 在不同的位置处添加sleep方法

			// 获得当前的帐户余额
			int balance = getBalance();
			// 修改余额，取200
			balance = balance - 200;
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			// 修改帐户余额
			setBalance(balance);
			System.out.println("取款后的帐户余额：" + balance);
		}

	}
```

![](http://myphoto.mtianyan.cn/20180808155556_8x8HNO_Screenshot.jpeg)

### 线程间通信

问题:帐户余额不够了怎么办? 等待存入足够的钱后处理

Queue类 里面存放n，两个线程一个生产，一个消费。

![](http://myphoto.mtianyan.cn/20180808155830_F6M1Jd_Screenshot.jpeg)

生产一个，取一个。

线程间通信: wait方法，中断方法的执行，使线程等待。

notify()方法: 唤醒处于等待的某一个线程,使其结束等待
notifyAll()方法: 唤醒所有处于等待的线程,使它们结束等待

```java
package cn.mtianyan.queue;

public class Queue {
	private int n;
	boolean flag=false; // false表示容器中没有数据了
	
	public synchronized int get() {
		if(!flag){
			try {
				wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
		System.out.println("消费："+n);
		flag=false; // 消费完毕，容器中没有数据
		notifyAll();
		return n;
	}

	public synchronized void set(int n) {
		if(flag){
			try {
				wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
		System.out.println("生产："+n);
		this.n = n;
		flag=true; // 生产完毕，容器中已经有数据
		notifyAll();
	}
	
}
```

一般使用noticeAll()，因为如果唤醒的单个线程还是我们刚休眠的生产线程，会继续死锁。

### 多线程总结

线程的概念
创建线程的两种方式

通过继承Thread类创建线程( MyThread )

```java
new MyThread().start()
```

通过实现Runnable接口创建线程(MyRunnable），Java不支持多继承，所以该方法更常用。

```java
new Thread(new MyRunnable()).start()
```

线程的状态和生命周期 线程的状态: 新建 可运行 运行 阻塞 终止

sleep方法， join方法

线程的优先级

同步概念，银行取款。

线程间通信

在下一集中，将带你领略Java输入输出流的风采。包括如何使用File类来操作文件和目录，字节流
和字符流的应用，以及Java的序列化与反序列化问题。































