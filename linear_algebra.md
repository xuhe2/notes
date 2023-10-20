# equation system

`定义`如果两个equation system has same solution set , they are equivalent.

I. The order in which any two equations are written may be interchanged. 

II. Both sides of an equation may be multiplied by the same nonzero real number.

 III. A multiple of one equation may be added to (or subtracted from) another.



# n*n system

`定义`strict triangle form:, in the kth equation, the coefficients of the first k − 1 variables are all zero and the coefficient of xk is nonzero (k = 1, ... , n).

> 上述的方式更加好找结果
>
> 使用后面的值带入上面的算式,可以求出结果.



如果矩阵是`n*n`的,那么它是square



对于矩阵

`定义`pivot:第一行第一列的元素

`定义`:pivotal row:第一行



## 消元矩阵

接下来就该回代（back substitution）了，这时我们在矩阵后面加上向量写成增广矩阵（augmented matrix）的形式



* 注意,我们需要第n步的行的前n-1个元素是nonzero的,如果不是,需要交换

* 一个n*n的消元矩阵需要运行n-1步.



## Row Echelon Form

In Section 1.1 we learned a method for reducing an n × n linear system to strict triangular form. However, this method will fail if, at any stage of the reduction process, all the possible choices for a pivot element in a given column are 0.

> 比如,迭代的时候发现不能找到需要的nonzero位置,迭代结束.



`定义`A matrix is said to be in row echelon form if (i) The first nonzero entry in each nonzero row is 1. (ii) If row k does not consist entirely of zeros, the number of leading zero entries in row k + 1 is greater than the number of leading zero entries in row k. (iii) If there are rows  whose entries are all zero, they are below the rows having nonzero entries.



`定义`The process of using row operations I, II, and III to transform a linear system into one whose augmented matrix is in row echelon form is called Gaussian elimination.



* 如果一个矩阵满足不存在全0的行的结果不是0的,那么它是consistent

* 一个矩阵如果是有结果的,并且它满足`strict triangular form`,那么结果是唯一的.



`定义`A linear system is said to be overdetermined if there are more equations than unknowns. Overdetermined systems are usually (but not always) inconsistent

`定义`A system of m linear equations in n unknowns is said to be underdetermined if there are fewer equations than unknowns (m < n)



`定义`A matrix is said to be in reduced row echelon form if (i) The matrix is in row echelon form. (ii) The first nonzero entry in each row is the only nonzero entry in its column

> 使用这种方法可以直接使用未使用的部分移到右边实现整体代换,也叫行最简矩阵



# 矩阵

the entity aij(第i行第j个的元素)叫做scalar



> 使用列向的矩阵很容易表示结果的值

`定义`The set of all n × 1 matrices of real numbers is called `Euclidean n-space` and is usually denoted by Rn



* 行的矩阵叫做 row vector
* 列的矩阵是column vector



## 相等的情况

> 当两个矩阵的大小和里面的元素都一一对应相等的时候,是相等的



## 一个数字对矩阵做乘法

> 里面全部的数字都需要和这个数字k相乘



## 矩阵运算

加法/加法 : 都是简单的一一对应运算



## 全0矩阵

使用`0`表示



## 矩阵乘法

`A*B = C`

* 结果矩阵的行数取决于A的行数,列数取决于B的列数

* 注意,矩阵乘法不能满足交换律



当你的2个矩阵相乘的时候



## 判断是否有解

Consistency Theorem for Linear Systems A linear system Ax = b is consistent if and only if b can be written as a linear combination of the column vectors of A

简化成这个形式查看是否有解



## 矩阵转置

> 沿对角线转换



`定义`一个矩阵如果是n*n,并且转置之后和之前都是一样的,叫做 symmetric



### 转置的运算规则

1. (AT ) T = A 
2. (αA) T = αAT 
3. (A + B) T = AT + BT 
4. (AB) T = BT AT



## rules

书本P63



## 矩阵的幂

把同一个矩阵对自己多次执行矩阵乘法

> 可以用来表示一个转移状态的参数,多次矩阵乘法之后,这个矩阵会趋向于稳定



> 例题 书本P66



## identity matrix(单位矩阵)

单位矩阵（Identity Matrix），通常用符号 "I" 表示，是一个特殊的方阵，其特点是主对角线上的元素都是1，而其他元素都是0。单位矩阵在线性代数和矩阵运算中起着重要的作用，类似于数字中的乘法单位元（1）。单位矩阵的大小可以是任意的，但通常用 "n×n" 表示，其中 "n" 是矩阵的阶数。



