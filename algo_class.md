# 错题

`100logN is O(N). ` 正确的

`(logN)^3 is O(N).` 正确的

使用**二叉树**实现**中缀表达式**的时候,可以用来表示括号

splay的旋转操作,每一次都在使得目标值向最上方靠近(是两个两个变化的).

splay的删除,需要先进行查找操作



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
* 删除的时候

> 1. 没有一个子节点的时候,删除自己
> 2. 有一个节点的时候,删除自己,把自己的子节点替换上来
> 3. 有两个子节点的时候,删除自己,用**左子树的最右节点或者右子树的最左节点**替换



* 使用**递归**的写法,返回的是当前的节点更新之后的状态.



# AVL

当一个子树存在
$$
BF(node) = height_l - height_r
$$
这个`BF(node)>1`的时候,说明这个子树是不平衡的,需要左旋或者右旋.

* 需要在节点中维护一个**代表当前节点高度**的值.



## 插入

插入一个数值

更新`BF`值,对一整个插入的路劲都进行更新

如果这个子树不是平衡的,我们需要**对当前不平衡的子树的root节点左旋/右旋**.

> 1. 右旋的话,**左节点的右子树插入到当前根节点的左节点**,左节点成为新的根节点



* 有些时候,需要先左旋然后右旋**(或者先右旋后左旋)**

> 比如左子树的右子树出现了过长的问题,需要**先在左子树做左旋**,然后在当前根节点右旋.



* RL

> 意思是right child的left subtree

RL rotate 指的是对right child的left subtree的旋转操作



1. 先和当前的节点比较,决定是去**左孩子/右孩子**
2. 和**左孩子/右孩子**比较,决定是**哪一个子树**.



## 删除操作

1. 按照二叉查找树的方式删除这个节点
2. 检查是否平衡



# splay tree(伸展树)

> 永远把最近访问的部分放在根节点(因为最近一次被访问的值很有可能被重复多次访问)



## 插入

1. 按照**二叉树**的方式插入节点
2. 更新节点

> 更新节点的时候也需要使用使用`zig-zag`,`zig-zig`,`zag-zig`的操作



## 删除

1. 查找这个节点(证明它是存在的,同时把它移到头部)
2. 使用和`二叉树`一样的方法删除它.



# B tree

有一个阶数的概念,代表一个节点最多可以有几个子节点.

a B tree of order M : M阶的B树



## 性质

1. 根节点要么是叶节点,要么有2到M的孩子
2. 所有节点(除去根节点)有`M/2向上取整`到`M`个孩子
3. 叶子是同一级深度的
4. 最后的存储是有序的



一个节点中

> s第一个值是指针,指向第一个子节点
>
> 后面由`数值和指针`组合构成,指针指向子节点,数值是指的是子节点中的最小值
>
> * 数值用来查找的时候比较	



## 插入

如果没满,直接插入到需要的位置



如果满了,那么当前的叶子节点会被记录,往上查找是否存在还能插入的节点,生成新的节点

> 新的节点也要满足子节点大于`M/2向上取整`,所以,需要切分叶子节点



## 时间复杂度

$$
M*\log_{M/2向上取整}^{N}
$$



# hash table

* 使用哈希的方法插入到一个数组中
* 每个元素有唯一的对应值



hashing function 哈希函数

`h(key)->hash table index`

collision handling strategies 哈希冲突



* hash table size 一般是素数

* 对字符串处理的时候,需要加上权重,不然先后就没有区别了



## separate chaining(哈希链式存储)

使用**链表**的方式存储**哈希值重复**的数值.



### 插入的时候

* 插入的时候,插入在**列表开头**的方式消耗的时间的复杂度是`O(1)`的.(所以,我们一般使用插入到头部)



### ASL(average search length)

$$
ASL = (C_1+...+C_n)/m
$$

* m:当前存储的数值的个数
* C_i:第i个空间存储的位置



### 查找的时候

使用了**n**次刺探代表一共比较**n+1**次



## open addressing(开放地址法)

* 当现在的数值的hash值冲突的时候,我们使用**probe(探测)**的办法,找到下一个位置.

> 比如,当冲突的时候,把**现在的hash值+1**.

linear probing 线性探测



### ASL

$$
ASL = 1/(m) \sum^{n}_{i=1}C_i
$$

m:已经插入的数值的个数

C_i:当前位置被查到的需要的刺探数量,C_i=abs(pos-H(key))



### 二次探测(quadratic probing)

$$
F(i) = i^2\\
i:第i次冲突
$$

* 插入的更加分散,效率更高.

第一次碰撞的时候,给hash index加上1

第二次加上4(就是2^2).



### 删除

删除的时候,可能会造成后面同一hash值的数值的**中断**

* 可以设置当前位置的信息为`被删除`状态.



## double hashing(双哈希)

$$
F(i) = i*hash_2(key)\\
i:第i次冲突\\
hash(i)+F(i)\\
hash(i)和hash_2(i)是不同的哈希函数
$$

* 使用两个哈希函数完成位置的查找,冲突的可能性更小.



## rehashing

当表太满的时候使用

1. 当当前的表的容量>=50%的时候,需要新的表
2. 建立一个新的表(大小是原来的2倍),把旧的表中的内容用新的哈希方法插入到新的哈希表中
