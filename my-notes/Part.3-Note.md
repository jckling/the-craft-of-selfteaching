# Part.3 摘要内容

## OOP

面向对象编程（OOP）
- 使用**对象**（Objects）作为核心的编程方式
    - **类**（Class）的实例
        - **子类**（SubClass）
        - Class ⊃ SubClass
    - **继承**（Inheritance）
        - 类与子类
    - **实例**（Instances）
- 把对象（Objects）的数据和运算过程**封装**（Encapsulate）在内部
    - 隐藏具体的实现细节
    - 数据 --> **属性**（Attributes）
    - 运算方法 --> **方法**（Methods）
- 外部仅能根据事先设计好的**界面**（Interface）与之沟通
- **抽象**（Abstract）
    - 简化复杂问题


## 类

### 定义 define

`class` 关键字

```python
Class myclass:
    def __init__(self, name=None):  # 初始化函数
        pass
    def func(self):
        pass
```

`self` 变量
- 约定命名
- 系统默认可以识别的变量
- 指代由 Class 创建的 Instance

`__init__` 函数
- 创建实例后就执行

### 继承 inheritance

创建子类
- 使用圆括号 `()`

```python
Class myclass:
    def __init__(self, name=None):  # 初始化函数
        pass
    def func(self):
        pass
    
Class mysubclass(myclass):
    def subfunc(self):
        pass
```

### 重写 override

子类中实现的方法覆盖父类原有的方法

```python
Class myclass:
    def __init__(self, name=None):  # 初始化函数
        pass
    def func(self):
        pass
    
Class mysubclass(myclass):
    def func(self):    # 重写
        pass
```

### 了解 inspect / 封装 encapsulation

```python
1. help(object)
2. dir(object)
3. object.__dict__
```

作用域 scope
- `hasattr(object, attr)`：查询这个 `object` 中有没有这个 `attr`，返回布尔值
- `getattr(object, attr)`：获取这个 `object` 中这个 `attr` 的值
- `setattr(object, attr, value)`：将这个 `object` 中的 `attr` 值设置为 `value`

```python
import datetime

class Golem:
    __population = 0    # 私有变量
    __life_span = 10    # 类外不可见
    
    def __init__(self, name=None):
        self.name = name
        self.built_year = datetime.date.today().year
        self.__active = True
        Golem.__population += 1    # here
    
    def say_hi(self):
        print('Hi!')
    
    def cease(self):
        self.__active = False
        Golem.__population -= 1    # here
    
    def is_active(self):
        if datetime.date.today().year - self.built_year >= Golem.__life_span:
            self.cease
        return self.__active
    
    @property  # 允许访问
    def population(self):
        return Golem.__population
    
    @population.setter  # 允许更改
    def population(self, value):
        Golem.__population = value
```

## 迭代器 Iterator

Python 中所有容器都是可迭代的

