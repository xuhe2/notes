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



# 是否渲染当前元素

使用JS的`&&`特性实现

```js
{flag && <input/>};
```



# hook函数

使用**函数闭包**的方式实现



使用规则:

1. 只能在组件中和其他的hook函数中使用
2. 在组件的顶层中调用(不能在if/for函数中)



# redux

用来管理**全局变量**

* 数据不可变



```bash
npm install @reduxjs/toolkit react-redux
```



文件保存在`store`文件夹下

需要一个`index.js`文件,配置使用`redux`

实例文件保存在`models`文件夹下



## `index.js`

查看官方文档

> 使用`configureStore `注册



```js
import { configureStore } from '@reduxjs/toolkit'

export default configureStore({
  reducer: {}
})
```



## `index.ts`

使用TS的语法避免报错信息

```ts
import { configureStore } from '@reduxjs/toolkit'

import counterReducer from "./models/counterSlice.ts";

const store =  configureStore({
    reducer: {
        counter: counterReducer
    }
})

export default store;
// 从 store 本身推断出 `RootState` 和 `AppDispatch` 类型
export type RootState = ReturnType<typeof store.getState>
// 推断出类型: {posts: PostsState, comments: CommentsState, users: UsersState}
export type AppDispatch = typeof store.dispatch

```





## `counterSlice.ts`

```tsx
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
    name: "counter",
    initialState: {
        value: 0
    },
    reducers: {
        increment: state => {
            state.value++;
        },
        decrement: state => {
            state.value--;
        }
    }
})

// 按需导出
export const { increment, decrement } = counterSlice.actions;
// 默认导出
export default counterSlice.reducer;
```

> 使用`initialState`设定初始化状态
>
> `reducers`作为处理状态的函数



## 注册reducer

```tsx
import { configureStore } from '@reduxjs/toolkit'

import counterReducer from "./models/counter";

export default configureStore({
    reducer: {
        counter: counterReducer
    }
})
```



## 在`main.ts`中加入`Provider`

```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.tsx";
import "./index.css";
// import bootstrap
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap/dist/js/bootstrap.bundle.min.js";
// import redux
import store from "./store/index.ts";
import { Provider } from "react-redux";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);

```

* 应该使用完整的文件名, 不应该缺少后缀名



## 定义`hooks.ts`

为防止TS语法的报错信息, 需要使用`hooks.ts`中的函数

```ts
import { TypedUseSelectorHook, useDispatch, useSelector } from 'react-redux'
import type { RootState, AppDispatch } from './index'

// 在整个应用程序中使用，而不是简单的 `useDispatch` 和 `useSelector`
export const useAppDispatch: () => AppDispatch = useDispatch
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector
```

使用`useAppDispatch`代替`useDispatch`

使用`useAppSelector`代替`useSelector`



## 在组件中使用`redux`

需要从`Slice`文件中导入`action`函数

从`hooks.ts`导入`useAppSelector`,`useAppDispatch`

```tsx
import { increment, decrement } from "../store/models/counterSlice.ts";
import { useAppDispatch, useAppSelector } from "../store/hooks.ts";

const Alert = () => {
  const count = useAppSelector((state) => state.counter.value);
  const dispatch = useAppDispatch();

  return (
    <>
      <div>{count}</div>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(decrement())}>-</button>
    </>
  );
};

export default Alert;

```



# react router

使用了router之后, 不需要使用`<App />`



## `src/routes/index.tsx`

```tsx
import App from "../App.tsx";
import { createBrowserRouter } from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    element: <App></App>,
  },
]);

export default router;

```

> 路由配置界面



## `main.tsx`

```tsx
// use router
import { RouterProvider } from "react-router-dom";
import router from "./routes/index.tsx";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <Provider store={store}>
      <RouterProvider router={router} />
    </Provider>
  </React.StrictMode>
);

```



## 跳转界面



### 声明式导航

使用`<Link>`跳转

> `to`属性作为需要跳转到的URL

```tsx
import { Link } from "react-router-dom";

const HomePage = () => {
  return (
    <>
      <div>HomePage</div>
      <Link to="/about">About</Link>
    </>
  );
};

export default HomePage;

```

* 是整个界面跳转



## 函数式导航

```tsx
const navigate = useNavigate();

<button onClick={() => navigate("about")}></button>
```



## 使用参数传递



## 嵌套路由

使用`children`配置路由嵌套关系

使用`<Outlet/>`作为二级路由的渲染位置



* 默认的二级路由

> 不需要`path`属性, 使用`index=true`实现



* 404 not found 界面

> `path`设置为`*`的时候, 就是`not found`的时候自动跳转的界面