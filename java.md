> JAVA 风格和 C++类似

> tips:
>
> > JAVA 程序的开始一定是一个`public class Main` class 下的一个`public static void main(String[] args)`的方法



# integer

```java
int num = Integer.parseInt("abc");
```





# float and double

> 浮点数运算和整数运算相比，只能进行加减乘除这些数值计算，不能做位运算和移位运算。
>
> 在计算机中，浮点数虽然表示的范围大，但是，浮点数有个非常重要的特点，就是浮点数常常无法精确表示。

- 由于浮点数存在运算误差，所以比较两个浮点数是否相等常常会出现错误的结果。正确的比较方法是判断两个浮点数之差的绝对值是否小于一个很小的数

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



* 给`float`的变量赋值的时候,需要使用`3.14f`.



# array

* 使用`ArrayList`.



- java array init

```java
int[] ns = new int[5];
```

> the prefix is `int[]`



## array copy

* 我们不能直接使用赋值，这样指向的是相同的内存空间，需要自己新开辟一部分的`Array`空间

在Java中，你可以使用不同的方法来复制一个新的数组，具体取决于你想要实现的功能和使用场景。下面介绍几种常见的方法。

### 1. 使用循环遍历复制数组：

这是一种最基本的方法，通过遍历源数组的每个元素，逐个复制到新的数组中。

```java
public class ArrayCopyExample {
    public static void main(String[] args) {
        int[] sourceArray = {1, 2, 3, 4, 5};
        int[] destinationArray = new int[sourceArray.length];

        for (int i = 0; i < sourceArray.length; i++) {
            destinationArray[i] = sourceArray[i];
        }

        // 现在 destinationArray 是 sourceArray 的副本
    }
}
```

### 2. 使用`System.arraycopy`方法：

Java提供了`System.arraycopy`方法来复制数组的一部分或整个数组。

```java
public class ArrayCopyExample {
    public static void main(String[] args) {
        int[] sourceArray = {1, 2, 3, 4, 5};
        int[] destinationArray = new int[sourceArray.length];

        System.arraycopy(sourceArray, 0, destinationArray, 0, sourceArray.length);

        // 现在 destinationArray 是 sourceArray 的副本
    }
}
```

### 3. 使用`Arrays.copyOf`方法：

`Arrays`类提供了一个`copyOf`方法，它可以在一行代码中完成数组复制操作。

```java
import java.util.Arrays;

public class ArrayCopyExample {
    public static void main(String[] args) {
        int[] sourceArray = {1, 2, 3, 4, 5};
        int[] destinationArray = Arrays.copyOf(sourceArray, sourceArray.length);

        // 现在 destinationArray 是 sourceArray 的副本
    }
}
```

### 4. 使用`clone`方法：

每个数组对象都有一个`clone`方法，可以用来创建一个数组的副本。

```java
public class ArrayCopyExample {
    public static void main(String[] args) {
        int[] sourceArray = {1, 2, 3, 4, 5};
        int[] destinationArray = sourceArray.clone();

        // 现在 destinationArray 是 sourceArray 的副本
    }
}
```

请注意，上述方法中创建的新数组都是浅复制，即数组元素本身并没有被复制，只是数组的引用被复制了。如果数组中包含对象元素，那么原数组和副本数组会引用相同的对象。如果需要深度复制（复制数组元素本身），就需要自行编写逻辑来实现。

根据你的需求，选择适合的方法来复制数组。



## array reverse

在Java中，你可以使用不同的方法来实现数组的反转。下面介绍两种常见的方法。

### 1. 使用循环遍历进行反转：

这是一种基本的方法，通过交换数组元素的位置来实现反转。

```java
public class ArrayReverseExample {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5};

        int left = 0;
        int right = array.length - 1;

        while (left < right) {
            // 交换左右两侧的元素
            int temp = array[left];
            array[left] = array[right];
            array[right] = temp;

            // 移动指针
            left++;
            right--;
        }

        // 现在 array 已经被反转
    }
}
```

### 2. 使用`Collections.reverse`方法（适用于包装类数组）：

如果你处理的是包装类数组（例如 `Integer[]`），你可以使用`java.util.Collections`类提供的`reverse`方法。

```java
import java.util.Arrays;
import java.util.Collections;

public class ArrayReverseExample {
    public static void main(String[] args) {
        Integer[] array = {1, 2, 3, 4, 5};

        // 将数组转换为 List，并使用 Collections.reverse 进行反转
        Collections.reverse(Arrays.asList(array));

        // 现在 array 已经被反转
    }
}
```

请注意，`Collections.reverse`方法适用于包装类数组（例如 `Integer[]`），对于基本数据类型数组（例如 `int[]`），不能直接使用该方法。

选择适合你情况的方法来反转数组。



## 数组扩容

* 复制原来的数组然后在最后追加

