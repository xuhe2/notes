* `JS`是动态类型的语言,需要的时候会自己转换,所以,一个变量可以给不同类型的值.

* 使用`npm`下载第三方库



# 注释

* `JS`的注释和`CPP`一样



# 变量声明

JavaScript 中有三种常见的变量声明方式：`var`、`let` 和 `const`。让我逐一为你介绍它们：

1. `var` 声明（`ES5`）
```javascript
// 使用 var 声明变量
var name = "John";
var age = 30;

// 变量声明提升：可以在声明之前使用变量
console.log(name); // 输出 "John"
```

`var` 声明的变量在整个函数作用域内都可见，这导致了变量提升的行为，即可以在变量声明之前使用变量，但其值会是 `undefined`。

2. `let` 声明（`ES6`）
```javascript
// 使用 let 声明变量
let name = "John";
let age = 30;

// 块级作用域：变量仅在其声明的代码块内可见
{
  let name = "Alice"; // 不会影响外部的 name 变量
  console.log(name); // 输出 "Alice"
}
console.log(name); // 输出 "John"
```

`let` 声明引入了块级作用域，变量仅在其声明的代码块内可见。这解决了 `var` 声明可能引起的作用域问题。

3. `const` 声明（`ES6`）
```javascript
// 使用 const 声明常量
const pi = 3.14;

// 常量的值不能被重新赋值
pi = 3.14159; // 会引发错误
```

`const` 声明用于创建常量，常量的值不能被重新赋值。它也具有块级作用域。

在现代 JavaScript 中，推荐使用 `let` 和 `const` 来声明变量，因为它们提供了更好的作用域控制和代码可读性。避免使用 `var` 声明，因为它在作用域和变量提升方面可能会引发一些意想不到的问题。

* 推荐使用`let`来实现变量的声明.



## 变量被声明但是没有被赋值

> 用 `var` 或 `let` 语句声明的变量，如果没有赋初始值，则其值为 [`undefined`]

* `undefined`在数值的情况下会被变成`NaN`.



## 变量没有被声明

> 如果访问一个未声明的变量会导致抛出 [`ReferenceError`] 异常



# 变量提升

> JavaScript 变量的另一个不同寻常的地方是，你可以先使用变量稍后再声明变量而不会引发异常。这一概念称为变量提升；JavaScript 变量感觉上是被“提升”或移到了函数或语句的最前面。但是，提升后的变量将返回 undefined 值。因此在使用或引用某个变量之后进行声明和初始化操作，这个被提升的变量仍将返回 undefined 值。

```javascript
/**
 * 例子 1
 */
console.log(x === undefined); // true
var x = 3;

/**
 * 例子 2
 */
// will return a value of undefined
var myvar = "my value";

(function () {
  console.log(myvar); // undefined
  var myvar = "local value";
})();
```



# 数据类型

- 七种基本数据类型：
  - 布尔值（Boolean），有 2 个值分别是：`true` 和 `false`。
  - null，一个表明 null 值的特殊关键字。JavaScript 是大小写敏感的，因此 `null` 与 `Null`、`NULL`或变体完全不同。
  - undefined，和 null 一样是一个特殊的关键字，undefined 表示变量未赋值时的属性。
  - 数字（Number），整数或浮点数，例如： `42` 或者 `3.14159`。
  - 任意精度的整数（BigInt），可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。
  - 字符串（String），字符串是一串表示文本值的字符序列，例如：`"Howdy"`。
  - 代表（Symbol，在 ECMAScript 6 中新添加的类型）。一种实例是唯一且不可改变的数据类型。
- 以及对象（Object）。



> 使用`+`的时候,数字会变成字符串加上去

```javascript
x = "The answer is " + 42; // "The answer is 42"
y = 42 + " is the answer"; // "42 is the answer"
```



> 使用`-`的时候不会变成字符串



## 字符串转换为数字

* 使用`parseInt`和`parseFloat`方法

```javascript
let a = "1";
console.log(parseInt(a))
```



* 使用`一元加法运算符`来实现

```javascript
"1.1" + "1.1" = "1.11.1"
(+"1.1") + (+"1.1") = 2.2
// 注意：加入括号为清楚起见，不是必需的。
```



## 在数组中使用多余的逗号的时候

> 代码不会报错,但是,在空余的位置会加上`undefined`填充.



# 语句块

> 用`{}`围起来的语句

* 注意使用`let`



## `if else`语句

* 和`CPP`一样

```javascript
if (condition_1) {
  statement_1;
} else if (condition_2) {
  statement_2;
} else if (condition_n_1) {
  statement_n;
} else {
  statement_last;
}
```



### 判断条件

- `false`
- `undefined`
- `null`
- `0`
- `NaN`
- 空字符串（`""`）

