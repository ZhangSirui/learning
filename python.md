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

9. 内置函数enumerate可以遍历并自动计数  
```
for counter, value in enumerate(some_list):
    print(counter, value)
```  
enumerate还可以接收参数，比如`enumerate(list, 1)`表示从第一个开始计数  

10. python字典的keys(), values(), items()都会返回一个list，其中items()返回的是键值对的list  

11. python的\*args和\*\*kwargs是约定生成的，只有前面的\*和\*\*是必须的  
\*args和\*\*kwargs用于函数定义，将不定数量的参数传递给一个函数  
\*args用来发送一个非键值对的可变数量的参数列表给一个函数, \*\*kwargs允许将不定长度的键值对，作为参数传给函数  
函数定义的时候可以接受可变参数  
```
def person(name, *args, **kwargs):
    print('name', name, 'age', args, 'other', kwargs)

kw = {'city': 'Beijing', 'job': 'Engineer'}
args = [1, 2, 3]
person('John', *args, **kw)
person('Mike', *args, **{'city': 'Beijing'})
```

12. python可以将函数赋值给一个变量，此时如果用del删除该函数，变量仍可以使用该函数的功能  
当函数名后面带()时，该函数会被执行；如果只有函数名，则可以被到处传递  

13. Python的赋值与深复制、浅复制  
> + 赋值  
Python中的赋值操作总是建立对象的引用值，而不是复制对象；Python中的变量更像是指针，而不是数据存储区域  
比如`x=1; y=x`，此时修改x的值，y的值也会跟着改变
> + 深复制与浅复制  
浅复制：  
![](snapshot/浅复制.png)  
深复制：  
![](snapshot/深复制.png)  
浅复制只是复制一个引用，而深复制会连同引用和指向的元素一同复制  
copy标准库模块能够生成完整拷贝；deepcopy的本质是递归copy  

14. 可以通过解压序列（tuple、list、str等）的方法来赋值给多个变量  
```
>>> p = (4, 5)  
>>> x, y = p  
>>> x  
4  
>>> y  
5  
>>> s = 'Hello'  
>>> a, b, c, d, e = s
>>> a  
'H'
```
注意**数量必须相等**  
python3之后，当想将序列中多个元素都赋值给一个变量时，可以使用\*号表达式  
```
>>> *trailing, current = [10,8,7,1,9,5,10,3]
>>> trailing
[10,8,7,1,9,5,10]
>>> current
3
```

15. **生成器**  
生成器也是一种迭代器，所谓迭代器就是定义了next方法的对象  
生成器只能对它迭代一次，这是因为他们的值并没有存在内存中，而是在运行时生成值  
生成器最佳应用场景是：你不想同一时间将所有计算出来的大量结果集分配到内存当中，特别是结果集里还包含循环，使用生成器可以减少资源消耗  
许多Python 2里的标准库函数都会返回列表，而Python 3都修改成了返回生成器，因为生成器占用更少的资源  

16. 字典的get方法  
返回指定key的value，如果value不在字典中，则返回默认值  
`dict.get(key, default=None)`，default可以自己指定  

17. **堆**  
heapq模块为堆模块  
`heapq.nlargest(n, iterable, key=None)`和`heapq.nsmallest(n, iterable, key=None)`返回一个集合的最大或最小的N个元素列表  
比如：  
```
import heapq
nums = [1, 8, 2, 23, 7, -4, 18, 23, 42, 37, 2]
print(heapq.nlargest(3, nums)) # prints [42, 37, 23]
print(heapq.nsmallest(3, nums)) # prints [-4, 1, 2]
```  
还可以接受关键字参数  
比如：  
```
portfolio = [
    {'name': 'IBM', 'shares': 100, 'price': 91.1},
    {'name': 'AAPL', 'shares': 50, 'price': 543.22},
    {'name': 'FB', 'shares': 200, 'price': 21.09},
    {'name': 'HPQ', 'shares': 35, 'price': 31.75},
    {'name': 'YHOO', 'shares': 45, 'price': 16.35},
    {'name': 'ACME', 'shares': 75, 'price': 115.65}
]
cheap = heapq.nsmallest(3, portfolio, key=lambda s: s['price'])
expensive = heapq.nlargest(3, portfolio, key=lambda s: s['price'])
```
本质都是堆排序  

18. 可以使用dir()来获取一个对象的所有属性和方法  

19. Python并没有提供抽象类和抽象方法，但是提供了内置模块abc来模拟抽象类  

20. 删除字典的一个key可以用del  

21. **__call__方法**  
。。。。。。。。

22. **包的概念**  
包定义了一个由模块、子包、子包下的子包等组成的Python应用环境  
在包的目录下，必须有一个__init__.py的文件，用来标识它是一个包  

23. **with语句**  
。。。。。

24. list的初始化  
初始化一个固定大小的list  
比如：初始化一个有5个元素，每个元素都为1的list可以通过`list = [1] * 5`  
python中的list是一个可变对象，对它进行赋值的时候会进行一个浅拷贝  
创建二维数组如果通过`list = [[0] * 3] * 3`的方式创建的话，实际是列表中每一个元素都指向同一个包含三个全为0元素的列表,  
故进行赋值如`list[0][1] = 1`时，得到的是`[[0, 1, 0], [0, 1, 0], [0, 1, 0]]`  
为了防止浅拷贝，可以用下面的方式创建二维数组：  
`a = [([0] * 3) for p in range(3)]`  

