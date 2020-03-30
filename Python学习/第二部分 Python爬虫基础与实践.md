# 第二部分 Python爬虫基础与实践

## 一、Python爬虫的准备工作

### **<font size=4 color=red>1.1 软件与终端的使用</font>**

1. **Pycharm软件的使用**

python -> xx.py

pycharm只是一个软件，是一python个解释器，通过提交程序代码，进行运行

pycharm中终端的作用是运行在pycharm中所写的代码

2. **终端运行程序**

在终端运营程序，必须要在对应的目录下运行，就是要找到文件路径

如何在没有pycharm时运行程序，在终端通过文件路径找到文件，然后执行文件，执行命令为：python XXX.py  （XXX.py)即为文件名。

* 终端使用命令

|     命令      |             执行内容             |
| :-----------: | :------------------------------: |
|      cd       | 切换文件夹、cd可以直接回到主目录 |
|      ls       |         展示文件夹中文件         |
| python XXX.py |      执行/运行 python 文件       |
|  mkdir XXXX   |    创建文件夹，XXXX为文件夹名    |
|     ls -a     |         展示一些隐藏文件         |
| touch XXX.py  |             创建文件             |
|  nano XXX.py  |          在终端编辑文件          |
|      cat      |      查看内容是否已经写进去      |
|   control+d   |       退出终端当前运行页面       |
|    quit()     |         退出终端当前程序         |
|     shell     | 通过指令和电脑进行交互，比如终端 |

3. **如何找到文件路径**

* 直接把文件拖到终端中就会显示路径
* pycharm中右键直接复制文件路径

### **<font size=4 color=red>1.2 Python函数类型</font>**

python能写出哪些函数类型？

1. bottle 用于包装/封装的函数

对两个函数进行封装：

```python
def one():
    pass
def two():
    pass
```

2. comput 用于计算的函数

* 死函数

```python
def do():
    pass
```

* 用于计算的函数会返回一些内容

  input -> func ->result， 函数一定要有输入和输出

```python
def do():
    return "something"
result = do()
print(do())
```

> something

```python
def do(things):
    return things + ' something'
result = do('hello')
print(result)
```

> hello something

3. 写不出包含新功能的函数

python看不懂别人的函数的情况：

* 语法上不明白
* 基于工程或者经验上的不解
* 业务上不明白



## 二、网页HTML知识

本章重要知识：

* autobro库
* 网页结构
* `from requests import Session`、`from bs4 import BeautifulSoup`的使用
* 网页中各种类型的识别及转化为`string`的技巧

### **<font size=4 color=red>1.1 网页基础</font>**

1. **网页html结构**

```python
from dominate.tags import * #意思是引出库里的所有函数
def part_one():
    with div() as root:
        button("click")
        for _ in range(3):
            li()
    return root

def part_two():
    with div() as root:
        span("nothing")

    return root

print(part_one()) #函数后面加括号是为了调用。
print(part_two())
```

> ```html
> <div>
>   <button>click</button>
>   <li></li>
>   <li></li>
>   <li></li>
> </div>
> <div>
>   <span>nothing</span>
> </div>
> ```

运行结果是html标签。

代码按照使用结构进行封装，分开的原因在于web中的领域要做可维护的html模板，能够在工程中最轻量地去维护，不会互相干扰。

2. **网页html请求**

在终端输入以下几个请求，结果不一样，但由于遵循了 http 协议，可以有不同的请求外观来得到不同的请求，所以都反映了网页结构。

* `curl`请求网页源代码、网页结构。实际上`curl`是一个非常有用的网站开发工具，有很多命令可以使用。

使用方法：

```python
curl website
```

示范：

```python
curl www.jd.com
```

> ```html
> <html>
> <head><title>302 Found</title></head>
> <body bgcolor="white">
> <center><h1>302 Found</h1></center>
> <hr><center>nginx</center>
> </body>
> </html>
> ```

* `http`请求网页源代码、网页结构。调用这个方法需要安装 httpie库。

使用方法：

```python
http website
```

示范：

```python
http www.jd.com
```

> ```html
> <html>
> <head><title>302 Found</title></head>
> <body bgcolor="white">
> <center><h1>302 Found</h1></center>
> <hr><center>nginx</center>
> </body>
> </html>
> ```

3. **autobro库**

<font size=3 color=**#3498DB**>**爬虫工具**</font>

<font size=3 color=**#3498DB**>**autobro库**</font>

```python
from pyppeteer import launch
import asyncio
import time

URL = "https://cn.bing.com/images/search?q=%E7%8C%AB&qs=n&form=QBIR&sp=-1&pq=%E7%8C%AB&sc=0-1&sk=&cvid=B885CF49C95C466D9FA914DB65AB4068"


async def main(url):
    now = str(time.time()).split(".")[1]
    browser = await launch(headless = False)
    page    = await browser.newPage()
    await page.goto(url)
    await page.waitFor(500)

    await page.screenshot(path=f"./{now}.png") #括号里的相当于是填进去的
    result = await page.content()
    await browser.close()
    return result

def fetch(target=URL):
    loop   = asyncio.get_event_loop()
    result = loop.run_until_complete(main(target))
    return result
```

使用方法：

```python
from autobro import fetch
result = fetch("http://www.example.com")
print(result)
```

⚠️ 使用别人的函数时，关注输入和结果，以及输入的类型和结果的类型。

⚠️ 显示没有autobro模板时，需要把 autobro.py 与 python 代码文件放在一个文件夹中。因为这个模板是手写的。

⚠️ 使用http协议获取网址的代码资料更快，一般情况下不使用autobro，直接使用http。再出现状况之后在使用autobro，作为一个备用。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**爬虫抢购网站**</font>

爬虫一个抢购网站，当页面出现“buy”或“go”时就立即下单。

```python
from autobro import fetch
result = fetch("https://daft.tech/buy")
print(result)
if buy in result:
    print('Go ahead and buy it!')
elif 'go' in result:
    print('go go')
else:
    print('Not yet hold on')
```

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**抢购：对京东网页进行截图**</font>

```python
from autobro import fetch
fetch('http://www.jd.com')
print(result)
```

