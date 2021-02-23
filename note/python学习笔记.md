# python学习笔记

## 第一章 	计算机基础

### 1.1  主机显示

PS1="\e[31m[\u@\h \w]$\e[m"^C

## 第二章 	python入门

### 2,1 安装python

yum -y install python3

yum -y install pip3

yum -y install ipython3

## 第三章 	数据类型

### 3.1 类型

数字（整形	长整型	浮点数	复数）	字符串	列表	元组	字典	集合

```
#=============================基本使用====================================
#1、用途

#2、定义方式

#3、常用操作+内置的方法

#============================该类型总结==================================
#存一个值or存多个值
    
#有序or无序

#可变or不可变（1、可变：值变，id不变。可变==不可hash 2、不可变：值变，id就变。不可变==可hash）
```

#### 字符串

```
#作用：名字，性别，国籍，地址等描述信息

#定义：在单引号\双引号\三引号内，由一串字符组成
name='egon'

#优先掌握的操作：
#1、按索引取值(正向取+反向取) ：只能取
#2、切片(顾头不顾尾，步长)
#3、长度len
#4、成员运算in和not in

#5、移除空白strip
#6、切分split
#7、循环
```

#### 列表

```
#ps:反向步长
l=[1,2,3,4,5,6]

#正向步长
l[0:3:1] #[1, 2, 3]
#反向步长
l[2::-1] #[3, 2, 1]
#列表翻转
l[::-1] #[6, 5, 4, 3, 2, 1]
```

#### 元组

```
#作用：存多个值，对比列表来说，元组不可变（是可以当做字典的key的），主要是用来读

#定义：与列表类型比，只不过[]换成()
age=(11,22,33,44,55)本质age=tuple((11,22,33,44,55))

#优先掌握的操作：
#1、按索引取值(正向取+反向取)：只能取   
#2、切片(顾头不顾尾，步长)
#3、长度
#4、成员运算in和not in

#5、循环
```



#### 集合

```
#作用：去重，关系运算，

#定义：
            知识点回顾
            可变类型是不可hash类型
            不可变类型是可hash类型

#定义集合:
            集合：可以包含多个元素，用逗号分割，
            集合的元素遵循三个原则：
             1：每个元素必须是不可变类型(可hash，可作为字典的key)
             2:没有重复的元素
             3：无序

注意集合的目的是将不同的值存放到一起，不同的集合间用来做关系运算，无需纠结于集合中单个值
 

#优先掌握的操作：
#1、长度len
#2、成员运算in和not in

#3、|合集
#4、&交集
#5、-差集
#6、^对称差集
#7、==
#8、父集：>,>= #9、子集：<,<=  
```



#### 数据类型总结（存储空间占用从低到高）

```
数字
字符串
集合：无序，即无序存索引相关信息
元组：有序，需要存索引相关信息，不可变
列表：有序，需要存索引相关信息，可变，需要处理数据的增删改
字典：无序，需要存key与value映射的相关信息，可变，需要处理数据的增删改
```

## 第四章 	文件操作

### 4.1流程

```
#1. 打开文件，得到文件句柄并赋值给一个变量
#2. 通过句柄对文件进行操作
#3. 关闭文件

#1. 打开文件，得到文件句柄并赋值给一个变量
f=open('a.txt','r',encoding='utf-8') #默认打开模式就为r

#2. 通过句柄对文件进行操作
data=f.read()

#3. 关闭文件
f.close()
```

### 4.2模式

```
#1. 打开文件的模式有(默认为文本模式)：
r ，只读模式【默认模式，文件必须存在，不存在则抛出异常】
w，只写模式【不可读；不存在则创建；存在则清空内容】
a， 之追加写模式【不可读；不存在则创建；存在则只追加内容】

#2. 对于非文本文件，我们只能使用b模式，"b"表示以字节的方式操作（而所有文件也都是以字节的形式存储的，使用这种模式无需考虑文本文件的字符编码、图片文件的jgp格式、视频文件的avi格式）
rb 
wb
ab
注：以b方式打开时，读取到的内容是字节类型，写入时也需要提供字节类型，不能指定编码

#3. 了解部分
"+" 表示可以同时读写某个文件
r+， 读写【可读，可写】
w+，写读【可读，可写】
a+， 写读【可读，可写】


x， 只写模式【不可读；不存在则创建，存在则报错】
x+ ，写读【可读，可写】
xb
```

### 4.3文件修改

```
import os

with open('a.txt') as read_f,open('.a.txt.swap','w') as write_f:
    for line in read_f:
        line=line.replace('alex','SB')
        write_f.write(line)

os.remove('a.txt')
os.rename('.a.txt.swap','a.txt') 
```



## 第五章 	函数

### 5.1 函数知识体系

```
1 什么是函数？
2 为什么要用函数？
3 函数的分类：内置函数与自定义函数
4 如何自定义函数
  语法
  定义有参数函数，及有参函数的应用场景
  定义无参数函数，及无参函数的应用场景
  定义空函数，及空函数的应用场景

5 调用函数
    如何调用函数
    函数的返回值
    函数参数的应用：形参和实参，位置参数，关键字参数，默认参数，*args，**kwargs

6 高阶函数（函数对象）
7 函数嵌套
8 作用域与名称空间
9 装饰器
10 迭代器与生成器及协程函数
11 三元运算，列表解析、生成器表达式
12 函数的递归调用
13 内置函数
14 面向过程编程与函数式编程
```

```
#1、位置参数：按照从左到右的顺序定义的参数
        位置形参：必选参数
        位置实参：按照位置给形参传值

#2、关键字参数：按照key=value的形式定义的实参
        无需按照位置为形参传值
        注意的问题：
                1. 关键字实参必须在位置实参右面
                2. 对同一个形参不能重复传值

#3、默认参数：形参在定义时就已经为其赋值
        可以传值也可以不传值，经常需要变得参数定义成位置形参，变化较小的参数定义成默认参数（形参）
        注意的问题：
                1. 只在定义时赋值一次
                2. 默认参数的定义应该在位置形参右面
                3. 默认参数通常应该定义成不可变类型


#4、可变长参数：
        可变长指的是实参值的个数不固定
        而实参有按位置和按关键字两种形式定义，针对这两种形式的可变长，形参对应有两种解决方案来完整地存放它们，分别是*args，**kwargs

        ===========*args===========
        def foo(x,y,*args):
            print(x,y)
            print(args)
        foo(1,2,3,4,5)

        def foo(x,y,*args):
            print(x,y)
            print(args)
        foo(1,2,*[3,4,5])


        def foo(x,y,z):
            print(x,y,z)
        foo(*[1,2,3])

        ===========**kwargs===========
        def foo(x,y,**kwargs):
            print(x,y)
            print(kwargs)
        foo(1,y=2,a=1,b=2,c=3)

        def foo(x,y,**kwargs):
            print(x,y)
            print(kwargs)
        foo(1,y=2,**{'a':1,'b':2,'c':3})


        def foo(x,y,z):
            print(x,y,z)
        foo(**{'z':1,'x':2,'y':3})

        ===========*args+**kwargs===========

        def foo(x,y):
            print(x,y)

        def wrapper(*args,**kwargs):
            print('====>')
            foo(*args,**kwargs)

#5、命名关键字参数：*后定义的参数，必须被传值（有默认值的除外），且必须按照关键字实参的形式传递
可以保证，传入的参数中一定包含某些关键字
        def foo(x,y,*args,a=1,b,**kwargs):
            print(x,y)
            print(args)
            print(a)
            print(b)
            print(kwargs)

        foo(1,2,3,4,5,b=3,c=4,d=5)
        结果：
            1
            2
            (3, 4, 5)
            1
            3
            {'c': 4, 'd': 5}
```

