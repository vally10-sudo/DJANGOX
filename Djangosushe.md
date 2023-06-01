# day15 初始django

## 1.安装

C:\Program Files\JetBrains\PyCharm 2019.1.1

## 2.创建项目

#### 2.1在终端

#### 2.2在pycharm---专业版才有

##### 特殊说明：

##### 默认项目的文件介绍：

mysite

manage.py----项目的管理，启动项目，创建APP，数据库管理--只是用

urls.py----URL和函数的对应关系，常常操作的文件

setting.py----项目的配置文件，链接数据库，哪个数据库，用户名，密码，读取，常操作（修改）

## 3.创建APP

-项目

    -app.用户管理（表结构、函数、HTML模板、CSS）

    -app.订单管理（表结构、函数、HTML模板、CSS）

    -app.后台管理（表结构、函数、HTML模板、CSS）

    -app.网站（表结构、函数、HTML模板、CSS）

    -app.API（表结构、函数、HTML模板、CSS）

..

注意：我们开发比较简洁，用不到多app，一般情况下，项目下创建1个app即可

├─app01
│  │  admin.py---固定，不用动，jango 提供admin后台管理功能
│  │  apps.py---固定，不用动--app启动类

models.py-----【重要】，操作数据库
│  │  tests.py---固定，不用动单元测试，不做
│  │  views.py---【重要】，函数
│  │  __init__.py
│  │
│  └─migrations
│          __init__.py
│
└─mytest
    │  asgi.py
    │  settings.py
    │  urls.py   【URL-函数】
    │  wsgi.py
    │  __init__.py
    │
    └─__pycache__
            settings.cpython-38.pyc
            __init__.cpython-38.pyc

## 4.快速上手

确保app已注册[settings.py]

![1662717755149](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1662717755149.png)

编写URL和视图函数的对应关系[urls.py]

![1662718507701](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1662718507701.png)

编写视图函数

![1662718653887](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1662718653887.png)

启动django 项目

命令行启动

python manage.py runserver

### 4.1再写一个页面

-url---函数

--函数

### 4.2    templates模板

![1662725173499](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1662725173499.png)

### 4.3 静态文件

在 开发过程中一般将：

图片

CSS

JS

都会当静态文件处理。

4.3.1 static目录

![1662728339197](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1662728339197.png)

4.3.2 引用静态文件

![1662728431653](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1662728431653.png)

#### 4.3.1 static目录

1.在app目录下创建static文件夹

![1663682085908](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1663682085908.png)

#### 4.3.2

![1663682183651](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1663682183651.png)

## 5.模板语法

本质上：在HTML中写一些占位符，由数据对这些占位符进行替换和处理

## 6.请求和响应

## 7.数据库操作

MySQL数据库 + pymysql

Django 开发操作数据库更简单，内部提供了ORM框架

7.1安装第三方模块

pip install mysqlclient

7.2 ORM

可以帮助我们做两件事情

创建，修改和删除数据库中的表（不用写SQL 语句，无法创建数据库）

操作表中的数据,不用写SQL 语句

insert into

update

select

1.自己创建数据库

启动MYSQ 服务

自带工具创建数据库

create database gx_day15 DEFAULT CHARSET utf8 COLLATE utf8_general_ci;

2.Django 连接数据库

在setting.py 文件中进行配置和修改

3.基于django 操作表

创建表

删除表

修改表

![1663772982091](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1663772982091.png)

4.操作表中的数据

```python
def orm(request):  
  
    #测试ORM操作表中的数据    ###### 1.新建 ######    # Department.objects.create(title="销售部")    # Department.objects.create(title="IT部")    # Department.objects.create(title="运营部")    #    # UserInfo.objects.create(name="刘备",password="123",age=99)    # UserInfo.objects.create(name="张飞", password="123", age=98)    # UserInfo.objects.create(name="关羽", password="123", age=97)  
  
    # ####  2.删除 #####  
    UserInfo.objects.filter(id=3).delete()            Department.objects.all().delete()  
  
    # 3.获取数据 #  
    # data_list = [对象---行，行，行] QuerySet 类型  
    # data_list = UserInfo.objects.all()    #  
    # for obj in data_list:  
    #     print(obj.id, obj.name, obj.password, obj.age)    #  
    # return HttpResponse("成功")  
    # data_list = UserInfo.objects.filter(id=1)  
  
    # 3.1获取第一条数据【对象】  
    # row_obj = UserInfo.objects.filter(id=1).first()  
    # print(row_obj.id, row_obj.name, row_obj.password, row_obj.age)  
  
    #    # 4.更新数据####  
    # UserInfo.objects.all().update(password=999)  
    # UserInfo.objects.filter(id=2).update(password=888)  
    return HttpResponse("成功")
```

# ##案例：用户管理的功能

## 1.展示用户列表

url

-函数

- 获取所有用户信息
- HTML渲染

## 2.添加用户

-url

-函数

- GET，看到页面，输入内容
- POST--提交，写入到数据库

## 3.删除用户

-url

-函数

http://127.0.0.1:8000/info/delete/?nid=1

http://127.0.0.1:8000/info/delete/?nid=2

http://127.0.0.1:8000/info/delete/?nid=3

def 函数(request):

    nid = request.GET.get("nid")

    UserInfo.objects.filter(id=nid).delete()

return HttpResponse("删除成功")

# Day16 Django 开发

主题：员工管理系统

登录

注销

modern form

美化

## 1.新建项目

## 2.创建app01

python manage.py startapp app01

![1665237118274](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1665237118274.png)

## 3.设计表结构

![1665327424588](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1665327424588.png)

```

```

