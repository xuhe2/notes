* 使用PYTHON实现奇怪的SHELL功能



# 使用`pynput`实现监听

## 识别最近输入的一连串内容

```python
# 一个监听键盘输入的类
import re
import time

from webcrawler.NovelPassageCrawler import NovelPassageCrawler
from pynput.keyboard import Key, Listener
import os


class KeyboardListener:
    def __init__(self):
        self.esc_flag = False  # ESC键的标志
        self.listener = Listener(on_press=self.on_press, on_release=self.on_release)  # 创建监听器
        self.input = ''  # 儲存輸入的字串

    def clear_console(self):
        """
        清空控制台
        :return:
        """
        os.system('cls')

    def check_input(self):
        """
        检查输入的字串
        :return:
        """
        if self.input[-5:] == 'clear':  # 如果输入的字串最后四个字母是clear
            self.input = ''
            self.clear_console()  # 清空控制台
            return 'clear'  # 清空控制台

        if self.input[-4:] == 'exit':  # 如果输入的字串最后四个字母是exit
            self.input = ''
            # 停止监听
            self.listener.stop() # 停止监听



        return 'pass' # 什么都不做

    #

    def on_press(self, key):
        """
        按键按下的时候执行的函数
        :param key:
        :return:
        """
        # 检测到ESC键输入的时候,终止监听
        if key == Key.esc:
            self.esc_flag = True
            return False

        # 如果检测到CTRL键输入的时候，将标志设置为True
        try:
            # 储存输入的字串
            self.input += key.char  # 儲存輸入的字串
            self.check_input()  # 检查输入的字串
        except:
            pass

    def on_release(self, key):
        pass

    def start(self):
        """
        开始监听
        :return:
        """
        self.listener.start()  # 开始监听
        self.listener.join()  # 阻塞线程，直到监听器停止

    # 终止监听
    def stop(self):
        """
        停止监听
        :return:
        """
        self.listener.stop() # 停止监听


if __name__ == '__main__':
    url = 'https://m.23wxx.com/xs/30316/4368681.html'
    encoding = 'utf-8'

    novel_crawler = NovelPassageCrawler(url)

    print(novel_crawler.get_passage_content(use_filter='break'))

    test = KeyboardListener()
    test.start()
```



## 自动翻页

```python
# 一个监听键盘输入的类
import re
import time

from webcrawler.NovelPassageCrawler import NovelPassageCrawler
from pynput.keyboard import Key, Listener
import os


class KeyboardListener:
    def __init__(self, prev_page_func, next_page_func):
        self.esc_flag = False  # ESC键的标志

        # 上一页和下一页的函数
        self.prev_page_func = prev_page_func
        self.next_page_func = next_page_func

        self.listener = Listener(on_press=self.on_press, on_release=self.on_release)  # 创建监听器

    def __enter__(self):
        # 在进入上下文之前执行的操作
        # 初始化键盘监听器等
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        # 在退出上下文时执行的操作
        # 关闭键盘监听器等
        pass

    def on_press(self, key):
        """
        按键按下的时候执行的函数
        :param key:
        :return:
        """
        # 检测到ESC键输入的时候,终止监听
        if key == Key.esc:
            self.esc_flag = True
            self.listener.stop()

        # 如果检测到上箭头键或者回车输入的时候,则执行上一页的函数
        if key == Key.up or key == Key.enter:
            self.prev_page_func()

        # 如果检测到下箭头键输入的时候,则执行下一页的函数
        if key == Key.down:
            self.next_page_func()

    def on_release(self, key):
        pass

    def start(self):
        """
        开始监听
        :return:
        """
        self.listener.start()  # 开始监听
        self.listener.join()  # 阻塞线程，直到监听器停止

    # 终止监听
    def stop(self):
        """
        停止监听
        :return:
        """
        self.listener.stop()  # 停止监听


if __name__ == '__main__':
    def prev_page():
        print("上一页")


    def next_page():
        print("下一页")


    test = KeyboardListener(prev_page_func=prev_page, next_page_func=next_page)
    test.start()
```





## 移动光标

```python
\x1b[<n>A    # 将光标上移n行
\x1b[<n>B    # 将光标下移n行
```



# `shell code`



