# cargo指令

`cargo new <project name>`创建新项目

`cargo build`构建项目

`cargo run`运行项目



# 使用包

```rust
use std::io;
```



# 获取输入

```rust
use std::io;

fn main() {
    println!("Hello, world!");
    let mut buf = String::new();
    io::stdin().read_line(&mut buf).expect("fail to read");
    println!("{}", buf.trim()); // 去除末尾的换行符
}

```



* 需要传入一个字符串的可变的引用
* 追加字符串内容, 不是覆盖



# 输出

使用`{}`作为占位符



# 变量

* 默认是**不可变**的变量

使用`mut`定义一个可变的变量

使用`::`使用**静态函数(关联函数)**, 比如`String::new()`创建一个字符串实例



字符串使用的时候, 需要使用`.push_str`方法来追加字符串



## 比较