* 使用`ArrayList`动态数组

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        // 创建一个空的 ArrayList
        ArrayList<Integer> numbers = new ArrayList<>();

        // 添加元素
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);

        // 访问元素
        int firstNumber = numbers.get(0);
        System.out.println("First number: " + firstNumber);

        // 修改元素
        numbers.set(1, 25);

        // 删除元素
        numbers.remove(0);

        // 遍历元素
        for (int num : numbers) {
            System.out.println(num);
        }
    }
}
```



## 多维数组



Java中的二维数组实际上是数组的数组，你可以将其想象为一个表格或者矩阵。二维数组在表示矩阵、游戏棋盘等情况下非常有用。下面是如何定义、初始化和使用二维数组的示例：

```java
public class TwoDimensionalArrayExample {
    public static void main(String[] args) {
        // 定义一个 3x3 的二维数组
        int[][] matrix = new int[3][3];

        // 初始化数组元素
        matrix[0][0] = 1;
        matrix[0][1] = 2;
        matrix[0][2] = 3;
        matrix[1][0] = 4;
        matrix[1][1] = 5;
        matrix[1][2] = 6;
        matrix[2][0] = 7;
        matrix[2][1] = 8;
        matrix[2][2] = 9;

        // 访问数组元素
        int value = matrix[1][2];  // 获取第二行第三列的元素，值为6

        // 打印数组内容
        for (int row = 0; row < matrix.length; row++) {
            for (int col = 0; col < matrix[row].length; col++) {
                System.out.print(matrix[row][col] + " ");
            }
            System.out.println();
        }
    }
}
```

在这个示例中，我们首先定义了一个3x3的整数二维数组`matrix`。然后，我们分别初始化了每个数组元素的值，并通过嵌套的循环遍历和打印了整个二维数组的内容。

你还可以使用更简洁的语法来定义和初始化二维数组：

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

这种方式可以更清晰地表示二维数组的结构。

二维数组的操作和一维数组类似，你可以使用索引来访问和修改元素。需要注意的是，二维数组的行数和列数可以是不同的，但在每一行中，列数必须相同。



# input and output

## input

- 可以通过创建`Scanner`类的实例来实现输入

```java
import java.util.Scanner;
```

## output

> 在前面的代码中，我们总是使用`System.out.println()`来向屏幕输出一些内容。
>
> `println`是 print line 的缩写，表示输出并换行。因此，如果输出后不想换行，可以用`print()`

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

- use the `for`

```java
for (int i=0; i<ns.length; i++)
```

- use the `for each`

```java
for (int n : ns)
```

# sort the array

- use the `Array.sort`

```java
import java.util.Arrays;
int[] ns = { 28, 12, 89, 73, 65, 18, 96, 50, 8, 36 };
Arrays.sort(ns);
```

> 排序是升序

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

- run the program

```java
$ java Main -version
v 1.0
```

# class

> tips:
>
> > 在一个 class 文件中只能存在一个和文件名一样名字的`public class`

> 在 Java 的类中也使用和 CPP 一样的`this`

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

# overload function

举个例子，`String`类提供了多个重载方法`indexOf()`，可以查找子串：

- `int indexOf(int ch)`：根据字符的 Unicode 码查找；
- `int indexOf(String str)`：根据字符串查找；
- `int indexOf(int ch, int fromIndex)`：根据字符查找，但指定起始位置；
- `int indexOf(String str, int fromIndex)`根据字符串查找，但指定起始位置。

# 继承

> 继承是面向对象编程中非常强大的一种机制，它首先可以复用代码。当我们让`Student`从`Person`继承时，`Student`就获得了`Person`的所有功能，我们只需要为`Student`编写新增的功能。
>
> Java 使用`extends`关键字来实现继承：

```python
class Person {
    private String name;
    private int age;

    public String getName() {...}
    public void setName(String name) {...}
    public int getAge() {...}
    public void setAge(int age) {...}
}

class Student extends Person {
    // 不要重复name和age字段/方法,
    // 只需要定义新增score字段/方法:
    private int score;

    public int getScore() { … }
    public void setScore(int score) { … }
}
```

- Java 只允许一个 class 继承自一个类，因此，一个类有且仅有一个父类。只有`Object`特殊，它没有父类。

- 和 CPP 一样存在三种访问的权限级别

## super

`super`关键字表示父类（超类）。子类引用父类的字段时，可以用`super.fieldName`。例如：

```java
class Student extends Person {
    public String hello() {
        return "Hello, " + super.name;
    }
}
```



* 注意,当一个函数是当前类没有的时候,会向上一级父类去找.



### 使用`super()`调用父类的构造函数

> 在 Java 中，任何`class`的构造方法，第一行语句必须是调用父类的构造方法。如果没有明确地调用父类的构造方法，编译器会帮我们自动加一句`super();`
>
> 所以,当父类不存在某个构造函数`(比如参数不存在的构造函数)`的时候,程序会报错

- 我们需要手动调用`super()`构造函数

```python
class Student extends Person {
    protected int score;