```python
# 实现小说阅读器的shell界面

from webcrawler.NovelCrawler import NovelCrawler
import csv
import os
import re
from KeyboardListener import KeyboardListener
from pynput.keyboard import Key, Controller


class Shell:
    def __init__(self):
        # 历史命令记录
        self.command_history = []

        # 阅读方式
        self.read_mode = '-shell'  # 默认为shell模式

        self.books = []  # 书籍列表
        self.last_read_index = []  # 最后阅读的索引
        with open('books.csv', 'r', encoding='utf-8') as f:
            reader = csv.reader(f)
            for row in reader:
                if not row:  # 如果是空行，則跳过
                    continue

                # 文件的格式是 name, url, from_tag, auto_next_page, last_read_index
                self.books.append(NovelCrawler(name=row[0].strip(), url=row[1].strip(), from_tag=row[2],
                                               auto_next_page=bool(row[3].strip())))  # 书籍
                self.last_read_index.append(int(row[4]))  # 最后阅读的索引

        self.book_url = None  # 当前的书籍的url
        self.book_index = None  # 当前的书籍的下标
        self.book_chapter = 1  # 当前的书籍的章节

    # 展示当前的状态
    def print_head(self):
        """
        打印当前的状态
        :return:
        """
        if self.book_index is None:
            print("[no book]>> ", end='')  # 没有书籍
        else:
            print(f"[reading `{self.books[self.book_index].info['name']}`]>> ", end='')  # 有书籍

    # 打印分割线
    def print_divider(self):
        """
        打印分割线
        :return:
        """
        print('-' * 89)
        print('-' * 40, 'divider', '-' * 40)  # 打印分割线
        print('-' * 89)

    # 获取阅读进度
    def get_progress(self, book_index):
        """
        获取阅读进度
        :return:
        """
        # 如果book_index超过了范围,则返回None
        if book_index < 0 or book_index >= len(self.books):
            return None

        return self.books[book_index].get_read_progress(self.last_read_index[book_index])  # 获取阅读进度

    def _ls(self, command):
        # 返回值元素初始化
        res = []

        # 第一个参数是ls,后面的参数可能是`-book/-b`或者`-chapter/-c`

        # 如果没有参数,则显示所有的书籍
        if len(command) == 1:
            for i in range(len(self.books)):
                # 使用get_progress()方法获取进度
                res.append(
                    f'no.{i}\tname: {self.books[i].name}\tlast_read: 第{self.last_read_index[i]}章\tprogress_rate: {self.get_progress(i)}%')
            return res

        # 如果有参数,则显示对应的书籍
        if command[1] == '-book' or command[1] == '-b':
            for i in range(len(self.books)):  # 显示书籍列表
                # 使用get_progress()方法获取进度
                res.append(
                    f'no.{i}\tname: {self.books[i].name}\tlast_read: 第{self.last_read_index[i]}章\tprogress_rate: {self.get_progress(i)}%')
            return res

        elif command[1] == '-chapter' or command[1] == '-c':
            # 如果不存在当前的书籍,则显示错误信息
            if self.book_index is None:
                res.append('ls error: no book selected')
                return res

            number = None
            if len(command) == 3 and (command[2] == '-number' or command[2] == '-n'):
                # 当参数为[-number/-n]时,默认显示10个章节
                number = 10
            elif len(command) == 4 and (command[2] == '-number' or command[2] == '-n') and command[3].isdigit():
                # 当参数为[-number/-n] [number]时,显示指定个数的章节
                number = int(command[3])
            elif len(command) < 3:
                # 当参数完全不存在时,pass
                pass
            else:
                # 显示参数错误信息
                res.append('ls error: wrong parameter')
                return res

            if number is None:
                # 显示当前书本章节列表,下标从1开始
                for i in range(self.books[self.book_index].max_chapter_index):
                    # 如果不是当前阅读的章节
                    if i + 1 != self.book_chapter:
                        res.append(f'       no.{i + 1}\t{self.books[self.book_index].chapter_info[i][0]}')  # 显示章节名字
                    else:
                        res.append(f'now->>[no.{i + 1}\t{self.books[self.book_index].chapter_info[i][0]}]<<-')  # 显示章节名字
            else:
                # 选取从上一次阅读的章节开始的number个章节,下标从1开始,所以要减1,同时防止越界
                for i in range(self.last_read_index[self.book_index] - 1,
                               min(self.last_read_index[self.book_index] - 1 + number,
                                   self.books[self.book_index].max_chapter_index)):
                    # 如果不是当前阅读的章节
                    if i + 1 != self.book_chapter:
                        res.append(f'       no.{i + 1}\t{self.books[self.book_index].chapter_info[i][0]}')
                    else:
                        res.append(f'now->>[no.{i + 1}\t{self.books[self.book_index].chapter_info[i][0]}]<<-')

            # 显示上一次阅读的章节和进度
            res.append('\n')  # 空行
            res.append(f'last read chapter: 第{self.last_read_index[self.book_index]}章')
            res.append(f'progress rate: {self.get_progress(self.book_index)}%')

            return res

        # 如果参数不对,则显示错误信息
        res.append(f'ls error: no command named {command[1]}')
        return res

    # 获取history命令要显示的内容
    def _history(self):
        return self.command_history  # 返回历史命令记录

    # 获取read命令要显示的内容
    def _read(self, command):
        # 如果不存在选中的书籍,则显示错误信息
        if self.book_index is None:
            print('read error: no book selected')
            return None

        # 初始化要阅读的章节的索引,默认是上一次阅读的章节
        index = self.last_read_index[self.book_index]

        for param in command[1:]:
            # 如果参数是章节的索引,则读取对应的章节
            if re.match(r'^\d+$', param):
                index = int(param)

            # 如果参数是阅读模式,则更新阅读模式
            elif param == '-shell' or param == '-s':
                self.read_mode = '-shell'
            elif param == '-window' or param == '-w':
                self.read_mode = '-window'
            else:
                print('read error: read method param error')
                return None

        # 检查章节索引是否合法
        if index < 1 or index > self.books[self.book_index].max_chapter_index:
            print('read error: chapter index error')
            return None

        # 更新阅读进度
        self.last_read_index[self.book_index] = index
        self.book_chapter = index

        # 如果来源是<div>标签
        # 返回要显示的内容
        if self.books[self.book_index].info['from_tag'] == 'div':
            return self.books[self.book_index].get_chapter_content_by_index(index - 1, use_filter='break',
                                                                            div_class='Readarea ReadAjax_content')
        elif self.books[self.book_index].info['from_tag'] == 'p':
            return self.books[self.book_index].get_chapter_content_by_index(index - 1, use_filter='break',
                                                                            div_class='content')
        else:
            # 如果来源上述标签,则显示错误信息
            print('read error: from_tag error')
            return None

    # 光标上移动到文章的开头的上一行
    def move_cursor_up(self, passage):
        """
        光标上移动n行
        :param n:
        :return:
        """
        # 找到`\n`的个数
        n = passage.count('\n')
        # 光标上移动n行
        print(f'\x1b[{n}A')

    # prev_page_func函数实现翻页
    def _prev_page_func(self):
        # 如果不存在选中的书籍,则显示错误信息
        if self.book_index is None:
            print('prev_page error: no book selected')
            return

        # 如果翻到不存在的页面,则显示错误信息
        if self.book_chapter == 1:
            print('prev_page error: no prev page')
            return

        # 翻页
        self.book_chapter -= 1
        self.last_read_index[self.book_index] = self.book_chapter

        # 读取章节
        if self.read_mode == '-shell':
            # 打印分割线
            self.print_divider()
            # 使用_read()方法读取章节
            print(self._read(['read', self.read_mode, str(self.book_chapter)]))

        # next_page_func函数实现翻页

    def _next_page_func(self):
        # 如果不存在选中的书籍,则显示错误信息
        if self.book_index is None:
            print('next_page error: no book selected')
            return

        # 如果翻到不存在的页面,则显示错误信息
        if self.book_chapter == self.books[self.book_index].max_chapter_index:
            print('next_page error: no next page')
            return

        # 翻页
        self.book_chapter += 1
        self.last_read_index[self.book_index] = self.book_chapter

        # 读取章节
        if self.read_mode == '-shell':
            # 打印分割线
            self.print_divider()
            # 使用_read()方法读取章节
            print(self._read(['read', self.read_mode, str(self.book_chapter)]))

    # 获取命令,切分命令
    def get_command(self, command):
        """
        获取命令
        :return:
        """
        # 切分命令
        try:
            # 用空格分割,去掉空白内容
            info = command.split(' ')
            info = [i.strip() for i in info if i.strip() != '']

            # 把格式为`"XX`和`XX"`的内容合并
            for i in range(len(info)):
                if re.match(r'^".*', info[i]) and not re.match(r'.*"$', info[i]):
                    info[i] = info[i] + ' ' + info[i + 1]
                    info[i + 1] = ''
            # 把格式为`'XX`和`XX'`的内容合并
            for i in range(len(info)):
                if re.match(r"^'.*", info[i]) and not re.match(r".*'$", info[i]):
                    info[i] = info[i] + ' ' + info[i + 1]
                    info[i + 1] = ''
            # 去除空白内容
            info = [i for i in info if i != '']

            # 去除''和""
            info = [i.strip("'").strip('"') for i in info]
        except Exception as e:
            print('add error:', e)
            return None

        return info

    """
    命令函数
    """

    # save命令
    def save(self):
        """
        将当前的书籍信息保存到文件中
        :return:
        """
        try:
            with open('books.csv', 'w', encoding='utf-8') as f:
                writer = csv.writer(f)
                for i in range(len(self.books)):
                    writer.writerow(
                        [self.books[i].info['name'], self.books[i].info['url'], self.books[i].info['from_tag'],
                         self.books[i].info['auto_next_page'], self.last_read_index[i]])

        except Exception as e:
            print('save error: ' + e)

    # help命令
    def help(self, command):
        # 第一个参数是`help`,可能存在第二个参数,第二个参数代表要访问的命令

        # 初始化所有的帮助信息
        helps = {
            'help': """
            help [command]
            显示帮助信息,如果有command参数,则显示command的帮助信息
            """,

            'add': """
            add url [-p/-d] [-n/-name name] [-c/-close-auto]
            添加书籍,第一个参数是书籍的URL,第二个参数是书籍的来源,默认是<p>标签,第三个参数是书籍的名字,默认是unknown,第四个参数是是否自动翻页,默认是True
            """,

            'rm': """
            rm index
            删除书籍,第一个参数是书籍的下标(从0开始)
            """,

            'ls': """
            ls [-book/-b] [-chapter/-c] [-number/-n] [number]
            显示书籍列表,第一个参数是显示书籍列表,第二个参数是显示章节列表
            最后的参数代表从上一次阅读的章节开始往后显示number个章节
            """,

            'read': """
            read [-shell/-s]/[-window/-w] [index] 
            读取书籍,第一个参数是书籍章节的下标(从1开始),如果没有参数,则读取上一次阅读的书籍的章节
            使用-shell参数,则使用shell模式,使用-window参数,则使用窗口模式
            """,

            'choose': """
            choose [index]
            选择书籍,第一个参数是书籍的下标(从0开始)
            """,

            'clear': """
            clear
            清屏
            """,

            'history': """
            history
            显示历史命令
            """,
            'save': """
            save
            保存书籍信息
            """,

            'exit': """
            exit
            退出程序
            """
        }

        # 如果没有参数,则显示所有的帮助信息
        if len(command) == 1:
            for key in helps:
                print(helps[key])
            return
        else:
            # 如果有参数,则显示对应的帮助信息
            if command[1] in helps:
                print(helps[command[1]])
            else:
                print(f'no command named {command[1]}')

    # add命令
    def add(self, command):
        """
        添加书籍
        :param command:
        :return:
        """

        # 第一个参数是add,第二个参数是URL
        if len(command) < 2:
            print('add error: not enough parameters')
            return
        if not re.match(r'^https?://.*', command[1]):
            print('add error: url error')
            return

        # 初始化
        from_tag = 'div'  # 默认是<div>标签
        auto_next_page = True  # 默认是自动翻页
        name = 'unknown'  # 默认书籍名字是unknown

        for param in command:
            # 来源是<p>标签
            if param == '-p':
                from_tag = 'p'

            # 来源是<div>标签
            if param == '-d' or param == '-div':
                from_tag = 'div'

            # 当`-name/-n`的时候,下一个参数是书籍的名字
            if param == '-n' or param == '-name':
                # 如果下一个参数开头是`-`,说明没有书籍名字
                if command[command.index(param) + 1][0] == '-':
                    continue
                name = command[command.index(param) + 1]

            # 当`-close-auto/-c`的时候,不自动查找下一页的章节
            if param == '-c' or param == '-close-auto':
                auto_next_page = False

        # 加入books
        self.books.append(NovelCrawler(name=name, url=command[1], from_tag=from_tag, auto_next_page=auto_next_page))

        # 加入last_read_index
        self.last_read_index.append(1)

        # 保存
        self.save()

    # 删除书籍
    def rm(self, index):
        """
        删除书籍
        :param index:
        :return:
        """
        # 不在范围内
        if index < 0 or index >= len(self.books):
            print('rm error: index out of range')
            return

        # 删除
        try:
            self.books.pop(index)  # 删除书本
            self.last_read_index.pop(index)  # 删除最近阅读的下标

            # 如果删除的是当前的书籍,则重置当前的书籍
            if self.book_index == index:
                self.book_url = None
                self.book_index = None
                self.book_chapter = 1

        except Exception as e:
            print('rm error:', e)
            return

        # 保存
        self.save()

    # 获取ls命令要显示的书籍列表

    # ls命令
    def ls(self, command):
        # 获取要显示的列表
        res = self._ls(command)

        # 打印列表
        for i in res:
            print(i)

    # clear命令
    def clear(self):
        # 清屏
        os.system('cls')

    # history命令
    def history(self):
        # 打印历史记录
        index = 0
        for i in self.command_history:
            index += 1
            print(f'{index}: {i}')

    # exit命令
    def exit(self):
        # 保存
        self.save()
        # 退出程序具体实现在`run`函数中

    # choose命令
    def choose(self, command):
        """
        选择书籍
        :param command:
        :return:
        """
        # 如果没有参数,则显示错误信息
        if len(command) == 1:
            print('choose error: not enough parameters')
            return

        # 如果有参数,则选择书籍
        try:
            self.book_index = int(command[1])
            self.book_url = self.books[self.book_index].url
            self.book_chapter = self.last_read_index[self.book_index]

        except Exception as e:
            print('choose error:', e)
            return

    # read命令
    def read(self, command):
        # 打印分割线
        self.print_divider()
        # 使用_read函数读取
        passage = self._read(command)
        print(passage)

        # 使用KeyboardListener监听键盘输入
        with KeyboardListener(prev_page_func=self._prev_page_func, next_page_func=self._next_page_func) as listener:
            self.listener = listener
            self.listener.start()

    # run命令
    def run(self):
        # 欢迎信息
        print('Welcome to NovelReader!')
        print('Type "help" to get help')

        command = ''
        while True:
            # 打印头部
            self.print_head()
            # 输入命令
            command = input()
            # 添加到历史记录
            self.command_history.append(command)
            # 获取命令
            command = self.get_command(command)

            # 如果命令是None或者空的,则继续循环
            if command is None or command == []:
                continue

            # `add`命令
            if command[0] == 'add':
                self.add(command)

            # `rm`命令
            elif command[0] == 'rm':
                self.rm(int(command[1]))

            # `ls`命令
            elif command[0] == 'ls':
                self.ls(command)

            # `clear`命令
            elif command[0] == 'clear':
                self.clear()

            # `history`命令
            elif command[0] == 'history':
                self.history()

            # `help`命令
            elif command[0] == 'help':
                self.help(command)

            # `exit`命令
            elif command[0] == 'exit':
                self.exit()
                break

            # `choose`命令
            elif command[0] == 'choose':
                self.choose(command)

            # `read`命令
            elif command[0] == 'read':
                self.read(command)

            # `save`命令
            elif command[0] == 'save':
                self.save()

            # 不存在的错误命令
            else:
                print('error: command not found')


if __name__ == '__main__':
    shell = Shell()
    shell.run()
    # data = 'add https://www.tasim.net/book/10967/ -d -n "今天也没变成玩偶呢"'
    #
    # data = test.get_command(data)
    # # print(data)
    # #
    # test.add(data)  # 添加书籍
    # # print(test.books[0].info)
    #
    # test.choose(['choose', '0'])  # 选择书籍
    #
    # test.print_head()
    # my_input = input()
    # test.ls(test.get_command(my_input))  # 显示书籍列表
    #
    # # test.clear()  # 清屏
    # # test.help(test.get_command(my_input))
    #
    # # test.ls(test.get_command('ls -b'))  # 显示书籍列表
    # #
    # # test.read(test.get_command('read 1'))  # 读取书籍
    #
    # test.rm(0)  # 删除书籍
    # print(len(test.books))
```