```
什么时候该有返回值？
　　　　调用函数，经过一系列的操作，最后要拿到一个明确的结果，则必须要有返回值
　　　　通常有参函数需要有返回值，输入参数，经过计算，得到一个最终的结果
什么时候不需要有返回值？
　　　　调用函数，仅仅只是执行一系列的操作，最后不需要得到什么结果，则无需有返回值
　　　　通常无参函数不需要有返回值
```

### 5.2函数对象、函数嵌套、名称空间与作用域、装饰器

函数对象

```
#1 可以被引用
#2 可以当作参数传递
#3 返回值可以是函数
#3 可以当作容器类型的元素
```

嵌套

```
def f1():
    def f2():
        def f3():
            print('from f3')
        f3()
    f2()

f1()
f3() #报错，为何？请看下一小节
```

一 名称空间

```
名称空间：存放名字的地方，三种名称空间
```

**二 名称空间的加载顺序**

```
python test.py
#1、python解释器先启动，因而首先加载的是：内置名称空间
#2、执行test.py文件，然后以文件为基础，加载全局名称空间
#3、在执行文件的过程中如果调用函数，则临时产生局部名称空间
```

三 名字的查找顺序

```
局部名称空间--->全局名称空间--->内置名称空间

#需要注意的是：在全局无法查看局部的，在局部可以查看全局的，如下示例

# max=1
def f1():
    # max=2
    def f2():
        # max=3
        print(max)
    f2()
f1()
print(max) 
```

四作用域

```
#1、作用域即范围
        - 全局范围（内置名称空间与全局名称空间属于该范围）：全局存活，全局有效
　     - 局部范围（局部名称空间属于该范围）：临时存活，局部有效
#2、作用域关系是在函数定义阶段就已经固定的，与函数的调用位置无关，如下
x=1
def f1():
    def f2():
        print(x)
    return f2
x=100
def f3(func):
    x=2
    func()
x=10000
f3(f1())

#3、查看作用域：globals(),locals()


LEGB 代表名字查找顺序: locals -> enclosing function -> globals -> __builtins__
locals 是函数内的名字空间，包括局部变量和形参
enclosing 外部嵌套函数的名字空间（闭包中常见）
globals 全局变量，函数定义所在模块的名字空间
builtins 内置模块的名字空间
```

### 5.3闭包

```
#内部函数包含对外部作用域而非全局作用域的引用

#提示：之前我们都是通过参数将外部的值传给函数，闭包提供了另外一种思路，包起来喽，包起呦，包起来哇

        def counter():
            n=0
            def incr():
                nonlocal n
                x=n
                n+=1
                return x
            return incr

        c=counter()
        print(c())
        print(c())
        print(c())
        print(c.__closure__[0].cell_contents) #查看闭包的元素
```

二 闭包的意义与应用

```
#闭包的意义：返回的函数对象，不仅仅是一个函数对象，在该函数外还包裹了一层作用域，这使得，该函数无论在何处调用，优先使用自己外层包裹的作用域
#应用领域：延迟计算（原来我们是传参，现在我们是包起来）
    from urllib.request import urlopen

    def index(url):
        def get():
            return urlopen(url).read()
        return get

    baidu=index('http://www.baidu.com')
    print(baidu().decode('utf-8'))
```

### 5.4装饰器

装饰器就是闭包函数的一种应用场景

**一 为何要用装饰器**

```
#开放封闭原则：对修改封闭，对扩展开放
```

**二 什么是装饰器**

```
装饰器他人的器具，本身可以是任意可调用对象，被装饰者也可以是任意可调用对象。
强调装饰器的原则：1 不修改被装饰对象的源代码 2 不修改被装饰对象的调用方式
装饰器的目标：在遵循1和2的前提下，为被装饰对象添加上新功能
```

### 5.5三元表达式、生成器表达式、匿名函数、内置函数

**一 三元表达式**

```
name=input('姓名>>: ')
res='SB' if name == 'alex' else 'NB'
print(res)
```

二 生成器表达式

```
#1、把列表推导式的[]换成()就是生成器表达式

#2、示例：生一筐鸡蛋变成给你一只老母鸡，用的时候就下蛋，这也是生成器的特性
>>> chicken=('鸡蛋%s' %i for i in range(5))
>>> chicken
<generator object <genexpr> at 0x10143f200>
>>> next(chicken)
'鸡蛋0'
>>> list(chicken) #因chicken可迭代，因而可以转成列表
['鸡蛋1', '鸡蛋2', '鸡蛋3', '鸡蛋4',]

#3、优点：省内存，一次只产生一个值在内存中
```

三匿名函数

一 什么是匿名函数

```
匿名就是没有名字
def func(x,y,z=1):
    return x+y+z

匿名
lambda x,y,z=1:x+y+z #与函数有相同的作用域，但是匿名意味着引用计数为0，使用一次就释放，除非让其有名字
func=lambda x,y,z=1:x+y+z 
func(1,2,3)
#让其有名字就没有意义
```

**二 有名字的函数与匿名函数的对比**

```
#有名函数与匿名函数的对比
有名函数：循环使用，保存了名字，通过名字就可以重复引用函数功能

匿名函数：一次性使用，随时随时定义

应用：max，min，sorted,map,reduce,filter
```





## 第六章	 模块

### 1、什么是模块？

```
大家之前在编写ATM作业时，思路是先将程序中都需要有哪些功能定义出来，然后在需要用的地方调用即可。
比起之前通篇垒代码的方式，将重复要用的功能定义成函数会让程序更加简洁，这不能不算做是一种进步，
但问题是，随着程序功能越来越多，再将所有的代码都放到一起，程序的组织结构仍然会不清晰，不方便管理，
以后我们写程序，都是分文件的，如果多个文件中都需要用到同一段功能，难道我们要重复编写该功能吗？很明显不能
这就需要我们找到一种解决方案，能够将程序中经常要用的功能集合到一起，然后在想用的地方随时导入使用，
这几乎就是模块的全部含义了

最后总结：
模块就是一组功能的集合体，我们的程序可以导入模块来复用模块里的功能。
```

```
#常见的场景：一个模块就是一个包含了一组功能的python文件,比如spam.py，模块名为spam，可以通过import spam使用。

#在python中，模块的使用方式都是一样的，但其实细说的话，模块可以分为四个通用类别：　

　　1 使用python编写的.py文件

　　2 已被编译为共享库或DLL的C或C++扩展

　　3 把一系列模块组织到一起的文件夹（注：文件夹下有一个__init__.py文件，该文件夹称之为包）

　　4 使用C编写并链接到python解释器的内置模块
```

2、为何要使用模块

```
#1、从文件级别组织程序，更方便管理
随着程序的发展，功能越来越多，为了方便管理，我们通常将程序分成一个个的文件，这样做程序的结构更清晰，方便管理。这时我们不仅仅可以把这些文件当做脚本去执行，还可以把他们当做模块来导入到其他的模块中，实现了功能的重复利用

#2、拿来主义，提升开发效率
同样的原理，我们也可以下载别人写好的模块然后导入到自己的项目中使用，这种拿来主义，可以极大地提升我们的开发效率

#ps：
如果你退出python解释器然后重新进入，那么你之前定义的函数或者变量都将丢失，因此我们通常将程序写到文件中以便永久保存下来，需要时就通过python test.py方式去执行，此时test.py被称为脚本script。
```