```
from django.db import models

# Create your models here.

class Department(models.Model):
    """部门表"""
    title = models.CharField(verbose_name='标题', max_length=32)

class UserInfo(models.Model):
    """员工表"""
    name = models.CharField(verbose_name="姓名", max_length=16)
    password = models.CharField(verbose_name="密码", max_length=64)
    age = models.IntegerField(verbose_name="年龄")
    account = models.DecimalField(verbose_name="账户余额", max_digits=10, decimal_places=2, default=0)
    create_time = models.DateTimeField(verbose_name="入职时间")

    #无约束
    # depart_id = models.BigIntegerField(verbose_name="部门ID")

    #有约束

    # -to 与那张表关联
    # - to_field，表中那一列关联
    # 2.django 自动
    # 写的depart
    # 生成数据列 depart_id
    # 3.部门表被删除
    # 3.1 级联删除
    # depart = models.ForeignKey(to="Department", to_field="id",on_delete=models.CASCADE)
    # 3.2 置空

    # depart = models.ForeignKey(to="Department",to_field="id", null=True, blank=True, on_delete=models.SET_NULL)

    gender_choices = (
        (1,"男"),
        (2,"女"),
    )
    gender = models.SmallIntegerField(verbose_name="性别")


```

## 4.在MySQL中生成表

-工具连接MYSQL生成数据库

create database gx_day16 DEFAULT CHARSET utf8 COLLATE utf8_general_ci;

-修改配置文件，连接MySQL

```
DATABASES = {    'default': {        'ENGINE': 'django.db.backends.mysql',        'NAME': 'gx_day15',        'USER': 'root',        'PASSWORD': "123456",        'HOST': '127.0.0.1',        'PORT': 3306,    }}
```

![1665495616357](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1665495616357.png)

django 命令生成数据表

python manage.py makemigrations

python manage.py migrate

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1665496947689.png)

表结构创建成功：

![1665496972270](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1665496972270.png)

下面就是增删改查操作。

## 5.静态文件的创建和管理

static目录和templates目录

![1665498630614](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1665498630614.png)

1.先写URL

![1666101866301](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666101866301.png)

2.再写视图

![1666101924125](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666101924125.png)

3.再写HTML

![1666101967337](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666101967337.png)

![1666103309361](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666103309361.png)

![1666103371847](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666103371847.png)

![1666104203088](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666104203088.png)

1.从数据库取数据

![1666104673547](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666104673547.png)

2.展示到前端页面

![1666104722245](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666104722245.png)

进入列表页面添加跳转连接：

![1666186820809](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666186820809.png)

跳转到URL：

![1666186887871](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666186887871.png)

```python
from django.contrib import admin
from django.urls import path
# import django.contrib import admin
# import django.urls 
import path from app01 
import views
urlpatterns = [  
    # path('admin/', admin.site.urls),  
    path('depart/list/', views.depart_list),  
    path('depart/add/', views.depart_add),
]
```

再到视图函数：

![1666186952463](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666186952463.png)

```
from django.shortcuts import render
from app01 import models
# Create your views here.def depart_list(request):  

'''部门列表'''    # 取数据库中获取所有部门信息    # [对象,对象]  
queryset = models.Department.objects.all()  
return render(request, 'depart_list.html',{'queryset':queryset})
def depart_add(request):  
'''添加部门'''  
return render(request, 'depart_add.html')
```

再到页面：

![1666187005518](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666187005518.png)

```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
    <head>  
    <meta charset="UTF-8">  
    <title>Title</title>  
    <!--    <link rel="stylesheet" href="{% static 'plugins/bootstrap-3.4.1/css/bootstrap.css/bootstrap.min.css' %}">-->  
    <style>      
        .navbar{            border-radius: 0;        }  
    </style>
    </head>
    <body>
        <nav class="navbar navbar-default">  
            <div class="container">  
                <!-- Brand and toggle get grouped for better mobile display -->  
                <div class="navbar-header">    
                  
                    <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">      
                        <span class="sr-only">Toggle navigation</span>      
                        <span class="icon-bar"></span>      
                        <span class="icon-bar"></span>      
                        <span class="icon-bar"></span>    
                    </button>    
                    <a class="navbar-brand" href="#">联通用户管理系统</a>  
                </div>    <!-- Collect the nav links, forms, and other content for toggling -->  
                <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">    
                    <ul class="nav navbar-nav">      
                        <li><a href="/depart/list/">部门管理</a></li>      
                        <li><a href="#">Link</a></li>      
                        <li><a href="#">Link</a></li>    
                    </ul>    
                    <ul class="nav navbar-nav navbar-right">      
                        <li><a href="#">登录</a></li>      
                        <li class="dropdown">        
                            <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">vally 
                                <span class="caret"></span></a>        
                            <ul class="dropdown-menu">          
                                <li><a href="#">个人资料</a></li>          
                                <li><a href="#">我的信息</a></li>          
                                <li role="separator" class="divider"></li>          
                                <li><a href="#">注销</a></li>        
                            </ul>      
                        </li>    
                    </ul>  
                </div><!-- /.navbar-collapse -->  
            </div><!-- /.container-fluid -->
        </nav>
        <div>  
            <div class="container">      
                <div class="panel panel-default">        
                    <div class="panel-heading">          
                        <h3 class="panel-title">新建部门</h3>        
                    </div>        
                    <div class="panel-body">          
                        <form>            
                            <div class="form-group">              
                                <label>标题</label>              
                                <input type="text" class="form-control"  placeholder="标题" name="title" />            
                            </div>                
                            <button type="submit" class="btn btn-primary">提交</button>          
                        </form>        
                    </div>      
                </div>  
            </div>
        </div>
        <!--<script src="{% static 'js/jquery-3.6.1.min.js' %}"></script>--><!--<script src="{% static 'plugins/bootstrap-3.4.1/css/bootstrap.css/bootstrap.min.css'%}"></script>-->
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css">
        <script type="text/javascript" src="http://code.jquery.com/jquery-1.10.0.js"></script>
        <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/js/bootstrap.min.js"></script></body>
</html>
```

