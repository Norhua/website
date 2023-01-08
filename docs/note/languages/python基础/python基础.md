# Python基础
> 来源：https://docs.python.org/zh-cn/3/tutorial/index.html

## 数字

交互模式下，上次输出的表达式会赋给变量 `_` 

## 字符串

如果不希望前置 `\` 的字符转义成特殊字符，可以使用 *原始字符串*，在引号前添加 `r` 即可：

字符串可以用 `+` 合并（粘到一起），也可以用 `*` 重复

相邻的两个或多个 *字符串字面值* （引号标注的字符）会自动合并

字符串支持 *索引* （下标访问），第一个字符的索引是 0。单字符没有专用的类型，就是长度为一的字符串：索引还支持负数，用负数索引时，从右边开始计数：

```python
>>> word = 'Python'
>>> word[0]  # character in position 0
'P'
>>> word[5]  # character in position 5
'n'
```

除了索引，字符串还支持 *切片*。索引可以提取单个字符，*切片* 则提取子字符串：

```python
>>> word[0:2]  # characters from position 0 (included) to 2 (excluded)
'Py'
>>> word[2:5]  # characters from position 2 (included) to 5 (excluded)
'tho'
```

切片索引的默认值很有用；省略开始索引时，默认值为 0，省略结束索引时，默认为到字符串的结尾

```python
>>> word[:2]   # character from the beginning to position 2 (excluded)
'Py'
>>> word[4:]   # characters from position 4 (included) to the end
'on'
>>> word[-2:]  # characters from the second-last (included) to the end
'on'
```

```
 +---+---+---+---+---+---+
 | P | y | t | h | o | n |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1
```

索引越界会报错：

```python
>>> word[42]  # the word only has 6 characters
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
```

但是，切片会自动处理越界索引：

```python
>>> word[4:42]
'on'
>>> word[42:]
''
```

Python 字符串不能修改，是 [immutable](https://docs.python.org/zh-cn/3/glossary.html#term-immutable) 的。因此，为字符串中某个索引位置赋值会报错：

```python
>>> word[0] = 'J'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> word[2:] = 'py'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

要生成不同的字符串，应新建一个字符串：

```python
>>> 'J' + word[1:]
'Jython'
>>> word[:2] + 'py'
'Pypy'
```