**为模块名起别名**

为已经导入的模块起别名的方式对编写可扩展的代码很有用

```
1 import spam as sm
2 print(sm.money)
```



### 2、from...import...的使用

```
 1 from spam import read1,read2
 
 唯一的区别就是：使用from...import...则是将spam中的名字直接导入到当前的名称空间中，所以在当前名称空间中，直接使用名字就可以了、无需加前缀：spam.
```



### 3、py文件区分两种用途:模块与脚本

```
#编写好的一个python文件可以有两种用途：
    一：脚本，一个文件就是整个程序，用来被执行
    二：模块，文件中存放着一堆功能，用来被导入使用


#python为我们内置了全局变量__name__，
    当文件被当做脚本执行时：__name__ 等于'__main__'
    当文件被当做模块导入时：__name__等于模块名

#作用：用来控制.py文件在不同的应用场景下执行不同的逻辑
    if __name__ == '__main__':
```



### 4、包介绍

```
#官网解释
Packages are a way of structuring Python’s module namespace by using “dotted module names”
包是一种通过使用‘.模块名’来组织python模块名称空间的方式。

#具体的：包就是一个包含有__init__.py文件的文件夹，所以其实我们创建包的目的就是为了用文件夹将文件/模块组织起来

#需要强调的是：
　　1. 在python3中，即使包下没有__init__.py文件，import 包仍然不会报错，而在python2中，包下一定要有该文件，否则import 包报错

　　2. 创建包的目的不是为了运行，而是被导入使用，记住，包只是模块的一种形式而已，包的本质就是一种模块　　
```

**为何要使用包**

```
包的本质就是一个文件夹，那么文件夹唯一的功能就是将文件组织起来
随着功能越写越多，我们无法将所以功能都放到一个文件中，于是我们使用模块去组织功能，而随着模块越来越多，我们就需要用文件夹将模块文件组织起来，以此来提高程序的结构性和可维护性
```

包总结：

```
总结包的使用需要牢记三点
1、导包就是在导包下__init__.py文件
2、包内部的导入应该使用相对导入，相对导入也只能在包内部使用，而且...取上一级不能出包
3、
使用语句中的点代表的是访问属性
    m.n.x ----> 向m要n，向n要x
而导入语句中的点代表的是路径分隔符
    import a.b.c --> a/b/c，文件夹下a下有子文件夹b，文件夹b下有子文件或文件夹c
所以导入语句中点的左边必须是一个包
```

### 5、常用模块

#### 1,time跟datetime

- 时间戳(timestamp)：通常来说，时间戳表示的是从1970年1月1日00:00:00开始按秒计算的偏移量。我们运行“type(time.time())”，返回的是float类型。
- 格式化的时间字符串(Format String)
- 结构化的时间(struct_time)：struct_time元组共有9个元素共九个元素:(年，月，日，时，分，秒，一年中第几周，一年中第几天，夏令时)

```
1 import time
2 #--------------------------我们先以当前时间为准,让大家快速认识三种形式的时间
3 print(time.time()) # 时间戳:1487130156.419527
4 print(time.strftime("%Y-%m-%d %X")) #格式化的时间字符串:'2017-02-15 11:40:53'
5 
6 print(time.localtime()) #本地时区的struct_time
7 print(time.gmtime())    #UTC时区的struct_time
```

datetime

```
import datetime

# print(datetime.datetime.now()) #返回 2016-08-19 12:47:03.941925
#print(datetime.date.fromtimestamp(time.time()) )  # 时间戳直接转成日期格式 2016-08-19
# print(datetime.datetime.now() )
# print(datetime.datetime.now() + datetime.timedelta(3)) #当前时间+3天
# print(datetime.datetime.now() + datetime.timedelta(-3)) #当前时间-3天
# print(datetime.datetime.now() + datetime.timedelta(hours=3)) #当前时间+3小时
# print(datetime.datetime.now() + datetime.timedelta(minutes=30)) #当前时间+30分


#
# c_time  = datetime.datetime.now()
# print(c_time.replace(minute=3,hour=2)) #时间替换
```

#### 2，random

```
 1 import random
 2  
 3 print(random.random())#(0,1)----float    大于0且小于1之间的小数
 4  
 5 print(random.randint(1,3))  #[1,3]    大于等于1且小于等于3之间的整数
 6  
 7 print(random.randrange(1,3)) #[1,3)    大于等于1且小于3之间的整数
 8  
 9 print(random.choice([1,'23',[4,5]]))#1或者23或者[4,5]
10  
11 print(random.sample([1,'23',[4,5]],2))#列表元素任意2个组合
12  
13 print(random.uniform(1,3))#大于1小于3的小数，如1.927109612082716 
14  
15  
16 item=[1,3,5,7,9]
17 random.shuffle(item) #打乱item的顺序,相当于"洗牌"
18 print(item)
```

#### 3，os

```
os.getcwd() 获取当前工作目录，即当前python脚本工作的目录路径
os.chdir("dirname")  改变当前脚本工作目录；相当于shell下cd
os.curdir  返回当前目录: ('.')
os.pardir  获取当前目录的父目录字符串名：('..')
os.makedirs('dirname1/dirname2')    可生成多层递归目录
os.removedirs('dirname1')    若目录为空，则删除，并递归到上一级目录，如若也为空，则删除，依此类推
os.mkdir('dirname')    生成单级目录；相当于shell中mkdir dirname
os.rmdir('dirname')    删除单级空目录，若目录不为空则无法删除，报错；相当于shell中rmdir dirname
os.listdir('dirname')    列出指定目录下的所有文件和子目录，包括隐藏文件，并以列表方式打印
os.remove()  删除一个文件
os.rename("oldname","newname")  重命名文件/目录
os.stat('path/filename')  获取文件/目录信息
os.sep    输出操作系统特定的路径分隔符，win下为"\\",Linux下为"/"
os.linesep    输出当前平台使用的行终止符，win下为"\t\n",Linux下为"\n"
os.pathsep    输出用于分割文件路径的字符串 win下为;,Linux下为:
os.name    输出字符串指示当前使用平台。win->'nt'; Linux->'posix'
os.system("bash command")  运行shell命令，直接显示
os.environ  获取系统环境变量
os.path.abspath(path)  返回path规范化的绝对路径
os.path.split(path)  将path分割成目录和文件名二元组返回
os.path.dirname(path)  返回path的目录。其实就是os.path.split(path)的第一个元素
os.path.basename(path)  返回path最后的文件名。如何path以／或\结尾，那么就会返回空值。即os.path.split(path)的第二个元素
os.path.exists(path)  如果path存在，返回True；如果path不存在，返回False
os.path.isabs(path)  如果path是绝对路径，返回True
os.path.isfile(path)  如果path是一个存在的文件，返回True。否则返回False
os.path.isdir(path)  如果path是一个存在的目录，则返回True。否则返回False
os.path.join(path1[, path2[, ...]])  将多个路径组合后返回，第一个绝对路径之前的参数将被忽略
os.path.getatime(path)  返回path所指向的文件或者目录的最后存取时间
os.path.getmtime(path)  返回path所指向的文件或者目录的最后修改时间
os.path.getsize(path) 返回path的大小
```

