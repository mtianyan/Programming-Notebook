Linux C语言编程基本原理与实践(2018-06-16 19:12:15)

## Linux C语言编程基本原理与实践

高效的学习带着目的性: 是什么 -> 干什么 -> 怎么用

### 重识C语言

1. C语言是一种通用的, 面向过程的编程语言, 在系统与应用软件的开发应用较广
2. 是人类和计算机交流的一种方式
3. ANSI C： 是C语言的标准, 为了避免各开发商用的C语言语法的差异
4. C语言的特点: 简单, 快速, 高性能, 兼容性好, 功能强大, 易于学习

![mark](http://myphoto.mtianyan.cn/blog/180604/IC5jjKjCfK.png?imageslim)

#### C语言适合做什么

1. Linux嵌入式, 小工具(命令行下的cd, ls之类的命令) 小巧灵活，语法简单，适合做小工具
2. 与硬件打交道的程序: 操作系统, ARM嵌入式, 单片机编程以及Arduino编程等等
3. 对性能要求较高的应用程序: NGINX(C)的并发量 = Apache(C++) * 10

#### C适合领域
1. 小工具（语法简单）
2. 和硬件打交道的程序 ARM嵌入式，单片机，Arduino编程（有指针，可操作内存）
3. 有高性能要求的程序

>nginx:c apache:c++ 

linux嵌入式

### 开发环境与配置：

- C语言是随着UNIX诞生而产生的一门编程语言
- Mac电脑是Unix内核; Windows下可以安装Linux虚拟机

Ubuntu：

  1. Ubuntu和CentOS是较为常用的Linux发行版本, 个人电脑用Ubuntu更好
  2. Ubuntu的kylin版对中文支持很好
  3. amd64版: AMD当初率先推出64位CPU, 所以Ubuntu把64位CPU型号定义为amd64(Intel照用), 一直沿用到现今; 32位用x86
  4. LTS版: 长时间的技术支持版本
  5. 装Ubuntu系统可以选择双系统, 也可在原来的Windows电脑上装虚拟机

PS: 尽量在Linux环境下开发C语言程序

#### 常用指令

- 终端编辑器：emacs vim
- 安装软件：`sudo apt install 【软件名】`
- 更新软件：`sudo apt update`

- `Ctrl+Alt+T`：打开终端
- `cd ~`     ：进入当前用户的根目录
- `pwd`       ：查看当前所在路径
- `ls`        ：当前章目录包含哪些文件
- `ls -l`     :显示当前文件的类型，权限，创建时间，名字
- `ls -al`或`ll`:显示隐藏文件

>如果前面是`d`就是文件夹,`-`就是普通类型的文件

- `touch **`  ：创建字符型文件
- `rm **`     ：删除
- `mkdir **`  :创建目录(文件夹)
- `vi **`     ：打开(进入)文件

>vi 一个不存在的文件，进入后无法输入内容，因当前在命令模式下；按字符i，可进入INSERT插入模式，就可输入内容，按Esc返回命令模式;

在**命令模式**下：

- `:w`      ：保存该文件
- `:q`      ：退出
- `i`       ：当前光标前面插入字符
- `Shift+i` ：跳到本行行首插入字符
- `a`       ：当前光标后面插入字符
- `Shift+a` ：跳到本行末尾插入字符
- `o`       ：在当前下一行插入字符
- `Shift+o` ：在当前上一行插入字符
- `x`       ：删除当前光标所处字符
- `d+d`     ：删除整行

Linux下最好用的文本编辑器: emacs, vim

- `cc -v(gcc -v)`: 查看编译器版本

- apt-get是一条linux命令，适用于deb包管理式的操作系统，主要用于自动从互联网的软件仓库中搜索、安装、升级、卸载软件或操作系统。

- `clear`：清洁屏幕

### Linux下第一个C程序

linux下一般不用`void main`，最新c语言标准，`int main`

```c
#include <stdio.h>

int main()
{
    printf("hello,world!\n");
    return 0;
}
```

```
cc a.c
```

默认会为我们编译并生成可执行文件a.out(可读可写可执行)

![mark](http://myphoto.mtianyan.cn/blog/180615/Bf9c6kllB8.png?imageslim)

- `./`表示当前路径下，
- `./a.out` 执行当前路径下的a.out文件
- `r`表示可读  `w`表示可写  `x`表示可执行

三组重复的顺序为"创建者","用户组","任意其他用户"

### 多个源文件分而治之

c语言是一个结构化的程序语言，是支持多函数的。程序可由若干个函数组成。

```c
vim hello.c
```

最原始版本的实现(hello.c):

```c
#include <stdio.h>

int max(int a, int b)
{
    if(a>b){
        return a;      
    }else{
        return b;
    }
}

int main()
{
    int a1 = 33;
    int a2 = 21;
    int maxNum = max(a1,a2);
    printf("the max value is %d\n",maxNum);
    return 0;
}
```

- 我们的stdio.h是在我们的user/include中被内置了

![mark](http://myphoto.mtianyan.cn/blog/180615/5aCh7EL6aL.png?imageslim)

- 在编写max函数时对齐，编写内部时括号进行缩进对齐。

![mark](http://myphoto.mtianyan.cn/blog/180615/j8DeEB9aBm.png?imageslim)

附加知识: vim分屏显示

- `:sp 文件名` //创建（打开）新文件
- 上屏: `ctrl+w+上箭头`
- 下屏: `ctrl+w+下箭头`
- 打开行号 `:set nu`
- 剪切：(最后一行行数)+dd
- 粘贴：p

//这两个不用点冒号

![mark](http://myphoto.mtianyan.cn/blog/180615/B5CA9Ig1db.png?imageslim)

- 关闭行号：set nonu

![mark](http://myphoto.mtianyan.cn/blog/180615/mE1bdJFica.png?imageslim)

>如果就是上图代码直接编译会报错，这是一个未声明的函数。

>有两种分离方案: 


- 第一种是`int max(int a,int b);`,在hello.c中声明该方法，然后编译的时候需要加上max.c
- 一种是`#include "max.c"` 然后编译的时候就不需要加上max.c一起编译

**版本1:**

0-hello.c:

```c
#include <stdio.h>
int max(int a,int b);

int main()
{
    int a1 = 33;
    int a2 = 21;
    int maxNum = max(a1,a2);
    printf("the max value is %d\n",maxNum);
    return 0;
}
```

0-max.c:

```c
int max (int a, int b)
{
    if(a>b){
	    return a;
    }else{
	    return b;
    }
}
```

编译命令:

```c
gcc 0-hello.c 0-max.c -o 0-hello.out
```

如果不加上0-max.c一起编译，会出现错误

```
gcc 0-hello.c -o 0-hello.out
/tmp/cc8GuaAH.o：在函数‘main’中：
0-hello.c:(.text+0x21)：对‘max’未定义的引用
collect2: error: ld returned 1 exit status
```

**版本2**

1-hello.c:

```c
#include <stdio.h>
#include "0-max.c"

int main()
{
    int a1 = 33;
    int a2 = 21;
    int maxNum = max(a1,a2);
    printf("the max value is %d\n",maxNum);
    return 0;
}
```

0-max.c与原来的一致

编译命令:
```c
gcc 1-hello.c -o 1-hello.out
```

如果此时多加了0-max.c一起编译

```c
gcc 1-hello.c 0-max.c -o 1-hello.out
/tmp/ccjcCmVa.o：在函数‘max’中：
0-max.c:(.text+0x0): `max'被多次定义
/tmp/cclIxMtD.o:1-hello.c:(.text+0x0)：第一次在此定义
collect2: error: ld returned 1 exit status
```

终端下：

- `gcc 文件名.c -o 命名.out`
- 生成.out并命名
- `#include <>`表示在预装的库里查找
- `#include "max.c"`表示在当前目录内查找文件

>`include "max.c"`相当于把整个函数复制进来了。效果等同于写进来

- `wqa` 是将多个文件一起保存

### 头文件与函数定义分离

>把函数的声明和定义分离开来

代码没有main函数不能执行，main是入口。

- .h 头文件
- .o 编译之后的中间文件
- .c 源代码

```
mtianyan@ubuntu:~/Desktop/zjuPlan/CSF878/CCode/linux_c/2-lesson/part1$ ls
0-max.c  1-hello.c
```

加快编译速度

```
gcc -c 0-max.c -o 0-max.o
```

将max.c变成max.o之后，我们需要把hello.c中的include注释掉并添上方法声明

```c
#include <stdio.h>
//#include "0-max.c"
int max(int a,int b);
```

可读可写不可执行,max.o相当于计算器对于源代码进行了翻译，变成计算机可识别的机器码

```c
gcc 0-max.o 1-hello.c -o 1-hello.out
```

新建一个min.c

```c
int min (int a, int b)
{
    if(a<b){
	    return a;
    }else{
	    return b;
    }
}
```

hello.c中进行minNum的调用

```c
#include <stdio.h>
//#include "0-max.c"
int max(int a,int b);
int min(int a,int b);

int main()
{
    int a1 = 33;
    int a2 = 21;
    int maxNum = max(a1,a2); 
    int minNum = min(a1,a2);
    printf("the max value is %d\n",maxNum); 
    printf("the min value is %d\n",minNum);
    return 0;
}
```

编译命令：

```
gcc -c min.c -o min.o
```

```
gcc 0-max.o min.o 1-hello.c -o 2-hello.out
```

加快编译速度。不会再修改的函数，公共框架和公共类编译生成静态库。

**gcc的编译流程分为4步：**

预处理(Pre-Processing) －> 编译(Compling) -> 汇编(Assembling) -> 连接(Linking) 

预处理: 处理`#include` `#define` `#ifdef` 等宏命令

编译: 把预处理完的文件编译为汇编程序`.s`

汇编: 把汇编程序`.s`编译为`.o`二进制文件

- `gcc -c min.c -o min.o`  //把文件min.c预编译成文件min.o
- `cp 文件名a  文件b`       //把文件a拷贝成新的文件b
- 使用`yy`复制一行   使用 `行号n+yy`复制n行    
- 使用`p`对复制的行进行粘贴
- 源代码文件用`cat`命令可以查看

那么问题又来了，我们现在的max函数和min函数是自己编写的，即使不加声明，我们也知道需要哪些参数，参数是什么类型，返回值是什么类型。如果这个函数不是我们编写的，别人又编写成了max.o min.o 我们看不到源代码，又不知道函数的传入参数与返回。`.h`文件的好处就来了

我们创建一个文件夹part2

max.h 代码：

```c
int maxNum(int a, int b);
```

min.h 代码：

```c
int minNum(int a ,int b);
```

hello.c代码：

```c
#include <stdio.h>
#include "max.h"
#include "min.h"

int main()
{
    int a1 = 33;
    int a2 = 21;
    int maxNum = max(a1,a2); 
    int minNum = min(a1,a2);
    printf("the max value is %d\n",maxNum);
    printf("the min value is %d\n",minNum);
}
```

![mark](http://myphoto.mtianyan.cn/blog/180616/kLlGmD172C.png?imageslim)

```
gcc max.o min.o hello.c -o hello.out
```

```c
warning: implicit declaration of function ‘max’; did you mean ‘main’? 
```

>出现警告，但不影响正常的编译运行。

### makFile的编写

- make工具可以将大型的开发项目分成若干个模块
- `make -v`
- `sudo apt-get install make`
- make工具可以很清晰和很快捷的整理源文件

make工具的内部也是使用的gcc

>我们自己开发还是安装软件都要使用到`make` 和`make install`这两个命令

因为当我们的源文件很多很多的时候

```
gcc max.c min.c hello.c -o hello.out
```

命令就会很长很长。

编写一个Makefile可以同时编译多个文件，告诉依赖关系。

-  vim Makefile
-  写入：

```c
hello.out:max.o min.o hello.c
	  gcc max.o min.o hello.c -o hello.out
max.o:max.c
	  gcc -c max.c
min.o:min.c
	  gcc -c min.c
# 添加注释
```

-  执行命令`make`

>编写 Makefile 缩进使用 tab 键(八个空格，否则出错)

```c
Makefile:3: *** 遗漏分隔符 (null)。 停止。
```

- 重命名文件 `mv MakeFile makefile`

从上往下找，从下往上编译出来。 已经生成出来的文件不会再重新生成。

```c
make: “hello.out”已是最新。 （up to date）
```

### 详细讲解main函数中的返回值的作用以及main函数中的参数意义

![mark](http://myphoto.mtianyan.cn/blog/180616/9k8Ef5E5bF.png?imageslim)

main.c:

```c
#include <stdio.h>

int main(int argc,char* argv[]) //main函数完整形式
{
    printf("hello,world\n");
    return 101;
}
```

```
gcc main.c -o main.out && ./main.out
```

- `gcc main.c -o main.out && ./ main.out` 可以依次执行两条命令
- `return 0` 用来验证程序运行是否成功。
- 命令`echo $?`用来查看返回值

![mark](http://myphoto.mtianyan.cn/blog/180616/lmjHJbaG7a.png?imageslim)

`./main.out && ls`打印出helloworld的同时，列出当前目录。因为main.out的return值为0，判定为成功执行。

`./main2.out && ls`打印出helloworld，未列出当前目录。因为main.out的return值为101（非0），判定为不成功执行。

### main函数中的参数

```c
int main(int argc, char* argv[])//main函数完整形式
```
argc统计输入参数的个数。只输入文件名时个数为1

`argv[]`存放每个参数的内容
如：

- 输入  ./main3.out -l -a
- argv = 3
- argc[0] = ./main.out
- argc[1] = -l
- argc[2] = -a

>argc(argument count),存放着传入main函数的参数个数是几个。

>argv(argument vector)，存放具体传入的参数

main3.c:

```c
#include <stdio.h>

int main(int argc,char* argv[])
{
    printf("argc is %d\n",argc);
    //int i;
    for(int i =0;i<argc;i++){
	printf("argv[%d]is %s\n",i,argv[i]);
    }

    return 101;
}
```

```
$ ./main3.out -a -l
argc is 3
argv[0]is ./main3.out
argv[1]is -a
argv[2]is -l
```

### Linux下的标准输入流输出流与错误流

- C语言是如何被操作系统调用的
- 操作系统如何传递参数
- main函数的返回值含义

linux把所有东西当作文件处理

- 标准输入流文件：`stdin` 键盘
- 标准输出流文件：`stdout` 显示器
- 标准错误流文件：`stderr`
- 这是系统默认创建
- `fprintf fscanf`：将输入输出放入...
- `printf("")` 是对`fprintf(stdout,"")`函数的封装.
- `scanf("")` 是对`fscanf(stdin,"")`函数的封装

```c
#include <stdio.h>

int main()
{
    // printf("hello world!\n");
    fprintf(stdout,"hello world \n");
    int a;
    //scanf("%d",&a);
    fscanf(stdin,"%d",&a);
    if(a<0){
	 fprintf(stderr,"the value must >0\n");
	 # 返回值不等于0表明函数出错
	 return 1;
    }

    //printf("input value is: %d\n",a);
    return 0;

}

```

### 输出输出流与错误流的重定向

Linux几乎可以用于任何领域，这里我们不得不提出linux的通道。
`管道`起到了很重要的作用，**不同应用程序之间要配合使用**，就需要用到管道。

**Demo:**main.c
>先理解输入流，输出流和错误流的**重定向机制**，对于管道的理解会比较容易些。

```c
#include <stdio.h>

int main()
{
int i,j;
printf("input the int value i:\n"); \\printf其实对fprintf的封装，是从标准输出流（即stdout）来输出这个过程
scanf("%d", &i); //默认输入流是键盘
printf("input the int value j:\n");
scanf("%d", &j);
printf("i+j=%d\n", i+j);
}
```

- 执行编译命令`cc main.c`, 得到`a.out`，运行a.out，我们分别输入3和5输入到终端.

- 我们可以使用命令`./a.out 1>> a.txt`,其中`>>`符号（不写参数就是输出流），之前默认输出流是终端，现在我们则改为输出到a.txt中，我们执行命令后，分别输入3回车后再输入5。再使用命令cat a.txt，我们可以看到我们已经输出到文件里的内容。

![mark](http://myphoto.mtianyan.cn/blog/180616/bC7b1C8B5d.png?imageslim)

我们标准输出流是`1>>`,输入流是`0>>`

- 我们再次执行`./a.out >> a.txt`，我们再次输入参数，完成后我们再次使用`cat`来查看a.txt文件里的内容，发现之前的内容还在，新的输出内容**追加到了后面**。

- 再举一个重定向的例子，我们使用命令`ls /etc >> etc.txt`，我们将ls目录下的内容输入到了etc.txt文件中

- 但我们如若改重定向符号想覆盖掉之前的内容，可以把双箭头`>>`改为单箭头`>`，则文件中先前的内容就会被覆盖掉。

### 输入流重定向

- 我们可以创建一个文件vi input.txt，内容如下：

```c
18
9
```

- 我们再次执行`./a.out < input.txt`，不存在追加模式，所以我们用单箭头`<`，我们可以将要输入的内容全部在input.txt中准备好，命令执行后，我们便在终端上可以看到结果。

![mark](http://myphoto.mtianyan.cn/blog/180616/giKGFDhG55.png?imageslim)

```c
#include <stdio.h>

int main()
{
	int i,j;
	printf("input the int value i:\n"); 
	scanf("%d", &i); //默认输入流是键盘
	printf("input the int value j:\n");
	scanf("%d", &j);
	if(0!=j){	
	    printf("%d/%d=%d\n",i,j,i/j);
	}else{
	    fprintf(stderr,"j != 0\n");
	    return 1;
	
	}


	return 0;
}

```

>注意代码规范小技巧，0和j的比较，0放前面如果漏了等号会报错

`echo $?` 查看返回值

```
./main.out 1>true.txt 2>false.txt < input.txt
```

- 将输出保存到t.txt.
- 错误保存到f.txt.
- 从input.txt读入数据

![mark](http://myphoto.mtianyan.cn/blog/180616/a8E9449J28.png?imageslim)

而当值错误，产生除零错误时。

![mark](http://myphoto.mtianyan.cn/blog/180616/f0KJHI60f3.png?imageslim)

>上图是当j=0时的运行情况。

![mark](http://myphoto.mtianyan.cn/blog/180616/dh9kB6c7Bl.png?imageslim)

重定向到其他地方。

### 管道原理及应用。

管道：

把前面的输出流作为后面工具的输入流，用一个`|`表示.

-  `grep` :查看指定文本，搜出包含字符的文本

- 终端中输入: `ls /etc/ | grep ab`

>- `ls /etc/` 的输出作为`grep`的输入
- `ls /etc/ | grep ab` 在/etc/文件下查找含有ab字符的文件名

![mark](http://myphoto.mtianyan.cn/blog/180616/hi9HEdI9HK.png?imageslim)

- `ps -e`:查看系统运行的进程

```
ps -e | grep ssh
```

![mark](http://myphoto.mtianyan.cn/blog/180616/728Ie3hg74.png?imageslim)

>查看包含ssh的进程

### 实践编程，用简单的C语言代码，编写一个实用的C语言小程序

avg.c :

```c
#include <stdio.h>

int main()
{
    int s,n;
    scanf("%d,%d",&s,&n);
    float v = s/n;
    printf("v =%f\n",v);
    return 0;
}
```

编译命令:
```
cc avg.c -o avg.out
```

input.c:

```c
#include <stdio.h>

int main()
{
    int flag =1;
    int i;
    int s = 0;
    int count=0;
    while(flag){
	scanf("%d",&i);
	if(0==i) break; #等于零跳出
	count++;
	s+=i;
    }
    printf("%d,%d\n",s,count);
    return 0;
}
```

```
cc input.c -o input.out
```

![mark](http://myphoto.mtianyan.cn/blog/180616/AgF7LfCjFe.png?imageslim)

注意上面的代码中应该将s初始化为0.否则会产生问题。

使用时：

```
./input.out | ./avg.out
```
实现将input的数据之间求平均值。
