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

* 函数可以作为变量传递



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



## 设置默认值

如果一个函数被调用，但有参数（argument）未被提供，那么相应的值就会变成 `undefined`。

例如，之前提到的函数 `showMessage(from, text)` 可以只使用一个参数（argument）调用：

```javascript
showMessage("Ann");
```



那不是错误，这样调用将输出 `"*Ann*: undefined"`。因为参数 `text` 的值未被传递，所以变成了 `undefined`。

我们可以使用 `=` 为函数声明中的参数指定所谓的“默认”（如果对应参数的值未被传递则使用）值：

```javascript
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```



* 早期的时候,没有默认值的写法,需要显示的判断然后添加



## 箭头函数

* 匿名函数

它被称为“箭头函数”，因为它看起来像这样：

```javascript
let func = (arg1, arg2, ..., argN) => expression;
```

> 让我们来看一个具体的例子：
>
> ```javascript
> let sum = (a, b) => a + b;
> 
> /* 这个箭头函数是下面这个函数的更短的版本：
> 
> let sum = function(a, b) {
>   return a + b;
> };
> */
> 
> alert( sum(1, 2) ); // 3
> ```





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

* 你需要使用`break`语句

> 可以通过不适用`break`语句,把多种情况连在一起

```javascript
  case '0':
  case '1':
    alert( 'One or zero' );
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



* 注意,最后的属性应该使用`,`结尾



* 对象中可以使用`this`



> 对象的属性可以不适用`""`来包括属性名,但是遇到特殊字符空格等必须使用

> 对象的方法在写的时候需要使用`XXX:function(){}`,使用的是匿名函数



## 访问属性

1. 使用`for in`语句遍历里面的内容



## 访问属性(在不确定是否存在的时候)



* 当你访问不存在的属性值的时候,属性值是`undefined`,你可以使用`in`去检查是否存在这个属性名(注意,只能是属性名)





* 使用遍历的方式查找属性名(输出的类型是字符串)

> 使用`for in`语句

语法：

```javascript
for (let key in object) {
  // 对此对象属性中的每个键执行的代码
}
```

* 注意,当你访问的数字型的时候,会出问题



> 当你在遍历访问属性的时候,如果可以转换成`number`的属性名是自动排序的



## 引用和赋值

> 把一个原始类型直接赋值给别的东西的时候,是拷贝
>
> 但是,对象是引用

```javascript
Object.assign(dest, [src1, src2, src3...])
```



我们也可以用 `Object.assign` 代替 `for..in` 循环来进行简单克隆：

```javascript
let user = {
  name: "John",
  age: 30
};

let clone = Object.assign({}, user);
```

它将 `user` 中的所有属性拷贝到了一个空对象中，并返回这个新的对象。

还有其他克隆对象的方法，例如使用 [spread 语法](https://zh.javascript.info/rest-parameters-spread) `clone = {...user}`，在后面的章节中我们会讲到。





## 多词属性

> 对于中间使用`空格`分隔的属性无法使用`.`的方式直接访问,选哟使用`[]`的方式



## 对象中的键使用变量

> 使用`[]`包裹变量

例如：

```javascript
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
  [fruit]: 5, // 属性名是从 fruit 变量中得到的
};

alert( bag.apple ); // 5 如果 fruit="apple"
```



> 我们可以使用更加复杂的方式

我们可以在方括号中使用更复杂的表达式：

```javascript
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```



* 属性名不受关键词的限制
* 你在设置和查询属性的时候,属性名都会被转变成为字符串的格式



## 内置对象



### `Math`

> 可以使用`Math.PI`来访问圆周率

> 有`ceil`,`floor`,`round`,`random`等方法





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



## 数字类型

假如我们需要表示 10 亿。显然，我们可以这样写：

```javascript
let billion = 1000000000;
```

我们也可以使用下划线 `_` 作为分隔符：

```javascript
let billion = 1_000_000_000;
```

在 JavaScript 中，我们可以通过在数字后面附加字母 `"e"` 并指定零的个数来缩短数字：

```javascript
let billion = 1e9;  // 10 亿，字面意思：数字 1 后面跟 9 个 0