#### 4，sys

```
1 sys.argv           命令行参数List，第一个元素是程序本身路径
2 sys.exit(n)        退出程序，正常退出时exit(0)
3 sys.version        获取Python解释程序的版本信息
4 sys.maxint         最大的Int值
5 sys.path           返回模块的搜索路径，初始化时使用PYTHONPATH环境变量的值
6 sys.platform       返回操作系统平台名称
```

5，shutil

高级的 文件、文件夹、压缩包 处理模块

**shutil.copyfileobj(fsrc, fdst[, length])**
将文件内容拷贝到另一个文件中

```
1 import shutil
2  
3 shutil.copyfileobj(open('old.xml','r'), open('new.xml', 'w'))
```

 

**shutil.copyfile(src, dst)**
拷贝文件

```
1 shutil.copyfile('f1.log', 'f2.log') #目标文件无需存在
```

 

**shutil.copymode(src, dst)**
仅拷贝权限。内容、组、用户均不变

```
1 shutil.copymode('f1.log', 'f2.log') #目标文件必须存在
```

 

**shutil.copystat(src, dst)**
仅拷贝状态的信息，包括：mode bits, atime, mtime, flags

```
1 shutil.copystat('f1.log', 'f2.log') #目标文件必须存在
```

 

**shutil.copy(src, dst)**
拷贝文件和权限

```
1 import shutil
2  
3 shutil.copy('f1.log', 'f2.log')
```

 

**shutil.copy2(src, dst)**
拷贝文件和状态信息

```
1 import shutil
2  
3 shutil.copy2('f1.log', 'f2.log')
```

 

**shutil.ignore_patterns(\*patterns)**
**shutil.copytree(src, dst, symlinks=False, ignore=None)**
递归的去拷贝文件夹

```
1 import shutil
2  
3 shutil.copytree('folder1', 'folder2', ignore=shutil.ignore_patterns('*.pyc', 'tmp*')) #目标目录不能存在，注意对folder2目录父级目录要有可写权限，ignore的意思是排除 
```

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) 拷贝软连接

 

**shutil.rmtree(path[, ignore_errors[, onerror]])**
递归的去删除文件

```
1 import shutil
2  
3 shutil.rmtree('folder1')
```

 

**shutil.move(src, dst)**
递归的去移动文件，它类似mv命令，其实就是重命名。

```
1 import shutil
2  
3 shutil.move('folder1', 'folder3')
```

 

**shutil.make_archive(base_name, format,...)**

创建压缩包并返回文件路径，例如：zip、tar

创建压缩包并返回文件路径，例如：zip、tar

- base_name： 压缩包的文件名，也可以是压缩包的路径。只是文件名时，则保存至当前目录，否则保存至指定路径，
  如 data_bak            =>保存至当前路径
  如：/tmp/data_bak =>保存至/tmp/
- format：	压缩包种类，“zip”, “tar”, “bztar”，“gztar”
- root_dir：	要压缩的文件夹路径（默认当前目录）
- owner：	用户，默认当前用户
- group：	组，默认当前组
- logger：	用于记录日志，通常是logging.Logger对象

```
1 #将 /data 下的文件打包放置当前程序目录
2 import shutil
3 ret = shutil.make_archive("data_bak", 'gztar', root_dir='/data')
4   
5   
6 #将 /data下的文件打包放置 /tmp/目录
7 import shutil
8 ret = shutil.make_archive("/tmp/data_bak", 'gztar', root_dir='/data') 
```

shutil 对压缩包的处理是调用 ZipFile 和 TarFile 两个模块来进行的，详细：

```
import zipfile

# 压缩
z = zipfile.ZipFile('laxi.zip', 'w')
z.write('a.log')
z.write('data.data')
z.close()

# 解压
z = zipfile.ZipFile('laxi.zip', 'r')
z.extractall(path='.')
z.close()
```



```
import tarfile

# 压缩
>>> t=tarfile.open('/tmp/egon.tar','w')
>>> t.add('/test1/a.py',arcname='a.bak')
>>> t.add('/test1/b.py',arcname='b.bak')
>>> t.close()


# 解压
>>> t=tarfile.open('/tmp/egon.tar','r')
>>> t.extractall('/egon')
>>> t.close()
```

#### 6，json&pickle模块

用eval内置方法可以将一个字符串转成python对象

**什么是序列化？**

我们把对象(变量)从内存中变成可存储或传输的过程称之为序列化，在Python中叫pickling，在其他语言中也被称之为serialization，marshalling，flattening等等，都是一个意思。

**为什么要序列化？**

1：持久保存状态

需知一个软件/程序的执行就在处理一系列状态的变化，在编程语言中，'状态'会以各种各样有结构的数据类型(也可简单的理解为变量)的形式被保存在内存中。

内存是无法永久保存数据的，当程序运行了一段时间，我们断电或者重启程序，内存中关于这个程序的之前一段时间的数据（有结构）都被清空了。

在断电或重启程序之前将程序当前内存中所有的数据都保存下来（保存到文件中），以便于下次程序执行能够从文件中载入之前的数据，然后继续执行，这就是序列化。

具体的来说，你玩使命召唤闯到了第13关，你保存游戏状态，关机走人，下次再玩，还能从上次的位置开始继续闯关。或如，虚拟机状态的挂起等。

2：跨平台数据交互

序列化之后，不仅可以把序列化后的内容写入磁盘，还可以通过网络传输到别的机器上，如果收发的双方约定好实用一种序列化的格式，那么便打破了平台/语言差异化带来的限制，实现了跨平台数据交互。

反过来，把变量内容从序列化的对象重新读到内存里称之为反序列化，即unpickling。



#### 7，logging

**一 日志级别**

```
CRITICAL = 50 #FATAL = CRITICAL
ERROR = 40
WARNING = 30 #WARN = WARNING
INFO = 20
DEBUG = 10
NOTSET = 0 #不设置
```

二 默认级别为warning，默认打印到终端

```
import logging

logging.debug('调试debug')
logging.info('消息info')
logging.warning('警告warn')
logging.error('错误error')
logging.critical('严重critical')

'''
WARNING:root:警告warn
ERROR:root:错误error
CRITICAL:root:严重critical
'''
```

三 为logging模块指定全局配置，针对所有logger有效，控制打印到文件中

```
可在logging.basicConfig()函数中通过具体参数来更改logging模块默认行为，可用参数有
filename：用指定的文件名创建FiledHandler（后边会具体讲解handler的概念），这样日志会被存储在指定的文件中。
filemode：文件打开方式，在指定了filename时使用这个参数，默认值为“a”还可指定为“w”。
format：指定handler使用的日志显示格式。 
datefmt：指定日期时间格式。 
level：设置rootlogger（后边会讲解具体概念）的日志级别 
stream：用指定的stream创建StreamHandler。可以指定输出到sys.stderr,sys.stdout或者文件，默认为sys.stderr。若同时列出了filename和stream两个参数，则stream参数会被忽略。



#格式
%(name)s：Logger的名字，并非用户名，详细查看

%(levelno)s：数字形式的日志级别

%(levelname)s：文本形式的日志级别

%(pathname)s：调用日志输出函数的模块的完整路径名，可能没有

%(filename)s：调用日志输出函数的模块的文件名

%(module)s：调用日志输出函数的模块名

%(funcName)s：调用日志输出函数的函数名

%(lineno)d：调用日志输出函数的语句所在的代码行

%(created)f：当前时间，用UNIX标准的表示时间的浮 点数表示

%(relativeCreated)d：输出日志信息时的，自Logger创建以 来的毫秒数

%(asctime)s：字符串形式的当前时间。默认格式是 “2003-07-08 16:49:45,896”。逗号后面的是毫秒

%(thread)d：线程ID。可能没有

%(threadName)s：线程名。可能没有

%(process)d：进程ID。可能没有

%(message)s：用户输出的消息

 
```

