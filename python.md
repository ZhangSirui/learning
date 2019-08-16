# Python 学习

1. Python在定义类的时候，继承父类object是新式类，Python3中默认所有类都继承object，这么写便于Python2和3统一  

2. Python可以引入ConfigParser来进行配置文件的读取与写入  

3. Python通过uuid模块来生成唯一ID，分为五个算法，使用时通过例如uuid.uuid1()生成

4. 三个函数式编程的内置函数  

| name | function |
| ---- | ---- |
| filter | 把一个函数应用于序列的每一项，保留该函数返回真值时的所有元素 |
| map | 对序列中的每一个元素执行函数 |
| reduce | 对序列前两个元素执行函数，生成的结果 |

5. for循环整个作为参数时，可以整个传入  
如：打印10以内的偶数  
`print [x for x in range(10) if x%2==0]`

6. Python闭包  
闭包避免使用了全局变量，闭包允许函数与其所操作的某些数据相互关联起来
例如：

