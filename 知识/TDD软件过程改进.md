[TOC]

### 0. 安装环境

1.[selenium 3+python3.6 for MacOS的配置](https://blog.csdn.net/dou_being/article/details/80155261)：安装python并且设置好环境变量为python3，source文件生效；下载selenium、firefox。参考本笔记文件的`python/0.安装与切换版本`。

```shell
$ python --version
python 3.8···
```

2.[在mac上安装geckodriver](https://blog.csdn.net/vulnerableyears/article/details/92016645)、[geckodriver下载地址](https://github.com/mozilla/geckodriver/releases)：在下载地址找到对应的系统版本将geckodriver下载下来之后，解压安装包得到可执行app`geckodriver`：`/Users/[localname]/Downloads/geckodriver`是解压之后的可执行app的路径：

```shell
$ cd /usr/local/bin
$ sudo cp /Users/[localname]/Downloads/geckodriver .
```

3.[安装django](https://www.jianshu.com/p/e57b57cef05e)：安装django。在安装之前首先检查一下`pip`是否会下载到`python3`的文件夹里（在切换了python版本并且source环境之后pip就会直接下载到python3的文件夹里）。

```shell
$ pip3 --version
>>> pip 21.0.1 from /Library/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages/pip (python 3.8)

$ pip3 install django
>>> ......(安装信息)

$ django-admin.py --version
>>> 3.1.7
```

****

### 1.开始构建测试项目

`TDD`文件夹为根目录：

1.`TDD/functional_tests.py`

2.`TDD/superlists`

#### 0.运行最简单的`functional_tests`：

```shell
cd TDD
touch functional_tests.py
```

```python
// functional_tests.py
from selenium import webdriver

browser = webdriver.Firefox()
browser.get('http://localhost:8000')

assert 'Django' in browser.title
```

​	打开一开始创建的py文件测试：

```shell
$ python functional_tests.py
```

#### 1.Django生成文件

​	-使用django生成一个文件`superlists`，本文件夹内会生成`superlists`和`geckodriver.log`；进入`superlists`，执行`manage.py`文件。

```shell
$ django-admin.py startproject superlists
```

​	-运行`TDD/superlists/manage.py`，可以获取测试过程产生的**logs** => 该窗口用作查看日志。

```shell
$ cd superlists
$ python manage.py runserver
```

​	-打开新窗口，测试`TDD/functional_tests.py`，同时可以看到日志窗口产生新logs

```shell
$ cd TDD
$ python functional_tests.py
```

#### 2.使用unittest运行`functional_tests`

​	将`TDD/functional_tests.py`修改成unittest方式

```python
from selenium import webdriver
import unittest

class NewVisitorTest(unittest.TestCase):
  def setUp(self):
    self.browser = webdriver.Firefox()
    
  def tearDown(self):
    self.browser.quit()
    
  def test_can_start_a_list_and_retrieve_it_later(self):
    self.browser.get('http://localhost:8000')
   	self.assertIn('To-Do', self.browser.title)
    self.fail('Finish the test!')

if __name__ == '__main__':
  unittest.main()
```

```shell
$ cd TDD
$ python functional_tests.py
```

#### 3.

****

### 2.测试解析url

#### 1.创建新的文件`lists`

​	在`TDD/superlists`目录底下创建新文件

```shell
$ cd TDD/superlists
$ python manage.py startapp lists
```

​	编写测试文件`TDD/superlists/lists/test.py`，测试最简单的断言`SmokeTest`；测试以`test_`为前缀。

```python
from django.test import TestCase

class SmokeTest(TestCase):
  def test_bad_maths(self):
    self.assertEqual(1+1, 3)
```

```shell
$ python manage.py test
```

#### 2.编写url解析的测试

​	编写`TDD/superlists/lists/test.py`，改为以下测试内容，会获得预期的失败：**home_page无法import**

```python
from django.urls import resolve
from django.test import TestCase
from lists.views import home_page

class HomePageTest(TestCase):
  def test_root_url_resolve_to_home_page_view(self):
    found = resolve('/')
    self.assertEqual(found.func, home_page)
```

```shell
$ python manage.py test
```

​	编写`TDD/superlists/lists/views.py`，并且修改完后重新运行，报错变更，确定需要修改的地方就是`view.py`文件。

```python
from django.shortcuts import render

home_page = None // 用来确认需要修改的地方
```

​	通过上面操作，进一步锁定`resolve`函数为下一步需要操作的地方，编写「用于整个站点映射功能」的文件`TDD/superlists/url.py`，并且把`TDD/superlists/lists/view.py`的`home_page`进行修改；运行之后可以返回OK的结果

```python
# url.py
from django.conf.urls import url
from lists import views

urlpatterns = [
  url(r'^$', views.home_page, name="home"),
]
```

```python
# view.py
from django.shortcuts import render

def home_page():
  pass
```

​	最后，在跑通了准备工作之后，继续编写一个网页测试用例，`TDD/superlists/lists/test.py`

```python
from django.urls import resolve
from django.test import TestCase
from django.http import HttpRequest

from lists.views import home_page

class HomePageTest(TestCase):
  def test_root_url_resolve_to_home_page_view(self):
    found = resolve('/')
    self.assertEqual(found.func, home_page)
    
  def test_home_page_returns_correct_html(self):
    request = HttpRequest()
    response = home_page(request)
    html = response.content.decode('utf8')
    self.assertTrue(html.startswith('<html>'))
    self.assertIn('<title>To-Do lists</title>', html)
    self.assertTrue(html.endswith('</html>'))
```









