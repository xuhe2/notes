# TIPS

使用卡诺图的时候,必须使用gray code

卡诺图中的X(**无关状态**)在表达式中是d(1,2...)

圈起来的时候一定要2的幂次个数



一个圆圈可以表示非,一个斜线也可以表示非.



> 公式化简方法
> $$
> A+AB = A
> $$
> 



最大项是最小项的非



151 8选1

153 4选一



# 1-1



analog 模拟

digital 电子



DAC : digital to analog converter

> in a mixed system



# 1-2

1. use votage level
2. use current level



> bit : one binary digit



clock:时钟:同步不同的元器件



pulse: 脉冲

pulse width:脉宽:从上升边的50%到下降边的50%的距离



rising edge : 从0到1的上升边

falling edge : 从1到0的下降边



rising time : 从10%到90%的上升需要的时间

falling time



占空比（Duty Cycle）是一个在电子技术中经常使用的概念，通常用于描述周期性信号（如脉冲信号或方波信号）中的高电平（或开启状态）与总周期之间的比例。占空比通常用百分比表示，它告诉我们信号在一个周期内处于高电平状态的时间与整个周期的比例。

占空比的计算公式如下：


$$
\text{占空比} (\%) = \frac{\text{高电平时间}}{\text{总周期时间}} \times 100\%
$$


其中：

- 高电平时间：信号处于高电平状态（逻辑“1”或通常是正电压）的持续时间。
- 总周期时间：一个完整的周期所需要的时间。

举例来说，如果有一个方波信号，周期为1秒，其中高电平时间为0.2秒，那么占空比为：
$$
[ \text{占空比} = \frac{0.2\, \text{秒}}{1\, \text{秒}} \times 100\% = 20\% ]
$$




这表示在这个信号中，高电平占了总周期的20%。

占空比在电子电路中非常重要，因为它可以影响信号的平均功率、频率响应以及电路的性能。在控制电路、PWM（脉宽调制）调光、电机驱动、信号传输等应用中，占空比的设置和调整都扮演着关键的角色。







数据传输

1. serial transform单传递,一次只传送一个1bit
2. parallel transform并发传输,一次传递多个



# 2 



## 2-1

radix/base : 进制

carry : 进位



## 进制转换

小数点之后的部分不断乘以2,如果结果等于1的时候获得当前位置是1



## 2-5



1. 反码（Ones' Complement）：
   - 反码是一种用于表示有符号整数的编码方式。
   - 在反码中，正数的二进制表示与其绝对值的二进制表示相同，即符号位为0。
   - 负数的反码表示方法是将其绝对值的二进制表示中的每一位取反（0变为1，1变为0），同时保留符号位为1表示负数。
   - 反码的缺点是有两个零表示：+0和-0。
2. 补码（Two's Complement）：
   - 补码也是一种用于表示有符号整数的编码方式，是最广泛使用的有符号整数表示方法。
   - 在补码中，正数的二进制表示与其绝对值的二进制表示相同，即符号位为0。
   - 负数的补码表示方法是将其绝对值的二进制表示中的每一位取反（0变为1，1变为0），然后再加1，同时保留符号位为1表示负数。
   - 补码的优点是只有一个零表示：0，而且它可以更自然地支持加法和减法操作，因为减法可以通过加法来实现。



* 其实,计算单元只有加法器



* 注意,需要体现出进制的位数.



## BCD`binary coded decimal`

> 本质是十进制数
>
> 所以不可能出现1010-1111
>
> 当你需要使用`BCD`编码表示13这样的时候,他是和16进制的表示方式是不同的.



## `gray`code

表达的位数依次提升的时候,每次变化的位数只有一位.

* 防止一次一次变化的时候,造成数据传输的问题.

* 可以实现和2进制数值额相互转换.



* is a unweighted code



### gray code和binary code转换

二进制和格雷码都是一种数字编码方式，它们的特点是相邻的两个数只有一位二进制位不同。二进制和格雷码的转换可以用异或运算来实现。具体的原理和公式如下：