    public Student(String name, int age, int score) {
        super(name, age); // 调用父类的构造方法Person(String, int)
        this.score = score;
    }
}
```

- 子类不会继承父类的构造函数
- 必须放在子类构造函数的开头

## 阻止继承

正常情况下，只要某个 class 没有`final`修饰符，那么任何类都可以从该 class 继承。

## 限定哪些能够继承

> 从 Java 15 开始，允许使用`sealed`修饰 class，并通过`permits`明确写出能够从该 class 继承的子类名称。

## 向上转型

如果一个引用变量的类型是`Student`，那么它可以指向一个`Student`类型的实例：

```
Student s = new Student();
```

如果一个引用类型的变量是`Person`，那么它可以指向一个`Person`类型的实例：

```Java
Person p = new Person();
```

现在问题来了：如果`Student`是从`Person`继承下来的，那么，一个引用类型为`Person`的变量，能否指向`Student`类型的实例？

```
Person p = new Student(); // ???
```

测试一下就可以发现，这种指向是允许的！

这是因为`Student`继承自`Person`，因此，它拥有`Person`的全部功能。`Person`类型的变量，如果指向`Student`类型的实例，对它进行操作，是没有问题的！

这种把一个子类类型安全地变为父类类型的赋值，被称为向上转型（upcasting）。

向上转型实际上是把一个子类型安全地变为更加抽象的父类型：

```
Student s = new Student();
Person p = s; // upcasting, ok
Object o1 = p; // upcasting, ok
Object o2 = s; // upcasting, ok
```

注意到继承树是`Student > Person > Object`，所以，可以把`Student`类型转型为`Person`，或者更高层次的`Object`。

# 多态

> 在继承关系中，子类如果定义了一个与父类方法签名完全相同的方法，被称为覆写（Override）。

```java
class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}
```

## `final`

```java
final class Person {
    protected String name;
}

// compile error: 不允许继承自Person
class Student extends Person {
}
```

## 虚函数(抽象函数)

如果父类的方法本身不需要实现任何功能，仅仅是为了定义方法签名，目的是让子类去覆写它，那么，可以把父类的方法声明为抽象方法：

```java
class Person {
    public abstract void run();
}
```

# `interface`接口

在 Java 中，使用`interface`可以声明一个接口：

```java
interface Person {
    void run();
    String getName();
}
```

所谓`interface`，就是比抽象类还要抽象的纯抽象接口，因为它连字段都不能有。因为接口定义的所有方法默认都是`public abstract`的，所以这两个修饰符不需要写出来（写不写效果都一样）。

- 接口的派生类

当一个具体的`class`去实现一个`interface`时，需要使用`implements`关键字。举个例子：

```java
class Student implements Person {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    @Override
    public void run() {
        System.out.println(this.name + " run");
    }

    @Override
    public String getName() {
        return this.name;
    }
}
```

- 一个类可以实现多个接口类

| abstract class | interface               |                                |
| :------------- | :---------------------- | ------------------------------ |
| 继承           | 只能 extends 一个 class | 可以 implements 多个 interface |
| 字段           | 可以定义实例字段        | 不能定义实例字段               |
| 抽象方法       | 可以定义抽象方法        | 可以定义抽象方法               |
| 非抽象方法     | 可以定义非抽象方法      | 可以定义 default 方法          |

## 接口继承

一个`interface`可以继承自另一个`interface`。`interface`继承自`interface`使用`extends`，它相当于扩展了接口的方法。例如：

```
interface Hello {
    void hello();
}

interface Person extends Hello {
    void run();
    String getName();
}
```

此时，`Person`接口继承自`Hello`接口，因此，`Person`接口现在实际上有 3 个抽象方法签名，其中一个来自继承的`Hello`接口。

## 使用`default`方法

在接口中，可以定义`default`方法。例如，把`Person`接口的`run()`方法改为`default`方法：

```java
interface Person {
    String getName();
    default void run() {
        System.out.println(getName() + " run");
    }
}
```

# 静态`static`

> ---
>
> 在一个`class`中定义的字段，我们称之为实例字段。实例字段的特点是，每个实例都有独立的字段，各个实例的同名字段互不影响。
>
> 还有一种字段，是用`static`修饰的字段，称为静态字段：`static field`。
>
> 实例字段在每个实例中都有自己的一个独立“空间”，但是静态字段只有一个共享“空间”，所有实例都会共享该字段。

- 和 CPP 一样

## 关于接口`interface`的静态使用

因为`interface`是一个纯抽象类，所以它不能定义实例字段。但是，`interface`是可以有静态字段的，并且静态字段必须为`final`类型：

```java
public interface Person {
    public static final int MALE = 1;
    public static final int FEMALE = 2;
}
```

实际上，因为`interface`的字段只能是`public static final`类型，所以我们可以把这些修饰符都去掉，上述代码可以简写为：

```java
public interface Person {
    // 编译器会自动加上public statc final:
    int MALE = 1;
    int FEMALE = 2;
}
```



# `main `  function

> 主函数的实现
>
> * 主函数的调用来自JAVA虚拟机
> * 主函数需要是`public`,因为是来自外部的访问
> * 主函数需要是`static`,因为需要不创建这个实例
> * 可以接受外来的一些参数





# 包

* 在`src`文件夹那创建

> 我们使用`package`来解决名字冲突。
>
> Java 定义了一种名字空间，称之为包：`package`。一个类总是属于某个包，类名（比如`Person`）只是一个简写，真正的完整类名是`包名.类名`。

小明的`Person.java`文件：

```java
package ming; // 申明包名ming

