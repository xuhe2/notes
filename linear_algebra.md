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



# 向量空间 vector space

$$
R^n代表n维度的向量空间\\
使用竖着的表示
$$



一个向量空间中,不同的元素相加之后依旧在空间中,不同的元素乘以常数也是在当前的向量空间中的.**封闭性**

* 书本P131

 

## 验证一个矩阵是向量空间

1. 验证是非空子集
2. 验证满足数乘的封闭性
3. 验证满足加法的封闭性.



## 命名

{0} zero subspace

`{0} , V`是travial subspace 

除了上述两个,其他叫做`proper space`



# null space

存在使得`Ax=0`的部分
$$
N(A) = 0\\
Ax = 0的解
$$

* 可以使用矩阵的积表示



# span

Let v1, v2, ... , vn be vectors in a vector space V. A sum of the form α1v1 + α2v2 +···+ αnvn, where α1, ... , αn are scalars, is called a linear combination of v1, v2, ... , vn. The set of all linear combinations of v1, v2, ... , vn is called the span of v1, ... , vn. The span of v1, ... , vn will be denoted by Span(v1, ... , vn).

> 让 v1、v2、...、vn 代表向量空间 V 中的向量。一个以 α1v1 + α2v2 +···+ αnvn 形式的和，其中 α1、...、αn 是标量，被称为 v1、v2、...、vn 的线性组合。所有 v1、v2、...、vn 的线性组合构成的集合被称为 v1、v2、...、vn 的张成（span）。v1、v2、...、vn 的张成通常用 Span(v1, v2, ... , vn) 表示。这表示了所有可能的线性组合，其中标量可以是任意实数，它们组成了一个向量空间，该向量空间被称为 v1、v2、...、vn 的张成。



## spanning space

The set {v1, ... , vn} is a spanning set for V if and only if every vector in V can be written as a linear combination of v1, v2, ... , vn

> 这个向量空间的任何元素可以由这个
> $$
> α_1v_1 + α_2v_2 +···+ α_nv_n
> $$
> 生成出来,那么这个span叫做spanning space



* 如果**e1,e2,e3**可以使用**span**中的元素表示出来,那么就是



## 线性空间的结论

* 如果
  $$
  v_1,v_2,v_3....在向量空间中\\
  并且span(...)=V,其中的一个v_?可以使用其他元素表示\\
  那么可以使用这n-1个部分的span生成整个向量空间
  $$
  
* $$
  其中一个向量可以表示成别的n-1个向量的组合\\
  那么存在c_1v_1+c_2v_2+...c_nv_n=0\\
  并且c_1,c_2...的部分不全为0
  $$



# 线性无关

The vectors v1, v2, ... , vn in a vector space V are said to be **linearly independent(线性无关)** if
$$
c_1v_1+c_2v_2...+c_nv_n=0
$$
那么这些`c1,c2...`必须全部是0

相反,

就是**linear dependent(线性相关)**.



## 结论

 Let x1, x2, ... , xn be n vectors in Rn and let X = (x1, ... , xn). The vectors x1, x2, ... , xn will be linearly dependent if and only if X is singular



# Basis(最小生成集)

需要满足

1. v1,v2,v3...vn是线性无关的  **使用Ax=0或者行列式!=0**
2. v1,v2,...vn是生成集  **使用e1,e2,e3验证**

* 加上或减去任何一个元素,都不再是basis
* 删除一个元素之后就不是生成集了



## 结论1

$$
 If~{v_1, v_2, ... , v_n}~is~a~spanning~set~for~a~vector~space~V,\\ then~any~collection~of~m~vectors~in~V,~where~m > n,~is~linearly~dependent
$$



## 扩展结论1

> 当两个空间都是basis的时候,那么这两个空间的大小相同



* 其他结论通过书本 P160 看



# Changing Coordinates(改变表示方式,使用其他basis)

transition matrix : 转换矩阵



## 把其他basis改成e1,e2表示

$$
x = Uc
$$

U 是转换矩阵,把使用其他basis表示改成用e1,e2表示
$$
U = (u_1,u_2,...u_n)
$$




## 把用e1,e2表示的改成其他basis表示

乘上 U的逆矩阵
$$
c = U^{-1}x
$$


