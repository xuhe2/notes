# 错题

`100logN is O(N). ` 正确的

`(logN)^3 is O(N).` 正确的

使用**二叉树**实现**中缀表达式**的时候,可以用来表示括号

splay的旋转操作,每一次都在使得目标值向最上方靠近(是两个两个变化的).

splay的删除,需要先进行查找操作

文件系统的输出需要**先序遍历**

空树的深度为-1

The time bound of the FIND operation in a B+ tree containing *N* numbers is *O*(log*N*), no matter what the degree of the tree is.

`key > node->keys[i]`

> - For height = 0, we can only have a single node in an AVL tree, i.e. n(0) = 1
> - For height = 1, we can have a minimum of two nodes in an AVL tree, i.e. n(1) = 2
> - Now for any height ‘h’, root will have two subtrees (left and right). Out of which one has to be of height h-1 and other of h-2. [root node excluded]
> - So, **n(h) = 1 + n(h-1) + n(h-2)** is the required recurrence relation for h>=2 [1 is added for the root node]



polynomial calculation : 多项式计算



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

以当前点的子节点作为子树的root节点的时候,子树的个数

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



# binary heap

* 注意,下标从1开始



## 性质

1. 除去底层，每一层的节点都是满的
2. 父子节点存在大小关系



一个height是h的树
$$
2^h <= 总的节点个数 <= 2^{h+1}-1
$$


## 实现

使用数组模拟(所以,我们不使用index=0的情况)



* 注意,初始化的时候,需要在第一个位置创建一个哨兵数据.

```cpp
int index = H->size+1; // 因为存在哨兵位置
```

> 我们的下标从1开始使用.
>
> 0位置是哨兵,所以循环的时候不需要判断index=0,因为哨兵小于/大于一切.



## 删除

删除操作指删除堆中最大的元素，即删除根结点。

但是如果直接删除，则变成了两个堆，难以处理。

所以不妨考虑插入操作的逆过程，设法将根结点移到最后一个结点，然后直接删掉。

然而实际上不好做，我们通常采用的方法是，把根结点和最后一个结点直接交换。

于是直接删掉（在最后一个结点处的）根结点，但是新的根结点可能不满足堆性质……

**向下调整**：在该结点的儿子中，找一个**最大/最小**的，与该结点交换，重复此过程直到底层。

可以证明，删除并向下调整后，没有其他结点不满足堆性质。

时间复杂度O(log(N))



* 需要确定**向下调整**的时候选择哪个子树调整



### 删除任意一个键值

1. decreaseKey 减少这个键值的大小,使得它成为root
2. 然后删除root



## 建树

1. 一个一个插入全部的数值



2. 开始的时候全部放到数组里面去，然后除了没有子节点的节点(**不能继续下渗的节点**)之外

,从低层不断地PercolateDown,所以,下面的子树先满足heap的性质,在向上做操作,使得整个树都满足heap性质.

* 时间复杂度O(N),**由于每个节点最多只需要向下移动一次**,线性时间(linear time complexity)



## 查询任何一个值

需要**linear time complexity**



# 选择排序(selection sort)

找到最大值/最小值,放到尾部/头部

* 时间复杂度 O(N^2)



# 冒泡排序(bubble sort)

* 时间复杂度 O(N^2)



# 插入排序(insertion sort)



```c
int tmp = r[i];
int j=i;
while(j>0 && r[j-1]>tmp){
    r[j] = r[j-1];
    j--;
}
r[j] = tmp;
```



* 时间复杂度 O(N^2)



# shell sort



hk-sort: 每隔**hk-1**构成的**子数组**进行排序使其有序



# 使用**heap**排序

* 内存是两倍的问题可以通过**共用同一个数组空间解决**,即heap删除的底部节点的数组空间用来存**排完序之后的数组的内容**

* 使用0作为下标开始点的时候,`left = 2*i + 1`



# merge sort(归并排序)

divide phase

conquer phase

* 合并的时候,如果一个子数组空了,直接把**非空的数组的值全部放到里面去**.


$$
T(N) = 2T(\frac{N}{2}) + O(N)
$$

> 所以,总的时间复杂度是O(N*log(N)) **好的时间复杂度**



## 弊端

需要使用额外的空间**tmpArray**



# 快速排序

* 相比于**归并排序**,不需要使用多余的空间



## 如何避免最坏的情况出现

> 使用`pivot = A[0]`的时候,如果原来的是已经排好序的,可能出现O(N^2)的时间复杂度

> 使用`median-of-three`方法,取**开头 中间 结尾**三个部分的值比较



* 开始的时候把KEY放到数组的末尾(如果已经排序好了三个值,那么可以不对最后的变更)

1. 使用`L,R`两个指针,指向`开头`和`结尾-1`(**不包含KEY所在的位置**)
2. 在左边找比KEY大的,在右边找比KEY小的,交换两者(**如果i>j的时候,结束当前步骤**)
3. 交换KEY和**下标i**指向的值.(就是把KEY放入正确位置)



* 最大值不参加排序



# bucket sort(桶排序)

可能浪费很大的内存空间



# radix sort(基数排序)

* 桶排序的升级版

> 基数排序的方式可以采用LSD（Least significant digital）或MSD（Most significant digital），LSD的排序方式由键值的最右边开始，而MSD则相反，由键值的最左边开始



# 算法的稳定性(stable)

相同的数字经过排序之后,相对位置不发生移动的叫做**稳定的排序算法**

反之,则是**不稳定的排序算法**.



# 图论

不是树,树不会有环.



graph : 由edge,vertices构成
$$
<v_i,v_j>指的是从v_i到v_j的边
$$


分成**有向图**和**无向图**.



## 度

一个顶点的度是和它相关联的边的个数.(无向图)