```
#======介绍
可在logging.basicConfig()函数中可通过具体参数来更改logging模块默认行为，可用参数有
filename：用指定的文件名创建FiledHandler（后边会具体讲解handler的概念），这样日志会被存储在指定的文件中。
filemode：文件打开方式，在指定了filename时使用这个参数，默认值为“a”还可指定为“w”。
format：指定handler使用的日志显示格式。
datefmt：指定日期时间格式。
level：设置rootlogger（后边会讲解具体概念）的日志级别
stream：用指定的stream创建StreamHandler。可以指定输出到sys.stderr,sys.stdout或者文件，默认为sys.stderr。若同时列出了filename和stream两个参数，则stream参数会被忽略。


format参数中可能用到的格式化串：
%(name)s Logger的名字
%(levelno)s 数字形式的日志级别
%(levelname)s 文本形式的日志级别
%(pathname)s 调用日志输出函数的模块的完整路径名，可能没有
%(filename)s 调用日志输出函数的模块的文件名
%(module)s 调用日志输出函数的模块名
%(funcName)s 调用日志输出函数的函数名
%(lineno)d 调用日志输出函数的语句所在的代码行
%(created)f 当前时间，用UNIX标准的表示时间的浮 点数表示
%(relativeCreated)d 输出日志信息时的，自Logger创建以 来的毫秒数
%(asctime)s 字符串形式的当前时间。默认格式是 “2003-07-08 16:49:45,896”。逗号后面的是毫秒
%(thread)d 线程ID。可能没有
%(threadName)s 线程名。可能没有
%(process)d 进程ID。可能没有
%(message)s用户输出的消息

#========使用
import logging
logging.basicConfig(filename='access.log',
                    format='%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
                    datefmt='%Y-%m-%d %H:%M:%S %p',
                    level=10)

logging.debug('调试debug')
logging.info('消息info')
logging.warning('警告warn')
logging.error('错误error')
logging.critical('严重critical')





#========结果
access.log内容:
2017-07-28 20:32:17 PM - root - DEBUG -test:  调试debug
2017-07-28 20:32:17 PM - root - INFO -test:  消息info
2017-07-28 20:32:17 PM - root - WARNING -test:  警告warn
2017-07-28 20:32:17 PM - root - ERROR -test:  错误error
2017-07-28 20:32:17 PM - root - CRITICAL -test:  严重critical

part2: 可以为logging模块指定模块级的配置,即所有logger的配置
```

四 logging模块的Formatter，Handler，Logger，Filter对象

```
#logger：产生日志的对象

#Filter：过滤日志的对象

#Handler：接收日志然后控制打印到不同的地方，FileHandler用来打印到文件中，StreamHandler用来打印到终端

#Formatter对象：可以定制不同的日志格式对象，然后绑定给不同的Handler对象使用，以此来控制不同的Handler的日志格式
```

```
import logging

#1、logger对象：负责产生日志，然后交给Filter过滤，然后交给不同的Handler输出
logger=logging.getLogger(__file__)

#2、Filter对象：不常用，略

#3、Handler对象：接收logger传来的日志，然后控制输出
h1=logging.FileHandler('t1.log') #打印到文件
h2=logging.FileHandler('t2.log') #打印到文件
h3=logging.StreamHandler() #打印到终端

#4、Formatter对象：日志格式
formmater1=logging.Formatter('%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
                    datefmt='%Y-%m-%d %H:%M:%S %p',)

formmater2=logging.Formatter('%(asctime)s :  %(message)s',
                    datefmt='%Y-%m-%d %H:%M:%S %p',)

formmater3=logging.Formatter('%(name)s %(message)s',)


#5、为Handler对象绑定格式
h1.setFormatter(formmater1)
h2.setFormatter(formmater2)
h3.setFormatter(formmater3)

#6、将Handler添加给logger并设置日志级别
logger.addHandler(h1)
logger.addHandler(h2)
logger.addHandler(h3)
logger.setLevel(10)

#7、测试
logger.debug('debug')
logger.info('info')
logger.warning('warning')
logger.error('error')
logger.critical('critical')
```

五 Logger与Handler的级别

**logger是第一级过滤，然后才能到handler，我们可以给logger和handler同时设置level，但是需要注意的是**

```
Logger is also the first to filter the message based on a level — if you set the logger to INFO, and all handlers to DEBUG, you still won't receive DEBUG messages on handlers — they'll be rejected by the logger itself. If you set logger to DEBUG, but all handlers to INFO, you won't receive any DEBUG messages either — because while the logger says "ok, process this", the handlers reject it (DEBUG < INFO).



#验证
import logging


form=logging.Formatter('%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
                    datefmt='%Y-%m-%d %H:%M:%S %p',)

ch=logging.StreamHandler()

ch.setFormatter(form)
# ch.setLevel(10)
ch.setLevel(20)

l1=logging.getLogger('root')
# l1.setLevel(20)
l1.setLevel(10)
l1.addHandler(ch)

l1.debug('l1 debug')
```

**==========================直奔主题版============================**

1、日志级别与配置

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import logging

# 一：日志配置
logging.basicConfig(
    # 1、日志输出位置：1、终端 2、文件
    # filename='access.log', # 不指定，默认打印到终端

    # 2、日志格式
    format='%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',

    # 3、时间格式
    datefmt='%Y-%m-%d %H:%M:%S %p',

    # 4、日志级别
    # critical => 50
    # error => 40
    # warning => 30
    # info => 20
    # debug => 10
    level=30,
)

# 二：输出日志
logging.debug('调试debug')
logging.info('消息info')
logging.warning('警告warn')
logging.error('错误error')
logging.critical('严重critical')

'''
# 注意下面的root是默认的日志名字
WARNING:root:警告warn
ERROR:root:错误error
CRITICAL:root:严重critical
'''
```

2、日志配置字典

```
"""
logging配置
"""

import os

# 1、定义三种日志输出格式，日志中可能用到的格式化串如下
# %(name)s Logger的名字
# %(levelno)s 数字形式的日志级别
# %(levelname)s 文本形式的日志级别
# %(pathname)s 调用日志输出函数的模块的完整路径名，可能没有
# %(filename)s 调用日志输出函数的模块的文件名
# %(module)s 调用日志输出函数的模块名
# %(funcName)s 调用日志输出函数的函数名
# %(lineno)d 调用日志输出函数的语句所在的代码行
# %(created)f 当前时间，用UNIX标准的表示时间的浮 点数表示
# %(relativeCreated)d 输出日志信息时的，自Logger创建以 来的毫秒数
# %(asctime)s 字符串形式的当前时间。默认格式是 “2003-07-08 16:49:45,896”。逗号后面的是毫秒
# %(thread)d 线程ID。可能没有
# %(threadName)s 线程名。可能没有
# %(process)d 进程ID。可能没有
# %(message)s用户输出的消息

