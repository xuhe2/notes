# python

## 类型

### 定义一个变量

* 不需要定义类型
* python的变量是没有类型的

> 使用type()查看变量的类型

```pyth
print(type(var))
```

### 类型转换

```pyth
a=123;
a_str=str(a);
a_int=int(a_str);
a_float=float(a_str);
```

> 浮点数在转换为整数的时候会丢失小数部分

## 运算符

`//` 整除

`/` 是浮点数的运算

`**` 指数运算

## 字符串

```pytho
print(f"name = {var-name}");  #也可以实现占位
```



> 单引号`''` 可以,双引号`""` 可以,三个双引号`""" """` 也可以.

> 可以使用转移字符`\` 来去掉引号的效用

`%s` 占位符

```python
name = "%s%s" %(name,num);  //实现string和int类型的相加
```

## 精度控制

`m.n` m是宽度(当m小于数字位数的时候不生效);n是小数的个数.

> 11.35是五个宽度.

`%m.nf` 来输出.

## 输入

```python
name = input();
#OK
name = input("请输入");
#先输出话然后再读取
```

* `input()` 函数默认是字符串.

## 布尔类型

> True and False

## if语句

```pytho
if(1>0):
    print("yes");
```

* 需要使用`:` 来追加

```pyth
age = 18;
if(age>=18):
    print("adult");
else:
    print("young");
```



```pytho
h = input();
h=int(h);
if(h>170):
    print("high");
elif(h>160):
    print("mid");
else:
    print("...");
```



* python的缩进代表你是哪个if的步骤。



## while语句

```pytho
i = 1;
while i<=100:
    print(i);
    i+=1;
```



## 输出

* 输出不换行

```pyth
print("xu",end='')
print("he")
```

* 快速格式化输出(无法控制精度)

```pyth
number = 100
print(f"number is {number}")
```

* `\t` 制表符

```pytho
print("yes\tbro")
print("no\tbro")
```

## for语句

> 循环可以对:
>
> 1. 字符串
> 2. 列表
> 3. 元组
> 4. ....



> 对于字符串类型,PY可以实现遍历取出所有的数字.`遍历循环` 

```pyth
name = "xuhe"
for x in name:
    print(x)
```



* `range` 语句

> 1. `range(5)` 代表从0开始不包含5.
> 2. `range(num1,num2)` 代表`[num1,num2)` .
> 3. `range(num1,num2,step)` .

```python
for i in range(3,10):
    print(i)
```

## 自定义函数

> 在函数的内部没有可以执行的部分的时候要写上`pass`,否则是语法错误.

```pytho
def lenfunc(data):
    cnt = 0
    for tmp in data:
        cnt+=1
    return cnt
```

* 参数传递

```pytho
def func(x,y):
    return x+y

print(func(1,2))
```

> 缺省值

```pytho
def func(x,y,z=1):
    return x+y+z

print(func(1,2))
```

* 返回`None` 

```pytho
def func(x,y,z=1):
    return None
```

* 函数注释(在函数中使用多行注释)

```pytho
def func(x,y,z=1):
    """
    
    :param x:
    :param y:
    :param z:
    :return:
    """
    return x+y+z
```

* python函数的缺省值指向的是一个一直存在的对象
* 所以它必须是一个不可修改的值

```python
def func(l = list()):
    l.append("xuhe")
    return l

print(func()) #xuhe
print(func()) #xuhe,xuhe
```

> 缺省值被修改了

### 可变参数

```python
def func(*number):  #加一个*使得它是可变参数
    sum = 0
    for i in number:
        sum+=i
    return sum

number = [1,2,3]
print(func(*number)) #传入参数的时候也需要加上*
print(func(1,2,3))
```

### 关键字参数

> 对于关键字参数，函数的调用者可以传入任意不受限制的关键字参数。至于到底传入了哪些，就需要在函数内部通过`kw`检查。
>
> 传入的参数形式是`key-name = var-name` ,然后会被封装成`dict`模式.



```python
def func(**kw):
    if "city" in kw :  #检测是否传入这个关键字
        print("city",kw["city"])
    print(kw)

func(city="hangzhou",job="worker")
```

```python
def func(*,city,job): #已经定义好了关键字的名字
    print("city=",city)
    print("job=",job)