public class Person {
}
```

小军的`Arrays.java`文件：

```java
package mr.jun; // 申明包名mr.jun

public class Arrays {
}
```

- 在写`import`的时候，可以使用`*`，表示把这个包下面的所有`class`都导入进来（但不包括子包的`class`）

```java
// 导入mr.jun包的所有class:
import mr.jun.*;
```

- 注意,我们一般不使用这种方式

> 还有一种 import static 的语法，它可以导入可以导入一个类的静态字段和静态方法.



## 命名规范

> `com.公司名.项目名.模块名`



# 作用域

> 和 CPP 一样

- 推荐把`private`方法放到后面，因为`public`方法定义了类对外提供的功能，阅读代码的时候，应该先关注`public`方法

## 嵌套类的作用域

> 由于 Java 支持嵌套类，如果一个类内部还定义了嵌套类，那么，嵌套类拥有访问`private`的权限

```java
public class Main {
    public static void main(String[] args) {
        Inner i = new Inner();
        i.hi();
    }

    // private方法:
    private static void hello() {
        System.out.println("private hello!");
    }

    // 静态内部类:
    static class Inner {
        public void hi() {
            Main.hello();
        }
    }
}
```

# 内部类

> 如果一个类定义在另一个类的内部，这个类就是内部类（Nested Class）.

```java
class Outer {
    class Inner {
        // 定义了一个Inner Class
    }
}
```

- 内部类的与普通类有个最大的不同，就是 Inner Class 的实例不能单独存在，必须依附于一个 Outer Class 的实例。

```java
public class Main {
    public static void main(String[] args) {
        Outer outer = new Outer("Nested"); // 实例化一个Outer
        Outer.Inner inner = outer.new Inner(); // 实例化一个Inner
        inner.hello();
    }
}

class Outer {
    private String name;

    Outer(String name) {
        this.name = name;
    }

    class Inner {
        void hello() {
            System.out.println("Hello, " + Outer.this.name);
        }
    }
}
```

> 观察上述代码，要实例化一个 Inner，我们必须首先创建一个 Outer 的实例，然后，调用 Outer 实例的 new 来创建 Inner 实例：

```java
Outer.Inner inner = outer.new Inner();
```

- 观察 Java 编译器编译后的.class 文件可以发现，Outer 类被编译为 Outer.class，而 Inner 类被编译为 Outer$Inner.class

## 匿名类

```java
class Polygon {
   public void display() {
      System.out.println("在 Polygon 类内部");
   }
}

class AnonymousDemo {
   public void createClass() {

      // 创建的匿名类继承了 Polygon 类
      Polygon p1 = new Polygon() {
         public void display() {
            System.out.println("在匿名类内部。");
         }
      };
      p1.display();
   }
}