编辑urls: 最后一行：

![1666273934121](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666273934121.png)

编辑 views.py

![1666274014008](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666274014008.png)

编辑html

![1666274090039](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666274090039.png)

![1666274139294](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666274139294.png)

更新部门并提交数据库：

![1666275036649](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666275036649.png)

## 6.部门管理

体验---最原始的方法

Django 提供Form 和 ModelForm组件（方便）。

## 7.模板的继承

- 部门列表
- 添加部门
- 编辑部门

定义母版：

layout.html

```html
{% load static %}<!DOCTYPE html><html lang="en"><head>    <meta charset="UTF-8">    <title>Title</title><!--    <link rel="stylesheet" href="{% static 'plugins/bootstrap-3.4.1/css/bootstrap.css/bootstrap.min.css' %}">-->    <style>        .navbar{            border-radius: 0;        }    </style></head><body><nav class="navbar navbar-default">  <div class="container">    <!-- Brand and toggle get grouped for better mobile display -->    <div class="navbar-header">      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">        <span class="sr-only">Toggle navigation</span>        <span class="icon-bar"></span>        <span class="icon-bar"></span>        <span class="icon-bar"></span>      </button>      <a class="navbar-brand" href="#">联通用户管理系统</a>    </div>    <!-- Collect the nav links, forms, and other content for toggling -->    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">      <ul class="nav navbar-nav">        <li><a href="/depart/list/">部门管理</a></li>        <li><a href="#">Link</a></li>        <li><a href="#">Link</a></li>        <li><a href="#">Link</a></li>      </ul>      <ul class="nav navbar-nav navbar-right">        <li><a href="#">登录</a></li>        <li class="dropdown">          <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">vally <span class="caret"></span></a>          <ul class="dropdown-menu">            <li><a href="#">个人资料</a></li>            <li><a href="#">我的信息</a></li>            <li role="separator" class="divider"></li>            <li><a href="#">注销</a></li>          </ul>        </li>      </ul>    </div><!-- /.navbar-collapse -->  </div><!-- /.container-fluid --></nav><div>  {% block content %}  {% endblock %}</div><!--<script src="{% static 'js/jquery-3.6.1.min.js' %}"></script>--><!--<script src="{% static 'plugins/bootstrap-3.4.1/css/bootstrap.css/bootstrap.min.css'%}"></script>--><link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css"><script type="text/javascript" src="http://code.jquery.com/jquery-1.10.0.js"></script><script type="text/javascript" src="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/js/bootstrap.min.js"></script></body></html>
```

继承母版：

```html
{% extends 'layout.html' %}
{% block css %}  

<link rel="">
{% endblock %}

{% block content %}  
<h1>首页</h1>
{% endblock %}

{% js content %}  
<h1>首页</h1>
{% endblock %}
```

## 8.用户管理

insert into app01_userinfo(name,password,age,account,create_time,gender,depart_id) values("刘东","123",23,100.68,"2011-11-11",2,3);

insert into app01_userinfo(name,password,age,account,create_time,gender,depart_id) values("韩超","666",23,100.68,"2011-11-11",1,3);

insert into app01_userinfo(name,password,age,account,create_time,gender,depart_id) values("朱湖","999",23,100.68,"2011-11-11",1,4);

![1666622651559](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666622651559.png)

插入数据之后，现在的数据

![1666623125843](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666623125843.png)

insert into app01_department(title) values("IT部门"),("销售部");

### 显示用户列表

![1666707958794](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1666707958794.png)

此时model.py

```python
from django.db import models# Create your models here.class Department(models.Model):    """部门表"""    title = models.CharField(verbose_name='标题', max_length=32)class UserInfo(models.Model):    """员工表"""    name = models.CharField(verbose_name="姓名", max_length=16)    password = models.CharField(verbose_name="密码", max_length=64)    age = models.IntegerField(verbose_name="年龄")    account = models.DecimalField(verbose_name="账户余额", max_digits=10, decimal_places=2, default=0)    create_time = models.DateTimeField(verbose_name="入职时间")    #无约束    # depart_id = models.BigIntegerField(verbose_name="部门ID")    #有约束    # -to 与那张表关联    # - to_field，表中那一列关联    # 2.django 自动    # 写的depart    # 生成数据列 depart_id    # 3.部门表被删除    # 3.1 级联删除    depart = models.ForeignKey(to="Department", to_field="id",null=True, blank=True,on_delete=models.CASCADE)    # 3.2 置空    # depart = models.ForeignKey(to="Department",to_field="id", null=True, blank=True, on_delete=models.SET_NULL)    gender_choices = (        (1,"男"),        (2,"女"),    )    gender = models.SmallIntegerField(verbose_name="性别",choices=gender_choices)
```

此时views.py

```python
def user_list(request):    '''用户管理'''    # 获取所有用户列表[obj,obj]    queryset = models.UserInfo.objects.all()    """    #用python的方法来做的    for obj in queryset:        # print(obj.id, obj.name, obj.account, obj.create_time.strftime("%Y-%m-%d"), obj.gender, obj.get_gender_display())        # obj.gender  # 1,2        # obj.get_gender_display()  #get_字段名称_display()        obj.depart_id   #获取数据库中存储的哪个字段的名字        # xx = models.Department.objects.filter(id=obj.depart_id).first()        # xx.title        obj.depart.title  # 根据id自动去关联的表中获取那一行数据depart 对象        """    return render(request, 'user_list.html',{"queryset": queryset})
```

此时

user_list.html

