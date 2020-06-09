### 高级特性
#### 切片：针对list 和tuple
```
# L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3。即索引0，1，2，正好是3个元素
# Python支持L[-1]取倒数第一个元素，那么它同样支持倒数切片
L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
>>> L[0:3]
['Michael', 'Sarah', 'Tracy']

>>> L[:3]
['Michael', 'Sarah', 'Tracy']

>>> L[-2:]
['Bob', 'Jack']

>>> L[-2:-1]
['Bob']
# 特殊方法
[begin:end:step]
[:10:2] #前十个 每两个取一个

# tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，只是操作的结果仍是tuple
# 字符串'xxx'也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，只是操作结果仍是字符串
```
---
#### 迭代
通过for循环来遍历list或tuple dict  
因为dict的存储不是按照list的方式顺序排列，所以，迭代出的结果顺序很可能不一样。  
默认情况下，dict迭代的是key。如果要迭代value，可以用for value in d.values()，如果要同时迭代key和value，可以用for k, v in d.items()。  
```
>>> d = {'a': 1, 'b': 2, 'c': 3}
>>> for key in d:
...     print(key)
...
a
c
b

# 通过collections模块的Iterable类型判断是否可迭代
>>> from collections import Iterable
>>> isinstance('abc', Iterable) # str是否可迭代
True
>>> isinstance([1,2,3], Iterable) # list是否可迭代
True
>>> isinstance(123, Iterable) # 整数是否可迭代
False

# 内置的enumerate函数可以把一个list变成索引-元素对
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C

```
---
#### 列表生成式

```
# for循环后面还可以加上if判断，这样我们就可以筛选出仅偶数的平方：
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]

>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']

>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> [k + '=' + v for k, v in d.items()]
['y=B', 'x=A', 'z=C']

>>> [x if x % 2 == 0 else -x for x in range(1, 11)]
[-1, 2, -3, 4, -5, 6, -7, 8, -9, 10]
```
#### 生成器
```
>>> L = [x * x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>
#创建L和g的区别仅在于最外层的[]和()，L是一个list，而g是一个generator(生成器)
# 使用next(g)来获取下一个生成器的内容 或者使用for循环 for x in g
```
#### 迭代器
直接作用于for循环的数据类型有以下几种：  
一类是集合数据类型，如list、tuple、dict、set、str等；  
一类是generator，包括生成器和带yield的generator function。  
这些可以直接作用于for循环的对象统称为可迭代对象：Iterable。  
可以使用isinstance()判断一个对象是否是Iterable对象：  
```
>>> from collections.abc import Iterable
>>> isinstance([], Iterable)
True
>>> isinstance({}, Iterable)
True
>>> isinstance('abc', Iterable)
True
>>> isinstance((x for x in range(10)), Iterable)
True
>>> isinstance(100, Iterable)
False
```
可以被next()函数调用并不断返回下一个值的对象称为迭代器：Iterator。

可以使用isinstance()判断一个对象是否是Iterator对象：
```
#生成器都是Iterator对象，但list、dict、str虽然是Iterable，却不是Iterator。
#把list、dict、str等Iterable变成Iterator可以使用iter()函数：

#凡是可作用于for循环的对象都是Iterable类型；
#凡是可作用于next()函数的对象都是Iterator类型，它们表示一个惰性计算的序列；
#集合数据类型如list、dict、str等是Iterable但不是Iterator，不过可以通过iter()函数获得一个Iterator对象。


# Iterable ->for 可迭代
# Iterator ->for 可迭代并且 next() 可以获取下一个值
```


### 函数式编程
#### 高阶函数
```
def add(x, y, f):
    return f(x) + f(y) 
# 当我们调用add(-5, 6, abs)时，参数x，y和f分别接收-5，6和abs，根据函数定义，我们可以推导计算过程为：
x = -5
y = 6
f = abs
f(x) + f(y) ==> abs(-5) + abs(6) ==> 11
return 11
```

#### map/reduce
```
map
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]

# reduce
>>> from functools import reduce
>>> def fn(x, y):
...     return x * 10 + y
...
>>> reduce(fn, [1, 3, 5, 7, 9])
13579

# map接受一个参数  reduce 接受两个参数
```
#### filter
```
# 和map()类似，filter()也接收一个函数和一个序列。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。
def is_odd(n):
    return n % 2 == 1

list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
# 结果: [1, 5, 9, 15]
```

#### sorted
```
>>> sorted([36, 5, -12, 9, -21])
[-21, -12, 5, 9, 36]
# sorted()函数也是一个高阶函数，它还可以接收一个key函数来实现自定义的排序
# 按绝对值大小排序
>>> sorted([36, 5, -12, 9, -21], key=abs)
[5, 9, -12, -21, 36]

# 对字符排序默认为ASCII的大小比较的，使用下面的key可以忽略大小写进行排序
>>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower)
['about', 'bob', 'Credit', 'Zoo']
```

#### 返回函数  闭包
```
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum

# 调用lazy_sum()时，返回的并不是求和结果，而是求和函数：
>>> f = lazy_sum(1, 3, 5, 7, 9)
>>> f
# 调用函数f时，才真正计算求和的结果：
>>> f()
25
```
#### 匿名函数 lambda表达式
```
#  匿名函数lambda x: x * x实际上就是：冒号前面的x表示函数参数
def f(x):
    return x * x
```

#### 装饰器 （目前理解为注解）
函数也是一个对象，而且函数对象可以被赋值给变量  
函数对象有一个__name__属性，可以拿到函数的名字，固定属性 
```
def fun():
    pass

fun.__name__ = 'fun'
```
在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）  
```
# decorator就是一个返回函数的高阶函数。所以，我们要定义一个能打印日志的decorator，可以定义如下：
def log(func):
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper

@log
def now():
    print('2015-3-25')

# 调用now
>>> now()
call now():
2015-3-25
```

#### 偏函数
```
# functools.partial就是帮助我们创建一个偏函数的，不需要我们自己定义int2()，可以直接使用下面的代码创建一个新的函数int2：
>>> import functools
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64
>>> int2('1010101')
85
# 总结functools.partial的作用就是，把一个函数的某些参数给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数会更简单。
max2 = functools.partial(max, 10)
实际上会把10作为*args的一部分自动加到左边，也就是：
max2(5, 6, 7)
相当于：
args = (10, 5, 6, 7)
max(*args)
结果为10。

```