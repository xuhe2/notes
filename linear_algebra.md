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



# 矩阵的秩

当矩阵是n*n的时候,`n*`的矩阵叫做`n阶子式`.
