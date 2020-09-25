# Part.2 摘要内容

## 函数定义

关键字 `def`

函数名
- 大小写字母和下划线开头
- 名称中不能有空格
    - 下划线
    - 驼峰式命名
- 不能和关键字同名

|     -      | Python     | Keyword    | List       |     -      |
| ---------- | ---------- | ---------- | ---------- | ---------- |
| `and`      | `as`       | `assert`   | `async`    | `await`    |
| `break`    | `class`    | `continue` | `def`      | `del`      |
| `elif`     | `else`     | `except`   | `False`    | `finally`  |
| `for`      | `from`     | `global`   | `if`       | `import`   |
| `in`       | `is`       | `lambda`   | `None`     | `nonlocal` |
| `not`      | `or`       | `pass`     | `raise`    | `return`   |
| `True`     | `try`      | `while`    | `with`     | `yield`    |

使用代码查询关键字列表

```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"

import keyword
keyword.kwlist               # 列出所有关键字
keyword.iskeyword('if')      # 查询某个词是不是关键字
```

- [PEP 8 -- Style Guide for Python Code: Naming Conventions](https://www.python.org/dev/peps/pep-0008/#naming-conventions)
- [PEP 526 -- Syntax for Variable Annotations](https://www.python.org/dev/peps/pep-0526/)
- [PEPs](https://www.python.org/dev/peps/)
    - Python Enhancement Proposals

参数
- 圆括号 `()`
- 可以有很多个参数

返回值
- 没有 `return` 默认返回 `None`

### 参数

位置参数

接收很多值的位置参数
- 参数名前标注星号 `*`
- 列表形式
- 可接收一系列的值
- 当作容器处理：使用 `for...in...` 遍历
- 将容器传递给位置参数时，在参数前加上星号 `*`

一个函数中，接收很多值的位置参数只能有一个，且必须在位置参数之后

关键字参数
- 为参数设定默认值
- 可选参数

接收很多值的关键字参数
- 参数名前标注两个星号 `**`
- 字典形式
- 将容器传递给位置参数时，在参数前加上两个星号 `**`

参数顺序：

> **Order of Arguments**
> 1. Positional
> 2. Arbitrary Positional
> 3. Keyword
> 4. Arbitrary Keyword


## 作用域 scope

全局变量
- 在所有函数之外被赋值而后开始使用
- 作用域是全局的
    - 在函数内外都可以被调用

局部变量
- 在函数内部被赋值而后开始使用
- 作用域是局部的
    - 无法被函数外的代码调用

> 在函数内部绝对不调用全局变量。即便是必须改变全局变量，也只能通过函数的返回值在函数外改变全局变量。

可变容器作为参数传递
- 传递的是指针，可变容器会被改变
- 建议创建拷贝

## lambda 关键字

匿名函数

lambda 语法结构：
- BNF 标注

> `lambda_expr ::= "lambda" [parameter_list] ":" expression`

更简洁

```python
add = lambda x, y : x + y
add(3, 5)
```

1. 作为另一个函数的返回值

```python
def make_incrementor(n):
    return lambda x: x + n

f = make_incrementor(42)    # 返回的匿名函数
f(0)    # 42
f(1)    # 43

ff = make_incrementor       # 别名
```

2. 作为另一个函数的参数

接收函数为参数的函数
- 内建函数 `map()`

```python
def double_it(n):
    return n * 2

a_list = [1, 2, 3, 4, 5, 6]

b_list = list(map(double_it, a_list))
b_list      # [2, 4, 6, 8, 10, 12]

c_list = list(map(lambda x: x * 2, a_list))
c_list      # [2, 4, 6, 8, 10, 12]
```

可以给 `map()` 传递若干个课迭代对象

```python
a_list = [1, 3, 5]
b_list = [2, 4, 6]

list(map(lambda x, y: x * y, a_list, b_list))       # [2, 12, 30]
```

## 递归 recursion

递归函数
- 在自身内部调用自身的函数

无限循环
- 也称为死循环

必要条件
- `return` 语句中返回自身的调用
- 终止条件
    - 一个条件下返回的不再是自身调用


递归三原则
1. 根据定义，递归函数必须在内部调用自己；
2. 必须设定一个退出条件；
3. 递归过程中必须能够逐步达到退出条件。

## 模块 Module

任何一个 `.py` 文件都可以被称为模块，模块名称就是文件名

`import ...` 模块文件检索顺序
- 内置模块
    - `sys.builtin_module_names`
    - 自定义模块最好不要和内置模块重名
- `sys.path` 返回的目录列表
    - 当前工作目录排在第一位
    - `sys.path.append()` 添加搜索位置

导入
- 模块中所有函数
    - `from module import *`
    - `import module`
- 模块中指定函数：
    - `from module import function`
    - `import module.function`

[包](https://docs.python.org/3/reference/import.html#regular-packages) Packages
- `__init__.py`
    - 标识所在目录形成一个包含多个模块的包
- 拥有自己独立的 [命名空间](https://docs.python.org/3/glossary.html#term-namespace-package) namespace

```
parent/
    __init__.py
    one/
        __init__.py
    two/
        __init__.py
    three/
        __init__.py
```

在 `import` 语句执行的时候，模块中的非函数部分的可执行代码，只执行一次


```python
# 彩蛋
import this
```

[dir()](https://docs.python.org/3/library/functions.html#dir) 函数
- 查看模块中可访问的变量名称和函数名称

## 别名 alias

作用
- 提高代码可读性
- 避免混淆
- 避免输入太多字符

`as` 关键字
- 函数别名：`from module import function as func`
- 模块别名：`import module as mod`

直接为函数起别名
- 使用 `=`，例如 `func = function`

## Docstring

文档注释
- 可以是单行或多行字符串
- 必须在函数定义的内部语句块的开头
    - 必须与其他语句一样保持相应的缩进（Indention）

规范
1. 无论是单行还是多行的 Docstring，一概使用三个双引号括起；
2. 在 Docstring 内部，文字开始之前，以及文字结束之后，都不要有空行；
3. 多行 Docstring，第一行是概要，随后空一行，再写其它部分；
4. 完善的 Docstring，应该概括清楚以下内容：参数、返回值、可能触发的错误类型、可能的副作用，以及函数的使用限制等等；
5. 每个参数的说明都使用单独的一行。

注意
- 写 Why 远比写 What 重要
- Why >> What

[Sphinx](https://www.sphinx-doc.org/en/master/)
- 可以从 `.py` 文件里提取所有 Docstring，进而生成完整的 Documentation
- 使用 reStructureText 标记语言，文件后缀为 `.rst`
- 通过插件，Sphinx 也能支持 Google Style Docstring 和 Numpy Style Docstring

## 异常处理


语法错误 Syntax Errors

异常 Exceptions
- 程序执行后才发生（Runtime Errors）


`try` 语句块
- 特殊的流程控制
- 可以与 `except`、`else`、`finally` 结合使用


```python
# 1
try:
    do_something()
except built_in_error as name_of_error:
    do_something()
else:
    do_something()

# 2
try:
    do_something()
except built_in_error as name_of_error:
    do_something()
else:
    do_something()
finally:
    do_something()

# 3
try:
    do_something()
except built_in_error as name_of_error:
    do_something()
else:
    try:
        do_something()
    except built_in_error as name_of_error:
        do_something()
...
```

## 程序执行


当一个模块被 `import` 语句导入时，模块的 `__name__` 就是模块名；

当一个模块被运行时，`__name__` 就被 Python 解释器设定为 `__main__` 。


把程序封装到 `main()` 中，并在模块中加上以下代码：

```python
if __name__ == '__main__':
    main()
```

1. 当 Python 文件被当作模块，被 `import` 语句导入时，`if` 判断失败，`main()` 函数不被执行；
2. 当 Python 文件被 `python -m` 运行的时候，`if` 判断成功，`main()` 函数才被执行。

## 其他

凡事都可以分为：
- Must have
- Should have
- Could have
- Won't have

# 参阅

概念
- [机器人三定律](https://zh.wikipedia.org/wiki/%E6%9C%BA%E5%99%A8%E4%BA%BA%E4%B8%89%E5%AE%9A%E5%BE%8B)
- [MoSCoW method](https://en.wikipedia.org/wiki/MoSCoW_method)
- [测试驱动开发（Test-Driven Development, TDD）](https://zh.wikipedia.org/zh-hans/%E6%B5%8B%E8%AF%95%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91)
- [普林斯顿大学 - 递归](https://introcs.cs.princeton.edu/java/23recursion/)

Python 语言参考
- [运算符优先级](https://docs.python.org/3/reference/expressions.html#operator-precedence)

文档注释规范
- [PEP 257 -- Docstring Conventions](https://www.python.org/dev/peps/pep-0257/)
- [PEP 258 -- Docutils Design Specification](https://www.python.org/dev/peps/pep-0258/)

Sphinx 插件
- [sphinx.ext.napoleon – Support for NumPy and Google style docstrings](http://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html)
- [sphinx.ext.autodoc – Include documentation from docstrings](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html)

异常处理相关
- [内置异常](https://docs.python.org/3/library/exceptions.html)
- [处理异常](https://wiki.python.org/moin/HandlingExceptions)

单元测试相关
- [unittest --- 单元测试框架](https://docs.python.org/3/library/unittest.html)
- [doctest --- 测试交互性的Python示例](https://docs.python.org/3/library/doctest.html)

Python 彩蛋
- [OrkoHunter/python-easter-eggs](https://github.com/OrkoHunter/python-easter-eggs)