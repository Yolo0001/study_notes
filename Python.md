# 基础知识

## 变量和简单数据类型

### 变量

#### 变量的命名和使用

- 变量名只能包含字母、数字和下划线。变量名可以字母或下划线打头，但不能以数字打头

`message_1` ✔

`1_message`❌

- 变量名不能包含空格，但可使用下划线来分隔其中的单词

`greeting_message`✔

`greeting message`❌

- 不要将Python关键字和函数名用作变量名，即不要使用Python保留用于特殊用途的单词

##### Python关键字

下面的关键字都有特殊含义，如果你将它们用作变量名，将引发错误：

| False  | class    | finally | is       | return |
| ------ | -------- | ------- | -------- | ------ |
| None   | continue | for     | lambda   | try    |
| True   | def      | from    | nonlocal | while  |
| and    | del      | global  | not      | with   |
| as     | elif     | if      | or       | yield  |
| assert | else     | import  | pass     |        |
| break  | except   | in      | raise    |        |

#####  Python 内置函数

将内置函数名用作变量名时，不会导致错误，但将覆盖这些函数的行为：

| abs()         | divmod()    | input()      | open()      | staticmethod() |
| ------------- | ----------- | ------------ | ----------- | -------------- |
| all()         | enumerate() | int()        | ord()       | str()          |
| any()         | eval()      | isinstance() | pow()       | sum()          |
| basestring()  | execfile()  | issubclass() | print()     | super()        |
| bin()         | file()      | iter()       | property()  | tuple()        |
| bool()        | filter()    | len()        | range()     | type()         |
| bytearray()   | float()     | list()       | raw_input() | unicar()       |
| callable()    | format()    | locals()     | reduce()    | unicode()      |
| chr()         | frozenset() | long()       | reload()    | vars()         |
| classmethod() | getattr()   | map()        | repr()      | xrange()       |
| cmp()         | globals()   | max()        | reversed()  | Zip()          |
| compile()     | hasattr()   | memoryview() | round()     | _import\_()    |
| complex()     | hash()      | min()        | set()       | apply()        |
| delattr()     | help()      | next()       | setattr()   | buffer()       |
| dict()        | hex()       | object()     | slice()     | coerce()       |
| dir()         | id()        | oct()        | sorted()    | intern()       |

> 在Python 2.7中，print是关键字而不是函数。另外，Python 3没有内置函数unicode()。这两个单词都不应用作变量名。

- 慎用小写字母l和大写字母O，因为它们可能被人错看成数字1和0。

