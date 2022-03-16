# flask 学习
# 章一 初识Flask
## Pipenv 的下载和使用
**Pipenv 的下载**

```pip install pipenv```

**Pipenv 的使用**

首先确保当前的工作目录在示例程序项目的根目录，使用`pipenv install`

- 若是想要显示的激活虚拟环境 ： `pipenv shell` 然后使用`exit`推出
- 当然也可以只使用 `pipenv run `
 > pipenv run python hello.py 

## 1.2 Hello Flask
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return '<h1>Hello Flask</h1>'
```

对于语句进行逐个解释
```
from flask import Flask
app = Flask(__name__)
```
从flask包导入Flask类，实例化这个类，就得到了程序实例app
传入Flask类构造方法的第一个参数是模块或者包的名称，所以使用特殊变量`__name__`

>  Python会根据所处的模块来赋予_ name_ 变量相应的值，对于我们的程序来说( app.py),这个值为app。除此之外，这也会帮助Flask在相应的文件夹里找到需要的资源，比如模板和静态文件。

### 1.2.1 注册路由

在一个Web应用里，客户端和服务器上的Flask程序的交互可以简单概括为以下几步:

1. 用户在浏览器输人URL访问某个资源。

2.  Flask接收用户请求并分析请求的URL。

3. 为这个URL找到对应的处理函数。

4. 执行函数并生成响应，返回给浏览器。

5. 浏览器接收并解析响应，将信息显示在页面中。

我们要做的是:

建立处理请求的函数，并为其定义对应的URL规则。

只需为函数附加**app.route()装饰器**，并传入URL规则作为参数，我们就可以让URL与函数建立关联。

这个过程我们称为**注册路由( route)**，路由负责管理URL和函数之间的映射，而这个函数则被称为**视图函数(viewfunction)**。

> **路由**是一个动词：按某路线发送|调用与请求URL对应的视图函数

app.route()装饰器把根地址/和index()函数绑定起来，当用户访问这个URL时就会触发index()函数。

视图函数返回的值将作为响应的主体

#### 视图绑定多个URL

```
# 一个视图函数绑定多个URl
@app.route('/hi')
@app.route('/hello')
def sayhello():
    return '<h1>HelloFlask!</h1>'
```

#### 动态URL | 在 URl 规则中添加变量   

使用`<变量名>`在URL中，Flask在处理请求时候，会将变量传入视图函数，所以可以添加参数来获取这个变量值

```
# 在URL中引入变量
@app. route(' /greet/ <name>')
def greet (name) :
    return '<h1>Hello,%s!</h1>' %name
```

因为URL中可以包含变量，所以我们将传入app.route()的字符串称为**URL规则**，而不是URL。

Flask会解析请求并把请求的URL与视图函数的URL规则进行匹配。

比如，这个greet视图的URL规则为/greet/<name>，那么类似/greet/foo、/greet/bar的请求都会触发这个视图函数。

而当URL规则包含变量的时候，若是用户所访问的URl中没有添加变量，那么Flask会在匹配失败后，返回一个 `404`，因此：

可以在`app.route`装饰器里使用**URl变量默认值**：对应的参数为:`defaults`，该参数接收**字典**作为输入，存储URL变量和默认值的映射

```
# 在URL中引入变量
# 并设置默认值
@app.route('/greet',defaults={'name':'Programmer'})
@app.route('/greet/<name>')
def greet (name) :
    return '<h1>Hello,%s!</h1>' %name
```

## 1.3 启动开发服务器

### 1.3.1 Run，Flask，Run！

```
flask run
```

#### 自动发现程序实例

在运行程序前，一般需要提供程序实例所在的模块的位置，但是flask也会也会自动的去探测程序的实例（这就是原来为什么一直要export FLASK_APP）,Flask的自动探测规则为：

- 从当前目录寻找app.py和wsgi.py模块，并从中寻找名为app或application的程序实例。
- 从环境变量FLASK_ _APP对应的值寻找名为app或application的程序实例。
- 如果安装了`python-dotenv`，会使用它自动从`.flaskenv`和`.env`中加载环境变量

#### 安装 dotenv 和其使用方法 为了避免频繁设置环境变量

“除了FLASK_APP,在后面我们还会用到其他环境变量。环境变量在新创建命令行窗口或重启电脑后就清除了，每次都要重设变量有些麻烦。而且如果你同时开发多个Flask程序，这个FLASK_ APP就需要在不同的值之间切换。**为了避免频繁设置环境变量**，我们可以使用python-dotenv管理项目的环境变量”

```
pipenv install python-dotenv
```

在项目根目录下分别创建两个文件:` .env` 和`.flaskenv`。

- `.flaskenv `用来存储和Flask相关的公开环境变量，比如FLASK_APP;
- `.env`用来存储包含敏感信息的环境变量，比如后面我们会用来配置Email服务器的账户名与密码。

在.flaskenv或.env文件中，环境变量使用键值对的形式定义，每行一个，以#开头的为注释

### 1.3.2 更多的启动选项

#### 使服务器外部可见

```
flask run --host=0.0.0.0
```

#### 改变默认端口

flask 的默认端口为： 5000

```
flask run --port=8000
```

###  1.3.3 设置运行环境

使用`FLASK_ENV`环境变量用来设置环境，默认为production。开发时可以切换为development

使用：`.flaskenv`：添加一行

```
FLASK_ENV = "development"
```

## 1.4 Python Sheel

这没什么好写的



## 1.5 Falsk 扩展

初始化过程：提供一个扩展类，实例化这个类，传入创建程序实例app作为参数

扩展会在传入的程序实例上注册一些处理函数，并加载一些配置

> 以某扩展实现了Foo 功能为例，这个扩展的名称将是Flask-Foo或Foo-Flask ;程序包或模
> 块的命名使用小写加下划线，即flask_ foo (即导人时的名称);用于初始化的类- -般为 Foo,实
> 例化的类实例一.般使用小写，即foo。初始化这个假想中的Flask-Foo扩展的示例如下所示:

```
from flask import Flask
from flask_foo import Foo

