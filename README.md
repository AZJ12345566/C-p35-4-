# C-p35-4-
C语言学习笔记 p35指针详解(4)
//C陷阱和缺陷
#include<stdio.h>
void Print(char* str)
{
    printf("%s\n",str);
}
int main()
{
    int a=0;
    int* pa;
    void(*p)(char*)=Print;//这里的p不能放在char*后面
    (*p)("hello bit");
    return 0;
}

//代码1
(*(void(*)())0)();
//void(*)()函数指针类型-0就是一个函数的地址
//这行代码本质就是一次函数调用，，调用0地址处，参数为无参，返回类型为void的那个函数

//代码2
void (*signal(int,void(*)(int)))(int);
//此代码第一个参数为整形，第二个参数为函数指针类型
//简洁版
typedef void(*pfun_t)(int);//后面的参数名永远和*放在一起
pfun_t signal(int,pfun_t);
//这两句代码合起来变成上面那一句复杂的代码
//代码口头阐述：
//signal是一个函数声明
//signal函数的参数有2个，第一个是int，第二个是函数指针，该函数指针指向的函数的参数是int，返回类型是void
//signal函数的返回类型也是一个函数指针：该函数指针指向的函数的参数是int，返回类型是void



int main()
{
    int a=10;
    int b=20;
    int(*pa)(int,int)=Add;
    printf("%d\n",pa(2,3));
    printf("%d\n",Add(2,3));
    printf("%d\n",*pa(2,3));//这种是编不过去的，必须给*pa加()
    printf("%d\n",(*pa)(2,3));
    retrun 0;
}



//函数指针数组
int Add(int x,int y)
{
    return x+y;
}
intSub(int x,int y)
{
    return x-y;
}
int Mul(int x,int y)
{
    return x*y;
}
int Div(int x,int y)
{
    return x/y;
}
int main()
{
    //指针数组
    int* arr[5];
    //需要一个数组，这个数组可以存放4个函数的地址-函数指针的数组
    int(*pa)(int,int)=Add;//Sub/Mul/Div
    int(*parr[4])(int,int)={Add,Sub,Mul,Div}//函数指针数组
    inti=0;
    for(i=0;i<4;i++)
    {
        printf("%d\n",parr[i](2,3));
    }
    return 0;
}