alert( 7.3e9 );  // 73 亿（与 7300000000 和 7_300_000_000 相同）
```

换句话说，`e` 把数字乘以 `1` 后面跟着给定数量的 0 的数字。



* 转换为进制数

> 使用`num.toString(base)`方法



```
Math.floor
```

向下舍入：`3.1` 变成 `3`，`-1.1` 变成 `-2`。

```
Math.ceil
```

向上舍入：`3.1` 变成 `4`，`-1.1` 变成 `-1`。

```
Math.round
```

向最近的整数舍入：`3.1` 变成 `3`，`3.6` 变成 `4`，中间值 `3.5` 变成 `4`。

`Math.trunc`（IE 浏览器不支持这个方法）

移除小数点后的所有内容而没有舍入：`3.1` 变成 `3`，`-1.1` 变成 `-1`



## 字符串类型

* 注意,是`只读`的

> 使用反引号的时候,可以插入值和换行.

> 访问字符的时候
>
> 1. 使用下标访问的方式
> 2. 使用`charAt()`方法

我们也可以使用 `for..of` 遍历字符：

```javascript
for (let char of "Hello") {
  alert(char); // H,e,l,l,o（char 变为 "H"，然后是 "e"，然后是 "l" 等）
}
```

[toLowerCase()](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase) 和 [toUpperCase()](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) 方法可以改变大小写：

```javascript
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
```



* 查找字符串

> 使用`indexOf`方法
>
> * 注意,在如果把查找语句作为`if`语句的条件的时候,需要手动和`-1`比较

它从给定位置 `pos` 开始，在 `str` 中查找 `substr`，如果没有找到，则返回 `-1`，否则返回匹配成功的位置。

例如：

```javascript
let str = 'Widget with id';

alert( str.indexOf('Widget') ); // 0，因为 'Widget' 一开始就被找到
alert( str.indexOf('widget') ); // -1，没有找到，检索是大小写敏感的

alert( str.indexOf("id") ); // 1，"id" 在位置 1 处（……idget 和 id）
```

### 

更现代的方法 [str.includes(substr, pos)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/includes) 根据 `str` 中是否包含 `substr` 来返回 `true/false`。

如果我们需要检测匹配，但不需要它的位置，那么这是正确的选择：

```javascript
alert( "Widget with id".includes("Widget") ); // true

alert( "Hello".includes("Bye") ); // false
```

`str.includes` 的第二个可选参数是开始搜索的起始位置：

```javascript
alert( "Widget".includes("id") ); // true
alert( "Widget".includes("id", 3) ); // false, 从位置 3 开始没有 "id"
```

方法 [str.startsWith](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith) 和 [str.endsWith](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith) 的功能与其名称所表示的意思相同：

```javascript
alert( "Widget".startsWith("Wid") ); // true，"Widget" 以 "Wid" 开始
alert( "Widget".endsWith("get") ); // true，"Widget" 以 "get" 结束
```



* 字符串切片

> 使用**str.slice(start [, end])**,后半部分不包括
>
> 可以使用负数值从结尾开始

| 方法                    | 选择方式……                                | 负值参数            |
| :---------------------- | :---------------------------------------- | :------------------ |
| `slice(start, end)`     | 从 `start` 到 `end`（不含 `end`）         | 允许                |
| `substring(start, end)` | 从 `start` 到 `end`（不含 `end`）         | 负值被视为 `0`      |
| `substr(start, length)` | 从 `start` 开始获取长为 `length` 的字符串 | 允许 `start` 为负数 |



## 数组方法

- `push` 在末端添加一个元素.
- `shift` 取出队列首端的一个元素，整个队列往前移，这样原先排第二的元素现在排在了第一。

- `push` 在末端添加一个元素.
- `pop` 从末端取出一个元素.
- `unshift`往首部分添加一个元素



> 注意,本质是`对象`



> 使用`toSring`方法会把数组变成中间使用`,`链接起来的字符串



> 注意,不能使用`==`比较数组



* 删除数组元素(直接`delete`会造成位置空缺)

> 使用`splice`,

我们可以将 `deleteCount` 设置为 `0`，`splice` 方法就能够插入元素而不用删除任何元素：

```javascript
let arr = ["I", "study", "JavaScript"];

