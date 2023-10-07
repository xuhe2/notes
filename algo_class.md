# 错题

`100logN is O(N). ` 正确的

`(logN)^3 is O(N).` 正确的



# 证明法

induction : 归纳

contradiction : 反证



# recursive

base case : 终止时候的基本情况



# 算法分析(algo analysis)

time complexity

space complexity



> 加减乘除,赋值都是一个基础操作.



constant 

logarithmic

linear 

log linear

quadratic

cubic

polynomial

exponential

factorial



分析的时候,需要使用time complexity



## big-oh notation

`定义`big-oh-notation : a function **T(N) =O(f(N))** if there exists n0 and c s.t. **T(N)<=c*f(N)** whenever **N>=n0** 

> 所以`f(N)`的增长率是大于`T(N)`的,可以用来表示上界,这是一种渐进分析的方式



* 注意,根据定义,当复杂度是`O(N)`的时候,复杂度是`O(N^2)`也是对的.



## omega notation

`定义`omega notation : a function **T(N) = omega(g(0))** if there exists n0 and c s.t. **T(N)  >= c*g(N)** whenever **N>=n0**



## theta notation

当一个函数同时满足big-oh和omega的时候,它是thetanotation.



## little-oh notation

当increasing rate is less than the T(N)



# 空间复杂度

取决于变量的多少

* 在旧的机子上面存在一位的INT,就有不同的系数项



# list



可以使用`array`简单实现

> 优点 : 可以O(1)访问数组其中的内容



## 双向链表double circularly linked list



polynomial 多项式



coefficient 系数

exponent 



# LIFO

last in first out



* 栈

> 可以解决匹配`括号是否闭合`的问题,比如,在检查代码中



使用计算器的时候,如何检测运算的先后顺序

> 使用postfix expression,不使用infix expression
>
> infix expression : 1 + 2
>
> postfix expression : 1 2 +



* 在带`()`的计算器的时候

> 在出现`)`的时候,立刻pop直到`(`的全部内容,因为,括号里面的内容的权重很高
>
> 其他都一样



* 出现`^`的时候,需要不随意切分组



# FiFO

第一个进第一个出去
