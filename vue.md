# 项目目录结构

`node_modules`项目运行依赖文件

`public`资源文件夹

`src`源码文件夹

`index.html`入口文件

`package.json`信息描述文件

`vue.config.js`vue配置文件



# 文本插值

```vue
<span>Message: {{ msg }}</span>
```



# 原始HTML

```vue
<p>Using text interpolation: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```



* 这里看到的 `v-html` attribute 被称为一个**指令**。



# 响应式变量

使用`ref`

[在Vue.js中，响应式变量是指可以自动追踪其变化并更新视图的变量。在Vue.js 3.0中，响应式变量是通过JavaScript的Proxy对象实现的。Vue.js提供了两种方法来创建响应式变量：`ref()`和`reactive()`。`ref()`用于创建单个值的响应式变量，而`reactive()`用于创建对象和数组的响应式变量。在Vue.js中，可以使用`$refs`对象来访问DOM元素或组件实例的引用。如果您想了解更多关于Vue.js响应式变量的信息，请查看以下链接：](https://cn.vuejs.org/guide/essentials/reactivity-fundamentals.html)[1](https://bing.com/search?q=响应式变量)[2](https://cn.vuejs.org/guide/essentials/reactivity-fundamentals.html)[3](https://blog.csdn.net/qq_38249409/article/details/129593767)[4](https://cn.vuejs.org/guide/extras/reactivity-transform.html) 。



# 绑定属性



## Attribute 绑定

双大括号不能在 HTML attributes 中使用。想要响应式地绑定一个 attribute，应该使用 [`v-bind` 指令](https://cn.vuejs.org/api/built-in-directives.html#v-bind)：

template

```
<div v-bind:id="dynamicId"></div>
```



## 简写

因为 `v-bind` 非常常用，我们提供了特定的简写语法：

template

```vue
<div :id="dynamicId"></div>
```



> 使用绑定的方式实现按钮是否可用



## 绑定JSON对象



```javascript
data() {
  return {
    objectOfAttrs: {
      id: 'container',
      class: 'wrapper'
    }
  }
}
```



```vue
<div v-bind="objectOfAttrs"></div>
```



# 指令

> 使用`v-`开头的特殊的属性是`指令`

```
<p v-if="seen">Now you see me</p>
```

这里，`v-if` 指令会基于表达式 `seen` 的值的真假来移除/插入该 `<p>` 元素。

* 通过`vue`官网的`API文档`进行查看

# 参数

有些指令(特殊属性)需要一些参数,指令和参数之间使用`:`分割



# 动态参数

参数的名字也可以是动态决定的

```vue
<!--
注意，参数表达式有一些约束，
参见下面“动态参数值的限制”与“动态参数语法的限制”章节的解释
-->
<a v-bind:[attributeName]="url"> ... </a>

<!-- 简写 -->
<a :[attributeName]="url"> ... </a>
```



当使用 DOM 内嵌模板 (直接写在 HTML 文件里的模板) 时，我们需要避免在名称中使用大写字母，因为浏览器会强制将其转换为小写：

template

```
<a :[someAttr]="value"> ... </a>
```

上面的例子将会在 DOM 内嵌模板中被转换为 `:[someattr]`。如果你的组件拥有 “someAttr” 属性而非 “someattr”，这段代码将不会工作。单文件组件内的模板**不**受此限制。



# 计算属性

针对一些属性,我们需要对里面的部分进行处理之后返回一个值

> 使用`computed`

```javascript
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  },
  computed: {
    // 一个计算属性的 getter
    publishedBooksMessage() {
      // `this` 指向当前组件实例
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  }
}
```



# 对象和样式的绑定

在绑定`class`属性的时候

```vue
<div :class="{ active: isActive }"></div>
```

上面的语法表示 `active` 是否存在取决于数据属性 `isActive` 的[真假值](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)。

> 同时使用多个`class`定义样式的时候可以使用这样子真假值的方式,方便后续的添加和删除



* 可以直接使用对象实现上述的多个`class`的绑定

```vue
data() {
  return {
    classObject: {
      active: true,
      'text-danger': false
    }
  }
}
<div :class="classObject"></div>
```



# 使用数组来绑定

> 这样绑定可以修改`class`的名

```vue
data() {
  return {
    activeClass: 'active',
    errorClass: 'text-danger'
  }
}
<div :class="[activeClass, errorClass]"></div>
```

```vue
<div class="active text-danger"></div>
```



# 内联样式

> 使用`style`来确定你的CSS样式



* 使用**自动前缀**的技术
* 可以使用数组的方式放入多个值



# 条件渲染

> 使用`v-if`指令

```vue
<h1 v-if="awesome">Vue is awesome!</h1>
```

> 只有在表达式返回`true`的时候才能正常渲染



> 使用`v-else`指令

```vue
<button @click="awesome = !awesome">Toggle</button>

<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

* 一个 `v-else` 元素必须跟在一个 `v-if` 或者 `v-else-if` 元素后面，否则它将不会被识别



> 使用`v-else-if`

```vue
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```



> 使用`v-show`来渲染元素

```vue
<h1 v-show="ok">Hello!</h1>
```

* 不同之处在于 `v-show` 会在 DOM 渲染中保留该元素；`v-show` 仅切换了该元素上名为 `display` 的 CSS 属性。



# `v-for`

* 可以使用数字代表循环次数

```vue
<span v-for="n in 10">{{ n }}</span>
```



* 当它们同时存在于一个节点上时，`v-if` 比 `v-for` 的优先级更高。这意味着 `v-if` 的条件将无法访问到 `v-for` 作用域内定义的变量别名

```vue
<!--
 这会抛出一个错误，因为属性 todo 此时
 没有在该实例上定义
-->
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo.name }}
</li>
```





# `v-for`列表渲染

> 使用`v-for`

```vue
data() {
  return {
    items: [{ message: 'Foo' }, { message: 'Bar' }]
  }
}
<li v-for="item in items">
  {{ item.message }}
