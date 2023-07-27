> JAVA风格和C++类似

> tips:
>
> > JAVA程序的开始一定是一个`public class Main` class 下的一个`public static void main(String[] args)`的方法



# float and double

> 浮点数运算和整数运算相比，只能进行加减乘除这些数值计算，不能做位运算和移位运算。
>
> 在计算机中，浮点数虽然表示的范围大，但是，浮点数有个非常重要的特点，就是浮点数常常无法精确表示。

* 由于浮点数存在运算误差，所以比较两个浮点数是否相等常常会出现错误的结果。正确的比较方法是判断两个浮点数之差的绝对值是否小于一个很小的数

```java
// 比较x和y是否相等，先计算其差的绝对值:
double r = Math.abs(x - y);
// 再判断绝对值是否足够小:
if (r < 0.00001) {
    // 可以认为相等
} else {
    // 不相等
}
```



# array

* java array init

```java
int[] ns = new int[5]; 
```

> the prefix is `int[]`



# input and output

> 在前面的代码中，我们总是使用`System.out.println()`来向屏幕输出一些内容。
>
> `println`是print line的缩写，表示输出并换行。因此，如果输出后不想换行，可以用`print()`



## format the output

> 如果要把数据显示成我们期望的格式，就需要使用格式化输出的功能。格式化输出使用`System.out.printf()`，通过使用占位符`%?`，`printf()`可以把后面的参数格式化成指定格式

```java
public class Main {
    public static void main(String[] args) {
        double d = 3.1415926;
        System.out.printf("%.2f\n", d); // 显示两位小数3.14
        System.out.printf("%.4f\n", d); // 显示4位小数3.1416
    }
}
```



| 占位符 | 说明                             |
| :----- | :------------------------------- |
| %d     | 格式化输出整数                   |
| %x     | 格式化输出十六进制整数           |
| %f     | 格式化输出浮点数                 |
| %e     | 格式化输出科学计数法表示的浮点数 |
| %s     | 格式化字符串                     |



# through the array

* use the `for` 

```java
for (int i=0; i<ns.length; i++)
```

* use the `for each`

```java
for (int n : ns)
```



# sort the array 

* use the `Array.sort`

```java
import java.util.Arrays;
int[] ns = { 28, 12, 89, 73, 65, 18, 96, 50, 8, 36 };
Arrays.sort(ns);
```



# use the terminal params



```java
public class Main {
    public static void main(String[] args) {
        for (String arg : args) {
            if ("-version".equals(arg)) {
                System.out.println("v 1.0");
                break;
            }
        }
    }
}
```

* run the program

```java
$ java Main -version
v 1.0
```



# class 

> tips:
>
> > 在一个class文件中只能存在一个和文件名一样名字的`public class`



## attribute

```java
class Person {
    public String name;
    public int age;
}
```



# constructor

> 由于构造方法是如此特殊，所以构造方法的名称就是类名。构造方法的参数没有限制，在方法内部，也可以编写任意语句。但是，和普通方法相比，构造方法没有返回值（也没有`void`），调用构造方法，必须用`new`操作符。

```java
	public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
```



