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

# list可以包含list（二维数组）
s = ['python', 'java', ['asp', 'php'], 'scheme']

```