class Main {
   public static void main(String[] args) {
       AnonymousDemo an = new AnonymousDemo();
       an.createClass();
   }
}
```

## Static Nested Class

最后一种内部类和 Inner Class 类似，但是使用 static 修饰，称为静态内部类（Static Nested Class）

> 用 static 修饰的内部类和 Inner Class 有很大的不同，它不再依附于 Outer 的实例，而是一个完全独立的类，因此无法引用 Outer.this，但它可以访问 Outer 的 private 静态字段和静态方法。如果把 StaticNested 移到 Outer 之外，就失去了访问 private 的权限。

# class path

因为 Java 是编译型语言，源码文件是.java，而编译后的.class 文件才是真正可以被 JVM 执行的字节码。因此，JVM 需要知道，如果要加载一个 abc.xyz.Hello 的类，应该去哪搜索对应的 Hello.class 文件。

所以，classpath 就是一组目录的集合，它设置的搜索路径与操作系统相关。例如，在 Windows 系统上，用;分隔，带空格的目录用""括起来，可能长这样：

`C:\work\project1\bin;C:\shared;"D:\My Documents\project1\bin"`
在 Linux 系统上，用:分隔，可能长这样：

`/usr/shared:/usr/local/bin:/home/liaoxuefeng/bin`

# jar 包

如果有很多.class 文件，散落在各层目录中，肯定不便于管理。如果能把目录打一个包，变成一个文件，就方便多了。

jar 包就是用来干这个事的，它可以把 package 组织的目录层级，以及各个目录下的所有文件（包括.class 文件和其他文件）都打成一个 jar 文件，这样一来，无论是备份，还是发给客户，就简单多了。

jar 包实际上就是一个 zip 格式的压缩文件，而 jar 包相当于目录。如果我们要执行一个 jar 包的 class，就可以把 jar 包放到 classpath 中：

java -cp ./hello.jar abc.xyz.Hello
这样 JVM 会自动在 hello.jar 文件里去搜索某个类。



# `null pointer`BUG

Java中容易造成空指针问题的原因主要是因为在Java中，引用类型的变量默认可以指向`null`，这意味着它们未指向任何有效的对象实例。当试图访问一个为`null`的对象引用上的成员变量、调用方法或进行其他操作时，就会触发空指针异常（`NullPointerException`）。以下是一些常见导致空指针问题的情况：

1. **未初始化的引用：** 如果你声明了一个引用变量，但在使用之前没有将其初始化为一个对象，那么它的默认值为`null`。在尝试访问这个引用上的任何成员时，都会触发空指针异常。

    ```java
    String str;  // 未初始化的引用，默认为 null
    int length = str.length();  // 触发空指针异常
    ```

2. **方法返回值为`null`：** 如果你调用一个方法，它返回了`null`，然后你尝试在该返回值上调用方法，也会触发空指针异常。

    ```java
    String str = someMethod();  // 假设 someMethod 返回 null
    int length = str.length();  // 触发空指针异常
    ```

3. **集合和数组元素为`null`：** 在集合类（如`ArrayList`、`HashMap`等）或数组中，元素可以为`null`。如果你尝试访问或操作一个为`null`的元素，就会触发空指针异常。

    ```java
    List<String> list = new ArrayList<>();
    list.add(null);
    int length = list.get(0).length();  // 触发空指针异常
    ```

4. **对象属性为`null`：** 如果一个对象的属性（成员变量）为`null`，而你试图访问该属性，同样会触发空指针异常。

    ```java
    class Person {
        String name;
    }
    
    Person person = new Person();
    int length = person.name.length();  // 触发空指针异常
    ```

为了避免空指针异常，你可以采取以下预防措施：

- 始终确保在使用对象引用之前进行初始化，确保它不是`null`。
- 在调用可能返回`null`的方法时，先检查返回值是否为`null`。
- 在访问集合、数组和对象属性之前，先检查是否为`null`。
- 使用条件语句或空值合并操作符（Java 8及更高版本）来处理可能为`null`的情况。

虽然Java中容易出现空指针问题，但遵循良好的编程实践和对潜在问题的警惕性可以帮助你避免这些问题。



## 处理`NullPointerException`

* 注意,这是一种代码编写时候的问题,所以,我们需要修改代码,而不是使用`catch`来隐藏问题.

成员变量在定义时初始化：

```
public class Person {
    private String name = "";
}
```

使用空字符串`""`而不是默认的`null`可避免很多`NullPointerException`，编写业务逻辑时，用空字符串`""`表示未填写比`null`安全得多。



返回空字符串`""`、空数组而不是`null`：

```
public String[] readLinesFromFile(String file) {
    if (getFileSize(file) == 0) {
        // 返回空数组而不是null:
        return new String[0];
    }
    ...
}
```

这样可以使得调用方无需检查结果是否为`null`。

如果调用方一定要根据`null`判断，比如返回`null`表示文件不存在，那么考虑返回`Optional<T>`：

```
public Optional<String> readFromFile(String file) {
    if (!fileExist(file)) {
        return Optional.empty();
    }
    ...
}
```

这样调用方必须通过`Optional.isPresent()`判断是否有结果。



## `Optional`类

* 用于解决空指针的问题.

`Optional`是Java 8引入的一个类，旨在解决空指针异常问题，并提供更好的处理可能为`null`的情况。它是一种包装类，用于表示一个可能存在 可能为空的值。通过使用`Optional`，你可以更明确地处理可能为空的对象，避免不必要的空指针异常。

以下是一些关于`Optional`的重要信息：

1. **创建`Optional`实例：** 你可以使用`Optional`类的静态方法来创建一个`Optional`实例，用于包装一个可能为空的值。例如：

   ```java
   Optional<String> optionalValue = Optional.ofNullable(someValue);
   ```

   这里的`someValue`可以是任何引用类型，包括可能为`null`的对象。

2. **检查是否存在值：** 使用`isPresent()`方法来检查`Optional`实例是否包含一个非`null`的值。

   ```java
   if (optionalValue.isPresent()) {
       // 执行操作
   }
   ```

3. **获取值：** 使用`get()`方法来获取`Optional`实例中的值。但要注意，如果值为`null`，调用`get()`方法将引发`NoSuchElementException`。

   ```java
   String value = optionalValue.get();
   ```

4. **避免空指针异常：** 使用`orElse()`方法来获取`Optional`中的值，如果值为`null`，则返回指定的默认值。

   ```java
   String value = optionalValue.orElse("default");
   ```

5. **处理值不存在的情况：** 使用`ifPresent()`方法结合Lambda表达式来处理值存在的情况。

   ```java
   optionalValue.ifPresent(val -> System.out.println("Value: " + val));
   ```

6. **链式处理：** `Optional`支持链式操作，你可以使用`map()`、`flatMap()`等方法对值进行处理，而无需担心空指针异常。

   ```java
   Optional<String> transformed = optionalValue.map(val -> val.toUpperCase());
   ```

7. **自定义处理：** 你可以使用`orElseGet()`、`orElseThrow()`等方法来进行更复杂的处理，根据具体情况返回默认值或抛出异常。

`Optional`并不是所有情况下都是必需的，但在你需要处理可能为空的值，并希望明确处理为空情况时，它是一个很有用的工具。要注意，过度使用`Optional`可能会使代码变得复杂，因此需要根据具体情况谨慎使用。



# 异常处理机制



从继承关系可知：`Throwable`是异常体系的根，它继承自`Object`。`Throwable`有两个体系：`Error`和`Exception`，`Error`表示严重的错误，程序对此一般无能为力，例如：

- `OutOfMemoryError`：内存耗尽
- `NoClassDefFoundError`：无法加载某个Class
- `StackOverflowError`：栈溢出

而`Exception`则是运行时的错误，它可以被捕获并处理。

某些异常是应用程序逻辑处理的一部分，应该捕获并处理。例如：

- `NumberFormatException`：数值类型的格式错误
- `FileNotFoundException`：未找到文件
- `SocketException`：读取网络失败

还有一些异常是程序逻辑编写不对造成的，应该修复程序本身。例如：

- `NullPointerException`：对某个`null`的对象调用方法或字段
- `IndexOutOfBoundsException`：数组索引越界

`Exception`又分为两大类：

1. `RuntimeException`以及它的子类；
2. 非`RuntimeException`（包括`IOException`、`ReflectiveOperationException`等等）



```
public byte[] getBytes(String charsetName) throws UnsupportedEncodingException {
    ...
}
```

在方法定义的时候，使用`throws Xxx`表示该方法可能抛出的异常类型。调用方在调用的时候，必须强制捕获这些异常，否则编译器会报错。

在`toGBK()`方法中，因为调用了`String.getBytes(String)`方法，就必须捕获`UnsupportedEncodingException`。我们也可以不捕获它，而是在方法定义处用throws表示`toGBK()`方法可能会抛出`UnsupportedEncodingException`，就可以让`toGBK()`方法通过编译器检查：

```java
public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) throws UnsupportedEncodingException {
        return s.getBytes("GBK");
    }
}
```



## 抛出异常

* 使用和`CPP`一样的方式,用`throw`语句抛出

```java
void process2(String s) {
    if (s==null) {
        throw new NullPointerException();
    }
}
```



### 处理异常之后再抛出异常

* 当你处理了之前捕获的异常然后再抛出一个异常的时候,之前的那个异常的信息会丢失
* 为了防止之前异常来源丢失

```java
		catch (NullPointerException e) {
            throw new IllegalArgumentException(e);
        }
