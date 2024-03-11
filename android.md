# 主界面

需要在`AndroidManifest`中注册

在`<intent-filter>`中添加需要的内容



* 界面和逻辑分离



在`res`中

* `drawable`放图片
* `map`放图标
* `values`放文字
* `layout`放布局

* `mipmap`是应用图标



# log

使用`Log`来打印日志

* 可以使用过滤来检查对应的内容

第一个参数是tag,第二个参数是msg



# 界面

界面样式

`wrap_content`包含全部子内容

`match_parent`沾满父组件的内容



## 创建界面

1. 创建XML界面文件
2. 创建JAVA代码文件
3. 在注册文件中配置使用

* 可以注解使用AS的功能创建一个新的**activity**



> 在`layout`中创建文件使用`_`分割,开头是`activity`



> 在配置文件的`application`中配置`activity`



## 使用`values`文件夹

存放文字/样式的文件夹

在`strings.xml`文件中配置了可能用到的字符串的内容, 使用`name`属性值来访问



使用`string`的时候, 使用`@string/xxxx`导入



## 跳转界面

使用`Intent`实现



# 文件

`manifests`存放注册配置文件

`layout`放配置文件



## 清单文件

`package`配置包的信息

文字信息保存在`values`的`strings.xml`配置文件中

`label`是APP的名字

`theme`是APP的显示的风格



# activity

是应用组件, 提供一个屏幕, 完成交互的功能



使用`XML`编写界面, 使用`JAVA`来编写逻辑功能



## 渲染使用

```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        TextView tv = findViewById(R.id.tv_title);
        tv.setText("Hello World! xuhe");
        
    }
```

`R`代表`res`文件夾下的资源

`layout`代表文件夹的名字

`activity_main`代表XML文件的名字

使用`findViewById`实现获取组件对象



# 组件



## 添加事件

使用组件的`setOnClickListener`方法实现

传入一个`View.OnClickListener`对象实例

对象实例被构建的时候需要使用重写一个`onClick`函数实现



## 设置文本

使用`android:text`或者`setText`设置文本内容

