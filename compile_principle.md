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