## 矩阵的逆

逆矩阵是线性代数中的一个重要概念。一个方阵（即行数和列数相等的矩阵）A 的逆矩阵，通常表示为 A^(-1)，具有以下性质：当矩阵 A 与其逆矩阵 A^(-1) 相乘时，结果是一个单位矩阵（Identity Matrix，通常表示为 I）。

数学上，对于一个可逆的方阵 A，满足以下条件：

A * A^(-1) = A^(-1) * A = I

其中，A 是原矩阵，A^(-1) 是逆矩阵，I 是单位矩阵。



* (AB)^-1 = B^-1 A^-1



`定义`An n × n matrix A is said to be nonsingular or invertible if there exists a matrix B such that AB = BA = I. The matrix B is said to be a multiplicative inverse of A.



## singular matrix

> 不能进行逆运算的矩阵



# 初等矩阵elementary matrix

1. premultiplying 左乘 

premultiplying A by E `EA`

2. postmultipying 右乘

3. 乘起来的矩阵,就是把当前行/列



## 交换行列

左乘是和行有关的操作

右乘是和列有关的操作



> if E is a elementary matrix , E is nonsingular , 那么E的逆矩阵一定是同大小的初等矩阵



## row equivalent(行等价)

A matrix B is row equivalent to a matrix A if there exists a finite sequence E1, E2, ... , Ek of elementary matrices such that  B可以通过有限次的变换之后得到



## 求逆矩阵

> if A is nonsingular , then A is row equivalent to I and hence 
> $$
> E_1*E_2...E_3*A~=~I
> $$
> 



* 使用行阶梯型的操作

> 把矩阵A变成矩阵I
>
> 同步在I矩阵执行一样的操作就可以得到A



## 结论

当A是n*n的矩阵的时候,以下是一样的

1. A is nonsingular
2. `Ax = 0`只有一个解`x = 0`

> 因为`0*A的逆矩阵`是`0`,`A*X*A`的逆矩阵是`x`
>
> `x=0`成立

3. A矩阵 is row equivalent to I矩阵



# 三角矩阵(triangle matrix)

An n×n matrix A is said to be upper triangular if aij = 0 for i > j and lower triangular if aij = 0 for i < j. Also, A is said to be triangular if it is either upper triangular or lower triangular. For example, the 3 × 3 matrices



上三角矩阵(upper matrix) : 左下角都是0的矩阵

下三角矩阵(lower matrix) : 右上角都是0的矩阵



# partitioned matrix(分块矩阵)

把一个矩阵分成多个小部分

组成矩阵的是一个一个小的矩阵



例如

分块计算矩阵的行/列,然后合并在一起



# outer product expansion(外积)



# the determinant of a matrix

> 主对角线的乘积 - 反对角线的乘积
>
> 当不为0的时候,是nonsingular

Case 1. 1 × 1 Matrices If A = (a) is a 1 × 1 matrix, then A will have a multiplicative inverse if and only if a = 0. Thus, if we define det(A) = a then A will be nonsingular if and only if det(A) = 0.

如果是2*2的矩阵
$$
det(a) = a_{11}*a_{22}-a_{12}*a_{21}
$$

* 注意，首先需要

$$
a_{11}\neq0
$$

* 注意,当行列的个数大于2的时候,你需要比较全部的对角线

比如
$$
a_{11}a_{22}a_{33} − a_{11}a_{32}a_{23} − a_{12}a_{21}a_{33} + a_{12}a_{31}a_{23}  + a_{13}a_{21}a_{32} − a_{13}a_{31}a_{22} \neq 0
$$

* 注意,对角线法则

  > 你需要每一项都是相同的元素个数,如果一个对角线的元素个数少了,需要去另一个三角形中获取可以补全的对角线然后相乘



`定义`
$$
Let~A = (a_{ij})~be~an~n × n~matrix\\
and~let~M_{ij}~denote~the~(n − 1) × (n − 1)~matrix~obtained~from~A~by~deleting~the~row~and~column~containing~a_{ij}.\\
The~determinant~of
~M_{ij}~is~called~the~minor(余子式)~of~a_{ij}.\\
We~define~the~cofactor(代数余子式)~A_{ij}~of~a_{ij}~b
$$

> 删除`a_{ij}`对应的行列,剩下的合在一起就是`M_{ij}`.

* 我们可以使用这种写法实现求`det(A)`
* 注意,我们去找0越多的行进行上述操作最好



## 结论

