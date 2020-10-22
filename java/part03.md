#### 第三章java基本结构
---
> 根据java语言规范 main方法必须声明为public  
> java 注释不会出现在可执行程序中。因此添加注释不必考虑**可执行代码**膨胀  

> java是一种强类型语言，8种基本类型，4种类型，2种浮点类型，1种用于表示Unicode编码字符单元的字符类型char，1种用于表示真值的Boolean类型。

> 从java7开始 以0b或0B为前缀来表示二进制 还可以数字中间添加_ 方便阅读

```
例：0b1111_0100_0010_0100_0000
```

> float类型数值后缀为F或f，没有F后缀的浮点值默认位double

```
if(DOuble.isNaN(x))判断x是否为数值
```

> 浮点数无法精确计算数值，误差主要原因是浮点数值采用二进制表示，而二进制系统无法精确表示1/10，就好像十进制无法精确表示1/3

> 15/2 = 7   
> 15%2 = 1  
> 15.0/2 = 7.5  

> Math.sqrt(a) a的平方根  
> Math.pow(x,a) x的a次幂  
> StrictMath  精确的Math


> 运算符级别注意 ： && >||    a+=b+=c 等同于a+=(b+=c)

> n%2表达式 奇数为1 偶数为2 负数为-1  

> equalsIgnoreCase()方法可以忽略大小写比较是否相等  

> 创建数字数组是所有元素初始化值为0，boolean数组初始化值为false，对象数组的元素默认为null  

> 数组拷贝可以使用Arrays.copyOf(firstAry,firstAry.length)  
> 上述方法可以扩展数组Arrays.copyOf(firstAry,firstAry.length*2) 新数组长度扩展2倍  

```
数组初始化
int[] a = new int[100];//长度100的数组
int a[] = new int[100];//长度100的数组

int[] a = {1,2,3,4,5,6,7,8} //初始化同时赋值

new int[]{2,3,4,5,6,7} //初始化匿名数组

```

> 想要快速打印一个二维数组元素列表，可以直接调用 Arrays.deepToString()