25. ==和is  
前者是比较value，即将变量转换为具体的值，相当于Java的equals；
is比较id，即比较是否指向同一个对象

26. **pyc**  
pyc文件是py文件编译而成的，为了提高执行的速度而进行的预编译  
下次启动前，如果没有修改源码的话，会自动使用pyc文件  
pyc文件在Python拥有写权限的时候会自动生成，没有写权限的话，会生成一个pyc文件到内存，程序运行结束后自动删除  

27. strip()是只要string边上的字符（开头或结尾）在序列内，就会把它删掉，与顺序无关；如果想删除掉特定的子串，可以用replace()  

28. 函数或模块获取自己的调用对象，可以用  
```
import traceback
print(traceback.extract_stack()[0][0])
```

29. **Python中的下划线**  
> 1). 在解释器中，"\_"代表交互式解释器中上一条语句的结果  
```
>>> 42
42
>>> _
42
>>> print('hello')
hello
>>> _
42
>>> a=11
>>> _
42
>>> 11 == 12
False
>>> _
False
```
> 2). 作为一个临时名称，比如在for循环中使用，表示分配了一个特定的名称，并不会后面再次使用，做占位符用  
> 3). 国际化  
> 4). 在变量或方法名前使用"\_"用于指定该属性为私有  
> 5). 双下划线用在方法名前，用来避免子类覆盖其内容  
> 6). 在变量命名时，如果刚好要用到的变量名与Python关键字冲突，可以在结尾上加单下划线，比如：class_

30. \_\_file\_\_表示当前脚本的运行路径  
如果执行命令时使用的是绝对路径，\_\_file\_\_就是脚本的绝对路径；使用的是相对路径，那它就是相对路径  
但在交互式解释环境中无法使用，会有异常，因为此时\_\_file\_\_并未生成  

31. 内置函数callable()可以用来判断对象是否可调用  

32. 内置函数divmod()把除数和余数运算结果结合起来，返回一个包含商和余数的元组(a//b, a%b)

33. 时分秒字符串与秒数的互相转换  
[时分秒与秒数的互相转换]<https://www.cnblogs.com/gayhub/p/6154707.html>

34. import module和from module import的区别  
使用import module，模块自身被导入，但是它保持着自己的名字空间，这就是为什么你需要使用模块名来访问函数或属性的原因(module.function)；  
使用from module import，实际上是从另一个模块中将指定的函数和属性导入到你自己的名字空间，这就是为什么你可以直接访问它们却不需要引用它们来源的模块的原因

35. \_\_import\_\_与import语句具有同样的功能  
\_\_import\_\_是一个函数，并且只接收字符串作为参数，本质上import语句就是调用\_\_import\_\_来进行导入工作的  
通常用于动态加载模块的场景

36. **字符串分割**  
`re.split()`分割很实用，例如：  
```
>>> line = 'asdf fjdk; afed, fjek,asdf, foo'
>>> import re
>>> re.split(r'[;,\s]\s*', line)
['asdf', 'fjdk', 'afed', 'fjek', 'asdf', 'foo']
```
对于简单的字符串操作可以使用str模块下的函数，复杂字符串操作都可以考虑re模块

37. **弱引用**  
weakref模块可以创建对一个对象的弱引用  
对于python来说，如果一个对象有一个常规的引用，它是不会被GC回收的，但如果只剩一个弱引用，那么是可以被GC回收的

38. set集合无法进行json序列化，可以使用pickle来进行序列化

39. **生成器**  
包含yield的函数即生成器generator  
每一次的next，函数会执行到yield，然后返回yield的值，然后暂停，下一次的时候再从yield开始接着跑

40. **eventlet**  
Eventlet是以协程概念建立起来的网络库  
协程和普通线程的区别是:  
> + 协程开销很小  
> + 协程共享数据，不需要锁，同一时刻只有一个线程能访问数据，通过队列去查找等待的数据  

使用eventlet库可以通过协程实现并发  
所谓并发，就是开启了多个greenthread(绿色线程)，并且对这些greenthread进行管理，以实现非阻塞式的I/O  
**greenlet**就是协程，有几个特点：  
    > 1). 每个协程都有自己私有的stack及局部变量  
    > 2). 同一时间内只有一个协程在运行，不需要对某些共享变量加锁  
    > 3). 协程之间的执行顺序完全由程序来控制  
**greenThread**是对greenlet进行的简单封装  
eventlet包通过一定的控制，避免完全由程序来控制协程执行顺序导致的代码复杂  
**greenPool**提供对greenthread池的支持，有效限制了greenthread过多导致的内存不足

41. python多线程  
python多线程相当于单位时间内只有一个线程在运行，如果是多核CPU单位时间内也只是一个核在运行  
原因是python存在一个GIL（全局解释器锁），当一个线程在运行的时候，会自动上锁  
所以python并不适合计算密集型的程序，解决办法是计算密集型的任务用c 编写，通过.so链接库把内容加载到Python中来执行