```

> 这样写可以防止之前的异常信息丢失.
>
> * 保留一开始的情况!





## 子类和父类的异常类

存在多个`catch`的时候，`catch`的顺序非常重要：子类必须写在前面。例如：

```
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (IOException e) {
        System.out.println("IO error");
    } catch (UnsupportedEncodingException e) { // 永远捕获不到
        System.out.println("Bad encoding");
    }
}
```

对于上面的代码，`UnsupportedEncodingException`异常是永远捕获不到的，因为它是`IOException`的子类。当抛出`UnsupportedEncodingException`异常时，会被`catch (IOException e) { ... }`捕获并执行。



## `finally`

* 使用`finally`可以使得最后一定有被处理
* 可以存在不`catch`,直接`finally`的情况.

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (UnsupportedEncodingException e) {
        System.out.println("Bad encoding");
    } catch (IOException e) {
        System.out.println("IO error");
    } finally {
        System.out.println("END");
    }
}
```

注意`finally`有几个特点：

1. `finally`语句不是必须的，可写可不写；
2. `finally`总是最后执行。



## 当处理的不同的异常类的处理方式一样的时候

因为处理`IOException`和`NumberFormatException`的代码是相同的，所以我们可以把它两用`|`合并到一起：

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (IOException | NumberFormatException e) { // IOException或NumberFormatException
        System.out.println("Bad input");
    } catch (Exception e) {
        System.out.println("Unknown error");
    }
}
```



## 显示调用的堆栈

* 感觉`IDE`的报错提醒也是一样的.

```java
		try {
            process1();
        } catch (Exception e) {
            e.printStackTrace();
        }
```

通过`printStackTrace()`可以打印出方法的调用栈，类似：

```java
java.lang.NumberFormatException: null
    at java.base/java.lang.Integer.parseInt(Integer.java:614)
    at java.base/java.lang.Integer.parseInt(Integer.java:770)
    at Main.process2(Main.java:16)
    at Main.process1(Main.java:12)
    at Main.main(Main.java:5)
```



## `assertion`断言使用

* 是一个`关键字`,可以通过使用这个关键字,实现调试.



使用`assert`语句时，还可以添加一个可选的断言消息：

```java
assert x >= 0 : "x must >= 0";
```



### `assertion`断言不起作用

这是因为JVM默认关闭断言指令，即遇到`assert`语句就自动忽略了，不执行。

要执行`assert`语句，必须给Java虚拟机传递`-enableassertions`（可简写为`-ea`）参数启用断言。所以，上述程序必须在命令行下运行才有效果：

```
$ java -ea Main.java
Exception in thread "main" java.lang.AssertionError
	at Main.main(Main.java:5)