## 用v1,v2的表示换成u1,u2表示

$$
转换矩阵是~U^{-1}V
$$



# 扩展到其他维度

coordinate vector : 坐标向量



## 在**I**下的坐标

**I**是单位矩阵,所以,可以坐标写成
$$
[x]_I
$$


## 结论

$$
V[x]_V = U[x]_u\\
把V表示的转换为U表示\\
[x]_V = V^{-1}U[x]_U
$$

---



# 行空间,列空间

书本P174

> 如果 A 是一个 m × n 的矩阵，那么由 A 的行向量张成的 R1×n 空间被称为 A 的行空间。由 A 的列向量张成的 Rm 空间被称为 A 的列空间。
>
> 简而言之，A 的行空间包括了矩阵 A 的所有行向量张成的空间，而 A 的列空间包括了矩阵 A 的所有列向量张成的空间。这两个空间在线性代数中具有重要的性质和应用，它们帮助我们理解矩阵的结构和性质。



## 结论1

Two row equivalent matrices have the same row space

> 两个行等价的矩阵由一样的行空间
>
> > 行等价代表可以通过三个变换之后得到一样的值



# 矩阵秩(the rank of matrix)

The rank of a matrix A, denoted rank(A), is the dimension of the row space of A

> 就是basis的元素个数,就是线性空间可以张成的空间的维度



1. 使用**三个行变换**把式子变成**row echelon form**(三角形,前面位0的式子).
2. 求的非0行的个数.



## 求解basis of row space of A

1. 化成row echelon form的形式
2. 找**有非0前导元素存在的那一行**作为basis的一部分



## 结论1

A linear system Ax = b is consistent if and only if b is in the column space of A



一个线性方程组 Ax = b 是相容的，当且仅当向量 b 存在于矩阵 A 的列空间中。



## 如何求解basis of column of A

* 我们知道在求basis of row space of A的时候,我们需要把**有非零前导元素所在的那行**作为basis的一部分.(所以,别乱换行的前后顺序)



> 1. 化成row echelon form的形式
> 2. 找**有非0前导元素存在的那一列**作为basis的一部分



# 线性变换(linear transformation)

 A mapping L from a vector space V into a vector space W is said to be a linear transformation if
$$
L (αv_1 + βv_2) = αL (v_1) + βL (v_2)
$$

> 以上是同维度的线性变换



* 线性变换可以是同纬度的,也可以是不同维度的线性变换.

* 注意,都是在向量空间中操作的



## 证明

1. 先证明

$$
L(\alpha x) = \alpha L(x)
$$

2. 再证明

$$
L(x,y) = L(x) + L(y)
$$



## 结论

$$
所有从R^n到R^m的线性变换都存在一个矩阵使得可以转化过去
$$





1. 如果 L 是一个线性变换，将向量空间 V 映射到向量空间 W，那么对于 V 的零向量 0V 和 W 的零向量 0W，L 对这两个零向量的映射结果是相同的，都等于 W 的零向量，即 L(0V) = 0W。

2. 线性变换 L 具有加法和标量乘法的性质，即对于 V 中的任意向量 v1, v2, ..., vn，以及任意标量 α1, α2, ..., αn，L 对它们的线性组合的映射等于相应线性组合的映射，即 L(α1v1 + α2v2 + ... + αnvn) = α1L(v1) + α2L(v2) + ... + αnL(vn)。

3. 对于任何 V 中的向量 v，L 对其取负的映射结果等于取负后再映射的结果，即 L(-v) = -L(v)。这表示线性变换对向量的反向操作等于取负后再映射。

这些性质表明线性变换在保持线性关系方面非常重要。线性变换将向量的线性组合映射到对应线性组合的结果，同时保持零向量不变，以及负向量的映射等于取负后再映射。这些性质有助于我们理解线性代数和向量空间中的重要概念。



# 核(kernel)

**核（Kernel）**：在线性代数中，核是线性变换中的一个概念。对于线性变换L: V → W，它的核ker(L)是定义在向量空间V上的子集。核包含所有使线性变换L(v)等于零向量0W（W中的零向量）的向量v。数学上表示为：

ker(L) = {v ∈ V | L(v) = 0W }