```html
{% extends 'layout.html' %}{% block content %}<div class="container">    <div style="margin-bottom: 10px">        <a class="btn btn-success" href="/user/add/">            <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>            新建用户        </a>    </div>    <div class="panel panel-default">        <div class="panel-heading">            <span class="glyphicon glyphicon-th" aria-hidden="true"></span>            用户列表        </div>        <table class="table table-bordered">            <thead>            <tr>                <th>ID</th>                <th>姓名</th>                <th>密码</th>                <th>年龄</th>                <th>余额</th>                <th>入职时间</th>                <th>性别</th>                <th>所属部门</th>                <th>操作</th>            </tr>            </thead>            <tbody>            {% for obj in queryset %}            <tr>                <th> {{ obj.id }} </th>                <td> {{ obj.name }} </td>                <td> {{ obj.password }} </td>                <td> {{ obj.age }} </td>                <td> {{ obj.account }} </td>                <td> {{ obj.create_time|date:"Y-m-d" }} </td>                <td> {{ obj.get_gender_display }} </td>                <td> {{ obj.depart.title }} </td>                <td>                    <a class="btn btn-primary btn-xs" href="#">编辑</a>                    <a class="btn btn-danger btn-xs" href="#">删除</a>                </td>            </tr>            {% endfor %}            </tbody>        </table>    </div></div>{% endblock %}
```

### 新建用户

- 用原始的方式思路：不会采用（本质）麻烦

  ---数据校验

  ---错误，应该提示

  ---页面的每一个字段，都需要写入html。费劲

  ---关联的数据需要手动获取和循环展示在页面中

漏洞百出，自己要做的事情太多。

- django 组件
  - form组件（小简便）--只能做前三个事情+代码
  - modelForm最简便--- 最牛逼

### 8.1 初识Form

1.views.py

class MyForm(Form):

    user = forms.CharField(widget=form.Input)

    pwd = form.CharField(widget=form.Input)

    email = form.CharField(widget=form.Input)

def user_add(request):

    if request.method == "GET":

    form = MyForm()

    return render(request, 'user_add.html',{"form":form})

2.user_add.html

- --`<form method="post">`
  {{ form.user }}---自动给你生成input 标签
  {% for field in form %}
  {{ field }}
  {% endfor %}

```html
<!-- <input type="text" class="form-control" /> -->
```

</form>

### 8.2 ModelForm(增删改查--推荐的方法)

0.models.py

```python
class UserInfo(models.Model):    """员工表"""  
    name = models.CharField(verbose_name="姓名", max_length=16)  
    password = models.CharField(verbose_name="密码", max_length=64)  
    age = models.IntegerField(verbose_name="年龄")  
    account = models.DecimalField(verbose_name="账户余额", max_digits=10, decimal_places=2, default=0)  
    create_time = models.DateTimeField(verbose_name="入职时间")   
    #无约束    # depart_id = models.BigIntegerField(verbose_name="部门ID")  
    #有约束  
    # -to 与那张表关联  
    # - to_field，表中那一列关联  
    # 2.django 自动   
    # 写的depart  
    # 生成数据列 depart_id  
    # 3.部门表被删除  
    # 3.1 级联删除  
    depart = models.ForeignKey(to="Department", to_field="id",null=True, blank=True,on_delete=models.CASCADE)  
    # 3.2 置空  
    # depart = models.ForeignKey(to="Department",to_field="id", null=True, blank=True, on_delete=models.SET_NULL)  
    gender_choices = (        (1,"男"),        (2,"女"),    )  
    gender = models.SmallIntegerField(verbose_name="性别",choices=gender_choices)
```

1.views.py

class MyForm(ModelForm):

    class Meta:
		model = UserInfo

    fields = ["name","password","age"]

def user_add(request):

    if request.method == "GET":

    form = MyForm()

    return render(request, 'user_add.html',{"form":form})

2.user_add.html

- --`<form method="post">`
  {{ form.user }}---自动给你生成input 标签
  {% for field in form %}
  {{ field }}
  {% endfor %}

```html
<!-- <input type="text" class="form-control" /> -->
```

</form>

数据在页面中展示出来了。

```html
<!DOCTYPE html><html lang="en"><head>  
<meta charset="UTF-8">  
    <title>Title</title></head><body>  
    <form method="post">      
        {% csrf_token %}      
        {% for field in form %}          
        {{ field.label }}: {{ field }}      
        {% endfor %}  
    </form>
    </body>
</html>
```

modelform  在类一定义，前端就显示了。

加样式成功：

```
class UserModelForm(forms.ModelForm):    class Meta:        model = models.UserInfo        fields = ["name", "password", "age", 'account', 'create_time', "gender", "depart"]        widgets = {            "name": forms.TextInput(attrs={"class": "form-control"}),            "password": forms.PasswordInput(attrs={"class": "form-control"}),            "age": forms.TextInput(attrs={"class": "form-control"}),            "account": forms.TextInput(attrs={"class": "form-control"}),            "create_time": forms.TextInput(attrs={"class": "form-control"}),            # "gender": forms.TextInput(attrs={"class": "form-control"}),            # "depart": forms.TextInput(attrs={"class": "form-control"}),        }
```

加样式失败：

```
# def __int__(self, *args, **kwargs):#     super().__init__(*args, **kwargs)##     # 循环找到所有的插件，添加了 class = "form-control"#     for name, field in self.fields.items():#         field.widget.attrs = {"class": "form-control", "placeholder": field.label}
```

modelform 直接保存

```python
def user_model_form_add(request):  
    """添加用户，基于modelForm版本"""  
    if request.method == "GET":      
        form = UserModelForm()      
        return render(request, 'user_model_form_add.html', {"form": form})  
    # 用户通过POST提交数据，必须对数据进行校验，不允许为空  
    form = UserModelForm(data=request.POST)  
    if form.is_valid():      
        # 如果数据合法，保存到数据库      
        # print(form.cleaned_data)      
        # models.UserInfo.      
        form.save()      
        return redirect('/user/list/')  
    else:      
        print(form.errors)
```

利用modelsform 进行校验