func(job="worker",city="hangzhou")
```

### 尾递归优化



## 容器

### 列表

```python
name = ["xuhe","xuhe"]
print(name)
```

* 初始化`空列表`

```python
name1 = []
name2 = list() #都可以
```

> 在列表中,存储的数据类型是不受限制的. 

* 列表嵌套列表

```pytho
number = [[1,2],[3,4]]
print(number)
```

* 下标索引

```python
name = [1,2,3]
print(name[2])
```

> 下标索引可以是负数,代表从后面开始第几位.

```pytho
name = [1,2,3]
print(name[-1]) #输出最后一位
```

> 对于嵌套的列表,如同二维数组处理

* 查找位置`返回的是下标` 

```pytho
number = [1,2,3,4]
print(number.index(1))
```

> 使用下标查找修改里面的值

```python
number = [1,2,3,4]
number[number.index(2)] = 100
print(number)
```

* 插入操作

```pytho
number = [1,2,3,4]
number.insert(0,100) #插入在0这个位置
```

> 配合index使用

```python
number = [1,2,3,4]
number.insert(number.index(2)+1,100) #插入在2和3之间
```

* 追加操作

```pytho
number = [1,2,3,4]
number.append(5)
```

> 追加一连串的

```python
number = [1,2,3,4]
tmp = [5,6,7]
number.extend(tmp)
```

* 删除元素

> 使用关键字删除下标的数值

```pytho
number = [1,2,3,4]
del number[0]
```

> 使用方法删除下标的数值
>
> > 本质是取出这个位置的数值然后返回

```python
number = [1,2,3,4]
tmp = number.pop(0)
```

* 对元素的删除操作

> 从左到右遍历查找对应的元素然后删除第一个找到的

```python
number = [1,2,3,4,2]
number.remove(2)
```

> 如果找不到会报错

* 清空列表

```python
number.clear()
```

* 统计元素的个数

```python
number = [1,2,3,4,2]
print(number.count(2))
```

* 查看列表的大小

```python
number = [1,2,3,4,2]
print(len(number))
```

* 列表的遍历(迭代)

> 使用`while` 语句

```python
index = 0
while index < len(number):
    print(number[index])
    index+=1
```

> 使用`for`语句

```python
for x in number:
    print(x)
```

#### 列表生成方式

```python
mylist = list(x*x for x in range(1,11))
print(mylist)
```

> 可以嵌套写

> 在里面加上IF判断.

* 可以使用函数

```python
mylist = ["A","B","C"]
tmp = [s.lower() for s in mylist]
print(tmp)
```

* 判断实例类型

```python
L2 = [x.lower() for x in L1 if isinstance(x,str)]
```





### 元组

> 适用于元素不可以被修改的时候.

```pytho
a = (1,2) #生成一个元组
```

> 生成空的元组的时候

```python
a = ()
b = tuple()
```

* 在定义只有一个元素的元组的时候,一定要在元素后加上一个逗号

```pytho
a =(1,)
```

>可以使用`index`方法,可以使用`count`方法

* 元组的元素不可改变,但是元素的内部的东西可以改变,例如`list`可以改变

### 字符串

> 是不可以被修改的.
>
> 如果要修改就是得到修改之后得新的字符串.

* 可以使用`isspace()`判断是否为空格.

```python
mystr = " iamxuhe "
print(mystr[0].isspace())
```

* 字符串的查找

```pytho
name = "xuhe"
print(name.index("xu")) #返回的是第一个出现这个子串的头位置
```

* 字符串的替换

```python
name = "xuhexu"
res = name.replace("xu","d") #原来的字符串是只读的,修改之后返回新的字符串
```

* 字符串的切分

```python
mystr = "my name is xuhe"
mylist = mystr.split(" ")
```

> using the whitespace to split the string . 

* strip`去除头尾中的部分东西`

> when the param is empty , we delete the whitespace in the front and the end . 
>
> 也可以使用`[:::]`切片实现.

```python
name = "12xuhe12"
tmp = name.strip("12")
```

> the param is  "12" , and it will to find the '1' and '2' character from the front and the end to delete . 

* count`统计特定字符串的个数`

```python
name = "xuhexuhe"
tmp = name.count("xu")
```

### 序列

> 序列[起始下标:结束下标:步长]`(结束下标是开区间)`
>
> 不会修改原来的序列,得到新的序列.
>
> * 对容器可以使用

```python
mylist = [0,1,2,3,4]
print(mylist[1:3:1]) #输出的是[1,2]
```

> when the param is empty , the ans is all the var .

> it can make the string ;

```python
mystr = "0123456"
print(mystr[1:6])
```

> it also can operate the tuple .

### 集合

> 自动去重,并且是无序的.

```python
myset = {}
myset = set()
```

> 使用`={}` 定义,使用`type()`检查的时候,是`dict`类型.

* 因为它是没有顺序的,所以不支持下标索引,并且不可以使用序列的切分.
* 添加元素

```pytho
myset = {1,2}
myset.add(3) #增加一个元素,如果重复了会去重.
```

* 删除元素

```python
myset = {1,2}
myset.remove(1)
```

* 随机取出一个元素

```python
myset = {1,2}
tmp = myset.pop()
print(tmp)
```

* 清空

```python
myset.clear()
```

* 查找当前集合中有的,但是在别的集合中没有的元素构成的集合.

```pytho
myset1 = {1,2}
myset2 = {2,3}
tmp = myset1.difference(myset2) #返回一个新的集合,不会修改原来的集合
print(tmp)
```

* 在一个集合中消除两个集合的交集(会修改当前的集合`无返回值`)

```python
myset1 = {1,2}
myset2 = {2,3}
myset1.difference_update(myset2)
print(myset1)
```

* 合并两个集合,返回的是一个新的集合`不修改原来的集合`

```pytho
myset1 = {1,2}
myset2 = {2,3}
myset3 = myset1.union(myset2)
print(myset3)
```

* 统计集合中的元素个数

> 使用`len()`函数

```python
myset1 = {1,2}
print(len(myset1))
```

* 集合元素的遍历

> 不支持使用`while`语句遍历.
>
> > 因为无法使用下标索引.

> 可以使用`for`语句遍历

```python
myset1 = {1,2}
for x in myset1:
    print(x)