</li>
```

* 可以使用第二个参数,第二个参数是当前项的位置索引



> 使用`in`代替`of`

```vue
<div v-for="item of items"></div>
```



# `v-for`和对象

> 可以使用对象解析的方式访问对象



# 事件绑定

> 使用`@`/`v-on`

* 函数的参数可以是`event`代表当前的事件的参数



## 内联事件

* 模板编译器会通过检查 `v-on` 的值是否是合法的 JavaScript 标识符或属性访问路径来断定是何种形式的事件处理器。举例来说，`foo`、`foo.bar` 和 `foo['bar']` 会被视为方法事件处理器，而 `foo()` 和 `count++` 会被视为内联事件处理器。

```vue
<button @click="say('hello')">Say hello</button>
<button @click="say('bye')">Say bye</button>
```

> 本质是当成函数被执行



* 在内联事件中使用`event`参数

有时我们需要在内联事件处理器中访问原生 DOM 事件。你可以向该处理器方法传入一个特殊的 `$event` 变量，或者使用内联箭头函数



## 案件修饰符

```vue
<!-- 仅在 `key` 为 `Enter` 时调用 `submit` -->
<input @keyup.enter="submit" />
```



* 设置确切的按键

```vue
<!-- 当按下 Ctrl 时，即使同时按下 Alt 或 Shift 也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 仅当按下 Ctrl 且未按任何其他键时才会触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 仅当没有按下任何系统按键时触发 -->
<button @click.exact="onClick">A</button>
```



# 表单输入绑定

当输入内容改变的时候,变量的内容实时改变

```vue
<p>Message is: {{ message }}</p>
<input v-model="message" placeholder="edit me" />
```

* `checkbox`/`radio`也可以这样操作



可以把多个内容放入数组之中去

```vue
<div>Checked names: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames">
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
<label for="mike">Mike</label>
```



使用`v-for`渲染复选框

```vue
export default {
  data() {
    return {
      selected: 'A',
      options: [
        { text: 'One', value: 'A' },
        { text: 'Two', value: 'B' },
        { text: 'Three', value: 'C' }
      ]
    }
  }
}
<select v-model="selected">
  <option v-for="option in options" :key="option.value" :value="option.value">
    {{ option.text }}
  </option>
</select>

<div>Selected: {{ selected }}</div>
```



## `v-model`修饰符

`.lazy`在每次**change**事件之后,而不是全程实时更新

> 比如,一个`<input>`标签,只有在它输入并且失去焦点的时候,才会更新内容



`.number`自动把内容编译成数字

> 不能正确编译的时候,返回原来的数字



`.trim`去除输入内容的开头和结尾的空格



# 生命周期

在执行一系列的渲染操作之前执行某个函数



# 定义一个组件

```vue
<script>
export default {
  data() {
    return {
      count: 0
    }
  }
}
</script>

<template>
  <button @click="count++">You clicked me {{ count }} times.</button>
