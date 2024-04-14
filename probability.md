# 样本空间 sample space

* 是一个集合
* 可能出现的全部情况的集合



* 可能有多个的样本空间对于同一类情况



## 大数量的样本空间

use statement or rule

`S = {x|x is a city with population more than 1000000}`



# 事件 event

例如，

骰子的值可以被3整除

event A is {3,6}



* 事件空间是样本空间的子集



* 两个特殊集合,空集(代表不可能发生),全集(代表一定发生)



* 非负性



complement 补集

intersection 交集

disjoint 没有相关元素的



# permutation

排列



# combination

$$
C_{r}^{n} = \frac{n!}{(n-r)!r!}
$$



# frequency and proability

频率的可能性取决于实验

* 实验的次数足够多的时候, 频率会稳定到概率



多余多个有交集的事件使用**容斥**



# a partition of S

一些事件交集为空,并集是S全集,那么就是S的划分

* mutually exclusive
* union is S



# 条件概率

P(A|D) 指的是在D条件下
$$
\frac{P(AD)}{P(D)}
$$
就是结果

* 条件概率和原来的概率可能相等



## 独立

如果`P(B|A)=P(B)`,那么他们是independent

独立的时候, `P(AB) = P(A)P(B)`,`P(A'B) = P(A')P(B)`



# multiplicative rules

`P(A∩B) =P(A)P(B|A)`



如果A,B是独立的, 那么`P(A∩B) = P(A)P(B|A) = P(A)P(B)`

* 必然事件和其他事件也是独立的



`P(A1∩A2∩A3∩ ∩Ak)=P(A1)P(A2|A1)P(A3|A1∩A2)...P(Ak|A1∩A2∩A3∩ ∩Ak−1)`



# random variable

每种情况对应的值的内容

M代表match variable



# probability mass function

(x,p(x))是一个函数

> P(x)>=0
>
> 全部的加一起为1



* p(x)是离散分布的内容, 加起来是1



# cumulative function/distribution

随机变量小于等于某个数的概率



`F(x) = P(X <= x)`

* 当出现x是不合理(不会出现的值)的时候, P(x)为0



把一个一个分段的函数部分写成**左闭合右开放**的分段函数, p(x)



## 概率密度函数



使用图表示的时候, P(...) = 阴影面积, 所以叫做**概率密度函数(probability density function)** 代表f(x), **f(x)积分的累计结果是F(x)**

> 全部面积相加等于1
>
> 面积表示落在这里的可能性



* 对于所有x, 概率密度非负
* 全部相加, 概率是1
* 在一个范围内做积分的结果是这个范围内出现的概率



## continuous proability distribution

continuous proability distribution不可以使用离散的方式表达, 并且在单点上的概率可能是0

* 对于**连续性的**, 单点是没有意义的, 所以`P(a<x<b) = P(a<=x<=b)`, 这点对非连续性是无效的
* 不可以使用bar table form(离散方法)表示



# 多维度的(joint probability function)

P(X=x, Y=y)

* 和一维的一样对待



# marginal distribution(边缘分布)

对于一个有多个变量的概率函数, 当我们只想考虑**一个变量**的时候
$$
p_{x}(x) = \sum_{y}p(x,y)\\
指的是x单变量的概率密度函数,p(x,y)是双变量的概率密度函数
$$

> 想知道x的边缘密度函数, 把y**包含全部范围**考虑



鉴于**multiplicative rules**, 我们得出
$$
P(X=x|Y=y) = \frac{p(x,y)}{p_y(y)}
$$


鉴于**两者独立关系**, 得出
$$
P(X=x,Y=y) = p(x)p(y)
$$


对于static independent的函数

我们需要检查是否存在
$$
p(x,y) = p(x)*p(y)
$$

* 对于**多个随机变量**都是独立的, `p(x,y,z)=p(x)p(y)p(z)`



# 数学期望

数学期望, 使用**数值X期望概率**的总和(对于**离散型**的)

对于**非离散型**的, 把加法换成积分, 使用
$$
\int_{a}^{b}x*f(x) dx
$$
如果计算函数g(x)的期望, 那么
$$
\int_{a}^{b}g(x)*f(x) dx
$$

> 把x换成g(x)



![image-20240402143719667](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240402143719667.png)



* 数学期望不基于实验

* 平均值是基于实验的



求E(g(x,y))的时候, 使用二重积分



对于有两个变量x,y的式子, 只求x的期望

> 可以在二重积分的时候, 把y的范围设置为无穷
>
> 或者先获得x的期望函数



## 转换公式

$$
E(aX+b) = a*E(X) + b\\
E(g(x)+h(x)) = E(g(x)) + E(h(x))对于加减运算不破坏
$$







对于2个参数, 并且这二者是独立的
$$
E(XY) = E(X)*E(Y)
$$
因为存在
$$
f(x,y) = f_x(x)*f_y(y)带入E(XY)的式子可以分出E(X)E(Y)
$$


## 方差 variance

$$
Var(X) = E((X-x的均值)^2)
$$

也可以使用
$$
E(X^2)-(E(X))^2\\
X^2的期望减去X的期望的平方
$$




## 标准差 standard deviation

对方差开根号, 然后取正数的部分.



## Covariance 协方差矩阵

$$
Con(X,Y) = E(g(X,Y))\\
其中g(X,Y) = (X-\mu X)(Y-\mu Y)\\
可以使用Con(X,Y) = E(XY) - E(X)E(Y)
$$



* 可以是负数



如果大的X经常导致大的Y, 小的X经常导致小的Y, 那么
$$
(X - \mu X)(Y - \mu Y)往往是正数;反之, 往往是负数.
$$


* 当X,Y是独立的时候, Cov(X,Y)是0, 因为`E(X,Y) = E(X)E(Y)`.



对于`E[(X-1)^2]`可以使用解方程的方式, 分解成`E(X^2) - 2E(X) +1`结果也是一样的.
