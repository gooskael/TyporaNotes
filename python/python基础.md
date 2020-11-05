[TOC]

### python常见问题

#### 注释

> 单行注释 #
>
> 多行注释 ''' '''  /  """ """
>
> ```python
> # 这是一个单行注释
> ```
>
> ```python
> '''这是一个多行注释'''
> """这是一个多行注释"""
> ```

#### 代码分行

> 对于列表、元组，有","可以直接换行继续写内容
>
> 对于一般代码，使用转义字符 \ 连接两行代码
>
> ```python
> list_example = ["a",
>                "b","c"]
> 
> if a == 10 or \
> b == 10:
>   print("RIGHT")
> ```

#### 遍历列表、元组等

```python
# 使用for循环
	#list
list_check = ["A","B","C","D","E"]
for item in list_check:
    print(item,end = ".")
	# tuple
tuple_check = ("A","B","C","D","E")
for word in tuple_check:
    print(word, end = ",")
    
# 遍历部分，切片
for item in list_check[:3]:
  print(item, end = ".")
```

#### print()函数

```python
# print函数默认调用后以\n结尾，即自动跳行
print("第一行")
print("第二行")
>> 
第一行
第二行

# 可以修改参数end
print("first", end = ',')
print("second", end = '.')
print("third")
>> first,second.third
```



### 变量

#### 变量命名规则

> - 变量名只能包含*字母*、*数字*和*下划线*
>- 变量名不能包含空格，最好使用小写字母，避免大写字母
> - 不要将python关键字和函数名用作变量名。

#### 文件夹命名

> 最好使用**小写字母**，并使用**下划线**来表示空格

#### 变量关键字表

```python
# 查看python关键字表
# print在python2中是关键字，在python3中是内置函数
import keyword
# keyword.kwlist #每输出一个关键字都会跳行
for i in keyword.kwlist:
  print(i,end=",")
```

```python
'False','None','True','and','as','assert','async','await','break','class','continue','def','del','elif','else','except','finally','for','from','global','if','import','in','is','lambda','nonlocal','not','or','pass','raise','return','try','while','with','yield'
```

#### 内置函数

[Python内置函数查询表——总结篇](https://blog.csdn.net/qdPython/article/details/99642060)

> 在python2里，print是属于关键字
>
> 在python3里，print是属于内置函数

#### 变量赋值

1. 单变量赋值
2. 变量操作
3. 多变量赋值

> ```python
> # 单变量赋值
> message = "hellow python"
> print(message)
> ```
>
> ```python
> # 变量操作
> message = "change the content" #直接对变量操作修改内容
> print(message)
> ```
>
> ```python
> # 多变量赋值
> a = b = c = 1
> print(a,b,c)
> # 分别赋值
> a, b, c = 1, 2, 'SAM'
> print(a,b,c)
> ```

### 字符串

#### 基本定义

1. 用引号括起来的都是字符串
2. 单双引号交替使用

> ```python
> # 单双引号并无差别，但是句子中使用引号的时候需要交叉使用
> print('single quotation mark')
> print("double quotation mark")
> print("double 'single'")
> ```
>
> ```python
> # 修改字符串大小写，并不改变原数据
> name = "i want to DO SOMETHING"
> print(name.title()) #每个单词首字母大写
> print(name.upper()) #全部字母大写
> print(name.lower()) #全部字母小写
> ```
>
> ```python
> # 拼接字符串
> first_name = 'STEPHEN'
> last_name = 'SAM'
> full_name = first_name + " " + last_name
> print(full_name)
> greeting = "Hello, " + full_name.title() + "!"
> print(greeting)
> ```
>
> ```python
> # 通过拼接，使一个句子里包含单双引号
> single_str = "'HEY'"
> double_str = '"Hey"'
> print("I want single " + single_str + " and double " + double_str)
> ```

#### 转义符、换行符 & 制表符

1. 转义符 和 反转义符

   ```python
   # 转义符 \
   # 反转义符 \\
   ```

2. 换行符

   ```python
   # 换行符 \n,跳行
   print("something\nanother")
   >> something
   >> another
   ```

3. 制表符

   ```python
   # 制表符 \t, t取table之意，每一个缩进取8个字符长度。
   ```

#### 删除字符串空白 -- 前/后

> 删除字符串的空白只能对字符串的首尾进行删除

##### 删除首部字符串空白使用lstrip()函数 l str ip

```python
# 删除空白函数只是对副本进行操作
lr_word = " python "
# 删除前空白
lr_word.lstrip()
>> 'python '
```

##### 删除尾部字符串空白使用rstrip()函数 rear str ip

```python
# 删除后空白
lr_word.rstrip()
>> ' python'
# 原字符串并没有修改
lr_word
>> 	' python '
```

##### 使用该两个函数都是对字符串的副本进行操作，对原字符串不会进行修改。如果需要对原字符串进行修改，要反赋值。

```python
# 反赋值修改原字符串
lr_word = lr_word.lstrip().rstrip()
lr_word
>> 'python'
```

#### 数字

##### 数字运算

1. 加减乘除 + - * /
2. 乘方 **
3. 向下取整 //
4. 取模（取余数）

```python
# //向下取整
-9 // 2 
>> -5
```

```python
# 整型相乘，结果为整型
2 * 2
>> 4
```

```python
# 整型相除，结果为浮点数
8 / 2
>> 4.0
```

##### 类型转换

1. 整型 int()
2. 浮点数 float()
3. 字符串 str()

```python
# 如果需要整型结果，需要类型转换
int(8 / 2)
>> 4
```

```python
# 如果需要浮点数结果，需要类型转换
2 * float(2)
>> 4.0
```

```python
# 转换成字符串 str()
age = 23
# message = "Happy " + age + " Birthday!" # 整型不能和字符串拼接
message = "Happy " + str(age) + " Birthday!"
message
```

##### 