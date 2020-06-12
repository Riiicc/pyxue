### 面向对象编程
```
# 类构造方法
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score
#__init__方法的第一个参数永远是self，表示创建的实例本身

# 内部属性不被外部访问，可以把属性的名称前加上两个下划线__，在Python中，实例的变量名如果以__开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问
# 在Python中，变量名类似__xxx__的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量
```