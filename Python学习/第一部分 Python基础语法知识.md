



# 第一部分 Python基础知识
## 一、 变量与字符串（Variable & String）
### **<font size=4 color=red>1.1 变量</font>**

变量就是编程中最基本的存储单位，变量会暂时储存你放进去的东西。
 `answer = 42`
 “answer”为标识符，“=”为赋值符，“42”为值

* Python对大小写敏感，也就是“A”与“a”不是同一个变量。
* 变量的命名也很关键，主要有以下两种命名办法：
    * 驼峰式命名法
    * 帕斯卡命名法

### **<font size=4 color=red>1.2 print()函数</font>**
放入对象就能将结果打印的函数
* print()函数中，括号里边的为对象，如果对象是一个函数的话，不需要加引号；如果对象不是一个函数，则需要加引号。
* 学会合理运用print，在循环结束的时候可以用`print('done')`、`print('=============")`作为一个标识进行提示或区分。

### **<font size=4 color=red>1.3 字符串</font>**
在双引号或者单引号之间的文字，单双引号是完全一样的。

1. **字符串相加**
   正确示范

```python
what_he_does = ' plays '
his_instrument = 'guitar'
his_name = 'Robert Johnson'
artist_intro = his_name + what_he_does + his_instrument
print(artist_intro)
>>> Robert Johnson plays guitar
```
​		错误示范
```python
num = 1 
string = '1'
print(num + string)
>>>TypeError: unsupported operand type(s) for +: 'int' and 'str'
```
num是整数（integer），string是字符串（string），不同类型的数据不能进行合并。如果我不知道数据是什么类型，可以用type()函数，比如`print(type(word))`来查看函数类型。
对上面的进行修改，使之能运行。将string变成integer。
```python
num = 1 
string = '1' 
num2 = int(string)
print(num + num2)
>>> 2
```
2. **字符串相乘**

```python
words = 'words' * 3
print(words)
>>> wordswordswords
```
```python
word = 'a loooooong word'
num = 12
string = 'bang!'
total = string * (len(word) - num)
print(total)
>>> bang!bang!bang!bang!
```
```python
print(len(word))
>>> 16
```
3. **字符串的分片与索引**

```python
name = 'My name is Nike'
print(name[0])
print(name[-4]) #倒数第四个字符，不算零
print(name[11:14])
print(name[11:15])
print(name[5:])
print(name[:5])
>>> M
>>> N
>>> Nik
>>> Nike
>>> me is Nike
>>> My na
```
字符位置示意图

| Name =   | M    | y    |      | N    | a    | m    | e    |      | i    | s    |      | M    | i    | k    | e    |
| -------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Indexing | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   |
| Indexing | -15  | -14  | -13  | -12  | -11  | -10  | -9   | -8   | -7   | -6   | -5   | -4   | -3   | -2   | -1   |
<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**小游戏：找出你朋友中的魔鬼**</font>

```python
word = 'friends' #一定要加引号，否则显示没有定义
find_the_evil_in_your_friends = word[0] + word[2:4] + word[-3:-1]
print(find_the_evil_in_your_friends)
>>> fiend
```
4. **字符串的方法**
   Python是面向对象进行的编程语言，对象拥有各种特性、功能，专业术语称之为————方法。

**方法一：隐藏信息**

```python
phone_number = '1386-666-0006'
hiding_numeber = phone_number.replace(phone_number[:9],'*' * 9) #'*' * 9表示用9个*代替
print(hiding_numeber)
>>> *********0006
```
**方法二：搜索信息**

```python
search = '168'
num_a = '1386-168-0006'
num_b = '1681-222-0006'
print(search + ' is at ' + str(num_a.find(search) + 1 ) + ' to ' + str(num_a.find(search) + len(search)) + ' of num_a')
print(search + ' is at ' + str(num_b.find(search) + 1 ) + ' to ' + str(num_b.find(search) + len(search)) + ' of num_b')
print(num_a.find(search))
print(num_b.find(search))
>>> 168 is at 6 to 8 of num_a
>>> 168 is at 1 to 3 of num_b
>>> 5
>>> 0
```
5. **字符串格式化符**

```python
print('{} a word she can get what she {} for.'.format('With','came'))
print('{preposition} a word she can get what she {verb} for.'.format(preposition = 'With', verb = 'came'))
print('{0} a word she can get what she {1} for.'.format('With', 'came')) #谨记这种方式不需要对0和1赋值，0和1只是表示位置。
>>> With a word she can get what she came for.
>>> With a word she can get what she came for.
>>> With a word she can get what she came for.
```

### **<font size=4 color=red>1.4 字符串之间的相互转换</font>**

1. **bytes与string**

```python
#bytes object
b = b"example"
# str object
s = "example"
```

* str to bytes

  * 方法1：

  ```python 
  bytes(s, encoding = "utf8")
  ```

  示范：

  ```python
  b = b"example"
  s = "example"
  print(bytes(s, encoding = "utf8"))
  print(type(bytes(s, encoding = "utf8")))
  ```

  > b'example'
  > <class 'bytes'>

  * 方法2:

  ```python
  str.encode(s)
  ```

  ​	示范：

  ```python
  b = b"example"
  s = "example"
  print(str.encode(s))
  print(type(str.encode(s)))
  ```

  > b'example'
  > <class 'bytes'>	

* bytes to str

  * 方法1:

  ```python
  str(b, encoding = "utf-8")
  ```

  示范：

  ```python
  b = b"example"
  s = "example"
  print(str(b, encoding = "utf-8"))
  print(type(str(b, encoding = "utf-8")))
  ```

  > example
  > <class 'str'>

  * 方法2

  ```python
  bytes.decode(b)
  ```

  示范：

  ```python
  b = b"example"
  s = "example"
  print(bytes.decode(b))
  print(type(bytes.decode(b)))
  ```

  > example
  > <class 'str'>



## 二、函数（Function）