```python
# #####modelform示例 #######
from django import forms
class UserModelForm(forms.ModelForm):  
    name = forms.CharField(min_length=3, label="用户名")
  
        form = UserModelForm(data=request.POST)
    if form.is_valid():
        # 如果数据合法，保存到数据库
        # print(form.cleaned_data)
        # models.UserInfo.
        form.save()
        return redirect('/user/list/')

# 校验失败，在页面上显示错误信息
    return render(request, 'user_model_form_add.html', {"form": form})
    # else:
    #     print(form.errors)
```

修改成中文校验

```
# LANGUAGE_CODE = 'en-us'
LANGUAGE_CODE = 'zh-hans'
TIME_ZONE = 'UTC'
USE_I18N = True
USE_L10N = True
USE_TZ = True
```

# Day17 Django 开发

- 部门管理
- 用户列表

  - 用户列表
  - 新建用户

    ModelForm,针对数据库中的某个表进行操作，对数据进行校验，HTML的标签，显示错误信息

    Form  -

### 8.4 编辑用户

点击编辑，跳转到编辑页面，将编辑的ID带过去

编辑页面，默认数据，根据ID获取并设置到页面中

提交

数据校验

错误提示

在数据库中更新

models.UserInfo.filter(id=4).update()

用modelform ,实现编辑功能：

```python
def user_edit(request,nid):  
    """编辑用户"""  
    row_object = models.UserInfo.objects.filter(id=nid).first()  
    if request.method == "GET":      
        # 根据ID取数据库获取要编辑的那一行数据      
        form = UserModelForm(instance=row_object)      
        return render(request, 'user_edit.html', {'form': form})  
    form = UserModelForm(data=request.POST, instance=row_object)  
    if form.is_valid():      
        form.save()      
        return redirect('/user/list/')  
    return render(request, 'user_edit.html', {"form": form})
```

很简单了。

8.5 删除

添加URLS

```python
# 用户管理
path('user/list/', views.user_list),
path('user/add/', views.user_add),
path('user/model/form/add/', views.user_model_form_add),
path('user/<int:nid>/edit/', views.user_edit),
path('user/<int:nid>/delete/', views.user_delete),
```

定义函数

```python
def user_delete(request, nid):  
models.UserInfo.objects.filter(id=nid).delete()  
return redirect('/user/list/')
```

### 9.靓号管理

#### 9.1 表结构

![1668000382407](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1668000382407.png)

根据表结构的需求，创建类（models.py中）。由类生成数据库中的表

```python
class PrettyNum(models.Model):  
    """靓号管理"""  
    mobile = models.CharField(verbose_name="手机号",max_length=11)   
    # 想要允许是空值，加  null=True, blank=True  
    price = models.IntegerField(verbose_name="价格", default=0)  
    level_choices = (      
        (1, "1级"),      
        (2, "2级"),      
        (3, "3级"),      
        (4, "4级"),  
    )  
    level = models.SmallIntegerField(verbose_name="级别",choices=level_choices, default=1)  
    status_choices = (      
        (1, "已占用"),      
        (2, "未使用"),  
    )  
    status = models.SmallIntegerField(verbose_name="状态", choices=status_choices, default=2)
```

运行：

(venv) D:\django\day160\myblog>***python manage.py makemigrations***
Migrations for 'app01':
  app01\migrations\0004_prettynum.py

    - Create model PrettyNum

(venv) D:\django\day160\myblog>***python manage.py migrate***
Operations to perform:
  Apply all migrations: admin, app01, auth, contenttypes, sessions
Running migrations:
  Applying app01.0004_prettynum... OK

![1668001591572](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1668001591572.png)

自己在数据库中创建一些数据：

![1668001536478](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1668001536478.png)

insert into app01_prettynum(mobile,price,level,status)values("13636363636",19,1,1);

![1668001874941](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1668001874941.png)

#### 9.2 靓号列表

#### URL

```python
urlpatterns = [    # path('admin/', admin.site.urls),    # 部门管理    path('depart/list/', views.depart_list),    path('depart/add/', views.depart_add),    path('depart/delete/', views.depart_delete),    # http://127.0.0.1:8000/depart/2/edit/    path('depart/<int:nid>/edit/', views.depart_edit),    # 用户管理    path('user/list/', views.user_list),    path('user/add/', views.user_add),    path('user/model/form/add/', views.user_model_form_add),    path('user/<int:nid>/edit/', views.user_edit),    path('user/<int:nid>/delete/', views.user_delete),    # path('user/delete/', views.user_delete),    # # http://127.0.0.1:8000/user/2/edit/    # path('user/<int:nid>/edit/', views.user_edit),  
    # 靓号管理  
    path('pretty/list/', views.pretty_list),
]
```

- 函数
  - 获取所有靓号
  - 结合html+render将靓号罗列出来
    - id  号码  价格  级别（chinese）  状态(chinese)

```python
def pretty_list(request):  
    """靓号列表"""  
    # select * from app01_prettynum order by level desc  
    queryset = models.PrettyNum.objects.all().order_by("-level")  
    return render(request, 'pretty_list.html',{"queryset":queryset})
```

前端页面：

```html
{% extends 'layout.html' %}{% block content %}
<div class="container">  
    <div style="margin-bottom: 10px">      
        <a class="btn btn-success" href="#">          
            <span aria-hidden="true" class="glyphicon glyphicon-plus"></span>            新建靓号      
        </a>  
    </div>    <
    div class="panel panel-default">      
    <div class="panel-heading">          
        <span aria-hidden="true" class="glyphicon glyphicon-th"></span>          
        用户列表      
    </div>      
    <table class="table table-bordered">          
        <thead>          
            <tr>              
                <th>ID</th>              
                <th>号码</th>              
                <th>价格</th>              
                <th>级别</th>              
                <th>状态</th>              
                <th>操作</th>          
            </tr>          
        </thead>          
        <tbody>          
            {% for obj in queryset %}          
            <tr>              
                <th> {{ obj.id }}</th>              
                <td> {{ obj.mobile }}</td>              
                <td> {{ obj.price }}</td>              
                <td> {{ obj.get_level_display }}</td>              
                <td> {{ obj.get_status_display }}</td>              
                <td>                  
                    <a class="btn btn-primary btn-xs" href="#">编辑</a>                  
                    <a class="btn btn-danger btn-xs" href="#">删除</a>              
                </td>          
            </tr>          
            {% endfor %}          
        </tbody>      
    </table>  
    </div>
</div>

{% endblock %}
```

