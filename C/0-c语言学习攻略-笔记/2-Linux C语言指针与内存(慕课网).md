## Linux C语言指针与内存

前面我们对于:

- c语言的基本用法
- makeFile文件的使用
- main函数的详解
- 标准输入输出流以及错误流管道

### 工具与原理

![mark](http://myphoto.mtianyan.cn/blog/180617/DcFLi53kee.png?imageslim)

>指针与内存都是c语言中的要点与难点

- 指针
- 数组
- 字符串
- 堆内存与栈内存的差异
- gdb内存调试工具

![mark](http://myphoto.mtianyan.cn/blog/180617/8bb0gG673h.png?imageslim)

gdb是linux中的调试工具，可以让我们直接查看内存中的数据。

我们可以看到cpu到底做了什么事，而内存中又发生了什么变化

### C语言中指针的基本用法(初识指针)

main0.c：

```c
#include <stdio.h>

void change(int a, int b)
{
    int tmp =a;
    a=b;
    b=tmp;
}

int main()
{
    int a=5;
    int b=3;
    change(a,b);
    printf("num a =%d\n num b =%d\n",a,b);
    return 0;
}
```

上述代码无法实现a,b数值的交换。

![mark](http://myphoto.mtianyan.cn/blog/180617/AGbAhCFH4E.png?imageslim)

改为指针类型实现代码如下：

main1.c:

```c
#include <stdio.h>
void change(int *a, int *b)
{
    int tmp =*a;
    *a=*b;
    *b=tmp;
}

int main()
{
    int a=5;
    int b=3;
    change(&a,&b);
    printf("num a =%d\nnum b =%d\n",a,b);
    return 0;
}

```

为原来的变量值加上`*`, change函数改为传入`&a &b`
3和5可以成功的交换。

![mark](http://myphoto.mtianyan.cn/blog/180617/B8Cc44aG39.png?imageslim)

`int* a` 与 `int *a`都是可以的，被称为指针。`&` 取地址符。

我们要引入工具来分析

- 需要将**实参的地址**传到子函数才能改变实参! 如`change(&a,&b)`

C语言中**int未初始化时，初值为随机**

int变量未初始化的默认初值，和变量的类型有关

- 局部变量，在未初始化情况下，初值为随机值。C规范对该初值并没有做规定，具体实现由编译器决定。如VC/VS等编译器，会将初始值值为0xCCCCCCCC,而GCC等编译器则是不可预知的随机值。
- 静态局部变量，即带static修饰的局部变量。全局变量和静态全局变量，即定义在函数外，不属于任何一个函数的变量。这几种默认初值为0.

### gdb工具的使用

>通过gdb工具分析原理，分析结果

安装gdb工具：

```
sudo apt install gdb
gdb -v
```

gdb可以单步调试，打断点，查看内存中变量。但是即使生成了可调试版本，还是需要源代码`.c`的

- `gcc -g main0.c -o main0_debug.out`生成可调试版本。
- `gdb ./main0_debug.out`

- `l` 全称`list`：查看源代码
- `回车`：继续执行上条指令(此时的上条指令为`l`)
- `break 行数`：设置断点
- `start` ：单步调试
- `p a` 全称`print`：查看a在内存中的情况
- `n`：执行到下一条语句

![mark](http://myphoto.mtianyan.cn/blog/180617/mkEH90hGaF.png?imageslim)

>`$1` `$2` 只表明是第几个变量。正在显示的这行是待执行。

我们想看change函数里面是啥？而不是直接执行完函数。

- `s`：进入函数内部

![mark](http://myphoto.mtianyan.cn/blog/180617/FJeieEj68d.png?imageslim)

>可以看到只是把数字传进去了。

![mark](http://myphoto.mtianyan.cn/blog/180617/ICCL72ieBl.png?imageslim)

- `bt`：查看函数堆栈(可以看到main函数和change函数)
- `f 1`：切换到1号函数(栈顶的是我们当前所在函数)
- `q`：退出调试

形参与实参，函数默认传入变量其实只是将数值传入，而函数内部的局部变量不会改变全局中的数值。change中的形参a,b只是个代号而已。

### 使用gdb调试带指针的版本

![mark](http://myphoto.mtianyan.cn/blog/180617/D4diDf7Flg.png?imageslim)

>此时传递的是地址。正好相差四个字节。

下节课会介绍计算机内存的分配，什么是堆内存，什么是栈内存，内存地址，指针变量的实质是什么东西。

- `p *a` 

>`int *a`时, `p a`打印出的是a的内存地址, `p *a`打印的是这个地址里对应的值.
`P &a`显示a的内存地址空间

![mark](http://myphoto.mtianyan.cn/blog/180617/1176eAGG3D.png?imageslim)

### 

- `P &functionname`: p + &函数名, 显示函数程序在代码段的内存地址

```c
*a    取a这个地址的内容
&a    取a这个变量的地址
```

因为不知道一个指针指向的数据有多大, 所以需要在声明一个指针变量的时候需要明确的类型。

不能交换数值的解析：只是传值，只是change的局部变量，是实参的备份。

可以交换数值的解析加：变量加个指针，change传入取地址符，实现交换功能。

### 计算机中数据表示方法：

计算机内存中最小的单位叫做字节(Byte)

![mark](http://myphoto.mtianyan.cn/blog/180619/B61bB86Fha.png?imageslim)

>一个字节是八个二进制位

为什么是二进制呢？

>因为我们的计算机是电子计算机，电流只有两个状态: 高电位(亮) 低电位(不亮)

![mark](http://myphoto.mtianyan.cn/blog/180619/Bgl441AE5h.png?imageslim)

人类习惯于十进制数字，可以将二进制与十进制进行转换。(十个手指头)

>十进制满十进一，二进制满二进一

二进制写起来太长了，为了方便我们显示。

**0x表示十六进制**(满16进1 ABCDEF)

1个16进制的数字，就可以表示**4位二进制数字**

- 计算用二进制
- 显示用十进制
- 编程用16进制

### 内存管理

- 内存是什么？

>计算机系统中内存是由操作系统来统一管理的，一个字节有八个bit，也就是八个二进制位。

![mark](http://myphoto.mtianyan.cn/blog/180619/alj3hAeGmK.png?imageslim)

>不管插几个内存条，都会把内存看成一个整体来计算内存大小。可是内存也不是你想插多少就插多少的。

![mark](http://myphoto.mtianyan.cn/blog/180619/Fe33AEGFaI.png?imageslim)

>32位的操作系统最大只能使用4G的内存

- 那么问题来了，为什么32位操作系统只能使用4G内存呢？

因为32位的硬件平台上，cpu的地址总线是32位，也就是操作系统的寻址空间是32位。

>32位指的是:  给内存编号只能编到32个二进制位(这个编号就类似于我们街道的门牌号码)

比如一个小区只有八栋楼，那么这个编号就不能超过8.

cpu的地址总线有多少根，那么编号也就只能有多少个组合。

因为地址总线可以存在多种状态。

![mark](http://myphoto.mtianyan.cn/blog/180619/jcfhj6AC3I.png?imageslim)

32根地址总线就有2的32次方个状态

其中的一个编号就可以代表一个(内存的最小存储单位)字节。

>所以一共可以存储2的32次方个字节。

- 那么问题来了2的32次方个字节等于多少呢？

![mark](http://myphoto.mtianyan.cn/blog/180619/550Cm3eFEg.png?imageslim)

![mark](http://myphoto.mtianyan.cn/blog/180619/ecDCjDb72g.png?imageslim)

1024个字节等于1KB 1024个KB等于1MB，1024个MB等于1GB

内存分配:

1byte = 8bit(1字节 = 8进制位)

4G内存远远不够用。(64位操作系统出现)

![mark](http://myphoto.mtianyan.cn/blog/180619/0eKI3ihGC1.png?imageslim)

GB T PB EB

![mark](http://myphoto.mtianyan.cn/blog/180619/b7AcH90k41.png?imageslim)

操作系统会对所有内存进行编号。每个号码表示一个唯一的字节存放地址，一个字节可以存放8个二进制位的数据。

所以64位操作系统内存地址编号

![mark](http://myphoto.mtianyan.cn/blog/180619/842285Gmm0.png?imageslim)

![mark](http://myphoto.mtianyan.cn/blog/180619/eJHmffh4ih.png?imageslim)

>一共64个零到64个一

![mark](http://myphoto.mtianyan.cn/blog/180619/ckGDLEG4be.png?imageslim)

左侧便是我们的计算机中内存的编号示意图，从16位的0到16位的16个f。右侧则是我们每个编号对应的内存，每个字节(byte)可以保存8个bit(状态位)

这些内存全都要交给操作系统来管理。因为我们的一个计算机中可能同时要运行多个程序。
多个程序由不同的人或团队来开发，如果要由程序员来进行内存直接的管理是不太合理的。

多个程序对同一个内存地址来进行操作的话，到底分给哪个程序呢？这会引起冲突。

>内存的占用不确定，	不需要程序员来自己管理内存

![mark](http://myphoto.mtianyan.cn/blog/180619/3ekj37cAJJ.png?imageslim)

![mark](http://myphoto.mtianyan.cn/blog/180619/4Dm1Hkh5Kh.png?imageslim)

![mark](http://myphoto.mtianyan.cn/blog/180619/je6CiBCb6H.png?imageslim)

>应用程序是由操作系统来调用的

`main()`函数就是所有函数的入口,操作系统知道入口后就能执行代码了,程序就可以被调用了。

![mark](http://myphoto.mtianyan.cn/blog/180619/l9HKfBlBed.png?imageslim)

>操作系统： 除了能给内存做编号以外，还可以给内存做一定的规划

比如在64位操作系统中: 程序员可以使用的内存只要有前面的48位就可以了。

也就是0X7fffffffffffffff(0x7fffffffffff = 01111111111111111111111111111111111111111111111)以下的。

而以上的内存空间是给操作系统内核使用的。

- 用户内存和操作系统内存隔离开的好处:

>操作系统的内存不会被大量占用，避免机器卡住，卡死，死机等状态。

>可通过操作系统把应用程序关闭，使得操作系统更安全。 

![mark](http://myphoto.mtianyan.cn/blog/180619/23DJc63LKg.png?imageslim)

作为用户程序的内存空间又可以进行分段，从高到低又划分为：、

- 系统内核(乱入，属用户程序内存之外)
- 栈（暂时存储首先执行的程序状态）
- 自由可分配内存（可动态分配内存）
- 堆
- 数据段（声明一些全局变量或者声明一些常量）
- 代码段（程序源代码编译后存放在此）

我们写的c语言代码，编写的函数在编译后存到磁盘，运行程序时，就把源代码编译后的二进制数据加载到内存中。将源代码编译之后的二进制就会被存放在**代码段**。

声明的全局变量或常量放置在数据段。

![mark](http://myphoto.mtianyan.cn/blog/180619/4B7Lgk5F1C.png?imageslim)

>数据段的内存地址编号通常会大于代码段。

![mark](http://myphoto.mtianyan.cn/blog/180619/1f4IJ89IbB.png?imageslim)

高位内存空间分配给操作系统内核使用，低位内存空间分配给用户程序使用。

每次调用新的函数，就将新的函数压入栈区,正在调用的函数将位于栈顶。

64位系统中 只有前48位是给程序员使用的。 0x7fffffffffffffff ~ 0x0

剧透: 下一节中看在应用程序中栈，堆，数据段，代码段的作用。

### 变量与指针的本质

简单的例子:

```c
#include <stdio.h>

int global = 0;

int rect(int a,int b)
{
    static int count=0;
    count++;
    global++;
    int s=a*b;
    return s;
}

int quadrate(int a)
{
    static int count=0;
    count++;
    global++;
    int s = rect(a,a);
    return s;
}

int main()
{
    int a=3;
    int b=4;
    int *pa =&a;
    int *pb =&b;
    int *pglobal =&global;
    int (*pquadrate)(int a)= &quadrate;
    int s = quadrate(a);
    printf("%d\n",s);  
}
```

rect求长方形面积，quadrate求正方形面积(内部实际调用了求长方形面积)。
为了方面我们查看内存的情况，添加了个业务逻辑无关的一些变量。

```c
int global = 0;
```
>全局变量global

```c
static int count=0;
count++;
global++;
```

>函数内的静态变量: count，每个函数调用内部都让count和global加加。

main函数中声明了一系列的指针。
```c
int *pa =&a;
int *pb =&b;
int *pglobal =&global;
int (*pquadrate)(int a)= &quadrate;
```

```
gcc -g main.c -o main.out  //加-g生成的main.out才可以用gdb进行调试
gdb ./main.out   //调试
```

gdb调试命令:

- `l`(list)     列出代码
- `start`       开始调试
- `n`           单步调试
- `s`           进入函数内部
- `p 变量名`     输出变量的值
- `bt`          查看栈标号
- `f 栈标号`     切换栈
- `q`           退出gdb
- `回车`         重复执行上一次的命令

之所以可以调试代码？是机器码被加载进了我们的内存(代码段，它位于整个内存空间的最低位)

![mark](http://myphoto.mtianyan.cn/blog/180619/87Kjadi8EC.png?imageslim)

每一行都是我们的一条指令，被存放在代码段。但是c语言的语法是不允许我们直接操作代码段的。

>除了代码编译后会存在代码段以外，还有一个地方保存我们当前程序运行的状态，比如当前在调用哪个函数，当前调用的函数运行到多少行？并且这个函数中有哪些变量，这些变量的值是什么

就像是一张照相机拍摄的快照，记录当前的状态信息。这些信息会被记录到栈内存中。

![mark](http://myphoto.mtianyan.cn/blog/180619/2f3FL1G5lE.png?imageslim)

可以打印出当前的变量值，因为这个信息被记录在了栈内存当中。

![mark](http://myphoto.mtianyan.cn/blog/180619/cDEhEB3feG.png?imageslim)

因为还没有运行`int *pa = &a;` 内存中的pa值为空。

![mark](http://myphoto.mtianyan.cn/blog/180619/7b9b0AKccb.png?imageslim)

a里面是3，b里面是4，都被栈内存记录下来了。

![mark](http://myphoto.mtianyan.cn/blog/180619/Klkjm26d5k.png?imageslim)

**变量的本质是什么？**

- 变量名只是一个代号(一个标识符)
- 变量的本质就是内存

**指针的本质？**

![mark](http://myphoto.mtianyan.cn/blog/180619/B7a3BJCA7f.png?imageslim)

![mark](http://myphoto.mtianyan.cn/blog/180619/d5AC5301B4.png?imageslim)

指针pa也是一个变量，它也有自己的内存地址(0x7fffffffdcc8)。而这个内存地址中保存的数据是内存地址(0x7fffffffdcc0)。

C语言中所有的变量都有类型。

![mark](http://myphoto.mtianyan.cn/blog/180619/jd9galaKmd.png?imageslim)

- 指针保存的就是内存的地址。
- 变量: a = 第五个柜子第二个抽屉。

![mark](http://myphoto.mtianyan.cn/blog/180619/0FAB98fbcA.png?imageslim)

### 操作系统对于内存的管理

我们可以看到操作系统是如何管理内存的，以及gcc这类编译器对于我们源代码所做的优化。

代码段在整个内存地址中编号最小。

![mark](http://myphoto.mtianyan.cn/blog/180619/e9Hi2K59bk.png?imageslim)

>可以看出rect的编号小于quadrate的。代码段中保存我们编译之后的机器码。计算机在执行的时候rect函数先被加载进去。quadrate函数后被加载进去。先加载进去的内存地址就更小一些。

因为这两个函数是顺序执行的，多以使用大的减小的就是rect在内存中占用的大小。

![mark](http://myphoto.mtianyan.cn/blog/180619/ADc75HEaK3.png?imageslim)

**数据段: 全局变量 & 常量都在我们的数据段当中。**

![mark](http://myphoto.mtianyan.cn/blog/180619/7AB4c6BLB2.png?imageslim)

>可以看到数据段的地址是要比代码段大的。

一个函数可以被多次调用，main函数可以被操作系统多次调用。

![mark](http://myphoto.mtianyan.cn/blog/180619/a7i1H1GGff.png?imageslim)

>如我们多开qq

![mark](http://myphoto.mtianyan.cn/blog/180619/lHC9e42bAK.png?imageslim)

我们连续声明了两个变量，为何两个变量ab的地址不连续呢？ 

>因为这里的地址指的是内存的首地址，如int占四个字节。那么dcbc dcbd dcde dcbf都是属于变量a的内存空间。那么下一个内存地址的首地址就是dcc0了。

我们的b的首地址是dcc0，它也是int类型四个字节，为啥下一个变量pa的地址不是dcc4而是dcc8呢？

>这里就涉及到我们编译器的优化了，它为了让cpu操作指令更快，提升程序的执行效率会对我们的源代码做一定的优化。编译之后的指令存储有可能和我们编写代码的顺序不一样。

在代码中我们还声明了另一个整数类型变量s

```c
int s = quadrate(a);
```

![mark](http://myphoto.mtianyan.cn/blog/180619/k1jKCm3d1A.png?imageslim)

可以看到同样为整数类型的变量s的地址与前两个a，b是连续的。

>**gcc编译器的优化**，如果我们的函数中声明了若干个整型变量，若干个指针类型变量，若干个浮点型变量，它会把我们的同一类型的变量声明放到一起。接下来才声明指针变量。

这样的好处: 讲到数组，指针计算的时候，解释它的好处。

32位系统指针占用4个字节, 也就是32个bit, 64位系统占用64个bit, 也就是8字节。

![mark](http://myphoto.mtianyan.cn/blog/180619/5iClkC3Ich.png?imageslim)

可以看到指针pa的内存占用从dcc8 到 dcd0(共8个字节)pb从dcd0到dcd8，(共八个字节)，不管指针指向什么，它本身内存中存放的都是内存地址，占八个字节。

```c
int (*pquadrate)(int a)= &quadrate;
```

![mark](http://myphoto.mtianyan.cn/blog/180620/FaFiGCIidH.png?imageslim)

由dcd8 加上8个字节。来到了dce0

代码段中内存地址越来越大，先声明的函数地址小，后声明的函数地址大。
栈先声明的地址大，后声明的地址小，与代码段数据段相反。

下一节中: main函数调用正方形，正方形调用长方形。搞清栈内存如何分配的，再搞清静态变量，局部变量都是怎么存放的，理解函数的返回值return。

### 函数栈以及数据段内存

进行再一次的调试。

![mark](http://myphoto.mtianyan.cn/blog/180620/dcHLgK3eLI.png?imageslim)

运行到函数quadrate时，将a=3传入。

![mark](http://myphoto.mtianyan.cn/blog/180620/7JaIbBakH8.png?imageslim)

>可以看到栈中最下面的内存地址是最先分配的，如果从内存地址的大小来体现的话，main函数的内存地址大小第比较大的。

![mark](http://myphoto.mtianyan.cn/blog/180620/Chcm92dAlj.png?imageslim)

可以看到最先调用的main函数在最下面，然后是第二个调用的quadrate函数，最上面永远是当前执行的函数。

**栈的特点: 先进后出。** 最后进的是rect函数，最先出去的也应该是rect函数。

![mark](http://myphoto.mtianyan.cn/blog/180620/i68eldBgbJ.png?imageslim)

可以看到越到栈顶的函数，两个s(第一个s是存放栈顶的rect函数返回值的，第二个s是存放quadrate函数返回值的)

> 0x7fffffffdc74  0x7fffffffdc9c 栈顶的更小一点，也可以体现出越晚进来的，地址越小。

![mark](http://myphoto.mtianyan.cn/blog/180620/69KhmCjkKj.png?imageslim)

可以看到更早进来的main函数中s地址更大。**因此栈中是越早进来越在栈底，地址越大。**

![mark](http://myphoto.mtianyan.cn/blog/180620/F0be0J0CJA.png?imageslim)

可以看出我们在rect中的静态变量count，和我们在quadrate中的静态变量count是连续存储的。

```c
static int count=0;
```

![mark](http://myphoto.mtianyan.cn/blog/180620/e5b0cGJkeE.png?imageslim)

>可以看出函数内的两个静态局部变量count是独立的，连续存储的。而两个函数中的global变量都是指向同一个地址的。

观察大小，我们局部静态变量count的地址值和去全局变量的地址值都很小。因此说明他们并不存放在栈中。(栈的地址很大)

我们的静态变量，常量，包括全局变量，默认都存储在数据段中。由于静态变量时属于某个函数特有的，所以静态变量也是属于某个函数特定的，是独立的。全局变量是所有函数公用的，但是由于他们都在数据段中，即使一个函数被多次调用，静态变量指向的还是数据段中的一个固定地址。不同函数里的count是不同的count，但是同一个函数不管调用多少次，这个count都指向同一块内存。

数据段（data segment）通常是指用来存放程序中已初始化的全局变量的一块内存区域。数据段属于静态内存分配。 

编译器优化代码,把声明时不在一起的同一类型变量,放到一起(某种程度上修改了源码)

>如声明

```c
int a; float b; int c;
```

编译后变量a的地址和c的地址是连在一起的.CPU在编译的时候对栈内变量的存储地址进行优化，他会将类型相同的变量在连续地址中储存。

地址分配: 代码段,数据段是从下往上分配(先低地址,后高地址)。栈是从上往下分配(先高地址,后低地址)

**函数中静态变量,局部变量区别:**

**局部变量**在**栈**(相对数据段而言的高地址)中,而**静态变量**在**数据段**(低地址)中.
所以在多次调用函数时,**静态变量不会被重新初始化**.或者这么说,静态变量的生存周期和数据段相同,局部变量生存时间受调用函数时,**所属函数进栈出栈的影响而会重新初始化**.

全局变量和静态变量都在数据段中,但静态变量是某个函数特有的.

下面来探究函数指针是怎么一回事?

指针可以指向一个变量，吧变量的值取出来。函数指针？

### (函数指针与指针指向的数据访问)

修改我们的源代码(上面我用的是修改过的，但是不影响上面概念的理解)

```c
int s = quadrate(a);
```
修改为:

```c
// int s = quadrate(a);
int s = (*pquadrate)(a);
```

函数指针在调用的时候传入a的值进来。

```
gcc -g main.c -o main.out  //加-g生成的main.out才可以用gdb进行调试
gdb ./main.out   //调试
```

```c
int (*pquadrate)(int a)= &quadrate;
```

>这一行是一个函数指针

![mark](http://myphoto.mtianyan.cn/blog/180620/b6J1gfd91l.png?imageslim)

这里依然可以进入函数内部，运行代码时函数指针也可以调用函数内容。这种做法经常用于写程序时做回调函数使用。

- `p &a` 是将变量a的内存地址找出来。`&`符号时取地址符

![mark](http://myphoto.mtianyan.cn/blog/180620/I7E2bI1IDe.png?imageslim)

- 如果已经知道一个地址如何取里面的数据？

![mark](http://myphoto.mtianyan.cn/blog/180620/f449FhdECg.png?imageslim)

- `p *&a`: 取变量a所在地址的值 (先进行`&`运算,`&a`相当于取变量a的地址,在执行`*`运算，`*&p`相当于取变量a所在地址的值）

- `p &*a`：取变量a的地址 (先进行`*`运算,`*a`相当于变量a的值，再进行`&`运算，`&*p`就相当于取变量a的地址）

`quadrate` 本身是一个函数指针，`*quadrate`取出了指向的函数内容(一组指令构成)，
`(*quadrate)(3)`就表示调用函数，并传入参数3

![mark](http://myphoto.mtianyan.cn/blog/180620/4k5aA5D0fC.png?imageslim)

- `p pa`  pa是指向pa的地址。
- `p *pa` 代表取出0x7fffffffdcbc这个地址存放的值，pa指向的是一个栈的地址，如果是栈内存地址肯定是要访问数据，栈，堆，数据段内存都认为是取数据。代码段是找到一个代码块。

![mark](http://myphoto.mtianyan.cn/blog/180620/Glg1Kj6KfJ.png?imageslim)

- `p &pa` 指找到pa变量本身的地址。

下面: 数组，动态堆内存创建，指针运算。

### 数组申明的内存排列

示例代码:

```c
#include <stdio.h>
int main()
{
	int a =3;
	int b =2;
	int array[3];
	array[0] =1;
	array[1] =10;
	array[2] =100;
	int *p=&a;
	int i;
	for (i = 0; i < 6; i++)
	{
		printf("*p=%d\n",*p);
		p++;
	}
	printf("-------------------------------------\n");
	p =&a;
	for (i = 0; i < 6; i++)	
	{
		printf("p[%d]=%d\n",i,p[i] );
	}
	return 0;
}
```

为了说明问题，所有的数据类型统统是整型，除了指针p以外。c语言的数组类型是比较原始的，在函数内声明，因此也在栈内存当中。指针p指向a的地址。

p是一个指针，指针的加加操作。我们类比一下，整数类型的加加，3++，下次打印就会变成4。

p[i] 指针的括号取值，与数组取值有些类似。

```
gcc -g main.c -o main.out  //加-g生成的main.out才可以用gdb进行调试
./main.out        //观察结果
gdb ./main.out   //调试
```

![mark](http://myphoto.mtianyan.cn/blog/180620/ca9c14lKK9.png?imageslim)

**for循环括号里加不加int，内存中还有区别的。**

![mark](http://myphoto.mtianyan.cn/blog/180620/Ah86J4cjKD.png?imageslim)

指针p指向的值等于3,1,2

int类型的内存地址和数组内存地址不连续,而是差了16位。

```c
for (i = 0; i < 6; i++)
        {
                printf("*p=%d\n",*p );
                if(i == 2){
                   p=p+4;
                }
                else{
                   p++;
                }
        }
```
将第一个for循环中的代码改为如上面所示。

![mark](http://myphoto.mtianyan.cn/blog/180620/0LiKc8jmDe.png?imageslim)

```c
for(i = 0; i < 6; i++)
        {
                if(i > 2){
                printf("p[%d]=%d\n",i+3,p[i+3] );
                }else{
                printf("p[%d]=%d\n",i,p[i] );
                }
        }
```

![mark](http://myphoto.mtianyan.cn/blog/180621/6Bik0KGmbm.png?imageslim)

![mark](http://myphoto.mtianyan.cn/blog/180621/i134296B6i.png?imageslim)

此时我们打印a的地址，打印p的地址是一样的。因为我们把a的地址赋值给了p

每个整型数字占四个字节。

```c
(gdb) p *p
$3 = 3
(gdb) p *&a
$4 = 3
(gdb) p *0x7fffffffdcc4
$5 = 3
(gdb) p * 0x7fffffffdcc4
$6 = 3
```

>可以看到四种等价的操作。都是`*`加上地址，可以直接打印出内存中的数据值。

![mark](http://myphoto.mtianyan.cn/blog/180621/ah902ACdaC.png?imageslim)

先声明了a，再声明了b。但是我们a的下一个内存地址中存放的却不是b。c8地址中存放的是0

**gcc编译器有自动优化功能**会把所有的同一类型的变量放到一起来声明。因为我们还声明过一个i变量，i也是整型的。
会把i也和a，b放在一起，具体哪个变量在前，哪个变量在后。

>通常情况先写的会在前面，这里因为我们i在很下面声明的，中间又隔了一个指针p

![mark](http://myphoto.mtianyan.cn/blog/180621/EkaccB6kLg.png?imageslim)

0的值就等于i的值，两个指向同一个地址。

main函数执行的栈中，最低的地址放的a的值，接下来是i的值，i的值之后应该推测是b的值。

```
0x7fffffffdcc8 + 4
0x7fffffffdccc
```

![mark](http://myphoto.mtianyan.cn/blog/180621/K229DIFm2I.png?imageslim)

>可以看出地址顺序依次增大: a i b

一直p p p的输出很麻烦，如何方便的输出？

```c
x/3d 0x7fffffffdcc4
```

x表示要输出内存中的值，/表示要输出几个值，输出3个值。按照什么类型来输出。`d`按照十进制进行输出。从哪个地址开始显示呢？

![mark](http://myphoto.mtianyan.cn/blog/180621/ej2Bdhm04g.png?imageslim)

我们还可以指定显示变量要有多大长度，默认是4个字节。 

![mark](http://myphoto.mtianyan.cn/blog/180621/gga6ikAJbh.png?imageslim)

取九块内存地址的内容，可以看到整数类型的数字和数组的存储中间相差三个内存空间(地址上从头到头，相差16个字节)

那些随机值是不可控的，程序中使用到未初始化的值，会对软件造成异常。

因为c语言不做指针的安全检查，它会操作这个地址的值等，未初始化，有可能是其他程序使用过的值。

栈内存中, 连续的地址空间来存放整型变量和我们的数组元素。

可以看出数组是按顺序放置元素的。

### 指针运算。

![mark](http://myphoto.mtianyan.cn/blog/180621/K8k2E9Hmf5.png?imageslim)

可以看到指针往下移动了4格，可是指针怎么知道要加四格呢？

>因为程序员在声明指针类型的时候是整型，int占四个字节。所以p++的时候会一次移动4个。

这是指针的偏移运算。指针的偏移运行效率高，性能好。

```c
p +=3;
```

>把指针往下移三格(整数类型指针)移动12个字节

```c
*p =101;
```

>将p指针所指向的值修改为101

```c
p =&a;
```

>让p再次指向a的地址,不影响我们下面的打印。

![mark](http://myphoto.mtianyan.cn/blog/180621/hIA0I90DG6.png?imageslim)

>可以看到原本p指向a，然后往下移动三格(忽略整型与数组中间三块内存，四个地址差)

第一次，从a移动到i；第二次，从i移动到b；第三次，从b移动到数组第一个元素。

```c
p[3] //等价于p +=3,也就是把p往下移动三格
```

```
*p = 101
//上面两行合二为一的想法是错的，因为只有下面这行才能起到理想目的。
p[3] = 101
```

```c
int *p=&a;
p[2];
*p = 66;
```

`P[4]`不是p往下面移动了4个位置，而是从p开始的地址往后移动4个位置取值，**p指向的地址还是不变的**这时候就不用跟采用`p++`时，再将指针归位了。

```c
int array[2];
int *pa =array;
pa[0]=1;
pa[1]=10;
pa[2]=100;
```

>如果说数组本身也是一种指针类型的话，里面就是地址。把地址赋给地址变量就不需要加取地址符了。


任何需要用数组操作的地方，都可以用指针来代替。因为我们的指针变量本质上是内存地址，数组也是地址。

反过来就不行了，指针能做的，数组不一定能做。

```c
int array[2];
array+=2;
```

>上面的代码就是错误的。

数组其实就是个**指针常量**，指针是**指针变量**，常量是不可更改的。array永远都指向的是同一个地址，当然地址里面的内容是可以改变的。


下节课: 一种特殊的数组，字符数组

### 字符数组和指针字符串

小示例代码:

```c
#include <stdio.h>

int main()
{
    char str[]="hello";
    char *str2="world";
    char str3[10];
    printf("input the value\n");
    scanf("%s",str3);
    printf("str is %s\n",str); 
    printf("str2 is %s\n",str2);
    printf("str3 is %s\n",str3);
}
```

声明了一个字符数组并赋值hello，又声明了一个字符指针，还声明了一个长度为10的字符数组，并未初始化。

通过scanf将输入的字符串写入str3中。

然后进行打印。

```
gcc -g main.c -o main.out
```

生成可调试代码。

![mark](http://myphoto.mtianyan.cn/blog/180621/02DDjgiLda.png?imageslim)

```
gdb main.out //开始调试
```

![mark](http://myphoto.mtianyan.cn/blog/180621/f7FHblfd48.png?imageslim)

>打印str和str2的时候，都可以打印出内存中的字符串来。

str直接打印出里面的值，因为str2指明的是指针类型，会等于一个地址`0x5555555548b4`。

地址是一个很小的地址(相对于0x7),是在代码段中的地址，是源代码编译就编译进去的。 而我们的str2只是指向这个地址而已。

![mark](http://myphoto.mtianyan.cn/blog/180621/Kdj8h4F7L3.png?imageslim)

可以看出str2这个指针对应的是整个数组的首地址而已。首地址对应的内存中存储着首字母w

119是w对应的ASCII码。第6个值，是因为上面o的那次,已经将指针后移了一位，++后移第二位。

![mark](http://myphoto.mtianyan.cn/blog/180621/9GCF6DlADi.png?imageslim)

指针忘记归位，导致str2只剩下三个字母。

字符类型的指针和字符数组也是可以混用的。

![mark](http://myphoto.mtianyan.cn/blog/180621/JgddE7BhKd.png?imageslim)

>一般的我们通过scanf输入，是要输入`&a`，也就是要加取地址符的。

声明str3的时候，它是一个字符数组，数组就是内存地址。**str3就可以直接传进去，不需要取地址符。**


```c
scanf("%s",str);
```

将输入存放至str中。

![mark](http://myphoto.mtianyan.cn/blog/180621/6im8lA8dkf.png?imageslim)

可以看到因为数组的本质是指针常量，str指向的地址，被mtianyan2str填充。而str3的指针还指向原来的位置，所以造成str3的内容为str的后半部分。

str在创建时有五个字母+一个null结束符，但是它的数组长度是6。

![mark](http://myphoto.mtianyan.cn/blog/180621/6B6jJh645B.png?imageslim)

所以计算str3时需要减去6个字母才可以得到。

```c
char str4[]={'h','e','l','l','o'};
int len = sizeof(str4) / sizeof(char);
```

而采用这种单字母初始化方法，数组长度与字符个数一致。

![mark](http://myphoto.mtianyan.cn/blog/180621/C0GGFdDAk6.png?imageslim)

我们尝试向str2中写入东西。

![mark](http://myphoto.mtianyan.cn/blog/180621/5i1cfBhm81.png?imageslim)

可以看到往str2写数据，会出现段错误(核心已转储的错误)

**c语言的字符串是一个字符数组，以/0结尾。有五个字符就有六个长度**

![mark](http://myphoto.mtianyan.cn/blog/180621/9e7DC15a4a.png?imageslim)

gdb的x命令，可以打印地址中的值
- `x/个数  地址`
- `x/6cb 地址`： 打印该地址后的6个字符,`c`：字符形式打印，`b`：打印的单位按byte

![mark](http://myphoto.mtianyan.cn/blog/180621/b4f8Jgad3J.png?imageslim)

scanf可以将输入存入str或str3，但是不能存入str2

堆和栈内存里才可以写入（预留空间才可写入)，而str2是编译之后，加载到内存的一个代码段变量，不允许写入。操作系统对内存做安全管理。

![mark](http://myphoto.mtianyan.cn/blog/180621/c031B6bj3g.png?imageslim)

>我们声明一个函数把一个函数定义好了，函数所在的栈的内存就分配好了。

而我们使用malloc函数，它会为我们分配堆内存。

### 字符数组的深入理解

示例代码2:

```c
#include <stdio.h>

int main()
{
    char str[]="hello";
    char *str2="world";
    char str3[10];
    printf("input the value\n");
    str[3]='\0';
    scanf("%s",str3);
    printf("str is %s\n",str); 
    printf("str2 is %s\n",str2);
    printf("str3 is %s\n",str3);
}
```

```c
gcc -g main2.c -o main2.out
```

![mark](http://myphoto.mtianyan.cn/blog/180621/FhH7e84DKL.png?imageslim)

只会打印出hel，因为prinf打印以`\0`为结束。

```c
char str1[] = "hello";
char str3[5];
```

可以认为str1的6个字节结束之后，就是str3指向的地址。

如果通过scanf输入到str1的值超过长度6，因为没有`\0`，还会继续往里写。都会写入str中。

- 当str1声明时,长度为五个字母加上`\0`为6,str3也是数组类型,与str1都在同一个内存空间中,并且在str1之后声明, 它们的地址应该是连续的。

- 当scanf输入到str1的值为 `HelloWorld`时,str1之前的大小装不下这么多字符,就会使用后面的内存地址,str3 本是空的并没有赋值,但是由于str1的内存溢出,装到了str3中,所以str3也是有值的.

**总之,数组内存溢出是件危险的事**

**string类型输出遇到`\0`结束**
**char类型输出遇到`\0`继续输出**

```c
#include <stdio.h>

int main()
{
    char str[]="hello";
    char *str2="world";
    char str3[10];
    printf("input the value\n");
    str[3] = '\0';
    scanf("%s",str3);
    int i=0;
    for(i=0;i<6;i++)
    {
      printf("%c\n",str[i]);
    }
    printf("str is %s\n",str); 
    printf("str2 is %s\n",str2);
    printf("str3 is %s\n",str3);
}
```

![mark](http://myphoto.mtianyan.cn/blog/180621/b72LG38EGF.png?imageslim)

