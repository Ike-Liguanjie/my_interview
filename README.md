# 前言
腾讯面失败后感觉自己需要学习的地方还很多，必须要改变以前的咸鱼状态，不然今后恐怕无缘大厂。<br>
所以总结一些面试官经常回问到的问题或者自己在看书过程中觉得重要的知识点，方便自己以后回顾。<br>

# 目录
* [一、Python](#Python)
    * [1 深浅拷贝](#1-深浅拷贝)
    * [2 装饰器](#2-装饰器)
    * [3 Python协议](#3-Python协议)
* [二、数据库](#数据库)
*     * [1 MySQL](#1-MySQL)
* [三、网络]
* [四、操作系统]
* [五、分布式及高并发]

# Python
为什么会有Python？因为我就是写Python的呗
## 1 深浅拷贝
深拷贝不用多说，完全新建一个内存地址将内容拷贝出来，修改不会影响到原来的数据，这里主要讲一下浅拷贝。<br>
在浅拷贝时候要注意，原对象中的可变元素是拷贝引用，修改会影响原有数据！<br>
什么意思呢，举个简单例子：<br>
```
a = (1, [1, 2], {1, 2}, 4)
b = list(a)
b[1].append(3)
b[2].add(3)
b.append(5)
print(a)
print(b)
```
这个时候的打印结果会是:<br>
```
(1, [1, 2, 3], {1, 2, 3}, 4)
[1, [1, 2, 3], {1, 2, 3}, 4, 5]
```
可以发现在单纯对b进行append的时候，a是不会发生改变的，但是对里面的list和set做操作时，原有数据就会发生改变。<br>
__注意：list()方法和列表生成器、字典生成器都属于浅拷贝。__<br>

## 2 装饰器
首先要知道装饰器是干什么的，我理解的装饰器就是在不干涉原有代码运行的前提下，做一些你想要做的事情，比如获取程序的运行时间、打印日志等等。
```
def do_something(func):
    def print_content():
        print('do something before')
        f = func()
        print('do something after')
        return f

    return print_content


@do_something
def hello_world():
    print('Hello world!')


if __name__ == '__main__':
    hello_world()
```
运行程序，控制台打印内容：
```
do something before
Hello world!
do something after
```
这就是一个很简单的装饰器，可以看到装饰器实际上是把被装饰的方法作为参数放到装饰器中运行，在print_content()中将参数方法返回给外层，在外层再将print_content返回给装饰器就可以了。<br>
__这里可能会感觉装饰器的写法比较像闭包，其实装饰器就是闭包，返回的是方法而不是结果。__<br>

## 3 Python协议
这个是在面试某个公司，面试官给的一道题目里接触到的。<br>
面试让我实现一个对象，创建这个对象的时候传一个带有空格的字符串例如"Hello world!"，创建的这个对象要能用for循环取出空格分割的"Hello"和"world"，用len()能得到分割后的长度。<br>
这个我当时知道意思是让我模拟列表、元组那些实现一个迭代器，虽然面试官有提醒我根据Python的协议去做，但具体怎么去实现，我当时毫无头绪，面试也就理所当然的挂了。<br>
下来之后查了一下，Python的对象是有一些自带的方法的，那个就是Python的协议。<br>
比如一个类你写了__init__就是初始化的方法，而__new__就是新建对象的时候调用。<br>
为什么list能被for循环，是因为内部实现了__iter__和__next__，而len()则是实现了__len__，这个感兴趣的可以下来看看。<br>

# 数据库
## 1 MySQL