If A is an n × n matrix, then det(AT ) = det(A)

>  `det(矩阵的转置) = det(矩阵本身)`



 If A is an n × n triangular matrix, then the determinant of A equals the product of the diagonal elements of A.

> 对角线矩阵的det等于对角线相乘

对角线矩阵例如

1 2 3

0 1 1

0 0 1



If A has a row or column consisting entirely of zeros, then det(A) = 0.

> 如果一个矩阵的行或列是全0的,那么它的det是0



 If A has two identical rows or two identical columns, then det(A) = 0.

如果矩阵 A 具有两个相同的行或两个相同的列，那么它的行列式（det(A)）等于零。这是线性代数中关于行列式的一个基本性质。这个性质对于判断矩阵的奇异性以及理解矩阵的可逆性非常重要。

以下是这个性质的解释：

1. **相同的行**：如果矩阵 A 具有两个相同的行，意味着至少有一行可以表示为另一行的线性组合。换句话说，这些行是线性相关的。在计算矩阵行列式时，其中一个步骤涉及形成行的线性组合。如果两行是相同的，那么行列式计算将包括一个具有全部零元素的行。当这种情况发生时，矩阵的行列式值将确保为零。

2. **相同的列**：类似地，如果矩阵 A 具有两个相同的列，意味着至少有一列可以表示为另一列的线性组合，表示列之间存在线性相关性。在行列式计算中，其中一个步骤涉及形成列的线性组合。如果两列是相同的，行列式计算将包括一个具有全部零元素的列，从而导致行列式值为零。

举个例子，考虑以下具有两个相同行的矩阵 A：

```
A = | 1  2  3 |
    | 4  5  6 |
    | 1  2  3 |
```

在这种情况下，第三行与第一行相同。计算矩阵 A 的行列式时，它将涉及一个具有全部零元素的行（即第一行与第三行之间的差异），从而导致 det(A) = 0。

这个性质在线性代数的各种应用中非常有价值，例如解线性方程组、确定矩阵的秩以及分析矩阵的可逆性。如果方阵的行列式为零，这表明矩阵是奇异的，没有逆矩阵。



# properties of deteminant

* 可以按照行来展开，也可以按照列来展开
* 注意，以下对行的操作也适用于列



## 结论1

Two rows of A are interchanged.

det(A) = - det(A)

> 交换任意两行或者列的,符号会变换.



## 结论2 

全部乘以一个值,可以把这个值提到矩阵的外面



## 结论3

1. 当矩阵 A 中的某一行的倍数（c倍）被加到另一行时，我们得到了一个新的矩阵 E。矩阵 E 是通过对单位矩阵 I（所有对角线上的元素都为1，其余为0）应用类型 III 的初等矩阵操作而形成的，其中类型 III 的操作是将第 i 行的 c 倍加到第 j 行上。

2. 让 det(EA) 表示矩阵 EA 的行列式。由于初等矩阵 E 是上三角矩阵（除对角线以下的元素全为0）且其对角线上的元素都是1，因此根据上三角矩阵的性质，它的行列式 det(E) 等于1。

3. 我们将展示 det(EA) = det(A)。这意味着矩阵 E 的行列式与矩阵 A 的行列式相等。换句话说，对矩阵 EA 应用初等矩阵操作不改变其行列式的值。

4. 进一步地，我们可以看到 det(EA) = det(E) det(A)，这是行列式的性质之一。因为 det(E) = 1，所以我们得到 det(EA) = det(A)。

总结起来，这段文字描述了一个关于矩阵操作和矩阵行列式的性质，特别是在矩阵的行列式计算中，如果一个初等矩阵是通过类型 III 的操作构建的，那么它的行列式等于1。并且，对矩阵 EA 应用这种初等矩阵操作不会改变其行列式的值，即 det(EA) = det(A)。这个性质在线性代数和矩阵计算中具有重要作用。



## 对于反对称行列式

> 指的是`aij = -aji`的行列式
>
> 1. 先转置,然后对于每一行都提取一个**-1**出来,相当于是取反,所以,和转置前一样
> 2. 我们得到`(-1)^N*Dn = Dn`,在`n is odd`的时候,是0.



## 分块行列式的计算的结论

按照原来的计算规则计算所得

A 0

0 B 

计算可以得到**det(A)*det(B)**



## 升阶法

把原来的行列式加上一行和一列

当你加上的**一列或者一行**



# 矩阵的秩

当矩阵是n*n的时候,`n*`的矩阵叫做`n阶子式`.