# 像(image)

**像（Image）**：对于线性变换L: V → W，它的像L(S)是定义在向量空间W上的子集。像是线性变换L应用于子空间S中所有向量所得到的结果的集合。数学上表示为：

L(S) = {w ∈ W | w = L(v) for some v ∈ S}

这意味着像包含了所有在S中的向量经过L映射后得到的W中的向量。



# 线性变换的矩阵表示

$$
L_A(x) = Ax
$$



## 计算矩阵表示

1. 计算矩阵A

$$
A_1 = L(e_1)\\
有通解A_n = L(e_n)\\
A = (A_1,A_2,....A_n)
$$



## 使用符号表示

$$
[L(v)]_F = Ax
$$


$$
[x]_E的意思是x在E作为basis表示下的矩阵
$$



# 相似度(similarity)

$$
C = B^{-1}*A*U\\
$$



## 结论

(i) 矩阵 B 表示线性变换 L 关于基 {u1, u2} 的矩阵表示。

(ii) 矩阵 A 表示线性变换 L 关于基 {e1, e2} 的矩阵表示。

(iii) 矩阵 U 表示从基 {u1, u2} 到基 {e1, e2} 的基变换的过渡矩阵。



Let E = {v1, ... , vn} and F = {w1, ... , wn} be two ordered bases for a vector space V, and let L be a linear operator on V. Let S be the transition matrix representing the change from F to E. If A is the matrix representing L with respect to E, and B is the matrix representing L with respect to F, then 
$$
B = S^{−1}*A*S.
$$


* A和A是相似的

* A和B是相似的,B和A就是相似的

* A和B相似,B和C相似,A和C相似.

* A和B是相似的,det(A)=det(B)

* $$
  A^T~和~B^T相似
  $$

* 乘以相同的常数k,依旧是相似的.



# 伴随矩阵

2*2矩阵的伴随矩阵的计算

对角线元素互换

负对角线的元素乘以-1



# Orthogonality(正交性)



## Scalar Product

$$
if~x~=~(x_1, ... , x_n)^T\\
and~y = (y_1, ... , y_n)^T \\
,then~
x^T y = x_1y_1 + x_2y_2 +···+ x_ny_n
$$



* $$
  x^Ty = ||x||~||y||~\cos\theta
  $$

* 



### 求一个向量的模(norm)

$$
||x|| = \sqrt{x^Tx}
$$





### 计算两个向量之间的距离

the distance between x and y is **||x-y||**



## 正交的

The vectors x and y in R2 (or R3) are said to be **orthogonal** if 
$$
x^Ty = 0
$$

* 0向量是特殊的正交的向量



## scalar projection

一个向量在另一个向量上的投影



## 结论

1. N(A)和A转置的列向量是正交的



## 正交的子空间

 Two subspaces X and Y of Rn are said to be orthogonal if xT y = 0 for every x ∈ X and every y ∈ Y. If X and Y are orthogonal, we write X ⊥ Y.



## 正交补集

Y的正交补集是所有和Y正交的向量构成的集合



## range of matrix A(矩阵A的范围)

$$
R(A) = \{
y ∈ R^n | y = A x~for~some~x ∈ R^m\}
$$



* $$
  R(A^T)和N(A)是正交的
  $$

* 



# 题目

* 0向量没有basis



* 计算R(A)的时候,可以进行行变换.



# least square problem

一个m*n的矩阵,有n的rank
$$
最小方差解 = (A^T A)^{-1}A^T b
$$




# 内积

书本P254



norm of 矩阵A = A的内积的开根号

* 正交的矩阵内积是0



scalar multiple: 标量倍数


$$
a = \frac{<u,v>}{||v||} 标量投影
$$


# 正交集合(orthogonal set)

Let v1, v2, ... , vn be nonzero vectors in an inner product space V. If  vi, vj = 0 whenever i = j, then {v1, v2, ... , vn} is said to be an orthogonal set of vectors.

> 令 v1, v2, ... , vn 为内积空间 V 中的非零向量。如果每当 i = j 时 vi, vj = 0，则 {v1, v2, ... , vn} 被称为正交集 向量。

* 注意,当两个被内积的矩阵是一样的时候,才不是0