- 二进制转格雷码：保留二进制的最高位作为格雷码的最高位，次高位的格雷码为二进制的高位和次高位相异或，其他位与次高位类似。

- 格雷码转二进制：保留格雷码的最高位作为二进制的最高位，次高位的二进制为高位二进制和次高位格雷码相异或，其他位与次高位类似。



# parity method

mas奇偶校验

> 传输的代码中,1的个数是奇数:奇校验
>
> 同理,偶校验

* 同来纠错的





# 逻辑门

## inverter

> 取反



## and gate

> A&B使用`AB`,或者中间加个点来表示.



mask:屏蔽字

> 可以使用`and`运算符来只保留我自己想要的几个位置的01值,其他位置的全部变成0
>
> 用来保留模板串中是1的位置的01值.



## or gate

> 使用`A+B`表示



* 也可以做`mask`操作



## NAND gate

与非门



* 可以用`NAND gate`表示全部的门



## NOR gate



anode : 阳极

阴极 : catnode





## XOR gate

异或门

> 表示符号:圆圈里面是叉叉



## XNOR gate

同或运算符

只有在AB输入相同的时候,才是1

> 圆圈里面加上点.

* 对于比较器有用.



# rules

1. commutative law 交换律
2. assocative law 结合律
3. distributive law 分配律



## 布尔代数

A+AB = A

> 可以使用`venn diagram`证明

* 书本P102



![image-20231225135336906](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20231225135336906.png)



# SOP/POS

sum of product : 乘积和

product of sum 



转换为标准变量的样子

> 在每一项中都需要出现全部的变量名



* 任意两个最小项的积一定是0
* 全部最小项的和一定是1
* 每两个相邻的最小项相加,可以约去一个因子

* 最大项和最小项是相互取反的,所以,最小项是and起来,最大项是or起来



# 卡诺图

使用方格图表示所有情况的图

> 用来化简逻辑函数



> 图的边上是枚举部分元素的情况
>
> 图的格子里面填的0/1/X



卡诺圈（Karnaugh Map，简称K-Map）是用于简化布尔函数的逻辑图形工具中的一种重要概念。卡诺圈用于在卡诺图中标记一组相邻的1方格，以便更容易地识别并简化布尔函数。

以下是有关卡诺圈的重要信息：

1. **卡诺图回顾**：卡诺圈通常用于卡诺图中，而卡诺图是一个用于可视化布尔函数的二进制输入组合的矩阵。每个方格代表一个输入组合，而1方格表示函数在该输入组合下的输出值为1。

2. **卡诺圈的形状**：卡诺圈通常由相邻的1方格组成，并形成一个矩形或正方形。卡诺圈的边缘必须与卡诺图的方格边界平行，不能倾斜。

3. **卡诺圈的目的**：卡诺圈的主要目的是将布尔函数中的最小项分组在卡诺图中，以便更容易地识别和简化这些最小项。分组的最小项可以合并成更简单的布尔表达式，从而减少逻辑门的数量和电路的复杂性。

4. **合并相邻的最小项**：卡诺圈可以用来合并相邻的最小项，这些最小项具有相同的输入变量。通常，一个卡诺圈内的最小项都有相同数量的输入变量，而且只有一个输入变量的不同。合并这些最小项将减少布尔函数中的项数。

5. **卡诺圈的规则**：卡诺圈的规则包括：
   - 卡诺圈必须是2的幂次方大小，例如，2x2、4x4、8x8等。
   - 卡诺圈不能重叠，也不能包含不相邻的方格。
   - 卡诺圈可以沿着卡诺图的边缘延伸。

通过使用卡诺圈，工程师可以更轻松地进行布尔函数的最小化，提高电路的效率，并减少逻辑门的数量。这对于数字电子电路的设计和优化非常重要。



> 边角的元素和另一个边的元素可以构成卡诺圈
>
> 其实,构成卡诺圈的元素是相邻的,也就代表这些相邻元素之间只有一个0/1符号位不一样
>
> 谁变了就不要谁,只写下不变的部分
>
> 圈起来的时候需要圈起来最大的部分.