```

### 字典

```python
d = {"a":1,"b":2}
for x in d:  #x是下标元素
    print(x)
    print(d[x])
```

> 在下标不存在的时候,PY会报错.

* 检查是否在字典中

```python
d = {"a":1,"b":2}
flag = "a" in d
print(flag)
```

> 或者使用`get()`函数.

```python
d = {"a":3,"b":2}
flag = d.get("a")
print(flag)  #返回的是下标映射的值
```

> when the index is not defined , it return `None`.

* 元素删除`pop`

```python
d = {"a":3,"b":2}
tmp = d.pop("a") #返回的映射的值，然后删除
print(tmp)
```

### 迭代

> 用来循环内部元素.

```python
mylist = [1,2,3,4,5]
for x in mylist:
    print(x,end=' ')
```

* 对于`dict`的迭代.

```python
mydict = {"name":"xuhe","number":"1","id":"23042"}
for x in mydict:
    print(x)
for v in mydict.values(): #用来遍历全部的映射的对象
    print(v)
```

* 返回下标和值的迭代

```python
mylist = [1,2,3,4,5]
for idx,x in enumerate(mylist): #枚举函数迭代
    print(idx,' ',x)
```

## 生成器

```python
>>> g = (x * x for x in range(10))
>>> for n in g:
...     print(n)
... 
0
1
4
9
16
25
36
49
64
81
```

> 在其中可以使用`yield`存储一个值.
>
> 在生成器函数中，当执行到`yield`语句时，函数会暂停执行，并将结果返回给调用方。下次调用生成器函数时，会从上次执行暂停的地方继续执行。

```python
def my_generator():
    for i in range(5):
        yield i

# 调用生成器函数，返回一个生成器对象
gen = my_generator()

# 用迭代器遍历生成器对象
for i in gen:
    print(i)

```



## 函数本身也可以是变量

```python
x = abs
print(x)
```

> 结论：函数本身也可以赋值给变量，即：变量可以指向函数

* 可以当作函数的参数传递,本质不是文本替换

```python
def func(a,b,f):
    return f(a)+f(b)

print(func(-1,1,abs))
```

## map/reduce

```python
def func(x):
    return x*x
mymap = map(func,[1,2,3,4,5,6])
print(list(mymap))
```

`map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回。



再看`reduce`的用法。`reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算，其效果就是：

```
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
```

```python
def func(x,y):
    return x*y

from functools import reduce

print(reduce(func,[1,2,3,4,5]))
```

## filter

> Python内建的`filter()`函数用于过滤序列。

```python
def func(number):
    return (number%2)==1

print(list(filter(func,[1,2,3,4,5])))
```

> 去除空的字符串

```python
def func(mystr):
    return mystr and mystr.strip()

print(list(filter(func,["A","B"," C"," "]))) #" C"会被保留
```

## 排序函数(sorted)

> Python内置的`sorted()`函数就可以对list进行排序.

```python
mylist = [3,2,1,-9]
res = sorted(mylist)
print(res)
```

> 反向

```python
mylist = [3,2,1,-9]
res = sorted(mylist,reverse=True)
print(res)
```



## 返回函数



```python
def func(*number):
    def sumfunc():
        sum = 0
        for x in number:
            sum += x
        return sum
    return sumfunc()

f = func(1,2,3,4,5,6)

print(f) #返回的是21
```

> 在这个例子中，我们在函数`lazy_sum`中又定义了函数`sum`，并且，内部函数`sum`可以引用外部函数`lazy_sum`的参数和局部变量，当`lazy_sum`返回函数`sum`时，相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）”的程序结构拥有极大的威力。

* 返回的是一个新的函数,即使传入的一样的参数,返回的函数也是不一样的.

## 闭包

注意到返回的函数在其定义内部引用了局部变量`args`，所以，当一个函数返回了一个函数后，其内部的局部变量还被新函数引用，所以，闭包用起来简单，实现起来可不容易。

另一个需要注意的问题是，返回的函数并没有立刻执行，而是直到调用了`f()`才执行。我们来看一个例子：

```
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f)
    return fs