> 结果为京东网页截图

此代码运行的结果是对京东页面的截图。实际上，这是在抢购中比较简单粗暴的一种策略：即当系统对页面截图的内容进行比对发生变化时就立即下单。一些抢购软件的原理就是这样，甚至抢购12306火车票的一些软件就是这样写出来的。

4. **网页结构解读**

* 不需要登录的基本上都是GET方法，比如：

```python
Request Method: GET
```

* 网页消息头相关知识：
  * [General headers](https://developer.mozilla.org/en-US/docs/Glossary/General_header): 同时适用于请求和响应消息，但与最终消息主体中传输的数据无关的消息头。
  * [Request headers](https://developer.mozilla.org/en-US/docs/Glossary/Request_header): 包含更多有关要获取的资源或客户端本身信息的消息头。Request Headers，Headers意思是增加一些额外的信息，来告诉网站这是谁，来自哪。比如accept language表示网站接受什么样的语言。User-Agent表示用哪个浏览器打开的。
  * [Response headers](https://developer.mozilla.org/en-US/docs/Glossary/Response_header): 包含有关响应的补充信息，如其位置或服务器本身（名称和版本等）的消息头。
  * [Entity headers](https://developer.mozilla.org/en-US/docs/Glossary/Entity_header): 包含有关实体主体的更多信息，比如主体长(Content-Length)度或其MIME类型。

* 如何调出网络消息头：

  打开网页后，分别执行：检查 > Network > 刷新页面 > Headers

* 查看访问地址

  消息头中的General > Request URL

* http协议

网站协议，http协议，根据网址就能够访问，而不需要进入搜索页面加搜索再进行访问。比如：`https://daft.website/result?from=北京&to=深圳&start=2019%2F03%2F12`，同时改变原文中的地址也能够访问。比如把深圳改为天津，也是一样能够访问的。这就是http协议较为方便的地方。

但凡符合http协议的网站，都可以通过curl实现对网页代码资料的请求。可以在终端实现。

在爬虫的时候要注意对网址的观察，这是爬虫极为重要的一步。网址的一般规范是：

```html
http [ flags ]  [ METHOD ]网址[ ITEM [ ITEM ]]
```

5. **Cookies、Session、Token、Sig**

主要作用在于鉴权

登陆之后，服务端保存Session，客户端保存Cookies，每一次的请求都会带着cookies，服务端session会判断是不是还在线，然后有权限进行操作。

Token，爬API时会发现有些网站或者APP时会用token进行鉴权。有些token会过期，有些不会过期。token是属于比较老的方式。

现在的App进行API访问时会有签名（sig），



### **<font size=4 color=red>1.2 简单的爬虫示范</font>**

爬虫机票订阅模拟网站：`https://daft.website/result?`

爬取整个网页html：

```python
from requests import Session
url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session() #Session() 类、对象，sesh就是Session的意思，随便取的。
# class in instance 实例
result = sesh.get(url) #OOP，面向对象，一组数据（这里是Session）OOP之后，OOP是针对不同状态下应该处理数据的模式和方式
print(result.content)#只要是对象就可以"."，所以这里result也是对象
print(type(result.content))
```

> b'<!DOCTYPE html>\n<html>\n  <head>\n    <title>Dominate</title><meta http-equiv="Content-Type" content="text/html; charset=utf-8" />\n    <link href="https://file-vlfxzgbkek.now.sh" rel="stylesheet">\n  </head>\n  <body class="bg-grey-light ">\n    <div class="flex flex-col container mx-auto w-1/2 ">       
>
> …...
>
> </div>\n      </div>\n    </div>\n  </body>\n</html>'
>
> <class 'bytes'>

打印出result.content发现是乱码，于是通过输入`print(type(result.content))`查看类型，发现类型是“bytes”，所以需要转换成“string”。

⚠️  Python中首字母大写就是类的意思，比如`sesh = Session()`。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**爬取机票模拟订阅网站的机票价格**</font>

<font size=3 color=**#7B7D7D**>**Step 1. 爬取整个网页html**</font>

```python
from requests import Session
from bs4 import BeautifulSoup

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session() #Session() 类、对象，sesh就是Session的意思，随便取的。
# class in instance
result = sesh.get(url)
print(result.text)
```

> ```html
> <!DOCTYPE html>
> <html>
>   <head>
>     <title>Dominate</title><meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
>     <link href="https://file-vlfxzgbkek.now.sh" rel="stylesheet">
>   </head>
>   <body class="bg-grey-light ">
>     <div class="flex flex-col container mx-auto w-1/2 ">
>       <div class="flex bg-white px-5 py-3 mb-1 h-24 items-center justify-between ">
>         <div>
>           <ul class="list-reset flex flex-col ">
>             <li>
>               <h5>中国国航CA1883</h5>
>             </li>
>             <li>
>               <span class="text-xs">波音 737-800(中型)</span>
>             </li>
>           </ul>
>         </div>
>  ......
> ```

解释soup对象是什么：

```python
from requests import Session
from bs4 import BeautifulSoup

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session() #Session() 类、对象，sesh就是Session的意思，随便取的。
result = sesh.get(url)

soup = BeautifulSoup(result.text,"html.parser") #放result参数，制定一个解析器
print(soup) #soup是一个对象
```

> ```html
> <html>
> <head>
> <title>Dominate</title><meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
> <link href="https://file-vlfxzgbkek.now.sh" rel="stylesheet"/>
> </head>
> <body class="bg-grey-light">
> <div class="flex flex-col container mx-auto w-1/2">
> <div class="flex bg-white px-5 py-3 mb-1 h-24 items-center justify-between">
> <div>
> <ul class="list-reset flex flex-col">
> <li>
> <h5>中国国航CA1883</h5>
> </li>
> <li>
> <span class="text-xs">波音 787-9(中型)</span>
> </li>
> </ul>
> </div>
>  ......
> ```

可以看出此时的soup对象与result.text所打印出来的soup对象并无实质区别，只是代码全部靠左对齐了。

<font size=3 color=**#7B7D7D**>**Step 2. 爬取所需资料html**</font>

```python
from requests import Session
from bs4 import BeautifulSoup

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session() #Session() 类、对象，sesh就是Session的意思，随便取的。
result = sesh.get(url)

soup = BeautifulSoup(result.text,"html.parser") #放result参数，制定一个解析器
result = soup.find_all("h3") #find_all是在全部网页html所有类中搜索，find是只搜索一个类。
print(result)
```

> ```html
> [<h3>10:30</h3>, <h3>8:27</h3>, <h3 class="text-orange mr-3">695</h3>, <h3>10:27</h3>, <h3>3:27</h3>, <h3 class="text-orange mr-3">1147</h3>, <h3>6:30</h3>, <h3>6:27</h3>, <h3 class="text-orange mr-3">804</h3>, <h3>10:23</h3>, <h3>8:30</h3>, <h3 class="text-orange mr-3">788</h3>, <h3>12:40</h3>, <h3>15:23</h3>, <h3 class="text-orange mr-3">733</h3>, <h3>7:40</h3>, <h3>8:40</h3>, <h3 class="text-orange mr-3">632</h3>, <h3>8:44</h3>, <h3>15:50</h3>, <h3 class="text-orange mr-3">588</h3>, <h3>15:44</h3>, <h3>3:44</h3>, <h3 class="text-orange mr-3">1164</h3>, <h3>10:27</h3>, <h3>8:23</h3>, <h3 class="text-orange mr-3">816</h3>, <h3>8:31</h3>, <h3>3:30</h3>, <h3 class="text-orange mr-3">798</h3>, <h3>8:31</h3>, <h3>6:30</h3>, <h3 class="text-orange mr-3">709</h3>, <h3>15:44</h3>, <h3>15:44</h3>, <h3 class="text-orange mr-3">884</h3>]
> ```

可以看到，打印出来的特征不够具体，运行结果包含了时间和价格，证明时间和价格都使用了`h3`标签。所以寻找某个值就要确定其特征，可以在代码页面用command+F筛选其特征，确保标签具有唯一性，可以通过添加类的方式进行。

筛选方式：`<h3 class="text-orange mr-3">1017</h3> `变成``h3.text-orange`进行搜索。

然后在编程中通过`"h3", class_ = "text-orange mr-3”`来执行编程中对此类的搜索。

<font size=3 color=**#7B7D7D**>**Step 3. 输出价格的html标签并获知其类型**</font>

```python
from requests import Session
from bs4 import BeautifulSoup

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session() #Session() 类、对象，sesh就是Session的意思，随便取的。
result = sesh.get(url)

soup = BeautifulSoup(result.text,"html.parser") #放result参数，制定一个解析器
result = soup.find_all("h3", class_ = "text-orange mr-3")
print(result)

for i in result:
    print(type(i))
```

`print(result)`的结果：

> ```html
> [<h3 class="text-orange mr-3">775</h3>, <h3 class="text-orange mr-3">559</h3>, <h3 class="text-orange mr-3">943</h3>, <h3 class="text-orange mr-3">894</h3>, <h3 class="text-orange mr-3">983</h3>, <h3 class="text-orange mr-3">914</h3>, <h3 class="text-orange mr-3">908</h3>, <h3 class="text-orange mr-3">614</h3>, <h3 class="text-orange mr-3">1244</h3>, <h3 class="text-orange mr-3">1117</h3>, <h3 class="text-orange mr-3">1072</h3>, <h3 class="text-orange mr-3">1067</h3>]
> ```

`print(type(i))`的结果：

> ```html
> <class 'bs4.element.Tag'>
>  ......
> ```

<font size=3 color=**#7B7D7D**>**Step 4. 输出价格**</font>

```python
from requests import Session
from bs4 import BeautifulSoup, element #注意加上element

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session()
result = sesh.get(url)

soup = BeautifulSoup(result.text,"html.parser")
result = soup.find_all("h3", class_ = "text-orange mr-3")

for i in result:
    assert isinstance(i, element.Tag) #注意这一句的语法
    price = i.get_text() #直接获取文字
    print(price)
```

> 644
> 574
> 884
> 999
> 1247
> 1154
> 714
> 568
> 591
> 1018
> 1111

⚠️ 由于 i 的类型是`<class 'bs4.element.Tag’>`，所以需要将其转化为string。

转化的技巧为：

1.直接在`from bs4 import BeautifulSoup`加上价格class的类型`<class 'bs4.element.Tag'>中的element `

2.在循环中添加``assert isinstance(i, element.Tag)`，注意`element.Tag`

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**爬取机票模拟订阅网站的机票价格的最大最小值**</font>

* 方法1

```python
from requests import Session
from bs4 import BeautifulSoup, element #注意加上element

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session()
result = sesh.get(url)

soup = BeautifulSoup(result.text,"html.parser")
result = soup.find_all("h3", class_ = "text-orange mr-3")

l = []
for i in result:
    assert isinstance(i, element.Tag)
    price = i.get_text() #直接获取文字。price是字符串,不能直接使用min、max求最大值
    l.append(int(price)) #把string转化成数字类型
    
print('机票价格最便宜的是{}。'.format(min(price)))
print('机票价格最贵的是{}。'.format(max(price)))
```

> 机票价格最便宜的是532。
> 机票价格最贵的是1786。

* 方法2:

```python
from requests import Session
from bs4 import BeautifulSoup, element #注意加上element

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session()
result = sesh.get(url)

soup = BeautifulSoup(result.text,"html.parser")
result = soup.find_all("h3", class_ = "text-orange mr-3")

price_list = []
for i in result:
    assert isinstance(i, element.Tag) #注意这一句的语法
    price =i.get_text() #直接获取文字
    list.append(price_list,price)
    
print(type(price_list)) #不能在for循环内，不然会输出一个递加的列表
print('机票价格最便宜的是{}。'.format(min(price_list)))
print('机票价格最贵的是{}。'.format(max(price_list)))
```

> <class 'list'>
>
> 机票价格最便宜的是798。
> 机票价格最贵的是1989。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**爬取机票模拟订阅网站的航空公司及对应的机票价格**</font>

```python
from requests import Session
from bs4 import BeautifulSoup, element #注意加上element

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12"
sesh = Session()
result = sesh.get(url)

soup = BeautifulSoup(result.text,"html.parser")

company = soup.find_all('h5')
company_list = []
for i in company:
    company = i.get_text()
    list.append(company_list, company)
    
price = soup.find_all("h3", class_ = "text-orange mr-3")
price_list = []
for i in price:
    assert isinstance(i, element.Tag)
    price = i.get_text()
    list.append(price_list, price)
    
####将company_list和price_list转化为字典格式
keys = company_list
values = price_list
dict = zip(keys, values)
for i in dict:
    print(i)
```

> ('中国国航CA1883', '854')
> ('东方航空MU5110', '614')
> ('东方航空MU5110', '996')
> ('东方航空MU5110', '523')
> ('东方航空MU5110', '874')
> ('南方航空CZ3907', '665')
> ('中国国航CA1883', '599')
> ('东方航空MU5110', '562')
> ('中国国航CA1883', '925')
> ('南方航空CZ3907', '1116')
> ('南方航空CZ3907', '1139')
> ('中国国航CA1883', '579')

⚠️ 如何实现字典中键值的一一对应



## 三、Python爬虫三步走

本章重要知识

* 使用`import time`防止高频访问IP被封
* 反爬网站使用autobro
* 高效的headers方法
* 针对网页结构变化的Selector方法的使用
* Selector方法一次抓取多个信息
* dataset库的使用
* DB Browser for SQLite数据库软件的安装及使用

### **<font size=4 color=red>3.1 认识Python爬虫三步走</font>**

1. 请求

web、构建header、条件判断、异常处理、循环

2. 解析

文本处理（洗数据）、循环、条件判断

3. 存储

数据结构、系统相关、循环、数据读写、条件判断

### **<font size=4 color=red>3.2 请求</font>**

1. **请求部分涉及的语法**

* 字符串拼接与字符串模板填充
* for loop & while loop
* condition test 条件判断
* data structure 数据结构

2. **字符串拼接与字符串模板填充**

* 字符串的拼接

对网址`https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12`进行拆分

```python
base = 'https://daft.website/result?'
start = 'from=%E5%8C%97%E4%BA%AC&'
dest = 'to=%E6%B7%B1%E5%9C%B3&'
date = 'start=2019%2F03%2F12'

from requests import Session
url = base + start + dest +date
result = Session().get(url)
print(result)
print(url)
```

> https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12

* 字符串模板填充

```python
start = "北京"  #在实际操作中，在不知道具体参数之前，可以将"北京" 换为None，dest和date同理。
dest = "天津"
date = "2020/3/16"
base = f"https://daft.website/result?from={start}&to={dest}&start=2020%"

from requests import Session
url = base + start + dest +date
result = Session().get(url)
print(result.text)
print(url)
```

> ```html
> <!DOCTYPE html>
> <html>
>   <head>
>     <title>Dominate</title><meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
>     <link href="https://file-vlfxzgbkek.now.sh" rel="stylesheet">
>   </head>
>   <body class="bg-grey-light ">
>     <div class="flex flex-col container mx-auto w-1/2 ">
>       <div class="flex bg-white px-5 py-3 mb-1 h-24 items-center justify-between ">
>         <div>
>           <ul class="list-reset flex flex-col ">
>             <li>
>               <h5>南方航空CZ3907</h5>
>             </li>
>             <li>
>               <span class="text-xs">波音 737-800(中型)</span>
>             </li>
>           </ul>
>         </div>
> ......
> ```

`base = f"https://daft.website/result?from={start}&to={dest}&start=2020%”`是由网址`https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2019%2F03%2F12`根据其特征而改的。

2. **for loop：用于多次请求**

```python
import time
from requests import Session

for i in ["2020/3/16","2020/3/17","2020/3/18"]: 
    start = "北京"
    dest = "天津"
    #date = "2020/3/16"对日期进行多次请求，这里不需要日期。
    base = f"https://daft.website/result?from={start}&to={dest}&start=2020%" #不要2020%也可
    result = Session().get(base) #此时的url变成base
    print(result.text)
    print("======================================================================================") #分隔作用，便于分隔多次请求的代码资料。
    time.sleep(2)
print(base)
```

> ```html
> <!DOCTYPE html>
> <html>
>   <head>
>     <title>Dominate</title><meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
>     <link href="https://file-vlfxzgbkek.now.sh" rel="stylesheet">
>   </head>
>   <body class="bg-grey-light ">
>     <div class="flex flex-col container mx-auto w-1/2 ">
>       <div class="flex bg-white px-5 py-3 mb-1 h-24 items-center justify-between ">
>         <div>
>           <ul class="list-reset flex flex-col ">
>             <li>
>               <h5>南方航空CZ3907</h5>
>             </li>
>             <li>
>               <span class="text-xs">波音 737(中型)</span>
>             </li>
>           </ul>
>         </div>
> ......
> ```

⚠️ ` for i in ["2020/3/16","2020/3/17","2020/3/18”]`: `[]`表示list，即`for i in list`。用循环是为了多次寻求，list是每次请求中不一样的东西。但一般的循环是这样写的，`for i in range()`: 此种方法主要是数据，日期等多样化列表请求循坏按上面写更加有效率。

⚠️ 此次没有在拼接处使用data数据，原因在于此次是对日期进行多次请求，在拼接处就不需要日期，把具体的多个日期填在循环处即可，以逗号隔开。

⚠️ 注意此处的时间模块：

```python 
import time #引入时间，防止高频访问IP被封
time.sleep(2) #一秒不得多于20次，此处为2秒钟一次。
```

⚠️ 多次循环的时候，为了区分结果，最好使用对`print()`进行巧妙运用。比如，在本次案例中使用的：	`print("===================================================================================") `

3. **while loop：监测网站的变化**

主要用于网站是否发生变化，比如抢票、抢购等。在之前所讲到的`autobro`也有同样的功能，不同的是`autobro`是通过截图的方式，`while loop`是通过信息判断的方式。

比如：通过网页信息监测手机模拟购买网站

```python
import time
from requests import Session

while True:
    result = Session().get("https://daft.tech/buy")
    print(result.text)
    print("==================================================================")
    time.sleep(1)
```

> ```html
> <!DOCTYPE html>
> <html>
>   <head>
>     <title>Dominate</title>
>     <link href="https://file-vlfxzgbkek.now.sh" rel="stylesheet">
>     <style>
>         .real-dark {
>              background-color: black;
>         };</style>
>   </head>
>  ......
> ```

4. **Condition Test 条件判断**

比如：通过网页信息监测手机模拟购买网站的抢购操作

```python
import time
from requests import Session

while True:
    result = Session().get("https://daft.tech/buy")
    if result.status_code == 200: #200代表请求成功
        print(result.text)
#        if "buy" in html #返回第一课笔记看是如何进行的
#           pass
        print("======================================================================")
  
    else: #注意else代表if的反面，包括300、400、500
        print("something wrong")
        print(result.status_code) #错误代码是什么
        print(result.text) #错误的详情信息是什么
        
    time.sleep(1)
```

> ```html
> <!DOCTYPE html>
> <html>
>   <head>
>     <title>Dominate</title>
>     <link href="https://file-vlfxzgbkek.now.sh" rel="stylesheet">
>     <style>
>         .real-dark {
>              background-color: black;
>         };</style>
>   </head>
> ```

这个的逻辑是先通过状态码来确定网页源码是否可以获取，如果可以获取则打印出网页源代码，不可以则告诉错误在何处。

下面关于知乎爬虫的例子可以清晰地说明这个问题：

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**爬取某一知乎专栏**</font>

```python
import time
from requests import Session

while True:
    result = Session().get("https://zhuanlan.zhihu.com/p/58931188")
    if result.status_code == 200: #200代表请求成功
        print(result.text)
        print("=====================================================================")
        
    else: #注意else代表if的反面，包括300、400、500
        print("something wrong")
        print(result.status_code) #错误代码是什么
        print(result.text) #错误的详情信息是什么
        
    time.sleep(1)
```

> ```html
> something wrong
> 400
> <html>
> <head><title>400 Bad Request</title></head>
> <body bgcolor="white">
> <center><h1>400 Bad Request</h1></center>
> <hr><center>openresty</center>
> </body>
> </html>
> ```

从运行结果可以看出，不能很顺利地爬取知乎专栏的网页，显示错误状态码为400，说明知乎实施了反爬措施。

此时我们可以用autobro来进行爬取，解决反爬问题。这里需要用到Chromium浏览器，否则会报错。Chromium浏览器的安装在终端进行即可。

**利用autobro爬取某一知乎专栏**

```python
from autobro import fetch
from requests import Session

while True:
    result = Session().get("https://zhuanlan.zhihu.com/p/58931188")
    if result.status_code == 200: #200代表请求成功
        print(result.text)
        print("======================================================================")
        
    else: #注意else代表if的反面，包括300、400、500
        print("something wrong, but I'll try autobro")
        html = fetch("https://zhuanlan.zhihu.com/p/58931188")
        print(html)
```

> ```html
> something wrong, but I'll try autobro
> <!DOCTYPE html><html lang="zh" data-hairline="true" data-theme="light" data-react-helmet="data-theme"><head><meta charset="utf-8"><title>橘猫被迫减肥5天能瘦吗？ - 知乎</title><meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1"><meta name="renderer" content="webkit"><meta name="force-rendering" content="webkit"><meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"><meta name="google-site-verification" content="FTeR0c8arOPKh8c5DYh_9uu98_zJbaWw53J-Sch9MTg"><meta data-react-helmet="true" name="keywords" content="宠物,动物,猫"><meta data-react-helmet="true" name="description" content="众所周知！虽说大橘为重！但也不要太重！所以咱家猪皮健康着想要开始减肥啦！为了做个表率！老父亲也要陪着一起锻炼减肥一起来看看这五天的成果吧~减肥大作战 ▼ 三猫小课堂又开课了今天来讲讲猫咪肥胖有哪些影响…"><meta data-react-helmet="true" property="og:title" content="橘猫被迫减肥5天能瘦吗？"><meta data-react-helmet="true" property="og:url" content="https://zhuanlan.zhihu.com/p/58931188"><meta data-react-helmet="true" property="og:description" content="众所周知！虽说大橘为重！但也不要太重！所以咱家猪皮健康着想要开始减肥啦！为了做个表率！老父亲也要陪着一起锻炼减肥一起来看看这五天的成果吧~减肥大作战 ▼ 三猫小课堂又开课了今天来讲讲猫咪肥胖有哪些影响…"><meta data-react-helmet="true" property="og:image" content="https://pic2.zhimg.com/v2-d4e2fac5c543e5d846f06dcb2e058d45_b.jpg"><meta data-react-helmet="true" property="og:type" content="article"><meta data-react-helmet="true" property="og:site_name" content="知乎专栏">......
> ```

由结果可以看到，通过autobro爬取网站源代码爬取。

5. **Data Structure 数据结构**

此刻要讲到一个新的办法`Headers`获取网站源代码，这种方法效率较高，所用时间更少。但是这个方法的弊端在于，这个库有时可用有时不可用。

```python
from fake_headers import Headers #这个库有时可以，有时不可以
from autobro import fetch
from requests import Session

sesh = Session()
headers = Headers()
sesh.headers = headers.generate() #是一个字典，查看是不是字典sesh.headers.后面全是字典的方法。
result = sesh.get("https://zhuanlan.zhihu.com/p/58931188")

if result.status_code == 200: #200代表请求成功
    print(result.text)
    print("======================================================================================")
else: #注意else代表if的反面，包括300、400、500
    print("something wrong, but I'll try autobro")
    html = fetch("https://zhuanlan.zhihu.com/p/58931188")
    print(html)
```

> ```html
> / usr / local / bin / python3 / Applications / PyCharm.app / Contents / plugins / python / helpers / pydev / pydevconsole.py - -mode = client - -port = 54267
> import sys;
> 
> print('Python %s on %s' % (sys.version, sys.platform))
> sys.path.extend(['/Users/zebchau/Documents/python/mugglecode_crawler_lesson'])
> Python
> 3.8
> .1(v3
> .8
> .1: 1
> b293b6006, Dec
> 18
> 2019, 14: 0
> 8: 53)
> Type
> 'copyright', 'credits' or 'license'
> for more information
> ......
> ```

这种方法输出的结果有更多的信息，并且网页源码是结构性的。

⚠️ header都是一个名词对应一个值，即键值结构，实际上就是字典。下面为header部分的内容。

```html
DNT: 1
Referer: https://zhuanlan.zhihu.com/p/58931188
Sec-Fetch-Dest: iframe
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Safari/537.36
```

⚠️ `sesh = Session() `客户端为了记住服务端干了什么，用cookie储存记录。网站后台用storage( 也叫Session，不要与headers的Session混淆）访问页面的人干了什么。

### **<font size=4 color=red>3.3 解析</font>**

1. **解析部分涉及的知识点**

* call function 解析部分多半部分都是在调用函数
* clean data 清洗数据
* 数据库 爬虫对数据库的要求不高

2. **Call Function 调用函数**

调用函数就是在代码中进行一些函数操作，通过这些函数来获取数据。

```python
from fake_headers import Headers #这个库有时可以，有时不可以
from bs4 import BeautifulSoup, element
from requests import Session

start = "北京"
dest = "天津"
date = "2020/3/17"
base = f"https://daft.website/result?from={start}&to={dest}&start={date}"

sesh = Session()
headers = Headers()
sesh.headers = headers.generate()
result = sesh.get(base)

soup = BeautifulSoup(result.text, "html.parser") #把结果给解释器
for e in soup.find_all("h3"):
    print(e)
    assert isinstance(e, element.Tag)
    print(e.get_text())
    print(type(e))
```

> ```html
> <h3>8:44</h3>
> 8:44
> <class 'bs4.element.Tag'>
> <h3>10:31</h3>
> 10:31
> <class 'bs4.element.Tag'>
> <h3 class="text-orange mr-3">551</h3>
> 551
> <class 'bs4.element.Tag'>
> <h3>3:50</h3>
> 3:50
> <class 'bs4.element.Tag'>
> <h3>8:50</h3>
> 8:50
> <class 'bs4.element.Tag'>
> ......
> ```

⚠️ 在爬虫中数据类型的转化非常重要，所有非基础类型数据，落地都会变成基础类型数据。`result.text`就是在进行数据类型的转换。

3.**Clean Data 清洗数据**

比如抓取的数据为123,456,67，需要洗数据，以逗号为分界点把数据分开，然后转一个int类型。
`"123,456,67".spilt(',') `

比如，抓取到的数据是脏的：人数      1234

主要有以下几种清洗办法：

```python
"人数      1234".spilt(" ")
"人数      1234".replace()
"人数      1234".lstrip()
"人数      1234".strip()
```

4. **数据库**

* 小数据可以用txt的方式保存

```python
file = open("./data.txt", "a") 
file.write()
```

⚠️ `a`模式的数据是一条一条、一行行的的，`w`模式则会把之前的数据覆盖掉

* 上万条的大数据存储用数据库的方式

  ```python
  import sqlite3
  ```

`sqlite3`库比较方便，不需要很强的权限、密码，甚至不需要占用额外的端口。Excel也可以，但是比较慢，也容易崩溃。搞数据分析的时候用csv。

* 利用`sqlite3`建立数据库需要注意的事项：
  * 添加字段相当于列的名字，字段的类型必须要选择，数据库对这个要求比较严格。
  * 类型：文字选`text`，数字选`integer`。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**爬取航班对应的航空公司的名字和价格**</font>

```python
# 请求
from requests import Session
from bs4 import BeautifulSoup

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2020%2F3%2F20&page1"
sesh = Session()
result = sesh.get(url)
html = result.text
print(type(html))

#解析
soup = BeautifulSoup(html, "html.parser") #第一个里边放文本，是str，第二个里边放解析器
price = soup.find_all("h3", class_ = "text-orange mr-3")
print(type(price))
company = soup.find_all("h5")

for i,k in zip(price, company):
    ticket_price, company_name = i.get_text(), k.get_text()
    print(company_name, ticket_price) #这种打印方法打印出来之后直接可以一一对应，比较规整
```

> <class 'str'>
> <class 'bs4.element.ResultSet'>
> 中国国航CA1883 820
> 东方航空MU5110 602
> 东方航空MU5110 1140
> 南方航空CZ3907 909
> 中国国航CA1883 735
> 中国国航CA1883 641
> 中国国航CA1883 978
> 中国国航CA1883 1075
> 南方航空CZ3907 674
> 东方航空MU5110 1069
> 中国国航CA1883 994
> 东方航空MU5110 866

⚠️ `requests`库有两个对象：`response`(结果）、`requests`（请求）。由 func() 到 result，用函数调用某个对象`requests.get(headers, auth)`（括号内调`headers`参数，`auth`是认证的意思）得到结果`result`(即`response`类型)，`result.txt`, `result.content`,  `result.headers`。

⚠️  带`find`的一般是复数格，复数格一般是装在列表中的，列表中的东西需要循坏才能得到。

⚠️ 列表的方法主要包括以下几类：

```python
[].append() #向列表里添加
[].clear() #清光列表
[].pop() #从列表里挤出去
```

⚠️ `` <h5>南方航空CZ3907</h5> `这种就没有特征了。像这种 `<h3 class="text-orange mr-3">762</h3> `才是有特征。没有特征的只能是赌一把，通过command+f来搜索`h5`，看看页面是不是有且只有一个`h5`元素针对这个主题，能够唯一选中。特别需要注意的是，通过command+f来搜索h5要注意数量能不能对上，有时候有些是广告。

⚠️ 循环两个列表的时候可以用zip函数，前提是要元素的数量一样。比如`for i,k in zip(price, company)`

```python
for i in price:
    print(i)
for j in company:
    print(j)
```

可以优化为：

```python
for i,k in zip(price, company):
    ticket_price, company_name = i.get_text(), k.get_text()
    print(company_name, ticket_price)
```

严格地来说，并不是如此优化，这种优化结合项目进行了优化。

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**Selector抓取航班对应的航空公司的名字和价格**</font>

这种方法比较方便，适用于公司业务变化比较快，在网页中类的名字还是这个名字，但是网页的结构发生了变化。

* Selector使用方法

```python
p = soup.select()
```

* 如何找到selector

  * 按类的名称去选择：

    * 方法1

      将类`list-reset flex flex-col ` 变成`ul.list-reset.flex.flex-col `，变的方法就是直接将空格全部换成英文的小数点`.`。

      注意，如果一个selector选不出来，给它加一个父层级的描述，如 `div.flex.flex-col > h3.text-orange.mr-3`。如果一个父层级不管用的话，可以再加一个`div.flex > div.flex.flex-col > h3.text-orange.mr-3`。

      ```html
      此处类的代码实际如下：
          <ul class="list-reset flex flex-col ">
          <li>
          <h5>南方航空CZ3907</h5>
          </li>
          <li>
          <span class="text-xs">波音 787-9(中型)</span>
          </li>
          </ul>
      
          <div class="flex ">
                <div class="flex flex-col">
                  <h3 class="text-orange mr-3">1129</h3>
                  <span class="text-grey-light text-xs">8 折</span>
                </div>
                <button class="bg-orange  px-4 py-2 border-lg rounded text-white">订票</button>
              </div>
      ```

    * 方法2

      选择body的下一级目录，点击右键选择`copy selector`，然后粘贴即可。粘贴出来的内容是： `body > div > div:nth-child(1)`，`div:nth-child(1)`表示名字，`body > `表示层次关系，箭头表示父级目录与子级的关系。`body`是整个文档本身，一个网页只能有一个`body`。注意只能按照原来的元素进行层级划分，中间不能多子元素，不然selector方法不会生效。

      注意这里是复制复制粘贴`body`的下一级目录，复制出来是这个样子的：`body > div > div:nth-child(1) `需要在`div`上添加上类的具体信息，空格处用点替代：`div.flex.flex-col.container.mx-auto.w-1/2`。完整的就是`body > div.flex.flex-col.container.mx-auto.w-1/2 > div:nth-child(1)`

```python
from requests import Session
from bs4 import BeautifulSoup

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2020%2F3%2F20&page1"
sesh = Session()
result = sesh.get(url)
html = result.text
print(type(html))

# 解析
soup = BeautifulSoup(html, "html.parser")  # 第一个里边放文本，是str，第二个里边放解析器
css = "body > div.flex.flex-col.container.mx-auto.w-1/2 > div:nth-child(1)"
price = soup.select("h3.text-orange.mr-3") 
print(type(price))
company = soup.find_all("h5")

for i, k in zip(price, company):
    ticket_price, company_name = i.get_text(), k.get_text()
    print(company_name, ticket_price) 
```

> <class 'str'>
> <class 'bs4.element.ResultSet'>
> 东方航空MU5110 1035
> 东方航空MU5110 685
> 南方航空CZ3907 730
> 东方航空MU5110 736
> 南方航空CZ3907 795
> 中国国航CA1883 1092
> 中国国航CA1883 727
> 东方航空MU5110 1098
> 东方航空MU5110 913
> 南方航空CZ3907 560
> 南方航空CZ3907 1035
> 中国国航CA1883 625

<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**一次抓取多信息：Selector方法抓取航班对应的航空公司的名字和价格**</font>

Selector可以一次把整个大类信息爬出来，然后再在大类信息去去找需要的信息，可以避免使用很多个selector。比如：将大类`div class="flex bg-white px-5 py-3 mb-1 h-24 items-center justify-between`找到并提取出来， 变成 `div.flex.bg-white.px-5.py-3.mb-1.h-24.items-center.justify-between`。

这种方法比建立多个selector明显效率更高。

```python
from requests import Session
from bs4 import BeautifulSoup

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2020%2F3%2F20&page1"
sesh = Session()
result = sesh.get(url)
html = result.text
print(type(html))

# 解析
soup = BeautifulSoup(html, "html.parser")  # 第一个里边放文本，是str，第二个里边放解析器
css = "div.flex.bg-white.px-5.py-3.mb-1.h-24.items-center.justify-between"
data_group = soup.select(css)
info = [i.get_text().split() for i in data_group] #一个对象连续调用两次方法
data = [[i[0],i[-4]] for i in info]
print(data)
```

> [['南方航空CZ3907', '1226'], ['南方航空CZ3907', '912'], ['南方航空CZ3907', '556'], ['东方航空MU5110', '1069'], ['中国国航CA1883', '809'], ['南方航空CZ3907', '897'], ['东方航空MU5110', '705'], ['南方航空CZ3907', '897'], ['南方航空CZ3907', '661'], ['中国国航CA1883', '1008'], ['中国国航CA1883', '1149'], ['南方航空CZ3907', '551']]

⚠️ 代码能简化的情形一定要简化，这样可以节省代码运行的效率。

```python
info = [i for i in data_group] #列表解析式
new_list = []
for i in data_group:
    new_list.append(i)
print(info)
```

可以简化为：

```python
info = [i.get_text() for i in data_group] #列表解析式
print(info)
```

⚠️ `info = [i.get_text().split() for i in data_group]`加上`split()`的原因在于之前输出来的信息有很多无用信息，需要清洗。这种也是一个对象连续调用两次方法。情况如下：

```python
\n\n\n\n东方航空MU5110\n\n\n空中客车 A330(大型)\n\n\n\n\n\n\n12:50\n\n\n北京机场\n\n\n\n\n\n12:44\n\n\n深圳机场\n\n\n\n\n\n744\n8 折\n\n订票\n\n
```

这种方法就相当于列表里边套列表`[[],[],[]]`

```python
'a b c'.split() -> ['a', 'b', 'c']
```

⚠️  对循环信息中的信息进行选择时也可以简化代码

比如信息输出是这样，需要选择航司和价格：

```html
[['中国国航CA1883', '空中客车', 'A350(大型)', '10:27', '北京机场', '8:40', '深圳机场', '1146', '8', '折', '订票'], ['东方航空MU5110', '空中客车', 'A350(大型)', '7:27', '北京机场', '3:23', '深圳机场', '752', '8', '折', '订票'], ['中国国航CA1883', '空中客车', 'A330(大型)', '3:44', '北京机场', '8:40', '深圳机场', '710', '8', '折', '订票'], ['中国国航CA1883', '波音', '787-9(中型)', '3:23', '北京机场', '8:50', '深圳机场', '587', '8', '折', '订票'], ['中国国航CA1883', '波音', '787-9(中型)', '15:40', '北京机场', '12:30', '深圳机场', '1164', '8', '折', '订票']
```

按照一般方法应该是这样：

```python
for i in info:
    print(i[0])
    print(i[-4])
```

进行代码简化就可以这样：

```python
data = [[i[0],i[-4]] for i in info]
print(data)
```

### **<font size=4 color=red>3.4 存储</font>**

存储需要ORM，数据库对应的驱动，帮助写入SQL类型的数据，最厉害的ORM是Diango ORM。

```python
from requests import Session
from bs4 import BeautifulSoup
import dataset

url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2020%2F3%2F20&page1"
sesh = Session()
result = sesh.get(url)
html = result.text
print(type(html))

# 解析
soup = BeautifulSoup(html, "html.parser")  # 第一个里边放文本，是str，第二个里边放解析器
css = "div.flex.bg-white.px-5.py-3.mb-1.h-24.items-center.justify-between"
data_group = soup.select(css)
info = [i.get_text().split() for i in data_group] #一个对象连续调用两次方法
data = [[i[0],i[-4]] for i in info]

#存储
db = dataset.connect("sqlite:///ticketdata.db")
##插入数据
tickets = db["tickets"]
for i  in data:
    company_name, tick_price = i
    tickets.insert(dict(company = company_name, price = tick_price)) #只能插入字典类型，因为数据库都是键值结构。不能插入列表。
print("done")
```

⚠️数据库是键值结构（k-v结构），只能插入字典类型。

⚠️ 在连接上数据库之后，要进行测试，方法如下：

```python
db = dataset.connect("sqlite:///ticketdata.db")
print(db["tickets"]) #不是字典，但是一般称之为键值结构。打印是为了测试类型。
#<Table(tickets)>，需要这一步
for i in db['tickets']:
    print(i) #打印出来的是之前写的假数据。
#OrderedDict([('company', '海南'), ('price', 998)])
```

⚠️ 在插入数据的时候，也要进行测试，以便找到dict中数据排列的顺序，具体方法如下：

```python
tickets = db["tickets"]
for i  in data:
    print(i) #测试数据的顺序及位子，为下面dict中的内容排列找依据。
    company_name, tick_price = i
    tickets.insert(dict(company = company_name, price = tick_price)) 
```

⚠️存储中数据库的路径和名字要写对

```python
db = dataset.connect("sqlite:///ticketdata.db")
```

本项目包含测试的完整代码如下：

```python
from requests import Session
from bs4 import BeautifulSoup
import dataset


url = "https://daft.website/result?from=%E5%8C%97%E4%BA%AC&to=%E6%B7%B1%E5%9C%B3&start=2020%2F3%2F20&page1"
sesh = Session()
result = sesh.get(url)
html = result.text
print(type(html))

# 解析
# company -> price
soup = BeautifulSoup(html, "html.parser")  # 第一个里边放文本，是str，第二个里边放解析器
css = "div.flex.bg-white.px-5.py-3.mb-1.h-24.items-center.justify-between"
#div class="flex bg-white px-5 py-3 mb-1 h-24 items-center justify-between" -> div.flex.bg-white.px-5.py-3.mb-1.h-24.items-center.justify-between
#此处是直接把整个大类的信息爬取出来，然后再在大类信息去去找需要的信息，可以避免使用很多个selector。
data_group = soup.select(css)
info = [i.get_text().split() for i in data_group] #一个对象连续调用两次方法
data = [[i[0],i[-4]] for i in info]
db = dataset.connect("sqlite:///ticketdata.db")
#k-v结构，即键值结构
print(db["tickets"]) #不是字典，但是一般称之为键值结构。打印是为了测试类型。
#<Table(tickets)>
for i in db['tickets']:
    print(i) #打印出来的是之前写的假数据。
#OrderedDict([('company', '海南'), ('price', 998)])
###接下来就是插入数据
tickets = db["tickets"]
for i  in data:
    print(i) #测试数据的顺序及位子，为下面dict中的内容排列找依据。
    company_name, tick_price = i
    tickets.insert(dict(company = company_name, price = tick_price)) #只能插入字典类型，因为数据库都是键值结构。不能插入列表。
print("done")
```



<font size=3 color=**#3498DB**>**示例**</font>

<font size=3 color=**#3498DB**>**爬虫贝壳成都租房**</font>

```python
from requests import Session
from bs4 import BeautifulSoup
import time
import random
import dataset

for i in range(1, 100):
    url = "https://cd.zu.ke.com/zufang/pg{}/#contentList".format(i + 1)
    result = Session().get(url)
    html = result.text
    
    proxies = {'http': '115.238.59.86', 'https': '222.95.144.212'}
    time.sleep(random.randint(0, 5))

    soup = BeautifulSoup(html, "html.parser")
    css = "#content > div.content__article > div.content__list > div:nth-child(1) > div"
    data_group = soup.select(css)
    info = [i.get_text().split() for i in data_group]
    data = [[i[0], i[2], i[3], i[5], i[8], i[10], i[11], i[-2]] for i in info]
    print(data)
    db = dataset.connect("sqlite:///bkcdzf.db")
    bkcdzf = db["bkcdzf"]
    for i in data:
        lease_way, room_direction, address, area, house_type, high_floor, floor, price = i
        bkcdzf.insert(dict(lease_way=lease_way, room_direction=room_direction, address=address, area=area, house_type=house_type, high_floor=high_floor, floor=floor, price=price))

print("done")
```

引出问题：

如何解决人际验证？

如何实现混合方法运用：比如`soup.select`和`soup.find`方法混用。

网站显示有一万多条数据，运行结果却只有138条数据，问题在哪？