* 注意,所有的格子都要圈起来(哪怕只有他自己)



* 使用`d`表示的是无关项.可以是0也可以是1,在卡诺图中,用`X`表示(合理使用可以方便化简)

> 注意,无关项使用约束条件来表示,比如`BC = 0`(表示方式),代表所有可以使用`BC`表示的项都是无关项.
>
> * 使用约束条件,可以使得圈(可能)更大.



# 逻辑电路

logic circuit

分成

> 1. combinational 和时间无关
> 2. sequential 时序(和时间有关)



# 组合电路(combinational)



## and-or

> 使用与门和或门



当var and their complements are available,我们可以直接获得取反的时候,我们不需要考虑非门.



注意

* 与非门和非或门(negative-or)是一样的
* 同理,或非门和非与门(negative-and)是一样的



## 画电路的时候

你需要合理使用SOP和POS



注意,合理使用卡诺图可以实现电路尽可能的少使用零件.



SSI : small scale intergation 1-10

MSI 10-100

LSI 100-1000

VLSI : very large 1000-10000



## 型号

54LS138

> 第一个参数`数字`,有54/74两种
>
> 1. 54军用
> 2. 74民用
>
> 第二个参数是使用TTL/CMOS
>
> 1. LS TTL
> 2. HC CMOS



> 注意,TTL是高功耗和高速,可以空着放输入脚
>
> 注意,CMOS不可以空着输入脚,因为空的时候是默认1



## half-adder(半加器)

半加器（Half Adder）是一种基本的数字电路，用于执行二进制数的加法操作。它可以将两个单独的二进制位相加，并生成两个输出：一个是和（Sum），另一个是进位（Carry）。

半加器有两个输入位：A和B，分别代表要相加的两个二进制位。它有两个输出位：Sum（和）和Carry（进位）：

1. **和位（Sum）**：Sum位表示A和B的二进制位相加的结果。它是通过异或门（XOR gate）计算得出的，其真值表如下：

   ```
   | A | B | Sum |
   |---|---|-----|
   | 0 | 0 |  0  |
   | 0 | 1 |  1  |
   | 1 | 0 |  1  |
   | 1 | 1 |  0  |
   ```

2. **进位位（Carry）**：Carry位表示A和B的二进制位相加时是否产生进位（进位到高位）。它是通过与门（AND gate）计算得出的，其真值表如下：

   ```
   | A | B | Carry |
   |---|---|-------|
   | 0 | 0 |   0   |
   | 0 | 1 |   0   |
   | 1 | 0 |   0   |
   | 1 | 1 |   1   |
   ```

半加器非常简单，用于处理两个单独的二进制位相加。但需要注意的是，半加器只能处理当前位的进位情况，不能处理来自更高位的进位。对于多位二进制数相加，通常需要使用全加器（Full Adder）或其他更高级的加法器。

半加器是数字电路设计的基本组成部分，用于构建更复杂的数字逻辑电路和算术运算电路。


$$
C_{out} = carry~out 进位的部分
$$


## full adder

> 可以使用半加器获得全加器

> 两个半加器可以组成全加器



注意

* **C_{out}** 是与门
* 个位数的数字计算是异或门



## parallel binary adder

可以通过连接**full adder**实现



> 同一级别的位置数相加,从小一位的位置加法那边拿进位数字相加
>
> 由此可以获得多个位数的二进制数相加



> **乘法**实现,使用移位操作,错位接上去
>
> 把需要乘起来的数字用二进制表示,然后看1的位置开始移位.



> 实现`相等`的操作符,可以使用同或门逐一比较



## COMP比较器

74LS85

使用同或运算符



> 从高位到低位进行比较
>
> 当A=B的时候,结果由`cascading input`(级联输入,级联输入也是三个,和结果的意义一样)决定



> 获得的结果是三个
>
> 1. A>B
> 2. A<B
> 3. A=B



例如

使用两个比较4位的二进制数字的电路组合比较8位的二进制数字

第一个比较器的位权重应该是低一点的

把第一个比较器的结果传给第二个比较器的级联输入(cascading input)