f1, f2, f3 = count()
```

在上面的例子中，每次循环，都创建了一个新的函数，然后，把创建的3个函数都返回了。

你可能认为调用`f1()`，`f2()`和`f3()`结果应该是`1`，`4`，`9`，但实际结果是：

```
>>> f1()
9
>>> f2()
9
>>> f3()
9
```

## lambda表达式

在Python中，对匿名函数提供了有限支持。还是以`map()`函数为例，计算f(x)=x2时，除了定义一个`f(x)`的函数外，还可以直接传入匿名函数：

```
>>> list(map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9]))
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

通过对比可以看出，匿名函数`lambda x: x * x`实际上就是：

```
def f(x):
    return x * x
```

关键字`lambda`表示匿名函数，冒号前面的`x`表示函数参数。

匿名函数有个限制，就是只能有一个表达式，不用写`return`，返回值就是该表达式的结果。

## 装饰器

由于函数也是一个对象，而且函数对象可以被赋值给变量，所以，通过变量也能调用该函数。

```python
>>> def now():
...     print('2015-3-25')
...
>>> f = now
>>> f()
2015-3-25
```

函数对象有一个`__name__`属性（注意：是前后各两个下划线），可以拿到函数的名字：

```python
>>> now.__name__
'now'
>>> f.__name__
'now'
```

在Python中，@语法是用来实现装饰器（Decorator）的语法糖。装饰器是一种函数，可以修改其他函数的功能。装饰器函数可以作为参数传递给其他函数，在其他函数的执行过程中修改其行为，从而实现一些额外的功能。

@语法可以让我们更方便地使用装饰器，使用@语法可以将一个装饰器函数直接应用到一个函数或方法上。例如，下面的代码演示了如何使用@语法定义一个简单的装饰器函数：

```
def my_decorator(func):
    def wrapper():
        print("Before the function is called.")
        func()
        print("After the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello, world!")

say_hello()
```

在上面的代码中，@my_decorator语法用于将my_decorator装饰器函数应用到say_hello函数上。因此，当我们调用say_hello函数时，实际上调用的是my_decorator函数返回的wrapper函数，从而在函数执行前后打印出一些信息。

需要注意的是，@语法只是一种语法糖，本质上是将装饰器函数作为参数传递给被装饰的函数。因此，@语法的本质是函数调用，只是更为简洁而已。



## 类

* 方法创建

```python
class xuhe:
    def add(x,y):
        return x+y

print(xuhe.add(1,2))
```

`class`后面紧接着是类名，即`Student`，类名通常是大写开头的单词，紧接着是`(object)`，表示该类是从哪个类继承下来的，继承的概念我们后面再讲，通常，如果没有合适的继承类，就使用`object`类，这是所有类最终都会继承的类。

```
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score
```

> 注意到`__init__`方法的第一个参数永远是`self`，表示创建的实例本身，因此，在`__init__`方法内部，就可以把各种属性绑定到`self`，因为`self`就指向创建的实例本身。
>
> 有了`__init__`方法，在创建实例的时候，就不能传入空的参数了，必须传入与`__init__`方法匹配的参数，但`self`不需要传，Python解释器自己会把实例变量传进去：



* 成员函数的实现

要定义一个方法，除了第一个参数是`self`外，其他和普通函数一样。要调用一个方法，只需要在实例变量上直接调用，除了`self`不用传递，其他参数正常传入：

```
>>> bart.print_score()
Bart Simpson: 59
```



### 继承

所以，在继承关系中，如果一个实例的数据类型是某个子类，那它的数据类型也可以被看做是父类。但是，反过来就不行：

```python
>>> b = Animal()
>>> isinstance(b, Dog)
False
```

并且还可以判断一个变量是否是某些类型中的一种，比如下面的代码就可以判断是否是list或者tuple：

```python
>>> isinstance([1, 2, 3], (list, tuple))
True
>>> isinstance((1, 2, 3), (list, tuple))
True
```

我们自己写的类，如果也想用`len(myObj)`的话，就自己写一个`__len__()`方法：

```python
>>> class MyDog(object):
...     def __len__(self):
...         return 100
...
>>> dog = MyDog()
>>> len(dog)
100
```

紧接着，可以测试该对象的属性：

```python
>>> hasattr(obj, 'x') # 有属性'x'吗？
True
>>> obj.x
9
>>> hasattr(obj, 'y') # 有属性'y'吗？
False
>>> setattr(obj, 'y', 19) # 设置一个属性'y'
>>> hasattr(obj, 'y') # 有属性'y'吗？
True
>>> getattr(obj, 'y') # 获取属性'y'
19
>>> obj.y # 获取属性'y'
19
```

可以传入一个default参数，如果属性不存在，就返回默认值：

```python
>>> getattr(obj, 'z', 404) # 获取属性'z'，如果不存在，返回默认值404
404
```

