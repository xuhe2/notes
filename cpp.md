# C++

## 引用

是一个别名。

一旦定义为引用，可以写在左边，

* 右值引用：引用的是表达式，并且不因为表达式里面的值改变而改变。
* 指向常量的指针

```cpp
int num=1;
const int*p=&num;
num=100;  //OK
```

* 常量指针,指针的指向不能改变,但是可以用来改指针指向的内容.

```cpp
int* const p=;
```

* 指向常量的常指针



* 当强制类型转化的时候会生成一个临时变量

  ```cpp
  const int &x=1.1;
  ```

  这样`x=1`,并且不会改变.

  如果一个`double number` 在赋值的时候进行了强制类型转化的话,对原来的`number`的变化,常引用不会出现变化.

  优先指向的是`char[]`,`int` 

  auto 指向的应该是明确的,并且

  ```cpp
  auto a=1,b=1.1  //error
  ```

* 去除一次const

  ```cpp
  const int &num=1;
  const_cast<int&>(num);  //去掉const
  ```

  ```cpp
  int &num=a;
  reinterpret_cast<int&>(num);  //完全不同的类型转换
  ```

  ```cpp
  dynamic_cast<type>(object);
  ```

* 缺省值,从左到右边,右边不能没有.



* 函数的返回值是引用

可以作为左值。

```cpp
int& func(int n);
```

* 函数重载

> 在类型不匹配的时候,会先类型转换
>
> > 如果只有函数的返回值不一样叫做函数重定义

```cpp
int f(int a);
int f(const int a);
//error 重定义
int f(int *a);
int f(const int *a);
//OK
int f(int &a);
int f(const int &a);
//OK
```



```cpp
inline func();
```

函数的体量比较小的时候使用



* `lambda` 

```cpp
[capture list](params list)mutable exception->return type{function body};
```

括号内部是传入的参数

在[]可以使用&/=使他可以访问外部变量,没有就不行

= 是复制过来的, & 是引用过来的



ADT(抽象数据类型)

* 抽象 : 注意外部接口
* 封装 : 注意内部实现

> class : 用来实现封装



##  设计一个CLASS

> 其他的类的指针或者引用可以在本类中成为成员
>
> 但是
>
> 本类的指针或者引用不能作为数据成员
>
> 不可以使用auto extern , 但是可以使用`decaltype` 

```cpp
return-type class-name::func(type-name){  //在外部实现内部的代码
}
```



把内部的函数的开头或者结尾加上const,`那不可以通过它修改本类的数据` 

`对于一个类创造,其中的成员函数都是使用的一样的空间.` 

```cpp
void func()const;
```



* 类的对象的赋值或者类的对象的指针的赋值是按位复制



## constructor and destructor

* constructor is a special function . 用来在对象被创建的时候初始化的函数
* destructor 用来在对象不用的时候销毁这个对象的函数



> 构造函数的名字和类的名字一样并且没有返回值,不能定义为`const` (const函数不能修改类的内容)
>
> 构造函数可以被重载
>
> 类里面的初始值的优先级高于类里面的构造函数,并且构造函数只能被系统调用.
>
> 没有自己定义构造函数,系统会生成空的构造函数.`do-nothing constructor`

```cpp
class-name(param_list){function-body}
```

* 没有return-type.

```cpp
class-name var(param-list);  //生成一个对象
```

* 使用new创建对象的时候也会被调用构造函数

* 一旦自己定义了构造函数,系统不会创建无参数的构造函数,所以,我们要自己写上无参数的构造函数.(或者可以使用缺省值)

* 构造函数要定义为public,因为在调用的时候是在类外面调用.

* 没有参数的构造函数不用写().

```cpp
class-name var = 10;  //=class-name var(10);
//需要一个构造函数
class-name(int var){}
```



初始化列表的初始化

> 初始化列表的执行顺序是按照你类里面的数组的顺序初始化的

```cpp
class MyClass {
  public:
    MyClass(int a, int b, int c)
      : x(a), y(b), z(c)
    {
      // constructor code
    }
  private:
    int x, y, z;
};
```

> 对于`const` , `引用成员` ,and so on必须这样.



* 委托构造函数

```cpp
class MyClass {
  public:
    MyClass(int a, int b, int c)
      : x(a), y(b), z(c)
    {
      // constructor code
    }
    MyClass(int a, int b)
      : MyClass(a, b, 0)
    {
      // constructor code
    }
  private:
    int x, y, z;
};
```



* destructor(析构函数)

> 析构函数不可以被重载

```cpp
~class-name(){}
```

* 在结束的时候自动调用

> 构造的时候是按照你生成的顺序,析构的时候是堆栈的顺序

> 在类里面动态申请的内存经常在析构函数里面delete



赋值的运算符 =

如果没有自己定义的话,系统生成一个,按位赋值.(在动态申请的内存大小赋值的时候会出问题,有指针的时候也会出问题)

```cpp
class-name& operator = (const class-name& var);  
var=var;  //拷贝的运算符
```

```cpp
class-name var = var ; //拷贝构造函数
```



* 浅拷贝(shallow copy) : 按位拷贝

* 深拷贝 : 自己写的.



```cpp
#include<utility>
int&& x=move(y);
```



* 利用已经有了的类来构造还没有被创建的对象

```cpp
class-name var = var;
```



> 移动函数:
>
> * 都是可以移动的
> * 没有显式的构造和析构函数
>
> 会默认生成