// 从索引 2 开始
// 删除 0 个元素
// 然后插入 "complex" 和 "language"
arr.splice(2, 0, "complex", "language");

alert( arr ); // "I", "study", "complex", "language", "JavaScript"
```



* `concat`

> [arr.concat](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) 创建一个新数组，其中包含来自于其他数组和其他项的值。
>
> 语法：
>
> ```javascript
> arr.concat(arg1, arg2...)
> ```

如果类数组对象具有 `Symbol.isConcatSpreadable` 属性，那么它就会被 `concat` 当作一个数组来处理：此对象中的元素将被添加：

```javascript
let arr = [1, 2];

let arrayLike = {
  0: "something",
  1: "else",
  [Symbol.isConcatSpreadable]: true,
  length: 2
};

alert( arr.concat(arrayLike) ); // 1,2,something,else
```



> 查找一个内容可以使用`indexOf`,`incldes`,使用`includes`可以发现`NaN`,但是另一个不行



* `find`

这时可以用 [arr.find](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/find) 方法。

语法如下：

```javascript
let result = arr.find(function(item, index, array) {
  // 如果返回 true，则返回 item 并停止迭代
  // 对于假值（falsy）的情况，则返回 undefined
});
```

例如，我们有一个存储用户的数组，每个用户都有 `id` 和 `name` 字段。让我们找到 `id == 1` 的那个用户：

```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);

alert(user.name); // John
```



### [filter](https://zh.javascript.info/array-methods#filter)

`find` 方法搜索的是使函数返回 `true` 的第一个（单个）元素。

如果需要匹配的有很多，我们可以使用 [arr.filter(fn)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)。

语法与 `find` 大致相同，但是 `filter` 返回的是所有匹配元素组成的数组：

```javascript
let results = arr.filter(function(item, index, array) {
  // 如果 true item 被 push 到 results，迭代继续
  // 如果什么都没找到，则返回空数组
});
```

例如：

```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

// 返回前两个用户的数组
let someUsers = users.filter(item => item.id < 3);

alert(someUsers.length); // 2
```





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



> 数字类型转换的时候,会忽略开头结尾的空格



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



# 比较

* 字符串比较

> 根据字典序

* 数字和字符串比较

> 转换成数字比较



## 严格比较

普通的相等性检查 `==` 存在一个问题，它不能区分出 `0` 和 `false`

**严格相等运算符 `===` 在进行比较时不会做任何的类型转换**

通过比较 `null` 和 0 可得：

```javascript
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) true
```



# 空值合并运算符

`a ?? b` 的结果是：

- 如果 `a` 是已定义的，则结果为 `a`，
- 如果 `a` 不是已定义的，则结果为 `b`。

例如，在这里，如果 `user` 的值不为 `null/undefined` 则显示 `user`，否则显示 `匿名`：

```javascript
let user;

alert(user ?? "匿名"); // 匿名（user 未定义）
```

在下面这个例子中，我们将一个名字赋值给了 `user`：

```javascript
let user = "John";

alert(user ?? "匿名"); // John（user 已定义）
```



# `new`

构造函数在技术上是常规函数。不过有两个约定：

1. 它们的命名以大写字母开头。
2. 它们只能由 `"new"` 操作符来执行。

换句话说，`new User(...)` 做的就是类似的事情：

```javascript
function User(name) {
  // this = {};（隐式创建）

  // 添加属性到 this
  this.name = name;
  this.isAdmin = false;

  // return this;（隐式返回）
}
```



## 检查是否使用`new`构造

> 使用`new.target`语法

我们也可以让 `new` 调用和常规调用做相同的工作，像这样：

```javascript
function User(name) {
  if (!new.target) { // 如果你没有通过 new 运行我
    return new User(name); // ……我会给你添加 new
  }

  this.name = name;
}