如果`Student`类本身需要绑定一个属性呢？可以直接在class中定义属性，这种属性是类属性，归`Student`类所有：

```
class Student(object):
    name = 'Student'
```

当我们定义了一个类属性后，这个属性虽然归类所有，但类的所有实例都可以访问到。

## 使用__slots__



如果我们想要限制实例的属性怎么办？比如，只允许对Student实例添加`name`和`age`属性。

为了达到限制的目的，Python允许在定义class的时候，定义一个特殊的`__slots__`变量，来限制该class实例能添加的属性：

```
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
```

然后，我们试试：

```
>>> s = Student() # 创建新的实例
>>> s.name = 'Michael' # 绑定属性'name'
>>> s.age = 25 # 绑定属性'age'
>>> s.score = 99 # 绑定属性'score'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Student' object has no attribute 'score'
```

由于`'score'`没有被放到`__slots__`中，所以不能绑定`score`属性，试图绑定`score`将得到`AttributeError`的错误。

使用`__slots__`要注意，`__slots__`定义的属性仅对当前类实例起作用，对继承的子类是不起作用的：

## @property



Python内置的`@property`装饰器就是负责把一个方法变成属性调用的：

```
class Student(object):

    @property
    def score(self):
        return self._score

    @score.setter
    def score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0 ~ 100!')
        self._score = value
```

`@property`的实现比较复杂，我们先考察如何使用。把一个getter方法变成属性，只需要加上`@property`就可以了，此时，`@property`本身又创建了另一个装饰器`@score.setter`，负责把一个setter方法变成属性赋值，于是，我们就拥有一个可控的属性操作：

```python
>>> s = Student()
>>> s.score = 60 # OK，实际转化为s.set_score(60)
>>> s.score # OK，实际转化为s.get_score()
60
>>> s.score = 9999
Traceback (most recent call last):
  ...
ValueError: score must between 0 ~ 100!
```



> tips:属性的方法名不要和实例变量重名

```python
class Student(object):

    # 方法名称和实例变量均为birth:
    @property
    def birth(self):  #error
        return self.birth
```

这是因为调用`s.birth`时，首先转换为方法调用，在执行`return self.birth`时，又视为访问`self`的属性，于是又转换为方法调用，造成无限递归，最终导致栈溢出报错`RecursionError`。



## 多重继承

### MixIn

在设计类的继承关系时，通常，主线都是单一继承下来的，例如，`Ostrich`继承自`Bird`。但是，如果需要“混入”额外的功能，通过多重继承就可以实现，比如，让`Ostrich`除了继承自`Bird`外，再同时继承`Runnable`。这种设计通常称之为MixIn。

为了更好地看出继承关系，我们把`Runnable`和`Flyable`改为`RunnableMixIn`和`FlyableMixIn`。类似的，你还可以定义出肉食动物`CarnivorousMixIn`和植食动物`HerbivoresMixIn`，让某个动物同时拥有好几个MixIn：

```
class Dog(Mammal, RunnableMixIn, CarnivorousMixIn):
    pass
```

MixIn的目的就是给一个类增加多个功能，这样，在设计类的时候，我们优先考虑通过多重继承来组合多个MixIn的功能，而不是设计多层次的复杂的继承关系。



## 定制类

### __iter__

如果一个类想被用于`for ... in`循环，类似list或tuple那样，就必须实现一个`__iter__()`方法，该方法返回一个迭代对象，然后，Python的for循环就会不断调用该迭代对象的`__next__()`方法拿到循环的下一个值，直到遇到`StopIteration`错误时退出循环。

我们以斐波那契数列为例，写一个Fib类，可以作用于for循环：

```
class Fib(object):
    def __init__(self):
        self.a, self.b = 0, 1 # 初始化两个计数器a，b

    def __iter__(self):
        return self # 实例本身就是迭代对象，故返回自己

    def __next__(self):
        self.a, self.b = self.b, self.a + self.b # 计算下一个值
        if self.a > 100000: # 退出循环的条件
            raise StopIteration()
        return self.a # 返回下一个值
```

现在，试试把Fib实例作用于for循环：

```
>>> for n in Fib():
...     print(n)
...
1
1
2
3
5
...
46368
75025
```

### __getitem__

Fib实例虽然能作用于for循环，看起来和list有点像，但是，把它当成list来使用还是不行，比如，取第5个元素：

```
>>> Fib()[5]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'Fib' object does not support indexing
```

要表现得像list那样按照下标取出元素，需要实现`__getitem__()`方法：

```
class Fib(object):
    def __getitem__(self, n):
        a, b = 1, 1
        for x in range(n):
            a, b = b, a + b
        return a
```

现在，就可以按下标访问数列的任意一项了：

```
>>> f = Fib()
>>> f[0]
1
>>> f[1]
1
>>> f[2]
2
>>> f[3]
3
>>> f[10]
89
>>> f[100]
573147844013817084101
```

