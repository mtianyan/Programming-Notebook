## Linux C语言结构体简介

前面学习了c语言的基本语法特性，本节进行更深入的学习。

- 预处理程序。 编译指令: 预处理, 宏定义，
- 建立自己的数据类型：结构体，联合体，动态数据结构
- c语言表达式工具 逻辑运算符： `&  |  ^  ~  <<  >>`
- 函数的递归调用方法

### 什么是预处理

```
vim helloworld.c
```

helloworld.c：

```c
#include <stdio.h>

int main()
{
    printf("hello,world!\n");
    return 0;
}
```
编译的目的:

>从c语言`.c`源文件变成可执行文件

```
gcc helloworld.c -o helloworld.out
./helloworld.out
```

编译的四个步骤:

>`.c`文件->`.i`文件->`.s`文件->`.o`文件->可执行文件(可运行)

- 1. 预处理
- 2. 编译     
- 3. 汇编      
- 4. 链接

记忆法: ISO三步走战略。

下面我们来查看预处理中要做的事情:

```
gcc -o helloworld.i helloworld.c -E
```

`-E`表示只让gcc执行预处理。

```c
// 查看helloworld.i文件
cat helloworld.i
```

vim跳到整个文档底部，命令: `:$`

![mark](http://myphoto.mtianyan.cn/blog/180622/khK8lm7Cc2.png?imageslim)

可以看到代码的底端是我们的main函数

对比一下`.i`文件和`.c`文件的区别

>首先:它们都是c的语法。其次.c文件main函数上面是`#include <stdio.h>`

而`.i` 文件中这行代码不见了，变成了上面这些东西。

**所以预处理所做的第一件事情就是展开头文件**

将`#include <stdio.h>`中`stdio.h`展开,将未注释的内容直接写入.i文件。

在预处理步骤中，除了展开头文件，还要进行宏替换。

### 宏是什么

c语言常量分为直接常量和符号常量:

```c
#define 标识符 常量值 (注意:没有分号)
```

helloMacro.c源代码：
```c
#include <stdio.h>
#define R 10

int main()
{
    int a =R;
    printf("a=%d\n");
    printf("hello,world!\n");
    return 0;
}
```

```
gcc -o helloMacro.i helloMacro.c -E
```

预处理过之后的代码

```c
# 4 "helloworld.c"
int main()
{
    int a =10;
    printf("a=%d\n");
    printf("hello,world!\n");
    return 0;
}
```

![mark](http://myphoto.mtianyan.cn/blog/180622/ImFI8hIama.png?imageslim)

>可以看到10是直接当做一个字符串来替换原本的宏定义R。

**宏的本质是发生在预处理阶段单纯的字符串替换(宏替换), 在预处理阶段,宏不考虑语法;**


示例代码2:
`vim helloMacro2.c`

```c
#include <stdio.h>
#define R 10
#define M int main(

M){
    printf("hello,world!\n");
    return 0;
}
```

```
gcc helloMacro2.c -o helloMacro2.out
./helloMacro2.out
```

预处理是没有问题的,可以成功的编译执行。**宏不考虑C语言的语法**。它很单纯，字符串替换。

![mark](http://myphoto.mtianyan.cn/blog/180622/dmckc6kEc0.png?imageslim)

- 宏用于大量反复使用的常量、数组buffer的大小，为了便于修改定义成宏。

通常定义数组我们这样写:

```c
int a[10];
int b[10];
```

定义两个相同大小的数组，这里我们就可以改为下面代码。

```c
#define R 10
int a[R];
int b[R];
```

>一次修改，可以修改两份。

宏也是可以传递参数的，可以做一些函数可以做的事情

### 宏函数

`vim helloMacroFunction.c`
源代码：
```c
#include <stdio.h>
#define R 10
#define M int main(
#define N(n) n*10



M){
    int a = R;
    int b = N(a);
    printf("b = %d\n",b);
    printf("a =%d\n",a);
    printf("hello,world!\n");
    return 0;
}
```

```
gcc helloMacroFunction.c -o helloMacroFunction.out
./helloMacroFunction.out
```

![mark](http://myphoto.mtianyan.cn/blog/180623/H8h6ka21D1.png?imageslim)

>这里的处理过程: 首先将参数a替换到上面的宏中，上面就变成了`N(a) a*10`,之后再用`a*10`替换下面的`N(a)`

```
int b = N(a); //变成了 int b =a*10;
```

```
gcc -o helloMacroFunction.i helloMacroFunction.c -E
```

预处理之后：

```c
# 8 "hello.c"
int main(){
    int a = 10;
    int b =a*10;
    printf("b = %d\n",b);
    printf("a =%d\n",a);
    printf("hello,world!\n");
    return 0;
}
```

![mark](http://myphoto.mtianyan.cn/blog/180623/1C6g1B2GLI.png?imageslim)

先不考虑宏实现，先来写一个正常的求和函数。

```
vim helloAdd.c
```

```c
#include <stdio.h>
#define R 20
#define M int main(
#define N(n) n*10

int add(int a,int b){
    return a+b;
}


M){
    int a = R;
    printf("a =%d\n",a);
    printf("hello,world!\n");

    int b =N(a);
    printf("b = %d\n",b);
    
    int c =add(a,b);
    printf("c =%d\n",c);

    return 0;
}
```

```
gcc helloAdd.c -o helloAdd.out
./helloAdd.out
```

![mark](http://myphoto.mtianyan.cn/blog/180623/1e0l32amb7.png?imageslim)

使用宏函数实现求和。

```
vim helloAddMacro.c
```

```c
#include <stdio.h>
#define R 20
#define M int main(
#define N(n) n*10
#define ADD(a,b) a+b
int add(int a,int b){
    return a+b;
}


M){
	int a = R;
    printf("a =%d\n",a);
    printf("hello,world!\n");

    int b =N(a);
    printf("b = %d\n",b);
    
    int c =add(a,b);
    printf("c =%d\n",c);

    int d =ADD(a,b);
    printf("d =%d\n",d);

    return 0;
}
```

```
gcc helloAddMacro.c -o helloAddMacro.out
./helloAddMacro.out
```

![mark](http://myphoto.mtianyan.cn/blog/180623/8AkCAcABGJ.png?imageslim)

>可以看到使用宏函数和普通函数的求和效果是一致的。结果与简单的字符串替换一致。

`ADD(a,b)` 被替换成 `a+b` 因此式子变成`int d = a+b;`

```
gcc -o helloAddMacro.i helloAddMacro.c -E
vim helloAddMacro.i
```

![mark](http://myphoto.mtianyan.cn/blog/180623/IEI4Kb22L7.png?imageslim)

版本3，宏定义中优先级问题。

```c
#include <stdio.h>
#define R 20
#define M int main(
#define N(n) n*10
#define ADD(a,b) a+b
int add(int a,int b){
    return a+b;
}


M){
	int a = R;
    printf("a =%d\n",a);
    printf("hello,world!\n");

    int b =N(a);
    printf("b = %d\n",b);
    
    int c =add(a,b);
    printf("c =%d\n",c);

    int d =ADD(a,b);
    printf("d =%d\n",d);

    int e =ADD(a,b) * ADD(a,b);
    printf("e =%d\n",e);

    return 0;
}
```

预测一下e的输出为: `a+b*a+b` ab先乘起来，a=20，b=200，ab=4000，然后加上a，b：得到结果(4220)

```
gcc helloAddMacroPrecedence.c -o helloAddMacroPrecedence.out
./helloAddMacroPrecedence.out
```

![mark](http://myphoto.mtianyan.cn/blog/180623/CbC6JmBkj2.png?imageslim)

>运算是等我们编译完了，执行的时候才会运行的。预处理阶段不会进行运算操作。

- **宏定义时由于本质是字符串的替换**

真正运算的时候，会按照运算符号的优先级来进行

解决方案:

```c
#define ADD(a,b) (a+b)
```

```
gcc helloAddMacroPrecedence.c -o helloAddMacroPrecedence2.out
./helloAddMacroPrecedence2.out
```

>加个括号，保证优先级更高一点。

![mark](http://myphoto.mtianyan.cn/blog/180624/B3jJC9bDAK.png?imageslim)


宏函数和正常函数的优势？

正常的add函数需要返回值类型，需要传递进来的参数有类型要求。

讲传入的a,b 类型进行改变，如变为两个浮点型数，程序就会**自动类型转换**。

但是**宏函数就没有这种要求**可以不用考虑输入值的类型，这与普通的函数定义不同。

```c
int c =add(10.5,20.4);
printf("c =%d\n",c);

float d =ADD(10.5,20.4);
printf("d =%f\n",d);
```

```
gcc helloAddMacroPrecedenceCompare.c -o helloAddMacroPrecedenceCompare.out
./helloAddMacroPrecedenceCompare.out
```

![mark](http://myphoto.mtianyan.cn/blog/180624/5ckDJ5j60a.png?imageslim)

>普通函数例如`int add(int a,int b)`除了在开头要声明值的类型，还要设置返回值，因此在定义过程与调用过程相对复杂。若能用宏定义实现的情况应优先考虑宏定义.

宏是不考虑数据类型，不考虑c语言的语法的。只是简单的字符串的处理。

预处理阶段，除了宏之外，还提供了一个叫做**mtianyan:条件编译**的功能。

>可以按照不同的条件，编译不同的程序部分，从而产生不同的目标代码文件。对于程序的移植和调试都是很有用的。

下集预告: 和宏比较相近的功能，`typedef`

### Linux C预处理之typedef

严格来讲，`typedef`和预处理是没多大关系的，放在这里是因为容易搞混淆。

- `typedef`作用是给一个变量类型起别名。

简记: 取别名; 但是**属于C语法**, 结束要加分号, 与`#define`不同, 它不需要加分号。

```c
typedef int tni;
```

将`int`用`tni`代替,在之后的`int`定义可直接写为:

```c
tni a;
```

我们之前定义指针的情况:

```c
int *p;
// 如果我们加上typedef
typedef int *p;
```

>`typedef int *p;` 是给`int *` 这个数据类型(还记得大明湖畔我们说过的，`typedef`作用是给一个变量类型起别名)起了别名`p`

```c
pq=null
// 根据上面的typedef等价于
int* q=null
```

将int类型换成tni:

```c
typedef int tni;

M){
    tni a = R;
```

```
gcc helloAddMacroPrecedenceCompareTypedef.c -o helloAddMacroPrecedenceCompareTypedef.out
./helloAddMacroPrecedenceCompareTypedef.out
```

![mark](http://myphoto.mtianyan.cn/blog/180624/LcfliHEjmk.png?imageslim)

>可以看到程序可以成功的运行，注意，**真名可以和别名共存**。

之前我们已经试验过了宏是会在预处理阶段被替换的,而tni不会在`.i`文件中被替换。

```c
gcc -o helloAddMacroPrecedenceCompareTypedef.i helloAddMacroPrecedenceCompareTypedef.c -E
vim helloAddMacroPrecedenceCompareTypedef.i
```

![mark](http://myphoto.mtianyan.cn/blog/180624/AGcghbBi6l.png?imageslim)

我们通常在使用`typedef`的时候,通常都是给自己自定义的数据类型起别名。

比如`size_t`就是系统给我们定义的一个类型的别名。

```c
typedef unsigned long size_t;

// 定义一个结构体
struct stu{
};

// 使用结构体的时候
struct stu xxx;

// 给结构体起别名
typedef struct stu{
} stu_t;
// 起了别名之后使用结构体
stu_t xxx;
```

区别2: 宏定义开头声明，全局任何作用域都可以直接使用。

>注意typedef如果写在方法体内,则只可作用于该作用域的花括号内。

下节课: 结构体

### 结构体的声明与定义

之前的学习中，使用的变量类型大多是一些比较简单的变量类型。

比如:

```c
int a = 0;
float b =0.0;
```

>这些变量之间没有什么联系,然而很多时候我们存储的数据比较复杂，不能通过简单的类型进行描述。

比如我们需要存储一个武器的信息:

![mark](http://myphoto.mtianyan.cn/blog/180624/hkc16GdI30.png?imageslim)

>它会包含武器的很多信息。之前的所有数据类型，都不足以描述一个武器的多种信息。

数组也不行，因为数组只能存放同类型的数据，武器的名字和价格类型不同。

**结构体是不同类型变量的集合** & **数组是相同类型变量的集合**

```
vim Cstructweapon.c
```

```c
#include <stdio.h>
struct weapon{
	// 武器名字
    char name[20];
    // 攻击力
    int atk;
    // 价格
    int price;
};

int main()
{
   int a =0;
   float b =0.0;

   struct weapon weapon_1;
   return 0;
}
```

>`struct 结构体类型名{}`，只是创建了一个结构体类型。

但是我们可以使用这一结构体类型`struct weapon`来声明变量

```c
struct weapon weapon_1;
```

>这种定义方法是声明和定义分离的形式。

第二种直接在声明时去定义。

```c
struct weapon{
	// 武器名字
    char name[20];
    // 攻击力
    int atk;
    // 价格
    int price;
}weapon_1;
```

>相当于定义了一个全局变量，变量名为weapon_1，类型是`struct weapon`。简单程序可以运用

第三种方法:

```c
struct{
	// 武器名字
    char name[20];
    // 攻击力
    int atk;
    // 价格
    int price;
}weapon_1;
```

>这种方法就不能用这个结构体类型去定义其他的变量。匿名结构体类型。

下节课预告: 如何进行结构体的初始化与引用

### 结构体的初始化与引用。

定义了结构体之后: 我们要知道如何初始化，以及如何访问结构体成员

在对结构体进行初始化的时候，可以等于一个初始化列表。通过一个花括号将常量括起来，
依次赋值给结构体成员。

```c
struct weapon weapon_1 = {"weapon_name",100,200};
// 访问结构体里的成员，使用点
printf("%s\n,%d\n",weapon_1.name,++weapon_1.price);
```

```c
#include <stdio.h>
struct weapon{
	// 武器名字
    char name[20];
    // 攻击力
    int atk;
    // 价格
    int price;
};

int main()
{
   int a =0;
   float b =0.0;

   struct weapon weapon_1 = {"weapon_name",100,200};
   // 访问结构体里的成员，使用点
   printf("%s\n%d\n",weapon_1.name,++weapon_1.price);
}
```

```
gcc Cstructweapon.c -o Cstructweapon.out
./Cstructweapon.out
```

![mark](http://myphoto.mtianyan.cn/blog/180625/EL995HgbbB.png?imageslim)

结构体成员变量可以和普通变量一样进行操作。`weapon_1.name`应该被我们视为一个整体

```c
a++;
++weapon_1.price //可以看出它可以像普通变量一样操作
```

### 结构体数组

如果我们需要十个武器的数据，我们需要使用数组，结构体数组。

- `.`(点)运算符是一个成员运算符，**在所有运算符中运算级最高**，可用`.`运算符访问结构体内部成员. 

>结构体数组和普通数组，差别不大。

```c
int a[2]; // 包含两个int类型的元素

//结构体数组里包含两个结构体类型的元素，每个元素有结构体里的三个成员
struct weapon weapon_2[2]; // 每个元素都是一个结构体类型的数据
```

vim CstructweaponArray.c(在原基础上添加代码)

```c
struct weapon weapon_2[2]={{"weapon_name1",50,100},{"weapon_name2",99,200}};
printf("%s\n%d\n",weapon_2[0].name,weapon_2[1].atk);
```

```
gcc CstructweaponArray.c -o CstructweaponArray.out
./CstructweaponArray.out
```

![mark](http://myphoto.mtianyan.cn/blog/180625/ejb6m242EF.png?imageslim)

两种结构体数组的初始化方式:

```c
// 直观式
struct weapon weapon_2[2]={{"weapon_name1",50,100},{"weapon_name2",99,200}};
// 一般式
struct weapon weapon_2[2]={"weapon_name1",50,100,"weapon_name2",99,200};
```

两种方式都可以成功的初始化。

### 结构体指针

了解: 什么是指向结构体变量的指针变量，以及如何去使用这个变量。

```c
struct weapon *w ;  //定义一个指向weapon的w结构体指针
w=&weapon_1;       //具体指向weapon_1的内存地址

(*w).name 		    //左右两侧的括号不可省略，因为.运算符优先级高于星
w->name          // 箭头叫做指向运算符
weapon_1.name   //这3种访问类型都是一样效果
```

```
vim CstructweaponArrayPointer.c
```

```c
struct weapon * w;
w = &weapon_1;
printf("---------------------------------\n");
printf("name=%s\nname=%s\nname=%s\n",(*w).name,w->name,weapon_1.name);
```

```
gcc CstructweaponArrayPointer.c -o CstructweaponArrayPointer.out
./CstructweaponArrayPointer.out
```

![mark](http://myphoto.mtianyan.cn/blog/180625/Khfb3aaAcE.png?imageslim)


### 结构体数组指针

```
cp CstructweaponArrayPointer.c CstructweaponArrayPointer2.c
vim CstructweaponArrayPointer2.c
```

**结构体数组指针,不用取地址符`&`**

数组的名字代表了这个数组的内存首地址, 数组括号内的长度代表了数组的单元数,数据类型是int的话就按照int类型(32位系统上是4个字节)乘以单元数的长度，如果数据类型是结构体的话就按照结构体的长度乘以单元的长度。

p++，不是内存位置右移了一个字节，而是右移了一个单位长度的结构体weapon的内存长度。所以就不难理解为什么右移到了第二个结构体实例的首地址上了。

```c
struct weapon weapon_2[2]={{"weapon_name1",50,100},{"weapon_name2",99,200}};
struct weapon *p;
p = weapon_2; //数组的名字对应着数组第一个元素的起始地址

// 取成员值: p->name 相当于 weapon_2[0].name
printf("%s\n",p->name);
printf("---------------------------------\n");
p++; // 等价于 weapon_2+1 让其指向weapon_2[1]
printf("%s\n",p->name);
```

```
gcc CstructweaponArrayPointer2.c -o CstructweaponArrayPointer2.out
./CstructweaponArrayPointer2.out
```
![mark](http://myphoto.mtianyan.cn/blog/180625/G5akIe8cA4.png?imageslim)

### Linux C 公用体

公用体类型也被称之为联合体，创建公用体类型可以使用关键字`union`

>理解起来很简单，让几个不同类型的变量共享同一块内存地址

```
vim union.c
```

```c
#include <stdio.h>
union data{
    int a;
    char b;
    int c;
}; // 代表a,b,c会只在同一个内存空间。

int main()
{
   union data data_1;
   data_1.b ='C';
   data_1.a =10; // 后面被赋值的成员才是真正起作用的成员
   return 0;
}
```

>优点是节省一部分的开销。缺点: 同一时刻只能存储一个成员。

比如，对b进行赋值，对a进行赋值。以最后一个赋值为准，因为所有成员共享一块内存。
(后赋值的会把前面的覆盖掉)

>共用体类型的长度是所有成员中最长的那个成员的长度。比如上面的例子中int有四个字节，char只有一个字节。int就是最长的，因此这个共用体类型就占四个字节。

```c
union data data_1 = {10};
```

>因此在对公用体或联合体赋值的时候，只能给一个变量。

**对于结构体来说，这个是不一样的**

```c
struct data{
    int a;
    char b;
    int c;
};
```
>可能会下意识的以为struct占用的内存空间大小是这几个成员变量的大小之和。 `4+1+4=9`

结构体的内存大小占用，涉及字节对齐，是一种计算机用空间换取时间的方式。

```
大小 = 最后一个成员的偏移量+最后一个成员的大小+(可选)末尾填充字节数。
```

>偏移量就是某一个成员的实际地址和结构体首地址之间的距离。(偏移量，实际地址和结构体首地址之间的距离)

- 对于成员a来说，a的地址就是结构体的首地址，偏移量0;
- b的偏移量4，自身大小为1;
- 结构体字节对齐准则: 每个结构体相对于首地址的偏移量都得是当前成员所占内存大小的整数倍，否则就会加上填充字节。
- c的偏移量为5，c自身大小为4.因为5不是4的整数倍，字节对齐时要补齐为8.然后加上c自身的4。
所以整个占用12。
- 然后再判断这个大小12是不是结构体中最宽的基本类型成员的整数倍。

>例子中最宽的是int，4可以被12整除。 如果不能，c之后也要填充末尾填充字节数。

union共用体是多种不同数据类型的合集，所占字节按照共用体里面所占内存空间最大的类型决定。

>例如有char(1字节)型和int(四字节)型，按照int型来计，整个共用体所占四个字节;
此外,共同体里面所有数据的地址是相同的,这个决定了它在有多种数据类型的时候,有且只能存放这些数据类型里面的一种数据。以最后一次赋值为准。

struct结构体也是不同数据类型的合集，所占字节按照里面所有数据类型的长度来决定.

>例如：char(1字节)和int(4字节),struct所占空间是8个字节,不是5个字节,原因是涉及到字节对齐,字节对齐是为了方便计算机快速的读取数据。

```c
vim struct_size.c
```

```c
#include <stdio.h>
struct data{
    int a;
    char b;
    int c;
};
int main(){
   // union data data_1;
   //data_1.b ='C';
   // data_1.a =10;
   printf("%lu\n",sizeof(struct data));

   return 0;
}
```

```c
gcc struct_size.c -o struct_size.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/hhhChaL7GD.png?imageslim)

>这里的12是这样计算来的，a是第一个成员，偏移量为0.b偏移量为4，b自身大小为1，可以整除，不用补字节，c偏移量为5，自身大小为4，字节对齐为8，加上自身大小4，12了。

然后判断12是不是结构体中最宽的基本类型成员的整数倍。

- `%p`表示输出这个指针
- `%d`表示后面的输出类型为有符号的10进制整形，
- `%u`表示无符号10进制整型，
- `%lu`表示输出无符号长整型整数(long unsigned)


```
vim union_address.c
```

```c
#include <stdio.h>
union data{
    int a;
    char b;
    int c;
}; // 代表a,b,c会只在同一个内存空间。

int main()
{
    union data data_1;
    data_1.b ='C';
    data_1.a =10;
    printf("%p\n%p\n%p\n",&data_1.a,&data_1.b,&data_1.c);
    return 0;
}
```

```
gcc union_address.c -o union_address.out
./union_address.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/KF4jmFH9Kh.png?imageslim)

共用体中成员变量的地址全部相同。

### Linux C 动态数据结构-静态链表

(之前使用到的都是)静态数据结构：

- 如：整型、浮点型、数组。
- 特点: 系统分配固定大小的存储空间

之后程序运行的时候，空间的位置和容量都不会再改变了。

>比如我们在使用数组的时候，数组的长度就必须事先定义好。但是很多时候我们不知道。

需要一个可以动态存储分配的数据结构。也就是可变大小的数据结构。

链表：

- 有一个头指针变量head，存放地址，地址指向第一个元素。没有头指针链表无法访问
- 链表中的每一个元素都是一个节点。
- 每个节点里包含两部分，包括用户需要的数据和下一个节点的地址，**各个元素的地址不一定是连续的(与数组的区别)**

![mark](http://myphoto.mtianyan.cn/blog/180705/8h1JI27hHd.png?imageslim)

>指向为空时链表结束。 在链表里访问某一个元素，必须通过上一个元素提供的下一个元素的地址才行。

想访问B元素，得找到a元素中存放的b元素的地址才能访问到b元素。

**静态链表：**

>(所有节点都是在程序中定义的，而不是临时开辟的）

【由三个武器信息的节点组成，所以用结构体类型作为节点元素】

```
vim struct_weapon_link.c
```

```c
#include <stdio.h>

struct weapon{
    int price;
    int atk; // 节点的数据部分

    struct weapon * next; // 下一节点的地址
};

int main()
{
   struct weapon a,b,c,*head; // 除过三个武器，还要定义一个头指针
   a.price =100;
   a.atk = 100;
   b.price =200;
   b.atk =200;
   c.price =300;
   c.atk =300;

   // 连接成链表
   head = &a;
   a.next =&b;
   b.next =&c;
   c.next = NULL;

   struct weapon *p;
   p =head;
   while(p!=NULL){
	 printf("%d,%d\n",p->atk,p->price);
	 p=p->next;
   }
}
```

```
gcc struct_weapon_link.c -o struct_weapon_link.out
./struct_weapon_link.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/GD8A8aaEhJ.png?imageslim)

>静态链表，所有的节点都是在程序中去定义的，而不是临时开辟的。

链表有一个头指针和尾指针，每个指针指向的是链表下一个数据的地址。

在结构体里面加入指针就构成链表，此时指针结构体包括两个部分，一个是信息域(数据域)，另一个是指针域。

### Linux C 动态数据结构-动态链表

链表：可以用`malloc`来动态分配所需的内存，并且需要用`free`手动释放在堆里面申请的内存。

程序执行过程中从无到有的建立起一个链表，也就是说需要一个一个的开辟新节点，输入新节点的数据，然后建立起前后相连的关系。

建立武器信息的单向动态链表：


```
vim dynamic_linked_list.c
```

```c
#include <stdio.h>
#include <malloc.h>

struct weapon{
  int price;
  int atk;
  struct weapon * next;
};

// 需要一个创建链表的函数，返回值是链表的头指针，返回类型是struct weapon *
struct weapon * create(){
   struct weapon *head;
   struct weapon *p1,*p2; // 3个指针都用来指向struct weapon类型数据,p1,p2分别指向当前新创建的节点和上一个节点。
   int n=0;// 临时变量，记录当前链表中节点个数
   // malloc分配内存块的函数，sizeof判断数据类型长度符
   // (int)malloc(16) 分配16个int型内存块
   p1=p2=(struct weapon*)malloc(sizeof(struct weapon));

   // 从键盘输入数据，给第一个节点。
   scanf("%d,%d",&p1->price,&p1->atk);
   head = NULL;// 一开始链表不存在，置空

   while(p1->price!=0){ // 约定price为0时停止输入
     n++;
     if(n==1) head=p1;
     else p2->next=p1;

     p2=p1; // 保留p1当前所指向的的地址，保留上一个节点。

     //需要开辟一个新的动态存储区，把这个的地址载给p1
     p1=(struct weapon*)malloc(sizeof(struct weapon));
     scanf("%d,%d",&p1->price,&p1->atk);//开辟后输入数据
}
p2->next=NULL;
return (head);
}//p1,p2一个用来指向链表新创立的节点，一个用来指向下一个节点
int main()
{
   struct weapon *p;
   p=create(); // p成为链表的头指针
   printf("%d,%d\n",p->price,p->atk);//打印第一个节点的信息
   return 0;
}
```

```
gcc dynamic_linked_list.c -o dynamic_linked_list.out
./dynamic_linked_list.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/BB958l3GII.png?imageslim)

```c
   while(p!=NULL){
   printf("%d,%d\n",p->atk,p->price);
   p=p->next;
   }
```

![mark](http://myphoto.mtianyan.cn/blog/180705/6fFAfl9dlH.png?imageslim)

### C语言中的位运算符:按位与、按位或、按位异或、左移和右移

#### LInux C 位运算之按位与

- 位：指二进制数中的一位 0 false 1 true
- 古老的微处理器速度：比加减运算快一些，比乘除法快很多
现在的框架中：通常与加减运算快相同，比乘除法快很多

六种位运算符

- & 按位与
- | 按位或
- ^按位异或
- ~按位取反
- <<左移
- >>右移

```
vim and_operation.c
```
- 位运算就是将参与运算的两个数据按照对应的二进制数逐位进行逻辑与运算。
- 参与运算的两个数必须是整型或者是字符型。
- 而且参与运算的数必须要以补码的方式出现。

```c
#include <stdio.h>

int main()
{
   // & | ^ ~ << >>

   int a = 4; //0100 int占用4字节，32位补码。
   int b = 7; //0111

   int c = a&b; //0100 逻辑与运算

   printf("%d\n",c);
   return 0;
}
```

```
gcc and_operation.c -o and_operation.out
./and_operation.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/4Jk3idiClL.png?imageslim)

按位与的应用

- 迅速清零(对于一个数中为1的位,让另一个数的相应位为0); 

任何一个数和0做按位与结果一定是0

- 保留指定位置(对另一个数的相应位置1); 取a的低8位，将b的低八位全部置为一，按位与即可。
- 奇偶判断（a和1做与运算）[a&1 //得到结果1为奇数，得到0为偶数]


```
vim odd_even.c
```

```c
#include <stdio.h>

int main()
{
   // & | ^ ~ << >>

   int a =4;//0100
   int b =7;//0111

   int c =a&1;//0100

   int d =b&1;//0100

   printf("%d\n",c);
   printf("%d\n",d);
   return 0;
}
```

输出为0,1; 输出为0是偶数，输出为1是奇数。 

>因为除过最后一位前面的都一定是2的倍数了。最后一位为1，表示是奇数。
最后一位为0，表示是偶数。

```
gcc odd_even.c -o odd_even.out
./odd_even.out
```

### 按位或运算。

将参与运算的两个数据按位进行逻辑或(有一个1的时候结果就是1)运算

```
vim bit_or.c
```

```c
#include <stdio.h>

int main()
{
   // & | ^ ~ << >>

   int a =9; //1001
   int b =5; //0101

   int c =a|b;//1101

   printf("%d\n",c);
   return 0;
}
```

```
gcc bit_or.c -o bit_or.out
./bit_or.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/Jm06Abd1hJ.png?imageslim)

>输出为1101(13)

**按位或的作用：**

设定数据的指定位,与255(0xFF)做按位或运算

比如我们想让9低八位的数据位设置为1.

>`a = a | 0xFF;` 设定数据a的指定二进制数后8位置为1


```c
vim bit_or_8.c
```

```c
#include <stdio.h>

int main()
{
   // & | ^ ~ << >>

   int a =9; //1001
   int b =5; //0101

   int c =a|b;//1101

   printf("%d\n",c);

   int a =a|0xff;

   printf("%d\n",a);
   return 0;
}
```

```
gcc bit_or_8.c -o bit_or_8.out
./bit_or_8.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/hcFlbJL3HC.png?imageslim)

### 按位异或`^`

将参与运算的两个数据按对应的二进制数逐位进行逻辑异或运算.只有对应位结果互斥，结果才为真。

```
vim bitwise_xor.c
```

```c
#include <stdio.h>

int main()
{
   // & | ^ ~ << >>

   int a =9; //1001
   int b =5; //0101

   int c =a^b;//1100

   printf("%d\n",c);
   return 0;
}
```

```
gcc bitwise_xor.c -o bitwise_xor.out
./bitwise_xor.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/L1ed6J1aAe.png?imageslim)

- 定位反转  让a中所有的0变成1,1变成0。

```
a^0xff;
```

- 数值交换

```
a= a^b;
b= b^a;
a= a^b;
```

```
vim bitwise_xor_change.c
```

```c
#include <stdio.h>

int main()
{
   // & | ^ ~ << >>

   int a =9; //1001
   int b =5; //0101

   a= a^b;
   b= b^a;
   a= a^b;
   printf("%d\n%d\n",a,b);
   return 0;
}
```

```
gcc bitwise_xor_change.c -o bitwise_xor_change.out
./bitwise_xor_change.out
```

>成功的将a,b进行了调换

![mark](http://myphoto.mtianyan.cn/blog/180705/EAigagg5cb.png?imageslim)

涉及到的运算原理可以具体如下阐述:(下面的= 是等于的意思 而非赋值号)

```
P0. x^x=0
P1. a^0=a
P2. c=a^x --> a=c^x (a=a^x^x=a^0=a)
```

故有交换 解释:

a^=b; 起先 a被赋值为 a^b
b^=a; 此时 b被赋值成最开始的a值,而a保持上一步骤中的结果值不变
a^=b; 此时 a被赋值成最开始的b值,而b保持上一步骤中的结果值不变

### 按位取反

唯一的一个单目运算符，右结合性。把零换成1,1换成0

```
~1000 = 0111
```

### 左移：高速乘以2; 右移：高速除以2

左移：将数据对应的二进制值逐位**左移**若干位;

>高位会被舍弃掉，低位补零; 相当于乘以2的n次方

**左移需要注意的是int是一个有符号的类型，移动过程中把符号位移出去了会溢出**

右移：将数据对应的二进制值逐位**右移**若干位

mtianyan: 低位丢弃，无符号数补零，有符号数，高位补0或1(根据符号位判断，就是正数数补0，负数补1); 相当于除以2的n次方。

```
vim left_right_shift.c
```

```c
#include <stdio.h>

int main()
{
   // & | ^ ~ << >>

   int a =3; //0000 0011
   a = a<<4; //0011 0000 32+16=48

   printf("a=%d\n",a);

   int i =1; // 0000 0001
   i = i<<33; // 相当于i<<1
   printf("i=%d\n",i);
   // 当移位位数超过该数值类型的最大位数时，编译器会用移位位数去模该类型位数，然后按照余数进行移位。 

   int b = 4;
   b = b>>1;

   printf("b=%d\n",b);
   return 0;
}
```

```
gcc left_right_shift.c -o left_right_shift.out
./left_right_shift.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/Lb5j1geJJI.png?imageslim)

>可以看到会报出warning

### 递归函数之递归调用

递归调用就是在调用函数的过程中，被调用的函数调用它本身的过程。

递归调用有时候会牺牲效率

```
vim recursiv_call.c
```

```c
#include <stdio.h>
void func(){
  printf("1\n");
  func();
  }

int main()
{
  func();
  return 0;
}
```

```
gcc recursiv_call.c -o recursiv_call.out
./recursiv_call.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/eKJDcKf6IF.png?imageslim)

>无尽地输出1，然后爆出段错误，核心已转储

因此我们的递归是要加上条件的。适当的时候选择是否递归，因为递归在某些时候会牺牲效率。


使用递归求阶乘

```
vim recursiv_call_factorial.c
```

```c
#include <stdio.h>
int func(int n)
{
    int r =0;
    if(n<0){
	  printf("error");
    }else if(n==0 || n==1){
    return 1;
    }else{
        r =n *func(n-1);
        return r;
    }
 }

int main()
{
   int n =0;
   printf("please input the num:");
   scanf("%d",&n);
   // 使用func求阶乘
   int result = func(n);
   printf("the result is %d\n",r);
   return 0;
}
```

```
gcc recursiv_call_factorial.c -o recursiv_call_factorial.out
./recursiv_call_factorial.out
```

![mark](http://myphoto.mtianyan.cn/blog/180705/084347FB5i.png?imageslim)

>注意这里递归的整型溢出

### 递归函数之递归原理

递归是一种编程技巧，函数调用过程中函数体内又调用了它自己

函数调用的过程:

![mark](http://myphoto.mtianyan.cn/blog/180705/1kfF57kidi.png?imageslim)

函数A调用函数B,main函数中调用A,A中调用了B,B有两个参数，a和b被称为形参。

函数没有被调用的时候，形参是不会被分配内存单元的。在A中调用了B，A就被称为主调函数。

主调函数中调用一个函数的时候，这个函数里的参数被称为实参。

![mark](http://myphoto.mtianyan.cn/blog/180705/5i9E59c1fj.png?imageslim)

函数调用所需要做的第一件事:

为被调用的函数(B)的形参分配一个临时的内存单元然后才能把两个对应的实参的值传递进来。

同时还需要传递的是主调函数(A)的返回地址。（俗称保护现场）

之所以要把A的返回地址保存起来，是因为被调函数(B)执行完了还需要继续执行主调函数(A)后面的代码。

通过return语句将函数计算后的值带回到主调函数。

保护现场时传递的返回地址，参数，函数调用结束的返回值。这些数据都保存在栈中。

递归是调用自身，但自身也是函数调用，本质就是函数的调用。

![mark](http://myphoto.mtianyan.cn/blog/180705/3IbaCi1JJC.png?imageslim)

求阶乘的函数，由于递归也是符合函数调用原则的，所以所有被调用的函数都会创建一个副本，为各自的调用者服务，不受其他函数影响。递归函数被调用多少次，就会创建多少个它自身的副本。

>这个副本就好像是一个新的函数一样。系统会用栈来管理它的内存。它是一个独立的存在，完全可以理解为这已经是一个新的func了。它被分配了独立的内存单元。

![mark](http://myphoto.mtianyan.cn/blog/180705/kgjji1ilil.png?imageslim)

>递归：大规模——>化简——>小规模，直到问题可求。
递归函数同时必须有 递归条件和递归表达式，否则会进入死循环。
递推(for)：则是由小问题的解逐步代入大问题并求出解。

![mark](http://myphoto.mtianyan.cn/blog/180705/c3K62gj5jf.png?imageslim)

### 总结

- 编译预处理：展开头文件、宏替换

- 自定义数据类型：结构体、联合体、链表实现，静态动态链表。结构体涉及字节对齐，共同体所有成员共用一个地址, 结构体内存占用计算方法。

- 逻辑运算符位运算

![mark](http://myphoto.mtianyan.cn/blog/180705/ekG8C2mJ4d.png?imageslim)

- 递归调用，递归思想和递推


