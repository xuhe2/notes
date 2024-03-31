* 使用的是大驼峰的命名法



# `.net`

dotnet = FCL + CLR

> framework class library 类似JAVA中的JDK
>
> common language runtime 类似JAVA的JVM



* 面向对象
* 事件驱动
* 存在GC



WPF: 界面可视化编程



# 编译流程

C# -> CIL(中间语言) -> JIT



# 变量

使用`decimal`,`float`,`double`

* 默认使用的是`double`



* int是一个结构体, 在CIL中叫做int32
* 全部的变量从`Object`继承, 才可以使用CLR管理内存

> 继承`Object`的分成2者
>
> 1. valueType, 结构体是作为值类型的, 申明的时候就有空间了, 不可继承
> 2. 引用类, 可继承



* 任何变量需要**被初始化过值之后才可以访问**, 但是可以写入(在`for`嵌套体中的初始化不被作为一个合格的初始化, 但是**块内容中的初始化是合格的**)



## 使用`var`

暗示变量的类型



* 使用`var`的时候,需要**初始化**.



## 纯文本

不存在`\`符号的转义或者别的内容

使用`@`运算符

```c#
// To generate Japanese invoices:
// Nihon no seikyū-sho o seisei suru ni wa:
Console.Write("\n\n\u65e5\u672c\u306e\u8acb\u6c42\u66f8\u3092\u751f\u6210\u3059\u308b\u306b\u306f\uff1a\n\t");
// User command to run an application
Console.WriteLine(@"c:\invoices\app.exe -j");
```



## 文本插值构建字符串变量

使用`$`符号实现

```c#
string name = "xuhe";
string str = $"hello {name}";
Console.Write(str);
```

* 使用文本插值的时候,可以插入一个数字类型.



* `@`和`$`符号可以一起使用



## 隐式类型转换

使用`+`连接字符串和数字类型的时候,会把数字类型转换成为字符串类型相加



转换浮点数到数字类型的时候,小数部分会被截断



## decimal

十进制表示的数字



## 类型转换

使用`int.Parse`, 可能存在报错

使用 `int.TryParse`尝试类型转换

> 返回值是**是否正确转换**, 需要传入一个结果值(out参数)



# 输入

```csharp
String str = Console.ReadLine();
Console.WriteLine(str);

