# install

```python
pip install scrapy
```



# 创建项目

* 在`power shell`中使用命令可以自动创建一个项目

```python
scrapy startproject [项目名称]
```



> 构建出来的项目
>
> >             [项目名字]
> >                 spiders # 这是文件夹
> >                     __init__.py
> >                 __init__.py
> >                 items.py
> >                 middlewares.py
> >                 pipelines.py    
> >                 settings.py
> >             scrapy.cfg
> >



# 初始化

>使用命令初始化我的要爬取的对象
>
>```python
>scrapy genspider douban_top250 movie.douban.com
>```

* 效果

```python
		# 爬虫名称
        name = 'douban_top250'
        # 允许的域名
        allowed_domains = ['movie.douban.com']
        # 入口URL
        start_urls = ['https://movie.douban.com/top250']
```



## tips

> 在`setting`的文件中设置了一次爬取间隔多少时间,以及优先级

> 修改`USER_AGENT`,防止被发现是爬虫



# 构建虚拟环境

> 在设置中找到当前项目的Python解释器
>
> 添加创建虚拟环境



# 编写`items.py`模块

> 这个模块用来实现`item`的派生类,一般从`scrapy.Item`基类中派生出来



> 在实现解析数据的时候,可以使用`scrapy.Field()`
>
> ```python
> title = scrapy.Field()
> ```
>
> 这样可以在接下来的`parse`方法中实现
>
> ```python
> Item['title'] = .....
> ```
>
> 

# `Spider`类的构建



## 域名和URL

> 注意`URL`的协议使用的是什么类型



## 写`parse`方法

> 2.在settings.py文件中开启 'USER_AGENT' 并设置为正确的代理
> 3.输出爬取的信息
> 例:
>     def parse(self, response):
>         print(response.text)
> 4.执行爬虫运行命令: scrapy crawl [爬虫名称]   例: scrapy crawl douban_top250

* 需要修改方法的实现方式

* 返回的时候使用`yield`方式



### 使用`Selector`对象

> 把`response`放入到`Selector`中去,可以在后续实现使用`CSS`或者`XPath`的方式解析内容

> 返回的数据很特殊,需要使用`extract_first()`获取第一个部分



* tips

> 获取到数据之后需要组装成`Item`
>
> 放入到自己创建的`Item`中
>
> 采用生成器的方式`yield`返回`Item`的实例
>
> > 1. **定义生成器函数：** 使用 `yield` 关键字定义生成器函数，它类似于普通函数，但不同的是在函数体中使用 `yield` 语句返回值。
> > 2. **暂停和继续：** 当生成器函数执行到 `yield` 语句时，会暂停执行并将当前值返回给调用者。下次调用生成器时，会从上次暂停的地方继续执行，直到再次遇到 `yield` 或函数结束。
> > 3. **迭代：** 生成器可以像普通的迭代器一样使用，在 `for` 循环中遍历或通过 `next()` 函数逐步获取值。
> > 4. **节省内存：** 生成器不会一次性生成所有值，而是按需生成，因此在处理大量数据时，不会占用过多的内存。



# 运行项目

* 在`power shell`中使用命令运行

```python
scrapy crawl [爬虫名称]
```

> 可以使用`-o [file_name]`方式控制输出

```python
    命令：scrapy crawl [爬虫名称] -o [保存文件名]
    例:
        1. scrapy crawl douban_top250 -o douban1.json
        2. scrapy crawl douban_top250 -o douban2.csv
```



# 获取下一页的内容

> 也是使用`Selector`来获取所有的下一页面的`link`



## 当`URL`不完整的时候

> 使用`HtmlResponse`类型中的`urljoin`方法来拼URL
>
> ```python
> url = reponse.urljoin(url)
> ```



## 把新的`Request`实例返回

> tips:
>
> 1. 返回的类型是`Request`的实例
> 2. 使用的`yield`方式返回



## 当开始的`URL`和按钮中`第一页的URL`不一样的时候

* 调度器会认为我的第一面的URL和开始的URL不一样,所以,会重复爬取第一面的内容

> 为了解决这个问题,我们可以直接不使用`start_url`,我们可以直接在开始解析之前,直接返回全部的`Request`

> 重写`start_requests`方法,使用`yield`的方式返回所有的`Request`实例



## tips

> 在重写方法的时候,注意两个方法的参数应该是一样的



# 使用管道将数据写入`excel`

* 使用的是`openpyxl`的模块

```python
pip install openpyxl
```



## `__init__`函数的实现

* 创建表

```python
self.wb = openpyxl.Workbook()
self.ws = wb.active
self.ws.title = 'XXX'
self.ws.append((XX,XX,...)) # 第一行
```



## `close_spider`方法(也有`open_spider`方法)

> 在爬虫结束的时候,运行这个函数

```python
self.wb.save("XXX") # 保存在这个地方
```



## `process_item`方法

* 这个方法用来实现数据的处理

> 从`item`中获取这个元素放入到`self.wb`中

* 每次获取数据的时候就会调用一次



### tips

> 对字典使用`get('XXX','')`,可以在不存在的时候,返回一个默认的值

> 管道也可以通过修改权值来控制先后的执行顺序
>
> 数据小的先执行



# 使用管道将数据写入`MySql`

* 使用`pymysql`模块实现

## tips

> 可以同时存在多个管道



## `__init__`

```python
self.db = pymysql.connect(host='',port=,user='',password='',database='',charset='utf8mb4')
```

> 关于`utf8mb4`
>
> 在 MySQL 中，`utf8mb4` 是一种字符编码格式，用于支持 Unicode 字符集的存储和处理。它是对标准的 UTF-8 编码的扩展，可以存储更广泛的 Unicode 字符，包括一些特殊的表情符号（如 Emoji 表情）。

```python
self.cursor = self.db.cursor()
```

> 获取光标的信息



## `process_item`

* 运行cursor

```python
self.cursor.execute('insert into XXXXXX...'.format(XXX,XX...))
```





## `close_spider`

* 关闭数据库

```python
self.db.close()
```



# 设置代理

* 可以在`Request`中添加`meta`参数实现

import scrapy

class MySpider(scrapy.Spider):
    name = 'my_spider'

```python
def start_requests(self):
    # 使用代理发送请求
    yield scrapy.Request(url='http://example.com', meta={'proxy': 'http://proxy_ip:proxy_port'})

def parse(self, response):
    # 解析网页内容
    pass
```



# 设置`cookie`

* 可以通过在`Request`中设置`cookie`来实现
* 可以通过在`middlewares`中实现



# 检查现在的库

使用`pip list`命令可以查看到现在安装的所有的第三方的名字和版本



# 获取依赖项,并且写入到文件中

* 当别人在使用代码的时候,可以使用这种方式来快捷的安装所有需要的依赖项

* 文件名字一般叫做`requirements.txt`

## 写入依赖项文件

```python
pip freeze > requirements.txt
```



## 通过依赖项文件来安装所有需要的依赖项

```python
pip install -r requirements.txt
```

