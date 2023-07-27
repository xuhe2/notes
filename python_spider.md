# `headers`

> 使用`about://version`查看

```python
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 Edg/114.0.1823.43
```



# URL

> 使用你要访问的界面的URL



```python
url = "https://nba.hupu.com/stats/players"  # 爬取的网址
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 Edg/114.0.1823.43"
}
```



# requests

> 使用`requests`接受返回东西

* 可以使用`text`查看



# xpath_helper

* 使用`alt+shift+x`来快捷启动

* 按住`shift`同时移动鼠标,检查要看的内容



* `tr`代表行,`td`代表列



# `lxml`

```python
import lxml.etree as et # 找到xpath
```



* 使用`text()`获取文本内容

```python

names = e.xpath(
    "/html[@class='expanded']/body/div[@id='data_js']/div[@class='table_data']/div[@class='tables']/table[@class='players_table']/tbody/tr/td[@class='left']/a/text()")
# 球员姓名

teams = e.xpath(
    "/html[@class='expanded']/body/div[@id='data_js']/div[@class='table_data']/div[@class='tables']/table[@class='players_table']/tbody/tr/td/a/text()    ")
# 球员所属球队

scores = e.xpath(
    "/html[@class='expanded']/body/div[@id='data_js']/div[@class='table_data']/div[@class='tables']/table[@class='players_table']/tbody/tr/td/text()")
# 球员得分
```



# code

```python
import requests as rq
import lxml.etree as et

url = "https://nba.hupu.com/stats/players"  # 爬取的网址
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 Edg/114.0.1823.43"
}

mydata = rq.get(url, headers=headers)  # 发送请求
e = et.HTML(mydata.text)  # 解析网页

names = e.xpath(
    "/html[@class='expanded']/body/div[@id='data_js']/div[@class='table_data']/div[@class='tables']/table[@class='players_table']/tbody/tr/td[@class='left']/a/text()")
# 球员姓名

teams = e.xpath(
    "/html[@class='expanded']/body/div[@id='data_js']/div[@class='table_data']/div[@class='tables']/table[@class='players_table']/tbody/tr/td/a/text()    ")
# 球员所属球队

scores = e.xpath(
    "/html[@class='expanded']/body/div[@id='data_js']/div[@class='table_data']/div[@class='tables']/table[@class='players_table']/tbody/tr/td/text()")
# 球员得分

with open("text.txt", "w",encoding="utf-8") as f:
    for n, t, s in zip(names, teams, scores):
        f.write(f"name: {n},\t\t team: {t},\t score: {s} \n")

```



# `status_code`

* 当返回的状态码是200的时候,可以访问

```python
print(mydata.status_code)
```



# `encoding`

* 可以使用`encoding`来检测编码的格式

```python
print(mydata.encoding)
```



# `UrlManager`

```python
class UrlManager:
    """
    url管理器
    """

    def __init__(self):
        """
        初始化新旧url集合
        """
        self._NewUrl = set()
        self._OldUrl = set()

    def has_new_url(self):
        """
        判断是否有新的url
        """
        return len(self._NewUrl) != 0

    def add_new_url(self, url):
        """
        获取新的url
        :param url:
        :return: None or url
        """
        if url == None or len(url) == 0:  # 如果url为空或者长度为0，返回None
            return None
        if url in self._NewUrl or url in self._OldUrl:  # 如果url在新旧url集合中，返回None
            return None
        self._NewUrl.add(url)  # 如果url不在新旧url集合中，将url添加到新url集合中
        return url

    def add_new_urls(self, urls):
        """
        将新的url添加到新url集合中
        :param urls:
        :return:
        """
        if urls == None or len(urls) == 0:
            return None
        for url in urls:
            self.add_new_url(url)  # 将urls中的url添加到新url集合中

    def get_url(self):
        """
        获取新的url
        :return: url or None
        """
        if self.has_new_url():
            url = self._NewUrl.pop()
            self._OldUrl.add(url)
            return url  # 如果有新的url，返回url
        else:
            return None  # 如果没有新的url，返回None


if __name__ == '__main__':
    test = UrlManager()
    test.add_new_url('http://www.baidu.com')
    test.add_new_url('http://www.zhihu.com')

    print(test.get_url())
    print(test.get_url())

    print(test.has_new_url())
```

* 添加了获取`未处理的URL集合的方式(get_unprocessed_url_set)`

```python
class UrlManager:
    """
    url管理器
    """

    def __init__(self):
        """
        初始化新旧url集合
        """
        self._NewUrl = set()
        self._OldUrl = set()

    def has_new_url(self):
        """
        判断是否有新的url
        """
        return len(self._NewUrl) != 0

    def add_new_url(self, url):
        """
        获取新的url
        :param url:
        :return: None or url
        """
        if url == None or len(url) == 0:  # 如果url为空或者长度为0，返回None
            return None
        if url in self._NewUrl or url in self._OldUrl:  # 如果url在新旧url集合中，返回None
            return None
        self._NewUrl.add(url)  # 如果url不在新旧url集合中，将url添加到新url集合中
        return url

    def add_new_urls(self, urls):
        """
        将新的url添加到新url集合中
        :param urls:
        :return:
        """
        if urls == None or len(urls) == 0:
            return None
        for url in urls:
            self.add_new_url(url)  # 将urls中的url添加到新url集合中

    def get_new_url(self):
        """
        获取新的url
        :return: url or None
        """
        if self.has_new_url():
            url = self._NewUrl.pop()
            self._OldUrl.add(url)
            return url  # 如果有新的url，返回url
        else:
            return None  # 如果没有新的url，返回None

    def get_unprocessed_url_set(self):
        """
        获取未处理的url集合
        :return: url集合
        """
        return self._NewUrl

if __name__ == '__main__':
    test = UrlManager()
    test.add_new_url('http://www.baidu.com')
    test.add_new_url('http://www.baidu.com')
    test.add_new_url('http://www.zhihu.com')
    test.get_new_url()
    s = test.get_unprocessed_url_set()

    print(s)
```

* 添加了初始化的初始化`未处理URL的集合`和`已处理的URL集合`的函数

```python
class UrlManager:
    """
    url管理器
    """

    def __init__(self, processed_url_set=set(), unprocessed_url_set=set()):
        """
        初始化url管理器
        :param process_url_set: 已经处理过了的url集合
        """
        self._NewUrl = unprocessed_url_set  # 新url集合
        self._OldUrl = processed_url_set  # 旧url集合

    def has_new_url(self):
        """
        判断是否有新的url
        """
        return len(self._NewUrl) != 0

    def add_new_url(self, url):
        """
        获取新的url
        :param url:
        :return: None or url
        """
        if url == None or len(url) == 0:  # 如果url为空或者长度为0，返回None
            return None
        if url in self._NewUrl or url in self._OldUrl:  # 如果url在新旧url集合中，返回None
            return None
        self._NewUrl.add(url)  # 如果url不在新旧url集合中，将url添加到新url集合中
        return url

    def add_new_urls(self, urls):
        """
        将新的url添加到新url集合中
        :param urls:
        :return:
        """
        if urls == None or len(urls) == 0:
            return None
        for url in urls:
            self.add_new_url(url)  # 将urls中的url添加到新url集合中

    def get_new_url(self):
        """
        获取新的url
        :return: url or None
        """
        if self.has_new_url():
            url = self._NewUrl.pop()
            self._OldUrl.add(url)
            return url  # 如果有新的url，返回url
        else:
            return None  # 如果没有新的url，返回None

    def get_unprocessed_url_set(self):
        """
        获取未处理的url集合
        :return: url集合
        """
        return self._NewUrl


if __name__ == '__main__':
    pre = set()
    pre.add('http://www.baidu.com')
    unprocessed_url_set = set()
    unprocessed_url_set.add('http://www.roxylib.com')
    test = UrlManager(processed_url_set=pre, unprocessed_url_set=unprocessed_url_set)
    test.add_new_url('http://www.baidu.com')
    # st.add_new_url('http://www.roxylib.com')

    print(test.get_unprocessed_url_set())
```





