# 函数声明
```go
func add(a int, b int) int {
	return a + b
}
```
使用类型后置的写法

函数可以返回多个返回值
```go
func swap(x, y string) (string, string) {
	return y, x
}
```

# 变量
使用`var`
```go
var c, python, java bool
```
* 如果初始化值已存在，则可以省略类型；变量会从初始值中获得类型。
* 在函数中，简洁赋值语句 := 可在类型明确的地方代替 var 声明。
* 没有明确初始值的变量声明会被赋予它们的 零值。

类型推导使用`变量的类型由右值推导得出`
* 使用`CONST`声明一个常量

## 结构体
```go
type Vertex struct {
	X int
	Y int
}
```
* 如果我们有一个指向结构体的指针 p，那么可以通过 (*p).X 来访问其字段 X。不过这么写太啰嗦了，所以语言也允许我们使用隐式间接引用，直接写 p.X 就可以。

使用结构体
```go
var (
	v1 = Vertex{1, 2}  // 创建一个 Vertex 类型的结构体
	v2 = Vertex{X: 1}  // Y:0 被隐式地赋予
	v3 = Vertex{}      // X:0 Y:0
	p  = &Vertex{1, 2} // 创建一个 *Vertex 类型的结构体（指针）
)
```
> 使用 Name: 语法可以仅列出部分字段。（字段名的顺序无关。）

### 定义结构体的方法
方法就是一类带特殊的**接收者**参数的函数。
```go
func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
```
可以访问结构体里面的内容,这个函数的实际实现是
```go
func Abs(v Vertex) float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
```

当需要修改结构体内容的时候,需要使用指针
```go
func (v *Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}
```
* 接受一个值作为参数的函数必须接受一个指定类型的值
* 以值为接收者的方法被调用时，接收者既能为值又能为指针

## 接口
方法签名的定义的集合
```go
type Abser interface {
	Abs() float64
}
```

结构体实现接口的时候,无需声明.
* 无需使用`implement`关键字
```go
package main

import "fmt"

type I interface {
	M()
}

type T struct {
	S string
}

// 此方法表示类型 T 实现了接口 I，但我们无需显式声明此事。
func (t T) M() {
	fmt.Println(t.S)
}

func main() {
	var i I = T{"hello"}
	i.M()
}
```
* 即使接受的是`nil`,也可以调用`nil`接口值的方法

空接口可以存储任意类型的值
```go
	var i interface{}
	describe(i)

	i = 42
	describe(i)

	i = "hello"
	describe(i)
```
检查接口类的底层值
```go
t := i.(T)
```
使用`switch`语句可以判断接口的底层值
```go
	switch v := i.(type) {
	case int:
		fmt.Printf("Twice %v is %v\n", v, v*2)
	case string:
		fmt.Printf("%q is %v bytes long\n", v, len(v))
	default:
		fmt.Printf("I don't know about type %T!\n", v)
	}
```

### `String`方法
`fmt`包会自动调用`String`方法来打印值

## 数组
```go
var a [5]int
```
* 数组的长度是其类型的一部分，因此 [3]int 和 [4]int 是不同的类型。

使用数组切片的时候, 需要使用`[:]`,并且切片是引用类型
* 切片的时候,可以忽略上下界
* 切片 s 的长度和容量可通过表达式 len(s) 和 cap(s) 来获取。
* 空的切片是`nil`
使用`make`创建动态数组.
使用`append`添加元素到切片中
```go
	// 这个切片会按需增长
	s = append(s, 1)
	printSlice(s)

	// 可以一次性添加多个元素
	s = append(s, 2, 3, 4)
```

### 遍历数组
使用`range`实现,返回2个值,一个是当前元素的下标,一个是当前元素对应的副本
```go
	var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}
	for i, v := range pow {
		fmt.Printf("2**%d = %d\n", i, v)
	}
```

## 映射
使用`map`创建映射
```go
type Vertex struct {
	Lat, Long float64
}

var m map[string]Vertex
```
* 映射的文法是 `make(map[key-type]val-type)`。

修改映射`m[key] = elem`

删除元素`delete(m, key)`

获取元素`elem, ok := m[key]`

# for语句
```go
	for i := 0; i < 10; i++ {
		sum += i
	}
```
* 不使用`()`
* 使用`for`代替`while`
* 没有`do-while`

## 无限循环
```go
	for {
    }
```

# if语句
```go
	if x > 10 {
		return true
	} else if x < 0
		return false
```
* 和`for`一样，`if`语句不需要`()`但是需要`{}`.

# defer
defer 语句会将函数推迟到外层函数返回之后执行。
```go
package main

import "fmt"

func main() {
	defer fmt.Println("world")

	fmt.Println("hello")
}
```
* 推迟的函数调用会被压入一个栈中。当外层函数返回时，被推迟的函数会按照后进先出的顺序调用。

# 输入
使用`fmt`的`Scanf`函数
```go
func main() {
	name := ""
	fmt.Scanf("%s", &name)
	fmt.Println("Hello, " + name)
}
```

# 并发
使用`go`关键字创建并发

`ch := make(chan int)`创建一个信道,用来接受返回值