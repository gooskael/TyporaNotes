### 1. 开始构建测试项目

0.先创建一个py文件：

```python
// functional_tests.py
from selenium import webdriver

browser = webdriver.Firefox()
browser.get('http://localhost:8000')

assert 'Django' in browser.title
```

1.[selenium 3+python3.6 for MacOS的配置](https://blog.csdn.net/dou_being/article/details/80155261)：安装python并且设置好环境变量为python3，source文件生效；下载selenium、firefox。

2.[在mac上安装geckodriver](https://blog.csdn.net/vulnerableyears/article/details/92016645)、[geckodriver下载地址](https://github.com/mozilla/geckodriver/releases)：在下载地址找到对应的系统版本将geckodriver下载下来之后，解压安装包得到可执行app`geckodriver`：`/Users/[localname]/Downloads/geckodriver`是解压之后的可执行app的路径：

```shell
$ cd /usr/local/bin
$ sudo cp /Users/[localname]/Downloads/geckodriver .
```

2.1打开一开始创建的py文件测试：

```shell
$ python functional_tests.py
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

3.1使用django生成一个文件`superlists`，本文件夹内会生成`superlists`和`geckodriver.log`；进入`superlists`，执行`manage.py`文件。

```shell
$ django-admin.py startproject superlists
$ cd superlists
$ python manage.py
```