</template>
```

或者

```vue
export default {
  data() {
    return {
      count: 0
    }
  },
  template: `
    <button @click="count++">
      You clicked me {{ count }} times.
    </button>`
}
```

* 是的,不需要在单个的`vue`文件中定义自己组件的名字,注意,你的组件的名字应该是你的文件名

* 组件的名字还是使用**大驼峰**命名法好



# 使用组件

```vue
<script>
import ButtonCounter from './ButtonCounter.vue'

export default {
  components: {
    ButtonCounter
  }
}
</script>

<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
</template>
```

> 这些`components`的声明很麻烦,在`vue3`中可以使用`setup`去掉



## 设置可以传递过去的参数

> 传递`props`参数

```vue
<!-- BlogPost.vue -->
<script>
export default {
  props: ['title']
}
</script>

<template>
  <h4>{{ title }}</h4>
</template>
```

* 因为参数可以是多个的,所以,使用的是`列表`



在`VUE3`中使用`defineProps`函数



> 设置`emits`参数
>
> 是方法名字



## 使用插槽分配内容

> 使用`<slot />`实现



# 组件注册



1. 全局注册

> 可以在任何地方使用这个组件

2. 局部注册

> 需要手动导入



# 使用`props`声明

```vue
export default {
  props: {
    title: String,
    likes: Number
  }
}
```

> 可以使用上面的代码实现预期的类型,如果类型错误,会在console丢出

```vue
// 使用 <script setup>
defineProps({
  title: String,
  likes: Number
})
```



* 传递`prop`的时候,我们可以使用`-`作为间隔的接近`HTML属性`的表达方式
* 注意,`props`是只读的变量



## 想修改`props`但是不影响外部的变量

```vue
const props = defineProps(['initialCounter'])

// 计数器只是将 props.initialCounter 作为初始值
// 像下面这样做就使 prop 和后续更新无关了
const counter = ref(props.initialCounter)
```



## `props`校验

```vue
defineProps({
  // 基础类型检查
  // （给出 `null` 和 `undefined` 值则会跳过任何类型检查）
  propA: Number,
  // 多种可能的类型
  propB: [String, Number],
  // 必传，且为 String 类型
  propC: {
    type: String,
    required: true
  },
  // Number 类型的默认值
  propD: {
    type: Number,
    default: 100
  },
  // 对象类型的默认值
  propE: {
    type: Object,
    // 对象或数组的默认值
    // 必须从一个工厂函数返回。
    // 该函数接收组件所接收到的原始 prop 作为参数。
    default(rawProps) {
      return { message: 'hello' }
    }
  },
  // 自定义类型校验函数
  propF: {
    validator(value) {
      // The value must match one of these strings
      return ['success', 'warning', 'danger'].includes(value)
    }
  },
  // 函数类型的默认值
  propG: {
    type: Function,
    // 不像对象或数组的默认，这不是一个
    // 工厂函数。这会是一个用来作为默认值的函数
    default() {
      return 'Default function'
    }
  }
})
```



> Boolean类型的特殊的转换

```
defineProps({
  disabled: Boolean
})
```

该组件可以被这样使用：

```vue
<!-- 等同于传入 :disabled="true" -->
<MyComponent disabled />

<!-- 等同于传入 :disabled="false" -->
<MyComponent />
```



# 事件绑定

> 使用`emits`
>
> 也可以使用`defineEmits`实现(VUE3)



* 可以传递对象进入,实现事件校验(校验参数是否合理)

```vue
<script setup>
const emit = defineEmits({
  // 没有校验
  click: null,

  // 校验 submit 事件
  submit: ({ email, password }) => {
    if (email && password) {
      return true
    } else {
      console.warn('Invalid submit event payload!')
      return false
    }
  }
})

function submitForm(email, password) {
  emit('submit', { email, password })
}
</script>
```



# `v-model`组件使用

在`<input>`中使用`v-model`

```vue
<input v-model="searchText" />
```

会被编译成

```vue
<input
  :value="searchText"
  @input="searchText = $event.target.value"
/>
```



在一个组件中使用的时候,会被编译成

```vue
<CustomInput
  :modelValue="searchText"
  @update:modelValue="newValue => searchText = newValue"
/>
```

所以,我们在编写可以使用`v-model`的组件的时候,需要使用

```vue
<!-- CustomInput.vue -->
<script setup>
defineProps(['modelValue'])
defineEmits(['update:modelValue'])
</script>

<template>
  <input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>
```

