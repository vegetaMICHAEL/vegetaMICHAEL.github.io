---
layout: post
title:  Python学习之面试题专辑
date:   2020-07-25 16:31:01 +0800
categories: jekyll
tag: jekyll
---

* content
{:toc}

**1. 一行代码实现1--100之和**

利用sum()函数求和

`sum(range(1, 100))`


**2. 如何在一个函数内部修改全局变量**

利用global在函数声明 修改全局变量
```
a = 5
def fn():
    global a
    a = 4
fn()
print(a)
```

**3. 列出5个python标准库**
- os：提供了不少与操作系统相关联的函数
- sys: 通常用于命令行参数
- re: 正则匹配
- math: 数学运算
- datetime:处理日期时间

**4. 字典如何删除键和合并两个字典**
del和update方法
```
dic = {"name":"zs","age":18}
del dic["name"]
dic
{'age':18}
dic2 = {"nema":"ls"}
dic.update(dic2)
dic
{'age':18,'name':'ls'}
```

**5. 谈下python的GIL**

- GIL 是python的全局解释器锁，同一进程中假如有多个线程运行，一个线程在运行python程序的时候会霸占python解释器（加了一把锁即GIL），使该进程内的其他线程无法运行，等该线程运行完后其他线程才能运行。如果线程运行过程中遇到耗时操作，则解释器锁解开，使其他线程运行。所以在多线程中，线程的运行仍是有先后顺序的，并不是同时进行。
- 多进程中因为每个进程都能被系统分配资源，相当于每个进程有了一个python解释器，所以多进程可以实现多个进程的同时运行，缺点是进程系统资源开销大。

**6. python实现列表去重的方法**

先通过集合去重，在转列表
```
lis = [11,12,13,12,15,16,13]
a = set(lis)
a
{11,12,13,15,16}
[x for x in a]
[11,12,13,15,16]
```

**7. fun(\*args,\*\*kwargs)中的\*args,\*\*kwargs什么意思？**

不确定调用函数时会传多少个参数，*args：非键值对可变数量参数列表
```
def demo(*args):
    ...
demo('a','b','c','d','e')
```
**kwargs：不定长度键值对
```
def demo(**args):
    ...
demo(name='hayisdvbfa')
```

**8. python2和python3的range（100）的区别**

python2返回列表，python3返回迭代器，节约内存

**9. 一句话解释什么样的语言能够用装饰器?**

函数可以作为参数传递的语言，可以使用装饰器
>在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）, 本质上，decorator就是一个返回函数的高阶函数

**10. python内建数据类型有哪些**

- 整型--int
- 布尔型--bool
- 字符串--str
- 列表--list
- 元组--tuple
- 字典--dict

**11. 简述面向对象中__new__和__init__区别**

__init__是初始化方法，创建对象后，就立刻被默认调用了，可接收参数，如图
![/styles/images/Python-problem/__init__.jpg]({{ '/styles/images/Python-problem/__init__.jpg' | prepend: site.baseurl  }})

1. __new__至少要有一个参数cls，代表当前类，此参数在实例化时由Python解释器自动识别
2. __new__必须要有返回值，返回实例化出来的实例，这点在自己实现__new__时要特别注意，可以return父类（通过super(当前类名, cls)）__new__出来的实例，或者直接是object的__new__出来的实例
3. __init__有一个参数self，就是这个__new__返回的实例，__init__在__new__的基础上可以完成一些其它初始化的动作，__init__不需要返回值
4. 如果__new__创建的是当前类的实例，会自动调用__init__函数，通过return语句里面调用的__new__函数的第一个参数是cls来保证是当前类实例，如果是其他类的类名，；那么实际创建返回的就是其他类的实例，其实就不会调用当前类的__init__函数，也不会调用其他类的__init__函数。

![/styles/images/Python-problem/__new__.jpg]({{ '/styles/images/Python-problem/__new__.jpg' | prepend: site.baseurl  }})

