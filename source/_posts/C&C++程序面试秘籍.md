# 1.	C/C++程序基础

## 1.	一般赋值语句

```C
#include <stdio.h>

int main (){
    int x = 3, y, z;
    x *= (y = z = 4);
    printf("x = %d\n", x);
    z = 2;

    x =(y = z);
    printf("x = %d\n",x);
    x =(y == z);
    printf("X = %d\n",x);
    x = (y & z);
    printf("X = %d\n",x);
    x = (y && z);
    printf("X = %d\n",x);

    y = 4;
    x = (y  | z) ;
    printf("x = %d\n",x);
    x= ( y || z);
    printf("x = %d\n",x);

    x = (y == z) ? 4:5;
    printf("x = %d\n", x);

    x = (y == z) ? 1 : (y<z) ? 2 : 3;
    printf("x = %d\n",x);

    return  0;

}
```

## 2.	C++域操作符

```Cpp
#include <iostream>

int value = 0;
void printvalue(){
    printf("value = %d\n",value);
}

int main (){
    int value = 0;
    value = 1;
    printf("value = %d\n",value);
	//1
    
    ::value = 2;
    printvalue();
	//2
    return 0;
}
//C中无法通过编译,14行报错
//C++中无错误,在C++中可以通过域操作符::来直接操作全局变量
```

## 3.	i++和++i的区别

```cpp
#include <iostream>

int main(void) {
    int i = 8;
    printf("%d\n", ++i);
    //9
    printf("%d\n", --i);
    //8
    printf("%d\n", i++);
    //8
    printf("%d\n", i--);
    //9
    printf("%d\n", -i++);
    //-8
    printf("%d\n", -i--);
    //-9
    printf("------\n");
    return 0;
}	
```

## 4.	i++与++i哪个效率更高

```Cpp
#include <stdio.h>

int main() {
    int i = 0;
    int x = 0;
    i++;
    ++i;
    x = i++;
    x = ++i;
    return 0;
}
//内建数据类型的情况，效率没有区别。
//自定义数据类型(尤其是class时)的情况，++i 效率较高。因为(++i)可以返回对象的引用,而(i++)必须返回对象的值.
//后缀式（i++）必须产生一个临时对象保存更改前对象的值并返回，所以导致在大对象的时候产生了较大的复制开销，引起效率降低
```

## 5.	 选择编程风格良好的条件比较语句

```
#include <iostream>
//A.假设布尔变量名字为flag,它与零值比较的标准if语句如下。
//1
    if (flag == TRUE)
    if (flag == FALSE)
//2
    if (flag)
    if (!flag)
//A的第二种风格较良好。根据布尔类型的语义，零值为“假”(记为FALSE)，任何非零值都是“真”(记为TRUE)。TRUE的值究竟是什么并没有统一的标准。例如Visual C++将TRUE定义为1，而Visual Basic则将TRUE定义为-1。因此不可将布尔变量直接与TRUE、FALSE进行比较。

//B.假设整型变量的名字为value,它与零值比较的标准if语句如下。
//1
    if (value == 0)
    if (value != 0)
//2
    if (value)
    if (!value)
//B的第一种风格较良好，第二种风格会让人误解value是布尔变量，应该将整型变量用“==” 或“!=”直接与0比较。

//C.假设浮点变量的名字为x，它与0.0的比较如下。
//1
    if (x == 0.0)
    if (x != 0.0)
//2
    if ((x >= -EPSINON) && (x <= EPSINON))      //EPSINON为允许的误差(精度)
    if ((x < - EPSINON) || (x > EPSINON))
//C的第二种风格较为良好.注意:无论是float还是double类型的变量,都有精度限制.所以一定要避免将浮点变量用“==” 或“!=”与数字比较,应该设法转换成“>=” 或“<=”形式

//D 指针变量p与0的比较如下。
//1
    if (p == 0)
    if (p != NULL)
//2
    if (p == 0)
    if (p != 0)
//D的第一种风格较良好，指针变量的零值是“空”(记为 NULL)。尽管NULL的值与0相同，但是两者意义不同。用p与NULL显式比较，强调p是指针变量。如用p与0比较，容易让人误解p是整型变量。

```

## 6.	√有符号变量与无符号变量的值的转换

```
#include <stdio.h>
#include <iostream>

char getChar(int x,int y){
    char c;
    unsigned int a = x;
    printf("unsigned y = %u\n",y);
    (a+y >10)?(c=1):(c=2);
    return c;
}
int main(void){
    char c1 = getChar(7, 4);
    char c2 = getChar(7, 3);
    char c3 = getChar(7, -7);
    char c4 = getChar(7, -8);
    printf("c1 = %d\n",c1);
    printf("c2 = %d\n",c2);

    printf("c3 = %d\n",c3) ;
    printf("C4 = %d\n",c4) ;
    return 0;

}
//c1 = 1
//c2 = 2
//c3 = 2
//C4 = 1
//注意:当表达式中存在有符号类型和无符号类型时，所有的操作数都自动转换成无符号类型。
```

## 7.	不使用任何中间变量如何将a,b的值进行交换

```Cpp
#include <stdio.h>

void swap1(int& a, int& b)
{
    int temp = a; //1使用局部变量temp完成交换
    a=b;
    b = temp;
};

void swap2(int &a, int &b)
{
//缺点是加减法是容易导致数据溢出
    a=a+b; // 1使用加减运算完成交换
    b=a-b;
    a=a-b;
};

void swap3(int &a, int &b)
{
    a^=b; //使用异或运算完成交换
    b^=a;
    a^=b;
};

int main(void)
{
    int a1=1,b1=2;
    int a2=3,b2=4;
    int a3=5,b3=6;
    int a = 2147483647,b = 1;
    swap1(a1,b1); //测试使用临时变量进行交换的版本
    swap2(a2,b2); //测试使用加减运算进行交换的版本
    swap3(a3,b3); //测试使用异或运算进行交换的版本
    printf("after swap... \n") ;
    printf("a1 = %d,b1 = %d\n", a1, b1);
    printf("a2 = %d,b2 = %d\n", a2, b2) ;
    printf("a3 = %d,b3 = %d\n", a3, b3) ;
    swap2(a,b);
    printf("a = %d, b = %d\n",a, b);
    return 0;
}

```

异或原理：相同为0,0与不为0的a异或为a。且满足交换律和结合律。

原理：

- a=a^b；
- b = b ^ a = b ^ (a ^ b) = b ^ a ^ b = b ^ b ^ a = 0 ^ a = a；
- a = a ^ b = (a ^ b) ^ a = a ^ a ^ b = 0 ^ b = b;

## 8.	 C++与C有什么不同

C是一个结构化语言，它的重点在于算法和数据结构。对语言本身而言, C是C++的子集。C程序的设计首要考虑的是如何通过一个过程， 对输入进行运算处理，得到输出。对于C++,首要考虑的是如何构造一个对象模型，让这个模型能够配合对应的问题，这样就可以通过获取对象的状态信息得到输出或实现过程控制。

因此，C与C++的最大区别在于，他们用于解决问题的思想方法不一样。

C实现了C++中过程化控制及其他相关功能。而在C++中的C,相对于原来的C还有所加强，引入了重载、内联函数、异常处理等。C++更是拓展了面向对象设计的内容，类、继承、虚函数、模板和包容器类等。

在C++中，不仅需要考虑数据封装，还需要考虑对象粒度的选择、对象接口的设计和继承、组合与继承的使用等问题。

相对于C，C++包含了更丰富的设计概念。

## 9.	 如何理解C++是面向对象化的，而C是面向过程化的

C是面向过程化的，但是C++不是完全面向对象化的。在C++中也完全可以写出与C一样过程化的程序，所以只能说C++拥有面向对象的特性。Java 是真正面向对象化的。

## 10.	 √标准头文件的结构

```Cpp
#ifndef __INCvxWorksh
#define __INCvxWorksh
#ifdef __cplusplus      //使用C++编译器
//ifdef __STDC__		//使用C编译器
//首先，被它修饰的目标是'extern'的。也就是告诉编译器，其声明的函数和变量可以在本模块或其他模块中使用。通常，在模块的头文件中对本模块提供给其他模块引用的函数和全局变量以关键字extern声明。
extern "C"{
#endif
/*
 *
 */
#ifdef  __cplusplus
};
#endif
#endif /* __INCvxWorksh */



//1,2,13行的作用是防止该头文件被重复引用。
//代码第3、4行指定编译器
//

```

其次，被它修饰的目标是“C“的，意思是其修饰的变量和函数是按照C语言方式编译和连接的。我们来看看C++中对类似C的函数是怎样编译的。作为一种面向对象的语言，C++语言支持函数重载，而C不支持。函数被C++编译后在符号库中的名字与C语言的不同，如下:

```
void foo( int x，int y);
void foo( int x，float y );
```

这两个函数编译生成的符号是不相同的，前者可能为_foo_int_int 之类，而后者可能为_foo_int_float之类。可以发现，这样的名字包含了函数名、函数参数数量及类型信息，C++就是靠这种机制来实现函数重载的。这样，如果在C中连接C++编译的符号时，就会因找到符号问题发生连接错误。
    如果加extern "C"声明后，模块编译生成foo的目标代码时，就不会对其名字进行特殊处理，采用了C语言的方式，也就是_foo之类，不会加上后面函数参数数量及类型信息相关的那一串了。因此exten "C"是C++编译器提供的与C连接交换指定的符号，用来解决名字匹配问题。

## 11.	 #include <head.h>和#include "head.h"有什么区别

尖括号< >表明这个文件是一个工程或标准头文件。查找过程会首先检查预定义的目录，我们可以通过设置搜索路径环境变量或命令行选项来修改这些目录。

如果文件名用一对引号括起来，则表明该文件是用户提供的头文件，查找该文件时将从当前文件目录(或文件名指定的其他目录)中寻找文件，然后在标准位置寻找文件。

## 12.	 C++中main函数执完后还执行其他语句吗?

很多时候，我们需要在程序退出的时候做一些诸如释放资源的操作，但程序退出的方式有很多种，例如main()函数运行结束，在程序的某个地方用exit()结束程序，用户通过Ctrl+C等操作发信号来终止程序，等等，因此需要有一种与程序退出方式无关的方法来进行程序退出时的必要处理。方法就是用atexit()函数来注册程序正常终止时要被调用的函数。

atexit()函数的参数是一个函数指针，函数指针指向一个没有参数也没有返回值的函数。

在一个程序中最多可以用atexit()注册32个处理函数，这些**处理函数的调用顺序与其注册的顺序相反**，即最先注册的最后调用，最后注册的最先调用。请看下面的程序代码。

```
#include<stdlib.h>   //使用atexit()函数必须包含头文件stdlib.h
#include<stdio.h>

void fn1(void);
void fn2(void) ;

int main(void) {
    atexit(fn1);   //使用atexit注册fn1()函数
    atexit(fn2);   //使用atexit注册fn2()函数
    printf("main exit.. . \n");
    return 0;
}
void fn1() {
    printf("calling fn1()...\n");   //fn1()函数打印内容
}
void fn2() {
    printf("calling fn2()...\n");   //fn2()函数打印内容
}

//main exit.. .
//calling fn2()...
//calling fn1()...
```

# 2.	预处理、const、static 与sizeof

## 1.	预处理的使用

```cpp
#include <stdio.h>
#include <stdlib.h>

#define DEBUG

int main() {
    int i = 0;
    char c;
    while (1) {
        i++;
        c = getchar();
        if (c != '\n') {
            getchar();
        }
        if (c == 'q' || c == 'Q') {
#ifdef DEBUG
            printf("we got:%c, about to exit.\n", c);
#endif
            break;
        } else {
            printf("i = %d", i);
#ifdef DEBUG
            printf(",we got:%c", c);
#endif
            printf("\n");
        }
    }
    return 0;
}
//a
//i = 1,we got:a
//v
//i = 2,we got:v
//q
//we got:q, about to exit.
```

## 2.	用#define实现宏并求最大值和最小值

```c++
#define MAX(x,y)  ( ( (x) > (y) ) ? x : y )
#define MIN(x,y)  ( ( (x) < (y) ) ? x : y )

//(1) #define 在宏上应用的基本知识。
//(2)三元运算符(? :)的知识。这个运算符能产生比if-else 更优化的代码，并且书写上更加简洁明了。
//(3)在宏中需要把参数小心地用括号括起来。因为宏只是简单的文本替换，如果不注意，很容易引起歧义。
```

## 3.	宏定义的使用

```cpp
#include <stdio.h>
#define SQR(x) (x*x)
int main() {
    int a, b = 3;
    a = SQR(b + 2);
    printf("a = %d\n",a);
    return 0;
}
//因为宏只是简单的文本替换，在第六行展开为a = (b + 2 * b + 2);输出为11.
//应改为#define SQR(x) ((x)*(x)),此时输出为25.
```

## 4.	代码写输出----宏参数的连接

```c+
#include <stdio.h>
#define STR(s)  #s
#define CONS(a,b) (int) (a##e##b)
int main()
{
    printf(STR(vck)) ;
    printf("\n");
    printf("%d\n",CONS(2,3)) ;
    return 0;
}
//vck
//2000
```

**用#把宏参数变为一个字符串，用##把两个宏参数贴合在一起。**
		  第12行中STR(s)定义的是一个参数s表示的字符串。在第8行的调用中，STR(vck)实际表示就是字符串"vck"。第13行中CONS(a,b)定义的是一一个将参数a与b按aeb连接起来的一个整型值。在第18行的调用中，CONS(2,3)实际表示就是整型值2e3，也就是十进制数2000。

## 5.	**用宏定义得到一个字的高位和低位字节**

```
#include <stdio.h>
#include <stdlib.h>

#define WORD_LO(x) ((int)((x) & 15))
#define WORD_HI(x) ((int) (x) >> 4)

int main (){
    printf("%d\n", sizeof(int));        //int 为4位
    printf("%d\n",WORD_LO(31));
    printf("%d\n", WORD_HI(31));
    return 0;
}
//15
//1
//31的二进制为0001 1111；
//低八位为1111 所以对应的十进制为15
//高八位为0001 所以对应的十进制为1
```

## 6.	用宏定义得到一个数组所含的元素个数

```c++
#include <stdio.h>

#define ARR_SIZE(a) (sizeof((a)) / sizeof((a[0])))

int main() {
    char arr[] = "qwertyuiop";
    int a[] = {2, 3, 4, 5};
    printf("%d\n", ARR_SIZE(arr));
    printf("%d\n", ARR_SIZE(a));
}

```

