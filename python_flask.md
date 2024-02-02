# 返回数据

默认是**HTML**类型,如果需要返回接收到的数据,我们需要使用`return f"Hello, {escape(name)}!"`进行转义.



# 接受参数类型

`@app.route('/post/<int:post_id>')`

| `string` | （缺省值） 接受任何不包含斜杠的文本 |
| -------- | ----------------------------------- |
| `int`    | 接受正整数                          |
| `float`  | 接受正浮点数                        |
| `path`   | 类似 `string` ，但可以包含斜杠      |
| `uuid`   | 接受 UUID 字符串                    |



# 是否使用URL尾部斜杠

> `projects` 的 URL 是中规中矩的，尾部有一个斜杠，看起来就如同一个文 件夹。访问一个没有斜杠结尾的 URL （ `/projects` ）时 Flask 会自动进 行重定向，帮您在尾部加上一个斜杠（ `/projects/` ）。
>
> `about` 的 URL 没有尾部斜杠，因此其行为表现与一个文件类似。如果访问 这个 URL 时添加了尾部斜杠（ `/about/` ）就会得到一个 404 “未找到” 错误。这样可以保持 URL 唯一，并有助于搜索引擎重复索引同一 页面。



# 使用`url_for`函数访问一个函数的URL请求地址

```python
from flask import url_for

app = Flask(__name__)

@app.route('/')
def index():
    return 'index'

@app.route('/login')
def login():
    return 'login'

@app.route('/user/<username>')
def profile(username):
    return f'{username}\'s profile'

with app.test_request_context():
    print(url_for('index'))
    print(url_for('login'))
    print(url_for('login', next='/'))
    print(url_for('profile', username='John Doe'))
```



# HTTP方法

