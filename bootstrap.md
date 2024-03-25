* 项目初始化时候的样式可能造成冲突



# 响应式



## 导航栏

以导航栏为例

只有在页面大小足够的时候才显示内容, 

```react
import "./App.css";

function App() {
  return (
    <>
      <nav
        className="navbar bg-dark border-bottom border-body navbar-expand-lg"
        data-bs-theme="dark"
      >
        <a className="navbar-brand" href="#">
          Title
        </a>
        <div className="collapse navbar-collapse">
          <ul className="navbar-nav me-auto mb-2 mb-lg-0">
            <li className="nav-item">
              <a className="nav-link active" aria-current="page" href="#">
                Home
              </a>
            </li>
            <li className="nav-item">
              <a className="nav-link" href="#">
                Features
              </a>
            </li>
            <li className="nav-item">
              <a className="nav-link" href="#">
                Pricing
              </a>
            </li>
          </ul>
        </div>
      </nav>
    </>
  );
}

export default App;

```

需要使用一个`navbar-expand-lg`样式申明这部分是响应式的, lg代表large, 检测屏幕的像素点

> 修改`lg`部分的内容, 可以设置不同的变换位置

子元素使用`collapse navbar-collapse`



### 设置导航栏按钮

```react
		<button
          className="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span className="navbar-toggler-icon"></span>
        </button>
```

一个拥有自己属性的button

* 注意, 需要配置**控制的内容的ID**

```react
<div className="collapse navbar-collapse" id="navbarNav">
```



## 固定到顶部

使用`fixed-top`的样式

* 注意, 这个导航栏可能遮挡别的内容, 可以使用伪类把内容放到下面去



## container

使用自带的容器样式, 可以保证边距

```react
<div className="container">
```





# 设置margin

使用`ms-auto`设置margin start = margin left作为auto, 就是左边自动填充

使用`me-auto`设置右边的填充



# 设置padding

使用`p-5`样式

> 这个5的单位是`rem`, 代表字节长度



# 居中

使用`text-lg-center`, 当满足`large`的时候, 会居中



# 布局

使用`d-md-flex`, 满足中间大小的时候, 使用`flex`布局方式