## 7.	找错----const 的使用

详细见[常量指针与指针常量的区别](#指针常量与常量指针的区别)

```cpp
#include <stdio.h>

int main() {
    const int x = 1;
    //声明时必须初始化
    int b = 10;
    int c = 20;

    //常量指针:指针指向的地址可更改,但确定指针后，该地址的内容为常量，不可更改,声明时可以不初始化
    const int *a1 = &b;
    
    //指针常量:指针的内容可更改,指针指向的地址为常量,声明时必须初始化
    int* const a2 = &b;
    
    //地址和内容都不可修改,声明时必须初始化
    const int *const a3 = &b;
    
    
    x = 2;          //(×)
    //常数(const)不可更改

    //int const *型  (常量指针)
    a1 = &c;        //(√)
    *a1 = 1;        //(×)
    //将1隐式转换为const int *a型,即变为地址,但所改地址为系统保留,报断错误.

    //int * const 型   (指针常量)
    a2 = &c;        //(×)
    *a2 = 1;        //(√)

    //const int *const 型
    a3 = &c;        //(×)
    *a3 = 1;        //(×)

    return 0;
}
```

**常量指针**的本质是指针，指针指向的是一个**常量**的地址。所以指针存放的常量的地址可更改，确定地址后，改地址对应的内容不可更改。因此修改指向的常量的地址从而间接修改指针指向的值。

**指针常量**的本质是常量，因此指针指向的地址是常量，不可更改，而指针指向的地址内容可以更改。

## 8.	说明const与#define的特点及区别

```C++
#include <stdio.h>

#define PI 3.1415926

int main () {
    float angel;
    angel = 30 * PI / 180;
    printf("%f", PI);
}
```

当程序进行编译的时候，编译器会首先将“#define Pi 3.1415926”以后所有代码中的“PI”全部换成“3.1415926"，然后进行编译。因此，#define常量则是一个Compile-Time概念，它的生命周期止于编译期，它存在于程序的代码段，在实际程序中它只是一个常数、一个命令中的参数，并没有实际的存在。
		  const常量存在于程序的数据段，并在堆栈分配了空间。const 常量是一个Run-Time的概念，它在程序中确确实实地存在着并可以被调用、传递。const 常量有数据类型，而宏常量没有数据类型。编译器可以对const常量进行类型安全检查。

## 9.	C++中const有什么作用(至少说出3个)

 (1) const 用于定义常量: const 定义的常量编译器可以对其进行数据静态类型安全检查。
 		 (2) const 修饰函数形式参数:当输入参数为用户自定义类型和抽象数据类型时，应该将“值传递”改为“const &传递”，可以提高效率。比较下面两段代码:

```cpp
void fun(A a);
void fun(A const &a) ;
```

第一个函数效率低。函数体内产生A类型的临时对象用于复制参数a,临时对象的构造、复制、析构过程都将消耗时间。而第二个函数提高了 效率。用“引用传递” 不需要产生临时对象，节省了临时对象的构造、复制、析构过程消耗的时间。但光用引用有可能改变a,所以加const。

(3) const 修饰函数的返回值:如给“指针传递”的函数返回值加const,则返回值不能被直接修改，且该返回值只能被赋值给加const修饰的同类型指针。例如。

```cpp
const char *GetChar (void){};
char *ch = GetChar(); 			// error
const char *ch = GetChar(); 	// correct
```

(4)const修饰类的成员函数(函数定义体):任何不会修改数据成员的函数都应用const修饰，这样，当不小心修改了数据成员或调用了非const成员函数时，编译器都会报错。const修饰类的成员函数形式为:

```cpp
int GetCount (void) const ;
```

## 10.	static有什么作用(至少说出2个)

在C语言中，关键字static有3个明显的作用:
		(1)在函数体，一个被声明为静态的变量在这一函数被调用的过程中维持其值不变。
		(2)在模块内(但在函数体外)，一个被声明为静态的变量可以被模块内所有函数访问，但不能被模块外其他函数访问。它是一个本地的全局变量。
		(3)在模块内，一个被声明为静态的函数只可被这一模块内的其他函数调用。那就是这个函数被限制在声明它的模块的本地范围内使用。

## 11.	static全局变量与普通的全局变量有什么区别

全局变量的说明之前再加上static就构成了静态的全局变量。全局变量本身就是静态存储方式，静态全局变量当然也是静态存储方式。这两者在存储方式上并无不同。

这两者的区别在于，非静态全局变量的作用域是整个源程序，当一个源程序由多个源文件组成时，非静态的全局变量在各个源文件中都是有效的;而静态全局变量则限制了其作用域，即只在定义该变量的源文件内有效，在同一源程序的其他源文件中不能使用它。由于静态全局变量的作用域局限于一个源文件内，只能为该源文件内的函数公用，因此可以避免在其他源文件中引起错误。

把局部变量改变为静态变量后是改变了它的存储方式，即改变了它的生存期;

把全局变量改变为静态变量后是改变了它的作用域，限制了它的使用范围。

static全局变量与普通全局变量的区别是，static 全局变量只初始化一次， 防止在其他文件单元中被引用。
		 static局部变量和普通局部变量的区别是，static局部变量只被初始化一次，下一次依据上一次结果值。
		 static函数与普通函数的区别是，static函数在内存中只有一份，普通函数在每个被调用中维持一份复制品。

## 12.	看代码写结果----C++类的静态成员

```cpp
#include <iostream>

using namespace std;

class widget {
public :
    widget() {
        count++;
    }

    ~widget() {
        --count;
    }

    static int num() {
        return count;
    }

private:
    static int count;
};


int widget::count = 0;

int main() {
    widget x, y;
    cout << "The Num.is" << widget::num() << endl;
    if (widget::num() > 1) {
        widget x, y, z;
        cout << "The Num.is" << widget::num() << endl;
    }
    widget z;
    cout << "The Num.is" << widget::num() << endl;
    return 0;
}
//The Num.is2
//The Num.is5
//The Num.is3
//通过以上的分析，可以看到运行到代码第26行时，只有两个类widget的实例，运行到代码第30行时，又产生了3个实例，然后这3个实例在第31行结束后被销毁(局部对象)。最后运行到代码第32行又产生了1个实例。
```

## 13.	使用sizeof计算普通变量所占空间大小

```

#include <iostream>
using namespace std;

void Func(char str[100]){
    printf("%d\n", sizeof(str));
}

int main (){

    char str[] = "hello";
    char *p = str;
    int n = 10;

    printf("%d\n", sizeof(str));
    //6

    printf("%d\n", sizeof(p) );
    //8
    
    printf("%d\n", sizeof(n) );
    //4
    
    Func("adsf");
    //8

    void *p1 = malloc(100);
    printf("%d\n", sizeof(p1));
    //8

}

```

如果数组变量被传入函数中做sizeof运算，则和指针的运算没有区别，否则得到整个数组占用内存的总大小。

对于指针,无论是何种类型的指针，其大小都是固定的，在32位WinNT平台下都是4。win64位为8。

## 14.	使用sizeof计算类对象所占空间大小

```cpp
#include <iostream>
using   namespace std;

class A {
public:
    int i;
};

class B {
public:
    char ch;
};

class C {
public:
    int i;
    short j;
};

class D {
public:
    int i;
    short j;
    char ch;
};

class E {
public:
    int i;
    int ii;
    short j;
    char ch;
    char chr;
};

class F {
public:
    int i;
    int ii;
    int iii;
    short j;
    char ch;
    char chr;
};

class G {
public:
    char ch;
    int i;
    short j;
    int ii;
    int iii;
    char chr;
};

int main() {
    cout << "sizeof(int) =" << sizeof(int) << endl;
    cout << "sizeof(short) =" << sizeof(short) << endl;
    cout << "sizeof(char) =" << sizeof(char) << endl;
    cout << endl;
    cout << "sizeof(A) =" << sizeof(A) << endl;
    cout << "sizeof(B) =" << sizeof(B) << endl;
    cout << "sizeof(C) =" << sizeof(C) << endl;
    cout << "sizeof(D) =" << sizeof(D) << endl;;
    cout << "sizeof(E) =" << sizeof(E) << endl;
    cout << "sizeof(F) =" << sizeof(F) << endl;
    cout << "sizeof(G) =" << sizeof(G) << endl;
    return 0;
}
//sizeof(int) =4
//sizeof(short) =2
//sizeof(char) =1
//
//sizeof(A) =4
//sizeof(B) =1
//sizeof(C) =8
//sizeof(D) =8
//sizeof(E) =12
//sizeof(F) =16
//sizeof(G) =24
```



字节对齐的细节和编译器实现相关，一般而言， 需要满足3个准则:

- 结构体变量的首地址能够被其最宽基本类型成员的大小所整除;

- 结构体每个成员相对于结构体首地址的偏移量(offset)都是成员大小的整数倍,如有需要，编译器会在成员之间加上填充字节(internal adding)

- 结构体的总大小为结构体最宽基本类型成员大小的整数信，如有需要，编译器会在最末一个成员之后加上填充字节(trailing padding)。

**注意**:在结构体或类中,最宽基本类型成员的**前面**皆按最大值处理,之后按照能否整除最大值填充字节(trailing padding).

## 15.	使用sizeof 计算含有虚函数的类对象的空间大小

```cpp
#include <iostream>
#include <stdio.h>

using namespace std;

class Base {

public:
    Base(int x) : a(x) {
    }

    void print() {
        cout << "base" << endl;
    }

private :
    int a;
};

class Derived : public Base {

public:

    Derived(int x) : Base(x - 1), b(x) {

    }

    void print() {
        cout << "derived" << endl;
    }

private:
    int b;
};

class A {
public:
    A(int x) : a(x) {
    }

    virtual void print() {

        cout << "A" << endl;
    }

private:
    int a;
};

class B : public A {
public:
    B(int x) : A(x - 1), b(x) {
    }

    virtual void print() {
        cout << "B" << endl;
    }

private :
    int b;
};

int main() {
    printf("sizeof(int)%d\n", sizeof(int));
    
    printf("int* :%d\n", sizeof(int *));
    printf("char *:%d\n", sizeof(char *));
    printf("double *:%d\n", sizeof(double *));
    printf("float *:%d\n", sizeof(float *));


    Base obj1(1);
    cout << "size of Base obj is" << sizeof(obj1) << endl;;
    Derived obj2(2);
    cout << "size of Derived obj is" << sizeof(obj2) << endl;
    A a(1);
    cout << "size of A obj is" << sizeof(a) << endl;
    B b(1);
    cout << "size of B obj is" << sizeof(b) << endl;
    return 0;
}

//sizeof(int)4
//int* :8
//char *:8
//double *:8
//float *:8
//size of Base obj is4
//size of Derived obj is8
//size of A obj is16
//size of B obj is16
```

对于Base类来说，它占用内存大小为sizeof(int),等于4, print()函数不占内存。

对于Derived类来说，比Base类多一个整型成员， 因而多4个字节，一共是 8个字节。
		对于A类来说，由于它含有虚函数，因此占用的内存除了一个整型变量之外，还包括一个隐含的虚表指针成员，但是对于union、class、struct等来说，都采用的字节对齐方式，因此是16个字节。
		对于B类来说，比A类多一个整型成员，因而多4个字节，一共是16个字节。

**union、class、struct等大小与成员的先后顺序（字节对齐）有关。与权限的先后位置有关与否还未知**

**在32为平台。指针长度为4,而在64位平台指针长度为8。任意类型指针都是**

可以看出，普通函数不占用内存，只要有虚函数，就会占用一个指针大小的内存，原因是系统多用了一个指针维护这个类的虚函数表，并且注意这个虚函数无论含有多少项(类中含有多少个虚函数)都不会再影响类的大小。

## 16.	√使用sizeof计算虚拟继承的类对象的空间大小

```cpp
#include <iostream>

using namespace std;

class A {

};

class B {

};

class C : public A, public B {

};

class D : virtual public A {

};

class E : virtual public A, virtual public B {

};

class F{

public:
    int a;
    static int b;
};

int F::b = 10;

int main() {
    cout << "sizeof(A) ="<< sizeof(A) << endl;
    cout << "sizeof(B) ="<< sizeof(B) << endl;
    cout << "sizeof(C) ="<< sizeof(C) << endl;
    cout << "sizeof(D) ="<< sizeof(D) << endl ;
    cout << "sizeof(E) ="<< sizeof(E) << endl;
    cout << "sizeof(F) ="<< sizeof(F) << endl ;
    return 0;
}

//sizeof(A) =1
//sizeof(B) =1
//sizeof(C) =1
//sizeof(D) =8
//sizeof(E) =8
//sizeof(F) =4
```

代码第35行，由于A是空类，编译器会安插-一个char给空类，用来标记它的每一个对象。因此其大小为1个字节。
		代码第36行，类B大小和A相同，都是1个字节。
		代码第37行，类C是多重继承自A和B,其大小仍然为1个字节。
		**代码第38行，类D是虚继承自A,编译器为该类安插一个指向父类的指针，指针大小为8。由于此类有了指针，编译器不会安插一个char了。因此其大小是8个字节。**
		**代码第39行，类E虚继承自A并且也虚继承自B,因此它有指向父类A的指针与父类B的指针，大小为8个字节。**
		代码第40行，类F含有一个静态成员变量，这个静态成员的空间不在类的实例中，而是像全局变量一样在静态存储区中，被每一个类的实例共享，因此其大小是4个字节。

## 17.	sizeof与strlen 有哪些区别

1. sizeof是操作符，strlen 是函数。
2. sizeof操作符的结果类型是size_t, 它在头文件中typedef为unsigned int类型，该类型保证能容纳实现所建立的最大对象的字节大小。
3. sizeof可以用类型做参数，strlen只能用char*做参数，且必须是以"\0”结尾的。
4. 数组做sizeof的参数不退化，传递给strlen就退化为指针了。
5. 大部分编译程序在编译的时候sizeof 就被计算过了，这就是sizeof(x)可以用来定义数组维数的原因。strlen的结果要在运行的时候才能计算出来，它用来计算字符串的长度，不是类型占内存的大小。
6. sizeof后如果是类型，必须加括弧;如果是变量名，可以不加括弧。这是因为sizeof是个操作符，而不是个函数。

```
#include <stdio.h>
#include <cstring>
int main(){
    char str[20] = "0123456789";
    int a = strlen(str);
    int b = sizeof(str);
    printf("a:%d\n", a);
    printf("b:%d\n", b);
    //a为数组长度，不包括'\0'
    //b为分配的内存大小
    char *ss = "0123456789";
    int aa = sizeof(ss);
    int bb = strlen(ss);
    printf("aa:%d\n", aa);
    printf("bb:%d\n", bb);
    //aa为ss指针占用的内存空间，为8
    //bb为ss字符串长度
    return 0;
}
//a:10
//b:20
//aa:8
//bb:10
```



## 18.	sizeof有哪些用途

1. 与存储分配和I/O系统那样的例程进行通信

```
void* malloc(size_ t size) ;
size_ t fread (void* ptr,size_t size,size_t nmemb, FILE* stream);
```

2.	查看某个类型的对象在内存中所占的单元字节

```
void* memset(void* s, int c, sizeof(s)) ;
```

3. 在动态分配一对象时， 可以让系统知道要分配多少内存。

4. 便于一些类型的扩充，在Windows中很多结构类型就有-一个专用的字段是用来放该类型的字节大小的。

5. 由于操作数的字节数在实现时可能出现变化，建议在涉及操作数字节大小时用sizeof来代替常量计算。

6.	如果操作数是函数中的数组形参或函数类型的形参，则sizeof给出其指针的大小。
	
	

## 19.使用strlen()函数代替sizeof计算字符串长度

```
#include <iostream>
#include <stdio.h>
#include <string.h>

using namespace std;

void UpperCase(char str[]) {
    int test = sizeof(str);
    int test2 = sizeof(str[0]);

    //for (size_t i = 0; i < sizeof(str) / sizeof(str[0]); ++i) {
    //    if ('a' <= str[i] & str[i] <= 'z')
    //        str[i] -= ('a' - 'A');
    //}
    for (size_t i = 0; i < strlen(str); ++i) {
        if ('a' <= str[i] & str[i] <= 'z')
            str[i] -= ('a' - 'A');
    }
}

int main() {
    char str[] = "aBcDefghijkl";
    cout << "The length of str is " << sizeof(str) / sizeof(str[0]) << endl;
    UpperCase(str);
    cout << str << endl;
    return 0;
}

//The length of str is 13
//ABCDEFGHijkl
//修改后：
//The length of str is 12
//ABCDEFGHIJKL
```

sizeof(str)得到的并不是数组占用内存的总大小，而是一个字符指针的大小,为8字节,因此这里只能循环8次。
		sizeof(str)/sizeof(str[0])计算的是数组元素的个数，比字符串的长度大1,原因是数组的长度还包括字符串的结束符"\0"。
		应该用strlen()函数来代替sizeof计算字符串长度。

## 20.	使用sizeof计算联合体的大小

```
#include <iostream>
#include <stdio.h>

using namespace std;

union u {
    double a;
    int b;
};
union u2 {
    char a[13];
    int b;
};
union u3 {
    char a[13];
    char b;
};

int main() {
    cout << sizeof(u) << endl;
    cout << sizeof(u2) << endl;
    cout << sizeof(u3) << endl;
    return 0;
}
//并且对于复合数据类型，如union、struct、 class的对齐方式为成员中最大的成员对齐方式。
//8
//16
//13
```

这里又出现了CPU对齐的问题。所以编译器会尽量把数据放在它的对齐上以提高内存的命中率。对齐是可以更改的，使用#pragma pack(x)可以改变编译器的对齐方式。C++固有类型的对齐取编译器对齐方式与自身大小中较小的一个。例如，指定编译器按2对齐，int类型的大小是4,则int的对齐为2和4中较小的2。在默认的对齐方式下，因为几乎所有的数据类型都不大于默认的对齐方式8 (除了long double),所以所有的固有类型的对齐方式可以认为就是类型自身的大小。

```
#include <iostream>
#pragma pack(2)

using namespace std;
union u {
    char buf[9];
    int a;
};

int main() {
    cout << sizeof(u) << endl;
    return 0;
}
//#pragma pack()可以更改编译器的对齐大小
//10
```



## 21.	#pragma pack的作用

```c++
#include <iostream>
using namespace std;
#pragma pack(1)
struct test {
    char c;
    short s1;
    short s2;
    int i;
};

int main(){
    cout<< sizeof(test) <<endl;
    return 0;
}
//9
```



## 22.	为什么引入内联函数

引入内联函数的主要目的是，用它替代C语言中表达式形式的宏定义来解决程序中函数调用的效率问题。

这种宏定义在形式及使用上像一个函数，但它使用预处理器实现，没有了参数压栈、代码生成等一系列的操作，因此效率很高。这种宏定义在形式上类似于一个函数，但在使用它时，仅仅只是做预处理器符号表中的简单替换，因此它**不能进行参数有效性的检测**，也就不能享受C++编译器严格类型检查的好处。另外，**它的返回值也不能被强制转换为可转换的合适类型**，这样，它的使用就存在着一系列的隐患和局限性。另外，在C++中引入了类及类的访问控制，这样，如果一个操作或者说一个表达式涉及类的保护成员或私有成员，你就不可能使用这种宏定义来实现(因为无法将this指针放在合适的位置)。
		inline推出的目的，也正是为了取代这种表达式形式的宏定义。它消除了它的缺点，同时又很好地继承了它的优点。6

## 23.	为什么inline能很好地取代表达式形式的预定义

1. inline 定义的类的内联函数，函数的代码被放入符号表中，在使用时直接进行替换(像宏一样展开)，没有了调用的开销，效率也很高。
2. 类的内联函数也是一个真正的函数。编译器在调用一个内联函数时，首先会检查它的参数的类型，保证调用正确;然后进行一系列的相关检查，就像对待任何一个真正的函数一样。这样就消除了它的隐患和局限性。
3. inline可以作为某个类的成员函数，当然就可以在其中使用所在类的保护成员及私有成员。

## 24.	说明内联函数使用的场合

内联函数在C++类中应用最广的，应该是用来定义存取函数。我们定义的类中一般会把数据成员定义成私有的或者保护的，这样，外界就不能直接读写我们类成员的数据了。对于私有或者保护成员的读写就必须使用成员接口函数来进行。如果我们把这些读写成员函数定义成内联函数的话，将会获得比较好的效率。

```C++
class A {
private:
    int nTest;
    
public:
    int readTest() {
        return nTest;
    }

    void setTest(int i);
};

inline void A::setTest(int i){
    nTest = i;
}
```

类A的成员函数readTest()和setTest()都是inline 函数。

**readTest()函 数的定义体被放在类声明之中，因而readTest()自动转换成inline函数; setTest()函 数的定义体在类声明之外，因此要加上inline关键字**。

## 25.	为什么不把所有的函数都定义成内联函数

内联是以代码膨胀(复制)为代价的，仅仅省去了函数调用的开销，从而提高函数的执行效率。如果执行函数体内代码的时间相比于函数调用的开销较大，那么效率的收获会很少。另一方面，每一处内联函数的调用都要复制代码，将使程序的总代码量增大，消耗更多的内存空间。以下情况不宜使用内联。

1. 如果函数体内 的代码比较长，使用内联将导致内存消耗代价较高。
2. 如果函数体内出现循环，那么执行函数体内代码的时间要比函数调用的开销大。
3. 另外，类的构造函数和析构函数容易让人误解成使用内联更有效。要当心构造函数和析构函数可能会隐藏一些行为，如“偷偷地”执行了基类或成员对象的构造函数和析构函数。

所以不要随便地将构造函数和析构函数的定义体放在类声明中。一个好的编译器将会根据函数的定义体，自动地取消不值得的内联(这说明了inline不应该出现在函数的声明中)。

## 26.	内联函数与宏有什么区别

1. 内联函数在编译时展开，宏在预编译时展开。
2. 在编译的时候，内联函数可以直接被镶嵌到目标代码中，而宏只是一个简单的文本替换。
3. 内联函数可以完成诸如类型检测、语句是否正确等编译功能，宏就不具有这样的功能。
4. 宏不是函数，inline函数是函数。
5. 宏在定义时要小心处理宏参数(一般情况是把参数用括号括起来)，否则容易出现二义性。而内联函数定义时不会出现二义性。



# 3.	引用和指针

## 1.	一般变量引用

```c++
#include <iostream>
#include <string>

using namespace std;

int main(int argc, char *argv[]) {
    int a = 10;
    int b = 20;
    int &rn = a;
    int equal;
    rn = b;
    cout << "a=" << a << endl;
    cout << "b=" << b << endl;
    rn = 100;
    cout << "a=" << a << endl;
    cout << "b=" << b << endl;
    equal = (&a == &rn) ? 1 : 0;
    cout << "equal =" << equal << endl;
    return 0;
}

//代码第9行：声明rn为变量a的一个引用。
//a=20
//b=20
//a=100
//b=20
//equal =1
```

## 2.	指针变量引用

```c++
#include <iostream>

using namespace std;

int main(int argc, char *argv[]) {
    int a = 1;
    int b = 10;
    int *p = &a;
    int *&pa = p;
    (*pa)++;
    cout << "a =" << a << endl;
    cout << "b =" << b << endl;
    cout << "*p=" << *p << endl;
    pa = &b;
    (*pa)++;
    cout << "a = " << a << endl;
    cout << "b = " << b << endl;
    cout << "*p =" << *p << endl;
    return 0;
}
//a =2
//b =10
//*p=2
//a = 2
//b = 11
//*p =11

//代码第9行，声明p的一个指针引用pa。
```

指针引用更改的指向对象，则对应的指针也会更改指向对象。

## 3.	看代码找错误----变量引用

```
#include <iostream>

using namespace std;

int main(int argc, char *argv[]) {
    int a = 1, b = 2;
    //int &c;
    //int &d = a;
    //&d = b;
    int *p;
    *p = 5;
    return 0;
}

//7:error: 'c' declared as reference but not initialized

//9:error: lvalue required as left operand of assignment

//上面二者都因为引用类型的变量必须在声明时初始化，以后都不能再把该引用名作为其他变量名的别名。

//Segmentation fault  野指针   指针声明时不可先声明后赋值  而是后声明值得地址
```

引用类型的变量必须在声明时初始化，以后都不能再把该引用名作为其他变量名的别名。

## 4.	如何交换两个字符串

```
#include <iostream> 
#include <string.h>

using namespace std;

void swap(char *&x, char *&y) {		//此处*x，*y为指针引用
    char *temp;
    temp = x;
    x = y;
    y = temp;
}

void swap1(char **x, char **y) {		//x为指针ap的地址，*x为内容”hello“的地址
    char *temp;
    temp = *x;
    *x = *y;
    *y = temp;
}

int main() {
    char *ap = "hello";
    char *bp = "how are you?";
    cout << "ap:" << ap << endl;
    cout << "bp:" << bp << endl;
    //swap(ap, bp);
    //*ap，*x是同一个地址，因此内容相同
    swap1(&ap,&bp);
    //&ap为指针*ap的地址，ap为“hello”的地址，因此为二维指针。
    cout << "swap ap,bp" << endl;
    cout << "ap:" << ap << endl;
    cout << "bp:" << bp << endl;
    return 0;
}

//ap:hello
//bp:how are you?
//swap ap,bp
//ap:how are you?
//bp:hello
//swap采用指针引用传递指针地址，swap1采用二维数组来传递指针地址
```

## 5.	程序查错----参数引用

```
#include <iostream>

using namespace std;

const float pi = 3.14f;
float f;

float f1(float r) {
    f = r * r * pi;
    return f;
}
//f1()函数返回的是全局变量f的值

float &f2(float r) {
    f = r * r * pi;
    return f;
}
//f2()函数返回的是全局变量f的引用。

int main() {
    float f1(float= 5);
    float &f2(float= 5);
    float a = f1();
    //float &b = f1();

    float c = f2();
    float &d = f2();
    d += 1.0f;
    cout << "a=" << a << endl;
    //cout << "b=" << b << endl;
    cout << "c=" << c << endl;
    cout << "d=" << d << endl;
    cout << "f =" << f << endl;



    return 0;
}
//a=78.5
//c=78.5
//d=79.5
//f =79.5
//21行：声明函数f1（）的默认参数调用，其默认参数值为5。

//24:error: cannot bind non-const lvalue reference of type 'float&' to an rvalue of type 'float'
//不可直接给引用赋值  。将变量b赋为f10)的返回值。因为在f1()函数里，全局变量f的值78.5赋给一个临时变量temp,这个temp变量由编译器隐式地建立，然后建立这个temp的引用b。这里对一个临时变量temp进行引用会发生错误。

```

**C++规定*当函数返回的是非引用类型时*，函数会创建临时对象（temporary object），函数返回的就是这个临时对象。在求解表达式时，如果需要一个地方存储其运算结果，编译器会创建一个没有命名的对象，这就是临时对象。**
	***当函数返回引用类型时*，没有复制返回值，返回的是对象本身。**

**对一个临时变量temp进行引用会发生错误.**

## 6.	参数引用的常见错误

```
#include <iostream>

using namespace std;

class Test {

public:

    void f(const int &arg);

private:
    int value;
};

void Test::f(const int &arg) {
    //arg = 10;
    cout << "arg =" << arg << endl;
    value = 20;
}

int main() {
    int a = 7;
    const int b = 10;
    //int &c = b;
    const int &d = a;
    a++;
    //d++;
    Test test;
    test.f(a);
    cout << "a =" << a << endl;
    return 0;

}
//arg =8
//a =8
//16：error: assignment of read-only reference 'arg'
//    常量引用（const int &arg）的值不可被修改
//24：error: binding reference of type 'int&' to 'const int' discards qualifiers
//		常量的引用必须是的常量的。
//		非常量的应用可以是常量的，也可以不是常量的。
//27：error: increment of read-only reference 'd'
//    常量引用不可被修改与赋值
```

对于常量类型的变量，其引用也必须是常量类型的;对于非常量类型的变量，其引用可以是非常量的，也可以是常量的。但是要注意，无论什么情况，都不能**使用常量引用修改其引用的变量的值**,如上例27行。

## 7.	指针和引用有什么区别

1. **初始化要求不同**。引用在创建的同时必须初始化，即引用到一个有效的对象;而指针在定义的时候不必初始化，可以在定义后面的任何地方重新赋值。
2. **可修改性不同**。引用一旦被初始化为指向一个对象，它就不能被改变为另一个对象的引用;而指针在任何时候都可以改变为指向另一个对象。给引用赋值并不是改变它和原始对象的绑定关系。
3. 不存在NULL引用，**引用不能使用指向空值的引用**，它必须总是指向某个对象;而指针则可以是NULL,不需要总是指向某些对象，可以把指针指向任意的对象，所以指针更加灵活，也容易出错。
4. 测试需要的区别。由于引用不会指向空值，这意味着使用引用之前不需要测试它的合法性;而指针则需要经常进行测试。因此使用引用的代码效率比使用指针的要高。
5. 应用的区别。如果是指**一旦指向一个对象后就不会改变指向**，那么应该使用引用。如果有存在指向NULL (不指向任何对象)或在不同的时刻指向不同的对象这些可能性，应该使用指针。

实际上，在语言层面，引用的用法和对象一样;在二进制层面，**引用一般都是通过指针来实现的**，只不过编译器帮我们完成了转换。总体来说，引用既具有指针的效率，又具有变量使用的方便性和直观性。

## 8.	为什么传引用比传指针安全

由于不存在空引用，并且引用一旦被初始化为指向一个对象，它就不能被改变为另一个对象的引用，因此引用很安全。

对于指针来说，它可以随时指向别的对象，并且可以不被初始化，或为NULL,所以不安全。const指针仍然存在空指针(常量指针const int *p = NULL)，并且有可能产生野指针。

## 9.	复杂指针的声明

```cpp
a.一个整型数(An integer)		
	int a;
b.一个指向整型数的指针(A pointer to an integer)		
	int * a;
c.一个指向指针的指针，它指向的指针是指向一个整型数的(A pointer to a pointer to an integer )		
	int ** a;
d.一个有10个整型数的数组(An array of 10 integers)		
	int a[10];
e.一个有10个指针的数组，该指针是指向一个整型数的(An array of 10 pointers to integers )		
	int * a[10];
f. 一个指向有10个整型数数组的指针(A pointer to an array of 10 integers)		
	int (*a)[10];
g.一个指向函数的指针，该函数有一个 整型参数并返回一个整型数(A pointer to a function that takes an integer as an argument and returns an integer)		
	int (*a)(int);
h.一个有10个指针的数组，该指针指向一个函数，该函数有一个整型参数并返回一个整型数(An array of ten pointers to functions that take an integer argument and return an integer )		
	int (*a[10])(int)
```

**扩展知识:解读复杂指针声明**

使用右左法则:**首先从未定义的标识符开始阅读，然后往右看，再往左看**。每当遇到圆括号时，就应该掉转阅读方向。一旦解析完圆括号里面所有的东西，就跳出圆括号。重复这个过程，直到整个声明解析完毕。

1. int (\*func)(int *p);*

首先找到那个未定义的标识符，就是func,它的外面有一对圆括号，而且左边是一个\*号，这说明func是一个指针;然后跳出这个圆括号，先看右边，也是一个圆括号，这说明(\*func)是一个函数，而func是一个指向这类函数的指针，就是一个函数指针，这类函数具有int*类型的形参，返回值类型是int。

2. int (\*func)(int \*p，int (\*f)(int\*));

func被一对括号包含， 且左边有一个*号，说明func是一个指针，跳出括号，右边也有个括号，那么func是一一个指向函数的指针，这类函数具有int \*和int (\*)(int\* )这样的形参，返回值为int 类型。再来看一看func的形参int (\*f)(int\*)，类似前面的解释，f也是一个函数指针，指向的函数具有int\*类型的形参，返回值为int。

3. int (\*func[5])(int \*p);

func右边是一个[运算符，说明func是一个具有5个元素的数组；func 的左边有一个\*,说明func的元素是指针。要注意这里的\*不是修饰func的，而是修饰func[5]的，原因是[]运算符优先级比\*高，func 先跟[]结合，因此\*修饰的是func[5]。 跳出这个括号，看右边，也是一对圆括号，说明func数组的元素是函数类型的指针，它所指向的函数具有int* 类型的形参，返回值类型为int。

4. int (\*(\*func)[5])(int \*p);

func被一个圆括号包含，左边又有一个\*，那么func是一个指针;跳出括号，右边是一个[]运算符号，说明func是一个指向数组的指针。现在往左看，左边有一个\*号，说明这个数组的元素是指针;再跳出括号，右边又有一个括号，说明这个数组的元素是指向函数的指针。总结一下，就是: func 是一个指向数组的指针，这个数组的元素是函数指针，这些指针指向具有int\*类型的形参，返回值为int类型的函数。

5. int (\*(\*func)(int \*p))[5];

func是一个函数指针，这类函数具有int\*类型的形参，返回值是指向数组的指针，所指向的数组的元素是具有5个int元素的数组。

## 10.	看代码写结果----用指针赋值

```c++
#include <stdio.h>

int main(void) {

    char a[] = "hello,world";
    char *ptr = a;
    printf("%c\n", *(ptr + 4));
    printf("%c\n", ptr[4]);
    printf("%c\n", a[4]);
    printf("%c\n", *(a + 4));

    *(ptr + 4) += 1;
    printf("%s\n", a);
    printf("%s\n", ptr);
    return 0;
}
//o
//o
//o
//o
//hellp,world
//hellp,world
```

## 11.	指针加减操作

```
#include <stdio.h>

int main(void) {
    int a[5] = {1, 2, 3, 4, 5};
    //int *p =a ;
    int *ptr = (int *) (&a + 1);
    printf("%d\n", *(a + 1));
    printf("%d\n", *(ptr - 1));
    return 0;
}
```

对指针进行加1操作，得到的是下一个元素的地址，而不是原有地址值直接加1。所以，一个类型为t的指针的移动，以sizeof(t)为移动单位。

**a 是数组首地址，也就是 a[0] 的地址；&a 是 对象（数组）首地址；**

**a+1 是数组下一元素的地址，即 a[1]；而 &a+1 是下一个对象的地址， 即 a[5].**

在第6行中，（&a+1）取数组的首地址，+1表示加上a的长度（**此时a为数组变量，长度为5*sizeof(int)**),所以指针ptr移动到了a[5]的位置，已超出界限。

在第8行，将指针ptr移回了一个int的长度，此时位置是a[4]，及值为5。

## 12.	√指针比较

```
#include <iostream>

using namespace std;

int main(void) {
    char str1[] = "abc";
    char str2[] = "abc";
    const char str3[] = "abc";
    const char str4[] = "abc";
    const char *str5 = "abc";
    const char *str6 = "abc";
    char *str7 = "abc";
    char *str8 = "abc";
    cout << (str1 == str2) << endl;
    cout << (str3 == str4) << endl;
    cout << (str5 == str6) << endl;
    cout << (str6 == str7) << endl;
    cout << (str7 == str8) << endl;
    return 0;

}
//0
//0
//1
//1
//1
//str1,2,3,4都在栈中，str5,6,7,8都在栈中的数据区，且共用同一内存区。
//多个数组在栈中存放：可能是不同的内存空间
//多个字符指针咋栈中的存放方式：相同的数据存放在栈中的数据区，共用一个内存地址。
```

## 13.	√看代码找错误----内存访问违规

```
#include <iostream>
#include <cstring>

using namespace std;

int main() {
    char a;
    char *str1 = &a;
    char *str2 = "AAA";
    strcpy(str1, "hello");  //内存越界访问
    cout << str1 << endl;
    str2[0] = 'B';          //str2为常量，对str2[0]的赋值是不合法的。
    cout << str2 << endl;
    return 0;
}
```

第10行：内存访问越界，a的空间只有字节，而''hello''有6字节，因此会越界存储。

第12行：现在还不清楚。

## 14.	指针的隐式转换

```
#include <stdio.h>

int main() {
    int ival = 1024;
    int ival2 = 2048;
    int *pi1 = &ival;
    int *pi2 = &ival2;
    int **pi3 = 0;

    ival = *pi3;
    *pi2 = *pi3;
    ival = pi2;
    pi2 = *pi1;
    pi1 = *pi3;
    ival = *pi1;
    pi1 = ival;
    pi3 = &pi2;
    return 0;
}
// 17,18,19,20，23行 编译错误 ：int* 和 int是无法隐式转换的，需要强制转换
//todo：为理解空指针的分配操作
//21行 运行错误 ：无法读取空指针赋值区的内容。在win中，内存中专门有给空指针复制的空间，该空间不可呗访问。
```

编译错误：类型之间不能隐式转换，如int转换成int\*、 int\*转换成int等。

运行时错误：是因为在Windows平台，进程的内存空间有一块是专门用于NULL指针分配的分区，这个分区的地址空间是禁止进入的，因此就会发生内存访问违规现象，同时该进程将终止运行。

## 15.	指针常量与常量指针的区别

解惑：[找错----const 的使用](#找错----const 的使用)

- 常量指针，表述为“是常量的指针”，它首先应该是一个指针。
- 指针常量，表述为“是指针的常量”，它首先应该是一个常量。

常量指针，它是一个指向常量的指针。设置常量指针指向一个常量，为的就是防止写程序过程中对指针误操作出现了修改常量这样的错误，编译系统就会提示我们出错信息。因此，常量指针就是指向常量的指针，当确定指向地址后，该指针所指向的地址的内容是不可修改的。

指针常量，它首先是一个常量，然后才是一个指针。指针常量就是不能修改这个指针所指向的地址，一开始初始化指向哪儿，它就只能指向哪儿了，不能指向其他的地方了，就像一个数组的数组名一样，是一个固定的指针，不能对它移动操作。如果使用p++，系统就会提示出错。但是注意，这个指向的地方里的内容是可以替换的，这和上面说的常量指针是完全不同的概念。总之，指针常量就是指针的常量，它是不可改变地址的指针，但是可以对它所指向的内容进行修改。

## 16.	指针的区别

```
char * const p1;		//指针常量: 指针指向的地址不可修改，指向的地址内容可以更改
char const * p2;		//常量指针: 指针指向的地址可以修改，指向地址的内容不可更改。
const char *p3;			//常量指针：同上
const char *const p4;	//常量指针常量：都不可以修改
```

## 17.	找错----常量指针和指针常量的作用

```
#include <stdio.h>

int main() {
    const char *node1 = "abc";
    char *const node2 = "abc";

    node1[2] = 'k';     //Read-only vairiable is not assignable 只读变量，不可分配
    *node1[2] = 'K';    //指针数组 在此处不应该使用
    *node1 = "xyz";     //Read-only variable is not assignable  指向的地址可以变，地址对应的值不可以更改
    node1 = "xyz";      //√ 可以更改指针指向的地址，从而改变内容

    node2[2] = 'k';     //指针常量 可以更改指针指向的地址内容，但是不可对只读变量进行改写。
    *node2[2] = 'K';    //指针数组 在此处不应该使用
    *node2 = "xyz";     // 因为声明时直接赋值为常量的地址，而在例2-7中赋值为变量的地址。
    node2 = "xyz";      //Read-only vairiable is not assignable 只读变量，不可分配
    return 0;
}
```

此例与[例2-7](#找错----const 的使用)的不同之处在于2-7在声明是赋予的是变量的地址，因此可以做出相应的更改，而现在直接赋予常量字符串，因此操作在原有的基础上更改的范围进一步缩小。

例2-7如下：

```
#include <stdio.h>
#include <iostream>

using namespace std;

int main() {
    int a = 10;
    int b = 20;
    int c = 30;
    
    //指针常量：本质是常量，常量的内容是一个指针，一个指针最基本的就是所指向的地址，而一个指针型的常量意味着指向的地址不可变。
    // 因此指针常量指向的地址不可变，但指向的地址内容可以更改
    int *const p1 = &b;		//等同于 int const * p2 = &b;

    *p1 = 100;      //√
    //p1 = &c;        //×
    cout<<"*p1:"<<*p1<<endl;

    //常量指针：本质是指针，指针的内容是一个常量的地址，指针指向的地址可以改变，但指定地址后，该地址的对应的值不可以更改。
    // 因此常量指针指向的地址可以改变，但确定地址后，改地址的内容不可更改。
    const int *p2 = &a;
    p2 = &c;        //√
    //*p2 = 190;      //×
    cout<<"*p2:"<<*p2<<endl;
    return 0;
}

//*p1:100
//*p2:30
```

此时，p1为指针常量，本质是常量，常量的内容是一个指针，该指针指向的地址不可改变，指向地址的内容可以更改。如第15，16行。

p2是常量指针，本质是指针，指针最基本的要素就是指向的地址，指针指向的地址是可以改变的，而常量指针指向的是一个常量的地址，因此常量指针可以改变指向的地址，地址确定后，改地址对应的值就不可更改，如22,23行。

## 18.	this指针的正确叙述

关于类中this指针：

- 类的非静态成员函数是属于类的对象，含有this指针。而类的static函数属于类本身，不含this指针。
- 友元函数是非成员函数，所以它无法通过this指针获得一份拷贝。

## 19.看代码写结果----this 指针

```
#include <iostream>

using namespace std;

class MyClass {
public:
    int data;

    MyClass(int data) {
        this->data = data;
    }

    void print() {
        //cout << data << endl;
        cout << "hello!" << endl;
    }
};

int main() {
    MyClass *pMyClass;
    pMyClass = new MyClass(1);
    pMyClass->print();
    pMyClass[0].print();
    pMyClass[1].print();
    pMyClass[10000000].print();
    return 0;
}
//14行未注释是
//1
//hello!
//1
//hello!
//7602368
//hello!
//
//Process finished with exit code -1073741819 (0xC0000005)


//14行注释后
//hello!
//hello!
//hello!
//hello!
```

对于类成员函数而言，并不是一个对象对应一个单独的成员函数体，而是此类的所有对象共用这个成员函数体。当程序被编译之后，此成员函数地址即已确定。我们常说，调用类成员函数时，会将当前对象的this指针传给成员函数。没错，一个类的成员函数体只有一份，而成员函数之所以能把属于此类的各个对象的数据区别开，就在于每次执行类成员函数时，都会把当前对象的this 指针(对象首地址)传入成员函数，函数体内所有对类数据成员的访问，都会被转化为this->数据成员的方式。

如果print函数里没有访问对象的任何数据成员，那么此时传进来的对象this指针实际上是没有任何用处的。这样的函数，其特征与全局函数并没有太大区别。但如果取消第14行的注释，由于print函数要访问类的数据成员data，而类的数据成员是伴随着对象声明而产生的。但是，我们只new了一个MyClass，显然，下标"1"和 下标"10000000"的MyClass对象根本不存在，那么对它们的数据成员访问也显然是非法的。

## 20.	指针数组与数组指针的区别

**指针数组指一个数组里存放的都是同一个类型的指针**，如

```
int * a[10];
```

数组a里面存放了10个int \*型变量，由于它是一个数组，已经在栈区分配了10 个int\*的空间，也就是32位机上是40个byte,每个空间都可以存放一个int型变量的地址。这个时候，你可以为这个数组的每一个元素初始化。

**数组指针是一个指向一维或者多维数组的指针**，如

```
int * b = new int[10];
```

指针b指向含有10个整型数据的一维数组。注意，这个时候释放空间一定要delete [],否则会造成内存泄露。

```
#include <iostream>

using namespace std;

int main() {
    int x1[4] = {1, 2, 3, 4};
    int x2[2] = {5, 6};
    int x3[3] = {7, 8, 9};

    //a为指针数组
    int *a[2];
    //b为数组指针
    int *b = x1;
    int i = 0;
    a[0] = x2;
    a[1] = x3;
    cout << "输出a[0]: ";
    for (i = 0; i < sizeof(x2) / sizeof(int); i++) {
        cout << a[0][i] << " ";
    }
    cout << endl;
    cout << "输出a[1]: ";
    for (i = 0; i < sizeof(x3) / sizeof(int); i++) {
        cout << a[1][i] << " ";
    }
    cout << endl;
    cout << "输出b: ";
    for (i = 0; i < sizeof(x1) / sizeof(int); i++) {
        cout << b[i] << " ";
    }
    cout << endl;
    return 0;
}
//输出a[0]: 5 6
//输出a[1]: 7 8 9
//输出b: 1 2 3 4 
```

## 21.	找错----指针数组和数组指针的使用

```
void prt(char *str[]) {
    if (*str[0] == '\0')
        printf("str[0]:%s\n", "空");
    else
        printf("str[0]:%s\n", str[0]);
    printf("str[1]:%s\n", str[1]);
    printf("str[2]:%s\n", str[2]);
    printf("str[3]:%s\n", str[3]);
}

int main() {
    char *str[] = {"Welcome", "to", "Fortemedia", "Nanjing"};

    printf("%s\n", "--------------");
    char **p = str + 1;
    prt(str);
    printf("%s\n", "--------------");

    str[0] = (*p++) + 2;
    prt(str);
    printf("%s\n", "--------------");

    str[1] = *(p + 1);
    prt(str);
    printf("%s\n", "--------------");

    str[2] = p[1] + 3;
    prt(str);
    printf("%s\n", "--------------");

    str[3] = p[0] + (str[2] - str[1]);
    prt(str);


    return 0;
}
//--------------
//str[0]:Welcome
//str[1]:to
//str[2]:Fortemedia
//str[3]:Nanjing
//--------------
//str[0]:空
//str[1]:to
//str[2]:Fortemedia
//str[3]:Nanjing
//--------------
//str[0]:空
//str[1]:Nanjing
//str[2]:Fortemedia
//str[3]:Nanjing
//--------------
//str[0]:空
//str[1]:Nanjing
//str[2]:jing
//str[3]:Nanjing
//--------------
//str[0]:空
//str[1]:Nanjing
//str[2]:jing
//str[3]:g
```

代码第15行结束时，p指向'to'。

代码第19行结束时，p指向'Fortemedia'。此时str[0]指向第4个字符串"Nanjing"后面的元素，因此其内容为空。

代码第23行结束时，p没有移动，str[1]指向 p的后一个元素地址，即'Nanjing'。

代码第27行，此时p[1]指向'Nanjing'。p[1]+ 3即指向字符串的元素的第4个元素，即\'j\'字符。此行执行之后，str[2]等于\'j\'的地址。

代码第31行，由前文可知str[2] - str[1]等于3，而p[0]指向\'j\'的地址。因此str[4]指向"Nanjing"字符串中的最后一个字符\'g\'的地址。

## 22.	函数指针与指针函数的区别

**指针函数**是指带指针的函数，即本质是一个函数，并且返回类型是某一类型的指针。

事实上，每一个函数，即使它不带有返回某种类型的指针，它本身都有一个入口地址，该地址相当于一个指针。比如函数返回一个整型值，实际上也相当于返回一个指针变量的值，不过这时的变量是函数本身而已，而整个函数相当于一个"变量”。

**函数指针**是指向函数的指针变量，因而它本身首先应是指针变量，只不过该指针变量指向函数。有了指向函数的指针变量后，可用该指针变量调用函数，就如同用指针变量可引用其他类型的变量一样。

```Cpp
#include <iostream>

using namespace std;

int max(int x, int y) {
    return (x > y ? x : y);
};

//指针函数
float *find(float *s, int x) {
    return s + x;
};

int main() {
    float score[] = {10, 20, 30, 40};
    //函数指针
    int (*p)(int, int);
    float *q = find(score + 1, 1);
    int a;
    p = max;
    a = (*p)(1, 2);
    cout << "a = " << a << endl;
    cout << "*q=" << *q << endl;
    return 0;
}
//a = 2
//*q=30
```

## 23.	数组指针与函数指针的定义

定义下面的几种类型变量:

```Cpp
a.含有10个元素的指针数组		
	int * a[10];
b.数组指针
	int (*a)[10];或 int *a = new int[10];
c.函数指针
	void (*fun)(int,int);
d.指向函数的指针数组
	int (*fun[10])(int,int);
```

## 24.	各种指针的定义

```Cpp
a.函数指针
	int (*p)(int ,int);
b.函数返回指针
	int * p();
c.const指针
	const int * p;		//常量指针
d.指向const的指针
	int * const p;		//指针常量
e.指向const的const指针。
	const int * const p;
```

## 25.	代码改错----函数指针的使用

```Cpp
#include <iostream>

using namespace std;

int max(int x, int y) {
    return x > y ? x : y;
}

int main() {
    int *p;
    int a, b, c;
    int result;
    int max(x,y);
    //int max(int, int);    //仅用于函数声明(函数声明在main之后时，需要声明max函数。函数声明在前时，无需声明)。
    p = max;
    cout << "Please input three integer" << endl;
    cin >> a >> b >> c;
    result = (*p)((*p)(a, b), c);
    cout << "result = " << result << endl;
    return 0;
}
```

14行声明错误(按条件，可取消)。

15行指针转换错误，p为int *形指针，而max地址为(int *)(int,int)型。

**改正如下**：

```cpp
#include <iostream>

using namespace std;

int max(int x, int y) {
    return x > y ? x : y;
}

int main() {
    int (*p)(int, int);
    int a, b, c;
    int result;
    //int max(int, int);    //仅用于函数声明(函数声明在main之后时，需要声明max函数。函数声明在前时，无需声明)。
    p = &max;
    cout << "Please input three integer" << endl;
    cin >> a >> b >> c;
    result = (*p)((*p)(a, b), c);
    cout << "result = " << result << endl;
    return 0;
}
//Please input three integer
//2 5 6
//result = 6
```

## 26.	看代码写结果----函数指针的使用

```Cpp
#include <stdio.h>

int add1(int a1, int b1);

int add2(int a2, int b2);

int main(int argc, char *argv[]) {
    int numa1 = 1, numb1 = 2;
    int numa2 = 2, numb2 = 3;
    int (*op[2])(int a, int b);     //有两个指针的数组，指针指向一个函数，该函数具有两个int型参数，并返回一个int型值。
    op[0] = add1;
    op[1] = add2;
    printf("%d %d\n", op[0](numa1, numb1), op[1](numa2, numb2));
    //getchar();
    return 0;
}

int add1(int a1, int b1) {
    return a1 + b1;
}

int add2(int a2, int b2) {
    return a2 + b2;
}
//3 5
```

在代码第10行，定义了一个函数指针数组op，它含有两个指针元素。在第11行和第12行把这两个元素分别指向了add1和add2两个函数地址。最后在第13行打印出使用函数指针调用add1和add2这两个函数返回的结果。

## 27.	typedef用于函数指针定义

```cpp
typedef int (*pfun)(int x,int y);	
```

这里的pfun是一个使用typedef自定义的数据类型。它表示一个函数指针，其参数有两个，都是int类型，返回值也是int类型。可以按如下步骤使用:

```cpp
typedef int (*pfun)(int x,int y);
int fun(int x，int y);
pfun p = fun;
int ret = p(2，3);	
//要注意实现fun函数
```

第1行定义了pfun类型，表示-一个函数指针类型。

第2行定义了一个函数。

第3行定义了一个pfun类型的函数指针p,并赋给它fun的地址。

第4行调用p(2, 3)，实现fun(2, 3)的调用功能。

定义了一个函数指针类型，表示指向返回值为int,且同时带2个int参数的函数指针类型。**可以用这种类型定义函数指针来调用相同类型的函数**。

## 28.	什么是野指针

**“野指针”不是NULL指针，而是指向“垃圾”内存的指针**。人们一般不会错用NULL指针，因为用if语句很容易判断。但是“野指针”是很危险的，if 语句对它不起作用。“野指针”的成因主要有两种:

- **指针变量没 有被初始化**。任何指针变量刚被创建时不会自动成为NULL指针，它的默认值是随机的，它会乱指一气。所以，指针变量在创建的同时应当被初始化，要么将指针设置为NULL，要么让它指向合法的内存。
- **指针p被free或者delete之后，没有置为NULL**,让人误以为p是个合法的指针。

## 29.	看代码查错----“野指针” 的危害

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

int main() {
    //声明一个short *型指针，并且没有初始化
    short *bufptr;
    //声明一个short型数组
    short bufarray[20];
    //声明一个变量,取值为十八进制
    short var = 0x20;
    printf("var:%d\n", var);
    //对未初始化的指针不可直接赋值，只能用地址进行赋值
    *bufptr = var;	(×)
    bufarray[0] = var;

    return 0;
}
```

**改正1**：对15行进行修改，(对为初始化的指针进行赋值)

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

int main() {
    //声明一个short *型指针，并且没有初始化
    short *bufptr;
    //声明一个short型数组
    short bufarray[20];
    //声明一个变量,取值为十八进制
    short var = 0x20;
    printf("var:%d\n", var);
    //对未初始化的指针不可直接赋值，只能用地址进行赋值
    bufptr = &var;
    printf("*bufptr:%d\n", *bufptr);
    bufarray[0] = var;

    return 0;
}
//var:32
//*bufptr:32
```

**改正2**：

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

int main() {
    short *bufptr = (short *)malloc(sizeof(short));
    //声明一个short型数组
    short bufarray[20];
    //声明一个变量,取值为十八进制
    short var = 0x20;
    printf("var:%d\n", var);
    //对未初始化的指针不可直接赋值，只能用地址进行赋值
    //对于未初始化的但已经分配空间的指针，可以直接进行赋值。
    *bufptr = var;
    printf("*bufptr:%d\n", *bufptr);
    bufarray[0] = var;

    return 0;
}
//var:32
//*bufptr:32
```

**对未初始化的指针不可直接赋值，只能用地址进行赋值。**

**对于未初始化的但已经分配空间的指针，可以直接进行赋值。**

## 30.	有了malloc/free， 为什么还要new/delete

malloc与free是C++/C的标准库函数, new/delete是C++的运算符。它们都可用于申请动态内存和释放内存。

**对于非内部数据类型的对象(如结构体等)而言，光用malloc/free 无法满足动态对象的要求。对象在创建的同时要自动执行构造函数，对象在消亡之前要自动执行析构函数。由于malloc/free是库函数而不是运算符，不在编译器控制权限之内，不能够把执行构造函数和析构函数的任务强加于malloc/ree.**

因此，C++需要-一个能完成动态内存分配和初始化工作的运算符new,以及一个能完成清理与释放内存工作的运算符delete。注意: new/delete 不是库函数。请看下面的例子。

```
#include <iostream>

using namespace std;

class Obj {
public:
    Obj(void) {
        cout << "Initialization" << endl;
    }

    ~Obj(void) {
        cout << "Destroy" << endl;
    }
};

void UseMallocFree(void) {
    cout << "In UseMallocFree()..." << endl;
    Obj *a = (Obj *) malloc(sizeof(Obj));
    free(a);
}

void UseNewDelete(void) {
    cout << "In UseNewDelete()..." << endl;
    Obj *a = new Obj;
    delete a;
}

int main() {
    UseMallocFree();
    UseNewDelete();
    return 0;
}

//In UseMallocFree()...
//In UseNewDelete()...
//Initialization
//Destroy
```

## 31.	程序改错----指针的初始化

```
#include <stdio.h>
#include <malloc.h>

struct Tag_Node {
    struct Tag_Node *left;
    struct Tag_Node *right;
    int value;
};
typedef struct Tag_Node TNode;
TNode *root = NULL;

void append(int N);

int main() {
    append(63);
    append(45);
    append(32);
    append(77);
    append(96);
    append(21);
    append(17);
    //print();
    return 0;
}

void append(int N) {
    TNode *NewNode = (TNode *) malloc(sizeof(TNode));
    NewNode->value = N;
    if (root == NULL) {
        root = NewNode;
        return;
    } else {
        TNode *temp;
        temp = root;
        while ((N >= temp->value && temp->left != NULL) || (N < temp->value && temp->right != NULL)) {
            while (N >= temp->value && temp->left != NULL)
                temp = temp->left;
            while (N < temp->value && temp->right != NULL)
                temp = temp->right;
        }
        if (N >= temp->value)
            temp->left = NewNode;
        else
            temp->right = NewNode;
        return;
    }
}
```

TNode是一个结构体类型，它有left 和right两个成员指针，分别代表链接左、右两个元素，还有value成员表示元素节点的数据。在append函数中，它想把数据从左到右按降序排列。因此在第35、36、 38行使用while循环来查找合适的位置。这里有一个问题，在这3行都采用temp的left或right与NULL进行判断，然而对堆中分配的内存只做了成员
value 的初始化(第28行)，没有把left和right初始化为NULL,因此指针left和指针right与NULL进行的判断没有作用。结果是程序中会对野指针指向的地址进行赋值，从而导致程序崩溃。

**改正**：

```cpp
#include <stdio.h>
#include <malloc.h>

struct Tag_Node {
    struct Tag_Node *left;
    struct Tag_Node *right;
    int value;
};
typedef struct Tag_Node TNode;
TNode *root = NULL;

void append(int N);


int main() {
    append(63);
    append(45);
    append(32);
    append(77);
    append(96);
    append(21);
    append(17);
    printf("head: %d\n", root->value);
    return 0;
}

void append(int N) {
    TNode *NewNode = (TNode *) malloc(sizeof(TNode));
    NewNode->value = N;
    NewNode->left = NULL;
    NewNode->right = NULL;
    if (root == NULL) {
        root = NewNode;
        return;
    } else {
        TNode *temp;
        //从根节点开始遍历
        temp = root;
        //1.判断相关位置(左大右小)是否为NULL
        while ((N >= temp->value && temp->left != NULL) || (N < temp->value && temp->right != NULL)) {
            //2.当不为NULL时(表示有子节点)，进入子接点(递归),重复外部(步骤1)操作。
            while (N >= temp->value && temp->left != NULL)
                temp = temp->left;
            while (N < temp->value && temp->right != NULL)
                temp = temp->right;
        }
        //当节点为NULL时，表示找到该节点，应在此位置插入临时节点temp.(左大右小原则)
        if (N >= temp->value) {
            temp->left = NewNode;
            //形成双向链表(或者双向二叉树）
            NewNode->right = temp;
        } else {
            temp->right = NewNode;
            //形成双向链表(或者双向二叉树）
            NewNode->left = temp;
        }
        return;
    }
}
```

如上面的程序所示，在第30、31行添加了成员指针left和right的初始化，这样就杜绝了野指针的产生。第51、55行的目的是为了使链表是双向链表。这样在遍历链表时就会比较方便。

## 32.	各种内存分配和释放的函数的联系和区别

C语言的标准内存分配、释放函数: malloc、calloc、realloc、free 等。

malloc与calloc 的区别为1块与n块的区别。

- malloc的调用形式为

    ```
    (类型* )malloc(size)
    ```

    在内存的动态存储区中分配一块长度为“size”字节的连续区域，返回该区域的首地址，此时内存中的值没有初始化，是个随机数。

- calloc的调用形式为

    ```
    (类型* )calloc(n, size)
    ```

    在内存的动态存储区中分配n块长度为“size”字节的连续区域，返回首地址，此时内存中的值都被初始化为0。

- realloc的调用形式为

    ```
    (类型* )realloc(*ptr, size)
    ```

    将ptr内存大小增大到size,新增加的内存块没有初始化。

- free的调用形式为

    ```
    free(void *ptr)
    ```

    释放ptr所指向的一块内存空间。

C++中，new/delete函数可以调用类的构造函数和析构函数。

## 33.	程序找错一动态内存的传递

```Cpp
#include <iostream>
#include <cstring>

using namespace std;

class Base {
private:
    char *name;
public:
    Base(char *className) {
        name = new char[strlen(className)];
        strcpy(name, className);
    }

    ~Base() {
        delete name;
    }

    char *copyName() {
        char newname[10] = "";
        strcpy(newname, name);
        return newname;
    }

    char *getName() {
        return name;
    }
};

class Subclass : public Base {
public:
    Subclass(char *className) : Base(className) {
    }
};

int main() {
    Base *pBase = new Subclass("test");
    printf("name: %s\n", pBase->getName());
    printf("new name: %s\n", pBase->copyName());
    return 0;
}
//name: test
//new name: (null)
```

这个程序有Base 和Subclass两个类，其中Subclass 是Base的子类。在本题里，Subclass只是被用来向Base的构造函数传递字符串参数，以达到为Base的私有成员赋值的目的。

代码第11行，在Base的构造函数中用new分配了堆内存。其内存大小为传入的字符串长度，这里有个bug。由于字符串是是以0作为结束符的，应该多分配一个字节存放0。

Base的成员函数copyName()中，返回其内数组的地址。由于数组处于栈中，当copyName调用结束后，栈就会被销毁。这里应返回堆内存地址。

**改正：**

```Cpp
#include <iostream>
#include <cstring>

using namespace std;

class Base {
private:
    char *name;
public:
    Base(char *className) {
        name = new char[strlen(className)+1];
        strcpy(name, className);
    }

    ~Base() {
        delete name;
    }

    char *copyName() {
        char *newname = new char(strlen(name)+1);
        strcpy(newname, name);
        return newname;
    }

    char *getName() {
        return name;
    }
};

class Subclass : public Base {
public:
    Subclass(char *className) : Base(className) {
    }
};

int main() {
    Base *pBase = new Subclass("test");
    printf("name: %s\n", pBase->getName());
    printf("new name: %s\n", pBase->copyName());
    return 0;
}	
//name: test
//new name: test
```

## 34.	动态内存的传递

```cpp
#include <iostream>
#include <cstring>

using namespace std;

void GetMemory(char *p, int num) {
    p = (char *) malloc(sizeof(char) * num);
};

int main(void) {
    char *str = NULL;
    GetMemory(str, 10);
    strcpy(str, "hello");
    return 0;
}
```

这里的GetMemory函数有问题。GetMemory函数体内的p实际上是main函数中的str变量在GetMemory函数栈中的一个备份，因为编译器总是为函数的每个参数制作临时的变量。因此，虽然在代码第7行中p申请了堆内存，但是返回到main函数时，str 还是NULL,并不指向那块堆内存。在代码第13行，调用strcpy时会导致程序崩溃。

实际上，GetMemory并不能做任何有用的事情。这里还要注意，由于从GetMemory函数返回时不能获得堆中内存的地址，那块堆内存就不能被继续引用，也就得不到释放，因此调用一次GetMemory函数就会产生num字节的**内存泄漏**。

可以采用3种方法来解决上面的动态内存不能传递的问题。

- 在C语言中，可以通过采用**指向指针的指针**解决这个问题，可以把str的地址传给函数GetMemory。

    ```cpp
    void GetMemory2(char **p, int num) {
        //对传递过来的二级指针中的源字符地址str2指针进行分配地址。
        *p = (char *) malloc(sizeof(char) * num);
    };
    ```

    

- 在C++中，多了一种选择，就是传递str**指针的引用**。

    ```cpp
    //char *&p = char *(&p) :指向char类型p的地址的指针变量。类似于二级指针。不同于GetMemory2中的参数1.取决于取地址是在调用该函数前或后(即在函数中进行取地址)。
    void GetMemory3(char *&p, int num) {
        p = (char *) malloc(sizeof(char) * num);
    };
    ```

- 使用**函数返回值**来传递动态内存。

    ```
    char *GetMemory4(int num) {
        char *p = (char *) malloc(sizeof(char) * num);
        return p;
    }
    ```

**改正：**

```cpp
#include <iostream>
#include <cstring>

using namespace std;

void GetMemory(char *p, int num) {
    p = (char *) malloc(sizeof(char) * num);
};

void GetMemory2(char **p, int num) {
    //对传递过来的二级指针中的源字符地址str2指针进行分配地址。
    *p = (char *) malloc(sizeof(char) * num);
};

//char *&p = char *(&p) :指向char类型p的地址的指针变量。类似于二级指针。不同于GetMemory2中的参数1.取决于取地址是在调用该函数前或后(即在函数中进行取地址)。
void GetMemory3(char *&p, int num) {
    p = (char *) malloc(sizeof(char) * num);
};

char *GetMemory4(int num) {
    char *p = (char *) malloc(sizeof(char) * num);
    return p;
}

int main(void) {
    char *str1 = NULL;
    char *str2 = NULL;
    char *str3 = NULL;
    char *str4 = NULL;
    GetMemory(str1, 20);
    
    //参数&str2为指针str2的地址，所以为二级指针。
    GetMemory2(&str2, 20);
    GetMemory3(str3, 20);
    str4 = GetMemory4(20);
    strcpy(str2, "GetMemory 2");
    strcpy(str3, "GetMemory 3");
    strcpy(str4, "GetMemory 4");
    cout << "str1 == NULL?" << (str1 == NULL ? "yes" : "no") << endl;
    cout << "str2:" << str2 << endl;
    cout << "str3:" << str3 << endl;
    cout << "str4:" << str4 << endl;
    free(str2);
    free(str3);
    free(str4);
    str2 = NULL;
    str3 = NULL;
    str4 = NULL;
    return 0;
}
//str1 == NULL?yes
//str2:GetMemory 2
//str3:GetMemory 3
//str4:GetMemory 4
```

在上面的代码中，

GetMemory不能传递动态内存，str始终都是NULL。

GetMemory2()函数采用二维指针作为参数传递; 

GetMemory3()函数采用指针的引用作为参数传递; 

GetMemory4()函数采用返回堆内存指针的方式。

可以看到这3个函数都能起到相同的作用。

另外注意第43~48行，这里在主函数推出之前把指针str2、str3和str4指向的堆内存释放并把指针赋为NULL。**每当决定不再使用堆内存时，应该把堆内存释放，并把指针赋为NULL，这样能避免内存泄漏以及产生野指针**，是良好的编程习惯。

## 35.	比较分析两个代码段的输出----动态内存的传递

**程序1:**

```cpp
#include <iostream>

char *GetMemory() {
    char p[] = "hello world";
    return p;
}

void Test(void) {
    char *str = NULL;
    str = GetMemory();
    printf(str);
}

int main(){
    Test();
    return 0;
}
```

**程序2：**

```cpp
#include <iostream>
#include <cstring>

void GetMemory(char *p) {
    p = (char *) malloc(100);
}

void Test(void) {
    char *str = NULL;
    GetMemory(str);
    strcpy(str, "hello world");
    printf(str);
}

int main() {
    Test();
    return 0;
}
```

程序1的GetMemory()返回的是指向栈内存的指针，该指针的地址不是NULL,但是当栈退出后，内容不定，有可能会输出乱码。改正参考[动态内存传递(第四种方式)](#动态内存的传递)

程序2的GetMemory()没有返回值，这个函数不能传递动态内存。在Test函数中，str变量的值通过参数传值的方式赋给GetMemory()的局部变量p。但是Test()中的 str 一直为NULL，所以第11 行中的调用会使程序崩溃。此外，由于堆内存在GetMemory()执行之后没有指针引用它，因此会产生内存泄露。等同于[动态内存传递(第一种方式)](#动态内存的传递)

## 36.	程序查错----“野指针”用于变量值的互换

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

void swap(int *p1, int *p2) {
    int *p;
    *p = *p1;
    *p1 = *p2;
    *p2 = *p;
}

int main(int argc, char *argv[]) {
    int a = 1;
    int b = 2;
    swap(&a, &b);
    return 0;
}
```

在代码第7行，声明了一个指针p,由于没有对p初始化，p是个野指针，它可能指向系统区。因此在代码第4行，对p指向的内存区赋值非常危险，会导致程序运行时崩溃。

**改正：**

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

void swap(int *p1, int *p2) {
    int p;
    p = *p1;
    *p1 = *p2;
    *p2 = p;
}

int main(int argc, char *argv[]) {
    int a = 1;
    int b = 2;
    swap(&a, &b);
    return 0;
}	
```

## 37.	内存的分配方式有几种

- **从静态存储区域分配**。内存在程序编译的时候就已经分配好，这块内存在程序的整个运行期间都存在，例如全局变量。
- **在栈上创建**。在执行函数时，**函数内局部变量**的存储单元都可以在栈上创建，函数执行结束时这些存储单元**自动被释放**。处理器的指令集中有关于栈内存的分配运算，因此效率很高，但是分配的内存容量有限。
- **从堆上分配，亦称动态内存分配**。程序在运行的时候用malloc或new申请任意多少的内存，程序员自己负责在何时用free 或delete 释放内存。动态内存的生存期由我们决定，使用非常灵活，但问题也最多。

## 38.	什么是句柄

句柄在Windows 编程中是-一个很重要的概念，在许多地方都扮演着重要的角色。在Windows环境中，句柄是用来标识项目的，这些项目包括:

- 模块(module)。
- 任务(task)。
- 实例(instance)。
- 文件(file) 。
- 内存块(block of memory)。
- 菜单(menu)。
- 控制(control)。
- 字体(font)。
- 资源(resource) ，包括图标(icon) 、光标(cursor) 、字符串(string) 等。
- GDI对象(GDI object)，包括位图(bitmap) ，画刷(brush) 、元文件(metafile) ,调色板(palette) 、画笔(pen) 、区域(region)，以及设备描述表(device context)。

Windows是一个以**虚拟内存**为基础的操作系统。在这种系统环境下，Windows 内存管理器经常在内存中来回移动对象，以此来满足各种应用程序的内存需要。对象被移动意味着它的地址变化了。由于地址总是如此变化，所以Windows操作系统为各应用程序腾出一些内存地址，用来专门登记各应用对象在内存中的地址变化，而这地址(存储单元的位置)本身是不变的。Windows内存管理器在移动对象在内存中的位置后，把对象新的地址告知这个句柄地址来保存。这样我们只需记住这个句柄地址就可以间接地知道对象具体在内存中的哪个位置。这个地址是在对象装载(Load) 时由系统分配给的，当系统卸载时(Unload)又释放给系统。

因此，Windows 程序中并不是用物理地址来标识一个内存块、文件、任务或动态装入模块的，相反，WINDOWS API给这些项目分配确定的句柄，并将句柄返回给应用程序，然后通过句柄来进行操作。

在Windows编程中会用到大量的句柄，比如HINSTANCE (实例句柄)、HBITMAP (位图句柄)、HDC (设备描述表句柄)、HICON (图标句柄)等。这当中还有一个通用的句柄，就是HANDLE，比如下面的语句:

```cpp
HINSTANCE hInstance;
HANDLE hInstance;
```

**句柄地址(稳定)→记载着对象在内存中的地址→对象在内存中的地址(不稳定)→实际对象**。但是，必须注意的是，程序每次重新启动，系统不能保证分配给这个程序的句柄还是原来的那个句柄，而且绝大多数情况的确是不一样的。

## 39.	指针与句柄有什么区别

指针对应着一个数据在内存中的地址，得到了指针就可以自由地修改该数据。Windows并不希望一般程序修改其内部数据结构，因为这样太不安全。所以Windows给每个使用GlobalAlloc等函数声明的内存区域指定一个句柄，句柄是一种指向指针的指针。

句柄和指针都是地址，不同之处在于:

- 句柄所指的可以是一个很复杂的结构，并且很有可能是与系统有关的。比如说线程的句柄，它指向的就是一个类或者结构，它和系统有很密切的关系。当一个线程由于不可预料的原因而终止时，系统就可以返回它所占用的资料，如CPU、内存等。反过来想可以知道，这个句柄中的某一些项是与系统进行交互的。由于Windows系统是一个多任务的系统，它随时都可能要分配内存、回收内存、重组内存。
- 指针也可以指向一个复杂的结构，但是通常是由用户定义的，所以必需的工作都要用户完成，特别是在删除的时候。

# 4.	字符串

## 1.	使用库函数将数字转换为字符串

C语言提供了几个标准库函数，可以将任意类型(整型、长整型、浮点型等)的数字转换为字符串。下面列举了各函数的方法及其说明。

- itoa():将整型值转换为字符串。
- ltoa():将长整型值转换为字符串。
- ultoa():将**无符号长整型**值转换为字符串。
- gevt():将**浮点型**数转换为字符串，取四舍五入。
- ecvt():将**双精度浮点型**值转换为字符串，转换结果中不包含十进制小数点。
- fcvt():以**指定位数为转换精度**，其余同ecvt()。

```cpp
# include <stdio.h>
# include <stdlib.h>

int main() {
    int num_int = 435;
    double num_double = 435.10f;
    char str_int[30]= {0};
    char str_double[30] = {0};
    //把整数num_int转换成字符串str_int 。
    //char *__cdecl itoa(int _Val,char *_DstBuf,int _Radix)
    itoa(num_int, str_int, 10);
    //把浮点数num_double转换成字符串str_double。
    //char *__cdecl gcvt(double _Val,int _NumOfDigits,char *_DstBuf)
    gcvt(num_double, 8, str_double);
    printf("str_int: %s\n", str_int);
    printf("str_double: %s\n", str_double);
    return 0;
}
//str_int: 435
//str_double: 435.10001
```

## 2.	不使用库函数将整数转换为字符串

**原代码：**

```cpp
#include <iostream>

using namespace std;

void int2str(int n, char *str) {
    char buf[10] = "";
    int i = 0;
    int len = 0;
    int temp = n < 0 ? -n : n;
    // temp 为n的绝对值
    if (str == NULL)
        return;

    while (temp) {
        buf[i++] = (temp % 10) + '0'; //把 temp的每一位上的数存入buf
        temp = temp / 10;
    }
    len = n < 0 ? ++i : i;
    //如果n是负数，则多需要一位来存储负号
    str[i] = 0;
    //末尾是结束符0
    while (1) {
        i--;
        if (buf[len - i - 1] == 0) {
            break;
        }
        str[i] = buf[len - i - 1];
        //把buf数组里的字符拷到字符串
    }
    if (i == 0) {
        str[i] = '-';
        //如果是负数，添加一个负号
    }
}

int main() {
    int nNum;
    char p[10];
    cout << "Please input an integer:";
    cin >> nNum;
    cout << "output:";
    int2str(nNum, p);
    //整型数转换成字符串
    cout << p << endl;
    return 0;
}
```

**myself代码：**

```cpp
#include <iostream>

using namespace std;

//计算字符数组长度
int myStrlen(char a[]) {
    int b = 0;
    for (int i = 0;; ++i) {
        if (a[i] != 0) {
            b++;
        } else {
            return b;
        }
    }
}

//按位保存
char *save(int num, char buf[]) {
    int i = 0;
    int a = num;
    int b = 0;
    while (1) {
        b = a % 10;
        a = a / 10;
        buf[i++] = b + '0';
        if (a == 0) {
            return buf;
        }
    }
}

//转换
char *int2str(int a, char *str) {
    //1.判断是否为负
    char buf[10] = {0};
    if (a < 0) {
        //使负数变为正数
        a = -a;
        str[0] = '-';
        //将数字转换为字符 倒序放入buf数组中。
        save(a, buf);
        //获取buf字符数组的长度
        int len = myStrlen(buf);
        for (int i = 1; i <= len; ++i) {
            str[i] = buf[len - i];
        }
        return str;
    } else {
        save(a, buf);
        int len = myStrlen(buf);
        for (int i = 0; i < len; ++i) {
            str[i] = buf[len - i - 1];
        }
        return str;
    }
}

int main() {
    //2^31 = 2147483648 超过该大小 则为负数。因此2147483650输出带有’-‘号.
    int a = -1235;
    char str[10];
    int2str(a, str);
    printf("str:%s\n", str);
    return 0;
}
```

## 3.	使用库函数将字符串转换为数字

C/C++提供了几个标准库函数，可以将字符串转换为任意类型(整型、长整型、浮点型等)的数字。

- atof():将字符串转换为双精度浮点型值。
- atoi():将字符串转换为整型值。
- atol():将字符串转换为长整型值。
- strtod():将字符串转换为双精度浮点型值，并报告不能被转换的所有剩余数字。
- strtol):将字符串转换为长整型值，并报告不能被转换的所有剩余数字。
- strtoul():将字符串转换为无符号长整型值，并报告不能被转换的所有剩余数字。

```cpp
#include <stdio.h>
#include <stdlib.h>

int main() {
    int num_int;
    double num_double;
    //将要被转换为整型值的字符串
    char str_int[30] = "435";
    //将要被转换为浮点型值的字符串
    char str_double[30] = "436.55";
    //转换为整型值
    num_int = atoi(str_int);
    //转换为浮点型值
    num_double = atof(str_double);
    printf("num_int: %d\n", num_int);
    printf("num_double: %lf\n", num_double);
    return 0;
}
//num_int: 435
//num_double: 436.550000
```

## 4.	不使用库函数将字符串转换为数字

**原代码：**

```cpp
#include <iostream>

using namespace std;;

int str2int(const char *str) {
    int temp = 0;
    //ptr保存str字符串开头
    const char *ptr = str;
    //如果第一-个字符是正负号，则移到下一个字符
    if (*str == '-' || *str == '+')
        str++;
    while (*str != 0) {
        //如果 当前字符不是数字，则退出循环
        if ((*str < '0') || (*str > '9')) {

            break;
        }
        // 如果当前字符是数字，则计算数值
        temp = temp * 10 + (*str - '0');
        //移到下一个字符
        str++;
    }
    //如果字符串以'-'开头，则转换成其相反数
    if (*ptr == '-') {
        temp = -temp;
    }
    return temp;
}

int main() {
    int n = 0;
    char p[10] = "";
    //从终端获取-一个字符串
    cin.getline(p, 20);
    n = str2int(p);
    cout << n << endl;
    return 0;
}
//-126
//-126
//125
//125
```

**myself代码：**

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

int str2int(char *str) {
    int out = 0;
    int flag = 1;
    //1.判断正负号,然后进指向下一位
    if (*str == '-') {
        //0为负数。1为正数
        flag = 0;
        //指针指向符号为之后
        str++;
    }
    //1.判断是否为数字
    while (*str != 0) {
        if (*str < '0' || *str > '9') {
            break;
        } else {
            out = out * 10 + (*str++ - 48);
        }
    }
    //根据标志位 更改符号
    return out = flag ? out : -out;
}


int main() {
    char input[20] = {0};
    int a[] = {1,2,3};
    int len = sizeof(a)/sizeof(int);
    //1.getline(char_type* __s, streamsize __n)
    //参数：char指针，n-1=保存有效长度。   -->n = 10,表示只保存9个输入结果，多余的将抛弃。
    //2.getline(char_type* __s, streamsize __n, char_type __delim)
    //参数:char指针，n-1=保存有效长度，自定义的结束符。
    cin.getline(input, 10);
    int out = str2int(input);
    printf("out:%d\n", out);

    return 0;
}
//123456
//out:123456
```

## 5.	编程实现strcpy函数

**原代码：**

```cpp
#include <stdio.h>

// 实现strSrc到strDest的复制
char *strcpy(char *strDest, const char *strSrc) {
    //判断参数strDest和strSrc的有效性
    if ((strDest == NULL) || (strSrc == NULL)) {
        return NULL;
    }
    //保存目标字符串的首地址
    char *strDestCopy = strDest;
    //把strSrc字符串的内容复制到strDest下
    while ((*strDest++ = *strSrc++) != '\0');
    return strDestCopy;
}

//实现获取strSrc字符串的长度
int getStrLen(const char *strSrc) {
    //保存长度
    int len = 0;
    //循环直到遇见结束符'\0'为止
    while (*strSrc++ != '\0') {
        len++;
    }
    return len;
}

int main() {
    //要被复制的源字符串
    char strSrc[] = "Hello World!";
    //要复制到的目的字符数组
    char strDest[20];
    //保存目的字符数组中字符串的长度
    int len = 0;
    //链式表达式,先复制后计算长度
    len = getStrLen(strcpy(strDest, strSrc));
    printf("strDest: %s\n", strDest);
    printf("Length of strDest: %d\n", len);
    return 0;
}
//strDest: Hello World!
//Length of strDest: 12
```

**myself代码：**

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

char *myStrcpy(char *dest, const char *src) {
    //1、判断是否为空
    if (src == NULL || src == NULL) {
        return NULL;
    }
    //保存字符串首地址
    char *temp = dest;
    //将src复制到dest中
    while (*src != '\0') {
        *dest++ = *src++;
    }
    return temp;
}

//计算字符数组长度
int myStrlen(const char *a) {
    int b = 0;
    while (*a++ != '\0') {
        b++;
    }
    return b;
}

int main() {
    char src[] = "Hello World!";
    char dest[20] = "";
    printf("src len:%d\n", myStrlen(src));
    printf("len:%d\n", myStrlen(myStrcpy(dest, src)));
    printf("dest len:%d\n", myStrlen(dest));
    printf("dest:%s\n", dest);
    return 0;
}
//src len:12
//len:12
//dest len:12
//dest:Hello World!
//不明白调试的时候，myStrcpy1中的dest无法查看实时相容。但结果正确。此时使用链式表达式求结果时，返回长度为0.。。。。
```

## 6.	编程实现memcpy函数

**原代码：**

```cpp
#include <stdio.h>
#include <assert.h>

void *memcpy2(void *memTo, const void *memFrom, size_t size) {
    //memTo和memFrom必须有效
    assert((memTo != NULL) && (memFrom != NULL));
    //保存memFrom首地址
    char *tempFrom = (char *) memFrom;
    //保存memTo首地址
    char *tempTo = (char *) memTo;
    //循环size次,复制memFrom的值到memTo中
    while (size-- > 0)
        *tempTo++ = *tempFrom++;
    return memTo;
}

int main() {
    //将被复制的字符数组
    char strSrc[] = "Hello World!";
    //目的字符数组
    char strDest[20];
    //复制strSrc的前4个字符到strDest中
    memcpy2(strDest, strSrc, 8);
    //把strDest的第5个元素赋为结束符'\0'
    strDest[8] = '\0';

    printf("strDest: %s\n", strDest);
    return 0;
}
//strDest: Hello Wo
```

**myself代码：**

```cpp
#include <stdio.h>
#include <iostream>
#include <cstring>

using namespace std;

void *myMemcpy(void *memTo, const void *memFrom, size_t size) {
    if (memTo == NULL || memFrom == NULL)
        return NULL;
    char *tempMemto = (char *) memTo;
    char *tempMemForm = (char *) memFrom;
    char *temp = tempMemto;
    while (size-- > 0) {
        *tempMemto++ = *tempMemForm++;
    }
    *tempMemto = '\0';
    return tempMemto;
}

int main() {
    char from[] = "hello worldqwer";
    char to[20];
    myMemcpy(to, from, 8);
    printf("len:%d\n", strlen(to));
    printf("to:%s\n", to);
    return 0;
}
//len:8
//to:hello wo
```

## 7.	strcpy与memcpy的区别

- **复制的内容不同。**strcpy 只能复制字符串，而memcpy可以复制任意内容，例如字符数组、整型、结构体、类等。
- **复制的方法不同。**strcpy 不需要指定长度，它是遇到字符串结束符"\0"而结束的。memcpy则是根据其第三个参数决定复制的长度。
- **用途不同。**通常在复制字符串时用strcpy;而若需要复制其他类型数据，则一般用memcpy。

## 8.	改错----数组越界

```cpp
#include <stdio.h>
#include <iostream>
#include <cstring>

using namespace std;

void test1() {
    char string[10];
    char *str1 = "0123456789";
    strcpy(string, str1);
}

void test2() {
    char string[10], str1[10];
    int i;
    for (i = 0; i < 10; i++) {
        str1[i] = 'a';
        strcpy(string, str1);
    }
}

void test3(char *str1) {
    char string[10];
    if (strlen(str1) <= 10) {
        strcpy(string, str1);
    }
}

int main() {
    test1();
    test2();
    test3("123");
    return 0;
}
```

以上三个程序的通病是没有为字符串的'\0'留下空间，导致数组越界。对strcpy这种依靠'\0'判断结束的函数有一定局限。

## 9.	分析程序----数组越界

```cpp
#define MAX 255

int main() {
    unsigned char A[MAX], i;
    for (i = 0; i <= MAX; i++)
        A[i] = i;
}
```

代码第5行的for循环中用的是“<=”，当i=MAX时发生数组越界。注意:这个程序很容易使人误认为只有数组越界的问题，但只要再细心些就能发现，i 是无符号的char类型，它的范围是0~255，所以i<=MAX一直都是真，这样会导致无限循环。可以把“i<=MAX" 改为i<MAX，这样既避免了无限循环，又避免了数组越界。

**改正：**

```cpp
#define MAX 255

int main() {
    unsigned char A[MAX], i;
    for (i = 0; i < MAX; i++)
        A[i] = i;
}
```

## 10.	分析程序----打印操作可能产生数组越界

```cpp
#include <stdio.h>;

int main() {
    int a[5] = {0, 1, 2, 3, 4}, *p;
    p = a;
    printf("%d\n", *(p + 4 * sizeof(int)));
    return 0;
}
//4225568
```

打印越界归根结底仍是访问越界。

## 11.	编程实现计算字符串的长度

```cpp
#include <stdio.h>
#include <assert.h>

int strlen1(const char *src) {
    assert(NULL != src);
    //src必须有效
    int len = 0;
    //保存src的长度
    while (*src++ != '\0')
        //遇到结束符' \0'时退出循环
        len++;
    //每循环一-次，len 加1
    return len;
}

int strlen2(const char *src) {
    assert(NULL != src);
    //src必须有效
    const char *temp = src;
    //保存src首地址
    while (*src++ != '\0');
    //遇到结束符' \0 '时退出循环
    return (src - temp - 1);
    //返回尾部指针与头部指针之差，即长度
}

int main() {
    char p[] = "Hello World!";
    printf("strlen1 len: %d\n", strlen1(p));
    //打印方法1得到的结果
    printf("strlen2 len: %d\n", strlen2(p));
    //打印方法2得到的结果
    return 0;
}
```

strlen1和strlen2这两个函数都可以用来计算字符串长度。下面来比较它们的区别:

**strlen1用一个局部变量len在遍历的时候做自增，然后返回len。因此，每当while循环一次，就需要执行两次自增操作。**

**strlen2用一个局部变量temp记录src遍历前的位置。while 循环一次只需要一 次自增操作。最后返回指针之间的位置差。**

显然，strlen2比strlen1的效率要高，尤其是在字符串较长的时候。

## 12.	编程实现字符串中子串的查找

**原程序:**

```cpp
#include <stdio.h>
#include <assert.h>

char *strstr(char *src, char *sub) {
    const char *bp;
    const char *sp;
    //判断src 与sub的有效性
    if (src == NULL || NULL == sub) {
        return src;
    }
    //遍历 src字符串
    while (*src) {
        //用于src的遍历
        bp = src;
        //用于sub的遍历
        sp = sub;
        //遍历sub字符串
        do {
            //如果到了sub字符串结束符位置
            if (!*sp)
                //表示找到了sub字符串，退出
                return src;
        } while (*bp++ == *sp++);
        src += 1;
    }
    return NULL;
}

int main() {
    char p[] = "123456";
    char q[] = "34";
    char *r = strstr(p, q);
    printf("r:%s\n", r);
}
```

**myself程序：**

```cpp
#include <stdio.h>
#include <iostream>
#include <cstring>

using namespace std;

int myStrstr(const char *far_str, const char *sub_str) {

    if (*far_str == NULL || sub_str == NULL) {
        return 0;
    }
    int far_len = strlen(far_str);
    int sub_len = strlen(sub_str);
    //子串长度大于父串，返回-1
    if (far_len < sub_len) {
        return -1;
    }
    //用于记录far_str中第几个字符与sub_str中的首字符匹配
    int i = 0;

    while (*far_str) {
        if (*far_str == *sub_str) {
            //首字符相同,进行后续字符匹配,先判断sub_str是否结束，然后才判断二者后一位是否相等
            do {
                if (!*sub_str) {
                    return i;
                }
            } while (*far_str++ == *sub_str++);
        } else {
            //首字符不匹配时，是far_str指针移动
            far_str++;
            //记位加一
            i++;
        }
    }
    //没有匹配时，返回0
    return 0;
}

int main() {
    char a[] = "123456";
    char b[] = "3454";
    int c = myStrstr(a, b);
    printf("c:%d\n", c);
    return 0;
}
```

## 13.	编程实现字符串中各单词的翻转





# 5.	位运算与嵌入式编程

## 1.	位置转换

```cpp
#include <stdio.h>
int main(int argc,char* argv[]) {
    int i = 5.01;
    float f = 5;
    printf("%f\n", 5);
    printf("%f\n", 5.001);
    printf("%f\n", f);
    printf("%d\n", 5.01);
    printf("%d\n", i);
    return 0;
}

//0.000000    ?
//5.010000    
//5.000000  
//1889785610  ?
//5
```

32位平台中int和float都占4个字节，double 占8个字节。平台的

printf根据说明符“%f”，认为参数应该是个double类型的参数(在printf 函数中，float会自动转换成double)，因此从栈中读了8个字节。类似地，当printf后的说明符为"%d"时,会认为参数应该是个int类型的参数，因此从栈中读了4个字节。

代码第5行，首先参数5为int型，所以在栈中分配了4个字节的内存用于存放参数5。然后printf从栈中读8个字节。很显然，内存访问越界，会有不可预料的情况发生。

与之相反的是第8行，参数5.01占8个字节，而printf读4个字节，同样会出现不可预料的情况。

## 2.	看代码写出结果----位运算

```cpp
#include <stdio.h>

int main(int argc, char *argv[]) {
    //2字节，共2*8bit，所以范围为0-65535 
    unsigned short int i = 0;
    //1字节，8bit，取值范围为0-255
    unsigned char ii = 255;
    int j = 8, p, q;
    
    p = j << 1;
    q = j >> 1;
    i = i - 1;
    ii = ii + 1;
    printf("i = %d\n", i);
    printf("ii = %d\n", ii);
    printf("p = %d\n", p);
    printf("q = %d\n", q);
    return 0;
}
//i = 65535
//ii = 0
//p = 16
//q = 4
```

i在内存中为0x0000,减一之后，数据变为0xffff,即为65535.

ii在内存中为0xff，加一之后，数据变为0x00，结果为0.

## 3.	设置或清除特定的位

```cpp
#include <stdio.h>
#include <iostream>

#define BIT3 (0x1 << 3)

using namespace std;

static int a = 8;

//保证某一位为1
void set_bit3() {
    a |= BIT3;
}

//保证某一位为0
void clear_bit3() {
    a &= ~BIT3;
}

int main() {
    printf("a:%d\n", a);
    clear_bit3();
    printf("a:%d\n", a);
    set_bit3();
    printf("a:%d\n", a);
}
//a:8
//a:0
//a:8
```

## 4.	计算一个字节里有多少bit被置1

```cpp
#include <stdio.h>

#define BIT7 (0x1 << 7)  //10000000

int calculate(unsigned char C) {
    int count = 0;
    int i = 0;
    unsigned char comp = BIT7;
    for (i = 0; i < sizeof(C) * 8; i++) {
        //同 1 异 0
        if ((C & comp) != 0) {
            count++;
        }
        comp = comp >> 1;
    }
    return count;
}

int main(int argc, char *argv[]) {
    unsigned char c = 0;
    int count = 0;
    printf("c = ");
    scanf("%d", &c);
    count = calculate(c);
    printf("count = %d\n", count);
    return 0;
}
//c =254
//count = 7
```

一个字节(byte)有8位，因此首先在宏定义BIT7中将最高位置成1。然后在calculate函数中比较每个位是否被置成1，如果是，则为count++,循环结束后返回count的值。

## 5.	位运算改错

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

#define BIT_MASK(bit_pos) (0x01<<(bit_pos))

int Bit_Reset(unsigned int *val, unsigned char pos) {
    if (pos >= sizeof(unsigned int) * 8) {
        return 0;
    }
    val = (val && ~BIT_MASK(pos));
    return 1;
}


int main() {
    unsigned int a = 12; //1100
    Bit_Reset(&a, 3);
    return 0;
}
```

在第12 行中，‘&&’是逻辑运算符，不是位运算符，应该为‘&’，改为‘&’之后，出现问题，

```
cpp:12:43:error: invalid operands of types 'unsigned int*' and 'int' to binary 'operator&'
			#define BIT_MASK(bit_pos) (0x01<<(bit_pos))
													  ^
```

原因是预定义默认是int型，而val默认是(unsigned int *)型，因此将val变为(unsigned int)型，

**改正如下**：

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

#define BIT_MASK(bit_pos) (0x01<<(bit_pos))

int Bit_Reset(unsigned int *val, unsigned char pos) {
    if (pos >= sizeof(unsigned int) * 8) {
        return 0;
    }
    *val = (*val & ~BIT_MASK(pos));
    return 1;
}


int main() {
    unsigned int a = 12; //1100
    Bit_Reset(&a, 3);
    return 0;
}
```

## 6.	运用位运算交换a、b两数

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

int main() {
    int a = 3;
    int b = 5;

    a ^= b;
    b ^= a;
    a ^= b;

    printf("a:%d,b:%d\n", a, b);
    return 0;
}
//a:5,b:3
```

**异或**也称为**半加运算**，即相对于加法来说，**只相加，不进位**。

## 7.	列举并解释C++中的4种运算符转化以及它们的不同点

- **const_cast** 操作符:用来帮助调用那些**应该使用却没有使用const关键字的函数**。换句话说，就是供程序设计师在特殊情况下**将限制为const成员函数的const定义解除，使其能更改特定属性**。

- **dynamic_ cast** 操作符:如果启动了支持运行时间类型信息(RTTI)， dynamic_cast可以有助于判断在运行时所指向对象的确切类型。它与**typeid**运算符有关。**可以将一个基类的指针指向许多不同的子类型(派生类),然后将被转型为基础类的对象还原成原来的类**。不过，**限于对象指针的类型转换，而非对象变量**。

- **reinterpret_cast** 操作符:**将一个指针转换成其他类型的指针**，新类型的指针与旧指针可以毫不相关。通常用于某些非标准的指针数据类型转换，例如将(void \*)转换为(char)。它也可以用在指针和整型数之间的类型转换上。

    注意:它存在潜在的危险，除非有使用它的充分理由，否则就不要使用它。例如，它能够将一个(int \*)类型的指针转换为(float*)类型的指针，但是这样就会很容易造成整数数据不能被正确地读取。

- **static_cast** 操作符:它能在相关的对象和指针类型之间进行类型转换。有关的类之间必须通过继承、构造函数或者转换函数发生联系。static_cast操作符还能在数字(原始的)类型之间进行类型转换。通常情况下，**static_cast 操作符大多用于将数域宽度较大的类型转换为较小的类型**。当转换的类型是原始数据类型时，这种操作可以有效地禁止编译器发出警告。

## 8.	用#define声明一个参数

```cpp
#include <stdio.h>
#include <iostream>
#define SECOND_PER_YEAR (unsigned long) (365 * 24 * 60 * 60)
//#define SECOND_PER_YEAR  (365 * 24 * 60 * 60ul)

using namespace std;

int main(){

    printf("sizeof(long long)%d\n",sizeof(long long) );
    printf("sizeof(long)%d\n", sizeof(long));
    printf("sizeof(int)%d\n", sizeof(int));
    printf("sizeof(short)%d\n",sizeof(short) );

    printf("%ld\n", SECOND_PER_YEAR);
}
//64
//sizeof(long long)8
//sizeof(long)4
//sizeof(int)4
//sizeof(short)2
//31536000
```

书上的例子是在16位机器上，因此会溢出，而在32位或64位上，这个时间的值是不会溢出的，因此像第4行一样，末尾加ul。

## 9.	如何用C语言编写死循环

```cpp
while(1){}
```

```cpp
for(;;){}
```

```cpp
Loop:
...
goto Loop;
```

第一种**首推**，第二种无法见名知意，而第三种更偏向于汇编。

## 10.	√如何访问特定位置的内存

```cpp
#include <stdio.h>

using namespace std;

int main(){
    int *ptr;
    ptr = (int *)0x67a9;
    *ptr = 0x100;
    printf("%d\n", *ptr);
    return 0;
}
```

或者

```cpp
#include <stdio.h>

using namespace std;

int main(){
    *(int * const)(0x67a9) = 0x100;
    printf("%d\n", *ptr);
    return 0;
}
```

上述二者皆可以访问特定内存，但是运行时节会发生**段错误(Segmentation fault)**。无法为特定地址进行设置。

## 11.	对中断服务代码的评论

中断是嵌入式系统中重要的组成部分，这导致很多编译开发商提供一种扩 展，让标准C支持中断。而事实是，产生了一个新的关键字\_\_interrupt。 下面的代码就使用了\_\_interrupt关键字去定义一个中断服务子程序(ISR)。

```c
__interrupt double coputer_area(double radius){
	double area = PI * radius * radius;
	printf("Area = %f",area);
	return area;
}
```

错误：

- ISR不能返回一个值。
- ISR不能传递参数。
- 在许多的处理器/编译器中，浮点一般都是不可重入的。有些处理器/编译器需要让额外的寄存器入栈，有些处理器/编译器就是不允许在ISR中做浮点运算。此外，ISR应该是短且有效率的，在ISR中做浮点运算是不明智的。
- printf()经常有重入和性能上的问题。

## 12.	看代码写结果----整数的自动转换

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

void foo(void){
    unsigned int a = 6;
    int b = -20;
    printf("a+b: %u\n", a+b);
    if(a + b > 6)
        puts(">6");
    else
        puts("<=6");
}

int main(){
    foo();
    return 0;
}
//a+b: 4294967282
//>6
```

当表达式中存在**有符号类型**和**无符号类型**时，所有的操作数都自动转换为**无符号类型**。因此，-20变成了一个非常大的

正整数(-20 mod 2^32 = 4294967276)，所以该表达式计算出的结果(4294967276 + 6 = 4294967282)大于6。

## 13.	关键字static的作用是什么

在C语言中，关键字static有以下3个明显的作用。

- 在函数体内，一个被声明为静态的变量在这一函数被调用的过程中维持其值不变。
- 在模块内(但在函数体外)，一个被声明为静态的变量可以被模块内所有函数访问，但不能被模块外其他函数访问。它是一个本地的全局变量。
- 在模块内，一个被声明为静态的函数只可被这一模块内的其他函数调用。那就是，这个函数**被限制在声明它模块的本地范围内使用**。

## 14.	关键字volatile有什么含义

一个定义为volatile的变量是说这变量可能会被意想不到地改变，这样，编译器就不会去假设这个变量的值了。精确地说，就是优化器在**用到这个变量时必须每次都小心地重新读取这个变量的值**，而不是使用保存在寄存器里的备份。

- 并行设备的硬件寄存器(如状态寄存器); 
- 一个中断服务子程序(ISR)中会访问到的非自动变量(Non-automatic variables);
- 多线程应用中被几个任务共享的变量。

## 15.	判断处理器是Big_endian还是Little_endian

采用**Little-endian**模式的CPU对操作数的存放方式是**从低字节到高字节**，而**Big-endian**模式对操作数的存放方式是**从高字节到低字节**。简记为“**小端低低**”。

```c
#include <stdio.h>
#include <iostream>

using namespace std;

int checkCPU(){
    union w{
        int a;
        char b;
    } c;
    c.a = 0x12345678;
    return (c.b == 0x78);	
}

int main(){
    if (checkCPU())
        printf("%s\n", "little endian!\n");
    else
        printf("%s\n", "big endian!\n");
    return 0;
}
//little endian!
```

**联合体union的存放顺序是所有成员都从低地址开始存放**。

十六进制数：0x12345678在内存中的，表示如下：

|    高地址    |    31 ~24    |    23~16     |     15~8     |     7~0      | 低地址 |
| :----------: | :----------: | :----------: | :----------: | :----------: | :----: |
|   小端模式   |     0x12     |     0x34     |     0x56     |     0x78     |        |
| 存储次序方向 | $\leftarrow$ | $\leftarrow$ | $\leftarrow$ | $\leftarrow$ |        |
|              |              |              |              |              |        |
|   大端模式   |     0x78     |     0x56     |     0x34     |     0x12     |        |
| 存储次序方向 | $\leftarrow$ | $\leftarrow$ | $\leftarrow$ | $\leftarrow$ |        |

## 16.	评价代码片断----处理器字长

```c
#include <stdio.h>
#include <iostream>

using namespace std;

int main(){
    unsigned int zero = 0;
    //1's complement of zero。 零的 1的补码 即指0的反码。
    unsigned int compzero = 0xFFFF;
    return 0;
}
```

对于16位机器来说 这段代码是正确的。但是非16位机，则不正确。因为非十六位机的反码不是0xffff，所以取反更合适。

改正：

```c
#include <stdio.h>
#include <iostream>

using namespace std;

int main(){
    unsigned int zero = 0;
    //1's complement of zero。 零的 1的补码 即指0的反码。
    unsigned int compzero = ~zero;
    return 0;
}
```

# 6.	C++面向对象

## 1.	描述面向对象技术的基本概念