主菜单增加靓号管理

```html
<!-- Collect the nav links, forms, and other content for toggling -->
<div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">  
    <ul class="nav navbar-nav">  
        <li><a href="/depart/list/">部门管理</a></li>  
        <li><a href="/user/list/">用户管理</a></li>  
        <li><a href="/pretty/list/">靓号管理</a></li>  
        <li><a href="#">库存管理</a></li>  
        <li><a href="#">数据可视化</a></li>  
    </ul>
```

9.3 新建靓号

 -列表页面点击跳转： /pretty/add/

 -URL

-ModelForm 类

from django import forms

class PrettyModelForm(forms.ModelForm):

...

 -函数


- 实例化类的对象
- 通过render将对象传入到HTML中
- 模板的循环展示所有字段
- 点击提交

  - 数据校验
  - 保存到数据库
  - 跳转回靓号列表

```python
def pretty_add(request):  
    """添加靓号"""  
    if request.method == "GET":      
        form = PrettyModelForm()      
        return render(request, 'pretty_add.html', {"form": form})  
    form = PrettyModelForm(data=request.POST)  
    if form.is_valid():      
        form.save()      
        return redirect('/pretty/list/')  
    return render(request, 'pretty_add.html', {"form": form})
```

验证手机号有两种方式：

1.正则表达式

```python
from django.core.validators import RegexValidator
from django.core.exceptions import ValidationError
class PrettyModelForm(forms.ModelForm):  
    # 验证方式1：正则表达式  
    mobile = forms.CharField(  
        label="手机号",validators=[RegexValidator(r'^1\d{10}$', '手机号格式错误')],    # )
  
```

2.钩子方法

```python
# 验证方式2 ： 钩子方法
def clean_mobile(self):  
    txt_mobile = self.cleaned_data["mobile"]  
    if txt_mobile != 11:      
        # 如果验证不通过，返回错误      
        raise ValidationError("格式错误")  
        # 通过，返回用户输入的值  
        return txt_mobile
```

#### 9.4 编辑靓号

- 列表页面：/pretty/数字/edit/
- URL
- 函数

  - 根据ID 获取当前编辑的对象
  - modelform配合，默认显示数据
  - 提交修改

修改URL:

```PYTHON
# 靓号管理
path('pretty/list/', views.pretty_list),
path('pretty/add/', views.pretty_add),
path('pretty/<int:nid>/edit/', views.pretty_edit),
```

修改views.py:

```python
class PrettyEditModelForm(forms.ModelForm):  
    mobile = forms.CharField(disabled=True, label="手机号")  
    class Meta:      
        model = models.PrettyNum      
        fields = ['mobile', 'price', 'level', 'status']  
        def __int__(self, *args, **kwargs):      
            super().__init__(*args, **kwargs)      
            # 循环找到所有的插件，添加了 class = "form-control"      
            for name, field in self.fields.items():          
                field.widget.attrs = {"class": "form-control", "placeholder": field.label}
                def pretty_edit(request, nid):  
                    """编辑靓号"""  
                    row_object = models.PrettyNum.objects.filter(id=nid).first()  
                    if request.method == "GET":      
                        form = PrettyEditModelForm(instance=row_object)      
                        return render(request, 'pretty_edit.html', {"form": form})  
                    form = PrettyEditModelForm(data=request.POST, instance=row_object)  
                    if form.is_valid():      
                        form.save()      
                        return redirect('/pretty/list/')  
                    return render(request, 'pretty_edit.html', {"form": form})
```

增加pretty_edit.html:

```html
{% extends 'layout.html' %}
{% block content %}
<div class="container">  
    <div class="panel panel-default">      
        <div class="panel-heading">          
            <h3 class="panel-title">编辑靓号</h3>      
        </div>        <div class="panel-body">          
        <form method="post" novalidate>              
            {% csrf_token %}              
            {% for field in form %}              
            <div class="form-group">                  
                <label>{{ field.label }}</label>                  
                {{ field }}                  
                <span style="color: red;">{{ field.errors.0 }}</span>                  
                <!--<input class="form-control" name="user" placeholder="姓名" type="text"/>-->              
            </div>              
            {% endfor %}              
            <button class="btn btn-primary" type="submit">提交</button>          
        </form>      
        </div>  
    </div>
</div>
{% endblock %}
```

![1668605581378](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1668605581378.png)

![1668605601272](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1668605601272.png)

 不允许手机号重复

添加：正则表达式；手机号不能存在

去数据查询一下，有的话，不能添加

```python

#[obj,obj,]
queryset = models.PrettyNum.objects.filter(mobile="13636363636")

obj = models.PrettyNum.objects.filter(mobile="13636363636").first()

# True/False

exists = models.PrettyNum.objects.filter(mobile="13636363636").exists()
```

编辑：正则表达式；手机号不能存在

排除自己以外，其他的数据是否手机号是否重复？

```
# id!=2 and mobile= '1363636636'

models.PrettyNum.objects.filter(mobile="13636363636").exclude(id=2)
```

#### 9.5 搜索手机号

```
models.PrettyNum.objects.filter(mobile="1999999999",id=123)

data_dict = {"mobile":"19999999","id":123}
models.PrettyNum.objects.filter(**data_dict)

支持两种不同的写法
```

