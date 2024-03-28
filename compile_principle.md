自然语言

形式定义(使用**正则表达式**)

> 正则表示不是万能的
>
> 比如,一个中间对称的字符串不能被正则表达式显示

> 使用**上下文无关语法**CFG
>
> 可以表达expression



正则表达式->model->优化model->code



# 自动机 automator

自动检查构建代码(简化代码)



# 汇编器 assembler

从汇编到机器码

* 和编译器不同



# 结构

1. scanner
2. parser
3. semantic analyzer
4. source code optimizer 
5. code generator
6. target code optimizer



## scanner

lexical analysis 

输入stream of character, 输出tokens



例如

```
a[index] = 4 + 2
a,[,index,],=,4,+,2
```



## parser

determine the structure of program



会构建一个syntax tree, 检查代码是否正确

发现语句是什么类型



## semantic analyzer

检查语义是否正确

* 单句代码不出错, 上下文会出错(例如**类型检查**)



## source code optimizer

优化源代码阶段



## target code optimizer

优化汇编代码

> 改变快慢指令
>
> 使用不同的寻址模式



# other issues in compiler structre

1. analysis and synthesis(综合)

> analysis: 分析代码, 检查合法性, 语义检查/优化
>
> > lexical analysis, syntax analysis, semantic analysis(optimization)
>
> synthesis: code generation(optimization)

2. front end and back end

> 前端关于**source code**, 后端关于**target code**

3. passes

> 需要扫描几遍文件代码, 使得其可以作为target code

* 常见的有**one pass**,**three passes**



# 错题

`X1[Y2]=-2.13;`一共有7个

* `-2.13`是一个token
* `;`也是一个token
* 字面量是一个token



* 空格不算token



# scanning

分成`regular expression`和`finite automata`

> `finite automata`用来识别`regular expression`



一个scanner需要表达token的许多属性

> 类型
>
> 名字
>
> 值



## regular expression

r: regular expression

L(r): language of regular expression 这是一个集合



三种运算

concatenation 把二者连接起来

> `ab`的`L(r)`是{ab}

choice 或运算

> `a | b`的`L(r)`是{a,b}

* 在表达式中不能使用`|`, 需要转义

kleene closure 可以重复任意次
$$
\varepsilon 代表空字符串
$$

> `a*`代表a可以出现任意次, 为{空字符串,a,aa....}



例如

> s1={aa,b}, s2={a,bb}
>
> s1s2={aaa,aabb,ba,bbb}

* 会自动去重

* 有先后顺序的关系



`L(r*) = L(r)*`



* 不可以实现计数效果,比如b左边的a的个数等于右边的a的个数

  > 但是,a的个数是偶数是可以实现的,因为`aa`作为一个最小的元素

* L(r)应该是全集, 在尾部添加特殊情况, 排除一些空串的情况



## 运算优先级

`()`>`*`>`concatentation`>`|`



## legal symbol

$$
\sum指的是legal~symbol, 叫做alphabet
$$

最基本的符号的集合

所有的表达式需要使用这些构成(可以重复)



## 正则的符号

`+`代表至少一个

`.`代表任意字符

`[0-9]`代表字符范围

`~`代表排除以下可能

`?`可选可不选



* 保留字是固定写着的



## 需要处理的

ambiguity

white space: 包括空格,TAB,回车,注释

lookahead



## finite automata

获取输入的时候, 执行步骤的状态机



transition: 转换, 有标签的箭头线

state: 状态, 用圆圈构成

start state: 启动状态, 是一个没有标签的箭头线指向的圆圈

accepting state: 接受状态, 进入这个状态代表当前字符串就是我要找的, 用双重圆圈组成

> 如果被传入的字符没有transition可以进入, **即使已经进入accepting state, 也是一个error**



* 用来verify的



## DFA(deterministic finite automation)

有限自动机

M: machine 

M由alphabet组成, 一些状态集合S, 开始于s0(某个状态), 一些接受状态A(是S的子集), 有transition function(从一个集合映射到另一个集合) 



* 组合多个自动机可以成为一个新的自动机, 同时拥有两个自动机的原先的功能, 

  > 在多个自动机前面公用一个start state
  >
  > 



* 任何的DFA可以变成code



## NFA(nondeterministic finite automation)

不确定自动机



多个自动机组成新的自动机的时候, 可能出现同一个时间段出现相同的`transition`, 这个时候下一个状态就是不确定的

> `lookahead`: 直接检查更长的输入内容, 检查下一个会被输入的内容
>
> `backtracking`: 穷尽的方式(深搜回溯)