* 作为级联输入端的第一个原件的级联输入是`0 1 0`,代表相等的时候是相等的
* 当没有进位权重的时候,我们需要枚举比较然后用逻辑电路合在一起



# 译码器

把二进制数字转换为十进制数

> 使用枚举的方式,只有在某个数字的时候,对应的一个输出端才是`1/0`
>
> 注意,这会造成每个输出端之前都需要一个`与门/与非门`.

* 比如一个`4bit`的输入元器件,我们需要使用16个输出端.
* 有一个开关一样的`CS`输入端,输入0的时候是**正常工作**的?



> 使用两个译码器,配合使用他们的`CS`端,我们可以实现一个`8BIT`的译码器



**74HC138**是一个active high decoder,是`3BIT`的

可以使用`3BIT`的构成`4BIT`的译码器

> 当最高的位置是0的时候,一定是从`0-7`,最高位是1的时候,一定是从`8-15`
>
> 所以,需要使用`CS`输入端
>
> 它的输入端high的时候工作



## outline symbol

> 用来表示数字,就和计算器上面的屏幕一样



common catnode 共阴极 

common anode 共阳极 with active LOW decoder

> 共阳极的输入端已经接好高电平了,需要一个阴极输入点亮



### BCD/7-SEG

* 47型号->低电平有效
* 48型号->高电平有效



除了四个输入端口

`LT` light test 只要他输入的时候,用来测试是否有哪个输出端坏掉,如果它有效,输出应该是8. --> 使用的时候是0.

* 有些时候我们可能加上两个非门,没有效果,但是,一个是方便添加新的功能,一个是提高经过很多门之后衰减的电压



`BI'/RBO'` 灭零(blank input/ripple blanking output)

> 当它有效的时候(一般是0的时候),如果四个输入也是全0,也就是说输出是0,我们不显示0的数字样式,不会有亮起的部分

`RBI'`级联输入,用来获取上一级(高位置)的数字的`BI'/RBO'`输出

* 当同时显示多个位数的时候,使用高位的`RBO`给低位的`RBI`输入,开始的时候是0,所以,灭0,一旦出现非0位的时候,之后的`RBO`一直都是1,不会灭0.
* 注意,整数位置的最小位一直都是1,因为我们需要显示数字0的情况

* 输出小数点之后的位置的时候,从后往前显示



当输出的范围是`1010-1111`的时候,会造成错误状态



> 有一个`E`输入端,代表开关,1的时候正常工作





## 例题

例题:使用四个2输入的译码器实现4输入的译码器

> 需要使用最高的两个位数来决定`E`端的输入内容
>
> 使用译码器可以实现把最高的两位实现分成四组的情况出现

* 多出来的高位数字是需要作为分割情况的条件的.



例题:设计一个全减器



# 型号

74LS283 加法器

74LS85 大小比较器

138 3bit8输出的译码器

154 4bit16输出的译码器

74HC42 4bit10输出的译码器

74LS**47** 7-segment BCD Driver 控制LED输出的屏幕

74LS148(148)  8输入3输出的encoder

74HC157 2输入1输出的选择器

74LS153 MUX 数据选择器,由S端(select端选择)的输入决定 4输入1输出

74HC151 数据选择器 8输入1输出





# 74HC147 IC encoder(编码器)

active low

`HPRI` :high piority 高位优先级更高的 

十进制转BCD

> 用来选多个数字的优先级的
>
> 比如,多个数字取最大的



`EI(S)` enable input

`EO(Ys)` enable output



Ys' = (I0'\*I1'...\*I7'\*S)'

> 当输入无效但是正常工作的时候,是0.
>
> 1的时候代表正常

* 注意,低电平是active


