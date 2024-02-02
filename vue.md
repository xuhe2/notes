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



## `v-model`参数

默认情况下，`v-model` 在组件上都是使用 `modelValue` 作为 prop，并以 `update:modelValue` 作为对应的事件。

特殊情况我们可以修改`modelValue`作为别的名字,比如

```vue
<MyComponent v-model:title="bookTitle" />
```

```vue
<script setup>
defineProps(['title'])
defineEmits(['update:title'])
</script>
```



## 在组件中使用多个`v-model`参数

比如

使用方式

```vue
<UserName
  v-model:first-name="first"
  v-model:last-name="last"
/>
```

实现方式

```vue
<script setup>
defineProps({
  firstName: String,
  lastName: String
})

defineEmits(['update:firstName', 'update:lastName'])
</script>

<template>
  <input
    type="text"
    :value="firstName"
    @input="$emit('update:firstName', $event.target.value)"
  />
  <input
    type="text"
    :value="lastName"
    @input="$emit('update:lastName', $event.target.value)"
  />
</template>
```



## `v-model`修饰符

比如`.trim`，`.number` 和 `.lazy`



修饰符的访问可以使用

```vue
<script setup>
const props = defineProps({
  modelValue: String,
  modelModifiers: { default: () => ({}) }
})

defineEmits(['update:modelValue'])

console.log(props.modelModifiers) // { capitalize: true }
</script>

<template>
  <input
    type="text"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>
```

> `modelModifiers`是用来访问修饰符的方式

注意这里组件的 `modelModifiers` prop 包含了 `capitalize` 且其值为 `true`，因为它在模板中的 `v-model` 绑定 `v-model.capitalize="myText"` 上被使用了

> 我们需要手动检查然后实现这个部分

```vue
<script setup>
const props = defineProps({
  modelValue: String,
  modelModifiers: { default: () => ({}) }
})

const emit = defineEmits(['update:modelValue'])

function emitValue(e) {
  let value = e.target.value
  if (props.modelModifiers.capitalize) {
    value = value.charAt(0).toUpperCase() + value.slice(1)
  }
  emit('update:modelValue', value)
}
</script>

<template>
  <input type="text" :value="modelValue" @input="emitValue" />
</template>
```



# 透传属性`attributes`

当一个属性被传递给自己定义的组件,但是我没有在`props`,`emits`中设置这些属性参数,属性会被透传

当一个组件以单个元素为根作渲染时，透传的 attribute 会自动被添加到根元素上。举例来说，假如我们有一个 `<MyButton>` 组件

```vue
<!-- <MyButton> 的模板 -->
<button>click me</button>
```

透传的时候,会是

```vue
<MyButton class="large" />
```

我们知道父元素的属性是可以被子组件继承的

所以

```vue
<button class="large">click me</button>
```



* 对于`v-on`一样有作用



* 使用`defineEmits`,`defineProps`的时候,相当于是消费了参数



## 禁用透传参数

> 通过设置`inheritAttrs: false`来实现

