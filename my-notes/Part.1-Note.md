

# Part.1 摘要内容

## 布尔运算

布尔值
- `True`
- `False`

> Here are most of the built-in objects considered `False`:
> 
> > * constants defined to be false: `None` and `False`.
> > * zero of any numeric type: `0`, `0.0`, `0j`, `Decimal(0)`, `Fraction(0, 1)`
> > * empty sequences and collections: `''`, `()`, `[]`, `{}`, `set()`, `range(0)`

逻辑操作符

|    符号    | 意义     | 示例             | 布尔值  |
| ---------- | -------- | ---------------- | ------- |
| `==`       | 等于     | `1 == 2`         | `False` |
| `!=`       | 不等于   | `1 != 2`         | `True`  |
| `>`        | 大于     | `1 > 2`          | `False` |
| `>=`       | 大于等于 | `1 >= 1`         | `True`  |
| `<`        | 小于     | `1 < 2`          | `True`  |
| `<=`       | 小于等于 | `1 <= 2`         | `True`  |
| `in`       | 属于     | `'a' in 'basic'` | `True`  |

布尔操作符

|    符号    | 意义    | 示例             | 布尔值  |
| ---------- | ------ | ---------------- | ------- |
| `and`      | 与     | `1 and 0`         | `False` |
| `or`       | 或     | `1 or 0`         | `True`  |
| `not`      | 非     | `not 1`          | `False` |

布尔运算
- 并集、交集、差集、对称差集

## 流程控制

分支

```python
if expression:
    statements
else:
    statements

if expression:
    statements
elif expression:
    statements
else:
    statements
```

循环

```python
while expression:
    statements

for i in range(n):  # [0,n)
    statements

# 附加在 for 结尾的 else 语句块，在没有 break 发生的情况下会运行
for i in range(n):  # [0,n)
    statements
else:
    statements
```

其他流程控制
- `continue` 语句将忽略其后的语句开始下次循环；
- `break` 语句将从此结束当前循环，开始执行循环之后的语句；
- `pass`  语句什么都不干。

## 其他

语句
- 一个语句块必然由一个行末带有冒号 `:` 的语句起始

语句块
- 有着相同行首空白的语句同属于一个语句块

注释
- `#` 标示

操作符
- `+`、`-`、`*`、`/`、`//`、`%`、`**`

赋值符号+操作符
- `+=`、`-=`、...

## 值

常量
- 值不可改变

变量
- 值可以改变

操作符
- 数值操作符
    - `+`、`-`、`*`、`/`、`//`、`%`、`**`
    - `+`、`-` 可以对单个值操作，例如 `-3`
- 布尔值操作符
    - `not`、`and`、`or`
- 逻辑操作符
    - `==`、`!=`、`>`、`>=`、`<`、`<=`、`in`
- 字符串操作符
    - 拼接：`+` 和 ` `
    - 拷贝：`*`
    - 逻辑运算：`in`、`not in`；以及 `==`、`!=`、`>`、`>=`、`<`、`<=`

处理数值的内置函数
- `abs()`
- `int()`
- `float()`
- `divmod()`
- `pow()`
- `round()`

## 容器

有序容器
- 列表、字符串、元组、`range()` 等差数列
- 操作符
    - 拼接：`+` 和 ` `
    - 拷贝：`*`
    - 逻辑运算：`in`、`not in`；以及 `==`、`!=`、`>`、`>=`、`<`、`<=`

无序容器
- 集合、字典

可变容器
- 列表、集合、字典

不可变容器
- 字符串、元组、`range()` 等差数列

### 列表 list

生成方式

```python
a = []
b = [1, 2, 3]
c = list()
d = [(expression with x) for x in iterable] # 列表推导式
e = list(iterable)  # Type Casting
```

与字符串的异同
- 都是有序容器
- 列表是可变序列，字符串是不可变序列

排序方法
- `list.sort()`
- `list.reverse()`
- `sorted(list)`
- `reversed(list)`

类方法
- `list.append()`
- `list.clear()`
- `list.copy()`
- `list.extend()`
- `list.insert()`
- `list.pop()`
- `list.remove()`
- `list.reverse()`
- ...

### 元组 tuple

生成方式

```python
a = ()
b = 2,
c = (3,)
d = tuple()
e = tuple(iterable)
```

与列表的不同
- 元组相对于列表占用更小的内存

### 集合 set

生成方式

```python
a = {1, 2, 3}
b = set()
c = {}  # 字典
```

将序列转换为集合，返回去重的结果
- `a = set([1, 2, 2, 3, 3, 1])`

删除元素
- `set.remove()`
- 不能使用 `del`

集合运算
- 并集：`|`。`set.union()`
- 交集：`&`，`set.intersection()`
- 差集：`-`，`set.difference()`
- 对称差集：`^`，`set.symmetric_difference()`

逻辑运算
- `==`
- `!=`
- `set.isdisjoint()`
- `set.issubset()`。`<=`
- `<`
- `set.issuperset()`，`>=`
- `>`

更新
- `set.add()`
- `set.remove()`
- `set.discard()`
- `set.pop()`
- `set.clear()`
- `set.update()`
- `set.intersection_update()`
- `set.difference_update()`
- `set.symmetric_difference_update()`