# HTML



## tag

> `<XXX>`是开始一个东西,`<\XXX>`是结束一个东西



HTML（Hypertext Markup Language）是一种用于创建网页结构和内容的标记语言。HTML 使用标签（Tags）来定义网页中的元素，每个标签由尖括号包围，例如 `<tag>`。下面是一些常见的 HTML 标签及其功能的简要介绍：

1. `<html>`：定义 HTML 文档的根元素。
2. `<head>`：定义文档的头部，通常包含元数据（如标题、样式表、脚本等）。
3. `<title>`：定义文档的标题，显示在浏览器的标题栏或选项卡上。
4. `<body>`：定义文档的主体部分，包含网页的可见内容。
5. `<h1>` to `<h6>`：定义标题，按重要性递减，`h1` 为最高级标题。
6. `<p>`：定义段落。
7. `<a>`：定义超链接，用于跳转到其他页面或位置。
8. `<img>`：定义图像。
9. `<ul>` 和 `<li>`：定义无序列表和列表项。
10. `<ol>` 和 `<li>`：定义有序列表和列表项。
11. `<table>`、`<tr>`、`<td>`：定义表格、表格行和表格单元格。
12. `<div>`：定义文档中的分区或容器。
13. `<span>`：定义文档中的行内元素容器。
14. `<form>`：定义用户输入表单。
15. `<input>`：定义输入字段，如文本框、复选框、单选按钮等。
16. `<textarea>`：定义多行文本输入框。
17. `<button>`：定义按钮。
18. `<script>`：定义 JavaScript 代码。
19. `<style>`：定义内部样式表。
20. `<link>`：定义外部样式表或其他外部资源的引用。



## tag attributes

在 HTML 中，节点属性（Node Attributes）用于给 HTML 元素提供额外的信息或配置。属性以键值对的形式存在，通过在标签中使用属性名和属性值来定义。下面是一些常见的节点属性及其功能的简要介绍：

1. `href`（Hypertext Reference）：用于指定链接的目标 URL，通常在 `<a>` 标签中使用。它定义了链接的跳转地址或资源路径。

2. `src`（Source）：用于指定要加载的资源的 URL，通常在 `<img>`、`<script>`、`<audio>`、`<video>` 等标签中使用。它定义了要显示的图像、要执行的脚本或要播放的音视频文件的路径。

3. `id`（Identifier）：用于给元素指定唯一的标识符，以便通过 JavaScript 或 CSS 选择器进行引用和操作。

4. `class`：用于为元素指定一个或多个类名，以便通过 CSS 样式表或 JavaScript 进行样式设置或操作。一个元素可以有多个类名，类名之间用空格分隔。

5. `style`：用于为元素指定内联样式，即直接在元素标签中定义 CSS 样式规则。样式规则以键值对的形式出现，多个规则之间用分号分隔。

6. `title`：用于为元素提供额外的描述性信息，通常作为工具提示（Tooltip）显示。鼠标悬停在带有 `title` 属性的元素上时，将显示相关文本。

7. `alt`（Alternative Text）：用于为图像提供替代文本，当图像无法显示时或屏幕阅读器无法读取图像时，将显示该文本。

这些属性只是 HTML 中一小部分常见的节点属性，每个属性都有其特定的用途和作用范围。通过合理使用节点属性，可以为元素提供更多的功能和交互性。



# code

* 当我们使用条件的时候,因为`class`和关键字冲突,我们需要使用`class_`

```python
MyH2 = MySoup.find_all("h2", class_="entry-title")
```



* all code

```python
MyUrl = "https://www.roxylib.com"

import requests as req
from bs4 import BeautifulSoup as bs

MyData = req.get(MyUrl)
if MyData.status_code == 200:  # 200 means success
    print("Success!")
    print("this website encoding is ", MyData.encoding)
else:  # 404 means not found
    print("Error!")
    raise SystemExit

MySoup = bs(MyData.text, "html.parser")

MyH2 = MySoup.find_all("h2", class_="entry-title")
MyTitle = set()
MyRef = set()
for x in MyH2:
    MyTitle.add(x.find("a").get_text())
    MyRef.add(x.find("a").get("href"))

# for index, title, ref in zip(range(len(MyTitle)), MyTitle, MyRef):
#     print(index + 1, "\t", title, "\t", ref)

MyFile =open("text.txt","w")
for index, title, ref in zip(range(len(MyTitle)), MyTitle, MyRef):
    MyFile.write(str(index + 1) + "\t" + title + "\t" + ref + "\n")
```



# 正则表达式

在正则表达式中，如果直接给出字符，就是精确匹配。用`\d`可以匹配一个数字，`\w`可以匹配一个字母或数字，所以：

- `\d`：digit，数字字符。
- `\D`：non-digit，非数字字符。
- `\w`：word，单词字符（字母、数字、下划线）。
- `\W`：non-word，非单词字符。
- `\s`：whitespace，空白字符（空格、制表符、换行符等）。
- `\S`：non-whitespace，非空白字符。
- `\b`：word boundary，单词边界。
- `\B`：non-word boundary，非单词边界。

`.`可以匹配任意字符，所以：

- `'py.'`可以匹配`'pyc'`、`'pyo'`、`'py!'`等等。

要匹配变长的字符，在正则表达式中，用`*`表示任意个字符（包括0个），用`+`表示至少一个字符，用`?`表示0个或1个字符，用`{n}`表示n个字符，用`{n,m}`表示n-m个字符：

来看一个复杂的例子：`\d{3}\s+\d{3,8}`。

我们来从左到右解读一下：

1. `\d{3}`表示匹配3个数字，例如`'010'`；
2. `\s`可以匹配一个空格（也包括Tab等空白符），所以`\s+`表示至少有一个空格，例如匹配`' '`，`' '`等；
3. `\d{3,8}`表示3-8个数字，例如`'1234567'`。

> 如果要匹配`'010-12345'`这样的号码呢？由于`'-'`是特殊字符，在正则表达式中，要用`'\'`转义，所以，上面的正则是`\d{3}\-\d{3,8}`。



- `[0-9a-zA-Z\_]`可以匹配一个数字、字母或者下划线；
- `[0-9a-zA-Z\_]+`可以匹配至少由一个数字、字母或者下划线组成的字符串，比如`'a100'`，`'0_Z'`，`'Py3000'`等等；
- `[a-zA-Z\_][0-9a-zA-Z\_]*`可以匹配由字母或下划线开头，后接任意个由一个数字、字母或者下划线组成的字符串，也就是Python合法的变量；
- `[a-zA-Z\_][0-9a-zA-Z\_]{0, 19}`更精确地限制了变量的长度是1-20个字符（前面1个字符+后面最多19个字符）。

`A|B`可以匹配A或B，所以`(P|p)ython`可以匹配`'Python'`或者`'python'`。

`^`表示行的开头，`^\d`表示必须以数字开头。

`$`表示行的结束，`\d$`表示必须以数字结束。



## `re(Regular Expression)`

```python
s = 'ABC\\-001' # Python的字符串
# 对应的正则表达式字符串变成：
# 'ABC\-001'
```

