* 使用的是大驼峰的命名法



# 变量

使用`decimal`,`float`,`double`

* 默认使用的是`double`



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