```

还可以有选择地对特定地类启用断言，命令行参数是：`-ea:com.itranswarp.sample.Main`，表示只对`com.itranswarp.sample.Main`这个类启用断言。

或者对特定地包启用断言，命令行参数是：`-ea:com.itranswarp.sample...`（注意结尾有3个`.`），表示对`com.itranswarp.sample`这个包启动断言。

实际开发中，很少使用断言。更好的方法是编写单元测试，后续我们会讲解`JUnit`的使用。



## `logging`日志

* 你可以通过向日志打印部分数据实现检查部分数据的状态.

```java
import java.util.logging.Level;
import java.util.logging.Logger;
public class Hello {
    public static void main(String[] args) {
        Logger logger = Logger.getGlobal();
        logger.info("start process...");
        logger.warning("memory is running out...");
        logger.fine("ignored.");
        logger.severe("process will be terminated...");
    }
}
```

> 需要从`java.util.logging`中导入数据.



# 反射

反射（Reflection）是Java语言的一个强大特性，允许程序在运行时检查和操作类、对象、方法和字段等的信息。通过反射，你可以动态地获取类的信息，创建对象，调用方法，访问字段，以及执行其他与类结构相关的操作，而无需在编译时明确地知道类的结构。

以下是一些关于Java反射的重要信息：

1. **获取类对象：** 使用`Class`类可以获取一个类的`Class`对象。`Class`对象包含了类的各种信息，如类名、包名、父类、接口、构造函数、方法、字段等。

   ```java
   Class<?> classObject = ClassName.class; // 或者使用 Class.forName("ClassName")
   ```

2. **实例化对象：** 使用反射可以通过`Class`对象创建类的实例。

   ```java
   Class<?> classObject = ClassName.class;
   Object instance = classObject.newInstance();
   ```

3. **获取和调用方法：** 可以使用`getMethod()`方法获取类中的方法，并使用`invoke()`方法调用方法。

   ```java
   Method method = classObject.getMethod("methodName", parameterTypes);
   Object result = method.invoke(instance, arguments);
   ```

4. **获取和设置字段：** 可以使用`getField()`方法获取类中的字段，并使用`get()`和`set()`方法访问和修改字段的值。

   ```java
   Field field = classObject.getField("fieldName");
   Object value = field.get(instance);
   field.set(instance, newValue);
   ```

5. **访问私有成员：** 使用反射可以访问类中的私有方法和字段，但需要设置相关的访问权限。

   ```java
   Method privateMethod = classObject.getDeclaredMethod("privateMethodName", parameterTypes);
   privateMethod.setAccessible(true);
   Object result = privateMethod.invoke(instance, arguments);
   ```

6. **操作数组、泛型和注解：** 反射还可以用于处理数组、泛型、枚举、注解等。

7. **动态代理：** 反射可以实现动态代理，允许你创建一个代理类来代替实际对象，以实现一些通用的行为。

尽管反射功能非常强大且灵活，但也需要小心使用，因为它会在一定程度上降低性能，使代码更加复杂，并且可能绕过编译时的类型检查。在使用反射时，务必了解相关的风险和最佳实践，以确保代码的可维护性和性能。



## `Class`类

每加载一种`class`，JVM就为其创建一个`Class`类型的实例，并关联起来。注意：这里的`Class`类型是一个名叫`Class`的`class`。它长这样：

```
public final class Class {
    private Class() {}
}
```

以`String`类为例，当JVM加载`String`类时，它首先读取`String.class`文件到内存，然后，为`String`类创建一个`Class`实例并关联起来：

```java
Class cls = new Class(String);
```

由于JVM为每个加载的`class`创建了对应的`Class`实例，并在实例中保存了该`class`的所有信息，包括类名、包名、父类、实现的接口、所有方法、字段等，因此，如果获取了某个`Class`实例，我们就可以通过这个`Class`实例获取到该实例对应的`class`的所有信息。

* 只能由`JVM`创建



如何获取一个`class`的`Class`实例？有三个方法：

方法一：直接通过一个`class`的静态变量`class`获取：

```
Class cls = String.class;
```

方法二：如果我们有一个实例变量，可以通过该实例变量提供的`getClass()`方法获取：

```
String s = "Hello";
Class cls = s.getClass();
```

方法三：如果知道一个`class`的完整类名，可以通过静态方法`Class.forName()`获取：

```java
Class cls = Class.forName("java.lang.String");
```



### 访问字段

我们先看看如何通过`Class`实例获取字段信息。`Class`类提供了以下几个方法来获取字段：

- Field getField(name)：根据字段名获取某个public的field（包括父类）
- Field getDeclaredField(name)：根据字段名获取当前类的某个field（不包括父类）
- Field[] getFields()：获取所有public的field（包括父类）
- Field[] getDeclaredFields()：获取当前类的所有field（不包括父类）







## `instanceof`

* 用`instanceof`不但匹配指定类型，还匹配指定类型的子类



# 集合(collection)

> 是由若干个元素构成的整体.



## `LIST`

> 我们常用`ArrayList`
>
> - 在末尾添加一个元素：`boolean add(E e)`
> - 在指定索引添加一个元素：`boolean add(int index, E e)`
> - 删除指定索引的元素：`E remove(int index)`
> - 删除某个元素：`boolean remove(Object e)`
> - 获取指定索引的元素：`E get(int index)`
> - 获取链表大小（包含元素的个数）：`int size()`

* 注意,不能使用`List[index]`的方式访问那个下标的元素,只能使用`get`方法



### 创建`LIST`

> 可以使用`of`方法初始化的时候直接创建
>
> ```java
> List<Integer> list = List.of(1, 2, 5);
> ```



### 遍历`LIST`

> 1. 和数组类型，我们要遍历一个`List`，完全可以用`for`循环根据索引配合`get(int)`方法遍历



> 2. 但这种方式并不推荐，一是代码复杂，二是因为`get(int)`方法只有`ArrayList`的实现是高效的，换成`LinkedList`后，索引越大，访问速度越慢。
>
> 所以我们要始终坚持使用迭代器`Iterator`来访问`List`。`Iterator`本身也是一个对象，但它是由`List`的实例调用`iterator()`方法的时候创建的。`Iterator`对象知道如何遍历一个`List`，并且不同的`List`类型，返回的`Iterator`对象实现也是不同的，但总是具有最高的访问效率。

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("apple", "pear", "banana");
        for (Iterator<String> it = list.iterator(); it.hasNext(); ) {
            String s = it.next();
            System.out.println(s);
        }
    }
}
```