```python
s = r'ABC\-001' # Python的字符串
# 对应的正则表达式字符串不变：
# 'ABC\-001'
```

* 而在字符串前添加 `r` 前缀，可以创建一个原始字符串（raw string），即不对字符串中的转义字符进行转义处理。

### 切分字符串

用正则表达式切分字符串比用固定的字符更灵活，请看正常的切分代码：

```
>>> 'a b   c'.split(' ')
['a', 'b', '', '', 'c']
```

嗯，无法识别连续的空格，用正则表达式试试：

```
>>> re.split(r'\s+', 'a b   c')
['a', 'b', 'c']
```

无论多少个空格都可以正常分割。加入`,`试试：

```
>>> re.split(r'[\s\,]+', 'a,b, c  d')
['a', 'b', 'c', 'd']
```

再加入`;`试试：

```
>>> re.split(r'[\s\,\;]+', 'a,b;; c  d')
['a', 'b', 'c', 'd']
```



# 从一个网页扩展出去爬取

```python
from UrlManagerClass.UrlManager import UrlManager
import requests as req
from bs4 import BeautifulSoup as bs
import re


class CrawNewPage(object):
    """
    This class is used to craw a new page
    """

    def __init__(self, RootUrl, FileName, Pattern):  # RootUrl is the url of the root page
        """
        :param RootUrl: the url of the root page
        :param RootUrl: the url of the root page
        :param FileName: the name of the file that you want to save the data
        :param Pattern: the pattern of the url that you want to craw
        """
        if RootUrl is None or len(RootUrl) == 0:  # if url is empty
            print("Url is wrong")
            return
        self._Urls = UrlManager()
        self._Urls.add_new_url(RootUrl)
        self._Pattern = Pattern

        if FileName is None or len(FileName) == 0:  # if file name is empty
            print("File name is wrong")
            return
        self._File = open(FileName, "w", encoding="utf-8")

    def __del__(self):  # when the object is deleted
        """
        close the file
        :return:
        """
        self._File.close()

    def _get_new_url(self, MyUrl, MySoup):
        """
        get the new url
        :param MyUrl: the url of the page
        :param MySoup: the soup of the page
        :return: None
        """
        if MyUrl is None or len(MyUrl) == 0:  # if url is empty
            return
        if MySoup is None:  # if soup is empty
            return

        links = MySoup.find_all("a", href=True)  # find all the links
        for link in links:
            MyRef = link["href"]
            if re.match(self._Pattern, MyRef):  # if the url matches the pattern
                self._Urls.add_new_url(MyRef)

    def func(self):
        while self._Urls.has_new_url():  # if there is a new url
            MyUrl = self._Urls.get_url()  # get the url
            MyData = req.get(MyUrl, timeout=5)

            if MyData.status_code != 200:  # 200 means success
                print("Error!")  # 404 means not found
                continue

            MySoup = bs(MyData.text, "html.parser")
            if MySoup is None:  # if soup is empty
                print("Soup is empty")
                continue

            MyTitle = MySoup.title.getText()
            if MyTitle is None or len(MyTitle) == 0: # if title is empty
                print("Title is empty")
                continue
            # write the title and url to the file
            self._File.write(MyTitle + "\t" + MyUrl + "\n")
            # get new url
            self._get_new_url(MyUrl, MySoup)


if __name__ == '__main__':
    test = CrawNewPage("https://www.roxylib.com/", "text.txt", r"https://www.roxylib.com/.*")
    test.func()

# RootUrl = "https://www.roxylib.com"
# MyUrlManager = UrlManager()
# MyUrlManager.add_new_url(RootUrl)
# MyFile = open("text.txt", "w")
#
# while MyUrlManager.has_new_url():  # if there is a new url
#     MyUrl = MyUrlManager.get_url()
#     MyData = req.get(MyUrl, timeout=3)
#
#     if MyData.status_code != 200:  # 200 means success
#         print("Error!")  # 404 means not found
#         continue
#
#     MySoup = bs(MyData.text, "html.parser")
#     MyTitle = MySoup.title.getText()
#     print(MyTitle)
```



# 爬取天气信息

```python
MyUrl = "http://www.weather.com.cn/weather/101210101.shtml"

import requests as req
from bs4 import BeautifulSoup as bs
from queue import Queue as queue
import os
from pynput import keyboard
import tkinter as tk
from tkinter import messagebox


def get_weather():
    MyData = req.get(MyUrl)
    MyData.encoding = "utf-8"  # set encoding to utf-8 (default is ISO-8859-1
    if MyData.status_code == 200:  # 200 means success
        pass
    else:  # 404 means not found
        print("Error!")
        raise SystemExit

    MySoup = bs(MyData.text, "html.parser")

    # NowTime = MySoup.find("div", class_="con today clearfix") \
    #     .find("div", class_="left fl") \
    #     .find("div", class_="left-div") \
    #     .find("div", class_="ctop clearfix") \
    #     .find("div", class_="time fr").getText()
    # print(NowTime)

    # get the weather
    MyLis = MySoup.find("div", class_="con today clearfix") \
        .find("div", class_="left fl") \
        .find("div", class_="left-div") \
        .find("div", id="7d") \
        .find("ul", class_="t clearfix") \
        .find_all("li")  # MyLis is a bs4.element.ResultSet

    MyDates = queue()  # this is my date
    MyWeathers = queue()  # this is my weather
    MyTemps = queue()  # this is my temperature

    for MyLi in MyLis:
        MyDates.put(MyLi.find("h1").get_text())
        MyWeathers.put(MyLi.find("p").get_text())
        MyTemps.put(MyLi.find("p", class_="tem").get_text())

    MyFile = open("text.txt", "w", encoding="utf-8")

    for i in range(MyDates.qsize()):
        Date = MyDates.get()
        Weather = MyWeathers.get()
        Tem = MyTemps.get()
        # print(Date, Weather, Tem)  # print the resultw
        MyFile.write(Date + " " + Weather + " " + Tem + "\n")  # write the result to file

    MyFile.flush()  # flush the file
    MyFile.close()  # close the file


# show a information box
def show_infor_message_box(infor):
    # 创建主窗口
    root = tk.Tk()
    # 隐藏主窗口
    root.withdraw()
    # 弹出消息框
    messagebox.showinfo("information message box", infor)
    # 关闭主窗口
    root.destroy()


# check my keyboard input
AltPressed = False


def on_press(key):
    """
    when the ctrl is pressed, this function will be called
    :param key:
    :return:
    """
    global AltPressed
    if key == keyboard.Key.alt_l:
        AltPressed = True
    elif key == keyboard.Key.ctrl_l and AltPressed:
        print("Alt + Ctrl pressed")
        # show_infor_message_box("Alt + Ctrl pressed")
        get_weather()  # get the weather
        os.startfile(r"C:\pycharm\PyProject\py_learn\text.txt")  # open the file
        AltPressed = False  # reset the AltPressed
    else:
        AltPressed = False


def on_release(key):
    """
    when the ctrl is released, this function will be called
    :param key:
    :return:
    """
    if key == keyboard.Key.esc:
        print("esc pressed")
        MyListener.stop()  # stop the listener


MyListener = keyboard.Listener(on_press=on_press, on_release=on_release)  # create a listener

MyListener.start()
MyListener.join()
```



# 使用代理

```python
import time

import requests as req
from bs4 import BeautifulSoup as bs
import re

proxies = {
    "http": "http://47.90.126.138:9090"
}

url = "https://www.baidu.com"

response = req.get(url, proxies=proxies)

print(response.status_code)
```