这些都是`false`



* 注意,所有的对象都是`true`,不要混淆对象和上面这些

```javascript
if (new Boolean(false)) {  //this is true
    console.log("I'm inside the code block");
}
```



# `alert`

`alert` 是 JavaScript 中的一个内置函数，用于在浏览器中显示一个弹出警告框，向用户提供一条简短的信息或提示。它通常用于在用户执行某些操作时向其提供一些重要信息，或者在需要用户确认之前提醒用户。

以下是 `alert` 函数的基本用法：

```javascript
alert("这是一条警告信息！");
```

当这行代码被执行时，浏览器会弹出一个带有指定文本的对话框，其中包含一个确认按钮，用户可以点击确认来关闭对话框。

注意事项：
- `alert` 函数会阻塞浏览器的继续执行，直到用户关闭弹出框为止。因此，在使用 `alert` 的同时要考虑到用户体验，避免在关键操作中过多使用。
- 弹出的警告框通常不能自定义样式，其外观由浏览器决定，无法进行定制。
- 在现代 Web 开发中，通常更倾向于使用更灵活的提示和交互方式，比如使用模态框或者自定义的通知组件。

以下是一个示例，展示如何在页面加载后使用 `alert` 函数：

```html
<!DOCTYPE html>
<html>
<head>
  <title>Alert示例</title>
</head>
<body>
  <script>
    // 当页面加载完毕后，显示一个弹出框
    window.onload = function() {
      alert("欢迎访问我们的网站！");
    };
  </script>
</body>
</html>
```

在上述示例中，当页面加载完成后，会弹出一个包含欢迎信息的警告框。



# 函数

* 使用`function`定义

```javascript
function multiply(num1, num2) {
  let result = num1 * num2;
  return result;
}
```



## 使用`typescript`对函数的参数类型进行注释

```typescript
function greetUser(name: string, age: number): void {
  console.log(`Hello, ${name}! You are ${age} years old.`);
}
```



# 事件

* 比如点击界面

```javascript
document.querySelector("html").addEventListener("click", function () {
  alert("别戳我，我怕疼。");
});
```



# `for`语句

* 和`CPP`一样



## `for...in` 语句

[`for...in`] 语句循环一个指定的变量来循环一个对象所有可枚举的属性。JavaScript 会为每一个不同的属性执行指定的语句。

```
for (variable in object) {
  statements
}
```



# `switch`语句

`switch` 语句允许一个程序求一个表达式的值并且尝试去匹配表达式的值到一个 `case` 标签。如果匹配成功，这个程序执行相关的语句。`switch` 语句如下所示：

```
switch (expression) {
   case label_1:
      statements_1
      [break;]
   case label_2:
      statements_2
      [break;]
   ...
   default:
      statements_def
      [break;]
}
```



# 对象

```javascript
var person = {
  name: ["Bob", "Smith"],
  age: 32,
  gender: "male",
  interests: ["music", "skiing"],
  bio: function () {
    alert(
      this.name[0] +
        " " +
        this.name[1] +
        " is " +
        this.age +
        " years old. He likes " +
        this.interests[0] +
        " and " +
        this.interests[1] +
        ".",
    );
  },
  greeting: function () {
    alert("Hi! I'm " + this.name[0] + ".");
  },
};
```



# 在`ul`中实现搜索功能

* 搜索框

```javascript
<input type="text" id="searchInput" placeholder="输入关键词">
```

> 1. `type="text"`：这个属性指定了输入元素的类型为文本输入框。这意味着用户可以在这个输入框中输入任意文本信息。
> 2. `id="searchInput"`：这个属性给输入元素指定了一个唯一的标识符，即 ID。这个 ID 可以在 JavaScript 或 CSS 中用来引用这个特定的输入元素。例如，你可以通过 `document.getElementById("searchInput")` 获取这个输入框的引用。
> 3. `placeholder="输入关键词"`：这个属性设置了输入框中的占位符文本。占位符文本是在输入框为空时显示的灰色文本，用于提示用户输入内容的预期格式或内容。当用户开始在输入框中输入内容时，占位符文本会自动消失。



* 搜索的实现

```javascript
<!-- JavaScript 部分 -->
<script>
    // 获取输入框和列表项元素
    const searchInput = document.getElementById("searchInput");
    const listItems = document.querySelectorAll("#list li");

    // 当输入框内容变化时执行的代码
    searchInput.addEventListener("input", function () {
        // 获取输入框内容并转换为小写
        const searchTerm = searchInput.value.toLowerCase();

        // 遍历每个列表项
        listItems.forEach(item => {
            // 获取列表项的文本内容并转换为小写
            const text = item.textContent.toLowerCase();

            // 查找关键词在文本中的位置
            const index = text.indexOf(searchTerm);

            if (index !== -1) {
                // 创建一个新字符串，标注关键词
                const markedText = item.textContent.slice(0, index)
                    + "<span class='highlight'>"
                    + item.textContent.slice(index, index + searchTerm.length)
                    + "</span>"
                    + item.textContent.slice(index + searchTerm.length);

                // 将标注后的文本赋值给列表项
                item.innerHTML = markedText;

                // 显示匹配的列表项
                item.style.display = "block";
            } else {
                // 隐藏不匹配的列表项,当然也可以
                item.style.display = "none";
            }
        });
    });
</script>
```