# 2、强调：其中的%(name)s为getlogger时指定的名字
standard_format = '[%(asctime)s][%(threadName)s:%(thread)d][task_id:%(name)s][%(filename)s:%(lineno)d]' \
                  '[%(levelname)s][%(message)s]'

simple_format = '[%(levelname)s][%(asctime)s][%(filename)s:%(lineno)d]%(message)s'

test_format = '%(asctime)s] %(message)s'

# 3、日志配置字典
LOGGING_DIC = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'standard': {
            'format': standard_format
        },
        'simple': {
            'format': simple_format
        },
        'test': {
            'format': test_format
        },
    },
    'filters': {},
    'handlers': {
        #打印到终端的日志
        'console': {
            'level': 'DEBUG',
            'class': 'logging.StreamHandler',  # 打印到屏幕
            'formatter': 'simple'
        },
        #打印到文件的日志,收集info及以上的日志
        'default': {
            'level': 'DEBUG',
            'class': 'logging.handlers.RotatingFileHandler',  # 保存到文件,日志轮转
            'formatter': 'standard',
            # 可以定制日志文件路径
            # BASE_DIR = os.path.dirname(os.path.abspath(__file__))  # log文件的目录
            # LOG_PATH = os.path.join(BASE_DIR,'a1.log')
            'filename': 'a1.log',  # 日志文件
            'maxBytes': 1024*1024*5,  # 日志大小 5M
            'backupCount': 5,
            'encoding': 'utf-8',  # 日志文件的编码，再也不用担心中文log乱码了
        },
        'other': {
            'level': 'DEBUG',
            'class': 'logging.FileHandler',  # 保存到文件
            'formatter': 'test',
            'filename': 'a2.log',
            'encoding': 'utf-8',
        },
    },
    'loggers': {
        #logging.getLogger(__name__)拿到的logger配置
        '': {
            'handlers': ['default', 'console'],  # 这里把上面定义的两个handler都加上，即log数据既写入文件又打印到屏幕
            'level': 'DEBUG', # loggers(第一层日志级别关限制)--->handlers(第二层日志级别关卡限制)
            'propagate': False,  # 默认为True，向上（更高level的logger）传递，通常设置为False即可，否则会一份日志向上层层传递
        },
        '专门的采集': {
            'handlers': ['other',],
            'level': 'DEBUG',
            'propagate': False,
        },
    },
}
```

3、使用

```
import settings

# !!!强调!!!
# 1、logging是一个包，需要使用其下的config、getLogger，可以如下导入
# from logging import config
# from logging import getLogger

# 2、也可以使用如下导入
import logging.config # 这样连同logging.getLogger都一起导入了,然后使用前缀logging.config.

# 3、加载配置
logging.config.dictConfig(settings.LOGGING_DIC)

# 4、输出日志
logger1=logging.getLogger('用户交易')
logger1.info('egon儿子alex转账3亿冥币')