$$
Y_{ex} = [(I_{0}'+I_{1}'...+I_{7}')*S]'
$$

> 没有正常输入

* 当以上两者都是1的时候,不能正常工作
* 不可能出现两者都是0的时候



# multiplexers(data selectors)数据选择器

缩写**MUX**

* 多输入，单个输出

有两个S(select输入端),四个D(data输入端)

> S端的两个输入是二进制的表示,代表输出的值取决于哪个D端
>
> 举个例子
>
> S端的输入是01的时候,输出应该是取决于D1

74HC151(三个A端控制,8个输入)
$$
Y = D_{0}A_{0}'A_{1}'+.....
$$






* 当一个被锁定的时候,输出是无效的,但是不一定是全0



可以使用两个**8个数值的数据选择器**组成一个选择16个数值的选择器

> 最高位的数字枚举作为分类的条件,输入到enable input端
>
> 低位的数字输入到输入端



## tips

* 可以**使用D端的输入作为限制条件,保证A端的输入是几个特定的值**,(枚举的思想)
* 当A端的输入个数不够的时候,可以使用D端的输入也连接输入口实现(注意,**这个最多的个数只能欠缺一个**,因为A端口输入是和D端口输入是对应的)



# TG(传输门)

S1 = 1,S2 = 0的时候,输出的内容是1.



# 74HC153

74HC153（或74153）是一种集成电路（IC），通常被用作4-输入多路选择器/多路复用器。它具有两个4输入的多路选择器，使您能够选择其中一个输入信号并将其传递到输出。

以下是74HC153的一些关键特点和功能：

- **输入**：74HC153具有两个4输入的多路选择器，分别为A和B。每个多路选择器有4个输入引脚，用于连接待选择的信号。

- **输出**：它具有一个输出引脚（Y）和一个输出控制引脚（G/Y）。输出引脚（Y）将所选的输入信号传递到输出，而输出控制引脚（G/Y）用于控制输出的状态。

- **功能**：74HC153可以用于数据选择和多路复用。通过选择不同的输入，您可以在输出引脚上获取所需的信号。它通常用于数字电路中的数据路选择，将多个输入信号传递到单个输出。

- **工作原理**：选择器A和选择器B可以通过控制输入引脚来选择要传递到输出的信号。当G/Y引脚处于低电平时，选择器A处于活动状态，并将A端的选择信号传递到Y端。当G/Y引脚处于高电平时，选择器B处于活动状态，并将B端的选择信号传递到Y端。

74HC153是一种常见的数字电路元件，用于数据选择和多路复用任务。它可用于将多个输入信号引导到单个输出，适用于诸如多路开关、数据路选择和数字信号路由等应用。



# demultiplexers

数据分配器

* 一个输入,多个输出

有数据选择端(A端)

和**MUX**类似,用A端的输入作为一个二进制的下表来表示需要输入的端口的下标



# parity(奇数偶数校验)

根据8bit中的1的个数是奇数还是偶数来确定正确性

74LS280

> 不仅可以生成而且可以校验奇数偶数位置



# 时序图(timing diagram)



# latch(锁存器)

cross couple : 交叉连接

有两个输出端**Q Q'**


$$
Q/Q^N意思是初态\\
Q^*/Q^{N+1}意思是次态\\
S_D,R_D=0~no~change(保持状态),这个时候Q^*不会改变\\
$$

* 双稳态电路(bistable)



> SET 当S端的输入是激发态的时候
>
> RESET 当R端是激发态的时候

* 可以添加一个`EN/CLK`端(是否工作的端口).



* 使用两个**或非门**实现

* SR锁存器

> 状态方程

$$
Q^{N+1} = S + R'Q\\
RS = 0
$$

* D端锁存器

> 状态方程

$$
Q^{N+1} = D
$$





# edge-triggered flip-flops(边缘触发器)

上升沿 positive edge

下降沿 negative edge



可以配合锁存器使用,**只有在上升边/下降边**的时候才使用锁存器

* 使用**元器件边上的小三角**表示



`CP`:clock pluse



# JK触发器

* 当`S = 1,R = 1`的时候,是翻转(toggle),其他一样

> 状态方程

$$
Q^{N+1} = JQ' + K'Q
$$



# T'触发器

> 实现的是不断翻转的功能

存在是否toggle由T端决定的元器件

$$
Q^* = TQ'+T'Q
$$

* 注意,是**T'**,如果想实现从JK获得这个**T'触发器**,需要连接**T'**



# 时钟信号

可以使用**触发器**实现不断取反的元器件



# 触发器的同步和异步

同步 控制端有关

异步 控制端无关 和`CLR'(相当于S端)`和`PRE'(相当于R端)`有关

* 异步触发器的上面两个端口的输入



# 触发器的作用

1. 暂时的存储器(temporary storage)
2. 分频器(frequency division)

> 每使用一次JK触发器分频,它的频率都会慢一倍 输出频率是之前的CLK的变化频率的二分之一

3. 计数器(counter)



单稳态:astable

双稳态:bistable



# 计数器(counter)

asynchronous counter

> 是否由同一个控制

cascade 级联

decade 十进制

decade counter 十进制计数器

recycle 循环

ripple counter 纹波计数器

sequence 时序

sequential counter 时序计数器



* 使用JK触发器实现

* 有**加计数器(up counter)**,**减计数器(down counter)**.

> 当是上升沿翻转的时候,
>
> 加计数器的第二个JK触发器的`CLK`端来自上一个JK触发器的`Q'`端
>
> 减计数器的第二个JK触发器的`CLK`端来自上一个JK触发器的`Q`端

* 两个触发器之间**1个圈**是UP,**没有/有2个圈**的是DOWN.



# 取模(Decode Counter)

> 使用计数器实现,截断后面部分



可以计数0-9的叫做**BCD Decode Counter**,


$$
触发器有个统一重置线\\
从Q_1和Q_3中引出\\
\large这样1010的时候,会回0000状态
$$


* 可能出现**glitch(毛刺)**状态

* 可以计数的位数只能小于等于最大表示状态



## 异步

> 除了当前计数器的前一个计数器,还有别的方式,比如**统一控制重置的输入**控制.



## 74LS93A

分成2个部分(**部分译码 partial-decoding**)

1. 第一部分是取模2(只有一个计数器)
2. 第2部分是取模8(只有3个计数器)

* 可以是2,8,16的计数器



CLKA 控制第一个计数器

CLKB 控制第二个计数器,(如果你需要16位计数器,同时也是第二部分的第一个输入内容)

RO(1) 重置开关1号

RO(2) 重置开关2号





## 同步

> 我们输入的信号是CLK的边触发.
>
> **第一级的JK端一直是1,后面的输入端来自之前一级的输出端**,一直翻转等待激发状态



* 创造一个**对8取模**的同步的计数器的时候,我们需要把前两个的输出**与**起来作为第三个状态的输入

> 注意,第k级的输入需要前面k-1级的输出全部与起来作为输入.



### 步骤

1. 打表找到每个计数器翻转的时候的需要的状态.
2. 使用各种门实现逻辑



## 74LS163

> 是一个4位的同步计数器

* TC = 15



LOAD 并行置数

> 只要LOAD有效,会把D0,D1...传到Q0,Q1

CLR 清空

RCO ripple carry output表示最高位是否,用进位表示

> 数到15的时候,输出1

ENP,ENT enable count

> 都是激发态的时候开始计数



* CLK的级别比CLR高
* LOAD的级别比CLR低



## 73LS160

> 数到9的BCD synchronous Counter)



* TC=9

* 需要被CLK控制的是同步,不需要被CLK控制的是异步的.



# 计数器的补充概念

binary counter 使用全部的触发器,计数的个数是`2^n`个(就是达到了最大的可以取模的数字)

decode counter 使用部分计数个数



异步计时器会立刻重置状态,同步计时器需要等待下一个时钟信号

> 比如取余10,异步是从0-10,同步是0-9



* 清0是异步的,设置是同步的



# 74LS290

由一个**计算2的计数器**和**计算8的计算器**组成

存在
$$
S_{9(1)},S_{9(2)}当两个都是激发态的时候,设置9\\
R_{0(1)},R_{0(2)}当两个都是激发态的时候,设置0\\
CLK_0,CLK_1输入内容\\
使用Q_0连接CLK_1的时候,是2*5的状态计数
$$

* 输出端不能直接连在一起,需要使用与门.

* 置9端的优先级高于置0端.



# UP/DOWN (reversiable) counter

> 使用**同步**的方法

$$
J_1 = Q_1*UP+\bar Q_1*DOWN
$$



## 方法一,添加一个新的控制端UP/DOWN'

代表1的时候是UP,0的时候是DOWN.

CTEN:count enable 使能端

MAX/MIN:保持一个周期,当数到**最大值/最小值**的时候,会有作用

> 和RCO差不多,但是C的输出时长不一定是一个周期,可能是半个周期



# 题目

SR flip-flop都有约束条件

> basic S-R FF: 只有S,R输入端
>
> gated S-R FF/synchronous S-R FF: 电平触发的触发器



sequential logic ff: 时序触发器



可以使用JK触发器实现T触发器(J=K),可以使用JK触发器实现D触发器(J=K')



T触发器使用同或门实现



- **Moore型**：Moore型状态机的输出仅与当前状态有关。Moore型状态机的输出是由状态寄存器的值译码得到的。Moore型状态机的输出只能在状态转移时发生变化。
- **Mealy型**：Mealy型状态机的输出不仅与当前状态有关，还与输入信号有关。Mealy型状态机的输出是由现时的输入信号结合即将变成次态的现态编码成的输出信号。Mealy型状态机的输出可以在状态转移之前发生变化。



self-start function: 当加入错误的状态之后,能在一定的循环之后回到正常的状态里面,不会出现错误状态的死循环. 



# 使用计数器设计电路



可以通过卡诺图来设计.

1. 行列中的属性值是Q1,Q2,Q3,格子中的值是J/K值

2. 格子中的内容是用Q0,Q1,Q2表示的次态
   $$
   Q^{n+1} = Q_2Q_1
   $$





* 在最后一个数字的时候输出RCO(进位输出端)



1. drive function
2. state function
3. final function



# 计数器的级联

级联计数器,可以增大计数的范围

> 比如两个161计数器,可以实现计数16*16个数字

TC=RCO 进位端



# 题目

四位二进制计数器 terminal count 15

LD端**不需要使能端工作**

74LS160 异步的R(CLR)端**不需要等待时钟信号** LD端**需要等待**时钟信号

一个LED下面可能存在多个引脚,其中一个处于激发态就会亮灯(相当于或门),常和译码器配合使用



# 移位(shift register)

可以使用触发器实现,每来一个时钟脉冲,位数会往后走一个位置.

输出也是一个一个放出来的



* 存在循环移位的寄存器



串行/并行 输入/输出



## 串行输入

把触发器的**输入端和输出端**连起来

可以使用SR 或者 JK触发器实现(使用JK触发器实现的串行输入还可以使用J,K'端控制串行输入的部分)



## 并行输出

使用**逻辑门实现**,需要使用**D触发器**.

* 使用**与门**实现`SHIFT/LOAD'`端



### 74LS165

8位移位寄存器

* 可串行/并行输入



>  SH/LD' 移位,加载控制端
>
> SER 串行输入
>
> CLK 触发
>
> CLK INH 保持

* CLK 或者 CLK INH是高电平的时候,NO CHANGE状态



## 并行输入,并行输出

使用D触发器实现



## 双向移位寄存器

可以左移/后移

> RIGHT/LEFT': RIGHT代表向右边移动



# 半导体知识

本征半导体: 纯净具有晶体结构的半导体



晶格



N型半导体: (参杂磷)

> 多出自由电子

P型半导体: (参杂硼)

> 多出了空穴



PN结就是P型半导体和N型半导体一起做成的.

> 内电场的方向从N指向P



扩散

> P区的空穴和N区的电子复合

飘逸

> 和扩散相反的运动

* 当两者稳定的时候,中间出现**耗尽层**.



可以使用二极管实现逻辑门



## TTL

高功耗



## 三极管

- [截止区：当三极管的发射结电压小于导通电压（一般为0.5V或0.7V）时，三极管处于截止状态。此时，三极管未导通，基极电流为0，集电极电流也为0](https://bing.com/search?q=)[1](https://bing.com/search?q=)。
- [放大区：当三极管的发射结正偏，集电结反偏时，三极管处于放大状态。此时，三极管的基极电流控制集电极电流，且二者近似于线性关系。在基极加上一个小信号电流时，会引起集电极大的信号电流输出](https://bing.com/search?q=)[1](https://bing.com/search?q=)。
- [饱和区：当三极管的集电结电流增大到一定程度时，再增大基极电流，集电极电流不再增大，此时三极管进入饱和区。在饱和区，集电极电流最大，集电极和发射极之间的内阻最小，电压Uce只有0.1V~0.3V，Uce[2](https://zhuanlan.zhihu.com/p/379209495)。



## CMOS

* 输入端不可悬空



## 输入噪声容限

$$
表示输入输出的电压变化值\\
使用V_{NH}表示
$$



# 占空比(duty cycle)

$$
D = \frac{tw}{T}
$$

* tw: 脉宽

> 高电平所占总的周期时长的比例



# 方波

1. 对称的
2. 非对称的



# 施密特触发器

* 是**1/2V_DD的时候**,触发



正向的触发器的时候

>  当输入大于一个阈值的时候,输出高电平


$$
V_{T+} = \frac{1}{2} V_{DD}(1+\frac{R1}{R2})\\
V_{T-} 需要使得V_{I}' = \frac{1}{2}V_{DD}\\
V_{T-} = (1 - \frac{R1}{R2})V_{TH}
$$

> 输入电压的阈值这样求



## 叠加原理

[电路的叠加原理是在线性电路中的一个重要工具，可以帮助工程师简化复杂电路的分析过程。在一个线性电路中，若含有多个独立电源，则任意支路的电流或电压，都可以认为是电路中各个电源单独作用而其他电源不作用时，在该支路中产生的各电流分量或电压分量的代数和](https://zhuanlan.zhihu.com/p/341849918)[1](https://zhuanlan.zhihu.com/p/341849918)[2](https://zhuanlan.zhihu.com/p/483970874)[3](https://wenku.baidu.com/view/b0d98c7af9b069dc5022aaea998fcc22bdd14366.html).
$$
V_{TH} = \frac{R2}{R1+R2}V_{I} + \frac{R1}{R1+R2}V_{O}
$$


## 回差电压

$$
V = V_{T+} - V_{T-} = 2 \frac{R_1}{R_2} V_{TH}
$$



# 555定时器

1/3VDD

2/3VDD

> S,R都是触发状态的时候,输出是不确定的.
>
> 一般来说,我们不想要同时出现未定状态.



* 把输入端接到一起来.



## 需要的时间

$$
Time = R*C
$$





## 做成施密特触发器

输入端连到一起,并且,全部接入到输出端中.



低于1/3VDD的时候,输出高电平

处于1/3和2/3VDD之间的时候,是保持状态.

高于2/3VDD的时候,输出是低电平.



# 如何产生矩形波

1. 整形
2. 直接产生矩形波



# 单稳态触发器

存在**稳态,暂态**



* 长时间不改变电容两端的电压,可以认为这个电容断路.
* 当电容两端的电压发生突变的时候,会保持和突然变化的那端一样的状态.



当获得一个输入激发之后,之后需要等待重新充电电容完成结束触发状态.



# 多谐振荡器

可以对电容**充电和放电**.



为了调节两个R1,R2的值,从而调节占空比



# 复习

**或非门和与非门**是universal gate



half adder 一个位的二进制加法实现

full adder 三个二进制数的加法



parrel adder实现3x+2

> 2x的部分最低位变成1,C_in输入1



比较器级联的时候,先比较低4位,输出级联高4位.



我们现在用的一般是HPRI编码器

> $$
> Y_s' 处于激发态,正常工作但是无有效输入\\
> Y_{ex}'处于激发态,正常工作有有效输入
> $$
>
> 



153 四选一的数据选择器

* N个地址位的数据选择器支持不超过N+1个变量的布尔表达式