```python
#第一种方法
models.PrettyNu.objects.filter(id=12)   # 等于12

models.PrettyNu.objects.filter(id__gt=12) # 大于12

models.PrettyNu.objects.filter(id__gte=12) # 大于等于12
models.PrettyNu.objects.filter(id__lt=12) # 小于12

models.PrettyNu.objects.filter(id__lte=12) # 小于等于12

# 第二种方法
data_dict = {"id_lte":12}
models.PrettyNum.object.filter(**data_dict)


```

```python
models.PrettyNum.objects.filter(mobile="999") #等于
models.PrettyNum.objects.filter(mobile__startswith="199") # 筛选出以199开头
models.PrettyNum.objects.filter(mobile__endswith="999")  # 筛选出以999结尾
models.PrettyNum.objects.filter(mobile__contains="199")  # 筛选出包含999


# 第二种方法
data_dict = {mobile__contains:"199"}
models.PrettyNum.object.filter(**data_dict)

# 我们使用包含，进行搜索功能的开发


```

![1669209908159](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1669209908159.png)

实现搜索框的功能：

前端：

```html
<div style="float: right;width:300px;">  
    <form method="get">      
        <div class="input-group">              
            <input type="text" name="q" class="form-control" placeholder="search for..." value="{{ search_data }}">              
            <span class="input-group-btn">                  
                <button class="btn btn-default" type="submit">                      
                    <span class="glyphicon glyphicon-search" aria-hidden="true">
                    </span>                  
                </button>              
            </span>      
        </div>  
    </form>
</div>
```

![1669732805476](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1669732805476.png)

![1669732858653](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1669732858653.png)

views.py

```python
def pretty_list(request):  
"""靓号列表"""  
data_dict = {}  
search_data = request.GET.get('q',"")  
if search_data:      
    data_dict["mobile__contains"] = search_data  
queryset = models.PrettyNum.objects.filter(**data_dict).order_by("-level")  
return render(request, 'pretty_list.html', {"queryset": queryset,"search_data": search_data})
```

#### 9.6 分页功能

创建三百条数据：

```python
def pretty_list(request):  
"""靓号列表"""  
for i in range(300):      
models.PrettyNum.objects.create(mobile="18188888818", price=10, level=1, status=1 )
```

创建完删除，此条命令

```python
queryset = models.PrettyNum.objects.all()
queryset = models.PrettyNum.objects.all()[0:10]
queryset = models.PrettyNum.objects.filter()[0:10]

# 第一页
queryset = models.PrettyNum.objects.all()[0:10]

# 第2页
queryset = models.PrettyNum.objects.all()[10:20]


# 第3页
queryset = models.PrettyNum.objects.all()[20:30]

data = models.PrettyNum.objects.all().count()
data = models.PrettyNum.objects.filter(id=1).count()

```

- 分页的逻辑和处理的规则
- 封装分页类
  - 从头到尾开发
  - 写项目直接用【pagination.py】-公共组件
  - 

![1671114071934](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1671114071934.png)

```python
# 1.根据用户想要访问的页码，计算出起止位置
page = int(request.GET.get('page', 1))
page_size = 10 
# 每页显示10条
start = (page - 1) * page_size
end = page * page_size
```

模块化分页功能：

![1671117301779](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1671117301779.png)

```python
"""
自定义的分页组件
以后如果想用这个分页组件，需要做如下几件事：
在视图函数中：

    def pretty_list(request):
  
        data_dict = {}
        search_data = request.GET.get('q', "")
        if search_data:
            data_dict["mobile__contains"] = search_data
        # res = models.PrettyNum.objects.filter(**data_dict)
        # print(res)
        # <QuerySet [<PrettyNum: PrettyNum object (6)>]>
        # q1 = models.PrettyNum.objects.filter(mobile="18989989909", id=6)
        # print(q1)
        #
        # data_dict = {"mobile": "18989989901", "id": 7}
        # q2 = models.PrettyNum.objects.filter(**data_dict)
        # print(q2)
  
        # select * from app01_prettynum order by level desc
        from app01.utils.pagination import Pagination
        # 1.根据自己的情况筛选自己的数据
        queryset = models.PrettyNum.objects.filter(**data_dict).order_by("-level")
        queryset = models.PrettyNum.objects.all
      
        # 2.实例化分页对象
        page_object = Pagination(request, queryset)
  
        context = {"queryset": page_object.page_queryset,# 分完页的数据
                   "search_data": search_data,
                   "page_string":page_object.html() #页码
                   }
        return render(request, 'pretty_list.html', context)

在HTML中
            {% for obj in queryset %}
                {{ obj.xx }}
            {% endfor %}
    <ul class="pagination">
        {{ page_string }}
    </ul>
"""
from django.utils.safestring import mark_safe

class Pagination(object):

    def __init__(self, request, queryset, page_size=10, page_param="page", plus=5):
        """
        :param request: 请求的对象
        :param queryset: 符合条件的数据
        :param page_size: 每页显示多少条数据
        :param page_param: 在URL中传递的获取分页的参数
        :param plus: 显示当前页的前或后几页（页码）
        """
        page = request.GET.get(page_param, "1")
        if page.isdecimal():
            page = int(page)
        else:
            page = 1
        self.page = page
        self.page_size = page_size

        self.start = (page - 1) * page_size
        self.end = page * page_size

        self.page_queryset = queryset[self.start:self.end]

        self.plus = plus

        # 数据总条数
        total_count = queryset.count()
        # 总页面
        total_page_count, div = divmod(total_count, page_size)
        if div:
            total_page_count += 1
        self.total_page_count = total_page_count

    def html(self):

        # 计算出，显示当前页的前5页和后5页

        if self.total_page_count <= 2 * self.plus + 1:
            # 数据库中数据小于11页时
            start_page = 1
            end_page = self.total_page_count
        else:
            # 数据库的数据大于11页

            # 当前页小于 5
            if self.page <= self.plus:
                start_page = 1
                end_page = 2 * self.plus + 1
            else:
                # 当前页 大于5
                # 当前页+5 大于总页数
                if (self.page + self.plus) > self.total_page_count:
                    start_page = self.total_page_count - 2 * self.plus
                    end_page = self.total_page_count
                else:
                    start_page = self.page - self.plus
                    end_page = self.page + self.plus

        # 页码
        page_str_list = []

        page_str_list.append('<li><a href="?page={}">首页</a></li>'.format(1))

        # 上一页
        if self.page > 1:
            prev = '<li><a href="?page={}">上一页</a></li>'.format(self.page - 1)
        else:
            prev = '<li><a href="?page={}">上一页</a></li>'.format(1)
        page_str_list.append(prev)

        # 页码
        for i in range(start_page, end_page + 1):
            if i == self.page:
                ele = '<li class="active"><a href="?page={}">{}</a></li>'.format(i, i)
            else:
                ele = '<li><a href="?page={}">{}</a></li>'.format(i, i)
            page_str_list.append(ele)

            # 下一页
        if self.page < self.total_page_count:
            prev = '<li><a href="?page={}">下一页</a></li>'.format(self.page + 1)
        else:
            prev = '<li><a href="?page={}">下一页</a></li>'.format(self.total_page_count)
        page_str_list.append(prev)
        page_str_list.append('<li><a href="?page={}">尾页</a></li>'.format(self.total_page_count))
        page_string = mark_safe("".join(page_str_list))
        return page_string

        """
                <li><a href="?page=1">1</a></li>
                <li><a href="?page=2">2</a></li>
                <li><a href="?page=3">3</a></li>
                <li><a href="?page=4">4</a></li>
                <li><a href="?page=5">5</a></li>

        """
```

