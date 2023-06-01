3.APP

-项目

* app:用户管理【表结构，函数，HTML,CSS]
* app:订单管理【表结构，函数，HTML,CSS]
* admin.py ---django 默认提供了admin后台管理
* apps.py ---固定不用动
* models.py ---重要，对数据库操作
* views.py  重要，函数

urls.py Url--函数

4.快速上手

确保app 已注册，在seting中,app-installed

![1666444392760](image/note/1666444392760.png)

编写URL 和视图函数的对应关系，urls.py

![1666444580844](image/note/1666444580844.png)

编写视图函数，views.py

![1666444691562](image/note/1666444691562.png)

启动django 项目

命令行启动

python manage.py runserver

4.1 再写一个页面

url-页面，函数

views--

安装Odoo步骤：

升级PIP:

pip install --upgrade pip -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install -r ./requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install psycopg2-binary -i https://pypi.tuna.tsinghua.edu.cn/simple

4.2 templates 模板

![1666700828253](image/note/1666700828253.png)

4.3 静态文件

在开发过程汇总一般将：

图片

CSS

js

![1666700709256](image/note/1666700709256.png)


3.图表

 -highchart,国外

 -echarts，国内，百度开源