# logger2=logging.getLogger('专门的采集') # 名字传入的必须是'专门的采集'，与LOGGING_DIC中的配置唯一对应
# logger2.debug('专门采集的日志')
```

#### 8，re

一：什么是正则？

　正则就是用一些具有特殊含义的符号组合到一起（称为正则表达式）来描述字符或者字符串的方法。或者说：正则就是用来描述一类事物的规则。（在Python中）它内嵌在Python中，并通过 re 模块实现。正则表达式模式被编译成一系列的字节码，然后由用 C 编写的匹配引擎执行。

二：常用匹配模式(元字符)

| 字符     | 说明                                                         | Basic RegEx            | Extended RegEx | python RegEx | Perl regEx                                           |
| -------- | ------------------------------------------------------------ | ---------------------- | -------------- | ------------ | ---------------------------------------------------- |
| 转义     |                                                              | \                      | \              | \            | \                                                    |
| ^        | 匹配行首，例如'^dog'匹配以字符串dog开头的行（注意：awk 指令中，'^'则是匹配字符串的开始） | ^                      | ^              | ^            | ^                                                    |
| $        | 匹配行尾，例如：'^、dog$'匹配以字符串 dog 为结尾的行（注意：awk 指令中，'$'则是匹配字符串的结尾） | $                      | $              | $            | $                                                    |
| ^$       | 匹配空行                                                     | ^$                     | ^$             | ^$           | ^$                                                   |
| ^string$ | 匹配行，例如：'^dog$'匹配只含一个字符串 dog 的行             | ^string$               | ^string$       | ^string$     | ^string$                                             |
| \<       | 匹配单词，例如：'\<frog' （等价于'\bfrog'），匹配以 frog 开头的单词 | \<                     | \<             | **不支持**   | **不支持**（但可以使用\b来匹配单词，例如：'\bfrog'） |
| \>       | 匹配单词，例如：'frog\>'（等价于'frog\b '），匹配以 frog 结尾的单词 | \>                     | \>             | **不支持**   | **不支持**（但可以使用\b来匹配单词，例如：'frog\b'） |
| \<x\>    | 匹配一个单词或者一个特定字符，例如：'\<frog\>'（等价于'\bfrog\b'）、'\<G\>' | \<x\>                  | \<x\>          | **不支持**   | **不支持**（但可以使用\b来匹配单词，例如：'\bfrog\b' |
| ()       | 匹配表达式，例如：不支持'（frog）'                           | **不支持**（但可以使用 |                |              |                                                      |

|      | **不支持**（同())                                            | **不支持**（同()) | **不支持**（同()) |      |      |
| ---- | ------------------------------------------------------------ | ----------------- | ----------------- | ---- | ---: |
| ？   | 匹配前面的子表达式 0 次或 1 次（等价于{0,1}），例如：where(is)?能匹配"where" 以及"whereis" | **不支持**（同\?) | ？                | ？   |   ？ |
| \?   | 匹配前面的子表达式 0 次或 1 次（等价于'\{0,1\}'），例如：'where*i**s* |                   |                   |      |      |

| ”\?“ |                                 '能匹配 "where"以及"whereis" | **不支持**（同?) | **不支持**（同?)                                             | **不支持**（同?) |                                                            |
| ---- | -----------------------------------------------------------: | ---------------- | ------------------------------------------------------------ | ---------------- | ---------------------------------------------------------- |
| ?    | 当该字符紧跟在任何一个其他限制符（*, +, ?, {n},{n,}, {n,m}）  后面时，匹配模式是非贪婪的。非贪婪模式尽可能少的匹配所搜索的字符串，而默认的贪婪模式则尽可能多的匹配所搜索的字符串。例如，对于字符串  "oooo"，'o+?' 将匹配单个"o"，而 'o+' 将匹配所有 'o' | **不支持**       | **不支持**                                                   | **不支持**       | **不支持**                                                 |
| .    | 匹配除换行符（'\n'）之外的任意单个字符（注意：awk 指令中的句点能匹配换行符） | .                | .（如果要匹配包括“\n”在内的任何一个字符，请使用：'(^$)\|（.） | .                | .（如果要匹配包括“\n”在内的任何一个字符，请使用：' [.\n] ' |
| *    | 匹配前面的子表达式 0 次或多次（等价于{0, }），例如：zo* 能匹配 "z"以及 "zoo" | *                | *                                                            | *                | *                                                          |
| \+   | 匹配前面的子表达式 1 次或多次（等价于'\{1, \}'），例如：'where*i**s* |                  |                                                              |                  |                                                            |

| “\+ ”     | 匹配前面的子表达式 1 次或多次（等价于'\{1, \}'），例如：'where*i**s*\+ '能匹配 "whereis"以及"whereisis" | **不支持**（同+)       | **不支持**（同+) | **不支持**（同+) |           |
| --------- | ------------------------------------------------------------ | ---------------------- | ---------------- | ---------------- | --------- |
| +         | 匹配前面的子表达式 1 次或多次（等价于{1, }），例如：zo+能匹配 "zo"以及 "zoo"，但不能匹配 "z" | **不支持**（同\+)      | +                | +                | +         |
| {n}       | n 必须是一个 0 或者正整数，匹配子表达式 n 次，例如：zo{2}能匹配 | **不支持**（同\{n\})   | {n}              | {n}              | {n}       |
| {n,}      | "zooz"，但不能匹配 "Bob"n 必须是一个 0 或者正整数，匹配子表达式大于等于 n次，例如：go{2,} | **不支持**（同\{n,\})  | {n,}             | {n,}             | {n,}      |
| {n,m}     | 能匹配 "good"，但不能匹配 godm 和 n 均为非负整数，其中 n <= m，最少匹配 n 次且最多匹配 m 次 ，例如：o{1,3}将配"fooooood" 中的前三个 o（请注意在逗号和两个数之间不能有空格） | **不支持**（同\{n,m\}) | {n,m}            | {n,m}            | {n,m}     |
| x\|y      | 匹配 x 或 y，例如： 不支持'z\|（food）' 能匹配 "z" 或"food"；'（z\|f）ood' 则匹配"zood" 或 "food" | **不支持**（同x\|y)    | x\|y             | x\|y             | x\|y      |
| [0-9]     | 匹配从 0 到 9 中的任意一个数字字符（注意：要写成递增）       | [0-9]                  | [0-9]            | [0-9]            | [0-9]     |
| [xyz]     | 字符集合，匹配所包含的任意一个字符，例如：'[abc]'可以匹配"lay" 中的 'a'（注意：如果元字符，例如：. *等，它们被放在[ ]中，那么它们将变成一个普通字符） | [xyz]                  | [xyz]            | [xyz]            | [xyz]     |
| [^xyz]    | 负值字符集合，匹配未包含的任意一个字符（注意：不包括换行符），例如：'[^abc]' 可以匹配 "Lay" 中的'L'（注意：[^xyz]在awk 指令中则是匹配未包含的任意一个字符+换行符） | [^xyz]                 | [^xyz]           | [^xyz]           | [^xyz]    |
| [A-Za-z]  | 匹配大写字母或者小写字母中的任意一个字符（注意：要写成递增） | [A-Za-z]               | [A-Za-z]         | [A-Za-z]         | [A-Za-z]  |
| [^A-Za-z] | 匹配除了大写与小写字母之外的任意一个字符（注意：写成递增）   | [^A-Za-z]              | [^A-Za-z]        | [^A-Za-z]        | [^A-Za-z] |
| **\d**    | 匹配从 0 到 9 中的任意一个数字字符（等价于 [0-9]）           | **不支持**             | **不支持**       | \d               | \d        |
| **\D**    | 匹配非数字字符（等价于 [^0-9]）                              | **不支持**             | **不支持**       | \D               | \D        |
| \S        | 匹配任何非空白字符（等价于[^\f\n\r\t\v]）                    | **不支持**             | **不支持**       | \S               | \S        |
| \s        | 匹配任何空白字符，包括空格、制表符、换页符等等（等价于[ \f\n\r\t\v]） | **不支持**             | **不支持**       | \s               | \s        |
| \W        | 匹配任何非单词字符 (等价于[^A-Za-z0-9_])                     | \W                     | \W               | \W               | \W        |
| \w        | 匹配包括下划线的任何单词字符（等价于[A-Za-z0-9_]）           | \w                     | \w               | \w               | \w        |
| \B        | 匹配非单词边界，例如：'er\B' 能匹配 "verb" 中的'er'，但不能匹配"never" 中的'er' | \B                     | \B               | \B               | \B        |
| \b        | 匹配一个单词边界，也就是指单词和空格间的位置，例如： 'er\b' 可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的'er' | \b                     | \b               | \b               | \b        |
| \t        | 匹配一个横向制表符（等价于 \x09和 \cI）                      | **不支持**             | **不支持**       | \t               | \t        |
| \v        | 匹配一个垂直制表符（等价于 \x0b和 \cK）                      | **不支持**             | **不支持**       | \v               | \v        |
| \n        | 匹配一个换行符（等价于 \x0a 和\cJ）                          | **不支持**             | **不支持**       | \n               | \n        |
| \f        | 匹配一个换页符（等价于\x0c 和\cL）                           | **不支持**             | **不支持**       | \f               | \f        |
| \r        | 匹配一个回车符（等价于 \x0d 和\cM）                          | **不支持**             | **不支持**       | \r               | \r        |
| \\        | 匹配转义字符本身"\"                                          | \\                     | \\               | \\               | \\        |
| \cx       | 匹配由 x 指明的控制字符，例如：\cM匹配一个Control-M 或回车符，x 的值必须为A-Z 或 a-z 之一，否则，将 c 视为一个原义的 'c' 字符 | **不支持**             | **不支持**       |                  | \cx       |
| \xn       | 匹配 n，其中 n 为十六进制转义值。十六进制转义值必须为确定的两个数字长，例如：'\x41' 匹配 "A"。'\x041' 则等价于'\x04' & "1"。正则表达式中可以使用 ASCII 编码 | **不支持**             | **不支持**       |                  | \xn       |
| \num      | 匹配 num，其中 num是一个正整数。表示对所获取的匹配的引用     | **不支持**             | \num             | \num             |           |
| [:alnum:] | 匹配任何一个字母或数字（[A-Za-z0-9]），例如：'[[:alnum:]] '  | [:alnum:]              | [:alnum:]        | [:alnum:]        | [:alnum:] |
| [:alpha:] | 匹配任何一个字母（[A－Za－z]）， 例如：' [[:alpha:]] '       | [:alpha:]              | [:alpha:]        | [:alpha:]        | [:alpha:] |
| [:digit:] | 匹配任何一个数字（[0-9]），例如：'[[:digit:]] '              | [:digit:]              | [:digit:]        | [:digit:]        | [:digit:] |
| [:lower:] | 匹配任何一个小写字母（[a-z]）， 例如：' [[:lower:]] '        | [:lower:]              | [:lower:]        | [:lower:]        | [:lower:] |
| [:upper:] | 匹配任何一个大写字母（[A-Z]）                                | [:upper:]              | [:upper:]        | [:upper:]        | [:upper:] |
| [:space:] | 任何一个空白字符： 支持制表符、空格，例如：' [[:space:]] '   | [:space:]              | [:space:]        | [:space:]        | [:space:] |
| [:blank:] | 空格和制表符（横向和纵向），例如：'[[:blank:]]'ó'[\s\t\v]'   | [:blank:]              | [:blank:]        | [:blank:]        | [:blank:] |
| [:graph:] | 任何一个可以看得见的且可以打印的字符（注意：不包括空格和换行符等），例如：'[[:graph:]] ' | [:graph:]              | [:graph:]        | [:graph:]        | [:graph:] |
| [:print:] | 任何一个可以打印的字符（注意：不包括：[:cntrl:]、字符串结束符'\0'、EOF 文件结束符（-1）， 但包括空格符号），例如：'[[:print:]] ' | [:print:]              | [:print:]        | [:print:]        | [:print:] |

```
# =================================匹配模式=================================
#一对一的匹配
# 'hello'.replace(old,new)
# 'hello'.find('pattern')

