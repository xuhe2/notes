使用`VUE3`组合式API写法



# 克隆项目模板

国内的网速问题,所以,使用git去gitee克隆模板

```bash
git clone -b vite --depth=1 https://gitee.com/dcloud/uni-preset-vue.git
```

* 使用`vite`分支
* 只克隆最新的commit



# 初始化

使用`yarn`命令构建`node_modles`



# 使用H5模式开发

```bash
npm run dev:h5
```



# view

使用`<view>`而不是`<div>`可以实现更多的功能,在移动端适配的时候,更加好

> 当子元素被点击的时候,不希望父元素起反应,使用**阻止冒泡**.



* `hover-class`控制的是**按下的时候,class**

* `hover-stay-time`可以控制松手之后的保留状态



# text

文本应该放在`<text>`组件中,不能直接放在`<view>`中

* 使用`<text>`包裹的内容可以被赋值,但是`view`不可以

> 使用`selectable`属性



# 界面跳转

使用`<navigator>1</navigator>`可以实现



界面需要先在`pages.json`文件中注册(类似`router`实现)



* 当使用默认的跳转方式的时候,无法跳转到使用`tabBar`的界面



## 修改页面的标题内容

使用`uni.setNavigationBarTitle`API调用实现



## 使用API调用的方法实现跳转界面

```js
	function goHome() {
		uni.navigateTo({
			url: '/src/pages/index/index'
		})
	}
```

> 注意,无法使用API调用的方式跳到一个tabBar中的页面中去



* 使用`uni.navigateBack`可以实现回到上一个页面



# 底部导航栏

配置`pages.json`页面路由实现



* 需要实现`list`数组,里面是对象

* 使用的路由需要不适用`@`
* icon可以使用例如`iconfont`等

* 不支持SVG



# 信息显示

使用`uni`的API实现相关的功能



```js
	uni.showToast({

	})
```



## 取消信息显示

使用`uni.hideXXX`实现



## 显示加载信息

使用`showLoading`实现

* 一般需要使用`mask`



## 显示可交互的信息

使用`showModel`实现



## 从底部弹出的菜单

使用`showActionSheet`



# 数据缓存

使用API实现

```js
uni.setStorageSync()
```

获取的时候

```js
uni.getStorageSync()
```

删除的时候

```js
uni.removeStorageSync()
```



# 发送请求

使用API实现

```js
	uni.request({
		url: "https://jsonplaceholder.typicode.com/posts",
		success: (res) => {
			console.log(res);
		}
	})
```

* 使用`method`参数实现修改请求类型



# 预览图片

使用`previewImage`API实现



# hook function

使用`onReachBottom`实现触底加载更多



使用`enablePullDownRefresh`刷新,然后在界面中使用`onPullDownRefresh`实现下拉的时候的操作(发送网络请求更新界面)

* 需要手动停止下拉刷新



# 使用扩展组件

安装拓展组件插件的时候出现问题,缺少**SASS**

使用yarn安装



# 使用MD5加密

参考博客https://blog.csdn.net/ksws01/article/details/128293383



```shell
yarn add js-md5 -D
```



直接使用导入包的形式使用



# 使用拓展组件的弹出层

使用VUE3组合API写法的时候,需要定义好

```js
const popup = ref(null); // 创建一个引用
```



```vue
	<view>
		<uni-popup ref="popup" type="message">
			<uni-popup-message type="error" :duration="2000">
				error info
			</uni-popup-message>
		</uni-popup>
	</view>
```

定义组件



```js
popup.value.open('top'); // 使用.value来访问引用的实例
```

使用组件



# 文件传输

使用`uni`的扩展组件实现效果

```vue
<template>
	<view>
		<uni-file-picker :auto-upload="false" del-icon="" file-mediatype="image" mode="list" v-model:value="files.value"
			@select="select">
			<view class="file-picker">
				<uni-icons type="cloud-upload" size="100rpx"></uni-icons>
				<text>click to upload file</text>
			</view>
		</uni-file-picker>
		<button @click="upload" type="primary">upload</button>
	</view>
</template>

<script setup>
	import {
		reactive
	} from 'vue';

	const files = reactive({
		value: '',
		fileList: []
	});
	const select = (file) => {
		files.value = file;
		// add file to fileList
		files.fileList.push(file);
	}

	function upload() {
		const fileList = files.fileList;
		// upload fileList
		// for every file in fileList
		fileList.forEach((file) => {
			// upload file
			uni.uploadFile({
				url: 'http://192.168.101.7:5000/file/upload',
				name: 'file',
				filePath: file.tempFilePaths[0],
				success: () => {
					console.log('sucess');
				}
			});
		});
	}
</script>

<style>
	.file-picker {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 150rpx;
		border: 1rpx solid #ccc;
		border-radius: 10rpx;
		margin: 20rpx;
	}
</style>
```

* 需要手动实现`select`函数
* 需要使用`tempFilePaths`,文件上传的时候信息才是完整的