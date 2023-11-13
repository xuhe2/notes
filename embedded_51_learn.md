8位

RAM:512字节

ROM:8K(Flash)



# 概念



## 寄存器

存储以8个为一组的



## 驱动器

增强驱动能力



# 点亮LED灯

LED模块的电阻阅读方式

> 102 = 10 00
>
> 前面两位是有效位数
>
> 后面的位数是10的多少次方



使用CPU给寄存器写入值,然后通过驱动器实现控制我的硬件部分



* 根据LED模块的原理图,我们可以知道**从P20到P27**的部分可以用来控制LED模块
* 使用十六进制**使用`0x`作为开头**,代表我们给的是一个十六进制的值

注意,需要使用头文件

```c
#include <REGX52.H>
```

```c
P2 = 0xFE; 
```

然后给我的P2,代表从**P20到P27**八个,用十六进制表示的值



# 闪烁LED

使用STC-ISP的**软件延时计算器**

* 12MHZ
* 使用**STC-V1**指令集

使用它生成的函数



* 注意,需要使用头文件

```c
#include <INTRINS.H>
```



# 延时函数(使用ms)

```c
void Delay(unsigned int time_ms)		//@12.000MHz
{
	unsigned char i, j;
	while (time_ms--){
		i = 2;
		j = 239;
		do
		{
			while (--j);
		} while (--i);
	}
}
```



# 使用按键控制LED灯

注意,这个按键的抖动会干扰.

使用的**P3**来控制

```c
P2_0 = P3_0;
P2_1 = P3_1;
```







# 数码管的控制

* 译码器的使用的时候,需要使用**LE**(决定从哪边传输到哪边)



可以使用译码器(3输入**使用P2**)控制八个输出(代表**8个数码管亮的是哪个**)

使用**P0**控制数码管怎么亮



## 控制在数码管的哪个部分显示什么数据

```c
void Nixie(unsigned char Location,Number)
{
	unsigned char Nixietable[]={0x3F,0x06,0x5B,0x4F,0x66,0x6D,0x7D,0x07,0x7F,0x6F,0x77,0x7C,0x39,0x5E,0x79,0x71,0x00};
	switch(Location)
	{
		case 1:P2_4=1;P2_3=1;P2_2=1;break;//LED1
		case 2:P2_4=1;P2_3=1;P2_2=0;break;//LED2
		case 3:P2_4=1;P2_3=0;P2_2=1;break;//LED3
		case 4:P2_4=1;P2_3=0;P2_2=0;break;//LED4
		case 5:P2_4=0;P2_3=1;P2_2=1;break;//LED5
		case 6:P2_4=0;P2_3=1;P2_2=0;break;//LED6
		case 7:P2_4=0;P2_3=0;P2_2=1;break;//LED7
		case 8:P2_4=0;P2_3=0;P2_2=0;break;//LED8
	}
	P0=Nixietable[Number];
	Delay(1);
	P0 = 0x00;
}
```



# 矩阵键盘

使用举证表示的时候,比如8个IO口,可以实现**4*4**的按键个数