* 爬取代理IP

```python
import time

import requests as req
from bs4 import BeautifulSoup as bs
import csv


# 获取界面内容
def get_html(url, headers=None, proxies=None, timeout=3):
    """
    获取界面内容
    :param url:
    :param headers:
    :param proxies:
    :param timeout:
    :return:
    """
    try:
        response = req.get(url, headers=headers, proxies=proxies, timeout=timeout)
        if response.status_code == 200:
            return response  # 返回response对象
        else:
            print("状态码异常", response.status_code)
            return None
    except Exception as e:  # 网络连接异常
        print(e)
        return None


# 解析界面内容,获取代理ip
def get_ip(html):
    """
    解析界面，获取代理ip
    :param html:
    :return:
    """
    soup = bs(html.text, 'html.parser')
    ips = soup.find_all('td', attrs={'data-title': 'IP'})
    ports = soup.find_all('td', attrs={'data-title': 'PORT'})
    results = set()
    for i in range(len(ips)):
        ip = ips[i].text
        port = ports[i].text
        results.add("http://" + ip + ":" + port)
    return results


if __name__ == '__main__':
    proxies = {
        'http': 'http://60.182.35.230:8888'
    }

    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 Edg/114.0.1823.43"
    }
    # 打开CSV文件
    MyFile = open("ip.csv", "w", newline="")  # 打开文件
    # 获取开始时候的下标
    index = 1
    # 打开文件获取index
    with open('index.txt', 'r') as f:
        index = int(f.read())  # 读取文件

    for i in range(index, 500):
        url = f"https://www.kuaidaili.com/free/intr/{i}/"
        html = get_html(url, headers=headers, proxies=proxies)  # 获取界面内容
        results = get_ip(html)  # 获取代理ip
        for result in results:  # 遍历集合
            MyWriter = csv.writer(MyFile)  # 创建写入对象
            MyWriter.writerow([result])  # 写入数据

        MyFile.flush()  # 刷新缓冲区
        with open('index.txt', 'w') as f:  # 写入当前结束的下标
            f.write(str(i))
        print(f"第{i}页爬取完成")  # 打印爬取完成

        time.sleep(5)

    MyFile.close()

    # url = "https://www.kuaidaili.com/free/intr/1/"
    # html = get_html(url, headers=headers, proxies=proxies)
    # results = get_ip(html)
    #
    # with open("text.txt", "w") as f:
    #     for result in results:
    #         f.write(result + "\n")
```

* 拿出IP

```python
f = open("ip.csv", "r")
ip_list = f.readlines()
for x in ip_list:
    ip = x.strip()
    print(ip)
```





# 打包代码

* 使用`pyinstaller`模块

```python
Pyinstaller -F XXX.py
```



# 从一个网页扩展出去的爬取方式，CODE

```python
import requests as req
from bs4 import BeautifulSoup as bs
import csv
import re
# 自己的模組
from IPManager.IPManager import IPManager
from UrlManagerClass.UrlManager import UrlManager

# 初始化IP管理器
ip_manager = IPManager('ip.csv')

# 初始化正则表达式
pattern = re.compile(r'//www.pcauto.com.cn/.*?')

# 初始化追加写入文件
file = open("./data1/url.txt", "a", encoding='utf-8')
error_file = open("./data1/error_url.txt", "a", encoding='utf-8')

# 初始化url管理器
url_manager = UrlManager()


def get_while_url(url):
    """
    如果網址缺少https，則補上
    :param url:
    :return:
    """
    if not re.match('https.*', url):  # 如果網址缺少https
        url = 'https:' + url

    return url


def is_passage_url(url):
    """
    判断是否是文章链接
    :param url: 链接
    :return: 是文章链接返回True，否则返回False
    """
    # 判断是否是文章链接
    return re.match(r'https://www.pcauto.com.cn/.*\d+.html.*', url) and url.find('video') == -1 and url.find(
        'img') == -1 and url.find('index') == -1


def get_html(url):
    """
    取得網頁原始碼
    :param url: 網址
    :return: 回傳網頁原始碼
    """
    url = get_while_url(url)  # 如果網址缺少https，則補上
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 Edg/114.0.1823.43"
    }
    proxies = {
        'http': ip_manager.get_random_ip()  # 隨機取得一個IP
    }

    # html = req.get(url, headers=headers)  # 使用代理

    try:
        # 执行可能引发异常的代码
        html = req.get(url, headers=headers)
        # 处理响应数据
    except Exception as e:
        # 捕获任意异常
        print("Error occurred:", e)
        return None  # 返回None或进行其他处理

    if html.status_code == 200:  # 如果狀態碼是200
        html.encoding = 'utf-8'  # 設定編碼
        return html
    else:  # 如果狀態碼不是200
        return None  # 回傳None


def get_url(html):
    """
    取得網頁中的所有連結
    :param html: 網頁原始碼
    :return: 回傳網頁中的所有連結
    """
    soup = bs(html.text, 'html.parser')  # 使用BeautifulSoup解析網頁原始碼
    urls = soup.find_all('a')  # 找出所有的<a>標籤
    url_list = []
    for url in urls:  # 將所有的連結加入url_list
        new_url = url.get('href')
        if new_url is not None and pattern.match(new_url):  # 如果連結不是None且符合正則表達式
            url_list.append(new_url)
    return url_list


def get_tag(url):
    if url.find(r'/nation') != -1:
        return '新车'
    if url.find(r'/teach') != -1:
        return '导购'
    if url.find(r'/tech') != -1:
        return '技术'
    if url.find(r'/pingce') != -1:
        return '评测'
    if url.find(r'/qcbj') != -1:
        return '汽车报价'
    if url.find(r'/drivers') != -1:
        return '用车知识'
    if url.find(r'/taglist') != -1:
        return '车险'
    if url.find(r'/news') != -1:
        return '新闻'
    if url.find(r'/wenhua') != -1:
        return '文化'
    if url.find(r'/tuning') != -1:
        return '改装'
    if url.find(r'/motosport') != -1:
        return '赛事'
    if url.find(r'/wd') != -1:
        return '问答'
    if url.find(r'/article') != -1:
        return '文章'
    return 'None'


def write_url(url, title):
    """
    將連結寫入檔案
    :param url: 連結
    :return: None
    """
    url = url.strip()  # 去除空白
    file.write(url + '\t' + title + '\n')


def write_error_url(url, title):
    """
    將錯誤的連結寫入檔案
    :param url: 連結
    :return: None
    """
    url = url.strip()  # 去除空白
    error_file.write(url + '\t' + title + '\n')


def write_html(url, html):
    """
    將html寫入檔案
    :param html: html
    :return: None
    """
    file_name = url.split('/')  # 將網址以/分割
    file_name = '_'.join(file_name)  # 將網址以_連接
    # 去掉网址中的https:和.html
    file_name = file_name.replace('https:', '').replace('.html', '')
    # 移除文件名中的无效字符，只保留字母、数字、下划线、连字符和点
    file_name = re.sub(r'[^\w.-]', '', file_name)
    file_name = file_name.strip('_')  # 去掉網址前後的_

    with open('./data1/html/' + file_name + '.html', 'w', encoding='utf-8') as f:  # 將html寫入檔案
        f.write(html.text)


def craw_new_page(begin_url):
    url_manager.add_new_url(begin_url)  # 添加新的url
    idx = 1  # 計數器
    while url_manager.has_new_url():  # 如果有新的url
        new_url = url_manager.get_new_url()  # 取得新的url
        new_url = get_while_url(new_url)  # 如果網址缺少https，則補上
        title = get_tag(new_url)

        html = get_html(new_url)  # 取得網頁原始碼
        if not hasattr(html, 'status_code') or html.status_code != 200:  # 如果狀態碼不是200
            for i in range(3):  # 嘗試3次
                html = get_html(new_url)  # 取得網頁原始碼
                if hasattr(html, 'status_code') and html.status_code == 200:  # 如果狀態碼是200
                    break
            # 尝试三次之后，如果还是失败，就跳过这个url
            if not hasattr(html, 'status_code') or html.status_code != 200:  # 如果狀態碼不是200
                write_error_url(new_url, title)  # 將錯誤的連結寫入檔案
                print("爬取失敗：" + new_url)
                continue

        url_list = get_url(html)  # 取得網頁中的所有連結
        url_manager.add_new_urls(url_list)  # 添加新的url

        if is_passage_url(new_url):
            print('正在爬取第' + str(idx) + '個連結：' + new_url)
            idx += 1
            write_url(new_url, title)  # 將連結寫入檔案
            write_html(new_url, html)  # 將html寫入檔案


if __name__ == '__main__':
    url = "https://www.pcauto.com.cn/nation/3823/38231536.html"
    craw_new_page(url)
    with open('finished.txt', 'w', encoding='utf-8') as f:
        f.write('finished')
    #
    # url1 = "//www.baidu.com"
    # url2 = "https://www.baidu.com"
    # print(get_html(url1).status_code)
    # print(get_html(url2).status_code)
```