小bug,搜索加分页情况下

```python
分页时候，保留原来的搜索条件
http://127.0.0.1:8000/pretty/list/?page=1
      
```

分页模块化，没成功

### 10.时间插件

```html
    <title>Title</title><!--    <link rel="stylesheet" href="{% static 'plugins/bootstrap-3.4.1/css/bootstrap.css/bootstrap.min.css' %}">-->        <link rel="stylesheet" href="static/plugins/bootstrap-3.4.1/css/bootstrap.css">        <link rel="stylesheet" href="static/plugins/bootstrap-datepicker/css/bootstrap-datepicker.css">    <style>
```

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css"><script type="text/javascript" src="http://code.jquery.com/jquery-1.10.0.js"></script><script type="text/javascript" src="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/js/bootstrap.min.js"></script><script src="static/plugins/bootstrap-datepicker/js/bootstrap-datepicker.js"></script><script src="static/plugins/bootstrap-datepicker/locales/bootstrap-datestrap-datepicker.zh-CN.min.js"></script>
<script>  
    $(funtion(){  
      $('#dt').datepicker({    
        format:'yyyy-mm-dd',    
        startDate:'0',    
        language:"zh-CN",    
        autoclose:true  
    })  })
</script>
```

没引入成功

### 11.ModelForm 和 BootStrao 样式父类

- modelForm 可以帮助我们生成html 标签。

但没有bootstrap的样式。

```python
class UserModelForm(forms.ModelForm):
   
    name = forms.CharField(
        min_length=3,
        label="用户名",
    )

    class Meta:
        model = models.UserInfo
        fields = ["name","password"]
form = UserModelForm()
```

```python
{{form.name}}   生成普通的input框，里面没有样式
{{form.password}}
```

- 定义插件

```
class UserModelForm(forms.ModelForm):
    class Meta:
        model = models.UserInfo
        fields = ["name","password"]
		widgets = {
			"name": forms.TextInput(attrs={"class":"form-control"}),
			"password": forms.PasswordInput(attrs={"class":"form-control"}),
		}

```

```python
class UserModelForm(forms.ModelForm):
   
    name = forms.CharField(
        min_length=3,
        label="用户名",
        widget=forms.TextInput(attrs={"class":"form-control"})
    )

    class Meta:
        model = models.UserInfo
        fields = ["name","password"]
form = UserModelForm()
```

```
{{form.name}}   以以上两种方案，可以带bootstrap 样式，但依然太繁琐了
{{form.password}}
```

- 重新定义init方法

  ```python
  class UserModelForm(forms.ModelForm):
   class Meta:
          model = models.UserInfo
          fields = ["name", "password", "age"]

      def __int__(self, *args, **kwargs):
           super().__init__(*args, **kwargs)

           # 循环找到所有的插件，添加了 class = "form-control"
           for name, field in self.fields.items():
                  #字段中有属性，保留原来的属性，没有属性，才增加。
               if field.widget.attrs:
               	field.widget.attrs["class"] = "form-control"
                  field.widget.attrs["placeholder"] = field.label
              else:
  				field.widget.attrs = {
                  	"class": "form-control", 
                   	"placeholder": field.label
               	}
  ```

  $$


  $$

  每有一个都要写，还是很麻烦：

  - 自定义一个类

  ```python
  class BootStrapModelForm(forms.ModelForm):      
      def __int__(self, *args, **kwargs):
           super().__init__(*args, **kwargs)

           # 循环找到所有的插件，添加了 class = "form-control"
           for name, field in self.fields.items():
                  #字段中有属性，保留原来的属性，没有属性，才增加。
               if field.widget.attrs:
               	field.widget.attrs["class"] = "form-control"
                  field.widget.attrs["placeholder"] = field.label
              else:
  				field.widget.attrs = {
                  	"class": "form-control", 
                   	"placeholder": field.label
               	}
  ```

```python
class UserEditModelForm(BootStrapModelForm):
 class Meta:
        model = models.UserInfo
        fields = ["name", "password", "age"]
```