let john = User("John"); // 将调用重定向到新用户
alert(john.name); // John
```



在构造器中,直接`return`返回的是`this`.



# 访问可能不存在的元素

> 可以使用`?`

可能最先想到的方案是在访问该值的属性之前，使用 `if` 或条件运算符 `?` 对该值进行检查，像这样：

```javascript
let user = {};

alert(user.address ? user.address.street : undefined);
```



# `symbol`

> 代表唯一标识符

> 不会自动转换
>
> 转换为`string`类型的时候,需要使用`toString`方法

* 注意,对象中存在这个元素的时候,这个`for..in`语句会被跳过

> 当我们需要名字相同的`symbol`有相同的属性的时候,使用`Symbol.for()`的方式



# `const`的使用

* 对于基本的数据类型,如果设置为`const`,那么就不能修改值了

* 对于对象这种复杂的数据类型,即使设置为`const`,依旧可以修改内容

> 复杂数据类型内部保存的是指向真实内容的地址,所以,你修改内容的时候,不会修改地址,所以,可以修改真实的内容
>
> 当你给它赋值一个新的数组的时候,它会报错



# DOM

> 用来使用`WEB API`



## 获取`DOM`元素

> 使用`CSS`元素选择器获取`DOM`元素

```javascript
let myBox = document.querySelector('.box');
```

* 注意,你只能找到第一个元素

* 你可以使用选择器的语法来查找`DOM元素`.



> 使用`CSS选择器`查找全部的元素,获取的是一个数组

```javascript
		let myBox = document.querySelectorAll('.box');
        for (let i = 0; i < myBox.length; i++) {
            console.log(myBox[i]);
        }
```



> 修改常用的样式的时候,可以直接使用`.样式名字`的方式修改

> 修改样式的属性的时候
>
> 1. 使用直接使用`.样式属性名字`的方式访问
>
> * 如果出现`-`在中间,使用小驼峰命名法可以访问
>
> ```javascript
> myBox[i].style.width = "100px";
> ```
>
> 2. 使用`className`修改
>
> ```javascript
> myBox[i].className = "box2";
> ```
>
> 3. 当同时使用多个样式类的时候,使用`classList`来修改
>
> > 使用`add`追加
> >
> > 使用`remove`删除
> >
> > 使用`toggle`实现切换,有的话就删除,没有的话就添加



## 自定义的属性名字

> 使用`data-{自定义的类型名字}`来实现自定义的`CSS`属性名字
>
> 在访问的时候,可以使用`元素.dataset.自定义的ID名字`来实现访问.



## 使用定时器(间歇函数)

> 定时器,使用间歇函数

```javascript
		function printOk() {
            console.log("ok");
        }
        setInterval(printOk, 1000);
```

> 第一个参数是需要被执行的函数,第二个参数是以`ms`为单位的每次执行间隔的时间
>
> 返回的是一个id数字,这个是并发的,一个界面可以存在多个定时器,每个定时器都有一个独一无二的ID.



> 关闭定时器

> 使用`clearInterval`



## 添加事件响应

> 使用`元素名.addEventListener(事件名字,需要被执行的函数名字)`



## 事件类型

鼠标

> click
>
> mouseenter
>
> mouseleave

焦点事件

> focus
>
> blur

键盘事件

> keydown
>
> keyup

文本事件

> input



## 事件对象

> 当你在使用处理事件函数的时候,

```javascript
		element.addEventListener('input', function (e) {
            console.log(e.target.value);
        });
```

> 其中的参数`e(回调函数的第一个参数)`是事件对象,存储了这个事件的一些内容



属性

> `type`当前的事件类型
>
> `clientX/clientY`获取光标相对于浏览器可见窗口左上角的位置
>
> `offsetX/offsetY`获取光标相对于当前的`DOM`元素的左上角的位置
>
> `key`查看按下的值



## 环境对象

> 使用`this`,指向的是`window`(在非严格的情况下面)



## 事件流