#正则匹配
import re
#\w与\W
print(re.findall('\w','hello egon 123')) #['h', 'e', 'l', 'l', 'o', 'e', 'g', 'o', 'n', '1', '2', '3']
print(re.findall('\W','hello egon 123')) #[' ', ' ']

#\s与\S
print(re.findall('\s','hello  egon  123')) #[' ', ' ', ' ', ' ']
print(re.findall('\S','hello  egon  123')) #['h', 'e', 'l', 'l', 'o', 'e', 'g', 'o', 'n', '1', '2', '3']

#\n \t都是空,都可以被\s匹配
print(re.findall('\s','hello \n egon \t 123')) #[' ', '\n', ' ', ' ', '\t', ' ']

#\n与\t
print(re.findall(r'\n','hello egon \n123')) #['\n']
print(re.findall(r'\t','hello egon\t123')) #['\n']

#\d与\D
print(re.findall('\d','hello egon 123')) #['1', '2', '3']
print(re.findall('\D','hello egon 123')) #['h', 'e', 'l', 'l', 'o', ' ', 'e', 'g', 'o', 'n', ' ']

#\A与\Z
print(re.findall('\Ahe','hello egon 123')) #['he'],\A==>^
print(re.findall('123\Z','hello egon 123')) #['he'],\Z==>$
```

^ 
指定匹配必须出现在字符串的开头或行的开头。

\A 
指定匹配必须出现在字符串的开头（忽略 Multiline 选项）。

$ 
指定匹配必须出现在以下位置：字符串结尾、字符串结尾的 \n 之前或行的结尾。

\Z 
指定匹配必须出现在字符串的结尾或字符串结尾的 \n 之前（忽略 Multiline 选项）。

```
#^与$
print(re.findall('^h','hello egon 123')) #['h']
print(re.findall('3$','hello egon 123')) #['3']

# 重复匹配：| . | * | ? | .* | .*? | + | {n,m} |
#.
print(re.findall('a.b','a1b')) #['a1b']
print(re.findall('a.b','a1b a*b a b aaab')) #['a1b', 'a*b', 'a b', 'aab']
print(re.findall('a.b','a\nb')) #[]
print(re.findall('a.b','a\nb',re.S)) #['a\nb']
print(re.findall('a.b','a\nb',re.DOTALL)) #['a\nb']同上一条意思一样

#*
print(re.findall('ab*','bbbbbbb')) #[]
print(re.findall('ab*','a')) #['a']
print(re.findall('ab*','abbbb')) #['abbbb']

#?
print(re.findall('ab?','a')) #['a']
print(re.findall('ab?','abbb')) #['ab']
#匹配所有包含小数在内的数字
print(re.findall('\d+\.?\d*',"asdfasdf123as1.13dfa12adsf1asdf3")) #['123', '1.13', '12', '1', '3']

#.*默认为贪婪匹配
print(re.findall('a.*b','a1b22222222b')) #['a1b22222222b']

#.*?为非贪婪匹配：推荐使用
print(re.findall('a.*?b','a1b22222222b')) #['a1b']

#+
print(re.findall('ab+','a')) #[]
print(re.findall('ab+','abbb')) #['abbb']

#{n,m}
print(re.findall('ab{2}','abbb')) #['abb']
print(re.findall('ab{2,4}','abbb')) #['abb']
print(re.findall('ab{1,}','abbb')) #'ab{1,}' ===> 'ab+'
print(re.findall('ab{0,}','abbb')) #'ab{0,}' ===> 'ab*'

#[]
print(re.findall('a[1*-]b','a1b a*b a-b')) #[]内的都为普通字符了，且如果-没有被转意的话，应该放到[]的开头或结尾
print(re.findall('a[^1*-]b','a1b a*b a-b a=b')) #[]内的^代表的意思是取反，所以结果为['a=b']
print(re.findall('a[0-9]b','a1b a*b a-b a=b')) #[]内的^代表的意思是取反，所以结果为['a=b']
print(re.findall('a[a-z]b','a1b a*b a-b a=b aeb')) #[]内的^代表的意思是取反，所以结果为['a=b']
print(re.findall('a[a-zA-Z]b','a1b a*b a-b a=b aeb aEb')) #[]内的^代表的意思是取反，所以结果为['a=b']

#\# print(re.findall('a\\c','a\c')) #对于正则来说a\\c确实可以匹配到a\c,但是在python解释器读取a\\c时，会发生转义，然后交给re去执行，所以抛出异常
print(re.findall(r'a\\c','a\c')) #r代表告诉解释器使用rawstring，即原生字符串，把我们正则内的所有符号都当普通字符处理，不要转义
print(re.findall('a\\\\c','a\c')) #同上面的意思一样，和上面的结果一样都是['a\\c']

#():分组
print(re.findall('ab+','ababab123')) #['ab', 'ab', 'ab']
print(re.findall('(ab)+123','ababab123')) #['ab']，匹配到末尾的ab123中的ab
print(re.findall('(?:ab)+123','ababab123')) #findall的结果不是匹配的全部内容，而是组内的内容,?:可以让结果为匹配的全部内容
print(re.findall('href="(.*?)"','<a href="http://www.baidu.com">点击</a>'))#['http://www.baidu.com']
print(re.findall('href="(?:.*?)"','<a href="http://www.baidu.com">点击</a>'))#['href="http://www.baidu.com"']

#|
print(re.findall('compan(?:y|ies)','Too many companies have gone bankrupt, and the next one is my company'))
```

```
# ===========================re模块提供的方法介绍===========================
import re
#1
print(re.findall('e','alex make love') )   #['e', 'e', 'e'],返回所有满足匹配条件的结果,放在列表里
#2
print(re.search('e','alex make love').group()) #e,只到找到第一个匹配然后返回一个包含匹配信息的对象,该对象可以通过调用group()方法得到匹配的字符串,如果字符串没有匹配，则返回None。

#3
print(re.match('e','alex make love'))    #None,同search,不过在字符串开始处进行匹配,完全可以用search+^代替match

#4
print(re.split('[ab]','abcd'))     #['', '', 'cd']，先按'a'分割得到''和'bcd',再对''和'bcd'分别按'b'分割

#5
print('===>',re.sub('a','A','alex make love')) #===> Alex mAke love，不指定n，默认替换所有
print('===>',re.sub('a','A','alex make love',1)) #===> Alex make love
print('===>',re.sub('a','A','alex make love',2)) #===> Alex mAke love
print('===>',re.sub('^(\w+)(.*?\s)(\w+)(.*?\s)(\w+)(.*?)$',r'\5\2\3\4\1','alex make love')) #===> love make alex

print('===>',re.subn('a','A','alex make love')) #===> ('Alex mAke love', 2),结果带有总共替换的个数


#6
obj=re.compile('\d{2}')

print(obj.search('abc123eeee').group()) #12
print(obj.findall('abc123eeee')) #['12'],重用了obj
```



## 第七章 	面向对象

## 第八章 	网络编程

## 第九章 	并发编程

## 第十章  	数据库

## 第十一章 前端开发

## 第十二章	Django框架





