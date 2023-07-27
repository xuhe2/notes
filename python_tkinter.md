* `tkinter`中的控件的命名开头的字母是大写的



# `TK`

* 作为最高级的东西,包含其他组件

```python
import tkinter as tk

root = tk.Tk()
root.geometry("800x600")
root.title("小说阅读器")

root.mainloop() # 进入消息循环
```



# `frame`

* 一个框架作为一个界面的框架,实现界面之间的相互的转换.

```python
# 起始frame
frame_start = tk.Frame(root) # 创建Frame
frame_start.pack() # 将Frame添加到主窗口
```



## 布置`frame`内部

* 隐藏当前的frame

```python
frame_start.pack_forget()  # 隐藏frame_start
```





### 布置`label`

```python
# 布置一个label
tk.Label(frame_start, text="欢迎使用小说阅读器", font=("Arial", 20)).pack() # Label布置在Frame上
```



### 布置`button`

```python
btn.bind('<Enter>',func) # 绑定函数
```



# 设置菜单

> `tearoff`是菜单项中的一个选项，用于控制菜单的分离条（tear-off bar）的显示。
>
> 分离条是一个用于将菜单从主窗口分离出来的可拖动的工具栏。当用户点击分离条时，菜单会以独立的窗口形式显示。
>
> `tearoff`的默认值为1，表示分离条可见。如果将`tearoff`设置为0，分离条将被隐藏，菜单项将无法被拖动为独立窗口。
>
> 在你提供的代码中，`tearoff=0`表示菜单项中的分离条将被隐藏，用户将无法将菜单项拖动为独立窗口。如果将`tearoff`设置为1，则可以通过点击分离条将菜单项拖动为独立窗口。
>
> 注意：`tearoff`参数在不同操作系统的默认行为可能略有不同，具体表现取决于操作系统的窗口管理器。



```python
import tkinter as tk

root = tk.Tk()  # 创建主窗口
root.title("小说阅读器")  # 设置窗口标题
root.geometry("800x500+100+100")  # 设置窗口大小

menu = tk.Menu(root)  # 创建菜单

# 创建菜单项
filemenu = tk.Menu(menu, tearoff=0)  # 创建filemenu菜单
filemenu.add_command(label="打开", command=None)  # 添加打开菜单项
filemenu.add_command(label="保存", command=None)  # 添加保存菜单项

# 加入menu菜单
menu.add_cascade(label="文件", menu=filemenu)  # 将filemenu菜单添加到menu菜单中

root.config(menu=menu)  # 设置菜单

root.mainloop()  # 进入消息循环
```



# 制作状态栏



```python
# 设置状态栏
status_var = tk.StringVar()  # 创建状态栏变量
status_label = tk.Label(root, textvariable=status_var, bd=1, relief=tk.SUNKEN,
                        anchor=tk.W)  # 创建状态栏,设置边框bd=1,relief=tk.SUNKEN,anchor=tk.W 
```



* 修改显示的值

```python
status_var.set("欢迎使用小说阅读器")  # 设置状态栏的值
```



# 制作竖着的状态栏



```python
# 设置一个竖着的column_label放在左边,颜色换成灰色
column_var = tk.StringVar()  # 创建状态栏变量,用于显示当前列,从上到下
column_label = tk.Label(root, textvariable=column_var, bd=1, relief=tk.SUNKEN, anchor=tk.W, bg="gray", width=8)
column_label.pack(side=tk.LEFT, fill=tk.Y)

column_var.set("第一列")  # 设置状态栏的值
```



# `text`控件



```python
text_pad = tk.Text(root, undo=True, font=25)  # undo=True,可以撤销
text_pad.pack(expand=True, fill=tk.BOTH)  # expand=True,可以随着窗口的变化而变化, fill=tk.BOTH,可以填充整个窗口
```





# 修改text中的字体大小

* 采用二级菜单的方式

```python
def change_font_size(font_size=12):
    """
    改变字体大小
    :param font_size:
    :return:
    """
    text_pad.config(font=("Arial", font_size)) # 设置字体大小

# 使用一个二级菜单来设置字体大小
fontmenu = tk.Menu(menu, tearoff=0)
fontmenu.add_command(label="12", command=lambda: change_font_size(12))
fontmenu.add_command(label="14", command=lambda: change_font_size(14))
fontmenu.add_command(label="16", command=lambda: change_font_size(16))
fontmenu.add_command(label="18", command=lambda: change_font_size(18))
fontmenu.add_command(label="20", command=lambda: change_font_size(20))


# 把这个二级菜单添加到菜单栏
menu.add_cascade(label="字体大小", menu=fontmenu)
```



# `Scrollerbar`控件



```python
# 创建一个scroller
scroller = tk.Scrollbar(text_pad, width=20)  # 把scroller添加到text_pad
text_pad.config(yscrollcommand=scroller.set)  # 设置text_pad的yscrollcommand为scroller.set
scroller.config(command=text_pad.yview)  # 设置scroller的command为text_pad.yview
scroller.pack(side=tk.RIGHT, fill=tk.Y)  # 把scroller放在text_pad的右边,并且填充整个text_pad
```



# code:`记事本`