> `移动构造函数为什么要把原来的对象里面的指针变为空指针`
>
> - [为了避免内存泄漏。如果不把原来的对象里面的指针变为空指针，那么当原来的对象被析构时，它会释放掉它指向的内存，导致新对象的指针也失效.
> - [为了表明所有权的转移。移动构造函数的目的是把原来的对象里面的资源转移给新对象，而不是共享。所以把原来的对象里面的指针变为空指针，就表示它不再拥有那块资源.



> - [当我们需要用一个**已有的对象**来初始化另一个对象时，就会调用拷贝构造函数].
> - [当我们需要把一个对象作为**函数的参数**传递时，如果参数不是引用类型，就会调用拷贝构造函数
> - [当我们需要把一个对象作为**函数的返回值**返回时，如果返回值不是引用类型，就会调用拷贝构造函数]



* 在使用的时候如果没有定义移动函数,那么它不会调用移动函数.



## static 静态数据成员和成员函数

* `关键字使用一次` 



* 静态的成员函数`只能访问` 静态的数据成员.

> - 静态成员函数不属于任何对象，它是随着类的加载而加载的，它只能访问同样随着类加载而存在的静态成员变量。
> - 普通成员函数属于某个对象，它是在对象创建时才分配内存的，它可以访问所有成员变量，包括静态和非静态的。
> - 调用普通成员函数时，系统会隐式地传递一个this指针，指向当前对象的地址。而调用静态成员函数时，不需要this指针，因为它与任何对象都无关。





> 在类内部申明的时候加上`static` 

* 不需要对象创建就可以使用`静态的成员函数` .

* 可以`通过类名直接访问`不需要对象.



## THIS指针

```c++
a = 10;
this -> a = 10;
```

```c++
void func(int a);
=
void func(this* p , int a);
```

> 一个函数的静态参数是不自带THIS指针的,所以不能访问对象里面的东西.

```c++
class & func(){
    return *this;  //返回对象的引用
}
```





## 把对象作为参数传递的时候

* 是在PUBLIC里面调用.



> 当类作为函数的参数传递的时候,初始化的时候不仅要完成自己的初始化,也要完成自己的内部的对象的初始化.

```c++
class CExample {
public:
    int a;
    float b;
    //构造函数初始化列表
    CExample(): a(0),b(8.8) {}
};
```



> 聚合的关系用的一般是:指针
>
> 关联:用的是内部的对象的创建.



## 友元函数

* `friend` 只用定义一次.
* 可以被写在`private` 

```cpp
friend int func(class-name a){
    //可以直接访问a的私有对象
}
```

> 用于多次传递内容的时候

> friend function 可以是非成员函数，也可以是成员函数.

example

```cpp
class B; // forward declaration

class A {
   public:
      void Func1(B& b);
};

class B {
   private:
      int _b;
   public:
      B() : _b(0) {}
      friend void A::Func1(B& b);
};

void A::Func1(B& b) {
   // access private member of B
   cout << "B::_b = " << b._b << endl;
}
```

## 友元类

```cpp
friend class-name var;
```



友元类（Friend Class）是C++中的一种特殊类关系，它允许一个类（称为友元类）访问另一个类（称为被友元类）的私有成员和保护成员，即使这些成员在普通情况下是不可访问的。

通过将一个类声明为另一个类的友元类，被友元类可以授予友元类的成员函数或整个类对其私有或保护成员的访问权限。这种特性在某些情况下是很有用的，例如需要在两个类之间共享信息或实现紧密耦合的功能。

下面是友元类的一般示例：

```cpp
class FriendClass {
public:
    // 友元类可以访问被友元类的私有成员和保护成员
    void accessPrivateMember(OtherClass& obj) {
        int privateData = obj.privateData;
        obj.privateMethod();
    }
};

class OtherClass {
private:
    int privateData;

    // 友元类的声明
    friend class FriendClass;

    // 友元函数的声明
    friend void friendFunction(OtherClass&);

    // 友元类可以访问私有成员
    void privateMethod() {
        // 执行某些操作...
    }
};

// 友元函数可以访问被友元类的私有成员和保护成员
void friendFunction(OtherClass& obj) {
    int privateData = obj.privateData;
    obj.privateMethod();
}
```

在上述示例中，`OtherClass` 类被声明为 `FriendClass` 的友元类。这意味着 `FriendClass` 类可以访问 `OtherClass` 的私有成员和保护成员，例如 `privateData` 成员和 `privateMethod()` 方法。

此外，示例还展示了一个友元函数 `friendFunction()`，它也可以访问 `OtherClass` 的私有成员和保护成员。友元函数的声明需要在 `OtherClass` 类中进行。

需要注意的是，友元类关系是单向的，即被友元类不自动成为友元类。如果需要互相访问，需要分别声明友元类。

友元类的使用应该谨慎，因为它可以突破类的封装性原则，增加代码的复杂性和耦合度。一般情况下，应该优先考虑使用封装和公共接口来实现类之间的通信和访问控制。友元类应该作为一种较少使用的特殊情况下的设计选择。

## 继承

> `is a relationship` 关系

> 从一个已有的类继承
>
> > 可以增加积累的数据成员和成员函数
> >
> > 可以重载和重定义基类的函数
>
> > 不可以继承基类的构造函数和析构函数
> >
> > 不可以继承基类的友元函数
> >
> > 不可以继承基类的静态成员函数和静态成员

* 公有继承

```cpp
// base class
class Animal {
  public:
    // public member function
    void eat() {
      cout << "I can eat!" << endl;
    }

  protected:
    // protected member function
    void sleep() {
      cout << "I can sleep!" << endl;
    }
};

// derived class
class Dog : public Animal {
  public:
    // public member function
    void bark() {
      cout << "I can bark! Woof woof!" << endl;
    }
};
```

> 不做说明类默认是私有继承,结构体是公有继承

> `private`在继承的时候不能直接被访问,但是`protected` 可以,`直接派生类` (但是间接的派生类不可以访问)就可以访问了.(但是对外部都是隐藏的)

> 在任何情况下,私有的成员都不会被继承

* 使用`using` 来实现

```cpp

// base class
class Base {
  public:
    // public member function
    void print() {
      cout << "Base" << endl;
    }
};

// derived class
class Derived : public Base {
  public:
    // using declaration
    using Base::print;

    // public member function
    void print(int x) {
      cout << "Derived: " << x << endl;
    }
};
```

> 在私有继承的时候,接口的名字可以被改变.(但是实现方式是一样的)

* 阻止继承

```cpp
class var-name final{};
```

* 覆盖`override/redefinition` 

> 重定义的时候会覆盖掉基类的相关版本
>
> > 重定义是实现的是内域
> >
> > 原本的是外域
> >
> > > 内域的优先级高于外域

* * 在覆盖(改变接口或者扩展实现接口)的时候,就不是`is a relationship`关系.

> 在继承的时候如果在派生类中使用了同名的函数,会直接覆盖原来的函数,所以我们需要使用`using class-name::func-name` 来实现重载.
>
> > 但是从基类继承的私有成员不能使用`using` 来实现可见是不行的.

> 友元是一种C++中的特殊功能，它可以让一个函数或者一个类访问另一个类的私有或者保护的成员。为了实现这种功能，需要在被访问的类中使用friend关键字来声明哪些函数或者类是它的友元

### class scope(类域)

> 本质是嵌套的类,后面派生类在初始类的里面.
>
> 从里面开始找函数.

* 基类或者对象成员的初始化要在初始化列表里面.

* 如果基类中自定义了没有参数的构造函数,需要使用初始化列表构造函数.
* 派生类只负责直接基类的构造.(递归)

* 可以使用`using` 来继承构造函数.

> 按照声明/继承的顺序

> assignment copy and move operation can not be created auto when has the virtual des-func.

```cpp
class-name & operator = (const class-name & ){
    return *this;
}
```

> 派生类对象的可以被赋值给基类(截断)
>
> 派生类对象可以用来当基类的指针.
>
> 派生类可以用来当基类的引用.
>
> > 本质是当指针来指向开头

* 隐式类型转换

```cpp
drived-name *  = &base-name;
drived-name &  = base-name;
```

> C++中常用的类型转换运算符有四个，分别为：dynamic_cast、const_cast、static_cast、reinterpret_cast。² dynamic_cast主要用于将一个指向基类的指针转换为指向派生类的指针，或者将一个指向基类的引用转换为指向派生类的引用。¹ const_cast主要用于将const或volatile限定符去掉。¹ reinterpret_cast可以将一个指针转换为任意类型的指针，但是这种转换是不安全的，因为它不会进行任何类型检查。¹ static_cast可以将一个表达式转换为指定类型，但只能在编译时进行类型检查，不能在运行时进行类型检查。
>

### 多重继承

> 多重继承是指从多个直接基类中产生派生类。一个派生类如果只继承一个基类，称作单继承，那么如果继承了多个基类，就称作多继承。C++支持多重继承，但是Java不支持对类中多重继承的支持¹。多重继承容易让代码逻辑复杂、思路混乱，一直备受争议²。
>
> > 在调用在多个基类中都有定义的同名的函数的时候,需要指定.

```cpp
class-name.base-name::func();
```

> 按照继承的顺序来初始化.

### 虚基类(virtual base classes)

> 继承成员的重复性出问题.

```cpp
virtual public name;
```

> 防止出现多个副本.

* !虚基类先于非虚基类构造.! (8-1 code)

## 运算符重载

```cpp
type operator+(type,type);
```

> 只有先前定义好的可以被重载.

> `.`不可以重载,`::`也不可以.

> 特殊的函数,operator op是函数名字.
>
> 静态的重载是没有this指针的,在单个参数的时候是传入this指针的,所以少一个参数.
>
> `=`,`&`,`->`,`.`都是预先定义好的.

```cpp
a=b+c
a=b.operator+(c);
```

* 定义为友元之后,可以使重载的运算符直接访问私有的部分.

```cpp
2+a;
::operator+(type(2),a);  //先调用构造函数.
```

> ++运算符重载

```cpp
type operator++();  //前自增
type operator++(int);  //后自增
```

* 使用友元构造函数

```cpp
class MyClass {
public:
    MyClass(int value) : m_value(value) {}
    int getValue() const {
        return m_value;
    }
    friend MyClass& operator++(MyClass& obj);
    friend MyClass operator++(MyClass& obj, int);
private:
    int m_value;
};

MyClass& operator++(MyClass& obj) {
    ++obj.m_value;
    return obj;
}

MyClass operator++(MyClass& obj, int) {
    MyClass temp(obj);
    ++obj.m_value;
    return temp;
}
```

* 类型转换运算符

```cpp
class Complex {
public:
    Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}
    operator double() const { return real; } // 类型转换运算符
private:
    double real, imag;
};

int main() {
    Complex c(3.14, 2.72);
    double d = c; // 使用类型转换运算符将 Complex 对象转换为 double 类型
    std::cout << d << std::endl; // 输出 3.14
    return 0;
}
```

* 函数调用运算符重载(只能作为非静态的成员函数)

```cpp
class Multiplier {
public:
    Multiplier(int factor) : factor_(factor) {}
    int operator()(int value) {
        return factor_ * value;
    }
private:
    int factor_;
};

int main() {
    Multiplier m(10);
    int result = m(5); // 使用函数调用运算符，相当于调用 m.operator()(5)
    std::cout << result << std::endl; // 输出 50
    return 0;
}
```

* 输入输出流的双目运算符重载

```cpp
class Person
{
public:
    Person(std::string name, int age) : name(name), age(age) {}

    friend std::ostream &operator<<(std::ostream &os, const Person &person)
    {
        os << "Name: " << person.name << ", Age: " << person.age;
        return os;
    }

private:
    std::string name;
    int age;
};
```



## 使用内部的类实现的重载

> 重载的多肽,包括函数的重载和运算符的重载.

### 虚拟函数

* 可以在基类函数中使用派生类的函数.

```cpp
class Base {
public:
    virtual void func();
};
```

```cpp
class Derived : public Base {
public:
    void func();  // 重新定义虚函数
};
```

* 可以使用基类截断派生类的指针,来传递值.

> 1. 静态绑定(在编译的时候实现绑定)
>
> > 通过函数和运算符重载.
>
> 1. 动态绑定(在运行的时候实现绑定)
>
> > 使用继承和虚函数实现的.

* 不使用虚拟函数,直接使用的话是指针截断了,然后是基类的指针,无法使用派生类的函数.
* 或者使用强制类型转换,转换成为原来的类的指针.
* 使用了虚拟函数之后,不论是指针截断还是引用截断都是调用的是派生类的函数.

> 使用虚拟函数之后,相当于告诉是动态绑定.
>
> 在继承中,然后,在派生类中实现的是声明了的接口.

* 有些时候,就是要实现重载的时候,但是写错了,写出了一个新的函数,我们可以使用`override`来限定这个就是重载.

```cpp
class Base {
public:
    virtual void foo() { cout << "Base::foo" << endl; }
};

class Derived : public Base {
public:
    void foo() override { cout << "Derived::foo" << endl; }
};

int main() {
    Base* ptr = new Derived();
    ptr->foo();  // 调用 Derived::foo()，因为 Derived::foo() 覆盖了 Base::foo()
    return 0;
}
```

* 成员函数也可以设置成final,不可以被继承

* `一旦定义为虚拟之后,这个类和它的所有的派生类都有虚拟特性`

> * 只对当前级的类是否有虚拟特性有关.

```cpp
//只有在直接赋值的时候才能记忆原本的派生类类型
B *pb = d;  //OK
B b = d;
pb = &b;  //error
```



* 调用的函数的时候,从当前的级开始往下找,函数里面调用函数也是从当前的函数级别开始往下找. `?`

> 构造函数,静态成员函数不能被定义为虚构函数. `?` 
>
> > 构造函数和静态成员函数不能被定义为虚函数，因为虚函数依赖于运行时多态性，而构造函数和静态成员函数不涉及对象实例，无法通过对象进行调用。在C++中，虚函数的调用是通过对象指针或引用进行的，而在构造函数和静态成员函数中无法使用对象指针或引用进行调用。此外，静态成员函数也不属于任何对象，因此无法被定义为虚函数。
>
> 内联函数不能定义为虚拟函数.

* 析构函数可以被定义为虚函数.

> 析构函数能保证析构的时候,完全析构.
>
> * 有些时候对派生类的析构不是彻底的析构.

### 纯虚函数(do-nothing or pure virtual function)和抽象类

* 纯虚函数是指在基类中只声明函数原型而不提供函数实现的虚函数。它的声明形式为在函数原型后加上 `= 0`，例如：

```cpp
virtual void myFunction() = 0;
```

纯虚函数没有实际的函数体，它的作用是为派生类提供一个接口，让派生类必须实现该函数。如果派生类没有实现纯虚函数，那么该派生类也将成为抽象类，无法被实例化。

纯虚函数经常用于定义抽象基类，它只包含接口定义，而没有具体的实现。派生类必须实现这些接口，才能被实例化。这种机制可以有效地实现接口的多态性和继承。

需要注意的是，纯虚函数必须在基类中声明，并且不能直接被调用。如果在基类中定义了纯虚函数的实现，那么该函数将不再是纯虚函数，而是一个普通的虚函数。



* 抽象类(abstract class)

> 抽象类是指包含至少一个纯虚函数的类。抽象类不能被实例化，只能作为基类使用，用于定义接口规范。抽象类的目的是为了让派生类必须实现其定义的接口，从而达到多态性和继承的目的。
>
> 抽象类一般定义了接口的规范，但是没有提供具体的实现。派生类必须实现抽象类中定义的纯虚函数才能被实例化。如果派生类没有实现抽象类中的纯虚函数，那么该派生类也将成为抽象类，无法被实例化。
>
> 抽象类可以包含非纯虚函数，也可以包含成员变量、静态成员、成员函数和构造函数。抽象类的成员函数可以是虚函数或者非虚函数。如果一个抽象类中只有纯虚函数，那么它也被称为接口类。
>
> 需要注意的是，抽象类不能被实例化，因为它包含了未实现的纯虚函数。因此，抽象类只能作为基类来使用，不能直接创建对象。如果想要创建对象，必须先定义一个派生类，并实现其定义的纯虚函数。

* 直到某一个级别有具体实现了才算是非抽象类,继承之前的但不做定义都是抽象基类

### 运行时类型信息(RTTI)

> 1. 是公有的基类
> 2. 是公有的派生类
> 3. 和被转换的类是同一个基类的派生类.

* `typeid`函数 `?`

```cpp
#include <iostream>
#include <typeinfo>

int main() {
    int i = 42;
    const std::type_info& i_type = typeid(i);
    std::cout << "i's type: " << i_type.name() << std::endl;

    double d = 3.14;
    const std::type_info& d_type = typeid(d);
    std::cout << "d's type: " << d_type.name() << std::endl;

    return 0;
}
```



## 泛型编程

* instantiation

> 实例化



* 在`template`中出现过的参数,在后面的参数列表中也一定要出现一次.



* 使用模板化的函数,一般不分离函数和函数模板的实现.

> 同一种类型参数的模板函数的实例化是在它调用的第一次.
>
> 不同类型的参数在模板函数的实例化的时候,会多次实例化



* 当声明和实现分离的时候

```cpp
// template_class.h

#ifndef TEMPLATE_CLASS_H
#define TEMPLATE_CLASS_H

template<typename T>
class TemplateClass {
public:
    TemplateClass(T value);
    void PrintValue();

private:
    T m_value;
};

#endif  // TEMPLATE_CLASS_H
```

```cpp
// template_class.cpp

#include "template_class.h"
#include <iostream>

template<typename T>
TemplateClass<T>::TemplateClass(T value) : m_value(value) {}

template<typename T>
void TemplateClass<T>::PrintValue() {
    std::cout << "Value: " << m_value << std::endl;
}
```





* 它不会自动的数据类型的参数转换.(传参的时候)

* 在返回的时候可以做类型转换.



### 类型参数



### 非类型参数

```cpp
template<class T,int number>
```



在C++的泛型编程中，有两种参数类型可以在模板中使用：类型参数（type parameter）和非类型参数（non-type parameter）。

1. 类型参数（Type Parameter）：
类型参数是指在模板定义中使用的表示类型的参数。它允许我们编写通用的代码，能够处理多种不同的数据类型。类型参数使用占位符类型（如`T`、`U`、`typename`）来表示，在模板实例化时，可以通过指定具体的类型来替换这些占位符。

例如，下面是一个使用类型参数的函数模板示例：
```cpp
template <typename T>
T max(T a, T b) {
  return (a > b) ? a : b;
}
```
在这个例子中，`T` 是一个类型参数，可以用来表示不同的数据类型。调用 `max` 函数时，编译器会根据实际参数的类型生成对应的函数实例。

2. 非类型参数（Non-type Parameter）：
非类型参数是指在模板定义中使用的表示常量或枚举值的参数。它允许我们在模板中使用特定的常量或枚举值作为参数，从而实现对常量的泛化处理。

例如，下面是一个使用非类型参数的类模板示例：
```cpp
template <int N>
class Array {
  int data[N];
public:
  // ...
};
```
在这个例子中，`N` 是一个非类型参数，表示数组的大小。使用非类型参数可以在编译时就确定数组的大小，从而提供更高效的代码。

非类型参数可以是整型、指针、引用或枚举类型，但不能是浮点型、类类型或数组类型。非类型参数在模板实例化时必须是常量表达式，因为它们的值在编译时需要确定。

> 1. 浮点类型（float、double等）：由于浮点数的值可以是非常复杂的，无法在编译时期确定，因此不能作为非类型参数。
> 2. 类类型（class、struct、union等）：类类型的对象需要在运行时动态创建和销毁，无法在编译时期确定大小和属性，因此不能作为非类型参数。
> 3. 字符串类型（char*、std::string等）：字符串是一组字符的序列，长度和内容可以在运行时进行修改，无法在编译时期确定，因此不能作为非类型参数。
> 4. 函数类型（函数指针、成员函数指针等）：函数和函数指针具有运行时的动态特性，无法在编译时期确定函数的地址和行为，因此不能作为非类型参数。

通过使用类型参数和非类型参数，可以编写出更加通用和灵活的模板代码，以适应不同的需求和数据类型。这为泛型编程提供了更大的灵活性和扩展性。



* 对于非类型的参数,一定要传入一个常量

* ```cpp
  template<int number>
  .....
  
  func(1); //correct
  int a=1;
  func(a); //error
  ```



* 对模板函数也可以实现重载`需要参数的个数不一样`



### 模板类

```cpp
template <typename T>
class Stack {
private:
  T* data;
  int top;
  int capacity;
public:
  Stack(int size) : capacity(size), top(-1) {
    data = new T[size];
  }
  ~Stack() {
    delete[] data;
  }
  void push(T item) {
    if (top < capacity - 1) {
      data[++top] = item;
    }
  }
  T pop() {
    if (top >= 0) {
      return data[top--];
    }
    return T();
  }
};

int main() {
  Stack<int> intStack(10);  // 实例化一个整数类型的栈
  intStack.push(5);
  intStack.push(10);
  intStack.push(15);
  int poppedItem = intStack.pop();
  // ...

  Stack<double> doubleStack(5);  // 实例化一个双精度浮点数类型的栈
  doubleStack.push(3.14);
  double poppedItem = doubleStack.pop();
  // ...

  return 0;
}
```

* 在实现和库分离的时候

```cpp
#include "stack.h"

template <typename T>
Stack<T>::Stack(int size) : capacity(size), top(-1) {
  data = new T[size];
}

template <typename T>
Stack<T>::~Stack() {
  delete[] data;
}

template <typename T>
void Stack<T>::push(T item) {
  if (top < capacity - 1) {
    data[++top] = item;
  }
}

template <typename T>
T Stack<T>::pop() {
  if (top >= 0) {
    return data[top--];
  }
  return T();
}
```



* 在类模板中也是调用之后才会实例化.



* 模板参数也可以使用缺省值

```cpp
template <typename T = int, int N = 10>
class Array {
private:
  T data[N];
public:
  // ...
};

int main() {
  Array<> arr1;  // 使用默认参数 int 和 10 实例化 Array
  Array<double, 5> arr2;  // 显式指定参数 double 和 5 实例化 Array
  // ...
  return 0;
}
```



## STL

* container

> 用来存储数据.

> `rbegin()`指向末尾
>
> * `mutimap`:一个`key`指向多个值.



> `vectorname.assign(3,0)`前三个数字赋值成0



> `merge()`合并两个列表.
>
> > 在原来已经排序好了的时候,自动排序.
>
> ```cpp
> L2,merge(L1);
> ```



* `mutlimap`

```cpp
#include <iostream>
#include <map>

int main() {
  std::multimap<int, std::string> students;

  // 插入元素
  students.insert({ 1001, "Alice" });
  students.insert({ 1002, "Bob" });
  students.insert({ 1003, "Alice" });
  students.insert({ 1004, "Charlie" });

  // 遍历输出
  for (const auto& pair : students) {
    std::cout << "ID: " << pair.first << ", Name: " << pair.second << std::endl;
  }

  // 查找特定键的元素
  auto range = students.equal_range(1001);
  for (auto it = range.first; it != range.second; ++it) {
    std::cout << "ID: " << it->first << ", Name: " << it->second << std::endl;
  }

  return 0;
}
```



> `distance()`可以用来返回两个迭代器之间的差距.





## 异常处理

> Synchronous error : 同步的错误



### throw

```cpp
throw(exception);
throw exception;
//精准匹配
```



### try

> 使用`try`的时候,一旦出现问题,立刻跳出去查找`catch`语句.(跳出之后不会回来)
>
> 找到第一个类型匹配成功的`catch`语句

> 出现问题之后找到第一个匹配的`catch`,然后,运行`catch`之后的所有的语句(不会终止代码的运行)

* 在找不到`catch`的时候,使用`abort`函数默认退出程序.

### catch

> 参数只能有一个,用来精准匹配抛出的异常.
>
> 可以`从非常量到常量`,`从派生类到基类`,`函数转换成指向函数的指针`
>
> * 有且仅有这三种类型的默认转换.
>
> 所以,一个`catch`只能针对一个错误类型.

> 参数甚至可以只有类型,不带名称(如果不使用这个`e.what()`)



> 我们可以捕获所有的错误类型,来防止默认的停止.

在 C++ 中，可以使用通用的异常处理器 `catch (...)` 来捕获并处理所有类型的异常。`catch (...)` 块是一个特殊的异常处理块，它可以捕获任意类型的异常。

下面是一个使用 `catch (...)` 捕获所有异常类型的示例：

```cpp
try {
    // 代码块可能会抛出异常
} catch (...) {
    // 处理所有类型的异常
}
```

在上述示例中，`try` 块中的代码可能会抛出异常。如果抛出异常，程序会进入 `catch (...)` 块，并执行其中的处理代码。通过使用 `catch (...)`，可以捕获任何类型的异常，并在处理代码中采取适当的操作，如输出错误信息、记录日志、进行清理操作等。

需要注意的是，在使用 `catch (...)` 捕获所有异常时，程序会失去对异常类型的具体信息，因此无法针对不同类型的异常进行特定的处理。因此，建议在实际代码中尽量使用具体的异常类型进行捕获和处理，以便更好地理解和处理异常情况。只有在确实需要处理所有类型的异常，且对异常类型没有特定的处理需求时，才使用通用的异常处理器 `catch (...)`。



> 再次抛出异常
>
> 空的`throw`只能在`catch`中出现
>
> ```cpp
> throw;
> ```
>
> 如果希望错误信息进行修改,那么应该使用引用的方式(就像函数一样,传参数的形式)
>
> 可以认为是一个函数

二次抛出异常（rethrowing exception）是指在异常处理块内部重新抛出已捕获的异常，允许异常在更高层次的异常处理器中被捕获和处理。

在 C++ 中，可以使用 `throw` 关键字来重新抛出已捕获的异常。通常，这种情况下会在 `catch` 块中使用 `throw` 来将异常重新抛出，从而允许异常在调用栈的更高层次被捕获。

下面是一个简单的示例，演示了二次抛出异常的用法：

```cpp
void foo() {
    try {
        // 一些可能抛出异常的代码
    } catch (const std::exception& e) {
        // 异常处理代码
        // 在处理完异常后，重新抛出异常
        throw;  // 重新抛出已捕获的异常
    }
}

int main() {
    try {
        foo();
    } catch (const std::exception& e) {
        // 处理重新抛出的异常
        // ...
    }

    return 0;
}
```

在上述示例中，`foo()` 函数中的 `try` 块用于捕获可能抛出的异常，并在 `catch` 块中进行异常处理。在异常处理完成后，使用 `throw` 关键字重新抛出已捕获的异常。然后，在 `main()` 函数中的外部 `try` 块中，可以再次捕获并处理该异常。

通过二次抛出异常，可以将异常传递给更高级别的异常处理器，以便在不同的层次上进行更细粒度的异常处理。这种技术可以在不同的代码模块或层次之间传递异常，从而实现更灵活和细致的异常处理策略。

需要注意的是，当重新抛出异常时，异常的类型、信息和堆栈信息都会被保留。这样可以保持异常的一致性和完整性，使得上层的异常处理器能够获取到准确的异常信息，并进行相应的处理。



> `try`和`catch`应该连着使用,尽量不要放在一个类的内部的成员函数来实现.



### `cerr`

> `cerr` 是 C++ 标准库中的一个输出流对象，它用于向标准错误流（standard error stream）输出数据。它是 `std::ostream` 类型的对象，通过 `#include <iostream>` 头文件进行引用。
>
> 与 `cout`（标准输出流）相比，`cerr` 主要用于输出错误信息和诊断信息，而不是普通的程序输出。它不会被标准输出重定向，而是将输出直接发送到终端或日志文件，以便及时发现和处理错误。



## working with file

* 文件不能递归创建.





> 创建一个对象，把这个对象和文件绑定在一起.

> 在C++中，可以使用不同的方式进行文件的读写操作。以下是几种常见的文件读写方式的简要介绍：
>
> 1. 文本文件读写：
>    - 使用 `std::ifstream` 类来读取文本文件，使用 `std::ofstream` 类来写入文本文件。
>    - 可以使用 `open()` 函数打开文件，并使用 `>>` 和 `<<` 运算符进行读写操作。
>    - 可以使用 `getline()` 函数逐行读取文本文件的内容。
>    - 读写文本文件时，数据以文本形式存储，可读性好，但可能会有一些额外的格式化操作。
>    
> 2. 二进制文件读写：
>    - 使用 `std::ifstream` 类来读取二进制文件，使用 `std::ofstream` 类来写入二进制文件。
>    - 可以使用 `open()` 函数打开文件，并使用 `read()` 和 `write()` 函数进行读写操作。
>    - 读写二进制文件时，数据以二进制形式存储，通常用于存储复杂结构的数据，速度较快，但不可读。
>    
> 3. 以文本方式追加内容：
>    - 使用 `std::ofstream` 类，并设置 `std::ios::app` 标志来追加内容到文本文件末尾。
>    - 可以使用 `<<` 运算符将数据追加到文件中。
>    
> 4. 文件指针操作：
>    - 使用 `std::fstream` 类可以实现更灵活的文件读写操作。
>    - 可以使用 `open()` 函数打开文件，并使用 `seekg()` 和 `seekp()` 函数定位文件指针。
>    - 可以使用 `read()` 和 `write()` 函数进行指定位置的读写操作。
>    
> 5. 异常处理：
>    - 在文件读写过程中，可能会出现一些错误，如文件不存在、打开文件失败等。
>    - 可以使用 `try-catch` 语句来捕获并处理这些异常。
>    - 异常类型包括 `std::ifstream::failure`、`std::ofstream::failure`、`std::ios_base::failure` 等。
>
> 需要注意的是，在进行文件读写操作时，需要确保文件存在且具有适当的权限。此外，在操作文件后，需要及时关闭文件，以释放系统资源。可以使用 `close()` 函数来关闭文件。
>
> 这只是文件读写的一些常见方式，C++还提供了其他一些高级的文件读写操作，如文件流对象的状态检查、格式化输出等。可以根据具体的需求选择适合的文件读写方式。



* 使用构造函数的方式创建一个对象,那么这个参数中只能存在一个文件的

```cpp
std::ifstream inputFile("example.txt"); // 打开文本文件 example.txt
```

* 使用`open()`打开文件的时候,可以打开多个文件.

> 关掉之后可以再次打开



* 使用绝对路径打开的时候

在C++中，打开文件时使用的路径必须是有效的路径，否则将无法成功打开文件。如果使用的是绝对路径，但该路径不存在，那么无法创建文件并打开。

如果你想要创建一个文件，可以使用文件流对象的输出模式打开文件，并在打开失败时判断文件是否存在。如果文件不存在，则可以使用文件流对象的输入模式打开文件，并写入数据来创建文件。

以下是一个示例代码，展示了如何创建文件并打开它：

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ofstream outputFile("path/to/file.txt");  // 尝试打开文件

    if (outputFile.is_open()) {
        std::cout << "文件已打开" << std::endl;
        outputFile << "这是新创建的文件" << std::endl;
        outputFile.close();
    } else {
        std::cout << "文件打开失败，可能路径不存在" << std::endl;
        std::cout << "无法创建文件" << std::endl;
    }

    return 0;
}
```

在上述示例中，我们尝试打开一个文件 `"path/to/file.txt"`，如果路径存在并且文件打开成功，就可以向文件中写入数据。如果路径不存在或者打开失败，我们输出相应的错误消息。

需要注意的是，程序无法自动创建不存在的目录。如果路径中的目录不存在，你需要先创建目录，然后再打开文件进行写入操作。



* 使用`getline()`读入文件

```cpp
#include <iostream>

int main() {
    const int maxLength = 100; // 定义字符数组的最大长度
    char line[maxLength]; // 创建字符数组

    std::cout << "请输入一行文本：";
    std::cin.getline(line, maxLength); // 从标准输入读取一行文本到字符数组中

    std::cout << "输入的文本为：" << line << std::endl;

    return 0;
}
```

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ifstream inputFile("example.txt"); // 打开文件 example.txt

    if (inputFile.is_open()) {
        std::string line;
        while (std::getline(inputFile, line)) {
            std::cout << line << std::endl; // 逐行输出文件内容
        }
        inputFile.close(); // 关闭文件
    } else {
        std::cout << "无法打开文件" << std::endl;
    }

    return 0;
}
```



* 连续地读入文件

```cpp
while(fin){
    fin>>data;
}
```



* 检查文件是否读完

> 在C++中，你可以使用文件流对象的成员函数 `eof()` 来检查是否已经读取完文件。`eof()` 函数在文件流到达文件末尾时返回 true，否则返回 false

```cpp
        if (inputFile.eof()) {
            std::cout << "已读取完文件" << std::endl;
        } else {
            std::cout << "未读取完文件" << std::endl;
        }
```









> `exit(1)` 是 C++ 中的一个函数调用，用于终止程序的执行并返回一个退出状态码。它的作用是在程序运行过程中发生了一些严重的错误或不可恢复的情况时，提前终止程序并通知操作系统程序的执行状态。



* 检查文件是否打开

```cpp
if(fin.is_open())
if(fin.good())
```



* mode

```cpp
ios::app;
ios::in;
ios::ate;
ios::binary;
ios::notcreate
```

> `app`和`ate`,都会把文件指针知道文件末尾.

```cpp
myfile.open("file_name",ios::app|ios::notcreate);  //组合使用
```





### 文件指针

在 C++ 中，文件指针是用于表示文件流中的当前位置的指针，它指向文件中的某个位置，用于读取或写入数据。文件指针的位置由文件模式决定，不同的文件模式会使用不同的文件指针。下面是几种常见的文件模式及其对应的文件指针：

1. 输入模式（`std::ifstream`）：
   - `std::ios::in`：读取模式，文件指针指向下一个要读取的位置。
   - 文件指针可以使用 `seekg()` 函数进行定位，例如 `seekg(0)` 将文件指针定位到文件的开头。

2. 输出模式（`std::ofstream`）：
   - `std::ios::out`：写入模式，文件指针指向下一个要写入的位置。
   - 文件指针可以使用 `seekp()` 函数进行定位，例如 `seekp(0)` 将文件指针定位到文件的开头。
   - 在默认情况下，每次写入操作后，文件指针会自动向后移动。

3. 输入输出模式（`std::fstream`）：
   - `std::ios::in | std::ios::out`：既可读又可写的模式，文件指针可以用于读取和写入操作。
   - `seekg()` 和 `seekp()` 函数都可以用于定位文件指针。

对于输入模式和输出模式，文件指针的位置通常由读取或写入操作自动更新。你也可以使用 `tellg()` 和 `tellp()` 函数获取文件指针的当前位置，以便后续进行定位或查询。

下面是一个示例代码，演示了不同文件模式下文件指针的使用：

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ifstream inputFile("example.txt", std::ios::in); // 输入模式打开文件

    if (inputFile.is_open()) {
        // 获取文件指针的当前位置
        std::streampos position = inputFile.tellg();
        std::cout << "当前文件指针位置: " << position << std::endl;

        // 读取文件内容
        std::string line;
        while (std::getline(inputFile, line)) {
            std::cout << line << std::endl;
        }

        // 重新定位文件指针到开头
        inputFile.seekg(0);

        // 再次获取文件指针的当前位置
        position = inputFile.tellg();
        std::cout << "当前文件指针位置: " << position << std::endl;
    } else {
        std::cout << "无法打开文件" << std::endl;
    }

    inputFile.close(); // 关闭文件

    return 0;
}
```

在上述示例中，我们打开文件 `"example.txt"` 以输入模式进行读取操作。通过 `tellg()` 函数获取文件指针的当前位置，并输出到控制台。然后我们使用 `getline()` 函数逐行读取文件内容，并将每行内容打印到控制台。



* 文件指针使用的是字节

在 C++ 中，`seekg()` 和 `seekp()` 是用于定位文件指针位置的函数，用于在文件流中移动文件指针的位置。

1. `seekg()` 函数：
   - `seekg(pos)`：将输入文件流的文件指针定位到相对于文件开头的位置 `pos` 处。
   - `seekg(off, dir)`：将输入文件流的文件指针从当前位置偏移 `off` 个字节，并根据 `dir` 指定的方向进行定位。
   - `pos`：一个整数值，表示文件指针相对于文件开头的位置。
   - `off`：一个整数值，表示文件指针的偏移量。
   - `dir`：一个 `std::ios_base::seekdir` 类型的值，表示定位的方向，可以是 `std::ios_base::beg`（相对于文件开头）、`std::ios_base::cur`（相对于当前位置）或 `std::ios_base::end`（相对于文件末尾）。

2. `seekp()` 函数：
   - `seekp(pos)`：将输出文件流的文件指针定位到相对于文件开头的位置 `pos` 处。
   - `seekp(off, dir)`：将输出文件流的文件指针从当前位置偏移 `off` 个字节，并根据 `dir` 指定的方向进行定位。
   - `pos`：一个整数值，表示文件指针相对于文件开头的位置。
   - `off`：一个整数值，表示文件指针的偏移量。
   - `dir`：一个 `std::ios_base::seekdir` 类型的值，表示定位的方向，可以是 `std::ios_base::beg`（相对于文件开头）、`std::ios_base::cur`（相对于当前位置）或 `std::ios_base::end`（相对于文件末尾）。

下面是一个示例代码，演示了如何使用 `seekg()` 和 `seekp()` 函数进行文件指针的定位：

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::fstream file("example.txt", std::ios::in | std::ios::out);

    if (file.is_open()) {
        // 将文件指针定位到第 10 个字符处
        file.seekg(9);

        // 读取文件指针当前位置后的内容
        std::string line;
        std::getline(file, line);
        std::cout << "当前位置后的内容：" << line << std::endl;

        // 将文件指针定位到文件末尾
        file.seekp(0, std::ios_base::end);

        // 在文件末尾写入内容
        file << "追加的内容" << std::endl;
    } else {
        std::cout << "无法打开文件" << std::endl;
    }

    file.close(); // 关闭文件

    return 0;
}
```

在上述示例中，我们打开文件 `"example.txt"`，以输入输出模式进行读写操作。首先，我们使用 `

seekg()` 函数将文件指针定位到文件的第 10 个字符处，并读取文件指针当前位置后的内容。然后，我们使用 `seekp()` 函数将文件指针定位到文件末尾，并在文件末尾追加写入内容。最后，我们关闭文件。



* 当`seekp()`不传第二个参数的时候,默认的起始位置是文件的开头

* `write()和read()`方法都是对二进制文件的一个处理.





### 二进制文件读写

当进行二进制读写文件时，我们使用的是二进制模式而不是文本模式。这意味着我们可以直接读取和写入文件中的原始字节数据，而不会对其进行任何字符编码或解码。C++ 提供了 `std::fstream` 类来处理二进制文件的读写操作。

下面是一个简单的示例，演示如何使用二进制模式读写文件：

```cpp
#include <iostream>
#include <fstream>

struct Person {
    int id;
    std::string name;
    double salary;
};

int main() {
    // 写入二进制文件
    std::ofstream outputFile("data.bin", std::ios::binary);
    if (outputFile.is_open()) {
        Person p1{1, "John Doe", 5000.0};
        Person p2{2, "Jane Smith", 6000.0};

        outputFile.write(reinterpret_cast<const char*>(&p1), sizeof(Person));
        outputFile.write(reinterpret_cast<const char*>(&p2), sizeof(Person));

        outputFile.close();
    } else {
        std::cout << "无法打开文件" << std::endl;
        return 1;
    }

    // 读取二进制文件
    std::ifstream inputFile("data.bin", std::ios::binary);
    if (inputFile.is_open()) {
        Person p;
        while (inputFile.read(reinterpret_cast<char*>(&p), sizeof(Person))) {
            std::cout << "ID: " << p.id << ", Name: " << p.name << ", Salary: " << p.salary << std::endl;
        }

        inputFile.close();
    } else {
        std::cout << "无法打开文件" << std::endl;
        return 1;
    }

    return 0;
}
```

在上述示例中，我们定义了一个 `Person` 结构体来表示一个人的信息，包括 ID、姓名和工资。首先，我们使用二进制模式打开文件 `"data.bin"` 进行写入操作。然后，我们创建两个 `Person` 对象 `p1` 和 `p2`，并使用 `write()` 方法将它们的数据以二进制形式写入文件中。我们使用 `reinterpret_cast` 来将结构体指针转换为 `const char*` 类型的指针，以便进行字节级别的写入操作。

接下来，我们使用二进制模式打开同一个文件进行读取操作。使用 `read()` 方法读取文件的字节数据，并将其转换为 `Person` 结构体的对象。通过循环读取并输出每个人的信息，直到到达文件结尾。

需要注意的是，在进行二进制文件读写时，要确保写入和读取的数据类型和结构体的布局是一致的。否则，可能会导致数据读取错误或数据损坏。

总结来说，二进制文件读写允许我们以原始字节的形式直接读取和写入数据，非常适用于存储和读取复杂的数据结构或二进制数据。





* 修饰浮点数

在 C++ 中，`std::fixed` 是一个 I/O 操纵符（IO manipulator），用于控制浮点数的输出格式。

当使用 `std::fixed` 修饰浮点数输出时，它将强制浮点数的小数部分显示为固定的精度，即小数点后面的位数保持不变。默认情况下，浮点数输出是以科学计数法或自动选择表示方式显示的，而使用 `std::fixed` 可以更改为固定精度显示。

下面是一个示例代码，演示了如何使用 `std::fixed`：

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double number = 123.456789;

    std::cout << std::fixed << number << std::endl;

    return 0;
}
```

在上述示例中，我们定义了一个 `double` 类型的变量 `number`，其值为 `123.456789`。通过在输出语句中使用 `std::fixed`，我们可以将其输出为固定精度的浮点数，即小数点后面的位数保持不变。输出结果为 `123.456789`。

需要注意的是，`std::fixed` 会影响之后的所有浮点数输出，直到另一个输出格式修饰符出现或者被重置为默认格式。如果只想对某个特定的浮点数输出使用固定精度，可以在需要的地方临时使用 `std::fixed`，然后恢复为默认格式。

总结来说，`std::fixed` 是用于控制浮点数输出格式的操纵符，它可以将浮点数的小数部分显示为固定的精度。



# tips

> 读变量的含义的时候,先向右边看再向左边看.

> `const int`等价于`int const`





* 静态绑定和动态绑定

静态绑定（Static Binding）和动态绑定（Dynamic Binding）是面向对象编程中多态性的两种不同实现方式，它们之间存在以下区别：

1. 解析时机：静态绑定在编译时进行，而动态绑定在运行时进行。

2. 绑定对象：静态绑定是根据变量的静态类型进行绑定，而动态绑定是根据变量的实际类型进行绑定。

3. 绑定方式：静态绑定使用静态绑定符号（如"."或"->"）进行绑定，而动态绑定使用虚函数机制进行绑定。

4. 绑定结果：静态绑定调用的是编译时确定的函数，而动态绑定调用的是根据实际类型确定的函数。

5. 多态性表现：静态绑定不支持多态性，而动态绑定支持多态性。

静态绑定适用于非虚函数和静态成员函数，它的优势在于效率高，因为函数调用的目标在编译时就已确定，不需要额外的运行时开销。但是静态绑定不具备多态性的特点，无法实现基类指针或引用调用派生类的成员函数。

动态绑定适用于虚函数，它通过虚函数表（VTable）和虚函数指针（vptr）实现。在动态绑定下，函数的调用在运行时根据对象的实际类型来确定，可以实现运行时的多态性，提供了更大的灵活性和扩展性。

总之，静态绑定和动态绑定是在面向对象编程中实现多态性的两种不同方式。静态绑定在编译时确定函数调用，效率高但不支持多态性；动态绑定在运行时确定函数调用，支持多态性但会带来额外的运行时开销。选择使用哪种绑定方式取决于具体的需求和设计目标。



* 当类里面包含`char*`成员变量的时候,不能使用默认的`class operator = `,因为这个是浅拷贝,会导致多个指针指向同一块空间,在`delete`的时候造成多次的问题.



* `inline function`不能作为虚函数,因为本质是静态绑定
* 析构函数可以是虚函数,因为使用函数指针析构的时候需要完全析构.



* 只要有一个纯虚函数,这个类就是抽象类,抽象类无法被实例化.



* `typeid()`

```cpp
const std::type_info& typeid(const T&);
```



# 术语表

当然，下面是一份常见的 C++ 学习中的中文翻译英文的术语表：

| 中文术语       | 英文术语                     |
| -------------- | ---------------------------- |
| 抽象类         | Abstract class               |
| 析构函数       | Destructor                   |
| 构造函数       | Constructor                  |
| 继承           | Inheritance                  |
| 多态           | Polymorphism                 |
| 虚函数         | Virtual function             |
| 模板函数       | Template function            |
| 模板类         | Template class               |
| 命名空间       | Namespace                    |
| 成员函数       | Member function              |
| 成员变量       | Member variable              |
| 静态成员函数   | Static member function       |
| 静态成员变量   | Static member variable       |
| 友元函数       | Friend function              |
| 友元类         | Friend class                 |
| 运算符重载     | Operator overloading         |
| 重载函数       | Overloaded function          |
| 虚基类         | Virtual base class           |
| 纯虚函数       | Pure virtual function        |
| 动态绑定       | Dynamic binding              |
| 静态绑定       | Static binding               |
| 内联函数       | Inline function              |
| 类型转换运算符 | Type conversion operator     |
| 移动构造函数   | Move constructor             |
| 拷贝构造函数   | Copy constructor             |
| 自动类型推导   | Type inference               |
| 模板参数推导   | Template argument deduction  |
| 默认参数       | Default arguments            |
| 右值引用       | Rvalue reference             |
| 左值引用       | Lvalue reference             |
| 强制类型转换   | Explicit type conversion     |
| 隐式类型转换   | Implicit type conversion     |
| 重载解析       | Overload resolution          |
| 函数重载解析   | Function overload resolution |
| 虚析构函数     | Virtual destructor           |
| 常量成员函数   | Constant member function     |
| 模板参数列表   | Template parameter list      |
| 类型别名       | Typedef                      |
| 类型断言       | Type assertion               |
| 命令行参数     | Command line arguments       |
| 输入输出流     | Input/output stream          |
| 读取文件       | Read file                    |
| 写入文件       | Write file                   |
| 异常处理       | Exception handling           |
| 命令行界面     | Command line interface       |
| 标准库         | Standard library             |

这只是一份常见的术语表，可能并不全面，但可以帮助您理解 C++ 中的一些基本概念和术语。请注意，一些术语可能会根据上下文而略有不同。