`print()`:放入对象将结果打印
`input()`：让用户输入信息
`len()`：测量对象长度
`int()`：将字符串类型的数字转换成整数类型的函数
Python官网中关于各个内置函数介绍的链接：[python内置函数介绍中文版](https://docs.python.org/zh-cn/3/library/functions.html)

### **<font size=4 color=red>2.1 创建函数</font>**

函数示例

```python
def function(arg1, arg2:
		return 'something'
```

含义介绍：
def：define，定义一个函数，是关键字。

function：函数名

arg：argument/parameter，参数

return：返回结果，是关键字

something：结果

-> Define a function named 'function' which has two arguments: arg1 and arg2, return the result ——'Something'.

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**摄氏度转化函数**</font>

```python
def fahrenheit_converter(C):
    fahrenheit = C * 9/5 +32
    return str(fahrenheit) + '℉'#计算结果类型是float，不能与字符串℉相合并，所以需要用str()函数进行转换
C2F = fahrenheit_converter(35)
print(C2F)
>>> 95.0℉
```
函数必须要有返回值
```python
def fahrenheit_converter(C):
    fahrenheit = C * 9/5 +32
    print(str(fahrenheit) + '℉')
C2F = fahrenheit_converter(35)
print(C2F)
>>> 95.0℉
>>> None
```
return作为关键字在函数中起了返回值的作用，而print只是在函数中展示给我们的打印结果，是为人类设计的函数。因此上面的95.0℉实际上是调用函数后产生的数值，是`print(str(fahrenheit) + '℉')`产生的结果，而`print(C2F)`则返回数值None，即什么都没有。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**重量转换器：g -> kg**</font>

```python
def quality_converter(g):
    return str(g/1000) + 'kg'
print(quality_converter(200000))
>>> 200.0kg
```
<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**求直角三角形斜边长的函数**</font>

```python
import math
def third_side_length(a,b):
    return "The right triangle third side's length is {}".format(math.sqrt(a * a + b * b))
print(third_side_length(3,4))
>>> The right triangle third side's length is 5.0
```
### <font size=4 color=red>2.2 传递参数与参数类型</font>

在已经设定好的函数中，我们通过打出函数的名称并向括号中传递参数实现对函数的调用（call）。比如：
`fahrenheit_converter(35)`
传递参数的方式：

* 位置参数 positional argument
* 关键词参数 keyword argument

1. **梯形面积函数：对位置参数和关键词参数的示范**

   <font size=3 color=**#3498DB**>**示例**</font>

   <font size=3 color=**#3498DB**>**梯形面积函数**</font>

```python
def trapezoid_area(base_up, base_down, height):
    return "The area of the trapezoid is {}".format(1/2 * (base_up + base_down) * height)
print(trapezoid_area(1,2,3))
#调用函数时，直接输入对应数字，1,2,3分别对应base_up, base_down, height，这种传入参数的方式称为位置参数
print(trapezoid_area(base_up = 1, base_down = 2, height = 3))
#调用函数时，在参数名称后面赋值，这种传入参数的方式称为关键词参数
print(trapezoid_area(1, 2, height = 3))
#两个参数只能是位置参数在关键词参数后面时可以混用，其他形式则不可以混用。
>>> The area of the trapezoid is 4.5
```
2. **函数中的默认值设置**
   即在函数中给某个参数设定一个默认值（赋值），这个参数在函数运行中将不会变化。

```python
def trapezoid_area(base_up, base_down, height=3):
    return "The area of the trapezoid is {}".format(1 / 2 * (base_up + base_down) * height)
print(trapezoid_area(1,2))
>>> The area of the trapezoid is 4.5
```
### <font size=4 color=red>2.3 设计自己的函数</font>

1. **open与write函数**

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**open与write函数**</font>

```python
file = open('/Users/zebchau/Desktop/text.txt','w') 
#后面的'w'表示如果没有就在该路径创建一个有该名称的文本，有则追加覆盖文本内容。如果是'a'，则表示附加在后面，不覆盖。
file.write('hello, world')
```
2. **文本过滤器**

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**文本过滤器**</font>

```python
#设计函数：创建文件并写入内容  同时是敏感词过滤器的第一部分
def text_creat(name, msg): #定义函数的名称和参数
    desktop_path = '/Users/zebchau/Desktop/' #文件的桌面路径
    full_path = desktop_path + name + '.text' #文件的路径
    file = open(full_path,'w') #打开文件
    file.write(msg) #写入传入的参数msg，即要在文本中写入的内容
    file.close() #关闭文件
    print('Done') #提示程序执行完毕
text_creat('hello','hello world') #调用函数
#敏感词过滤
def text_filter(word, censored_word = 'lame', changed_word = 'Awesome'):
    return word.replace(censored_word, changed_word)
text_filter('python is lame!') #调用函数
#两个函数合并
def censored_text_create(name, msg):
    clean_msg = text_filter(msg) #将第一个函数传入的msg进行过滤并存储在clean_msg这个变量中
    text_creat(name,clean_msg) #将传入的name文件名和过滤好的文本clean_msg作为参数传入函数text_creat中
censored_text_create('try', 'lame! lame! lame!')
```
**附：Python中的数学运算规则**

| 符号 | 描述                                           | 实例(a = 10, b = 20)                             |
| ---- | ---------------------------------------------- | ------------------------------------------------ |
| +    | 加，两个对象相加                               | a+b 输出结果30                                   |
| -    | 减，两个对象相减                               | a-b 输出结果 -10                                 |
| *    | 乘，两个数相乘或是返回一个被重复若干次的字符串 | a*b 输出结果200                                  |
| /    | 除，x除以y                                     | b/a 输出结果2                                    |
| %    | 取模，返回除法的余数                           | b%a 输出结果0                                    |
| **   | 幂，返回x的y次幂                               | a**b 为10的20次方，输出结果100000000000000000000 |
| //   | 取整除，返回商的整数部分                       | 9//2输出结果4，9.0//2.0输出结果4.0               |



## 三、循环与判断（Loop & Judge）

### **<font size=4 color=red>3.1 逻辑控制与循环</font>**

1. **逻辑判断：True & False**
   布尔表达式：能够产生一个布尔值（True & False）的表达式。

```python
1 > 2                # False
1 < 2 <3             # True
42 != '42'           # True
'Name' == 'name'     # False
'M' in 'Magic'       # True
number = 12 
number is 12         # True
```
2. **比较运算（Comparison）**
   比较运算符，如果比较成立则返回True，不成立则返回False。

| 运算符 |               含义               |
| :----: | :------------------------------: |
|   ==   |    左右两边等值的时候返回True    |
|   !=   |     左右两边不相等时返回True     |
|   >    |    左边大于右边的时候返回True    |
|   <    |    左边小于右边的时候返回True    |
|   <=   | 左边小于或等于右边的时候返回True |
|   >=   | 左边大于或等于右边的时候返回True |

多条件比较

```python
middle = 5 
1 < middle < 10
```
变量的比较
```python
two = 1 + 1 
three = 1 + 3 
two < three
```
字符串比较
```python
'Eddie Van Helen' == 'eddie van helen'
```
函数的比较
```python
abs(-10) > len('length of this word')
#结果等价于10 > 19
```
注：abs()是一个会返回输入参数绝对值得函数。

3. **比较运算的一些小问题**

* 不同类型的对象不能使用“<，>，<=，>=”进行比较，但可以使用“==”，“!=”进行比较。
```python
42 > 'the answer'   无法比较
 42 == 'the answer' #False 
 42 != 'the answer' #True
```

* 浮点和比较虽然是不同类型，但是不影响比较运算
```python
5.0 == 5    #True
3.0 > 1     #True
```
* 布尔类型比较
```python
True > False 
True + False > False + False
```
等价于：
```python
1 > 0
1 + 0 > 0 + 0
```
> Why？
> 因为True & False对计算机来说就相当于1 & 0。
* `1 <> 3` 等价于`1!=3`

4. **成员运算符与身份运算符（Membership & Identify Operators）**

* in & not in
in & not in 是表示归属关系（Membership Operators）的布尔运算符。
成员运算符与身份运算符的关键词是 in 和 is，把 in 放在两个对象中间的含义是测试前者是否存在于后面的集合中。
字符串、浮点、整数、布尔类型、变量，甚至是另一个列表都可以储存在列表中，列表是非常实用的数据结构。
```python
album = ['Black Star', 'David Bowie', 25, True]
album.append('new song')
print(album[0], album[-1])
>>> Black Star new song
'Black Star' in album
>>> True
```
in 后面是一个集合形态的对象，字符串满足这种集合的特性，所以用 in 来测试。

* is & is not
is & is not 是表示身份鉴别（Membership Operators）的布尔运算符。
在Python中任何一个对象都要满足身份（Identity）、类型（Type）、值（Value）这三个点，缺一不可。is 操作符号就是来进行身份比对的。
```python
the_Eddie = 'Eddie' 
name = 'Eddie' 
the_Eddie == name     #True
the_Eddie is name     #True
```
当两个变量一致时，经过 is 对比后会返回 True。
Python中任何对象都可以判断其布尔值，除了 0、None 和多有空的序列与集合（列表、字典、集合）布尔值为 False 外，其他的都为 True ，我们可以使用函数 bool（）进行判别：
```python
bool(0)            #False
bool([])           #False
bool('')           #False
bool(False)        #False
bool(None)         #False
```
5. **布尔运算符（Boolean Operators）**
   and、or用于布尔值之间的运算，具体规则如下：

| 运算符  | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| not x   | 如果 x 是 True，则返回 False，否则返回 True                  |
| x and y | and 表示“并且”，如果 x 和 y 都是True，则返回 True；如果 x 和 y 都是 False，则返回 False |
| x or y  | or 表示“或者”，如果 x 和 y 有其中一个是True，则返回 True；如果 x 和 y 都是 False，则返回 False |

and、or经常用于处理复合条件，类似于1<n<3，也就是两个条件同时满足。

```python
1 < 3 and 2 < 5    #True
1 < 3 and 2 > 5    #False
1 < 3 or 2 > 5     #True 
1 > 3 or 2 > 5     #False
```
### **<font size=4 color=red>3.2 条件控制</font>**

* **if...else**

```python
if condition:
    do something
else:
    do something
```

if...else：如果...条件是成立的，就执行...；反之，就执行...
条件（condition）是指返回值为 True 的布尔表达式。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**登陆函数**</font>

```python
def account_login(): #定义函数，并不需要参数
    password = input('password') #使用input获得用户输入的字符串并储存在变量password中
    if password == '12345':
        print('Login success')
    else:
        print('Wrong password or invalid input') #打印错误提示
        account_login() #运行函数
account_login() #调用函数
```

也可以像下面这样，适用于 if 后面的布尔表达式过长或者难于理解。这种情况下，可以给变量赋值来储存布尔表达式返回的布尔值 True 或 False。
```python
def account_login():
    password = input('password:') 
    password_correct = password == '12345'  #HERE
    if password_correct: 
        print('Login success!')
    else:
        print('Wrong password or invalid input!')
        account_login() #运行函数
account_login() #调用函数.注意运行函数和调用函数不同，运行函数实是在对函数进行运行，而调用函数则是面向终端的。
```

* **if...elif...else**

```python
if condition_1:
    do something_1
elif condition_2:
    do something_2
else:
    do something_3
```

if...elif...else：如果condition_1条件是成立的，就执行something_1；如果不成立，就往下运行；如果condition_2条件是成立的，就执行something_2；如果不成立，就执行something_3。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**登陆函数增加密码重置功能**</font>

```python
password_list = ['name', '12345'] #创建列表，存储用户名、密码等信息
def account_login():
    password = input('Password:') #利用input获得用户输入的字符串并存储在变量password中
    password_correct = password ==password_list[-1] #当用户输入的密码等于密码列表中最后一个元素的时候，即用户最新设定的密码，登录成功
    password_reset = password == password_list[0] #用户密码输入错误，重置密码，并储存值列表的最后一个，成为新的密码
    if password_correct:
        print('Login Success')
    elif password_reset:
        new_password = input('Enter a new password:')
        password_list.append(new_password)
        print('Your password has changed succesfully') #密码输入错误并调用函数，再次输入密码
        account_login() #注意，由于密码输入错误，再次调用函数
    else:
        print('Wrong password or invalid input!')
        account_login()
account_login()
```

### **<font size=4 color=red>3.3 循环Loop</font>**

1. **for 循环**

```python
for item in iterable:
    do something
```

for...in...：于...其中的每一个元素，做...事情。

for、in：关键字

item：元素

iterable：集合，可迭代的。for循环在可迭代的序列被穷尽的时候停止。

示范：

```python
for every_letter in 'hello world':
    print(every_letter)
```

运行结果如下:

> h
> e
> l
> l
> o
>
> w
> o
> r
> l
> d

示范：

```python
for num in range(1,11):
    print(str(num) + '+ 1 =', num + 1 )
```

运行结果如下:

> 1+ 1 = 2
> 2+ 1 = 3
> 3+ 1 = 4
> 4+ 1 = 5
> 5+ 1 = 6
> 6+ 1 = 7
> 7+ 1 = 8
> 8+ 1 = 9
> 9+ 1 = 10
> 10+ 1 = 11

示范：for 和 if 的结合

```python
songlist = ['Holy Diver', 'Thunderstruck', 'Rebel Rebel']
for song in songlist:
    if song == 'Holy Diver':
        print(song, 'Dio') #song就是上一句中的歌名
    if song == 'Thunderstruck':
        print(song, 'AC/DC')
    if song == 'Rebel Rebel':
        print(song, 'David Bowie')
```

运行结果如下:

> Holy Diver Dio
> Thunderstruck AC/DC
> Rebel Rebel David Bowie

2. **嵌套循环（Nested Loop）**

   嵌套循环：在一个循环里边再添加一个循环

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**九九乘法表**</font>

```python
for i in range(1,10):
    for j in range(1,10):
        print('{} X {} = {}'.format(i, j, i*j))
```

3. **while循环**

   for循环会在迭代的序列被穷尽的时候终止，while则是在条件不成立的时候终止。

```python
while condition:
    do something
```

while：关键字

condition：成立的条件

死循环（Infinite Loop）：while后面的表达式永远成立，程序无休止的运行下去。

```python
while 1 < 3:
    print('1 is smaller than 3')
```

运行结果是“1 is smaller than 3”，且无限输出。

使while循环停下来

* 使用软件中的停止运行功能

* 在循环过程中制造某种可以使循环停下来的条件。

```python 
count = 0 #赋值为零的原因在于计数
while True:
    print('Repeat this line !')
    count = count + 1
    if count == 5: #在什么条件下停下来
        break #在循环过程中制造某种可以使循环停止下来的条件
```

运行结果如下:

> Repeat this line !
> Repeat this line !
> Repeat this line !
> Repeat this line !
> Repeat this line !

* 改变循环成立的条件

```python
password_list = ['name', '12345'] #创建列表，存储用户名、密码等信息
def account_login():
    tries = 3
    while tries > 0:
        password = input('Password:') #利用input获得用户输入的字符串并存储在变量password中
        password_correct = password ==password_list[-1] #当用户输入的密码等于密码列表中最后一个元素的时候，即用户最新设定的密码，登录成功
        password_reset = password == password_list[0] #用户密码输入错误，重置密码，并储存值列表的最后一个，成为新的密码
        if password_correct:
            print('Login Success')
        elif password_reset:
            new_password = input('Enter a new password:')
            password_list.append(new_password)
            print('Your password has changed succesfully') #密码输入错误并调用函数，再次输入密码
            account_login() #注意，由于密码输入错误，再次调用函数
        else:
            print('Wrong password or invalid input')
            tries = tries - 1 #整个运行的条件是tries>0，所以计算使其小于或等于零
            print(tries, 'times left')
    else:
        print('Wrong password or invalid input')
        account_login()
account_login()
```

⚠️  `tries > 0`是在while循环内，而次数的计算`tries = tries - 1`是在 if 循环内。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**在桌面的文件夹中创建10个文本**</font>

```python
def text_creation():
    path = '/Users/zebchau/Desktop/w/' #注意路径后面要加/
    for name in range(1, 11):
        with open(path + str(name) + '.txt', 'w') as text:
            text.write(str(name))
            text.close()
            print('Done')
text_creation()
```

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**复利计算函数**</font>

```python
def invest(amount, rate, time):
    print("principal amount: {}".format(amount))
    for t in range(1, time + 1):
        amount = amount * (1 + rate)
        print("year {}: ${}".format(t, amount))
invest(100, .05, 8)
```

运行结果如下：

> principal amount: 100
>
> year 1: $105.0  
>
> year 2: $110.25
>
> year 3: $115.7625
>
> year 4: $121.55062500000001
>
> year 5: $127.62815625000002
>
> year 6: $134.00956406250003
>
> year 7: $140.71004226562505
>
> year 8: $147.74554437890632

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**打印1 ～ 100内的偶数**</font>

```python
def even_print():
    for n in range(1, 101):
        if n%2 == 0:
            print(n)
even_print()
```

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**小游戏：猜大小**</font>

```python
import random
#构造摇骰子的函数
def roll_dice(numbers = 3, points = None):
    print('<<<<< ROLL THE DICE! >>>>>') #告知用户开始摇骰子
    if points is None: #如果参数中并未指定points，那么为points创建空的列表
        points = []
    while numbers > 0:
        point = random.randrange(1, 7)
        points.append(point)
        numbers = numbers - 1
    return points #返回结果的列表
#将点数转化成大小
def roll_result(total):
    isBig = 11 <= total <= 18
    isSmall = 3 <= total <= 10
    if isBig:
        return 'Big'
    elif isSmall:  #相当于另一个if
        return 'Small'
#开始游戏函数
def start_game():
    print('<<<<< GAME STARTS! >>>>>')
    chioces = ['Big', 'Small'] #规定什么是正确输入
    your_chioce = input('Big or Small :') #将用户输入的字符串存储到your_chioce中
    if your_chioce in chioces:
        points = roll_dice() #调用roll_dice函数，将返回的列表命名为points。
        total = sum(points) #点数求和
        youWin = your_chioce == roll_result(total) #设定胜利的条件：所选结果和计算机生成的结果是一致的。
        if youWin:
            print('The points are', points, 'You WIN !')
        else:
            print('The points are', points, 'You LOSE !')
    else: #如果输入错误则重新开始
        print('Invalid Words')
        start_game()
start_game() #调用函数，使程序运行3
```

⚠️ 23行的choices是必须的，提供了选择的列表。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**小游戏：摇骰子赌输赢游戏**</font>

```python
#构造摇骰子的函数
import random
def roll_dice(numbers = 3, points = None):
    print('<<<<< ROLL THE DICE! >>>>>') #告知用户开始摇骰子
    if points is None: #如果参数中并未指定points，那么为points创建空的列表
        points = []
    while numbers > 0:
        point = random.randrange(1, 7)
        points.append(point)
        numbers = numbers - 1
    return points #返回结果的列表
#将点数转化成大小
def roll_result(total):
    isBig = 11 <= total <= 18
    isSmall = 3 <= total <= 10
    if isBig:
        return 'Big'
    elif isSmall:  #相当于另一个if
        return 'Small'
#开始游戏函数
def start_game():
    your_money = 1000
    while your_money > 0:
        print('<<<<< GAME STARTS! >>>>>')
        chioces = ['Big', 'Small'] #规定什么是正确输入
        your_chioce = input('Big or Small :') #将用户输入的字符串存储到your_chioce中
        if your_chioce in chioces:
            your_bet = int(input('How much you wanna bet ?  - '))
            points = roll_dice() #调用roll_dice函数，将返回的列表命名为points。
            total = sum(points) #点数求和
            youWin = your_chioce == roll_result(total) #设定胜利的条件：所选结果和计算机生成的结果是一致的。
            if youWin:
                print('The points are', points, 'You WIN !')
                print("You gained {}, you have {} now".format(your_bet, your_money + your_bet))
                your_money = your_money + your_bet
            else:
                print('The points are', points, 'You LOSE !')
                print("You lost {}, you have {} now".format(your_bet, your_money - your_bet))
                your_money = your_money - your_bet
        else: #如果输入错误则重新开始
            print('Invalid Words')
            start_game()
    else:
        print('GAME OVER')
start_game() #调用函数，使程序运行
```

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**手机号真伪测试**</font>



```python
def number_test():
    while True:
        number = input('Enter your number: ')
        CN_mobile = [134, 135, 136, 137, 138, 139, 150, 151, 152, 157, 158, 159, 182, 183, 184, 187, 188, 147, 178, 1705]
        CN_union = [130, 131, 132, 155, 156, 185, 186, 145, 176, 1709]
        CN_telecom = [133, 153, 180, 181, 189, 177, 1700]
        first_three = int(number[:3])
        first_four = int(number[:4])

        if len(number) == 11:
            if first_three or first_four in CN_mobile:
                print('Operator: China Mobile')
                print('We\'re sending verification code via text to your phone:',number)
                break #注意break，否则会造成无限循环。while True的时候尽量使用。
            elif first_three in CN_union:
                print('Operator: China Union')
                print('We\'re sending verification code via text to your phone:', number)
                break
            elif first_three in CN_telecom:
                print('Operator: China Telecom')
                print('We\'re sending verification code via text to your phone:', number)
                break
            else:
                print('No such a operator')
        else:
            print('Invalid length, your number should be in 11 digits')
    number_test() #number_test(),放在while对着和if对着均可
number_test()
```



## 四、数据结构（Data Structure）

### **<font size=4 color=red>4.1 数据结构（Data Structure)</font>**

Python的四种数据结构

```python
list = [val1, val2, val3, val4]    #列表
dict = {key1:val1, key2:val2}      #字典
tuple = (val1, val2, val3, val4)   #元组
set = {val1, val2, val3, val4}     #集合
```

⚠️ 字典的 key 与 val 必须一一对应。

### **<font size=4 color=red>4.2 列表（list)</font>**

1. **列表具有的特征**

* 特征1：列表中的每一个元素都是<font color=red >可变</font>的，意味着可以添加、删除和修改元素
* 特征2：列表中的元素是<font color=red >有序</font>的，也就是说每一个元素都有一个位置，可以通过输入而查询该位置对应的值

```python
Weekday = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(Weekday[0])
```

运行结果如下：

> Monday

* 特征3：列表可以<font color=red >容纳python中的任何对象</font>

```python
all_in_list = [
    1,                   #整数
    1.0,                 #浮点数
    'a word',            #字符串
    print(1),            #函数
    True,                #布尔值
    [1, 2],              #列表中套列表
    (1, 2),              #元组
    {'key':'value'}      #字典
]
```

2. **列表的增删改查**

* 列表元素的插入

  * 插入方法1

  ```python
  fruit = ['pineapple', 'pear']
  fruit.insert(1, 'grape') #1是插入指定元素之前的位置
  print(fruit)
  ```

  运行结果如下：

  > ['pineapple', 'grape', 'pear']

  * 插入方法2

  ```python
  fruit = ['pineapple', 'pear']
  fruit[0:0] = ['Orange']
  print(fruit)
  ```

  运行结果如下：

  > ['pineapple', 'grape', 'pear']

* 列表元素的添加

  * 添加方法1

  ```pyton
  fruit = ['pineapple', 'pear']
  fruit.extend('h')
  print(fruit)
  ```

  运行结果如下：

  > ['pineapple', 'pear', 'h']

  * 添加方法2

  ```python
  fruit = ['pineapple', 'pear']
  fruit.extend('hello') #五个字母分别添加，而不是作为一个单词进行添加
  print(fruit)
  ```

  运行结果如下：

  > ['pineapple', 'pear', 'h', 'e', 'l', 'l', 'o']

* 列表元素的删除

  * 删除方法1

  ```python
  fruit = ['pineapple', 'grape', 'pear']
  fruit.remove('grape')
  print(fruit)
  ```

  运行结果如下：

  > ['pineapple', 'pear']

  * 删除方法2

  ```python
  fruit = ['pineapple', 'grape', 'pear']
  del fruit[0:2] #列表范围中的数字都是包含前面不包含后面
  print(fruit)
  ```

  运行结果如下：

  > ['pear']

* 列表中元素的替换

```python
fruit = ['pineapple', 'grape', 'pear']
fruit[0] = 'pear_fruit'
print(fruit)
```

运行结果如下：

> ['pear_fruit', 'grape', 'pear']

* 列表中元素的索引与查找

```python
periodic_table = ['H', 'He', 'Li', 'Be','B', 'C', 'N', 'O', 'F', 'Ne']
print(periodic_table[0])
print(periodic_table[-2])
print(periodic_table[0:3])
print(periodic_table[-10:-7])
print(periodic_table[-10:])
print(periodic_table[:9])
```

运行结果如下：

> H
> F
> ['H', 'He', 'Li']
> ['H', 'He', 'Li']
> ['H', 'He', 'Li', 'Be', 'B', 'C', 'N', 'O', 'F', 'Ne']
> ['H', 'He', 'Li', 'Be', 'B', 'C', 'N', 'O', 'F']

错误示范

```python
periodic_table = ['H', 'He', 'Li', 'Be','B', 'C', 'N', 'O', 'F', 'Ne']
print(periodic_table['H']) 
```

运行结果如下：

> TypeError: list indices must be integers or slices, not str

这个错误说明，列表只接受位置索引，不接受查看某个具体元素所在的位置。若需查看某个具体元素所在的位置，需要使用字典功能。

### **<font size=4 color=red>4.3 字典（Dictionary）</font>**

1. **字典具有的特征**

* 特征1：字典中的数据必须是以键值对的形式出现的

```python
NASDAQ_code = {
    'BIDU':'Baidu',
    'SINA':'Sina',
    'YOKU':'Youku'
}
```

  错误写法：

```python
NASDAQ_code = {
    'BIDU':
}
```

```python
key_test = {[]:'a test'}
print(key_test)
```

* 特征2：逻辑上讲，键是不能重复的，而值可以重复

```python
a = {'key':123, 'key':123}
print(a)
```

* 特征3：字典中的键（key）是不可变的，也就是无法改变的；而值（value）是可变的，可修改的，可以是任何对象

2. **字典的增删改查**

* 字典中元素的增加

  * 增加方法1

  ```python
  NASDAQ_code = {
      'BIDU':'Baidu',
      'SINA':'Sina'
  }
  NASDAQ_code['YOKU'] = 'Youku' #注意是用方括号进行增加与删除。函数用(), 不是函数用[]。
  print(NASDAQ_code)
  ```

  运行结果如下：

  > {'BIDU': 'Baidu', 'SINA': 'Sina', 'YOKU': 'Youku'}

  * 增加方法2

  ```python
  NASDAQ_code = {
      'BIDU':'Baidu',
      'SINA':'Sina'
  }
  NASDAQ_code.update({'FB':'Facebook', 'TSLA':'Tesla'})
  print(NASDAQ_code)
  ```

  运行结果如下：

  > {'BIDU': 'Baidu', 'SINA': 'Sina', 'FB': 'Facebook', 'TSLA': 'Tesla'}

* 字典中元素的删除

```python
NASDAQ_code = {
    'BIDU':'Baidu',
    'SINA':'Sina',
    'FB':'Facebook',
    'TSLA':'Tesla'
}
del NASDAQ_code['FB']
print(NASDAQ_code)
```

运行结果如下：

> {'BIDU': 'Baidu', 'SINA': 'Sina', 'TSLA': 'Tesla'}

* 字典中元素的索引与查找

字典使用花括号，但在索引内容时仍然同列表一样使用方括号。放入方括号的是字典中的键，也就是说需要通过键来索引值。同时，字典也不能够切片。

```python
NASDAQ_code = {
    'BIDU':'Baidu',
    'SINA':'Sina',
    'FB':'Facebook',
    'TSLA':'Tesla'
}
print(NASDAQ_code['TSLA'])
```

运行结果如下：

> Tesla

### **<font size=4 color=red>4.4 元组（Tuple）</font>**

元组可以理解成一个稳固版的列表，因为元组是不可修改的。列表中存在的方法均不可使用在元组上，但是元组可以索引和查找，方法与列表一样。

```python
letters = ('a', 'b', 'c', 'd', 'e', 'f', 'g')
print(letters[0])
```

运行结果如下：

> a

### **<font size=4 color=red>4.5 集合（Set）</font>**

集合中的元素是无序的、不重复的任意对象，可以通过集合去判断数据的从属关系，也可以通过集合把数据结构中的重复元素减掉。集合不能被切片和索引。

* 集合中元素的添加

```python
a_set = {1, 2, 3, 4}
a_set.add(5)
print(a_set)
```

运行结果如下：

> {1, 2, 3, 4, 5}

* 集合中元素的删除

```python
a_set = {1, 2, 3, 4, 5, 6}
a_set.discard(5)
print(a_set)
```

运行结果如下：

> {1, 2, 3, 4, 6}

### **<font size=4 color=red>4.6 数据结构的一些技巧</font>**

1. **多重循环**

* 按照字母或者日期排序

```python
num_list = [6, 2, 7, 4, 1, 3, 5]
print(sorted(num_list))
```

运行结果如下：

> [1, 2, 3, 4, 5, 6, 7]

```python
alphabet_list = ['j', 's', 'r', 'h', 'd', 'a', 'v']
print(sorted(alphabet_list))
```

运行结果如下：

> ['a', 'd', 'h', 'j', 'r', 's', 'v']

```python
date_list = ['2019/2/3', '2017/5/3', '2020/7/2', '2030/6/3', '2027/2/4', '2019/3/3']
print(sorted(date_list))
```

运行结果如下：

> ['2017/5/3', '2019/2/3', '2019/3/3', '2020/7/2', '2027/2/4', '2030/6/3']

* 逆序整理

```python
num_list = [6, 2, 7, 4, 1, 3, 5]
print(sorted(num_list, reverse = True))
```

运行结果如下：

> [7, 6, 5, 4, 3, 2, 1]

* 两个列表的整理：遍历

  * 方法1

  ```python
  num = [7, 4, 9, 5, 0]
  str = ['hello', 'are', 'be', 'done', 'can']
  for a, b in zip(num, str):
      print(b, 'is', a)
  ```

  运行结果如下：

  > hello is 7
  > are is 4
  > be is 9
  > done is 5
  > can is 0

  * 方法2

  ```python
  num = [7, 4, 9, 5, 0]
  str = ['hello', 'are', 'be', 'done', 'can']
  print(sorted(num))
  print(sorted(str))
  for a, b in zip(num, str):
      print(b, 'is', a)
  ```

  运行结果如下：

  > [0, 4, 5, 7, 9]
  > ['are', 'be', 'can', 'done', 'hello']
  >
  > hello is 7
  > are is 4
  > be is 9
  > done is 5
  > can is 0

  * 方法3

  ```python
  num = [7, 4, 9, 5, 0]
  str = ['hello', 'are', 'be', 'done', 'can']
  n = 0
  for each in num:
      print(str[n], 'is', each )
      n += 1
  ```

  运行结果如下：

  > hello is 7
  > are is 4
  > be is 9
  > done is 5
  > can is 0

  **zip函数的扩展：**

  ```python
  name_list = ['张三', '李四', '王五']
  age_list = [54, 18, 34]
  print(zip(name_list, age_list))
  print(type(zip(name_list, age_list)))
  print(*zip(name_list, age_list))
  print(list(zip(name_list, age_list)))
  print(dict(zip(name_list, age_list)))
  ```

  运行结果如下：

  > <zip object at 0x10c79c840>
  > <class 'zip'>
  > ('张三', 54) ('李四', 18) ('王五', 34)
  > [('张三', 54), ('李四', 18), ('王五', 34)]
  > {'张三': 54, '李四': 18, '王五': 34}

  ⚠️ 可以看出，直接输出zip(list1, list2)返回的是一个zip对象, 在前面加上*， 它输出了三个元组， 正是两个列表中的三个数据一一对应的结果，我们可以将此对象直接转化成列表，甚至字典。

* 多个列表的整理

```python
list1 = [1, 2, 3, 4, 5]
list2 = ['a', 'b', 'c', 'd', 'f']
list3 = ['A', 'B', 'C', 'D', 'F']
for number, lowercase, capital in zip(list1, list2, list3):
    print(number, lowercase, capital)
```

运行结果如下：

> 1 a A
> 2 b B
> 3 c C
> 4 d D
> 5 f F

2. **推导式（List Comprehension）/ 列表解析式**

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**将十个元素装进列表中**</font>

普通写法：

```python
a = []
for i in range(1,11):
    a.append(i)
print(a)
```

运行结果如下：

> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

列表解析式写法：

```python
b = [i for i in range(1, 11)] 
print(b)
```

运行结果如下：

> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

列表解析式的理解

```python
list = [item for item in iterable] # for 前面是想要放在列表中的元素，后面是 for 循环表达式
```

列表解析式的效率更高，在 for 循环中可以尽量使用这种办法。

示例：

```python
i=1
j=2
a = [j**2 for i in range(1, 10)]
c = [j+1 for i in range(1, 10)]
k = [n for n in range(1, 10) if n%2 == 0]
z = [letter.lower() for letter in 'ASDFGHJKL']
print(a)
print(c)
print(k)
print(z)
```

运行结果如下：

> [4, 4, 4, 4, 4, 4, 4, 4, 4]
> [3, 3, 3, 3, 3, 3, 3, 3, 3]
> [2, 4, 6, 8]
> ['a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l']

示例：

```python
i=1
j=2
d = {i:i+1 for i in range(4)}
g = {i:j for i,j in zip(range(1, 6), 'abcde')}
h = {i:j.upper() for i,j in zip(range(1,6), 'abcde')}
print(d)
print(g)
print(h)
```

运行结果如下：

> {0: 1, 1: 2, 2: 3, 3: 4}
> {1: 'a', 2: 'b', 3: 'c', 4: 'd', 5: 'e'}
> {1: 'A', 2: 'B', 3: 'C', 4: 'D', 5: 'E'}

⚠️ 字典的推导方式略有不同，主要是要满足创建字典必须键值对应。

3. **循环列表时获取元素的索引**

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**索引时得到每个元素的具体位置**</font>

```python
letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
for num, letters in enumerate(letters):
    print(letters, 'is', num + 1)
```

运行结果如下：

> a is 1
> b is 2
> c is 3
> d is 4
> e is 5
> f is 6
> g is 7

**综合项目：词频统计**

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**词频统计**</font>

知识准备

```python
lyric = 'The night begin to shine, the night begin to shine'
words = lyric.split()
print(words)
```

运行结果如下：

> ['The', 'night', 'begin', 'to', 'shine,', 'the', 'night', 'begin', 'to', 'shine']

词频统计：

```python
path = '/Users/zebchau/Desktop/Walden.txt'
with open(path, 'r') as text:
    words = text.read().split()
    for word in words:
        print('{}-{} times'.format(word, words.count(word)))
```

运行结果如下:

> -1 times
> Walden-64 times
> Contents-1 times
> WALDEN-1 times
> 1.-1 times
> Economy-3 times
> 2.-1 times
> Where-10 times
> I-1989 times
> …...

结果没有按顺序排列，结果中有空格，标点符号等。

程序优化：

```python
import string
path = '/Users/zebchau/Desktop/Walden.txt'
with open(path, 'r') as text:
    words = [raw_word.strip(string.punctuation).lower() for raw_word in text.read().split()] #在文字的首位去掉连在一起的标点符号，并把首字母大写转化为小写。
    words_index = set(words) #将列表用set函数转化成集合，自动去除掉其中所有重复的元素
    counts_dict = {index:words.count(index) for index in words_index} #创建一个以单词为键（key）出现频率为值（value）的字典
    for word in sorted(counts_dict, key = lambda x: counts_dict[x], reverse = True): #key = lambda x，可理解为以字典中的值为排序的参数
        print('{} -- {} times'.format(word, counts_dict[word])) #打印整理好后的函数
```

运行结果如下：

> the -- 7346 times
> and -- 4602 times
> of -- 3492 times
> to -- 3107 times
> a -- 3033 times
> in -- 2060 times
> i -- 2011 times
> it -- 1715 times
> is -- 1336 times
> that -- 1336 times
> …...



## 五、类（Class）

类是有一系列有共同特征和行为事物的抽象概念的总和。

### **<font size=4 color=red>5.1 基本概念</font>**

```python
class CocaCola: #使用class定义一个类。类的变量称为类的属性。
    formula = ['caffeine', 'sugar', 'water', 'soda'] #formula就相当于可口可乐的配方，
```

使用 class 定义一个类，formula 列表中的内容就是类的变量，称之为类的属性（Class Attribute）。

1. **类的实例化（Instance）：**

在左边创建一个变量，右边写上类的名字，看起来像是赋值的行为，称之为类的实例化。

```python
coke_for_me = CocaCola() #要将其函数化
coke_for_you = CocaCola()
```

2. **类属性的引用（Attribute Reference）**

在类的名字后面输入`.`，IDE就会自动联想出我们之前在定义类的时候写在里面的属性，而这就是类属性的引用。类的属性会被所有类的实例共享，所以当在类的实例后面再点上`.`，索引的属性值是完全一样的。

```python
class CocaCola: 
    formula = ['caffeine', 'sugar', 'water', 'soda'] 
coke_for_me = CocaCola()
coke_for_you = CocaCola()
print(CocaCola.formula)
print(coke_for_me.formula)
print(coke_for_you.formula)
```

运行结果如下：

> ['caffeine', 'sugar', 'water', 'soda']
> ['caffeine', 'sugar', 'water', 'soda']
> ['caffeine', 'sugar', 'water', 'soda']

类的属性与正常的变量并无区别：

```
class CocaCola:
    formula = ['caffeine', 'sugar', 'water', 'soda'] 
coke_for_me = CocaCola() 
coke_for_you = CocaCola()
for element in coke_for_me.formula:
    print(element)
```

运行结果如下：

> caffeine
> sugar
> water
> soda

3. **实例属性（Instance Attribute）**

在创建了类之后，通过`object.new_attr`的形式进行一个赋值，于是我们就得到一个新的实例变量，实例的变量就是实例变量，而实例变量有一个专门的术语，称之为实例属性。

```python
class CocaCola:
    formula = ['caffeine', 'sugar', 'water', 'soda']
coke_for_China = CocaCola()
coke_for_China.local_logo = '可口可乐' #创建实例属性
print(coke_for_China.local_logo) #打印实例属性引用结果
```

运行结果如下：

> 可口可乐

理解：可口可乐的配方（formula）属于可口可乐（Class），而“可口可乐”的中文标识（local_logo）属于中国区的每一瓶可乐（Instance）。

4. **实例方法**

类的实例可以通过函数进行引用，我们把这种方式称为方法（Method）。方法是供实例使用的，因此我们还可以称之为实例方法（Instance Method）。

```python
class CocaCola:
    formula = ['caffeine', 'sugar', 'water', 'soda']
    def drink(self): #self参数就是被创建的实例本身
        print('Energy!')
coke = CocaCola()
coke.drink()
```

运行结果如下：

> Energy!

解释说明self参数就是被创建的实例本身，实际上并未起作用：

```python
class CocaCola:
    formula = ['caffeine','sugar','water','soda']
    def drink(coke):
        print('Energy!')
coke = CocaCola()
coke.drink()
```

运行结果如下：

> Energy!

一旦一个类被实例化，便可以使用与函数相似的方式：

```python
coke = CocaCola
coke.drink() == CocaCola.drink(coke) #左右两边写法完全一致
```

被实例化的对象会被编译器默默地传入后面方法的括号中，作为第一个参数。上面这两种方法是一样的，但是我们更多地会写成前面那种形式。其实`self`这个参数名称是可以随意修改名称的(编译器并不会因此而报错)，但是按照Python的规矩，我们还是统一使用`self`。

5. **更多参数**

和函数一样，类的方法也能有属于自己的参数。

```python
class CocaCola:
    formula = ['caffeine','sugar','water','soda']
    def drink(self, how_much):
        if how_much == 'a sip':
            print('Cool~')
        elif how_much =='whole bottle':
            print('Headache!')
ice_coke = CocaCola()
ice_coke.drink('a sip') #注意有变动
```

运行结果如下：

> Cool~

6. **类属性和实例属性的再讲解**

* 类属性被重新赋值，会影响到类属性的引用。

```python
class TestA:
    attr = 1
obj_a = TestA()
TestA.attr = 42
print(obj_a.attr)
```

运行结果如下：

> 42

* 实例属性被重新赋值，会影响到类属性的引用。

```python
class TestA:
    attr = 1
obj_a = TestA()
obj_b = TestA()
obj_a.attr = 42
print(obj_a.attr)
```

运行结果如下：

> 42

* 类属性和实例属性具有相同的名称，那么`.`后面引用的将是类属性。Why？

```python
class TestA:
    attr = 1
    def __init__(self):
        self.attr = 42
obj_a = TestA()
print(obj_a.attr)
```

运行结果如下：

>  42

### **<font size=4 color=red>5.2 `_init_`魔术方法</font>**

`_init_ ()`的神奇之赴就在于，如果你在类里定义了它，在创建实例的时候它就能帮你自动地处理很多事情
比如新增突例属性。`_init_ ()`是initialize(初始化)的缩写，这也就意味着即使我们在创建实例的时候不去引用`_init_ ()`方法，其中的命令也会先被自动地执行。

范例：

```python
class FooBar:
    def __init__(self):
        self.somevar = 42
f = FooBar() #构造方法的简化
print(f.somevar)
```

运行结果如下：

> 42

直接一步到位创建实例属性：

```python
class CocaCola:
    formula = ['caffeine','sugar','water','soda']
    def __init__(self):
        self.Local_logo = '可口可乐'

        def drink(self): #HERE
            print('Energy!')
            
coke = CocaCola()
print(coke.Local_logo)
```

运行结果如下：

> 可口可乐

而之前的方法是先定义完类再创建实例属性：

```python
class CocaCola:
    formula = ['caffeine', 'sugar', 'water', 'soda']
coke_for_China = CocaCola() #定义类
coke_for_China.local_logo = '可口可乐' #创建实例属性 
print(coke_for_China.local_logo) #打印实例属性引用结果
```

运行结果如下：

> 可口可乐

`_init_ ()`的方法给类提供了极大的灵活性：

```python
class CocaCola:
    formula = ['caffeine','sugar','water','soda']
    def __init__(self):
        for element in self.formula:
            print('Coke has {}!'.format(element))
        def drink(self):
            print('Energy!')
coke = CocaCola()
```

运行结果如下：

> Coke has caffeine!
> Coke has sugar!
> Coke has water!
> Coke has soda!

除了必写的self参数之外，`_init_ ()`同祥可以有自己的参数，同时也不需要这样`obj._ init_()` 的方式来调用（因为是自动执行）而是在实例化的时候往类后面的括号中放迸参数，相应的所有参数都会传递到到这个特殊的`_init_ ()`方法中，和函数的参数的用法完全相同。

```python
class CocaCola:
    formula = ['caffeine','sugar','water','soda']
    def __init__(self, logo_name):
        self.local_logo = logo_name #左边是变量作为类的属性，右边是传入的这个参数作为变量，也就是说这个变量的赋值所储存的结果将取决于初始化的时候所传进来的参数 logo_name ，传进来是什么 self.local_logo 就是什么。

        def drink(self):
            print('Energy!')

coke = CocaCola('可口可乐')
print(coke.local_logo)
```

运行结果如下：

> 可口可乐

### **<font size=4 color=red>5.3 类的继承</font>**

示例：

```python
class CocaCola:
    calories = 140,
    sodium = 45,
    total_carb = 39,
    caffeine = 34,
    ingredients = [
        'High Fructose Corn Syrup',
        'Carbonated Water',
        'Phosphoric Acid',
        'Natural Flavors',
        'Caramel Color',
        'Caffeine',
    ]
    def __init__(self, logo_name):
        self.local_logo = logo_name
    def drink(self):
        print('You got {} cal energy!'.format(self.calories))
        
class CaffeineFree(CocaCola):#在CaffeineFree后面的括号中放入CocaCola，表示这个类是继承于CocaCola父类的，而CaffeineFree则成为了CocaCola的子类。
    caffeine = 0
    ingredients = [
        'High Fructose Corn Syrup',
        'Carbonated Water',
        'Phosphoric Acid',
        'Natural Flavors',
        'Caramel Color'
    ]
    coke_a = CaffeineFree('CocaCola-Free') 
    coke_a.drink()
```



示例：

```python
class Animal(object):  #  python3中所有类都可以继承于object基类
   def __init__(self, name, age):
       self.name = name
       self.age = age

   def call(self):
       print(self.name, '会叫')
#现在我们需要定义一个Cat猫类继承于Animal，猫类比动物类多一个sex属性。
class Cat(Animal):
   def __init__(self,name,age,sex):
       super(Cat, self).__init__(name,age)  # 不要忘记从Animal类引入属性
       self.sex=sex

if __name__ == '__main__':  # 单模块被引用时下面代码不会受影响，用于调试
   c = Cat('喵喵', 2, '男')  #  Cat继承了父类Animal的属性
c.call()  # 输出 喵喵 会叫 ，Cat继承了父类Animal的方法
```

运行结果如下：

> 喵喵 会叫

### **<font size=4 color=red>5.4 类的扩展理解</font>**

python中任何对象都是类的实例，下面的这些类型被称作内建类型，并不需要实例化。

```python
obj1 = 1
obj2 = 'string'
obj3 = []
obj4 = {}
print(type(obj1), type(obj2), type(obj3), type(obj4))
```

运行结果如下：

>  <class 'int'> <class 'str'> <class 'list'> <class 'dict'>

```python
from bs4 import BeautifulSoup
soup = BeautifulSoup
print(type(soup))
```

运行结果如下：

> <class 'type'>

**Tips**：在编辑器中，按住cmd点击BeautifulSoup可以查看soup对象的完整定义。

