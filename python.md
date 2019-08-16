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

6. Python的__name__是当前模块名  
当模块被直接运行时，模块名为原先的模块名  
`if __name__ == '__main__'`的意思就是，当直接运行该模块时，执行后面的代码

7. 装饰器  
装饰器本质是一个Python的函数或类，可以让其他函数或类在不需要做任何代码修改的前提下增加额外功能，常用于有切面需求的场景，比如：插入日志、性能测试、事务处理、缓存、权限校验等  
[理解Python装饰器]:<https://foofish.net/python-decorator.html>

8. 偏函数  
functools模块提供了偏函数功能，简单说，functools.partial作用就是把一个函数的某些参数固定住，返回一个新的函数，这样再调用这个新的函数时，就会更方便地实现一些定制功能  