number of nodes incident to it



入度: 指向当前节点的边的个数.

出度: 从当前点作为出发点的边的个数.



## 度的结论

> 一个边贡献两个度
>
> 所以,边的个数=所有度数相加/2



## 定义

length of path : 路径上边的个数

simple path : 边不重复



## adjacent matrix(邻接矩阵)

接通的时候是1,不接通的时候是0.



图是双向的,矩阵一定是对称的

矩阵对称,图不一定是双向的.



## dense graph(稀疏图)

边的个数很少,所以,很稀疏

所以,我们使用**邻接表**



## adjacent list

使用**list**实现邻接表

> 表里面存的是指向的节点的下标



需要的空间: n个节点作为开头+边的个数的2倍



# DFS

可以使用stack来模拟

* 类似先序遍历.



# BFS



* 类似层序遍历



# 拓扑排序(topological sorting)

AOV(activity on vertex) Network

predecessor: 前驱节点

transitive 传递性

reflective 自反性



* 一个本来就是孤立的点可以被放在拓扑排序的任何地方.

* 有环的时候不可能完成拓扑排序.



# 最短路算法

使用BFS查找无权最短路的长度.



strongly connected graph: 有向边但是可以构成环

weakly connected graph: 不构成环



# spanning tree(生成树)

树是一种**无向边构成的,无环的,有一个ROOT节点,所有点都是连通的(connected)**的图





## minimum spanning tree(最小生成树)

边权加起来最小的生成树



## prim

从一个点开始拓展出去,是贪心的方法扩展边(每次拓展代价最小的边,使用**heap**实现)



* 如果有**边的权重一样**的时候,可能会出现选择不同的起始点生成不同的树.



## kruskal

使用**heap和并查集实现**



* 在运行的任何一步下,不一定当前是环



# AOE network

计算完成全部任务的最短时间

> 拓扑排序的思想,不断实现前置的任务,取得是MAX,代表需要的最短时间



计算每个任务的最晚开始时间

> 从后面往前找,取得是MIN,代表最晚开始的时间点
>
> * 需要先找最短完成时间



# greedy algorithm(贪心算法)

解决optimization function(优化方法)

* it makes best decision at each stage



greedy criterion 贪婪准则

> 有些时候,local optimum is equal to global optimum



时间安排,使得平均完成时间最短

> 使短的时间先执行



# huffman code(哈夫曼编码)

当存储在二叉树中的时候,存储一个数字需要多少位的时候,取决于这个字符存储的节点的深度



* 是一个full tree(满二叉树)

> full tree : 要么当前节点是根节点,要么是有2个孩子的



* 不存在一种编码的表示是另一种编码表示的前缀(prefix)



## 构建树的步骤

1. 先找到2个最小的frequency的部分
2. 删除原来的2个部分,构成一个新的子树
3. 循环这个步骤,直到只有一棵树

> 这个**部分**可以是单独的一个节点,也可以是一个子树.



* 每个节点要存一个权值(代表子树加起来的frequency值)



# 复习

In the [mathematical](https://en.wikipedia.org/wiki/Mathematics) field of [graph theory](https://en.wikipedia.org/wiki/Graph_theory), a **complete graph** is a [simple](https://en.wikipedia.org/wiki/Simple_graph) [undirected graph](https://en.wikipedia.org/wiki/Undirected_graph) in which every pair of distinct [vertices](https://en.wikipedia.org/wiki/Vertex_(graph_theory)) is connected by a unique [edge](https://en.wikipedia.org/wiki/Edge_(graph_theory)).



链表的插入和删除都是O(1)



infix转换为postfix的时候,需要使用stack


$$
对于树\\
第i层的最多的节点个数是2^{i-1}\\
一个depth是k的树,最多的节点个数是2^{k+1}-1
$$


二叉查找树的时间复杂度取决于树的depth,O(depth)

AVL树可以保证复杂度是O(logN)



complete tree: 除了最后一层,其他都是满的节点

full binary tree: 只有叶子节点和有两个孩子的节点(例如哈夫曼树)



二叉树的遍历,需要的空间复杂度是O(H)

> H是二叉树的高度



实现文件系统一样的打印使用的是**先序遍历**.



siblings: 兄弟节点,有共同的父亲节点



RL rotation: 是右子树的左孩子超过范围的时候,执行的操作



查找B+树的时间复杂度是O(logN)

> 不论degree是多少



建heap的方式

> 1. 基于插入的方式,O(NlogN)
> 2. 基于建树**build**的方法,O(N)



随意访问一个heap中的节点,时间复杂度是O(N).



quick sort : 最坏的情况是O(n^2)的,取决于pivot的选取

merge sort : 需要O(N)的空间  需要合并logN次



使用比较的最好的最坏情况的时间复杂度为O(logN)



使用insertion sort排序一个非降序得到非升序(n个数据)

> 比较次数: (n-1)*(n)/2
>
> 移动次数可以小于比较次数.



# 算法设计课

最大公共序列:

```python
def longestCommonSubsequence(str1, str2) -> int:
    def dp(i, j):
        # 空串的 base case
        if i == -1 or j == -1:
            return 0
        if str1[i] == str2[j]:
            # 这边找到一个 lcs 的元素，继续往前找
            return dp(i - 1, j - 1) + 1
        else:
            # 谁能让 lcs 最长，就听谁的
            return max(dp(i-1, j), dp(i, j-1))
        
    # i 和 j 初始化为最后一个索引
    return dp(len(str1)-1, len(str2)-1)

```



## 矩阵连乘



多个矩阵连乘的时候, 不同的相乘的顺序决定计算的时间

![img](https://pic1.zhimg.com/80/v2-a8c6ab2aabe2cf2f9868cf5164c0b494_720w.webp)