> 3 . 使用`for each`的方式

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("apple", "pear", "banana");
        for (String s : list) {
            System.out.println(s);
        }
    }
}
```



### `List`转换为`Array`

> 把`List`变为`Array`有三种方法，第一种是调用`toArray()`方法直接返回一个`Object[]`数组

* 注意,这种方法会丢失原来的属性

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("apple", "pear", "banana");
        Object[] array = list.toArray();
        for (Object s : array) {
            System.out.println(s);
        }
    }
}
```

> 第二种方式是给`toArray(T[])`传入一个类型相同的`Array`，`List`内部自动把元素复制到传入的`Array`中

* 注意,你需要它变成的格式`T`不需要和之前定义`List`的时候的格式一样

```java
public class Main {
    public static void main(String[] args) {
        List<Integer> list = List.of(12, 34, 56);
        Integer[] array = list.toArray(new Integer[3]);
        for (Integer n : array) {
            System.out.println(n);
        }
    }
}
```



* tips

> 但是，如果我们传入类型不匹配的数组，例如，`String[]`类型的数组，由于`List`的元素是`Integer`，所以无法放入`String`数组，这个方法会抛出`ArrayStoreException`

> 如果传入的数组不够大，那么`List`内部会创建一个新的刚好够大的数组，填充后返回；如果传入的数组比`List`元素还要多，那么填充完元素后，剩下的数组元素一律填充`null`



### `Array`转换为`List`

把`Array`变为`List`就简单多了，通过`List.of(T...)`方法最简单：

```java
Integer[] array = { 1, 2, 3 };
List<Integer> list = List.of(array);
```

* 注意,返回的值是只读的
* 对只读`List`调用`add()`、`remove()`方法会抛出`UnsupportedOperationException`



# JVM

* 调用`main`方法的就是虚拟机



## 垃圾回收机制

* 注意,垃圾回收机制可以使用`GC`触发
* 不会阻塞进程

```java
System.gc() //
```



# 关键字



## `final`

使用`final`表示一个变量,那么这个变量是不可变的值



## `finally`

配合`try`,`catch`使用

在最后的被调用

 

## `Infinity`

出现在**除数为0的时候**,**可能出现`-Infinity`的情况**



## NaN

not a number

出现**被除数为0的时候**



# 基本数据类型缓存池

使用`Interger`对象的时候

1. 直接`new`一个实例,那么不会被缓存
2. 使用`valueOf`方法创建的实例,使用的相同的内存空间



字符串常量池

使用`""`创建的字符串使用的是**常量池**

使用`new String`创建出来的是一个新的

* 用来节约空间

* 使用`intern`方法返回的是**字符串常量池**中的引用



# 字符串拼接

使用**StringBuilder**的`append`方法

不使用`+`

* 可以提升性能

```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 100000; i++) {
    sb.append("六六六");
}
```



## 代码初始化块

使用`{}`包裹的代码可以不写在构造函数中也可以在构造的时候初始化,并且执行优先于构造函数



# 泛型

类似**模板化**

```java
class Arraylist<E> {
    private Object[] elementData;
    private int size = 0;

    public Arraylist(int initialCapacity) {
        this.elementData = new Object[initialCapacity];
    }
    
    public boolean add(E e) {
        elementData[size++] = e;
        return true;
    }
    
    E elementData(int index) {
        return (E) elementData[index];
    }
}
```



构建一个**泛型方法**



# 读取文件

```java
try {
    // 创建 File 对象，表示要扫描的文件
    File file = new File("docs/安装环境.md");
    Scanner scanner = new Scanner(file); // 创建 Scanner 对象，从文件中读取数据
    while (scanner.hasNextLine()) { // 判断文件中是否有下一行
        String line = scanner.nextLine(); // 读取文件中的下一行
        System.out.println(line); // 打印读取的行
    }
    scanner.close(); // 关闭 Scanner 对象
} catch (FileNotFoundException e) {
    System.out.println("文件不存在！");
}

```