内置函数 [`len()`](https://docs.python.org/zh-cn/3/library/functions.html#len) 返回字符串的长度：

```python
>>> s = 'supercalifragilisticexpialidocious'
>>> len(s)
34
```

!!! info "参见"

    [文本序列类型 --- str](https://docs.python.org/zh-cn/3/library/stdtypes.html#textseq)
    
    字符串是 *序列类型* ，支持序列类型的各种操作。
    
    [字符串的方法](https://docs.python.org/zh-cn/3/library/stdtypes.html#string-methods)
    
    字符串支持很多变形与查找方法。
    
    [格式字符串字面值](https://docs.python.org/zh-cn/3/reference/lexical_analysis.html#f-strings)
    
    内嵌表达式的字符串字面值。
    
    [格式字符串语法](https://docs.python.org/zh-cn/3/library/string.html#formatstrings)
    
    使用 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format) 格式化字符串。
    
    [printf 风格的字符串格式化](https://docs.python.org/zh-cn/3/library/stdtypes.html#old-string-formatting)
    
    这里详述了用 `%` 运算符格式化字符串的操作



## 列表

Python 支持多种 *复合* 数据类型，可将不同值组合在一起。最常用的 *列表* ，是用方括号标注，逗号分隔的一组值。*列表* 可以包含不同类型的元素，但一般情况下，各个元素的类型相同：

```python
>>> squares = [1, 4, 9, 16, 25]
>>> squares
[1, 4, 9, 16, 25]
```

和字符串（及其他内置 [sequence](https://docs.python.org/zh-cn/3/glossary.html#term-sequence) 类型）一样，列表也支持索引和切片：

切片操作返回包含请求元素的新列表。以下切片操作会返回列表的 [浅拷贝](https://docs.python.org/zh-cn/3/library/copy.html#shallow-vs-deep-copy)：

```python
>>> squares[:]
[1, 4, 9, 16, 25]
```

列表还支持合并操作：

```python
>>> cubes = [1, 8, 27, 65, 125]  # something's wrong here
>>> 4 ** 3  # the cube of 4 is 64, not 65!
64
>>> cubes[3] = 64  # replace the wrong value
>>> cubes
[1, 8, 27, 64, 125]
```

为切片赋值可以改变列表大小，甚至清空整个列表：

```python
>>> letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> letters
['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> # replace some values
>>> letters[2:5] = ['C', 'D', 'E']
>>> letters
['a', 'b', 'C', 'D', 'E', 'f', 'g']
>>> # now remove them
>>> letters[2:5] = []
>>> letters
['a', 'b', 'f', 'g']
>>> # clear the list by replacing all the elements with an empty list
>>> letters[:] = []
>>> letters
[]
```

内置函数 [`len()`](https://docs.python.org/zh-cn/3/library/functions.html#len) 也支持列表：

```python
>>> letters = ['a', 'b', 'c', 'd']
>>> len(letters)
4
```

还可以嵌套列表（创建包含其他列表的列表），例如：

```python
>>> a = ['a', 'b', 'c']
>>> n = [1, 2, 3]
>>> x = [a, n]
>>> x
[['a', 'b', 'c'], [1, 2, 3]]
>>> x[0]
['a', 'b', 'c']
>>> x[0][1]
'b'
```

## print()

[`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print) 函数输出给定参数的值。与表达式不同（比如，之前计算器的例子），它能处理多个参数，包括浮点数与字符串。它输出的字符串不带引号，且各参数项之间会插入一个空格，这样可以实现更好的格式化操作：

```python
>>> i = 256*256
>>> print('The value of i is', i)
The value of i is 65536
```

关键字参数 *end* 可以取消输出后面的换行, 或用另一个字符串结尾：

```python
>>> a, b = 0, 1
>>> while a < 1000:
...    print(a, end=',')
...    a, b = b, a+b
...
0,1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,
```
## 流程控制工具
### for
Python 的 for 语句与 C 或 Pascal 中的不同。Python 的 for 语句不迭代算术递增数值（如 Pascal），或是给予用户定义迭代步骤和暂停条件的能力（如 C），而是迭代列表或字符串等任意序列，元素的迭代顺序与在序列中出现的顺序一致。 例如：
```python
>>> # Measure some strings:
... words = ['cat', 'window', 'defenestrate']
>>> for w in words:
...    print(w, len(w))
...
cat 3
window 6
defenestrate 12
```
遍历集合时修改集合的内容，会很容易生成错误的结果。因此不能直接进行循环，而是应遍历该集合的副本或创建新的集合：
```python
# Create a sample collection
users = {'Hans': 'active', 'Éléonore': 'inactive', '景太郎': 'active'}

# Strategy:  Iterate over a copy
for user, status in users.copy().items():
    if status == 'inactive':
        del users[user]

# Strategy:  Create a new collection
active_users = {}
for user, status in users.items():
    if status == 'active':
        active_users[user] = status
```
### range()

内置函数 [`range()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#range) 常用于遍历数字序列，该函数可以生成算术级数：

```python
>>> for i in range(5):
...     print(i)
... 
0
1
2
3
4
```

生成的序列不包含给定的终止数值；`range(10)` 生成 10 个值，这是一个长度为 10 的序列，其中的元素索引都是合法的。range 可以不从 0 开始，还可以按指定幅度递增（递增幅度称为 '步进'，支持负数）：

```python
>>> list(range(5, 10))
[5, 6, 7, 8, 9]

>>> list(range(0, 10, 3))
[0, 3, 6, 9]

>>> list(range(-10, -100, -30))
[-10, -40, -70]
```

如果只输出 range，会出现意想不到的结果：

```python
>>> range(10)
range(0, 10)
```

[`range()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#range) 返回对象的操作和列表很像，但其实这两种对象不是一回事。迭代时，该对象基于所需序列返回连续项，并没有生成真正的列表，从而节省了空间。

这种对象称为可迭代对象 [iterable](https://docs.python.org/zh-cn/3/glossary.html#term-iterable)，函数或程序结构可通过该对象获取连续项，直到所有元素全部迭代完毕。[`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for) 语句就是这样的架构，[`sum()`](https://docs.python.org/zh-cn/3/library/functions.html#sum) 是一种把可迭代对象作为参数的函数：

```python
>>> sum(range(4))  # 0 + 1 + 2 + 3
6
```

下文将介绍更多返回可迭代对象或把可迭代对象当作参数的函数。 在 [数据结构](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#tut-structures) 这一章节中，我们将讨论有关 [`list()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#list) 的更多细节。

### 循环中的 `break`、`continue` 语句及 `else` 子句

[`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break) 语句和 C 中的类似，用于跳出最近的 [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for) 或 [`while`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#while) 循环。

循环语句支持 `else` 子句；[`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for) 循环中，可迭代对象中的元素全部循环完毕，或 [`while`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#while) 循环的条件为假时，执行该子句；[`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break) 语句终止循环时，不执行该子句。 请看下面这个查找素数的循环示例：

```python
for n in range(2, 10):
>>>     for x in range(2, n):
...         if n % x == 0:
...             print(n, 'equals', x, '*', n//x)
...             break
...     else:
...         # loop fell through without finding a factor
...         print(n, 'is a prime number')
... 
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```

与 [`if`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#if) 语句相比，循环的 `else` 子句更像 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 的 `else` 子句： [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 的 `else` 子句在未触发异常时执行，循环的 `else` 子句则在未运行 `break` 时执行。`try` 语句和异常详见 [异常的处理](https://docs.python.org/zh-cn/3/tutorial/errors.html#tut-handling)。

[`continue`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#continue) 语句也借鉴自 C 语言，表示继续执行循环的下一次迭代

### pass 语句

[`pass`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#pass) 语句不执行任何操作。语法上需要一个语句，但程序不实际执行任何动作时，可以使用该语句。例如：

```python
while True:
    pass  # Busy-wait for keyboard interrupt (Ctrl+C)
```

下面这段代码创建了一个最小的类：

```python
class MyEmptyClass:
    pass
```

[`pass`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#pass) 还可以用作函数或条件子句的占位符，让开发者聚焦更抽象的层次。此时，程序直接忽略 `pass`：

```python
def initlog(*args):
    pass   # Remember to implement this!
```



