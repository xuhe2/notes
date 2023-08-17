> JAVA 风格和 C++类似

> tips:
>
> > JAVA 程序的开始一定是一个`public class Main` class 下的一个`public static void main(String[] args)`的方法

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

# array

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