* 任何一个`NFA`可以变成`DFA`.

> 把同一个时间的相同操作合并成一个
>
> * 注意, 不相同的状态是不能合并的, 比如`accepting state`不能和普通state合并, 需要新建, 保持等级统一

$$
使用\varepsilon表示无操作也可以转换过去, 空操作, 使用\varepsilon来新建一个操作
$$



# 汤姆森构造 thompson's construction

使用直接列出一个一个NFA

* 适合机器
* 拆分成一个一个字符, 然后使用`concatenation`连接多个字符, 比如`ab`使用`a`和`b`来concatenation起来作为一个`ab`



# concatenation 

连接不同的自动机, 从上一个自动机的**accepting state**状态使用一个
$$
\varepsilon
$$
连接到另一个自动机的**start state**



# choice

开始**start state**使用多个
$$
\varepsilon
$$
作为每个原来的**start state**, 结尾部分公用一个**accepting state**, 所以原来的**accepting state**作为普通state, 使用
$$
\varepsilon
$$
连接到公用的**accepting state**



# 闭包

合并全部的
$$
\varepsilon
$$
, 使得全部可以到达的state作为一个state



# 从NFA到DFA(subset construction)

* DFA的下一个状态是唯一确定的



需要尽可能精简代码



使用**subset construction**算法实现, 转换之后也需要实现`start state`和`accepting state`



## 要求

去掉epsilon, **使用epsilon closure**

* 存在epsilon的话就是NFA

去除从一个single input character可以到达的multiple state





## epsilon closure

一个状态通过epsilon转换(线)可以到达的状态
$$
\bar1 = {1,2,4}~状态1通过\varepsilon线可以到达的state\\
多状态的闭包
$$
上面的state 1被消除epsilon closure之后, 这个状态会变成{1,2,4}

假设{1,2,4}经过一个`a`转换步骤之后会变成3, 3的epsilon closure是{2,3,4}, 那么下一个状态是{2,3,4}, 然后对{2,3,4}每个状态找epsilon closure



* 转换为DFA之后的accepting state指的是当前状态下包含**原先状态的accepting state**的状态都是**新的accepting state**.



## 最小化DFA

状态数最小的DFA就是最小化的, 合并状态



使用transition检查不同的state是否可以合并, 当不同的state有不同的transition的时候, 明显是不可以合并的



# parsing

需要执行**syntax analysis**任务



CFG: content-free grammars

3型文法和2型文法, 2型支持递归

the rules of CFG is recursive



实现递归使用**parse tree**



BNF(巴克斯范式) (作为grammar rules):

 `exp->exp op exp|(exp)|number` 

`op->+|-|*`

> number作为终结符, 其他是非终结符



nonterminal: 

terminal: 使用token组成, 用来terminal derivation



## 编译过程

tokens经过parser成为syntax tree

* 如果在编译中出现了错误



token使用写好的关键字, 或者使用`regular expression`表示

meta symbol: `->`,`|`   (只有这两个符号有特殊含义)



`sentence -> id = exp| if exp sentence`

有2种语句写法

> id是正则式

> 在sentence种嵌套sentence, 实现递归



## derivation

是a sequence of replacement, 使用grammar rules的右边替换single structure name

不断地替换, 从`begins with a single structure name`到`end with a string of token`



* language指的是经过**derivation**之后, 得到的所有可以得到地字符串, 使用符号`L(G)`.



使用grammar rules可以定义一个language



* 一个grammar可以有多个式子(rules)

只有一个start symbol, 所有的转换从`start symbol`开始



为什么巴克斯范式可以表示比regular expression多的内容

> 比如`E->(E)|E`, 可以表示出**左边和右边有一样多的括号数的表达式**, 可以count



* 任何的**左递归/右递归**可以写成正则表达式



* 不同推导顺序推出的式子一样, 那就是没有二义性的



## parse tree

可以从`syntax tree`转换为`abstract syntax tree`, 简化树的样子



1. start symbol作为root node
2. 中间的节点可以是nonterminal, leaf node is terminal



推导过程(和构建树的过程一样):

> 选中哪个nonterminal被替换, 被哪个替换 (使用**leftmost derivation**, 从最左边的nonterminal开始) (使用不同的推导顺序, 如果推出的式子一样, 那么是没有二义性的)



* 转换为`abstract syntax tree`需要减少node



## precedence and associativity(优先级和相关性)

grammar rules的从上到下的顺序可以表示优先级

`a*(b*c)`和`(a*b)*c`表示的式子结果一样, 但是表达不同



formal definition of CFG: 上下文无关语法的标准定义