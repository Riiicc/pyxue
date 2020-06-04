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
```