[iter()](https://docs.python.org/3/library/functions.html#iter)
- 返回 [迭代器](https://docs.python.org/zh-cn/3/glossary.html#term-iterator() 对象（iterator）
- 使用内置函数 [next()](https://docs.python.org/zh-cn/3/library/functions.html#next) 获取下一个元素，到最后一个元素时引发 [StopIteration](https://docs.python.org/zh-cn/3/library/exceptions.html#StopIteration) 异常

迭代器是对象（Object），编写自定义的迭代器使用 `Class` ，派生自 `Object`
- 迭代器协议
    - [\_\_iter\_\_](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__iter__)：返回迭代器对象本身
    - [\_\_next\_\_](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__)：从容器中返回下一项

```python
class Counter(object):
    def __init__(self, start, stop):
        self.current = start
        self.stop = stop
    def __iter__(self):
        return self
    def __next__(self):
        if self.current > self.stop:
            raise StopIteration
        else:
            c = self.current
            self.current += 1
        return c
```

## 生成器 Generator

- 返回 [生成器迭代器](https://docs.python.org/zh-cn/3/glossary.html#term-generator-iterator)
- 包含 [yield 表达式](https://docs.python.org/zh-cn/3/reference/expressions.html#yield-expressions)
    - 只能在函数定义的内部使用
    - 在一个函数体内使用 yield 表达式会使这个函数变成一个生成器
    - 禁止在实现推导式和生成器表达式的隐式嵌套作用域中使用 yield 表达式（Python3.8）
    
```python
def counter(start, stop):
    while start <= stop:
        yield start
        start += 1
```

[生成器表达式](https://docs.python.org/zh-cn/3/glossary.html#term-generator-expression)
- 返回一个迭代器的表达式
- 列表推导式：`[]`
- 集合推导式：`{}`

```python
sum(i*i for i in range(10))
```

## 装饰器 Decorator

[装饰器](https://docs.python.org/zh-cn/3/glossary.html#term-decorator)
- 返回值为另一个函数的函数
- 通常使用 `@wrapper` 语法形式进行函数变换
- 语法糖

[staticmethod()](https://docs.python.org/zh-cn/3/library/functions.html#staticmethod)
- 将方法转换为静态方法

```python
def f(...):
    ...
f = staticmethod(f)

# 等价
@staticmethod
def f(...):
    ...
```

[classmethod()](https://docs.python.org/zh-cn/3/library/functions.html#classmethod)
- 把一个方法封装成类方法

```python
class C:
    @classmethod
    def f(cls, arg1, arg2, ...): ...
```

常用于改变其他函数的行为

```python
def uppercase(func):
    def wrapper():
        original_result = func()
        modified_restult = original_result.upper()
        return modified_restult
    return wrapper
def strong(func):
    def wrapper():
        original_result = func()
        modified_restult = '<strong>'+original_result+'</strong>'
        return modified_restult
    return wrapper

@strong
@uppercase
def an_output():
    return 'The quick brown fox jumps over the lazy dog.'
print(an_output())
```

多个装饰器会以嵌套方式被应用

```python
@f1(arg)
@f2
def func(): pass

# 等价
def func(): pass
func = f1(arg)(f2(func))
```

带有参数的装饰器
- `*args`：任意位置参数
- `**kwargs`：任意关键字参数

```python
def trace(func):
    def wrapper(*args, **kwargs):
        print(f"Trace: You've called a function: {func.__name__}(),",
              f"with args: {args}; kwargs: {kwargs}")
    
        original_result = func(*args, **kwargs)
        print(f"Trace: {func.__name__}{args} returned: {original_result}")
        return original_result
    return wrapper

@trace
def say_hi(greeting, name=None):
    return greeting + '! ' + name + '.'

print(say_hi('Hello', name = 'Jack'))
```

## 正则表达式

- Regular Expression 简写为 regex、regexp、re
- 通常被称为一个模式（Pattern）
- 匹配（Match）、捕获（Capture）、替换（Replace）

操作符（Operator）
- `\` `+` `*` `.` `?` `-` `^` `$` `|` `(` `)` `[` `]` `{` `}` `<` `>` 

操作元（Operand）：原子（Atom）

| 排列 |         原子与操作符优先级      |（从高到低）|
|---|-----------------------------------|------------------------|
| 1 | 转义符号 (Escaping Symbol)               | `\` |
| 2 | 分组、捕获 (Grouping or Capturing)                          | `(...)` `(?:...)` `(?=...)` `(?!...)` `(?<=...)` `(?<!...)`     |
| 3 | 数量 (Quantifiers)      | `a*` `a+` `a?` `a{n, m}` |
| 4 | 序列与定位（Sequence and Anchor）| `abc` `^` `$` `\b` `\B`               |
| 5 | 或（Alternation）| <code>a&#124;b&#124;c</code>                   |
| 6 | 原子 (Atoms)                 | `a` `[^abc]` `\t` `\r` `\n` `\d` `\D` `\s` `\S` `\w` `\W` `.` |

### 原子

- 被运算的“值”
- 最基本的原子：本义字符
    - `a-zA-Z0-9_`
- 集合原子
    - 使用方括号标识 `[]`
    - 可以使用两个操作符
        - `-`：区间
        - `^`：非
            - 只能用一次，紧跟在 `[` 之后
- 类别原子
    - 代表一类字符的原子
    - `\d` 任意数字；等价于 `[0-9]`
    - `\D` 任意非数字；等价于 `[^0-9]`
    - `\w` 任意本义字符；等价于 `[a-zA-Z0-9_]`
    - `\W` 任意非本义字符；等价于 `[^a-zA-Z0-9_]`
    - `\s` 任意空白；相当于 `[ \f\n\r\t\v]`（注意，方括号内第一个字符是空格符号）
    - `\S` 任意非空白；相当于 `[^ \f\n\r\t\v]`（注意，紧随 `^` 之后的是一个空格符号）

    `.` 除 `\r` `\n` 之外的任意字符；相当于 `[^\r\n]`
- 边界原子
    - 也称为定位操作符，用于指定原子边界
    - `^` 匹配被搜索字符串的开始位置
    - `$` 匹配被搜索字符串的结束位置
    - `\b` 匹配单词的边界
        - `er\b`，能匹配 `coder` 中的 `er`，却不能匹配 `error` 中的 `er`
    - `\B` 匹配非单词边界
        - `er\B`，能匹配 `error` 中的 `er`，却不能匹配 `coder` 中的 `er`
- 组合原子
    - 使用圆括号 `()`，括号内的字符串被当作一整个原子

### 操作符

数量操作符
- 限定位于它们之前的**原子**允许出现的个数
    - 不加数量限定则代表出现一次且仅出现一次
- `+`：出现次数 ≥ 1
- `?`：0 ≤ 出现次数 ≤ 1
- `*`：出现次数 ≥ 0
- `{n}`：出现 n 次
- `{n,}`：至少出现 n 次
- `{n,m}`：至少出现 n 次，至多出现 m 次

或操作符 `|`
- 优先级最低

### 匹配并捕获

使用圆括号得到的匹配的值被暂存成一个带有索引的列表，第一个是 `$1`，第二个是 `$2`……
- Python 中调用 `re` 模块之后，在 `re.sub()` 中调用被匹配的值，用的索引方法是 `\1`、`\2`……

非捕获匹配
- 在圆括号内最开头加上 `?:` ：`(?:...)`
- `(?=pattern)`：正向肯定预查
- `(?!pattern)`：正向否定预查
- `(?<=pattern)`：反向肯定检查
- `(?<!pattern)`：反向否定检查

### 控制标记

全局控制标记（Flag）
- `A`/`ASCII`，默认为 `False`
- `I`/`IGNORECASE`，默认为 `False`
- `G`/`GLOBAL`，默认为 `True`
- `L`/`LOCALE`，默认为 `False`
- `M`/`MULTILINE`，默认为 `True`
- `S`/`DOTALL`，默认为 `False`
- `X`/`VERBOSE`，默认为 `False`

## BNF / EBNF

Backus-Naur Form（BNF，巴科斯-诺尔范式）

Extended Backus-Naur Form（EBNF，扩展巴科斯-诺尔范式）

- [上下文无关文法](https://en.wikipedia.org/wiki/Context-free_grammar)

符合语法的整数（Integer）

```
integer ::= [sign] digit +
sign    ::= "+" | "-"
digit   ::=  "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
``` 

> * `::=` 表示定义；
> * `< >` 尖括号里的内容表示必选内容；
> * `[ ]` 中是可选项；
> * `" "` 双引号里的内容表示字符；
> * ` | ` 竖线两边的是可选内容，相当于or；
> * ` * ` 表示零个或者多个；
> * ` + ` 表示一个或者多个。

[glob](https://docs.python.org/zh-cn/3/library/glob.html) 模块
- 根据 Unix 终端所用规则找出所有匹配特定模式的路径名
- 符号
    - `*`
    - `?`
    - `[abc]`
    - `[^abc]`

## 参阅

概念
- [Eureka effect](https://en.wikipedia.org/wiki/Eureka_effect)
- [Object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming)
- [glob (programming)](https://en.wikipedia.org/wiki/Glob_(programming))
- [Wildcard character](https://en.wikipedia.org/wiki/Wildcard_character)
- [How To Ask Questions The Smart Way](https://github.com/selfteaching/How-To-Ask-Questions-The-Smart-Way)

Python 语言参考
- [Python 3.8.6 文档](https://docs.python.org/zh-cn/3/)
- [函数定义](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#function-definitions)
- [PEP 3129 -- Class Decorators](https://www.python.org/dev/peps/pep-3129/)
- [Python Decorator Library](https://wiki.python.org/moin/PythonDecoratorLibrary)
- [生成器表达式和列表推导式](https://docs.python.org/zh-cn/3/howto/functional.html#generator-expressions-and-list-comprehensions)
- [re --- 正则表达式操作](https://docs.python.org/zh-cn/3/library/re.html)
- [正则表达式HOWTO](https://docs.python.org/zh-cn/3/howto/regex.html)
- [10. 完整的语法规范](https://docs.python.org/zh-cn/3/reference/grammar.html#full-grammar-specification)
- [格式字符串语法](https://docs.python.org/zh-cn/3/library/string.html#format-string-syntax)
- [1.2. 标注](https://docs.python.org/zh-cn/3/reference/introduction.html#notation)

正则表达式
- [regex 测试器](https://regex101.com/)
- [8 Regular Expressions You Should Know](https://bit.ly/2tz8v9n)

方法论
- [If it ain't broke, don't fix it](https://en.wikipedia.org/wiki/If_it_ain%27t_broke,_don%27t_fix_it)
- [KISS principle](https://en.wikipedia.org/wiki/KISS_principle)
- [Don't repeat yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
- [Feature creep](https://en.wikipedia.org/wiki/Feature_creep)
- [List of software development philosophies](https://en.wikipedia.org/wiki/List_of_software_development_philosophies)
- [Minimum viable product](https://en.wikipedia.org/wiki/Minimum_viable_product)
- [MoSCoW method](https://en.wikipedia.org/wiki/MoSCoW_method)
- [Overengineering](https://en.wikipedia.org/wiki/Overengineering)
- [Worse is better](https://en.wikipedia.org/wiki/Worse_is_better)
- [S.O.L.I.D.](https://en.wikipedia.org/wiki/SOLID)
- [Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy)

Google 搜索
- [20 Google Search Tips to Use Google More Efficiently](https://www.lifehack.org/articles/technology/20-tips-use-google-search-efficiently.html)
- [Google 搜索帮助](https://support.google.com/websearch#topic=3036132)

Python 电子书
- [Think Python 2e](http://greenteapress.com/wp/think-python-2e/)
- [A Bite of Python](https://python.swaroopch.com/)
- [Dive into Python](https://linux.die.net/diveintopython/html/)

[Python 书籍](https://pythonbooks.revolunet.com)
- [The Python Tutorial](https://docs.python.org/3/tutorial/)
- [The Hitchhiker's Guide to Python!](https://docs.python-guide.org/)
- [Think Python: How to think like a computer scientist](http://greenteapress.com/wp/think-python-2e/)
- [Automate the Boring Stuff with Python](https://automatetheboringstuff.com)
- [Effective Python](https://effectivepython.com)
- [Python Cookbook](https://www.amazon.com/Python-Cookbook-Recipes-Mastering-ebook/dp/B00DQV4GGY)
- [Fluent Python](https://www.amazon.com/Fluent-Python-Concise-Effective-Programming-ebook/dp/B0131L3PW4)
- [Problem Solving with Algorithms and Data Structures using Python](http://interactivepython.org/runestone/static/pythonds/index.html)
- [Mastering Object-oriented Python - Transform Your Approach to Python Programming](https://www.amazon.com/dp/B00JVQ14UO/ref=dp-kindle-redirect?_encoding=UTF8&btkr=1)

Chatsheet
- [Comprehensive Python Cheatsheet](https://gto76.github.io/python-cheatsheet/)
- [Python Crash Course - Cheat Sheets](https://github.com/ehmatthes/pcc/tree/master/cheat_sheets)
- [Pysheeet](https://www.pythonsheets.com/)