app=Flask(__name__)
foo = Foo(app)
```

## 1.6.项目配置

Flask中的配置变量就是一些大写的Python变量,通过`app.config`属性作为统一的接口来设置和获取

> 指向的是字典的子类

**加载配置方法**

1.  ```
   app.config['ADMIN_NAME']='Peter'
   ```

2. ```
   app.config.update(
   	TESTING = Ture,
   	SECRET_KEY = '_adasda'
   )
   ```

3. 存储在单独的python脚本,JSON文件,Python类中

**读取配置方法**

```
vlaue = app.config['ADMIN_NAME']
```

> 最好在程序实例app创建后就加载配置



##  ?1.7 URL与端点 可能是使用这个好匹配吧 不用一个一个改

如果`URL`都以硬编码的方式给出,那么会降低代码的易用性

使用Flask提供的`url_for()`获取`URL`,当路由中定义的`URL`规则被修改时,这个函数会返回正确的URL

> ? 这里不是很懂

调用url_for函数时候,第一个参数为端点值endpoint ,在Flask 中 endpoint 用来标记一个视图函数以及对应的URL规则

端点的默认值为视图函数的名称





## 1.8 Flask 命令

通过创建任意一个函数,并为其添加`app.cli.command()`装饰器,我们就可以注册一个flask命令 

```
@app.cli.command()
def hello():
    click.echo('Hello,Human!')
```

这里输入

```
flask hello 
```

click.echo(),可以在命令行界面输出字符

> PS: 这里会显示 "click" is not defined
>
> 在前面要加:import click

函数的名称:命令名称

若是使用`app.cli.command('say-hello')`,给装饰器传入参数来设置命令名称

## 1.9 模板与静态文件

模板文件存储在项目的根目录下的`templates`文件中

静态文件存储在项目的根目录下的`static`文件中

```
hello/
	- templates
	- static
	- app.py
```

## 1.10 Flask 与 MVC 架构

如果想要使用Flask来编写一个MVC 架构的程序，那么视图函数可以作为控制器（Controller)，视图（View）则是我们第3章将要学习的使用Jinja2渲染的HTML模板，而模型(Model）可以使用其他库来实现，在第5章我们会介绍使用SQLAlchemy来创建数据库.

## 章二 Flask 与 HTTP

## 2.1 请求响应循环

当用户访问一个URL，浏览器便生成对应的HTTP请求，经由互联网发送到对应的Web服务器。Web服务器接收请求，通过WSGI 将HTTP格式的请求数据转换成我们的Flask程序能够使用的Python数据。在程序中，Flask根据请求的URL执行对应的视图函数，获取返回值生成响应。响应依次经过WSGI转换生成HTTP响应，再经由Web服务器传递，最终被发出请求的客户端接收。浏览器渲染响应中包含的HTML和CSS代码，并执行JavaScript代码，最终把解析后的页面呈现在用户浏览器的窗口中.

## 2.2 HTTP 请求

```
http://helloflask.com/hello?name=Grey
```

`http://` :协议字符串，指定要使用的协议

`helloflask.com`:服务器地址

`/hello?name=Grey`:要获取的资源的路径

`?name=Grey`: 查询字符串: 从`?`开始,以键值对的形式写出,多个键值对之间使用`&`分隔

### 2.2.1 请求报文

### 2.2.2 Request 对象

```
from flask import Flask,request
```



```
@app.route('/hello')
def index():
    name = request.args.get('name','Flask') # 获取查询参数的值
    return '<h1>Hello,%s</h1>' %name        # 插入到返回值中
```

> 不应将用户传入的数据直接作为响应返回

### 2.2.3 在Flask中处理请求

#### 1. 路由匹配

#### 2. 设置监听的HTTP方法

#### 3. URL 处理

## 2.3 HTTP 响应

### 2.3.1 响应报文

### 2.3.2 在flask 中生成响应

 #### 1. 重定向

#### 2. 错误响应

### 2.3.2 响应格式



### 2.3.3 来一块 cookie





# 章五   数据库

## 5.3 使用 Flask-SQLAlchemy 管理数据库

> Alchemy 炼金术

实例化`Flask-SQLAlchemy` 提供的`SQLAlchemy`类 ，传入程序实例`app`，完成**初始化**

```
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app=Flask(__name__)

db = SQLAlchemy(app)
```



### 5.3.1 连接数据库服务器

要连接数据库服务器，首先要为我们的程序指定数据库`URI`

在`Flask-SQLAlchemy`里数据库URI 通过配置变量：`SQLALCHEMY_DATABASE_URI`

```
import os
...
app.config['SQLALCHEMY_DATABASE_URI'] = os.getenv('DATABASE_URL', prefix + os.path.join(app.root_path, 'data.db'))

```

### 5.3.2 定义数据库模型

所有的模型都继承自`Flask-SQLAlchemy`提供的`db.Model`类

```
# Models
class Note(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    body = db.Column(db.Text)
```

默认情况下，Flask-SQLAlchemy会根据模型类的名称生成一个表名称.

### 5.3.3 创建数据库和表

创建模型类后，我们需要手动创建数据库和对应的表，也就是我们常说的建库和建表。这通过对我们的db对象调用create_all()方法实现:

```
$flask shell
>>>from app import db
>>> db.create_all()
```

查看模型对应的SQL模式（建表语句）