但是list有个神奇的切片方法：

```
>>> list(range(100))[5:10]
[5, 6, 7, 8, 9]
```

对于Fib却报错。原因是`__getitem__()`传入的参数可能是一个int，也可能是一个切片对象`slice`，所以要做判断：

```python
class Fib(object):
    def __getitem__(self, n):
        if isinstance(n, int): # n是索引
            a, b = 1, 1
            for x in range(n):
                a, b = b, a + b
            return a
        if isinstance(n, slice): # n是切片
            start = n.start
            stop = n.stop
            if start is None:
                start = 0
            a, b = 1, 1
            L = []
            for x in range(stop):
                if x >= start:
                    L.append(a)
                a, b = b, a + b
            return L
```

现在试试Fib的切片：

```python
>>> f = Fib()
>>> f[0:5]
[1, 1, 2, 3, 5]
>>> f[:10]
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```



### __getattr__

正常情况下，当我们调用类的方法或属性时，如果不存在，就会报错。比如定义`Student`类：

```
class Student(object):
    
    def __init__(self):
        self.name = 'Michael'
```

调用`name`属性，没问题，但是，调用不存在的`score`属性，就有问题了：

```
>>> s = Student()
>>> print(s.name)
Michael
>>> print(s.score)
Traceback (most recent call last):
  ...
AttributeError: 'Student' object has no attribute 'score'
```

错误信息很清楚地告诉我们，没有找到`score`这个attribute。

要避免这个错误，除了可以加上一个`score`属性外，Python还有另一个机制，那就是写一个`__getattr__()`方法，动态返回一个属性。修改如下：

```
class Student(object):

    def __init__(self):
        self.name = 'Michael'

    def __getattr__(self, attr):
        if attr=='score':
            return 99
```

当调用不存在的属性时，比如`score`，Python解释器会试图调用`__getattr__(self, 'score')`来尝试获得属性，这样，我们就有机会返回`score`的值：

```python
>>> s = Student()
>>> s.name
'Michael'
>>> s.score
99
```

返回函数也是完全可以的：

```
class Student(object):

    def __getattr__(self, attr):
        if attr=='age':
            return lambda: 25
```

只是调用方式要变为：

```python
>>> s.age()
25
```







# pynput

Use `pynput.keyboard.Controller` like this:

```python
from pynput.keyboard import Key, Controller

keyboard = Controller()

# Press and release space
keyboard.press(Key.space)
keyboard.release(Key.space)

# Type a lower case A; this will work even if no key on the
# physical keyboard is labelled 'A'
keyboard.press('a')
keyboard.release('a')

# Type two upper case As
keyboard.press('A')
keyboard.release('A')
with keyboard.pressed(Key.shift):
    keyboard.press('a')
    keyboard.release('a')

# Type 'Hello World' using the shortcut type method
keyboard.type('Hello World')
```

* 检测一秒内是否有输入

```python
from pynput import keyboard

# The event listener will be running in this block
with keyboard.Events() as events:
    # Block at most one second
    event = events.get(1.0)
    if event is None:
        print('You did not press a key within one second')
    else:
        print('Received event {}'.format(event))
```

> 这段代码使用了pynput库中的`Events`类来监视键盘事件。在主程序中，我们在一个`with`语句块中创建了一个`Events`对象，并使用`get()`方法来等待一个键盘事件。在这个例子中，我们使用`get(1.0)`来等待1秒钟内的事件。如果在1秒钟内没有事件发生，程序将输出一条消息，否则程序将输出一个表示事件的字符串。
>
> 您可以在`if event is None:`的代码块中添加自己的逻辑来处理键盘事件。例如，如果您想等待用户输入一个特定的字符串，可以在这里添加一个循环来等待连续的按键事件，并在输入完整的字符串后触发您的操作。





# `matplotlib`

```python
import numpy as np
import matplotlib
import matplotlib.mlab as mlab
import matplotlib.pyplot as plt
import matplotlib.font_manager as fm
from mpl_toolkits.mplot3d import Axes3D

# 解决中文乱码问题
myfont = fm.FontProperties(fname="/Library/Fonts/Songti.ttc", size=14)
matplotlib.rcParams["axes.unicode_minus"] = False
```

* 用一行代码解决中文乱码的问题

```python
plt.rcParams['font.sans-serif'] = ['SimHei'] # 用来正常显示中文标签
```





## 使用`plot`画直线图

* 直线图

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3, 4]) # plt.plot([1,2],[3,4])
plt.ylabel('some numbers')
plt.show()
```

* 折线图

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]
plt.plot(x, y)
plt.show()
```

