### 数据类型和变量
整数、浮点、字符串  
字符串：单引号'或双引号"括起来的任意文本，如果字符串内部既包含'又包含"，可以用转义字符\来标识，如'I\'m \"OK\"!'，字符\本身也要转义，所以\\表示的字符就是\   
布尔值：True 和False 大小写敏感，布尔值可以用and、or和not运算。  
空值：空值是Python里一个特殊的值，用None表示。  
变量：变量名必须是大小写英文、数字和_的组合，且不能用数字开头。  
这种变量本身类型不固定的语言称之为动态语言，与之对应的是静态语言。  

---  

### list和tuple  
list是一种有序的集合，可以随时添加和删除其中的元素。  
list里面的元素的数据类型也可以不同  
```
classmates = ['Michael', 'Bob', 'Tracy']
classmates[0]
classmates[-1]
# 添加
classmates.append('Adam')
#插入
classmates.insert(1, 'Jack')
# 删除最后一个
classmates.pop() 
classmates.pop(index)

# list可以包含list（二维数组）
s = ['python', 'java', ['asp', 'php'], 'scheme']

#空list
L = []
len(L) ->0  # 长度为0
```

另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改  
tuple所谓的“不变”是说，tuple的每个元素，指向永远不变。即指向'a'，就不能改成指向'b'，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的  
```
classmates = ('Michael', 'Bob', 'Tracy')
#空tuple
classmates = ()
# 只有1个元素的tuple
classmates = (1,)
```

### 条件判断
```
age = 3
if age >= 18:
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')
```

### dict和set
Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。
```
#获取dict的值
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95

# 判断值是否存在
# 通过in判断key是否存在：
'tom' in d 
# 通过dict提供的get()方法，如果key不存在，可以返回None，或者自己指定的value
d.get('Bob1')
d.get('Bob2',-1)
#  删除一个key，用pop(key)方法


```
set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。  
```
#重复元素在set中自动被过滤
>>> s = set([1, 1, 2, 2, 3, 3])
>>> s
{1, 2, 3}
add(key)方法可以添加元素到set中
通过remove(key)方法可以删除元素
set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```

### 函数
```
# 空函数
def nop():
    pass


```