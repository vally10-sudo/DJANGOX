14.5配置数据库

###配置数据库：
按以下格式在mysite/settings.py中设置DATABASES节点
DATABASES = {
    ‘default’:{
    ‘ENGINE’:’django.db.backends.mysql’,
    ‘NAME’ :’数据库名’,
    ‘USER’:’数据库用户名称’，
    ‘PASSWORD’:’数据库用户密码’
    ‘HOST’:’数据库所在主机名’
            }
}

###数据模型

修改polls/models.py文件完成模型代码如下：
#!/usr/bin/python
#-*- coding: UTF-8 -*-

import datatime
from django.db import models
from django.utils import timezone

class Question(models.Model):
    question_text = models.Charfield(max_length=200)
    pub_date = models.DateTimeField('date published')

    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)

    def_str_(self)
        return self.question_text

class Choice(models.Model):
    question = models.ForeignKey(Qestion, on_delete=models.CASCADE)
    choice_text = models.Charfield(max_length=200)
votes = models.Integerfield(default=0)

def _str_(self):
    return self.choice_text

    上面代码中每一个类就是一个Django 模型
    他们都继承来自django.db.models.Model类
    而模型的每一个属性都是Field类的实例，同时也对一个数据库表的字段

###添加应用程序
在polls/apps.py脚本中，按以下格式将应用程序名添加到INSTALLED_APPS节点：
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'polls.apps.PollsConfig',
]

from django.apps import AppConfig

class PollsConfig(AppConfig):
name = 'polls'

执行以下命令创建生成数据库的脚本：
python manage.py makemigrations polls

数据库脚本存放在polls/migrations/文件夹下 0001_initial.py

运行以下命令启动web服务
python manage.py runserver

打开polls/admin.py文件，添加以下代码：
from django.contrib import admin
from .models import Qestion
admin.site.register(Question)

前端页面：
1.首页--展示最新的调查问卷
2.详细页面----具体问卷展示页，不显示投票结果但可以进行投票
3.结果展示页--展示某一问卷调查结果
4.投票--处理某一次投票
Django 通过URL确定调用哪一个视图

polls/views.py中添加以下视图：
def detail(request, question_id):
    return HttpResponse("将为你打开问卷  %s。" % question_id)

def results(request):
    response = "正在查看问卷 %s的结果"
    return HttpResponse(response % question_id)

def vote(request,question_id):
    return HttpResponse("请为问卷 %s 提交您的答案" % question_id)

修改polls.urls文件，添加URL映射：
urlpatterns = {
    #ex: /polls/
    path('',views.index, name='index'),
    #ex: /polls/5/
    path('[int:question_id](int:question_id)/',views.detail, name='detail'),
    #ex: /polls/5/results/
    path('[int:question_id](int:question_id)/result/',views.results, name='result'),
    #ex: /polls/5/vote/
    path('[int:question_id](int:question_id)/vote/',views.vote, name='vote'),
}

Django 能够正常调用解析URL是因为在settings.py中设置了ROOT_URLCONF = 'mysite.urls'
当用户访问的URL包含polls时，Django会根据mysite.urls中的设置，跳转到polls.urls并进行验证，直到找到第一个匹配的URL为止。

下面修改index视图，使它返回最新的5条调查问卷：
from .models import Question
def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    output = ', '.join([q.question_text for q in latest_question_list])
    return HttpResponse(output)

业务逻辑和页面显示分离，在polls文件夹下创建一个新文件夹templates,
为了目录结构清晰，在templates文件夹下再创建一个polls文件夹，在polls下创建一个index.html文件
这个Index.html就是即将应用于Index视图的模板

将下面代码写入模板文件Index.html
{% if latest_question_list %}

<ul>
{% for question in latest_question_list %}
    <li><a href="/polls/{{ quesiton.id }}/">{{ question.question_text }}</a></li>
{% endfor %}
</ul>
{% else %}
<p>还没调查问卷！</p>
{% endif %}

接下来重新修改index视图：
from django.http import HttpResponse
from django.template import loader
from .models import Question

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list':latest_question_list,
    }
    return HttpResponse(template.render(context, request))

新视图会从模板文件夹下载模板文件并将一个字典对象传入视图

from django.shortcuts import render
def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)

from django.http import Http404
from django.shortcuts import render
from .models import Question

def detail(request, question_id)
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("问卷不存在")
    return render(request, 'polls/detail.html',{'question':question})

在polls文件夹下创建一个detail.html文件并作为detail视图的模板文件
模板内容暂时用{{question}}表示
datail.html 和 index.html在同一文件夹下

from django.shortcuts import get_object_or_404, render
def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question':question})

14.11.1 模板语法
将一下代码复制到模板文件detail.html中

<h1>{{ question.question_text }}</h1>
<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }}</li>
{%  endfor %}
</ul>

{{}}是django 模板语言的函数语法
采用英文句点的方式访问变量的属性
如{{question.question_text}}
其中question是视图通过字典形式传递给模板的变量，通过. 访问question的属性

模板中{% %}形式的代码是Django模板语言的函数语法

客户端请求web页面——>controller(url.py) 去调用view(views.py)视图——>view保存请求，向model获取数据——>model调用数据库，更新数据，获取数据返回给view——>view视图使用数据填充到模板templates(.html)中——>最后发送给web页面内容到客户端。

教程参考CSDN:https://edu.csdn.net/skill/python/python-3-137?a=python-2-6&typeId=17457

django admin用户和密码都是：ies173666

postgresql: 密码123456

连接数据库：

DATABASES = {

    'default': {

    # 'ENGINE': 'django.db.backends.sqlite3',

    # 'NAME': BASE_DIR / 'db.sqlite3',

    'ENGINE':'django.db.backends.postgresql_psycopg2',

    'NAME':'gx_day16',

    'USER':'postgres',

    'PASSWORD':'123456',

    'HOST':'',

    'PORT':'',

    }

}

~~file:///D:/postgresql/doc/postgresql/html/tutorial-agg.html~~

**3.输入python manage.py shell-->from  django.db import connection-->cursor = connection.cursor如果没有返回任何错误说明数据库连接成功，**

![1666699709009](image/新文字文件/1666699709009.png)

创建数据库：create database gx_day16;

查看数据库： \l

进入数据库： \c + 数据库名称


4.3.1 static 目录

在app目录下创建static文件夹。

![1666787244396](image/Django/1666787244396.png)

4.3.2 引入静态文件


5.模板语法

本质：在HTML中写一些占位符，由数据对这些占位符进行替换和处理