冻结集合 Frozen Set
- 节省内存

### 字典 dict

生成方式

```python
a = dict(one=1, two=2, three=3)
b = {'one': 1, 'two': 2, 'three': 3}
c = dict(zip(['one', 'two', 'three'], [1, 2, 3]))
d = dict([('two', 2), ('one', 1), ('three', 3)])
e = dict({'three': 3, 'one': 1, 'two': 2})
f = {}
```

操作
- 更新：`a[key]=value`
- 添加：`a[key]=value`，`a.update(b)`
- 删除：`del a[key]`
- 逻辑操作：`key in a.keys()`，`value in a.values()`，`(key, value) in a.items()`

内置函数（对 key 进行操作）
- `len()`
- `max()`
- `min()`
- `list()`
- `tuple()`
- `set()`
- `sorted()`

类方法
- `dict.copy()`
- `dict.clear()`
- `dict.popitem()`
- `dict.pop()`
- `dict.get()`
- `dict.setdefault()`

### 字符串 str

表示
- 单引号：`'Hello, Python'`
- 双引号：`"Hello Python"`
- 三个单引号/双引号：`'''Hello Python'''`，`"""Hello Python"""`
    - 注意换行符

形式
- raw：`\t`、`\n`
- presentation：制表符、换行符

字符与数字之间的转换
- 字符-->数字：`ord()`
- 数字-->字符：`str()`

转义符 `\`
- 字符串中必须得用 `\\` 表示

换行符
- Unix 类操作系统：`\n`
- Windows 操作系统：`\r\n`

索引
- 从 `0` 开始，倒数第一个从 `-1` 开始

内置函数
- `ord()`
- `input()`
- `int()`
- `float()`
- `len()`
- `print()`

类方法（str 类）
- 大小写转换
    - `str.upper()`
    - `str.lower()`
    - `str.swapcase()`
    - `str.casefold()`
    - `str.capitalize()`
    - `str.title()`
- 查找
    - `str.count()`
    - `str.find()`
    - `str.rfind()`
    - `str.index()`
    - `str.startswith()`
    - `str.endswith()`
- 替换
    - `str.replace()`
    - `str.expandtabs()`
- 删除子字符
    - `str.strip()`
    - `str.lstrip()`
    - `str.rstrip()`
- 拆分
    - `str.splitlines()`
    - `str.split()`
    - `str.partition()`
- 拼接
    - `str.join()`
- 排版
    - `str.center()`
    - `str.ljust()`
    - `str.rjust()`
- 格式化字符串
    - `str.format()`
    - `f-string`
- 属性
    - `str.isalnum()`
    - `str.isalpha()`
    - `str.isdecimal()`
    - `str.isdigit()`
    - `str.isnumeric()`
    - `str.islower()`
    - `str.isupper()`
    - `str.istitle()`
    - `str.isprintable()`
    - `str.isspace()`
    - `str.isidentifier()`

### 迭代

迭代
- `for`

迭代元素及其索引
- `enumerate()`

同时迭代多个容器
- `zip()`

## 函数

函数名、参数、返回值、调用

种类
- 内置函数（Built-in）
- 其他模块里的函数
- 本身所属类中定义的函数（Method）

函数参数
- 位置参数 *arg*
    - 可选位置参数
    - 可接收很多值的位置参数
        - 一般来说，一个函数里最多只有一个可以接收很多值的位置参数
        - 如果还有若干个位置参数，那么，能够接收很多值的位置参数只能放在最后
- 关键字参数 *kwarg*
    - 函数定义中设置了默认值的参数

`Class` 函数
- Class 本质上来看就是一种特殊类型的函数

## 文件

创建
- `open()`

删除
- `os.remove()`

读写
- `f.read()`
- `f.readline()`
- `f.readlines()`
- `f.write()`
- `f.writelines()`

`with` 语句块
- 不用写 `f.close()`

# 参阅

概念
- [Human Development Index](http://hdr.undp.org/en/content/human-development-index-hdi)
    - [人类发展指数](https://zh.wikipedia.org/wiki/%E4%BA%BA%E7%B1%BB%E5%8F%91%E5%B1%95%E6%8C%87%E6%95%B0)
- [Backus–Naur form](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form)
    - [巴科斯范式](https://zh.wikipedia.org/wiki/%E5%B7%B4%E7%A7%91%E6%96%AF%E8%8C%83%E5%BC%8F)

教程
- [Python (v.3.6.3) 入门指南](http://www.pythondoc.com/pythontutorial3/)
- [Python 教程](https://docs.python.org/3/tutorial/index.html)

查询参考
- [Python 标准库](https://docs.python.org/3/library/index.html)
    - [内置类型](https://docs.python.org/3/library/stdtypes.html)
    - [内置函数](https://docs.python.org/3/library/functions.html)
    - [operator --- 标准运算符替代函数](https://docs.python.org/3/library/operator.html)
- [Python 语言参考](https://docs.python.org/3/reference/)
    - [表达式](https://docs.python.org/3/reference/expressions.html)
    - [运算符优先级](https://docs.python.org/3/reference/expressions.html#operator-precedence)
- [PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)