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