在 `<script setup>` 中使用 [`defineOptions`](https://cn.vuejs.org/api/sfc-script-setup.html#defineoptions)

```vue
<script setup>
defineOptions({
  inheritAttrs: false
})
// ...setup 逻辑
</script>
```

* 透传进来的参数可以使用`$attrs`访问

- 和 props 有所不同，透传 attributes 在 JavaScript 中保留了它们原始的大小写，所以像 `foo-bar` 这样的一个 attribute 需要通过 `$attrs['foo-bar']` 来访问。
- 像 `@click` 这样的一个 `v-on` 事件监听器将在此对象下被暴露为一个函数 `$attrs.onClick`。



## 多根节点透传

* 需要手动的显式绑定

```vue
<header>...</header>
<main v-bind="$attrs">...</main>
<footer>...</footer>
```



# 插槽

我们写在组件中的内容被称为`插槽内容`

> 使用`<slot/>`实现插入

```vue
<template>
  <button class="fancy-btn">
  	<slot/> <!-- slot outlet -->
	</button>
</template>

<style>
.fancy-btn {
  color: #fff;
  background: linear-gradient(315deg, #42d392 25%, #647eff);
  border: none;
  padding: 5px 10px;
  margin: 5px;
  border-radius: 8px;
  cursor: pointer;
}
</style>
```



* 注意,插槽的内容不局限于文本,可以是HTML

```vue
<script setup>
import FancyButton from './FancyButton.vue'
import AwesomeIcon from './AwesomeIcon.vue'
</script>

<template>
  <FancyButton>
    Click me
 	</FancyButton>
  <FancyButton>
    <span style="color:cyan">Click me! </span>
    <AwesomeIcon />
  </FancyButton>
</template>
```



## 设置默认插槽

如果我们想在父组件没有提供任何插槽内容时在 `<button>` 内渲染“Submit”，只需要将“Submit”写在 `<slot>` 标签之间来作为默认内容

```vue
<button type="submit">
  <slot>
    Submit <!-- 默认内容 -->
  </slot>
</button>
```



## 具名插槽

如果我需要把一些内容分开来插入到里面去,给部分内容设置插槽的名字很方便

```vue
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```

> 使用`<template>`和`v-slot`配合使用

```vue
<BaseLayout>
  <template v-slot:header>
    <!-- header 插槽的内容放这里 -->
  </template>
</BaseLayout>
```

* 可以把`v-slot`简写成`#`.

* 默认的`<slot>`可以写作`#default`(当然也可以不写,作为隐藏式的默认插槽)



## 给插槽传递参数

在某些场景下插槽的内容可能想要同时使用父组件域内和子组件域内的数据。要做到这一点，我们需要一种方法来让子组件在渲染时将一部分数据提供给插槽。

```vue
<!-- <MyComponent> 的模板 -->
<div>
  <slot :text="greetingMessage" :count="1"></slot>
</div>
```

```vue
<MyComponent v-slot="slotProps">
  {{ slotProps.text }} {{ slotProps.count }}
</MyComponent>
```



# 依赖注入

当我们需要给一个组件的**深层子组件**传递内容的时候,我们依赖**透传参数**,但是,着可能造成不必要的组件也获得了参数



## 使用`provide`和`inject`

```js
import { ref, provide } from 'vue'

const count = ref(0)
provide('key', count)
```

```js
<script setup>
import { inject } from 'vue'

const message = inject('message')
</script>
```



* 设置默认值

```vue
// 如果没有祖先组件提供 "message"
// `value` 会是 "这是默认值"
const value = inject('message', '这是默认值')
```





* 使用`工厂函数`

在一些场景中，默认值可能需要通过调用一个函数或初始化一个类来取得。为了避免在用不到默认值的情况下进行不必要的计算或产生副作用，我们可以使用工厂函数来创建默认值：

```js
const value = inject('key', () => new ExpensiveClass(), true)
```



## 一次传入多个

```js
<!-- 在供给方组件内 -->
<script setup>
import { provide, ref } from 'vue'

const location = ref('North Pole')

function updateLocation() {
  location.value = 'South Pole'
}

provide('location', {
  location,
  updateLocation
})
</script>
```

```js
<!-- 在注入方组件 -->
<script setup>
import { inject } from 'vue'

const { location, updateLocation } = inject('location')
</script>

<template>
  <button @click="updateLocation">{{ location }}</button>
</template>
```



## 被注入的值确保`read-only`

```js
<script setup>
import { ref, provide, readonly } from 'vue'

const count = ref(0)
provide('read-only-count', readonly(count))
</script>
```



## 使用`symbol`

至此，我们已经了解了如何使用字符串作为注入名。但如果你正在构建大型的应用，包含非常多的依赖提供，或者你正在编写提供给其他开发者使用的组件库，建议最好使用 Symbol 来作为注入名以避免潜在的冲突。

我们通常推荐在一个单独的文件中导出这些注入名 Symbol：



```js
// keys.js
export const myInjectionKey = Symbol()
```



```js
// 在供给方组件中
import { provide } from 'vue'
import { myInjectionKey } from './keys.js'

provide(myInjectionKey, { /*
  要提供的数据
*/ });
```



```js
// 注入方组件
import { inject } from 'vue'
import { myInjectionKey } from './keys.js'

const injected = inject(myInjectionKey)
```



# 接受响应式的状态

```js
// fetch.js
import { ref } from 'vue'

export function useFetch(url) {
  const data = ref(null)
  const error = ref(null)

  fetch(url)
    .then((res) => res.json())
    .then((json) => (data.value = json))
    .catch((err) => (error.value = err))

  return { data, error }
}
```

```js
const url = ref('/initial-url')

const { data, error } = useFetch(url)

// 这将会重新触发 fetch
url.value = '/new-url'
```



# 自定义指令

在 `<script setup>` 中，任何以 `v` 开头的驼峰式命名的变量都可以被用作一个自定义指令。在下面的例子中，`vFocus` 即可以在模板中以 `v-focus` 的形式使用。

```js
<script setup>
// 在模板中启用 v-focus
const vFocus = {
  mounted: (el) => el.focus()
}
</script>

<template>
  <input v-focus />
</template>
```



## 实现

```js
<div v-demo="{ color: 'white', text: 'hello!' }"></div>
```

```js
app.directive('demo', (el, binding) => {
  console.log(binding.value.color) // => "white"
  console.log(binding.value.text) // => "hello!"
})
```



# npm

```powershell
npm install --registry https://registry.npm.taobao.org
```



# 懒加载

```vue
const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  }
]
```



# 路由



```vue
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
```

> 在`app.vue`文件中使用



```vue
  <router-view />
```

> 路由的视图



## 使用子路由

> index.js配置

```javascript
import { createRouter, createWebHistory } from 'vue-router'

const routes = [
  {
    path: '/',
    name: 'Layout',
    component: () => import('../views/Layout/Layout.vue'),
    children: [{
      path: '/user',
      name: 'user',
      component: () => import('../views/Pages/UserList.vue')
    },]
  }
]

const router = createRouter({
  history: createWebHistory(),
  routes
})

export default router
```



使用**element-plus**组件库之后可以实现更好的效果

布局方面,使用

```vue
<template>
    <div class="common-layout">
        <el-container>
            <el-header>Header</el-header>
            <el-container>
                <el-aside width="200px">
                    <RouterLink to="/user">user</RouterLink>
                </el-aside>
                <el-main>
                    <RouterView></RouterView>
                </el-main>
            </el-container>
        </el-container>
    </div>
</template>
```

> 边栏的选择的路由会在`<RouterView>`中展示内容



# 具名导出,默认导出



- 不使用{}的时候，表示导入模块的**默认导出**（export default），这种方式只能导入一个值，而且可以随意命名，例如 `import A from './A'`。
- 使用{}的时候，表示导入模块的**命名导出**（export），这种方式可以导入多个值，但是必须和模块中的导出名称一致，例如 `import { A, B, C } from './A'`。
- 如果模块中既有默认导出又有命名导出，可以同时使用两种方式导入，例如 `import A, { B, C } from './A'`，其中A是默认导出，B和C是命名导出。
- 如果想要在导入的时候重命名导入的值，可以使用 `as` 关键字，例如 `import { A as X, B as Y } from './A'`，这样就可以用X和Y代替A和B。



# 使用**element-plus**设置表单

```vue
<el-form ref="formRef" :model="loginData" label-width="120px" class="demo-dynamic">
    <el-form-item prop="email" label="Email" :rules="[
        {
            required: true,
            message: 'Please input email address',
            trigger: 'blur',
        },
        {
            type: 'email',
            message: 'Please input correct email address',
            trigger: ['blur', 'change'],
        },
    ]">
        <el-input v-model="dynamicValidateForm.email" />
    </el-form-item>
    <el-form-item v-for="(domain, index) in dynamicValidateForm.domains" :key="domain.key" :label="'Domain' + index"
        :prop="'domains.' + index + '.value'" :rules="{
            required: true,
            message: 'domain can not be null',
            trigger: 'blur',
        }">
        <el-input v-model="domain.value" />
        <el-button class="mt-2" @click.prevent="removeDomain(domain)">Delete</el-button>
    </el-form-item>
    <el-form-item>
        <el-button type="primary" @click="submitForm(formRef)">Submit</el-button>
        <el-button @click="addDomain">New domain</el-button>
        <el-button @click="resetForm(formRef)">Reset</el-button>
    </el-form-item>
</el-form>
```

> 其中`:model`绑定的是**存储你想要获得的数据的字典**
>
> 在`el-form-item`中使用`prop="email"`绑定存储数据的字典的key



# 使用`@`

这样，你就可以在任何地方使用`@`来引用`src`目录下的文件，而不用担心当前文件的位置。例如，你可以这样导入`src/stores/counter.js`文件：

```js
import { useCounterStore } from '@/stores/counter'
```



# pinia

全局变量管理工具

```js
// stores/counter.js
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', {
  state: () => {
    return { count: 0 }
  },
  // 也可以这样定义
  // state: () => ({ count: 0 })
  actions: {
    increment() {
      this.count++
    },
  },
})
```

> 其中`state`是一个函数,返回的是一个字典对象



* `actions`是异步操作,可以返回`promise`



* 使用`pinia`构建的Store对象是一个具名的,使用的是具名导出



## 使用`store`



```js
import { useStore } from '@/Stores/index.js'
// 可以在组件中的任意位置访问 `store` 变量 ✨
const store = useStore();
```

1. 导入
2. 实例化,然后使用里面的变量



## 访问其中的`state`

```js
const store = useStore()

store.count++
```

> 直接访问`count`即可



* 重置为初始内容

```js
const store = useStore()

store.$reset()
```

```js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)

  function $reset() {
    count.value = 0
  }

  return { count, $reset }
})
```



## 访问引用和访问简单数据类型的区别

当试图获取一个简单的数据类型的时候

```js
const number = store.counter;
```

> 使用赋值给一个新的简单变量,是不可取的

> 但是获取一个复杂类型的时候,由于使用的是引用,这是可行的
>
> 函数也是可行的



## getters

创建函数,这个函数可以返回一个修改之后的属性值

```js
    getters: {
        doubleCount: (state) => state.counter * 2 // 定义一个getter
    }
```

> 传入state,是自己的,在实际使用的时候,它自动从实例中获得



## 组合式API风格编写pinia

```js
import { defineStore } from "pinia";

export const useStore = defineStore('counter', () => {
    const counter = 0;
    function increment() {
        this.counter++;
    }
    return { counter, increment }
});
```

> 最后需要return需要的内容



# js的this

指向的是使用当前函数的对象

> this来自上一级



* 使用严格模式的时候,不存在调用对象的时候,不会使用`window`,直接返回`undefined` 
* 使用`setTimeout`的时候,`this`指向的是windows



# 创建路由守卫

```js
router.beforeEach((to, from, next) => {}) 
```

> `to`:要前往的路由
>
> `from`:当前离开的路由
>
> `next`:函数,负责到下一个部分



* 注意,使用`next();`函数本身会触发路由守卫,可能导致死循环

```js
// 创建路由守卫
router.beforeEach((to, from, next) => {
  const userInfoStore = useUserInfoStore();
  if (!userInfoStore.userInfo.username && to.path !== '/login') {
    next('/login');
  } else {
    next();
  }
})
```

> 使用检查目标path的方式可以避免死循环



## 刷新造成pinia数据丢失

刷新会造成pinia数据丢失,需要使用数据持久化技术



## 储存在localStorage中避免丢失数据

加入`localStorage`

```js
localStorage.setItem("userInfo", JSON.stringify(loginData));
```





从`lcoalStorage`中读取数据

```js
import { defineStore } from "pinia";
import { reactive } from 'vue'

export const useUserInfoStore = defineStore('UserInfo', () => {
    const userInfo = reactive(localStorage.getItem('userInfo') ? JSON.parse(localStorage.getItem('userInfo')) : {});
    const setUserInfo = (info) => {
        Object.assign(userInfo, info);
    };
    return { userInfo, setUserInfo }
});
```

* 注意,存储的数据可能不存在



## 退出

```js
import LayoutMenu from '../Menu/LayoutMenu.vue'
import { useRouter } from 'vue-router';

import { useUserInfoStore } from '@/Stores/UserInfo';

const store = useUserInfoStore();
const router = useRouter();

function logout() {
    // 退出登陆逻辑
    localStorage.removeItem('userInfo');
    // 清除用户信息(当前)
    store.userInfo = {};
    // 跳转到登陆页面
    router.push('/login');
}
```





# 在JS代码中实现路由跳转

```js
const store = useUserInfoStore();
const router = useRouter();
function handleLogin() {
    store.userInfo = loginData;
    router.push("/"); // 跳转到主页，具体路由根据实际情况调整
};
```

* 注意,变量定义必须在外面



# axios

使用`axios`实现HTTP请求



* `timeout`指的是请求超时的时间



## 请求拦截和响应拦截

使用`axios`的方法实现拦截

```js
// 请求拦截
loginService.interceptors.request.use(
    config => {
        loading = ElLoading.service({
            lock: true,
            text: 'Loading',
            background: 'rgba(0, 0, 0, 0.7)'
        });
        return config;
    }
);
```

> 需要返回配置信息



## 出错时展示

使用element-plus的message展示错误消息



```js
import { ElMessage } from 'element-plus'
```

> 使用`Elmessage`展示



```js
        ElMessage({
            message: '网络异常',
            type: 'error'
        })
```

> 使用对象



## AXIOS的消息类型

axios 的 responseType 是一个选项，用于指定服务器响应的数据类型。不同的 responseType 可以影响 axios 如何处理响应数据。以下是一些常见的 responseType 类型及其用法示例：

- 默认值： ‘json’ ，会自动解析响应数据并返回一个 JavaScript 对象。例如：

```js
axios.get('/api/data').then(response => {
  console.log(response.data); // 返回解析后的 JavaScript 对象
});
```

- ‘arraybuffer’ ：返回一个 ArrayBuffer 对象，适用于处理二进制数据。例如：

```js
axios.get('/api/data', { responseType: 'arraybuffer' }).then(response => {
  console.log(response.data); // 返回 ArrayBuffer 对象
});
```

- ‘blob’ ：返回一个 Blob 对象，适用于处理图像等二进制数据。例如：

```js
axios.get('/api/image', { responseType: 'blob' }).then(response => {
  console.log(response.data); // 返回 Blob 对象
});
```

- ‘document’ ：返回一个 Document 对象，适用于处理 HTML/XML 数据。例如：

```js
axios.get('/api/data', { responseType: 'document' }).then(response => {
  console.log(response.data); // 返回 Document 对象
});
```

- ‘text’ ：返回一个字符串，适用于处理纯文本数据。例如：

```js
axios.get('/api/data', { responseType: 'text' }).then(response => {
  console.log(response.data); // 返回字符串
});
```

- ‘stream’ ：返回一个 Stream 对象，适用于处理流式数据。例如：

```js
// GET request for remote image in node.js
axios({
  method: 'get',
  url: '^5^',
  responseType: 'stream'
}).then(function (response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});
```