**12. 简述with方法打开处理文件帮我我们做了什么？**
```
f = open("./1.txt","wb")
try:
    f.write("hello world")
except:
    pass
finally:
    f.close()
```
打开文件在进行读写的时候可能会出现一些异常状况，如果按照常规的f.open

写法，我们需要try,except,finally，做异常判断，并且文件最终不管遇到什么情况，都要执行finally f.close()关闭文件，with方法帮我们实现了finally中f.close

（当然还有其他自定义功能，有兴趣可以研究with方法源码）

**13. 列表[1,2,3,4,5],请使用map()函数输出[1,4,9,16,25]，并使用列表推导式提取出大于10的数，最终输出[16,25]**

map（）函数第一个参数是fun，第二个参数是一般是list，第三个参数可以写list，也可以不写，根据需求
```
lis = [1,2,3,4,5]
def fn(x):
    return x**2
res = map(fn, lis)
res = [i for i in res if i>10]
res
[16,25]
```

**14. python中生成随机整数、随机小数、0--1之间小数方法**

- 随机整数：random.randint(a,b),生成区间内的整数
- 随机小数：习惯用numpy库，利用np.random.randn(5)生成5个随机小数
- 0-1随机小数：random.random(),括号中不传参

**15. 避免转义给字符串加哪个字母表示原始字符串？**

r , 表示需要原始字符串，不转义特殊字符
```
>>>print r'\n'
\n
```

**16. <div class="nam">中国</div>，用正则匹配出标签里面的内容（“中国”），其中class的类名是不确定的**

正则表达式
意义 | 符号
:----: | :---:
一个数字 | \d
一个字母或数字 | \w
一个空格 （也包括Tab等空白符） | \s
任意个字符（包括0个） | *
至少一个字符 | +
0个或1个字符 | ?
n个字符 | {n}
n-m个字符 | {n,m}
范围 | []
一个数字、字母或者下划线 | [0-9a-zA-Z\_]
至少由一个数字、字母或者下划线组成的字符串 | [0-9a-zA-Z\_]+
Python合法的变量(由字母或下划线开头，后接任意个由一个数字、字母或者下划线组成的字符串) | [a-zA-Z\_][0-9a-zA-Z\_]*
变量的长度是1-20个字符 | [a-zA-Z\_][0-9a-zA-Z\_]{0, 19}
A或B | A|B
行的开头 | ^
行的结束 | $
不用考虑转义的问题 | r前缀
判断正则表达式是否匹配 | 'import re
切分字符串 | re.split(r'[\s\,]+', 'a,b, c d')
```
import re
str = '<div class="nam">中国</div>'
#.* :.表示可有可无,*表示任意字符；.*?:提取文本
re = re.findall(r'<div class=".*">(.*?)</div>',str)
print(res)
```
**17. python中断言方法举例**

assert（）方法，断言成功，则程序继续执行，断言失败，则程序报错
```
a = 3
assert(a>1)
print('断言成功，程序继续执行')
b = 4
assert(b>9)
print("断言失败，程序报错")
```
**18. 数据表student有id,name,score,city字段，其中name中的名字可有重复，需要消除重复行,请写sql语句**

`select distinct name from student`

**19. 10个Linux常用命令**

ls pwd cd touch rm mkdir tree cp mv cat more grep echo

**20. python2和python3区别？列举5个**

1. Python2 既可以使用带小括号的方式，也可以使用一个空格来分隔打印内容，比 如 print 'hi'。Python3 使用 print 必须要以小括号包裹打印内容，比如 print('hi')
2. python2 range(1,10)返回列表。python3中返回迭代器，节约内存
3. python2中使用ascii编码。python中使用utf-8编码
4. python2中unicode表示字符串序列，str表示字节序列。python3中str表示字符串序列，byte表示字节序列
5. python2中为正常显示中文，引入coding声明。python3中不需要
6. python2中是raw_input()函数。python3中是input()函数