```python
import tkinter as tk

root = tk.Tk()
root.title("小说阅读器")
root.geometry("800x500+100+100")

# 创建一个菜单栏
menu = tk.Menu(root)  # 创建一个菜单栏
filemenu = tk.Menu(menu, tearoff=0)  # 创建一个文件菜单
filemenu.add_command(label="打开", command=None)
filemenu.add_command(label="保存", command=None)
menu.add_cascade(label="文件", menu=filemenu)

# 创建一个状态栏
status_var = tk.StringVar()  # 创建一个状态栏的变量
status_label = tk.Label(root, textvariable=status_var, bd=1, relief=tk.SUNKEN, anchor=tk.W)  # 创建一个状态栏的label
status_label.pack(side=tk.BOTTOM, fill=tk.X)  # 把状态栏放在root的底部,并且填充整个root

status_var.set("欢迎使用小说阅读器")  # 设置状态栏的内容

# 创建一个标签栏
column_var = tk.StringVar()
column_label = tk.Label(root, textvariable=column_var, bd=1, relief=tk.SUNKEN, anchor=tk.W, bg="gray",
                        width=8)  # 创建一个标签栏的label
column_label.pack(side=tk.LEFT, fill=tk.Y)  # 把标签栏放在root的左边,并且填充整个root

column_var.set("第一列")  # 设置标签栏的内容

text_pad = tk.Text(root, undo=True, font=25, bg='#FFFFCC')  # undo=True,可以撤销, font=25,字体大小为25,背景色为淡黄色
text_pad.pack(expand=True, fill=tk.BOTH)  # expand=True,可以随着窗口的变化而变化, fill=tk.BOTH,可以填充整个窗口


def change_font_size(font_size=12):
    """
    改变字体大小
    :param font_size:
    :return:
    """
    text_pad.config(font=("Arial", font_size))  # 设置字体大小


# 使用一个二级菜单来设置字体大小
fontmenu = tk.Menu(menu, tearoff=0)
fontmenu.add_command(label="12", command=lambda: change_font_size(12))
fontmenu.add_command(label="14", command=lambda: change_font_size(14))
fontmenu.add_command(label="16", command=lambda: change_font_size(16))
fontmenu.add_command(label="18", command=lambda: change_font_size(18))
fontmenu.add_command(label="20", command=lambda: change_font_size(20))

# 把这个二级菜单添加到菜单栏
menu.add_cascade(label="字体大小", menu=fontmenu)

# 创建一个scroller
scroller = tk.Scrollbar(text_pad, width=20)  # 把scroller添加到text_pad
text_pad.config(yscrollcommand=scroller.set)  # 设置text_pad的yscrollcommand为scroller.set
scroller.config(command=text_pad.yview)  # 设置scroller的command为text_pad.yview
scroller.pack(side=tk.RIGHT, fill=tk.Y)  # 把scroller放在text_pad的右边,并且填充整个text_pad

# 把菜单栏添加到root
root.config(menu=menu)

root.mainloop()
```





# `entry`控件

* 获取输出的内容

## 创建

```python
entry = tk.Entry(root, font=("Arial", 20))  # 创建一个entry
# entry = tk.Entry(root, font=("Arial", 20),show="*")  # show="*" 代表输入的内容用*代替
entry.pack()
```



## 获取里面的内容

```python
input_text = entry.get()  # 获取entry的内容
```



# 把内容输出到`text`中

* 实现函数

```python
def insert_point():
    """
    在光标处插入内容
    :return:
    """
    var = entry.get()  # 获取entry的内容
    text.insert("insert", var)  # 在光标处插入内容
```



* 绑定

```python
# 创建一个按钮,点击按钮,在光标处插入内容
btn_insert_point = tk.Button(root, text="在光标处插入内容", font=("Arial", 20), command=insert_point)
btn_insert_point.pack()
```



# `listbox`控件

> 使用并且设置内部的条目

```python
import tkinter as tk

root = tk.Tk()

var = tk.StringVar()
var.set((11, 22, 33, 44))  # 为变量设置值

listbox = tk.Listbox(root, listvariable=var,font = 30)  # 创建listbox
listbox.pack()

root.mainloop()
```



* 获取被选中的栏目

```python
listbox.curselection()  # 获取当前选中的值的索引
```



# `radio button`

* use radio button to print the string that you choose 

```python
# # no.5 radio button 练习
import tkinter as tk

root = tk.Tk()

# 设置一个label,显示选中的内容
var_label = tk.StringVar()
label = tk.Label(root, textvariable=var_label, font=30, bg='#FFFFCC')
label.pack()


def print_selection():
    """
    打印选中的内容
    :return:
    """
    label.config(text="您已经选择了" + var_label.get())  # 获取var_label的值,并且设置为label的text


# 设置radio button, width = 20, height = 2
radio_button1 = tk.Radiobutton(root, text="选项1", variable=var_label, value="选项1", font=30, width=20,
                               height=2, command=print_selection)  # 给variable设置一个值,当选中这个选项时,variable的值就是这个value
radio_button2 = tk.Radiobutton(root, text="选项2", variable=var_label, value="选项2", font=30, width=20, height=2,
                               command=print_selection)
radio_button3 = tk.Radiobutton(root, text="选项3", variable=var_label, value="选项3", font=30, width=20, height=2,
                               command=print_selection)

radio_button1.pack()
radio_button2.pack()
radio_button3.pack()

root.mainloop()
```