* 修改之后,还没有实际的运行测试的代码

```python
import requests as req
from bs4 import BeautifulSoup as bs
import csv
import re
# 自己的模組
from IPManager.IPManager import IPManager
from UrlManagerClass.UrlManager import UrlManager

# 初始化IP管理器
ip_manager = IPManager('ip.csv')

# 初始化正则表达式
pattern = re.compile(r'//www.pcauto.com.cn/.*?')

# 初始化追加写入文件
file = open("./data1/url.txt", "a", encoding='utf-8')
error_file = open("./data1/error_url.txt", "a", encoding='utf-8')

# 初始化url管理器
url_manager = UrlManager()

# 初始化异常次数
exception_num = 0  # 异常次数


def get_while_url(url):
    """
    如果網址缺少https，則補上
    :param url:
    :return:
    """
    if not re.match('https.*', url):  # 如果網址缺少https
        url = 'https:' + url

    return url


def is_passage_url(url):
    """
    判断是否是文章链接
    :param url: 链接
    :return: 是文章链接返回True，否则返回False
    """
    # 判断是否是文章链接
    return re.match(r'https://www.pcauto.com.cn/.*\d+.html.*', url) and url.find('video') == -1 and url.find(
        'img') == -1 and url.find('index') == -1


def get_html(url):
    """
    取得網頁原始碼
    :param url: 網址
    :return: 回傳網頁原始碼
    """
    url = get_while_url(url)  # 如果網址缺少https，則補上
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 Edg/114.0.1823.43"
    }
    proxies = {
        'http': ip_manager.get_random_ip()  # 隨機取得一個IP
    }

    # html = req.get(url, headers=headers)  # 使用代理

    try:
        # 执行可能引发异常的代码
        html = req.get(url, headers=headers)
        # 处理响应数据
    except Exception as e:
        # 捕获任意异常
        global exception_num  # 声明全局变量
        exception_num += 1  # 异常次数加1
        print("Error occurred:", e)
        return None  # 返回None或进行其他处理

    if html.status_code == 200:  # 如果狀態碼是200
        html.encoding = 'utf-8'  # 設定編碼
        return html
    else:  # 如果狀態碼不是200
        return None  # 回傳None


def get_url(html):
    """
    取得網頁中的所有連結
    :param html: 網頁原始碼
    :return: 回傳網頁中的所有連結
    """
    soup = bs(html.text, 'html.parser')  # 使用BeautifulSoup解析網頁原始碼
    urls = soup.find_all('a')  # 找出所有的<a>標籤
    url_list = []
    for url in urls:  # 將所有的連結加入url_list
        new_url = url.get('href')
        if new_url is not None and pattern.match(new_url):  # 如果連結不是None且符合正則表達式
            url_list.append(new_url)
    return url_list


def get_title(url):
    if url.find(r'/nation') != -1:
        return '新车'
    if url.find(r'/teach') != -1:
        return '导购'
    if url.find(r'/tech') != -1:
        return '技术'
    if url.find(r'/pingce') != -1:
        return '评测'
    if url.find(r'/qcbj') != -1:
        return '汽车报价'
    if url.find(r'/drivers') != -1:
        return '用车知识'
    if url.find(r'/taglist') != -1:
        return '车险'
    if url.find(r'/news') != -1:
        return '新闻'
    if url.find(r'/wenhua') != -1:
        return '文化'
    if url.find(r'/tuning') != -1:
        return '改装'
    if url.find(r'/motosport') != -1:
        return '赛事'
    if url.find(r'/wd') != -1:
        return '问答'
    if url.find(r'/article') != -1:
        return '文章'
    return 'None'


def write_url(url, title):
    """
    將連結寫入檔案
    :param url: 連結
    :return: None
    """
    url = url.strip()  # 去除空白
    file.write(url + '\t' + title + '\n')


def write_error_url(url, title):
    """
    將錯誤的連結寫入檔案
    :param url: 連結
    :return: None
    """
    url = url.strip()  # 去除空白
    error_file.write(url + '\t' + title + '\n')


def write_html(url, html):
    """
    將html寫入檔案
    :param html: html
    :return: None
    """
    file_name = url.split('/')  # 將網址以/分割
    file_name = '_'.join(file_name)  # 將網址以_連接
    # 去掉网址中的https:和.html
    file_name = file_name.replace('https:', '').replace('.html', '')
    # 移除文件名中的无效字符，只保留字母、数字、下划线、连字符和点
    file_name = re.sub(r'[^\w.-]', '', file_name)
    file_name = file_name.strip('_')  # 去掉網址前後的_

    with open('./data1/html/' + file_name + '.html', 'w', encoding='utf-8') as f:  # 將html寫入檔案
        f.write(html.text)


def craw_new_page(begin_url):
    url_manager.add_new_url(begin_url)  # 添加新的url
    idx = 1  # 計數器
    while url_manager.has_new_url():  # 如果有新的url
        new_url = url_manager.get_new_url()  # 取得新的url
        new_url = get_while_url(new_url)  # 如果網址缺少https，則補上
        title = get_title(new_url)

        html = get_html(new_url)  # 取得網頁原始碼
        if not hasattr(html, 'status_code') or html.status_code != 200:  # 如果狀態碼不是200
            for i in range(3):  # 嘗試3次
                html = get_html(new_url)  # 取得網頁原始碼
                if hasattr(html, 'status_code') and html.status_code == 200:  # 如果狀態碼是200
                    break
            # 尝试三次之后，如果还是失败，就跳过这个url
            if not hasattr(html, 'status_code') or html.status_code != 200:  # 如果狀態碼不是200
                write_error_url(new_url, title)  # 將錯誤的連結寫入檔案
                print("爬取失敗：" + new_url)
                continue

        url_list = get_url(html)  # 取得網頁中的所有連結
        url_manager.add_new_urls(url_list)  # 添加新的url

        if is_passage_url(new_url):
            print('正在爬取第' + str(idx) + '個連結：' + new_url)
            idx += 1
            write_url(new_url, title)  # 將連結寫入檔案
            write_html(new_url, html)  # 將html寫入檔案


if __name__ == '__main__':
    url = "https://www.pcauto.com.cn/nation/3823/38231536.html"
    craw_new_page(url)

    with open('finished.txt', 'w', encoding='utf-8') as f: # 將finished寫入檔案
        f.write('finished')
    print('finished')  # 顯示爬取完成
    print('excepted: ', exception_num)  # 顯示爬取失敗的連結數量
    #
    # url1 = "//www.baidu.com"
    # url2 = "https://www.baidu.com"
    # print(get_html(url1).status_code)
    # print(get_html(url2).status_code)
```