可以使用 [`route()`](https://dormousehole.readthedocs.io/en/latest/api.html#flask.Flask.route) 装饰器的 `methods` 参数来处理不同的 HTTP 方法。

```python
from flask import request

@app.route('/login', methods=['GET', 'POST'])
```



* 可以使用快捷方式调用



# 渲染模板

使用 [`render_template()`](https://dormousehole.readthedocs.io/en/latest/api.html#flask.render_template) 方法可以渲染模板，您只要提供模板 名称和需要作为参数传递给模板的变量就行了。下面是一个简单的模板渲染例 子:

```python
from flask import render_template

@app.route('/hello/')
@app.route('/hello/<name>')
def hello(name=None):
    return render_template('hello.html', name=name)
```



# 文件处理

如果想要知道文件上传之前其在客户端系统中的名称，可以使用 [`filename`](https://werkzeug.palletsprojects.com/en/2.3.x/datastructures/#werkzeug.datastructures.FileStorage.filename) 属性。但是请牢 记这个值是可以伪造的，永远不要信任这个值。如果想要把客户端的文件名作 为服务器上的文件名，可以通过 Werkzeug 提供的 [`secure_filename()`](https://werkzeug.palletsprojects.com/en/2.3.x/utils/#werkzeug.utils.secure_filename) 函数

`file.save(f"/var/www/uploads/{secure_filename(file.filename)}")`



```python
f = request.files['the_file']
f.save('/var/www/uploads/uploaded_file.txt')
```



# 请求数据

```python
from flask import request
```

> 请求数据在request中



## 访问cookies

```python
from flask import request

@app.route('/')
def index():
    username = request.cookies.get('username')
    # use cookies.get(key) instead of cookies[key] to not get a
    # KeyError if the cookie is missing
```

> 使用cookies的get方法,可以实现安全查询



## 设置cookies

```python
from flask import make_response

@app.route('/')
def index():
    resp = make_response(render_template(...))
    resp.set_cookie('username', 'the username')
    return resp
```



# session 

使用会话之前您必须设置一个密钥。

```python
from flask import session

# Set the secret key to some random bytes. Keep this really secret!
app.secret_key = b'_5#y2L"F4Q8z\n\xec]/'

@app.route('/')
def index():
    if 'username' in session:
        return f'Logged in as {session["username"]}'
    return 'You are not logged in'

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        session['username'] = request.form['username']
        return redirect(url_for('index'))
    return '''
        <form method="post">
            <p><input type=text name=username>
            <p><input type=submit value=Login>
        </form>
    '''

@app.route('/logout')
def logout():
    # remove the username from the session if it's there
    session.pop('username', None)
    return redirect(url_for('index'))
```



# 使用log日志



```python
app.logger.debug('A value for debugging')
app.logger.warning('A warning occurred (%d apples)', 42)
app.logger.error('An error occurred')
```



# 模板



```python
<h1>{{ username }}的个人主页</h1>
{% if bio %}
    <p>{{ bio }}</p>  {# 这里的缩进只是为了可读性，不是必须的 #}
{% else %}
    <p>自我介绍为空。</p>
{% endif %}  {# 大部分 Jinja 语句都需要声明关闭 #}
```

- `{{ ... }}` 用来标记变量。
- `{% ... %}` 用来标记语句，比如 if 语句，for 语句等。
- `{# ... #}` 用来写注释。



## 使用`render_template`函数的作用

> 模板代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>{{ name }}'s Watchlist</title>
</head>
<body>
    <h2>{{ name }}'s Watchlist</h2>
    {# 使用 length 过滤器获取 movies 变量的长度 #}
    <p>{{ movies|length }} Titles</p>
    <ul>
        {% for movie in movies %}  {# 迭代 movies 变量 #}
        <li>{{ movie.title }} - {{ movie.year }}</li>  {# 等同于 movie['title'] #}
        {% endfor %}  {# 使用 endfor 标签结束 for 语句 #}
    </ul>
    <footer>
        <small>&copy; 2018 <a href="http://helloflask.com/book/3">HelloFlask</a></small>
    </footer>
</body>
</html>
```



使用构建模板的函数

```python
from flask import Flask, render_template

# ...

@app.route('/')
def index():
    return render_template('index.html', name=name, movies=movies)
```



# 静态文件

静态文件（static files）和我们的模板概念相反，指的是内容不需要动态生成的文件。比如图片、CSS 文件和 JavaScript 脚本等。



```html
<img src="{{ url_for('static', filename='foo.jpg') }}">
```



# 数据库操作(ORM)

```bash
(env) $ pip install flask-sqlalchemy==2.5.1 sqlalchemy==1.4.47
```



## 创建数据库示例

```python
import os
import sys

from flask import Flask
from flask_sqlalchemy import SQLAlchemy

WIN = sys.platform.startswith('win')
if WIN:  # 如果是 Windows 系统，使用三个斜线
    prefix = 'sqlite:///'
else:  # 否则使用四个斜线
    prefix = 'sqlite:////'

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = prefix + os.path.join(app.root_path, 'data.db')
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False  # 关闭对模型修改的监控
# 在扩展类实例化前加载配置
db = SQLAlchemy(app)
```



## 创建数据库的表

```python
class User(db.Model):  # 表名将会是 user（自动生成，小写处理）
    id = db.Column(db.Integer, primary_key=True)  # 主键
    name = db.Column(db.String(20))  # 名字


class Movie(db.Model):  # 表名将会是 movie
    id = db.Column(db.Integer, primary_key=True)  # 主键
    title = db.Column(db.String(60))  # 电影标题
    year = db.Column(db.String(4))  # 电影年份
```

- 模型类要声明继承 `db.Model`。
- 每一个类属性（字段）要实例化 `db.Column`，传入的参数为字段的类型，下面的表格列出了常用的字段类。
- 在 `db.Column()` 中添加额外的选项（参数）可以对字段进行设置。比如，`primary_key` 设置当前字段是否为主键。除此之外，常用的选项还有 `nullable`（布尔值，是否允许为空值）、`index`（布尔值，是否设置索引）、`unique`（布尔值，是否允许重复值）、`default`（设置默认值）等。

常用的字段类型如下表所示：

| 字段类           | 说明                                          |
| :--------------- | :-------------------------------------------- |
| db.Integer       | 整型                                          |
| db.String (size) | 字符串，size 为最大长度，比如 `db.String(20)` |
| db.Text          | 长文本                                        |
| db.DateTime      | 时间日期，Python `datetime` 对象              |
| db.Float         | 浮点数                                        |
| db.Boolean       | 布尔值                                        |



## 创建数据库

* 可以使用命令行创建

```shel
(env) $ flask shell
>>> from app import db
>>> db.create_all()
```



* 可以使用代码



## 添加到数据库

需要向数据库对话内部添加

1. 使用自己创建的类构建一个数据
2. `db.session.add(user)  # 把新创建的记录添加到数据库会话`把数据添加到其中

> 添加内容,会把数据提交到一个临时空间

3. 提交`db.session.commit()  # 提交数据库会话，只需要在最后调用一次即可`



## 查询

查询方式`<模型类>.query.<过滤方法（可选）>.<查询方法>`



下面是一些常用的过滤方法：

| 过滤方法    | 说明                                                         |
| :---------- | :----------------------------------------------------------- |
| filter()    | 使用指定的规则过滤记录，返回新产生的查询对象                 |
| filter_by() | 使用指定规则过滤记录（以关键字表达式的形式），返回新产生的查询对象 |
| order_by()  | 根据指定条件对记录进行排序，返回新产生的查询对象             |
| group_by()  | 根据指定条件对记录进行分组，返回新产生的查询对象             |

下面是一些常用的查询方法：

| 查询方法       | 说明                                                         |
| :------------- | :----------------------------------------------------------- |
| all()          | 返回包含所有查询记录的列表                                   |
| first()        | 返回查询的第一条记录，如果未找到，则返回 None                |
| get(id)        | 传入主键值作为参数，返回指定主键值的记录，如果未找到，则返回 None |
| count()        | 返回查询结果的数量                                           |
| first_or_404() | 返回查询的第一条记录，如果未找到，则返回 404 错误响应        |
| get_or_404(id) | 传入主键值作为参数，返回指定主键值的记录，如果未找到，则返回 404 错误响应 |
| paginate()     | 返回一个 Pagination 对象，可以对记录进行分页处理             |



## 更新数据

1. 先获得数据对应的对象
2. 修改之后重新提交

```python
>>> movie = Movie.query.get(2)
>>> movie.title = 'WALL-E'  # 直接对实例属性赋予新的值即可
>>> movie.year = '2008'
>>> db.session.commit()  # 注意仍然需要调用这一行来提交改动
```



## 删除

删除的时候,需要用数据对应的对象作为删除的标准

```python
>>> movie = Movie.query.get(1)
>>> db.session.delete(movie)  # 使用 db.session.delete() 方法删除记录，传入模型实例
>>> db.session.commit()  # 提交改动
```





# 实现一个命令行操作

```python
import click


@app.cli.command()  # 注册为命令，可以传入 name 参数来自定义命令
@click.option('--drop', is_flag=True, help='Create after drop.')  # 设置选项
def initdb(drop):
    """Initialize the database."""
    if drop:  # 判断是否输入了选项
        db.drop_all()
    db.create_all()
    click.echo('Initialized database.')  # 输出提示信息
```



# 模板进阶

处理404错误

```python
@app.errorhandler(404)  # 传入要处理的错误代码
def page_not_found(e):  # 接受异常对象作为参数
    user = User.query.first()
    return render_template('404.html', user=user), 404  # 返回模板和状态码
```



## 模板上下文处理函数

使用`@app.context_processor`注入依赖

> 当一个变量在绝大多数的文件中都是用到的时候,我们需要直接让这个变量对外可见

```python
@app.context_processor
def inject_user():  # 函数名可以随意修改
    user = User.query.first()
    return dict(user=user)  # 需要返回字典，等同于 return {'user': user}
```

* 最后需要返回字典



## 编写一个base_html_template



```html
<!DOCTYPE html>
<html lang="en">
<head>
    {% block head %}
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ user.name }}'s Watchlist</title>
    <link rel="icon" href="{{ url_for('static', filename='favicon.ico') }}">
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}" type="text/css">
    {% endblock %}
</head>
<body>
    <h2>
        <img alt="Avatar" class="avatar" src="{{ url_for('static', filename='images/avatar.png') }}">
        {{ user.name }}'s Watchlist
    </h2>
    <nav>
        <ul>
            <li><a href="{{ url_for('index') }}">Home</a></li>
        </ul>
    </nav>
    {% block content %}{% endblock %}
    <footer>
        <small>&copy; 2018 <a href="http://helloflask.com/book/3">HelloFlask</a></small>
    </footer>
</body>
</html>
```

> 在基模板里，我们添加了两个块，一个是包含 `<head></head>` 内容的 `head` 块，另一个是用来在子模板中插入页面主体内容的 `content` 块。在复杂的项目里，你可以定义更多的块，方便在子模板中对基模板的各个部分插入内容。另外，块的名字没有特定要求，你可以自由修改。

* 默认模板内容是被覆盖的,如果,需要使用原来的内容,使用`{{super()}}`



# 表单



```html
<form method="post">  <!-- 指定提交方法为 POST -->
    <label for="name">名字</label>
    <input type="text" name="name" id="name"><br>  <!-- 文本输入框 -->
    <label for="occupation">职业</label>
    <input type="text" name="occupation" id="occupation"><br>  <!-- 文本输入框 -->
    <input type="submit" name="submit" value="登录">  <!-- 提交按钮 -->
</form>
```

> * 默认使用`GET`请求
>
> `<input>`输入使用`name`来确定对应的字段
>
> * 当鼠标点击对应的`<label>`标签的时候触发输入框,使用`for`



## 设置提交按钮

```python
<input class="btn" type="submit" name="submit" value="Add">
```



## 处理表单数据

默认情况下，当表单中的提交按钮被按下，浏览器会创建一个新的请求，默认发往当前 URL（在 `<form>` 元素使用 `action` 属性可以自定义目标 URL）。



### 请求对象

```python
from flask import request
```



### flash消息

向模板传递提示消息

```python
from flask import flash
```



## 重定向响应

重定向到另一个URL

```python
if not title or not year or len(year) != 4 or len(title) > 60:
    flash('Invalid title or year!')  
    return redirect(url_for('index'))  # 重定向回主页
flash('Item created.')
return redirect(url_for('index'))  # 重定向回主页
```



# 保存密码

使用密文保存密码



使用**werkzeug**实现

```python
>>> from werkzeug.security import generate_password_hash, check_password_hash
>>> pw_hash = generate_password_hash('dog')  # 为密码 dog 生成密码散列值
>>> pw_hash  # 查看密码散列值
'pbkdf2:sha256:50000$mm9UPTRI$ee68ebc71434a4405a28d34ae3f170757fb424663dc0ca15198cb881edc0978f'
>>> check_password_hash(pw_hash, 'dog')  # 检查散列值是否对应密码 dog
True
>>> check_password_hash(pw_hash, 'cat')  # 检查散列值是否对应密码 cat
False
```



## 设置类

继承于`db.Model`的PYTHON对象也可以使用方法

```python
from werkzeug.security import generate_password_hash, check_password_hash


class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(20))
    username = db.Column(db.String(20))  # 用户名
    password_hash = db.Column(db.String(128))  # 密码散列值

    def set_password(self, password):  # 用来设置密码的方法，接受密码作为参数
        self.password_hash = generate_password_hash(password)  # 将生成的密码保持到对应字段

    def validate_password(self, password):  # 用于验证密码的方法，接受密码作为参数
        return check_password_hash(self.password_hash, password)  # 返回布尔值
```



# 使用`flask-login`实现功能



```python
from flask_login import LoginManager

login_manager = LoginManager(app)  # 实例化扩展类

@login_manager.user_loader
def load_user(user_id):  # 创建用户加载回调函数，接受用户 ID 作为参数
    user = User.query.get(int(user_id))  # 用 ID 作为 User 模型的主键查询对应的用户
    return user  # 返回用户对象
```



数据库对象继承`UserMixin`

```python
from flask_login import UserMixin


class User(db.Model, UserMixin):
    # ...
```

> `is_authenticated` 属性：如果当前用户已经登录，那么 `current_user.is_authenticated` 会返回 `True`， 否则返回 `False`。有了 `current_user` 变量和这几个验证方法和属性，我们可以很轻松的判断当前用户的认证状态。



```python
from flask_login import login_required, logout_user

# ...

@app.route('/logout')
@login_required  # 用于视图保护，后面会详细介绍
def logout():
    logout_user()  # 登出用户
    flash('Goodbye.')
    return redirect(url_for('index'))  # 重定向回首页
```



## 认证保护

```python
@app.route('/movie/delete/<int:movie_id>', methods=['POST'])
@login_required  # 登录保护
def delete(movie_id):
    movie = Movie.query.get_or_404(movie_id)
    db.session.delete(movie)
    db.session.commit()
    flash('Item deleted.')
    return redirect(url_for('index'))
```

使用`login_required`可以实现登陆保护效果



添加了这个装饰器后，如果未登录的用户访问对应的 URL，Flask-Login 会把用户重定向到登录页面，并显示一个错误提示。为了让这个重定向操作正确执行，我们还需要把 `login_manager.login_view` 的值设为我们程序的登录视图端点（函数名），把下面这一行代码放到 `login_manager` 实例定义下面即可：

```python
login_manager.login_view = 'login'
```

* 可以通过设置 `login_manager.login_message` 来自定义错误提示消息



## 访问当前用户

使用`current_user`实现

```python
from flask_login import login_required, current_user

# ...

@app.route('/settings', methods=['GET', 'POST'])
@login_required
def settings():
    if request.method == 'POST':
        name = request.form['name']

        if not name or len(name) > 20:
            flash('Invalid input.')
            return redirect(url_for('settings'))

        current_user.name = name
        # current_user 会返回当前登录用户的数据库记录对象
        # 等同于下面的用法
        # user = User.query.first()
        # user.name = name
        db.session.commit()
        flash('Settings updated.')
        return redirect(url_for('index'))

    return render_template('settings.html')
```



## 模板内容保护

```html
<!-- 在模板中可以直接使用 current_user 变量 -->
{% if current_user.is_authenticated %}
<form method="post">
    Name <input type="text" name="title" autocomplete="off" required>
    Year <input type="text" name="year" autocomplete="off" required>
    <input class="btn" type="submit" name="submit" value="Add">
</form>
{% endif %}
```

> 自动检查用户是否登陆,然后生成模板



# 测试



## 单元测试

使用`unittest`实现

```python
import unittest

from hello import sayhello


class SayHelloTestCase(unittest.TestCase):  # 测试用例

    def setUp(self):  # 测试固件
        pass

    def tearDown(self):  # 测试固件
        pass

    def test_sayhello(self):  # 第 1 个测试
        rv = sayhello()
        self.assertEqual(rv, 'Hello!')

    def test_sayhello_to_somebody(self):  # 第 2 个测试
        rv = sayhello(to='Grey')
        self.assertEqual(rv, 'Hello, Grey!')


if __name__ == '__main__':
    unittest.main()
```

> 测试用例继承 `unittest.TestCase` 类，在这个类中创建的以 `test_` 开头的方法将会被视为测试方法。



- assertEqual(a, b)
- assertNotEqual(a, b)
- assertTrue(x)
- assertFalse(x)
- assertIs(a, b)
- assertIsNot(a, b)
- assertIsNone(x)
- assertIsNotNone(x)
- assertIn(a, b)
- assertNotIn(a, b)



```python
import unittest

from app import app, db, Movie, User


class WatchlistTestCase(unittest.TestCase):

    def setUp(self):
        # 更新配置
        app.config.update(
            TESTING=True,
            SQLALCHEMY_DATABASE_URI='sqlite:///:memory:'
        )
        # 创建数据库和表
        db.create_all()
        # 创建测试数据，一个用户，一个电影条目
        user = User(name='Test', username='test')
        user.set_password('123')
        movie = Movie(title='Test Movie Title', year='2019')
        # 使用 add_all() 方法一次添加多个模型类实例，传入列表
        db.session.add_all([user, movie])
        db.session.commit()

        self.client = app.test_client()  # 创建测试客户端
        self.runner = app.test_cli_runner()  # 创建测试命令运行器

    def tearDown(self):
        db.session.remove()  # 清除数据库会话
        db.drop_all()  # 删除数据库表

    # 测试程序实例是否存在
    def test_app_exist(self):
        self.assertIsNotNone(app)

    # 测试程序是否处于测试模式
    def test_app_is_testing(self):
        self.assertTrue(app.config['TESTING'])
```

> 需要继承`unittest.TestCase`



使用`status_code`检测状态码



# 使用mysql

```python
pymysql.install_as_MySQLdb()


class Config(object):
    """配置参数"""
    # 设置连接数据库的URL
    user = 'root'
    password = ''
    database = 'flask_learn'
    app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://%s:%s@127.0.0.1:3306/%s' % (user, password, database)

    # # 设置sqlalchemy自动更跟踪数据库
    # SQLALCHEMY_TRACK_MODIFICATIONS = True
    #
    # # 查询时会显示原始SQL语句
    # app.config['SQLALCHEMY_ECHO'] = True
    #
    # # 禁止自动提交数据处理
    # app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = False


# 读取配置
app.config.from_object(Config)

# 创建数据库sqlalchemy工具对象
db = SQLAlchemy(app)


class Role(db.Model):
    # 定义表名
    __tablename__ = 'roles'
    # 定义字段
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    name = db.Column(db.String(64), unique=True)
    users = db.relationship('User', backref='role')  # 反推与role关联的多个User模型对象


class User(db.Model):
    # 定义表名
    __tablename__ = 'users'
    # 定义字段
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    name = db.Column(db.String(64), unique=True, index=True)
    email = db.Column(db.String(64), unique=True)
    pswd = db.Column(db.String(64))
    role_id = db.Column(db.Integer, db.ForeignKey('roles.id'))  # 设置外键
```



# 使用`<link>`导入CSS样式

```html
<link rel="stylesheet" href="{{ url_for('static', filename='style/LoginView.css') }}">
```



# 设置蓝图

使用`Blueprint`,

```python
from flask import Flask, render_template, redirect, url_for, Blueprint

auth = Blueprint('auth', __name__)


@auth.route('/login')
def login():
    return render_template('Auth.html')
```

使用蓝图

```python
app = Flask(__name__)
app.register_blueprint(auth, url_prefix='/auth')
```

访问蓝图

```python
url_for('auth.login')
```



# 生成session secret key

```python
import secrets
app.secret_key = secrets.token_hex(16)
```



# 使用当前的APP

```python
from flask import current_app
```



# JSON

用来包裹字符串的双引号



## 获取请求体body中的内容

```python
# 把request.data转换成JSON
    try:
        data = json.loads(request.data)
    except json.JSONDecodeError as e:
        # 处理解析错误
        return jsonify({"error": "Invalid JSON format"}), 400
```





# 取消默认form提交

使用表单验证实现

```html
<form action="/auth/register" id="registrationForm" method="post" onsubmit="return validateForm()">
```



```javascript
    function validateForm() {
        {#构建数据对象#}
        let info = {
            Name: document.getElementById("username").value,
            Password: document.getElementById("password").value,
            Type: "user",
            AddBy: {
                Name: "",
                Type: ""
            }
        };

        {#发送 Axios 请求#}
        axios.post('/auth/register', info, {
            headers: {
                'Content-Type': 'application/json'
            }
        })
            .then(function (response) {
                {#处理响应#}
                console.log(response.data);
                alert('注册成功！');
            })
            .catch(function (error) {
                {#处理错误#}
                console.error(error);
            });

        {#返回 false 阻止默认表单提交行为#}
        return false;
    }
```