```c
#include <reg51.h>

#include "Delay.h"

#include "MatrixKeyboard.h"

unsigned int getMatrixKey()
{
    unsigned int key = 0;
    P1 = 0xFF;
    P1_3 = 0; // 扫描第一列
    if (!P1_7)
    {
        Delay(20); // 防抖
        while (!P1_7)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 1;
    }
    if (!P1_6)
    {
        Delay(20); // 防抖
        while (!P1_6)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 5;
    }
    if (!P1_5)
    {
        Delay(20); // 防抖
        while (!P1_5)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 9;
    }
    if (!P1_4)
    {
        Delay(20); // 防抖
        while (!P1_4)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 13;
    }

    P1 = 0xFF;
    P1_2 = 0;
    if (!P1_7)
    {
        Delay(20); // 防抖
        while (!P1_7)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 2;
    }
    if (!P1_6)
    {
        Delay(20); // 防抖
        while (!P1_6)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 6;
    }
    if (!P1_5)
    {
        Delay(20); // 防抖
        while (!P1_5)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 10;
    }
    if (!P1_4)
    {
        Delay(20); // 防抖
        while (!P1_4)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 14;
    }

    P1 = 0xFF;
    P1_1 = 0;
    if (!P1_7)
    {
        Delay(20); // 防抖
        while (!P1_7)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 3;
    }
    if (!P1_6)
    {
        Delay(20); // 防抖
        while (!P1_6)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 7;
    }
    if (!P1_5)
    {
        Delay(20); // 防抖
        while (!P1_5)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 11;
    }
    if (!P1_4)
    {
        Delay(20); // 防抖
        while (!P1_4)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 15;
    }

    P1 = 0xFF;
    P1_0 = 0;
    if (!P1_7)
    {
        Delay(20); // 防抖
        while (!P1_7)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 4;
    }
    if (!P1_6)
    {
        Delay(20); // 防抖
        while (!P1_6)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 8;
    }
    if (!P1_5)
    {
        Delay(20); // 防抖
        while (!P1_5)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 12;
    }
    if (!P1_4)
    {
        Delay(20); // 防抖
        while (!P1_4)
            ;      // 等待按键释放
        Delay(20); // 防抖
        key = 16;
    }

    P1 = 0xFF;

    return key; // 返回按下的键的编号
}
```



# 定时器(timer)

使用`while`语句实现暂停,对性能的消耗很大.

使用**定时器**软计时

* 使用定时器的时候不需要使用**CPU**.

* 定时器的资源和51单片机的信号有关,但是向下兼容

* 计数器最多只能到65535



> 使用脉冲信号进行计数,到达一定的程度之后,发送中断信号



SYSclk(系统时钟)有晶振周期



**T/C**是控制使用**Timer/Counter**的模式的开关



# 中断系统

可以使用多个中断源

* 每个中断源具有中断的优先级别
* 低优先级的中断执行中出现高优先级的中断也满足这些方式



# 定时器/计数器控制寄存器(TCON)

TF(timer flag) 标记是否当溢出的时候中断

TR(timer ready) 标记是否允许计数

TH(timer high) 控制的是计数器的高位

TL(timer low) 控制的是计数器的低位



* 单独赋值

```c
TF0 = 0;
FR0 = 0;
```



## 使用计时器

> 每隔1us计数+1
>
> 总计的时间是65535us
>
> 所以,
>
> 当我们设置TH TL 一起为64535的时候,距离响起来是1000us

```C
TH0 = 64535 / 256;
TL0 = 64535 % 256;
```

* 1e6 us = 1 s





# 定时器/计数器工作模式寄存器(TMOD)

M1 M0 用来控制什么模式

也可以设置C/T'

* `TMOD`不能只赋值一个位



# 中断寄存器

EA(enable all)是否允许使用全部,总开关

> IE里面还有控制单个的开关的方法

PT0 优先级控制



## 使用中断

```c
ET0 = 1;
EA = 1;
```



## 中断函数定义

```c
void Timer0_Routine() __interrupt 1
{
}
```

* `SDCC`使用`__interrupt`实现



> 因为每次调用中断函数之后,时间会**回到0**的状态,我们需要重置时间

```c
void Timer0_Routine() __interrupt 1
{
    // 重置时间
    TH0 = 64535 / 256;
    TL0 = 64535 % 256;
    // code
}
```



# 使用定时器计算器(来自STC-ISP)

1. 设置**系统频率**
2. 设置**定时器类型**
3. 设置**定时器模式**,设置为**16位**
4. 设置**定时器时钟**为**12T**.

* 每次都需要重新配置的

* 需要设置`EA`和`ET`.



# 串口通信



## SBUF

储存数据的地方



## SMOD

控制波特率的

> 给1的时候波特率加倍,给0的时候波特率不加倍



## SCON

* REN:是否同意接受信息.
* TI:发送中断请求的标志位



## 双8位自动重装

不需要手动不断设置初值

```c
TMOD |= 0x20;
```

一个8位计时,一个设置初始值.