```

> 读入一行



## 转换

使用`Convert`的`ToInt32`

使用`int`的`Parse`方法



# 值类型(value type)

简单变量, 指向的内存就存放着内容



# 引用类型(reference type)

存放的是复杂变量

* 使用CLR自动的垃圾回收



# 命名空间

使用`using <package name>`导入



* 命名空间可以嵌套



# 类

包含`instance variables`,`function`,`static`,`const`,`properties(setter/getter)`



属性是一个语法糖(实现了`getter`/`setter`)

```c#
public int X{
    get {
        return x;
    }
    set {
        x = value;
    }
}
```

* 不能和变量同名

> className.X = 1;



## 便捷的属性写法

```c#
public int x{ get; set; }
```

* 把实际的变量存在一个不显示的地方



不允许写入的做法

```c#
public int x{ get; private set; }
```



* 最好使用统一的属性来操作



## 构造函数

```c#
public class_name {
    
}
```

同时里面的属性会自动被赋值

* 需要表明`public`



```c#
public class_name: this(xx,xx) {}
```

在调用空参数构造函数的时候, 复用有参构造函数



## 析构函数

```c#
~class_name() {}
```

* 不需要`public`
* 一般不写, 可能阻止垃圾回收机制



## 不带访问修饰符的函数

不可访问

访问级别是`internal`

> 在同一个程序集中才可以访问



## 可变参数函数

使用`params`参数实现

```c#
static int func(params int[] n){}
func(1);
func(1,2);
func([1,2,3]);
```





## 方法参数

默认传递的是值

> 引用传递的也是值, 传递的是地址值



引用类型的参数

```c#
public void func(ref int a){}
```

```c#
func(ref a);
```



```c#
public void func(out int a) {}
```

```c#
func(out a);
```

* `ref`需要变量被初始化, 但是`out`可以不需要初始化
* `out`传入的参数不可以直接被`print`, out是**为了被赋值的**

* 返回值可以是`ref int`, 但是不可以是`out int`返回值.
* 返回参数使用括号包裹, 可以返回多个, 相当于是`()`元组, 接受的时候使用解析的方式打开



# `readonly`和`const`

`const`在编译的时候, 会被替换, 类似于`define`

`readonly`编译之后依旧存在



# if

* 不可以直接把int变量作为判断的条件, 不会自动把`int`转换为`bool`
* `&`和`&&`都是and,  `&`没有短路效果



# Object

所有的类都从`Object`中继承的

有`ToString`方法



# 工具类



## Array

引用类型, 从**Array**继承过来的信息

```c#
int[] a = new int[10];
```

* 没有的初始值的new, 会使用**默认值0**

* 使用参数`Length`检查长度



初始化

```c#
int[] arr = {1, 2, 3};
```

```c#
int[] arr = new int[]{1, 2};
```

* 当初始化指定的长度和传入的参数的值个数不一样的时候, **会错误**



循环数组

> 使用`for`直接遍历每个数组的长度, 作为下标访问

> 使用`foreach`遍历(不可修改值)

```c#
foreach(int i in arr){
    
}
```



使用工具类的静态方法**实现二分搜索, 实现排序**



### 二维数组

使用`,`

```c#
int[,] arr = new int[3,4];
```

* `arr`的`Length`是3*4, 总的长度
* 使用`GetLength()`,传入的参数是**第几维度**.



使用`foreach`输出二维数组的时候, 把二维压成了一维



锯齿数组

```c#
int[][] arr = new int[3][];
arr[0] = new int[4];
arr[1] = new int[5];
```

* 对于0维可以使用`GetLength`, 对于其他不确定长度的维度, 不可以使用



## string

使用的是`unicode`(使用2字节表示)

使用`CompareTo`进行比较



`str[0]='a'`错误, 对于索引器(只读)是不可以修改的

* 字符串是**不可变的**, 需要**接受返回值**
* 字符串的修改操作是低效的



* 需要对字符串的修改操作很多的时候, 使用`StringBuilder`实现



Pad和Trim做的是相反的操作



### 操作

add: +

修改: replace, trim, pad

切分: substring, spilt



使用`$`来快速格式化输出

`$"{number,10:F5}"`占十个位置, 浮点数部分占五个位置



## Char

是一个结构体struct



## Random

```c#
int number = random.Next(10,100);
```

* 左闭合右开放



## DateTime

显示自己的时间信息



## 元组

使用`()`

```c#
(string name, int number) person = ("xuhe", 1);
person.name;
```





* 也是一种值类型



# class

internal class(默认): 同一个程序集中就可以访问, 是同一个项目.



## data

instance fields,cont,inner class,static fields,readonly



* 存在内部类
* 只有构造函数可以设置readonly的变量
* 可以通过设置setter但是不设置getter, 让一个变量成为readonly

## method

包含instance method,static method,constructor,destructor,property,overloaded operation,index



* 默认是`private`.

* 使用析构函数会造成垃圾回收的延后, 所以, 如果需要手动的清除, 设置一个`Dispose`函数

> 在使用的时候, 使用`using(var a = new var()){}`的语法糖
>
> 或者显式的调用`Dispose`函数



### 构造函数



构造方法之间的调用

```c#
public class_name(): this(1){
    
}

public class_name(int number){
    //
}
```



调用的时候可以使用`{}`来初始化

```c#
class_name a = new class_name{
    var1 = 1;
}
```



* 当执行派生类的构造函数的时候, 会自动调用基类的无参构造函数.



### getter/setter

```c#
public int x{
    set{
        
    }
    private get{
        
    }
}
```



## 继承

字段和属性都是可以继承的

* 构造函数不可继承, 有static属性的.



## override

存在`override`关键字

```c#
public override func(){}
```



## virtual

虚函数



* 需要`virtual`和`override`配合使用, 才有多态的效果. 如果不使用, 那么是hide效果

* 可以给`property`使用



## abstract

有抽象方法就是抽象类

抽象类无法被继承

* 抽象方法只有申明, 没有实现, 但是虚方法可以有实现



## sealed

被继承了也不可以被重写的方法

* sealed是对下的, override是对上的, 所以2者可以共存
* `sealed`和`abstract`/`virtual`不可以共存



## 不可变类

注意, 行为是不可修改的

> 字段: private(不可以是protected)
>
> 属性: 没有set
>
> 方法: 不可以set, 返回一个new的新对象
>
> 给类添加sealed, 不可以被继承可以防止子类修改行为



## 调用基类的方法

使用`base`调用基类的操作, 比如`base()`无参构造函数, `base.func()`基类方法