# 检测按键输入



## 检测`/`输入

```javascript
// 监听键盘按键事件
document.addEventListener("keydown", function (event) {
    // 按下的键是 "/"
    if (event.key === "/") {
        // 将焦点放在搜索框上
        searchInput.focus();

        // 添加扩展样式，放大搜索框
        searchInput.classList.add("expanded");

        // 阻止默认的 "/" 键行为（防止在输入框中输入斜杠）
        event.preventDefault();
    }
});
```



## 检测鼠标焦点离开某个位置

* 使用`blur`(onblur)实现

```javascript
// 监听输入框失去焦点事件
searchInput.addEventListener("blur", function () {
    searchInput.classList.remove("expanded") /*取消扩大状态*/
});
```





# 渲染`markdown`文本(`GitHub`风格)

* 需要使用`marked,js`第三方库,使用`npm install XXX`安装,也可以使用直接导入

> 导入模块

```
<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
```



```javascript
function renderMarkdownFile(filePath, targetElementId) {
    const targetElement = document.getElementById(targetElementId);
    if (!targetElement) {
        console.error("Target element not found.");
        return;
    }

    const xhr = new XMLHttpRequest();
    xhr.open("GET", filePath, true);

    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
            const markdownContent = xhr.responseText;
            targetElement.innerHTML = marked.parse(markdownContent);
        }
    };

    xhr.send();
}
```



# 严格模式

> 在开头使用`"use strict";`,使得脚本使用**现代**模式

* 没有办法取消严格模式



# 变量

1. 变量名称必须仅包含字母、数字、符号 `$` 和 `_`。
2. 首字符必须非数字。

> 推荐使用`驼峰命名法`
>
> 严格区分大小写



## 普通变量

> 使用`let`



## 常量

> 使用`const`

* 我们经常使用全部大写的方式表达这个变量



## 类型

1. number
2. `BigInt`
3. String

> 在 JavaScript 中，有三种包含字符串的方式。
>
> 1. 双引号：`"Hello"`.
> 2. 单引号：`'Hello'`.
> 3. 反引号：``Hello``.
>
> 反引号是 **功能扩展** 引号。它们允许我们通过将变量和表达式包装在 `${…}` 中，来将它们嵌入到字符串中。
>
> ```javascript
> let name = "John";
> 
> // 嵌入一个变量
> alert( `Hello, ${name}!` ); // Hello, John!
> 
> // 嵌入一个表达式
> alert( `the result is ${1 + 2}` ); // the result is 3
> ```
>
> `$`运算符会被计算成一个变量

4. Boolean

> 使用`true`和`false`.



### 检查变量类型

> 使用`typeof`运算符

* 注意,`typeof null` 的结果为 `"object"`。这是官方承认的 `typeof` 的错误，这个问题来自于 JavaScript 语言的早期阶段，并为了兼容性而保留了下来。`null` 绝对不是一个 `object`。`null` 有自己的类型，它是一个特殊值。`typeof` 的行为在这里是错误的。



## 类型转换

我们也可以显式地调用 `String(value)` 来将 `value` 转换为字符串类型：

```javascript
let value = true;
alert(typeof value); // boolean

value = String(value); // 现在，值是一个字符串形式的 "true"
alert(typeof value); // string
```



> 在数学公式中进行计算的时候,会自动进行转换
>
> 不能正常表示的使用`NaN`表示



# 交互

1. `alert`

弹出的这个带有信息的小窗口被称为 **模态窗**。“modal” 意味着用户不能与页面的其他部分（例如点击其他按钮等）进行交互，直到他们处理完窗口。在上面示例这种情况下 —— 直到用户点击“确定”按钮

2. `prmpt`

`prompt` 函数接收两个参数：

```javascript
result = prompt(title, [default]);
```

* 注意,如果用户不输入,会是`null`

3. `confirm`

`confirm` 函数显示一个带有 `question` 以及确定和取消两个按钮的模态窗口。

点击确定返回 `true`，点击取消返回 `false`。

例如：

```javascript
let isBoss = confirm("Are you the boss?");

alert( isBoss ); // 如果“确定”按钮被按下，则显示 true
```
