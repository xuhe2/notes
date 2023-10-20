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



# 使用边的概念实现链表

`next`是一个`int`类型,含义是下一个参数的在数组中的index



# tree

> 可以同时是父节点和子节点



* 至多n-1个数地边
* 子树不能相互连接
* 子节点的个数可以不唯一,父节点的个数必须<=1
* 不能跨级连边



## degree

以当前点的子节点作为子树的root节点的时候,字数的个数

* 取决于子节点的多少



## leaf node

叶子节点



## path

从一个节点到另一个节点的路径是唯一的.



## depth

从root node到当前节点的需要的边的个数



## height

从当前节点到叶节点可以走的最长的边的个数 

the length of the longest path from now node to a leaf



* height of tree = height(root node) = depth(deepest node)



## element

有两个内容,FirstChild和NextSibling

* FirstChild : 指向下一级的子节点的第一个
* NextSibling : 指向同级的兄弟节点



## tree traversal

preorder : 先序遍历

postorder : 后序遍历



## 结论

$$
n_0 = n_2 + 1\\
证明：\\
n_0是没有子节点的节点个数，其他同理\\
n = n_0 + n_1 + n_2\\
边的个数 = n - 1\\
2*n_2 + n_1 = n - 1\\
代入证明成功
$$



* 你可以使用计算式子的后缀表达式构建出一个树



## binary search tree

* 插入的时候,如果出现空的下一个访问的节点,那么这个空的下一个节点就是我们需要插入的位置.
* 删除的时候,
