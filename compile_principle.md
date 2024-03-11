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

start state: 启动状态, 是一个没有标签的箭头线