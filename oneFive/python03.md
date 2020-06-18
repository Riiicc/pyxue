### 面向对象编程
#### 类和实例访问限制
```
# 类构造方法
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score
#__init__方法的第一个参数永远是self，表示创建的实例本身
#创建实例的时候，不能传入空的参数，必须传入与__init__方法匹配的参数

# 内部属性不被外部访问，可以把属性的名称前加上两个下划线__，在Python中，实例的变量名如果以__开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问
# 在Python中，变量名类似__xxx__的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量
```
#### 继承和多态
```
# 父类
class Animal(object):
    def run(self):
        print('Animal is running...')
# 继承Animal
class Dog(Animal):
    pass

class Cat(Animal):
    pass
# 多态同java
```
#### 获取对象信息
```
使用type()函数判断对象类型，基本类型都可以用type()判断
获得一个对象的所有属性和方法，可以使用dir()函数，它返回一个包含字符串的list
len() 返回对象长度  等同于 对象.__len__()

配合getattr()、setattr()以及hasattr()，我们可以直接操作一个对象的状态
>>> hasattr(obj, 'x') # 有属性'x'吗？
True
>>> obj.x
9
>>> hasattr(obj, 'y') # 有属性'y'吗？
False
>>> setattr(obj, 'y', 19) # 设置一个属性'y'
>>> hasattr(obj, 'y') # 有属性'y'吗？
True
>>> getattr(obj, 'y') # 获取属性'y'
19
>>> obj.y # 获取属性'y'
19
>>> getattr(obj, 'z', 404) # 获取属性'z'，如果不存在，返回默认值404
404 
```
#### 实例属性和类属性
```
# 类属性，归类所有
>>> class Student(object):
...     name = 'Student'

# 实例属性
# 实例绑定属性的方法是通过实例变量，或者通过self变量：
class Student(object):
    def __init__(self, name):
        self.name = name

s = Student('Bob')
s.score = 90

# 相同名称的实例属性将屏蔽掉类属性

```
### 面向对象高级编程
#### \_\_slots\_\_
```
__slots__用来限制实例可绑定的属性
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称

使用__slots__要注意，__slots__定义的属性仅对当前类实例起作用，对继承的子类是不起作用，但是子类中也可以定义__slots__，这样，子类实例允许定义的属性就是自身的__slots__加上父类的__slots__

```
#### @property
```
# 替代getter setter

>>> s = Student()
>>> s.score = 60 # OK，实际转化为s.set_score(60)
>>> s.score # OK，实际转化为s.get_score()


class Student(object):

    @property # getter
    def birth(self):
        return self._birth

    @birth.setter # setter
    def birth(self, value):
        self._birth = value

    # 只有property的 为只读（只能getter）
    @property
    def age(self):
        return 2015 - self._birth
```