* 设置线条的粗细

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]
plt.plot(x, y, linewidth=5) # 使用linewidth设置线条粗细
plt.show()
```

* 设置`xlabel`and`ylabel`

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]
plt.plot(x, y, linewidth=5) # 使用linewidth设置线条粗细
plt.title("Square Numbers", fontsize=24) # 设置图表标题，并给定字体大小
plt.xlabel("Value", fontsize=14) # 设置x轴标签
plt.ylabel("Square of Value", fontsize=14) # 设置y轴标签
plt.show()
```

* `sin` function

```python
import matplotlib.pyplot as plt
import numpy as np

# plt.rcParams['font.sans-serif'] = ['SimHei'] # 用来正常显示中文标签

# y=sin(x)
x = np.linspace(-np.pi, np.pi, 256, endpoint=True)
y = np.sin(x)
plt.plot(x, y)
plt.show()
```

* 一张图画两个函数

```python
import matplotlib.pyplot as plt
import numpy as np

# plt.rcParams['font.sans-serif'] = ['SimHei'] # 用来正常显示中文标签


x = np.linspace(-np.pi, np.pi, 256, endpoint=True)
# y=sin(x)
sin_y = np.sin(x)
# y=cos(x)
cos_y = np.cos(x)
plt.plot(x, sin_y)
plt.plot(x, cos_y)

plt.show()
```



## `scatter`散点图

```python
import matplotlib.pyplot as plt
import numpy as np

# plt.rcParams['font.sans-serif'] = ['SimHei'] # 用来正常显示中文标签


x = np.linspace(-np.pi, np.pi, 10, endpoint=True)
# y=sin(x)
sin_y = np.sin(x)
# draw a scatter graph
plt.scatter(x, sin_y, linewidths=0.1)
plt.show()
```



## 表示线的类型和颜色的特殊字符



| 颜色字符 | 颜色   |
| -------- | ------ |
| `'b'`    | 蓝色   |
| `'g'`    | 绿色   |
| `'r'`    | 红色   |
| `'c'`    | 青色   |
| `'m'`    | 洋红色 |
| `'y'`    | 黄色   |
| `'k'`    | 黑色   |
| `'w'`    | 白色   |

| 线条样式字符 | 线条样式 |
| ------------ | -------- |
| `'-'`        | 实线     |
| `'--'`       | 虚线     |
| `':'`        | 点线     |
| `'-.'`       | 点划线   |

使用这些字符可以在`plot`函数中指定绘图的颜色和线条样式，例如使用`'r--'`表示绘制红色的虚线。



## `legend`图例

```python
import matplotlib.pyplot as plt
import numpy as np

# plt.rcParams['font.sans-serif'] = ['SimHei'] # 用来正常显示中文标签

# y=x*x
x = np.arange(0, 100, 0.1)
y = x * x
plt.plot(x, y, label='y=x*x')
# y=x
y2 = x
plt.plot(x, y2, label='y=x')

plt.title('y=x*x')
plt.xlabel('x')
plt.ylabel('y')
plt.legend(loc='upper right', fontsize='small', fancybox=True)  # 设置字体大小和使用圆角边框
plt.show()
```

> 要在函数使用`label=`的条件下使用这个函数

```python
plt.plot(x, y, label='y=x*x')
```

* 使用`shadow`属性,使得这个图例更加显眼

```python
plt.legend(loc='upper left', shadow=True)
```





## `bar()`绘制`柱状图`

* 使用`xticks()`函数标记`x轴上的东西`

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams['font.sans-serif'] = ['SimHei']  # 用来正常显示中文标签

# 绘制柱状图
x = np.arange(5)
x_ticks = ['A', 'B', 'C', 'D', 'E']
y = [20, 10, 30, 25, 15]
plt.bar(x, y, align='center', color='c', alpha=0.8)
plt.xticks(x, x_ticks)
plt.xlabel('X')
plt.ylabel('Y')
plt.title('柱状图')
plt.show()
```

好的，我将以第一人称视角为你提供关于`subplot`的介绍。

## Subplot

Subplot 是 Matplotlib 中用于创建和布局多个子图的函数。它允许我们将一个大的图形区域分割为多个小的子图，并在每个子图中绘制不同的数据或图形。

### 语法

```python
import matplotlib.pyplot as plt

plt.subplot(rows, cols, index)
```

其中，`rows` 和 `cols` 分别表示子图的行数和列数，`index` 表示当前子图在整个图形区域中的位置。

### 示例

假设我们要创建一个学习笔记的图形，其中包含 2 行 2 列共 4 个子图。我们可以按照以下方式使用 `subplot` 函数创建和布局这些子图，并在每个子图中绘制不同的数据：

```python
import matplotlib.pyplot as plt

# 创建第一个子图
plt.subplot(2, 2, 1)
plt.plot(x1, y1)

# 创建第二个子图
plt.subplot(2, 2, 2)
plt.plot(x2, y2)

# 创建第三个子图
plt.subplot(2, 2, 3)
plt.plot(x3, y3)