# 解决动态加载的问题

* 通过一个原网站，在网站中，使用`chrome`中的`network`抓包`fetch/xhr`获得需要的URL,需要的URL的`?`符号后面的内容来自于`string parameter`,可以使用`query string parameters`查看

* 然后传入`param`这个参数

```python
import requests as req

from IPManager.IPManager import IPManager

ip = IPManager('ip.csv').get_random_ip()
proxies = {
    'http': ip
}

url = 'https://auto.sohu.com/qichexinwen.shtml'

params = {
    'pNo': '2'
}

html = req.get(url, params=params, proxies=proxies)
print(html.status_code)
print(html.text)
```





# selenium

Selenium是一个用于自动化浏览器操作的开源工具集。它支持多种浏览器（如Chrome、Firefox、Safari等）和多种操作系统（如Windows、macOS、Linux等），可以模拟用户在浏览器中的交互行为。

Selenium主要包含以下几个组件：

1. Selenium WebDriver: 是Selenium的核心组件，用于控制浏览器并模拟用户操作。它提供了多种编程语言的接口，如Python、Java、C#等，可以通过编写脚本来实现自动化测试、网页爬取、数据抓取等操作。
2. Selenium Grid: 是Selenium的分布式测试工具，可以在多个不同的浏览器和操作系统上并行运行测试。它可以通过将测试任务分发到不同的节点上，加快测试的执行速度。
3. Selenium IDE: 是一个浏览器插件，用于录制和回放用户在浏览器中的操作。它可以将用户的操作转化为Selenium脚本，方便测试人员快速创建测试用例。

Selenium的应用场景包括：

- 自动化测试：Selenium可以模拟用户在浏览器中的行为，用于执行自动化测试用例，检查网页功能、交互和界面的正确性。
- 网页爬取：Selenium可以帮助爬虫程序获取动态加载的网页内容，通过模拟浏览器操作来解析JavaScript生成的内容。
- 数据抓取：Selenium可以模拟用户登录、填写表单、点击按钮等操作，用于抓取需要登录或进行交互的网页数据。



> 安装在`Scripts`的文件夹下面(这个文件夹被包含在我的path中)



## 初始化一个浏览器的object

* init

```python
from selenium.webdriver import Chrome

web = Chrome()
```



## 点击对应的部分(使用`xpath`)

```python
web = Chrome()
web.get('https://www.roxylib.com/')

el = web.find_element(By.XPATH,'//*[@id="tag_cloud-3"]/nav/div/a[1]')

el.click()
```



## 使用搜索框

```python
from selenium.webdriver import Chrome
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

web = Chrome()
web.get('https://www.tasim.net/')

search = web.find_element(By.NAME, 'q')

search.send_keys('python', Keys.ENTER)
```



## 切换窗口

```python
web.switch_to.window(web.window_handles[-1])  # 切换到新打开的窗口
titles = web.find_elements(By.CLASS_NAME, 'bili-video-card__info--tit')  # 获取所有的视频信息
for x in titles:
    # 打印x中title元素内容
    print(x.text)
```



## 去掉子窗口

```python
web.close()
web.switch_to.window(web.window_handles[-1])
```



## 使用无头浏览器

```python
from selenium.webdriver.chrome.options import Options  # 从options模块中调用Options类

# 使用headless无界面浏览器模式
chrome_options = Options()  # 实例化Option对象
chrome_options.add_argument('--headless')  # 把Chrome浏览器设置为静默模式
web = Chrome(options=chrome_options)  # 设置引擎为Chrome，在后台默默运行
```





# `IPManager`

> 使用本package下的class,可以实现随机获取一个IP,使用代理

* 使用`get_proxies`函数,直接获取代理文件

```python
import requests
    html = requests.get('https://www.baidu.com', proxies=ip_manager.get_proxies()) # 使用代理
```

* code

```python
import csv
import random


class IPManager:
    """
    IP管理器
    初始化参数:CSV文件名
    """

    # 初始化,加入读取文件
    def __init__(self, filename='ip.csv'):
        """
        :param filename: CSV文件名
        """
        self._ip_list = []
        with open(filename, 'r') as f:
            reader = csv.reader(f)
            for row in reader:
                self._ip_list.append(row[0])

    # 随机获取一个IP
    def get_random_ip(self):
        """
        :return: 随机获取一个IP
        :return:
        """
        return random.choice(self._ip_list)

    def get_proxies(self):
        """
        获取适用于requests的proxies
        :return: proxies
        """
        proxies = {
            'http': self.get_random_ip()
        }
        return proxies


if __name__ == '__main__':
    ip_manager = IPManager('ip.csv')
    import requests
    html = requests.get('https://www.baidu.com', proxies=ip_manager.get_proxies()) # 使用代理
    print(html.status_code)
    print(html.text)
```





# `get_url_from_file`

* in the `url.txt` file , I use the `\t` to spilt the url and tag . 

```python
def get_url_from_file(file_path='./data1/url.txt'):
    """
    從檔案中取得網址
    :param file_path:
    :return:
    """
    url_list = []
    with open(file_path, 'r', encoding='utf-8') as f:
        for url_and_tag in f.readlines():  # 逐行讀取
            url = url_and_tag.split('\t')[0]  # 取得網址
            tag = url_and_tag.split('\t')[1].strip()  # 取得標籤
            url_list.append((url, tag))

    return url_list  # 回傳網址串列
```



# `get_file_name`

```python
def get_file_name(url):
    """
    取得檔案名稱
    :param url:
    :return:
    """
    file_name = url.split('/')  # 將網址以/分割
    file_name = '_'.join(file_name)  # 將網址以_連接
    # 去掉网址中的https:和.html
    file_name = file_name.replace('https:', '').replace('.html', '')
    # 移除文件名中的无效字符，只保留字母、数字、下划线、连字符和点
    file_name = re.sub(r'[^\w.-]', '', file_name)
    file_name = file_name.strip('_')  # 去掉網址前後的_
    file_name += '.html'  # 加上.html

    return file_name  # 回傳檔案名稱
```



# `webcrawler` package

* this package has those classes I give before , and add a `HTMLParser` to get the passage from the `html` source code .



## `CrawNewPage` class