# 正交标准集合(orthonomal set)

An orthonormal set of vectors is an orthogonal set of unit vectors.

> 正交向量集是单位向量的正交集。



## 使用标准正交基快速解答

[标准正交基可以快速求出一个向量在该空间的坐标。因为标准正交基的基向量两两正交，所以一个向量在标准正交基下的坐标就是它在每个基向量上的投影长度](https://bing.com/search?q=标准正交基)[1](https://bing.com/search?q=标准正交基)[。这样，我们就可以通过计算向量在每个基向量上的投影长度来求出向量在该空间的坐标，从而快速求出向量在该空间的任意线性组合的坐标](https://bing.com/search?q=标准正交基)[1](https://bing.com/search?q=标准正交基)。



[这个式子的意思是，如果{u1, u2, … , un}是内积空间V的一个标准正交基，且v是V中的一个向量，那么v在每个基向量上的投影长度就是v在该基向量上的坐标，即ci = v, ui。这个公式可以用来计算向量在标准正交基下的坐标，从而快速求出向量在该空间的任意线性组合的坐标](https://math.stackexchange.com/questions/2434528/let-v-1-v-2-v-n-be-a-basis-for-an-inner-product-space-v-show-that-th)[1](https://math.stackexchange.com/questions/2434528/let-v-1-v-2-v-n-be-a-basis-for-an-inner-product-space-v-show-that-th)。



* 注意,当**ai*aj(i==j)**的时候,



# 正交矩阵

An n × n matrix Q is said to be an orthogonal matrix if the column vectors of Q form an orthonormal set in Rn.

> [如果一个n x n的矩阵Q的列向量在Rn中构成一个标准正交基，那么矩阵Q被称为正交矩阵](https://en.wikipedia.org/wiki/Orthogonal_matrix)[1](https://en.wikipedia.org/wiki/Orthogonal_matrix)[2](https://ocw.mit.edu/courses/res-18-011-algebra-i-student-notes-fall-2021/mit18_701f21_lect12.pdf)。



*  An n × n matrix Q is orthogonal if and only if Q^T*Q = I.



## 结论

书本P268



补充: 

1. $$
   det(Q) = det(Q^{-1})=-1或者1
   $$

2. 正交矩阵的转置也是正交矩阵

3. 2个正交矩阵的乘积也是正交矩阵

4. $$
   <Qx,Qx> = <x,x>
   $$



# the Gram–Schmidt Orthogonalization Process

1. 选取一个开始的方向,变成开始的单位向量
2. 后面的单位向量去掉在其他方法上的分量,得到新的垂直分量



# 使用线代

当一个状态到下一个状态可以由当前状态的值构成的时候,可以使用矩阵表示.



# 特征向量(eigenvector)

特征向量是指在矩阵变换下，仅发生缩放变换而不改变方向的非零向量。更具体地说，如果一个矩阵A有一个特征值λ，那么存在一个**非零向量x**，使得Ax=λx。这个向量x就是A的特征向量。特征向量在许多领域中都有广泛的应用，例如物理学、计算机科学和工程学。特征向量可以帮助我们理解矩阵的性质，例如矩阵的对角化和矩阵的行列式。如果您需要更多关于特征向量的信息，请告诉我。



## 结论

$$
A(ax) = Aax = \lambda (ax)\\
x_1,x_2是特征矩阵,那么x_1+x_2也是
$$



## 求解特征矩阵的集合

$$
(A − λI)x = 0\\
N(A - \lambda I)就是结果
$$



## 计算特征向量的步骤

1. 使用`det(A − λI)=0`求出特征值
2. 然后求特征矩阵

> 如果有自由未知量,把一个式子变成多个,例如,书本P309



## 结论

$$
\sum^{n}_{i=1} \lambda _i = \sum^{n}_{i=1}a_{ii}\\
所有\lambda的乘积等于det(A)
$$



A is nonsingular , 特征值都非0

反之,则存在0.


$$
\lambda^{-1}也是A^{-1}的特征值
$$

$$
\lambda^m也是A^m的特诊值
$$


* 如果特征值都是不相同的,那么特征向量也是线性无关的.

> [如果一个矩阵A具有k个不同的特征值λ1，λ2，…，λk，对应的特征向量为x1，x2，…，xk，则特征向量集{x1，x2，…，xk}是线性无关的](https://math.stackexchange.com/questions/29371/how-to-prove-that-eigenvectors-from-different-eigenvalues-are-linearly-independe)[1](https://math.stackexchange.com/questions/29371/how-to-prove-that-eigenvectors-from-different-eigenvalues-are-linearly-independe)[2](https://math.stackexchange.com/questions/1407353/distinct-eigenvalues-and-linearly-independent-eigenvectors)[3](https://www.statlect.com/matrix-algebra/linear-independence-of-eigenvectors)。



# 对角化(diagonalizable)

对角化的矩阵X由x1,x2,x3...xn构成,x1,x2...xn来自特征向量空间



defective : 不可对角化的





# Hermitian Matrices

$$
 A~matrix~M~is~said~to~be~Hermitian~if~M = M^H.
$$





## 共轭

[共轭复数是指两个实部相等，虚部互为相反数的复数互为共轭复数 ](https://www.zhihu.com/topic/20330050/intro)[1](https://www.zhihu.com/topic/20330050/intro)[。例如，对于一个复数z=a+bi，它的共轭复数记作zˊ=a-bi ](https://www.zhihu.com/topic/20330050/intro)[1](https://www.zhihu.com/topic/20330050/intro)[。共轭复数的实部等于原复数的实部，而虚部则是原复数虚部的相反数 ](https://www.zhihu.com/topic/20330050/intro)[2](https://baike.baidu.com/item/共轭复数/2486343)[。共轭复数在复数的除法、模长、幂等式等方面有着重要的应用 ](https://www.zhihu.com/topic/20330050/intro)[1](https://www.zhihu.com/topic/20330050/intro)。



### 对矩阵的共轭

> 对矩阵的每一个值都取共轭.



## Complex Inner Products

$$
定义\bar z^T = z^H~and~||z|| = (z^Hz)^{1/2}
$$



### 结论

![image-20231212134930845](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20231212134930845.png)



## unitary matrix

一个×n×n矩阵U是**酉矩阵（unitary matrix）**，当且仅当它的列向量在Cn[中构成一个**标准正交基（orthonormal basis）**](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)。这意味着，对于任意的i和j，U的第i列第j行的元素等于U的第j列第i[行的元素的复共轭](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)[。酉矩阵也称为**幺正矩阵（unitary operator）**](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)[。酉矩阵具有许多重要的性质，例如它们保持向量的长度不变，即它们是**保范的（norm-preserving）**](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)[。酉矩阵在量子力学中非常重要，因为它们描述了具有必须为实数的特征值的算子](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)[。在信号处理中，酉矩阵用于傅里叶分析和信号表示](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)[。酉矩阵的特征值和特征向量在分析信号和提取有意义的信息方面起着至关重要的作用](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)[。酉矩阵在线性代数和数值分析中得到了广泛的研究。它们具有明确定义的谱特性，许多数值算法（例如Lanczos算法）利用这些特性进行高效的计算](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)[。酉矩阵还出现在奇异值分解（SVD）和特征值分解等技术中。](https://en.wikipedia.org/wiki/Unitary_matrix)[1](https://en.wikipedia.org/wiki/Unitary_matrix)



* 标准正交基,同时也是Hermitian Matrices

* 可能需要施密特正交化.



#  Quadratic Forms(二次形式)





## 结论

这是一个关于二次型的定义。在这里，我们有一个二次型()=f(x)=xTAx，其中A是一个×n×n的矩阵。如果对于所有的非零向量∈x∈Rn，二次型()f(x)只取一个符号，则称()f(x)是**定符号的（definite）**。如果对于所有的非零向量∈x∈Rn，二次型()f(x)都大于零，则称()f(x)是**正定的（positive definite）**。如果对于所有的非零向量∈x∈Rn，二次型()f(x)都小于零，则称()f(x)是**负定的（negative definite）**。如果二次型()f(x)取不同符号的值，则称()f(x)是**不定符号的（indefinite）**。如果()≥0f(x)≥0，并且存在一个非零向量≠0x\\=0，使得()=0f(x)=0，则称()f(x)是**正半定的（positive semidefinite）**。如果()≤0f(x)≤0，并且存在一个非零向量≠0x\\=0，使得()=0f(x)=0，则称()f(x)[是**负半定的（negative semidefinite）**。](https://en.wikipedia.org/wiki/Quadratic_form)[1](https://en.wikipedia.org/wiki/Quadratic_form)



* 可以通过**特征值**判断是否**positive definite**.

> 一个对称矩阵A[是正定的，当且仅当它的特征值均为正数](https://www.zhihu.com/question/439383662)[1](https://www.zhihu.com/question/439383662)。另外，A的所有主子式均为正数也是判断A[正定的充分必要条件](https://www.zhihu.com/question/439383662)[1](https://www.zhihu.com/question/439383662)。希望这能帮到你。



# 复习

从右往左计算式子



两个向量之间的distance : 向量x减去向量y得到的向量的长度


$$
转化矩阵B=U^{-1}AU
$$




R(A)代表A的range



求解
$$
S^{\perp} 代表和S垂直的所有矩阵
$$



strict triangle form 严格的三角矩阵格式



使用增广矩阵可以化简矩阵

> 注意,每个行的第一个非0元都需要是1
>
> 可以使用化简之后的矩阵判断是否是有解(consistent/inconsistent)的矩阵



简化的行阶梯型矩阵(gauss jordan reduction)

> 每行的第一个非0元所在的那一列只有它一个非0元素



scalar : 标量 
$$
a_1 代表列向量\\
\vec{a_1} 代表行向量
$$


I : 是单位矩阵


$$
A B \not= B A
$$


symmetric matrix : 对称矩阵

> 在转置之后是一样的矩阵


$$
singular \\
存在AB=I=BA,如果可逆,那么B是唯一的\\
性质: (AB)^{-1} = B^{-1} A^{-1}\\
     Ax=B有且仅有一个解,当nonsingular\\
     A是row~equivalent~to~I\\
求A的逆: (A|I) 经过行变换之后成为 (I|A^{-1}) 
$$

$$
转置的性质\\
(AB)^T = B^T A^T
$$

$$
计算阶数大于3的行列式,使用展开\\
对于行列式,行和列是等价的,即det(A)=det(A^{T})\\
当行列式是上三角行列式或者下三角行列式的时候,det就等于对角线的乘积\\
$$
行列式的性质: 

1. 把一行/一列的K倍拿到矩阵外面去. 把系数K放入矩阵内部的时候,只能选择一行/一列
2. 2行相对,或者一行是另一行的倍数的时候,det等于0
3. 一行减去另一行的K倍的时候,det不变
4. det(A)=0的时候,是singular的



子空间:

> 满足**加法封闭性,数乘封闭性**

零空间:
$$
N(A) = \{x|Ax = 0\}
$$
span space : 

> 张成空间

spanning set: 

> 一组向量,通过自由线性组合可以变成新的空间



线性相关(linear dependent):

> 同理,Ax=0有非0解

* det(A)=0代表线性相关



基的变换(change of basis)

> 从U到标准基表示,使用UA



线性变换(liner transformation)

> T(u + v) = T(u) + T(v) T(cu) = cT(u)



kernel

> 在值域中,使得L(v)=0的全部v构成的空间
>
> 符号: Ker()

range

> 符号: R()



scalar product(数量积/内积):



向量之间的距离:
$$
||x-y||
$$

$$
正交的性质: x^T y = 0
$$
scalar projection(标量投影);



空间正交:

> 空间中的任意两组向量都是正交的

正交补(orthogonal complement):

> 所有和Y中所有向量正交的向量,属于正交补空间

* 求解空间A的正交补,使用0空间的求解方法



orthogonal set;

> 一个向量集合,相互都是正交的
>
> * 向量需要是非0向量
> * 可以得到他们是线性无关的

orthonormal set:

> 拥有orthogonal set的性质,并且,向量的长度都是1

orthonormal basis:



特征值eigenvalue
$$
使得Ax = \lambda x\\
即存在N(A- \lambda I)\\
$$


nontrivial solution 非0解


$$
对角矩阵D: A = XDX^{-1}
$$