# 创建第四个子图
plt.subplot(2, 2, 4)
plt.plot(x4, y4)

plt.show()
```

在上述代码中，我们通过 `plt.subplot` 函数分别创建了四个子图，并在每个子图中绘制了不同的数据。这种布局方式使得我们可以在一个图形中同时展示多个相关或独立的数据，从而更好地比较和分析它们。

使用 `subplot` 函数可以轻松创建和布局多个子图，使得学习笔记的编写更加直观和清晰。你可以根据需要设置不同的行数、列数和子图位置，并在每个子图中进行自定义的绘图操作，以便更好地呈现你的数据和观察结果。



## 绘制一条辅助线

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 2, 3, 4]

plt.plot(x, y, 'ro')

plt.axhline(y=1, color='k') # black line
plt.axvline(x=1, color='k') # black line

plt.show()
```



## 使用`pie`绘制饼状图

```python
import matplotlib.pyplot as plt
import numpy as np

# 生成测试数据
mu, sigma = 100, 15
x = mu + sigma * np.random.randn(10000)

# 设置标题
plt.title("直方图", fontproperties=myfont)

# 画直方图, 并返回相关结果
n, bins, patches = plt.hist(x, bins=50, normed=1, cumulative=False, color="green", alpha=0.6, label="直方图")

# 根据直方图返回的结果, 画折线图
y = plt.normpdf(bins, mu, sigma)
plt.plot(bins, y, "r--", label="线条")

# 设置图例位置
plt.legend(loc="upper left", prop=myfont, shadow=True)

# 图形显示
plt.show()
```

> 在绘制`直方图`的时候,当数据很多的时候,是把很多的数据获取一个平均值放到一个直方里面,我们可以使用`bins=`的方式,控制总的`直方`的个数.



# `re`模块



## `findall`

```python
res = re.findall(pattern,string)
```



## `finditer`

```python
import re

it = re.finditer(r"\d+", "12 drummers drumming, 11 pipers piping, 10 lords a-leaping")

for match in it:
    print(match.group()) # 使用group()来获取
```

* 使用迭代器的效率更高



## `search()`

> 找到多个式子(匹配的),返回的是迭代器



## `match()`

> 从头开始匹配一个式子



## `compile()`

> 预加在正则表达式的内容

```python
import re

obj = re.compile(r'(\w+) (\w+)')

print(obj.sub(r'\2 \1', 'hello world'))
```

* 本质是提前加载`pattern`



* 在正则表达式中，`re.S` 是 re 模块的一个标记（flag），它用于指定一个特殊的匹配模式，即“单行模式”（single line mode）或称为“点号匹配换行模式”（dot-all mode）。

  默认情况下，正则表达式中的点号（`.`）不匹配换行符（`\n`）。然而，当使用 `re.S` 标记时，点号将匹配任意字符，包括换行符。这使得正则表达式可以跨越多行匹配，从而更方便地处理包含换行符的文本。



# `json`

> use `json` to make data to the json string . 

```python
import json

person = '{"name": "Bob", "languages": ["English", "Fench"]}' # JSON 字串

# JSON 字串轉成 Python dict
person_dict = json.loads(person)

print('type of person_dict:', type(person_dict))
print(person_dict)
```



* when it is dict , the key is arrounded by `'` , not the `"` , when it is `json string` , it is `"` , so by using the character ,we can find the type of data very quickly . 

* when it is json string , the boolean value is `true` or `false` , not `True` or `False` . 



## use `json.dump` to write the data

* use the `dump` to write the data to the `.json` file , the first parameter is the `dict` . 

```python
import json

# 字典格式
person = {
    'name': 'zhangsan',
    'age': 18
}

with open('test.json','w') as f: # 將字典寫入json檔案
    json.dump(person,f)
```



### `ident`

在 `json.dump()` 函数中，`indent` 参数用于指定生成的 JSON 数据的缩进级别，以增加可读性。

`indent` 参数接受一个整数值，表示缩进的空格数。设置为 `None` 或 0 表示不进行缩进，生成的 JSON 数据将会是一行。设置为正整数表示每个层级缩进的空格数，例如设置为 4 表示每个层级缩进4个空格。

下面是一个示例，演示如何使用 `indent` 参数生成带有缩进的 JSON 数据：

```python
import json

data = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

json_data = json.dumps(data, indent=4)
print(json_data)
```

输出结果如下：
```
{
    "name": "John",
    "age": 30,
    "city": "New York"
}
```

在上面的示例中，`json.dumps()` 函数将 Python 字典 `data` 序列化为 JSON 格式的字符串，并使用 `indent=4` 参数进行缩进。打印输出的 JSON 数据可以看到，每个层级都使用了4个空格进行缩进，使其更易读。

注意，`json.dumps()` 函数与 `json.dump()` 函数不同，它将 Python 对象序列化为 JSON 格式的字符串，而不是将其写入文件。