```python
from webcrawler.UrlManager import UrlManager
import requests as req
from bs4 import BeautifulSoup as bs
import re


class CrawNewPage(object):
    """
    This class is used to craw a new page
    """

    def __init__(self, RootUrl, FileName, Pattern):  # RootUrl is the url of the root page
        """
        :param RootUrl: the url of the root page
        :param RootUrl: the url of the root page
        :param FileName: the name of the file that you want to save the data
        :param Pattern: the pattern of the url that you want to craw
        """
        if RootUrl is None or len(RootUrl) == 0:  # if url is empty
            print("Url is wrong")
            return
        self._Urls = UrlManager()
        self._Urls.add_new_url(RootUrl)
        self._Pattern = Pattern

        if FileName is None or len(FileName) == 0:  # if file name is empty
            print("File name is wrong")
            return
        self._File = open(FileName, "w", encoding="utf-8")

    def __del__(self):  # when the object is deleted
        """
        close the file
        :return:
        """
        self._File.close()

    def _get_new_url(self, MyUrl, MySoup):
        """
        get the new url
        :param MyUrl: the url of the page
        :param MySoup: the soup of the page
        :return: None
        """
        if MyUrl is None or len(MyUrl) == 0:  # if url is empty
            return
        if MySoup is None:  # if soup is empty
            return

        links = MySoup.find_all("a", href=True)  # find all the links
        for link in links:
            MyRef = link["href"]
            if re.match(self._Pattern, MyRef):  # if the url matches the pattern
                self._Urls.add_new_url(MyRef)

    def func(self):
        while self._Urls.has_new_url():  # if there is a new url
            MyUrl = self._Urls.get_url()  # get the url
            MyData = req.get(MyUrl, timeout=5)

            if MyData.status_code != 200:  # 200 means success
                print("Error!")  # 404 means not found
                continue

            MySoup = bs(MyData.text, "html.parser")
            if MySoup is None:  # if soup is empty
                print("Soup is empty")
                continue

            MyTitle = MySoup.title.getText()
            if MyTitle is None or len(MyTitle) == 0: # if title is empty
                print("Title is empty")
                continue
            # write the title and url to the file
            self._File.write(MyTitle + "\t" + MyUrl + "\n")
            # get new url
            self._get_new_url(MyUrl, MySoup)


if __name__ == '__main__':
    test = CrawNewPage("https://www.roxylib.com/", "../CrawNewPageClass/text.txt", r"https://www.roxylib.com/.*")
    test.func()

# RootUrl = "https://www.roxylib.com"
# MyUrlManager = UrlManager()
# MyUrlManager.add_new_url(RootUrl)
# MyFile = open("text.txt", "w")
#
# while MyUrlManager.has_new_url():  # if there is a new url
#     MyUrl = MyUrlManager.get_url()
#     MyData = req.get(MyUrl, timeout=3)
#
#     if MyData.status_code != 200:  # 200 means success
#         print("Error!")  # 404 means not found
#         continue
#
#     MySoup = bs(MyData.text, "html.parser")
#     MyTitle = MySoup.title.getText()
#     print(MyTitle)
```



## `HTMLParser` class

```python
# 这是我用来处理HTML文件中的passage和别的东西的class

import json

from bs4 import BeautifulSoup as bs


class HTMLParser:
    """
    HTML解析器
    """

    def __init__(self, url=None, tag=None, html=None):
        """
        初始化参数
        :param url:
        :param tag:
        :param html:
        """
        self.url = url
        self.tag = tag
        self.html = html

    def get_title(self, html):
        """
        取得文章標題
        :param html: 網頁原始碼
        :return: 回傳文章標題, 如果出現錯誤, 回傳None
        """
        try:
            if hasattr(html, 'text'):  # 如果html有text屬性
                soup = bs(html.text, 'html.parser')
            else:
                soup = bs(html, 'html.parser')
            title = soup.select_one('title').text  # 取得文章標題
            title = title.strip()  # 去掉空白
        except Exception as e:
            print('get title error: ', e)  # 如果出現錯誤，印出錯誤訊息
            title = None

        return title

    def get_content(self, html):
        """
        取得文章內容
        :param html: 網頁原始碼
        :return: 回傳文章內容, 如果出現錯誤, 回傳None
        """
        try:
            if hasattr(html, 'text'):  # 如果html有text屬性
                soup = bs(html.text, 'html.parser')
            else:
                soup = bs(html, 'html.parser')
            # 先找到div標籤，再找到class為artText clearfix的div標籤
            passages = soup.find('div', class_='artText clearfix').find_all('p')
            result = []  # 建立一個空串列
            for p in passages:
                result.append(p.text)  # 將文章內容加入串列

            # 去掉空白和无意义的字符
            result = [x.strip() for x in result if x.strip() != '']
            # 把串列中的元素用\n連接起來
            result = '\n'.join(result)
        except Exception as e:
            print('get content error: ', e)  # 如果出現錯誤，印出錯誤訊息
            result = None

        return result

    def get_data_dict(self):
        title = self.get_title(self.html)  # 取得文章標題
        content = self.get_content(self.html)  # 取得文章內容
        if title is None or content is None:
            return None  # 如果文章標題或文章內容為None，回傳None

        try:
            # 我的dict格式，包含source(url), tag, title, content
            data_dict = {
                'source': self.url,
                'tag': self.tag,
                'title': title,
                'content': content
            }  # 建立一個字典
        except Exception as e:
            print('get data dict error: ', e)
            data_dict = None

        return data_dict  # 回傳字典

    def get_data_json(self):
        """
        將資料轉換成JSON格式
        :return: 回傳JSON格式的資料
        """
        data_dict = self.get_data_dict()  # 取得字典格式的資料
        if data_dict is None:
            return None # 如果data_dict為None，回傳None

        try:
            data_json = json.dumps(data_dict, ensure_ascii=False, indent=4)  # 將字典轉換成JSON格式
        except Exception as e:
            print('get data json error: ', e)
            data_json = None

        return data_json  # 回傳JSON格式的資料

    def write_to_file(self, path):
        """
        將資料寫入檔案
        :param path: 檔案路徑
        :return: 当写入成功时，回傳True，否则回傳False
        """
        data_json = self.get_data_json()
        if data_json is None:
            return False  # 如果data_json為None，回傳None

        try:
            with open(path, 'w', encoding='utf-8') as f:
                f.write(data_json)  # 將資料寫入檔案
        except Exception as e:
            print('write to file error: ', e)
            return False

        return True  # 回傳True
```



## `IPManager` class

```python
import csv
import random


class IPManager:
    """
    IP管理器
    初始化参数:CSV文件名
    """

    # 初始化,加入读取文件
    def __init__(self, filename='ip.csv'):
        """
        :param filename: CSV文件名
        """
        self._ip_list = []
        with open(filename, 'r') as f:
            reader = csv.reader(f)
            for row in reader:
                self._ip_list.append(row[0])

    # 随机获取一个IP
    def get_random_ip(self):
        """
        :return: 随机获取一个IP
        :return:
        """
        return random.choice(self._ip_list)

    def get_proxies(self):
        """
        获取适用于requests的proxies
        :return: proxies
        """
        proxies = {
            'http': self.get_random_ip()
        }
        return proxies


if __name__ == '__main__':
    ip_manager = IPManager('../IPManager/ip.csv')
    import requests
    html = requests.get('https://www.baidu.com', proxies=ip_manager.get_proxies()) # 使用代理
    print(html.status_code)
    print(html.text)
```



## `UrlManager` class

