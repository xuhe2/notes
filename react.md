# 使用`vite`构建项目

```shell
yarn create vite
```



# 创建一个组件

使用`.tsx`文件



```tsx
function MessageBox(){
    return <h1>hello world</h1>;
}

export default MessageBox;
```



## 使用插件快速创建

```tsx
rafce
```



## 使用变量

使用`{}`来包括变量

```tsx
function MessageBox() {
  const name: string = "xuhe";
  return <h1> hello {name} </h1>;
}

export default MessageBox;

```



## 组件函数返回值

一个组件函数只能返回一个大的组件内容

如果出现多个小组件,需要使用`Fragment`实现/使用`<></>`包裹

```tsx
import { Fragment } from "react";

function ListGroup() {
  return (
    <Fragment>
      <ul className="list-group">
        <li className="list-group-item" aria-disabled="false">
          An item
        </li>
        <li className="list-group-item">A second item</li>
        <li className="list-group-item">A third item</li>
        <li className="list-group-item">A fourth item</li>
        <li className="list-group-item">And a fifth one</li>
      </ul>
    </Fragment>
  );
}

export default ListGroup;

```



## 组件的`props`

在开头定义一个`interface`

```tsx
interface ListGroupProps {
  list: string[];
}
```

组件函数需要传入这个接口

```tsx
function ListGroup(props: ListGroupProps) {
```

* 使用解构的方式传入(**适用于参数少的时候**)

```tsx
function ListGroup({ list }: ListGroupProps) {
```



传入函数

```tsx
interface ListGroupProps {
  list: string[];
  onSelect: (index: number) => void;
}
```



## 传入ReactNode

需要使用默认的`children`作为变量名

```tsx
import { ReactNode } from "react";

interface Props {
  children?: ReactNode;
}

const Alert = (props: Props) => {
  return (
    <div className="alert alert-primary" role="alert">
      {props.children}
    </div>
  );
};

export default Alert;

```

* 类型是`ReactNode`



## 查看组件中的内容

使用`value`参数

```tsx
onChange={(e) => setName(e.target.value)}
```

> 当组件内容改动的时候,修改值

* 传入一个element



* 当需要修改父组件的值的时候,一般需要创建一个变量的副本

```tsx
  const [name, setName] = useState(props.name);
  const [password, setPassword] = useState(props.password);

```



* 修改父元素的内容,需要传入一个用于修改的函数

```tsx
interface EditInfoProps {
  name: string;
  password: string;
  updateInfo: (name: string, password: string) => void;
}
```





# bootstrap

本质是一个CSS/JS文件

在`main.tsx`文件中导入



* 使用扩展组件的时候,需要注意**class作为保留字,如果,需要return中的内容包含class,使用className替代**

```js
function ListGroup() {
  return (
    <ul className="list-group">
      <li className="list-group-item">An item</li>
      <li className="list-group-item">A second item</li>
      <li className="list-group-item">A third item</li>
      <li className="list-group-item">A fourth item</li>
      <li className="list-group-item">And a fifth one</li>
    </ul>
  );
}

export default ListGroup;

```



# tailwindcss



* 阻止默认样式

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
  corePlugins: {
    preflight: false,
  }
}


```





# 循环

使用JS语法实现循环,使用`map`实现

* 注意,`map`函数会返回一个东西,这个返回值需要作为一个**变量**,使用`{}`包裹,然后插入

```js
function ListGroup() {
  const list: string[] = ["new york", "china", "france"];
  return (
    <>
      <h1>React List Group</h1>
      <ul className="list-group">
        {list.map((item) => (
          <li className="list-group-item">{item}</li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```



* 使用`key`为你循环生成的标签设置标识,方便后续修改

* 重要的返回值,可以直接预先得到返回值放入/使用函数调用



# 事件

使用的是钩子函数,在对应的属性中传入一个变量就可以实现

```js
  const listItems = list.map((item) => (
    <li
      className="list-group-item"
      onClick={() => {
        console.log(item);
      }}
    >
      {item}
    </li>
  ));
```



* `onClick`接受的函数格式特定,传递参数特定



# hook change state

使用简单的变量,不能实时修改之后被更新出来,需要使用有**state**的

返回的是一个2个元素的列表

> 第一个是value
>
> 第二个是set value function

* 可以把它解析成2个部分内容(destruct)

```tsx
const [selectIndex, setSelectIndex] = useState(-1);
```



* 使用`useState`的时候,应该放在组件函数中,保证生命周期足够



# 夜晚/白天模式切换

toggle mode function

```tsx
function toggleTheme(): void {
  // 获取当前的主题模式
  const currentTheme = document.documentElement.getAttribute("data-bs-theme");

  // 根据当前的主题模式切换到另一种模式
  if (currentTheme === "dark") {
    document.documentElement.setAttribute("data-bs-theme", "light");
  } else {
    document.documentElement.setAttribute("data-bs-theme", "dark");
  }
}
```



* 设计一个`switch`按钮绑上去即可



# 获取界面元素

```tsx
import { useRef } from "react";

const Alert = () => {
  const inputRef = useRef(null);
  return (
    <div>
      <input type="text" ref={inputRef} />
      <button
        onClick={() => {
          console.log(inputRef.current);
        }}
      >
        Click
      </button>
    </div>
  );
};

export default Alert;

```

* `current`代表可用时指向的对象,然后可以使用**属性名**访问相应内容