```python
class UrlManager:
    """
    url管理器
    """

    def __init__(self, processed_url_set=set(), unprocessed_url_set=set()):
        """
        初始化url管理器
        :param process_url_set: 已经处理过了的url集合
        """
        self._NewUrl = unprocessed_url_set  # 新url集合
        self._OldUrl = processed_url_set  # 旧url集合

    def has_new_url(self):
        """
        判断是否有新的url
        """
        return len(self._NewUrl) != 0

    def add_new_url(self, url):
        """
        获取新的url
        :param url:
        :return: None or url
        """
        if url == None or len(url) == 0:  # 如果url为空或者长度为0，返回None
            return None
        if url in self._NewUrl or url in self._OldUrl:  # 如果url在新旧url集合中，返回None
            return None
        self._NewUrl.add(url)  # 如果url不在新旧url集合中，将url添加到新url集合中
        return url

    def add_new_urls(self, urls):
        """
        将新的url添加到新url集合中
        :param urls:
        :return:
        """
        if urls == None or len(urls) == 0:
            return None
        for url in urls:
            self.add_new_url(url)  # 将urls中的url添加到新url集合中

    def get_new_url(self):
        """
        获取新的url
        :return: url or None
        """
        if self.has_new_url():
            url = self._NewUrl.pop()
            self._OldUrl.add(url)
            return url  # 如果有新的url，返回url
        else:
            return None  # 如果没有新的url，返回None

    def get_unprocessed_url_set(self):
        """
        获取未处理的url集合
        :return: url集合
        """
        return self._NewUrl


if __name__ == '__main__':
    pre = set()
    pre.add('http://www.baidu.com')
    unprocessed_url_set = set()
    unprocessed_url_set.add('http://www.roxylib.com')
    test = UrlManager(processed_url_set=pre, unprocessed_url_set=unprocessed_url_set)
    test.add_new_url('http://www.baidu.com')
    # st.add_new_url('http://www.roxylib.com')

    print(test.get_unprocessed_url_set())
```



## `HTMLGetter`

```python
from webcrawler.IPManager import IPManager
import requests as req
import re
from bs4 import BeautifulSoup as bs


class HTMLGetter:
    def __init__(self, url=None):
        self.url = self.get_while_url(url)  # 如果網址缺少https，則補上

    def get_while_url(self, url):
        """
        如果網址缺少https，則補上
        :param url:
        :return:
        """
        if url is None:
            return None  # 如果網址是None，則回傳None

        if not re.match('https://.*', url):  # 如果網址缺少https
            url = 'https://' + url

        return url

    def get_main_url(self, html):
        """
        从url中找到主要的域名
        :param url:
        :return:
        """
        result = re.findall(r'https?://(.*?)/', html)
        if result:
            return result[0]
        else:
            return None

    def _get_html(self, url=None, params=None, endcoding='utf-8', use_proxy=False):
        """
        取得網頁原始碼
        :param url: 網址
        :return: 回傳網頁原始碼
        """
        if url is None:
            url = self.url  # 如果網址是None，則使用初始化的網址
        else:
            url = self.get_while_url(url)  # 如果網址缺少https，則補上

        headers = {
            "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 Edg/114.0.1823.43"
        }

        try:
            # 执行可能引发异常的代码
            if use_proxy:  # 如果使用代理
                self.ip_manager = IPManager()  # 初始化IP管理器
                html = req.get(url, headers=headers, proxies=self.ip_manager.get_proxies(), params=params)  # 取得網頁原始碼
            else:
                html = req.get(url, headers=headers, params=params)

            # 处理响应数据
        except Exception as e:
            # 捕获任意异常
            print("Error occurred:", e)
            return None  # 返回None或进行其他处理

        if html.status_code == 200:  # 如果狀態碼是200
            html.encoding = endcoding  # 設定編碼
            self.html = html  # 儲存網頁原始碼
            return html
        else:  # 如果狀態碼不是200
            return None  # 回傳None

    def get_html(self, url=None, params=None, endcoding='utf-8', use_proxy=False):
        """
        取得網頁原始碼
        :param url:
        :param params: 网页参数
        :param endcoding: 编码格式
        # :param use_proxy: 是否使用代理(True/False)
        :return: 回傳網頁原始碼
        """
        # 尝试三次
        if url is None:
            url = self.url  # 如果網址是None，則使用初始化的網址

        for i in range(3):
            html = self._get_html(url, params, endcoding, use_proxy)
            if html:
                return html
        return None

    def get_p(self, html=None):
        """
        获取网页代码中的所有的p标签
        :param html: 網頁原始碼, (requests物件,可以不傳入)
        :return: 返回所有的p标签(BeautifulSoup对象, list)
        """
        if html is None and hasattr(self, 'html'):
            html = self.html  # 如果網址是None，則使用初始化的網址

        if html is None and self.url is not None:
            html = self.get_html(url=self.url)  # 如果網址是None，則使用初始化的網址
            self.html = html  # 儲存網頁原始碼

        if html is None:
            return None  # 如果網址是None，則回傳None

        soup = bs(html.text, 'html.parser')  # 創建BeautifulSoup物件
        p_list = soup.find_all('p')  # 取得所有的p標籤
        return p_list  # 回傳所有的p標籤

    def get_passage_content(self, html=None):
        """
        取得文章內容
        :param html:
        :return:
        """
        p_list = self.get_p(html)
        if p_list is None:
            return None

        passage_content = ''  # 儲存文章內容
        for p in p_list:
            # 去除p標籤中的空白
            p_text = p.text.strip()
            # 去除\xa0
            p_text = re.sub('\xa0', '', p_text)
            # 如果存在內容
            if p_text:
                passage_content += p_text + '\n'  # 將內容加入文章內容

        return passage_content


if __name__ == '__main__':
    test = HTMLGetter('https://m.23wxx.com/xs/30316/4368683.html')
    print(test.get_passage_content())
```





# 小说阅读器



## `NovelCrawler`

```python
from webcrawler.HTMLGetter import HTMLGetter
import re
from bs4 import BeautifulSoup as bs


class NovelCrawler(HTMLGetter):
    def __init__(self, url=None):
        super().__init__(url)

    def __getattr__(self, item):
        return None  # 如果沒有該屬性，則回傳None

    def get_passage_content(self, html=None, use_filter=None, url=None):
        """
        取得文章內容
        :param html:
        :param use_filter: 对过滤进行的操作(continue/break)
        :param url:
        :return:
        """
        p_list = self.get_p(html)
        if p_list is None:
            return None

        if url is None:  # 如果網址是None，則使用初始化的網址
            url = self.url

        # 屏蔽存在主要URL的p標籤
        keyword_filter = None  # 作为关键词的过滤器
        if use_filter is not None and url is not None:
            keyword_filter = self.get_main_url(url)  # 作为关键词的过滤器

        passage_content = ''  # 儲存文章內容
        for p in p_list:
            # 去除p標籤中的空白
            p_text = p.text.strip()
            # 去除\xa0
            p_text = re.sub('\xa0', '', p_text)
            # 如果存在內容
            if p_text:
                # 如果存在主要URL
                if keyword_filter is not None and keyword_filter in p_text:  # 如果存在屏蔽的关键词
                    if use_filter == 'continue': # 如果是continue，則跳过
                        continue
                    elif use_filter == 'break': # 如果是break，則跳出
                        break

                else:
                    passage_content += p_text + '\n'

        return passage_content

    def get_passage_title(self, html=None):
        if html is None and hasattr(self, 'html'):
            html = self.html  # 如果網址是None，則使用初始化的網址

        if html is None and self.url is not None:
            html = self.get_html(url=self.url)  # 如果網址是None，則使用初始化的網址
            self.html = html  # 儲存網頁原始碼

        if html is None:
            return None  # 如果網址是None，則回傳None

        soup = bs(html.text, 'html.parser')  # 創建BeautifulSoup物件
        try:
            # 从head的title标签中获取标题
            title = soup.head.title.text

            # 去除標題中的空白
            title = title.strip()
            # 去除\xa0
            title = re.sub('\xa0', '', title)

        except:
            title = None

        return title  # 回傳標題


if __name__ == '__main__':
    test = NovelCrawler('https://m.23wxx.com/xs/30316/4368683.html')
    print(test.get_passage_content(use_filter='break'))
```



# 使用`session`解决需要登陆的情况

> 1. 通过`登陆`获取`cookie`,这个`cookie`是后续的登陆需要的信息
> 2. 使用`session`访问(不会丢失`cookie`)





