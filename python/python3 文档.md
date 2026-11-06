# 1 python 3

## 1.1 虚拟环境

``` powershell 命令
# Create a new directory for our project
uv init weather
cd weather

# Create virtual environment
uv venv 或 python -m venv .venv

#activate 
.venv\Scripts\activate

# 退出虚拟环境
deactivate
```

``` powershell w命令
# 创建指定版本的虚拟环境
uv venv --python 3.10.16

```

**包管理**：

``` python
#虚拟环境根据 requirements.txt导入包导入(不推荐)
uv pip install -r requirements.txt

#导出安装包列表(不推荐)
uv pip freeze > requirements.txt
```

``` python
# pyproject.toml 安装包（推荐）
# 开发环境使用-e参数
uv pip intasll -e .

#生产环境
pip install --no-cache-dir . -i https://pypi.tuna.tsinghua.edu.cn/simple

#查看虚拟环境包的位置
uv pip show mcp 

#在虚拟环境添加包
uv add "mcp[cli]"
uv add fastmcp

#虚拟环境更新指定版本mcp
uv pip install --upgrade mcp===1.9.1
uv pip install --upgrade fastmcp===2.5.1
```

**pip命令**：

 ```python
 #安装pip：
 python -m ensurepip
 
 #更新pip
 python -m pip install --upgrade pip
 
 #注意：不要使用pip install --upgrade pip更新pip自身，否则会在更新pip的时候删除掉pip
 
 #查看命令
 pip -h 
 
 pip intasll -e .
 
 #安装指定包
 pip install numpy
 
 #删除指定的包
 pip uninstall 包名 
 
 #列出安装的所有包
 pip list
 
 #查看某一个包的具体信息
 pip show 包名 
 
 ```

## 1.2 语法

### 1.2.1 基础语法

**标识符**：由字母、数字和下划线组成，不能以数字开头，区分大小写。

**保留关键字**：

| 类别 | 关键字 | 说明 |
| --- | --- | --- |
| 逻辑值 | `False` `None` `True` | 布尔值，`None`表示空值或无值 |
| 逻辑运算 | `and` `or` `not` | 逻辑值 |
| 条件控制 | `if` `elif` `else` | 条件判断语句 |
| 循环控制 | `for` `while` `break` `continue` | 循环语句 |
| 函数定义 | `def` `return` `lambda` | 定义函数 |
| 类定义 | `class` `del` | 定义类，`del`删除对象引用 |
| 异常处理 | `try` `except` `finally` `raise` | 异常处理语句 |
| 导入模块 | `import` `from` `as` | 导入模块 |
| 异步编程 | `async` `await` | |
| 作用域 | `global` `nonlocal` | |
| 其他 | `assert` `in` `is` `with` `yield` | |
| 其他 | `is` | 比较的是对象身份 |
| 其他 | `pass` | 空语句，用于占位 |

**变量**：

`Python` 中的变量不需要声明。每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。

**多个变量赋值**：

Python 允许你同时为多个变量赋值，`a = b = c = 1`

**注释**：

- 单行注释使用 `#`
- 多行注释使用 `'''` 或 `"""`。
- 注释嵌套，外层使用 `'''` 或 `"""`，内层使用 `#`

```python
'''
这是外部的多行注释
可以包含一些描述性的内容

# 这是内部的单行注释
# 可以嵌套在多行注释中
'''
```

注意：虽然多行字符串在这里被当作多行注释使用，但它实际上是一个字符串，我们只要不使用它，它不会影响程序的运行。

**Docstring 文档字符串**:

`Python` 的 `Docstring`（文档字符串）是一种特殊的注释，用于为函数、类、模块等添加文档说明。它类似于 `Java` 的 `Javadoc`，但更加强大和灵活。

与普通注释不同，`Docstring` 可以通过 `__doc__` 属性直接访问，也可以使用 `help()` 函数查看。

```python
def add(a, b):
    """返回两数之和"""
    return a + b

# 通过 __doc__ 属性访问
print(add.__doc__)  # 输出: 返回两数之和

# 通过 help() 函数查看
help(add) 
```

**inspect 模块提取文档**：

```python
import inspect

def add(a, b):
    """返回两数之和"""
    return a + b

# 使用 inspect.getdoc() 获取文档
print(inspect.getdoc(add))  # 输出: 返回两数之和
```

**缩进**：

`Python` 使用缩进来表示代码块，缩进可以是空格或制表符，但必须一致。

**多行语句**：

使用反斜杠 `\` 或括号 `()` 来实现多行语句。

```python
total = item_one + \
        item_two + \
        item_three
```

在 `[]`, `{}`, 或 `()` 中的多行语句，不需要使用反斜杠 `\`

```python
total = ['item_one', 'item_two', 'item_three',
        'item_four', 'item_five']
```

**按是否可变分类**：

- 不可变数据：`Number`、`String`、`bool`、`Tuple`
- 可变数据：`List`、`Dict`、`Set`

**同一行显示多条语句**:

语句之间使用分号 `;` 分割

#### 1.2.1.1 运算符

**算术运算符**：

假设变量 a=10，变量 b=21：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| `+` | 加法 | `a + b` 结果为 `31` |
| `-` | 减法 | `a - b` 结果为 `-11` |
| `*` | 乘法 | `a * b` 结果为 `210` |
| `/` | 除法 | `b / a` 结果为 `2.1` |
| `//` | 往小的方向取整除 | `b // a` 结果为 `2` |
| `%` | 取余 | `b % a` 结果为 `1` |
| `**` | 幂 | `a**b` 结果为10的21次方 |

**注意**：

- 数值的除法包含两个运算符：`/` 返回一个浮点数，`//` 返回一个整数（向下取整）。
- `//` 得到的并不一定是整数类型的数，它与分母分子的数据类型有关系。
- 在不同的机器上浮点运算的结果可能会不一样。
- 在混合计算时，`Python` 会把整型自动转换为浮点数

**比较运算符**：

假设变量 a 为 10，变量 b 为20：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| `==` | 等于，比较对象是否相等 | `(a == b)` 返回 `False` |
| `!=` | 不等于，比较两个对象是否不相等 | `(a != b)` 返回 `True` |
| `>` | 大于，返回x是否大于y | `(a > b)` 返回 `False` |
| `<` | 小于，返回x是否小于y | `(a < b)` 返回 `True` |
| `>=` | 大于等于，返回x是否大于等于y | `(a >= b)` 返回 `False` |
| `<=` | 小于等于，返回x是否小于等于y | `(a <= b)` 返回 `True` |

**赋值运算符**：

假设变量 a 为 10，变量 b 为 20：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| `=` | 简单的赋值运算符，把右边的值赋给左边 | `c = a + b` 将 `a + b` 的运算结果赋值给 `c` |
| `+=` | 加法赋值运算符，把右边的值加上左边的值，赋给左边 | `c += a` 等价于 `c = c + a` |
| `-=` | 减法赋值运算符，把右边的值减去左边的值，赋给左边 | `c -= a` 等价于 `c = c - a` |
| `*=` | 乘法赋值运算符，把右边的值乘以左边的值，赋给左边 | `c *= a` 等价于 `c = c * a` |
| `/=` | 除法赋值运算符，把右边的值除以左边的值，赋给左边 | `c /= a` 等价于 `c = c / a` |
| `//=` | 取整除赋值运算符，把右边的值除以左边的值，向下取整后赋给左边 | `c //= a` 等价于 `c = c // a` |
| `%=` | 取余赋值运算符，把右边的值除以左边的值，取余数后赋给左边 | `c %= a` 等价于 `c = c % a` |
| `**=` | 幂赋值运算符，把右边的值提升到左边的次幂后赋给左边 | `c **= a` 等价于 `c = c ** a` |
| `:=` | 海象运算符，这个运算符的主要目的是在表达式中同时进行赋值和返回赋值的值。`Python3.8` 新增 | |

```python
# 传统写法
n = 10
if n > 5:
    print(n)

# 使用海象运算符
if (n := 10) > 5:
    print(n)
```

**位运算符**：

假设变量 a 为 60（二进制：`0011 1100`），变量 b 为 13（二进制：`0000 1101`）：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| `&` | 按位与运算符：参与运算的两个值，如果两个相应位都为1，则该位的结果为1，否则为0 | `(a & b)` 输出结果 `12`，二进制解释：`0000 1100` |
| `\|` | 按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1 | `(a \| b)` 输出结果 `61`，二进制解释：`0011 1101` |
| `^` | 按位异或运算符：当两对应的二进位相异时，结果为1 | `(a ^ b)` 输出结果 `49`，二进制解释：`0011 0001` |
| `~` | 按位取反运算符：对数据的每个二进制位取反，即把1变为0，把0变为1。`~x` 类似于 `-x-1` | `~a` 输出结果 `-61`，二进制解释：`1100 0011` |
| `<<` | 左移动运算符：运算数的各二进位全部左移若干位，由 `<<` 右边的数字指定了移动的位数，高位丢弃，低位补0 | `a << 2` 输出结果 `240`，二进制解释：`1111 0000` |
| `>>` | 右移动运算符：把 `>>` 左边的运算数的各二进位全部右移若干位，`>>` 右边的数字指定了移动的位数 | `a >> 2` 输出结果 `15`，二进制解释：`0000 1111` |

**逻辑运算符**：

假设变量 a 为 `10`，变量 b 为 `20`：

| 运算符 | 逻辑表达式 | 描述 | 实例 |
| --- | --- | --- | --- |
| `and` | `x and y` | 布尔与：如果 `x` 为 `False`，`x and y` 将返回 `False`，否则它将返回 `y` 的计算值。 | `(a and b)` 返回 `20` |
| `or` | `x or y` | 布尔或：如果 `x` 是 `True`，它将返回 `x` 的值，否则它将返回 `y` 的计算值。 | `(a or b)` 返回 `10` |
| `not` | `not x` | 布尔非：如果 `x` 为 `True`，返回 `False`。如果 `x` 为 `False`，它将返回 `True`。 | `not(a and b)` 返回 `False` |

**成员运算符**：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| `in` | 如果在指定的序列中找到值返回 `True`，否则返回 `False` | `'H' in 'Hello'` 返回 `True` |
| `not in` | 如果在指定的序列中没有找到值返回 `True`，否则返回 `False` | `'H' not in 'Hello'` 返回 `False` |

**身份运算符**：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| `is` | `is` 是判断两个标识符是不是引用自一个对象 | `x is y`，类似 `id(x) == id(y)`，如果引用的是同一个对象则返回 `True`，否则返回 `False` |
| `is not` | `is not` 是判断两个标识符是不是引用自不同对象 | `x is not y`，类似 `id(a) != id(b)`，如果引用的不是同一个对象则返回结果 `True`，否则返回 `False` |

注意：

- `is` 用于判断两个变量引用对象是否为同一个， `==` 用于判断引用变量的值是否相等
- `id()` 函数用于获取对象内存地址，辅助判断是否为同一个对象。

**运算符优先级**：

从最高到最低优先级的所有运算符， 相同单元格内的运算符具有相同优先级。运算符均指二元运算，除非特别指出。 相同单元格内的运算符从左至右分组（除了幂运算是从右至左分组）：

| 运算符 | 描述 |
| --- | --- |
| `(expressions...)`, `[expressions...]`, `{key: value...}`, `{expressions...}` | 圆括号的表达式 |
| `x[index]`, `x[index:index]`, `x(arguments...)`, `x.attribute` | 读取，切片，调用，属性引用 |
| `await x` | `await` 表达式 |
| `**` | 乘方(指数) |
| `+x`, `-x`, `~x` | 正，负，按位非 NOT |
| `*`, `@`, `/`, `//`, `%` | 乘，矩阵乘，除，整除，取余 |
| `+`, `-` | 加和减 |
| `<<`, `>>` | 移位 |
| `&` | 按位与 AND |
| `^` | 按位异或 XOR |
| `\|` | 按位或 OR |
| `in`,`not in`, `is`,`is not`, `<`, `<=`, `>`, `>=`, `!=`, `==` | 比较运算，包括成员检测和标识号检测 |
| `not x` | 逻辑非 NOT |
| `and` | 逻辑与 AND |
| `or` | 逻辑或 OR |
| `if -- else` | 条件表达式 |
| `lambda` | `lambda` 表达式 |
| `:=` | 赋值表达式 |

#### 1.2.1.2 数字(Number)类型

- `int`: 整型，表示为长整型
- `bool`: 布尔，bool 是 int 的子类
- `float`: 浮点型
- `complex`: 复数型，复数由实数部分和虚数部分构成，可以用a + bj,或者complex(a,b)表示， 复数的实部a和虚部b都是浮点型

**进制**：

- 默认是十进制，整数字面量不允许前导零。
- `0b` 或 `0B` 表示二进制。
- `0o` 或 `0O` 表示八进制。
- `0x` 或 `0X` 表示十六进制。

**注意**：

- `Python3` 中，`bool` 是 `int` 的子类，`True` 和 `False` 可以和数字相加，`True==1`、`False==0` 会返回 `True`，但可以通过 `is` 来判断对象身份。
- `bool` 是 `int` 的子类，因此布尔值可以被看作整数来使用，其中 `True` 等价于 `1`，`False` 等价于 `0`
- 布尔类型可以和其他数据类型进行比较，等同于 `int` 类型的比较。
- 布尔类型也可以被转换成其他数据类型，转换时 `True` 转换成 `1`，`False` 转换成 `0`。
- 可以使用 `bool()` 函数将其他类型的值转换为布尔值。
  - `False`：`None`、`False`、零（`0`、`0.0`、`0j`）、空序列（如 `''`、`()`、`[]`）和空映射（如 `{}`）
  - 其他所有值转换为布尔值时均为 `True`。

**常量**：

| 常量 | 描述 |
| --- | --- |
| `pi` | 数学常量 `pi`（圆周率，一般以π来表示） |
| `e` | 数学常量 `e`，`e`即自然常数（自然常数）。 |

**数学函数(math)**：

| 函数 | 返回值（描述） |
| --- | --- |
| `abs(x)` | 返回数字的绝对值，如abs(-10) 返回 10 |
| `ceil(x)` | 返回数字的上入整数，如math.ceil(4.1) 返回 5 |
| `cmp(x, y)` | 比较函数，如果 `x < y` 返回 -1，如果 `x == y` 返回 0，如果 `x > y` 返回 1。 `Python 3` 已废弃，使用 (x>y)-(x<y) 替换 |
| `exp(x)` | 返回 `e` 的 `x` 次幂（`e` 是自然对数的底数）。如math.exp(1) 返回2.718281828459045 |
| `fabs(x)` | 返回数字 `x` 的绝对值，`fabs()` 函数返回浮点数。如math.fabs(-10) 返回10.0 |
| `floor(x)` | 返回数字 `x` 的下限（小于等于 `x` 的最大整数）。如math.floor(4.9)返回 4 |
| `log(x)` | 如同数学中的 `log`，返回 `x` 的自然对数，以 `e` 为底。如math.log(math.e)返回1.0 |
| `log10(x)` | 如同数学中的 `log10`，返回 `x` 的以 `10` 为底的对数。如math.log10(100)返回 2.0 |
| `max(x1, x2,...)` | 返回给定参数的最大值，参数可以为序列。 |
| `min(x1, x2,...)` | 返回给定参数的最小值，参数可以为序列。 |
| `modf(x)` | 返回 `x` 的整数部分与小数部分，两部分的数值符号与 `x` 相同，整数部分以浮点型表示。 |
| `pow(x, y)` | `x` 的 `y` 次幂。 |
| `round(x [,n])` | 返回浮点数 `x` 的四舍五入值，如给出 `n` 值，则代表舍入到小数点后的位数。其实准确的说是保留值将保留到离上一位更近的一端。 |
| `sqrt(x)` | 返回数字 `x` 的平方根。 |

**随机数函数(random)**：

| 函数 | 返回值（描述） |
| --- | --- |
| `choice(seq)` | 从序列的元素中随机挑选一个元素，比如random.choice(range(10))，从0到9中随机挑选一个整数。 |
| `randrange([start,] stop [,step])` | 从指定范围内，按指定基数递增的集合中获取一个随机数，基数默认值为1。 |
| `random()` | 随机生成下一个实数，它在[0,1)范围内。 |
| `seed([x])` | 改变随机数生成器的种子seed。如果你不了解其原理，你不必特别去设定seed，Python会帮你选择seed。 |
| `shuffle(lst)` | 将序列的所有元素随机排序。 |
| `uniform(x, y)` | 随机生成下一个实数，它在 [x, y] 范围内。 |

#### 1.2.1.3 字符串(String)

- `Python` 中单引号 `'` 和双引号 `"` 使用完全相同。
- 使用三引号(`'''` 或 `"""`)可以指定一个多行字符串。
- 转义符 `\`。
- 反斜杠可以用来转义，使用 `r` 可以让反斜杠不发生转义。 如 `r"this is a line with \n"` 则 `\n` 会显示，并不是换行。
- 按字面意义级联字符串，如 `"this " "is " "string"` 会被自动转换为 this is string。
- 字符串可以用 `+`运算符连接在一起，用 `*` 运算符重复，示例`abc * 2`。
- `Python` 中的字符串有两种索引方式，从左往右以 `0` 开始，从右往左以 `-1` 开始（取值时左闭右开，包含开始，不包含结尾）。
- `Python` 中的字符串不能改变。
- `Python` 没有单独的字符类型，一个字符就是长度为 `1` 的字符串。
- 字符串切片 `str[start:end]`，其中 `start`（包含）是切片开始的索引，`end`（不包含）是切片结束的索引。
- 字符串的切片可以加上步长参数 `step`，语法格式如下：`str[start:end:step]`

**字符串运算符**：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| `+` | 字符串连接 | `'Hello' + 'World'` 输出 `'HelloWorld'` |
| `*` | 重复输出字符串 | `'Hello' * 2` 输出 `'HelloHello'` |
| `[]` | 通过索引获取字符串中字符 | `'Hello'[1]` 输出 `'e'` |
| `[:]` | 截取字符串中的一部分，遵循左闭右开原则，str[0:2] 是不包含第 3 个字符的 | `'Hello'[1:3]` 输出 `'el'` |
| `in` | 成员运算符 - 如果字符串中包含给定的字符返回 `True` | `'H' in 'Hello'` 返回 `True` |
| `not in` | 成员运算符 - 如果字符串中不包含给定的字符返回 `True` | `'M' not in 'Hello'` 返回 `True` |
| `r/R` | 原始字符串 - 原始字符串：所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。 原始字符串除在字符串的第一个引号前加上字母 "r"（可以大小写）以外，与普通字符串有着几乎完全相同的语法。 | `r'\n'` 输出 `'\n'` |
| `%` | 格式字符串 - 格式字符串的语法是 `%` 操作符，后面跟着一个 `format` 函数的调用。 | `'Hello, %s' % 'World'` 输出 `'Hello, World'` |

**字符串格式化**：

| 格式 | 描述 |
| --- | --- |
| `%c` | 格式化字符及其ASCII码 |
| `%s` | 格式化字符串 |
| `%d` | 格式化整数 |
| `%u` | 格式化无符号整型 |
| `%o` | 格式化无符号八进制数 |
| `%x` | 格式化无符号十六进制数 |
| `%X` | 格式化无符号十六进制数（大写） |
| `%f` | 格式化浮点数字，可指定小数点后的精度 |
| `%e` | 用科学计数法格式化浮点数 |
| `%E` | 作用同`%e`，用科学计数法格式化浮点数 |
| `%g` | `%f` 和 `%e` 的简写 |
| `%G` | `%f` 和 `%E` 的简写 |
| `%p` | 用十六进制数格式化变量的内存地址 |
| `%%` | 输出`%`字符 |

**格式化操作符辅助指令**：

| 符号 | 功能 |
| --- | --- |
| `*` | 定义宽度或者小数点精度 |
| `-` | 用作左对齐 |
| `+` | 在正数前面显示加号 `+` |
| `<sp>` | 在正数前面显示空格 |
| `#` | 在八进制数前面显示零（`0`），在十六进制前面显示 `0x` 或 `0X` |
| `0` | 显示的数字前面填充 `0` |
| `%` | 显示百分比符号 |
| `(var)` | 映射变量（字典参数） |
| `m.n.` | `m` 是显示的最小总宽度，`n` 是小数点后的位数（如果可用） |

**字面量格式化字符串(f-string)**：

`f-string` 格式化字符串以 `f` 开头，后面跟着字符串，字符串中的表达式用大括号 `{}` 包起来，它会将变量或表达式计算后的值替换进去

**Unicode 字符串**：

`Python` 中定义一个 `Unicode` 字符串非常简单，只需要在字符串前面加上 `u` 或 `U` 即可

**字符串内建函数**：

| 函数 | 描述 |
| --- | --- |
| `capitalize()` | 将字符串的第一个字符转换为大写 |
| `count(str, beg= 0,end=len(string))` | 返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数 |
| `bytes.decode(encoding="utf-8", errors="strict")` | 以指定的编码格式解码 bytes 对象。默认编码为 'utf-8'。str.encode() 来编码返回bytes 对象 |
| `encode(encoding='UTF-8',errors='strict')` | 以 encoding 指定的编码格式编码字符串，如果出错默认报一个ValueError 的异常，除非 errors 指定的是'ignore'或者'replace' |
| `startswith(substr, beg=0,end=len(string))` | 检查字符串是否是以指定子字符串 substr 开头，是则返回 True，否则返回 False。如果beg 和 end 指定值，则在指定范围内检查。 |
| `endswith(suffix, beg=0, end=len(string))` | 检查字符串是否以 suffix 结束，如果 beg 或者 end 指定则检查指定的范围内是否以 suffix 结束，如果是，返回 True,否则返回 False。 |
| `expandtabs(tabsize=8)` | 把字符串 string 中的 tab 符号转为空格，tab 符号默认的空格数是 8。 |
| `find(str, beg=0 end=len(string))` | 检测 str 是否包含在字符串中，如果指定范围 beg 和 end，则检查是否包含在指定范围内，如果是返回开始的索引值，否则返回 `-1` |
| `rfind(str, beg=0,end=len(string))` | 类似于 find()函数，不过是从右边开始查找。 |
| `index(str, beg=0, end=len(string))` | 跟find()方法一样，只不过如果str不在字符串中会报一个异常。 |
| `rindex( str, beg=0,end=len(string))` | 类似于 index()，不过是从右边开始。 |
| `isidentifier()` | 如果字符串是合法的标识符，返回 True。标识符由字母、数字和下划线组成，不能以数字开头。 |
| `isalnum()` | 检查字符串是否由字母和数字组成，即字符串中的所有字符都是字母或数字。如果字符串至少有一个字符并且所有字符都是字母或数字则返回 True，否则返回 False |
| `isalpha()` | 如果字符串至少有一个字符并且所有字符都是字母或中文字则返回 True, 否则返回 False |
| `isdigit()` | 如果字符串只包含数字则返回 True 否则返回 False。 |
| `isdecimal()` | 检查字符串是否只包含十进制字符，如果是返回 true，否则返回 false |
| `isnumeric()` | 如果字符串只包含数字则返回 True 否则返回 False。 |
| `isspace()` | 如果字符串中只包含空白，则返回 True，否则返回 False。 |
| `istitle()` | 如果字符串是标题化的(见 title())则返回 True，否则返回 False |
| `title()` | 返回"标题化"的字符串,就是说所有单词都是以大写开始，其余字母均为小写 |
| `isupper()` | 如果字符串中至少包含一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True，否则返回 False |
| `islower()` | 如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True，否则返回 False |
| `join(seq)` | 以指定字符串作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串 |
| `len(string)` | 返回字符串长度 |
| `lower()` | 转换字符串中所有大写字符为小写 |
| `upper()` | 转换字符串中的小写字母为大写 |
| `lstrip()` | 截掉字符串左边的空格或指定字符 |
| `rstrip()` | 删除字符串末尾的空格或指定字符。 |
| `strip()` | 在字符串上执行 lstrip() 和 rstrip() |
| `max(str)` | 返回字符串 str 中最大的字母。 |
| `min(str)` | 返回字符串 str 中最小的字母。 |
| `replace(old, new [, max])` | 把 将字符串中的 old 替换成 new,如果 max 指定，则替换不超过 max 次。 |
| `split(str="", num=string.count(str))` | 以 str 为分隔符截取字符串，如果 num 有指定值，则仅截取 num+1 个子字符串 |
| `splitlines([keepends])` | 按照行('\r', '\r\n', \n')分隔，返回一个包含各行作为元素的列表，如果参数 keepends 为 False，不包含换行符，如果为 True，则保留换行符。 |
| `center(width, fillchar)` | 返回一个原字符串居中,并使用空格填充至长度 width 的新字符串，fillchar 可选，指定填充字符 |
| `ljust(width[, fillchar])` | 返回一个原字符串左对齐,并使用空格填充至长度 width 的新字符串，fillchar 可选。 |
| `rjust(width,[, fillchar])` | 返回一个原字符串右对齐,并使用空格填充至长度 width 的新字符串，fillchar 可选。 |
| `zfill(width)` | 返回长度为 width 的字符串，原字符串右对齐，前面填充0 |
| `translate(table,deletechars="")` | 根据 table 给出的表(包含 256 个字符)转换 string 的字符, 要过滤掉的字符放到 deletechars 参数中 |
| `swapcase()` | 翻转字符串中的大小写 |
| `format(*args, **kwargs)` | 格式化字符串 |

#### 1.2.1.4 列表(List)

Python 有 6 个序列的内置类型，但最常见的是列表和元组

列表中元素的类型可以不相同，它支持数字、字符串，甚至可以包含列表（即嵌套列表）。

- 列表写在方括号之间，元素用逗号隔开
- 空列表初始化：`list=[]`
- 列表中的元素是可以改变的
- 列表可以使用 `+`,`*` 操作符进行运算

列表截取的语法：

- `变量[头下标:尾下标]`，或者 `变量[头下标:尾下标:步长]`
- 索引值以 `0` 为开始值，`-1` 为从末尾的开始位置，（取值时左闭右开，包含开始，不包含结尾）
- del list[2]：删除指定下标的元素

**列表函数**：

| 函数 | 描述 |
| --- | --- |
| `len(list)` | 列表元素个数 |
| `max(list)` | 返回列表元素最大值 |
| `min(list)` | 返回列表元素最小值 |
| `list(seq)` | 将元组转换为列表 |

**列表方法**：

| 方法 | 描述 |
| --- | --- |
| `list.append(obj)` | 在列表末尾添加新的对象 |
| `list.count(obj)` | 统计某个元素在列表中出现的次数 |
| `list.extend(seq)` | 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| `list.index(obj)` | 从列表中找出某个值第一个匹配项的索引位置 |
| `list.insert(index, obj)` | 将对象插入列表 |
| `list.pop([index=-1])` | 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值 |
| `list.remove(obj)` | 移除列表中某个值的第一个匹配项 |
| `list.reverse()` | 反向列表中元素 |
| `list.sort( key=None, reverse=False)` | 对原列表进行排序，如果指定参数，则使用比较函数指定的比较函数 |
| `list.clear()` | 清空列表 |
| `list.copy()` | 复制列表 |

#### 1.2.1.5 元组(Tuple)

元组写在小括号 `()` 里，元素之间用逗号隔开。元组中的元素类型也可以不相同

- 元组的元素不能修改
- 元组也可以使用 `+`,`+=`,`*` 操作符进行运算
- 注意构造包含 0 或 1 个元素的元组的特殊语法规则
  - 空元组初始化：`tuple=()`
  - 单个元素元组初始化：`tuple=(1,)`，因为在没有逗号的情况下，`Python` 会将括号解释为数学运算中的括号

元组截取的语法：

- `变量[头下标:尾下标]`，或者 `变量[头下标:尾下标:步长]`
- 索引值以 `0` 为开始值，`-1` 为从末尾的开始位置，（取值时左闭右开，包含开始，不包含结尾）

**内置函数**：

| 函数 | 描述 |
| --- | --- |
| `len(tuple)` | 计算元组元素个数 |
| `max(tuple)` | 返回元组中元素最大值 |
| `min(tuple)` | 返回元组中元素最小值 |
| `tuple(seq)` | 将列表转换为元组 |

#### 1.2.1.6 字典(dict)

字典是一种映射类型，用 `{}` 标识，它是一个 `键(key) : 值(value)` 的集合。键(key) 必须使用不可变类型，且在同一个字典中键必须是唯一的

**注意**：

- 字典的键必须为不可变类型，且不能重复
- 创建空字典使用 `{}`或`dict()`
- `Python 3.7` 起，字典会保持元素的插入顺序，不再是无序的。如果需要有序字典的特性，直接使用普通 `dict` 即可

**内置函数**：

| 函数 | 描述 |
| --- | --- |
| `len(dict)` | 计算字典元素个数，即键的总数 |
| `str(dict)` | 输出字典，以可打印的字符串表示 |
| `type(variable)` | 返回输入的变量类型，如果变量是字典就返回 `dict` |

**内置方法**：

| 方法 | 描述 |
| --- | --- |
| `dict.clear()` | 删除字典内所有元素 |
| `dict.copy()` | 返回一个字典的浅复制 |
| `dict.fromkeys(seq[, value])` | 创建一个新字典，以序列 seq 中元素做字典的键，value 为字典所有键对应的初始值 |
| `dict.get(key, default=None)` | 返回指定键的值，如果键不存在，返回 `default` 值 |
| `key in dict` | 如果键在字典 dict 里返回 True，否则返回 False |
| `dict.items()` | 以列表返回可遍历的(键, 值) 元组数组 |
| `dict.keys()` | 返回一个可遍历的字典键视图 |
| `dict.setdefault(key, default=None)` | 和 `get()` 方法类似, 如果键不存在于字典中，将会添加键并将值设为默认值 |
| `dict.update(dict2)` | 把字典 dict2 的键/值对更新到 dict 里 |
| `dict.values()` | 以列表返回字典中的所有值 |
| `dict.pop(key[, default])` | 删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。 |
| `dict.popitem()` | 返回并删除字典中的最后一对键和值。 |

#### 1.2.1.7 集合(Set)

集合（`Set`）是一种无序、可变的数据类型，用于存储唯一的元素。集合中的元素不会重复，并且可以进行交集、并集、差集等常见的集合操作。

集合使用大括号 `{}` 表示，元素之间用逗号 `,` 分隔。也可以使用 `set()` 函数创建集合

**注意**：

- 创建一个空集合必须用 `set()` 而不是 `{}`，因为 `{}`创建的是一个空字典

**内置方法**：

| 方法 | 描述 |
| --- | --- |
| `add(elem)` | 向集合添加元素 |
| `clear()` | 移除集合中的所有元素 |
| `copy()` | 返回集合的浅拷贝 |
| `difference(set)` | 返回多个集合的差集 |
| `difference_update(set)` | 移除集合中的元素，该元素在指定集合也存在。 |
| `discard(elem)` | 移除指定元素 |
| `intersection(set)` | 返回集合的交集 |
| `intersection_update(set)` | 返回集合的交集，并更新原集合 |
| `isdisjoint(set)` | 判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。 |
| `issubset(set)` | 判断指定集合是否为该方法参数集合的子集。 |
| `issuperset(set)` | 判断该方法的参数集合是否为指定集合的子集 |
| `pop()` | 随机移除元素 |
| `remove(elem)` | 移除指定元素 |
| `symmetric_difference(set)` | 返回两个集合中不重复的元素集合。 |
| `symmetric_difference_update(set)` | 返回两个集合中不重复的元素，并更新到当前集合中。 |
| `union(set)` | 返回两个集合的并集 |
| `update(set)` | 给集合添加元素，添加多个值用逗号分隔 |
| `len(set)` | 返回集合元素个数 |

#### 1.2.1.8 二进制类型(bytes)

`bytes` 类型表示的是不可变的二进制序列（byte sequence）。与字符串类型不同的是，`bytes` 类型中的元素是整数值（0 到 255 之间的整数），而不是 `Unicode` 字符。

`bytes` 类型通常用于处理二进制数据，比如图像文件、音频文件、视频文件等。在网络编程中，也经常使用 `bytes` 类型来传输二进制数据。

创建 `bytes` 对象最常见的方式是使用 `b` 前缀。

#### 1.2.1.9 数据类型转换

**隐式类型转换**：

`Python` 会自动将一种数据类型转换为另一种数据类型，不需要我们去干预，比如`int`值转换为`float`值

**注意**：

- 在混合计算时，Python 会把整型自动转换为浮点数

**显示类别转换**：

| 函数 | 描述 |
| --- | --- |
| `int(x [,base])` | 将 x 转换为一个整数 |
| `float(x)` | 将 x 转换为一个浮点数 |
| `complex(real [,imag])` | 创建一个复数 |
| `str(x)` | 将对象 x 转换为字符串 |
| `repr(x)` | 将对象 x 转换为表达式字符串 |
| `eval(str)` | 计算字符串中的有效 Python 表达式，并返回一个对象 |
| `tuple(s)` | 将序列 s 转换为一个元组 |
| `list(s)` | 将序列 s 转换为一个列表 |
| `set(s)` | 转换为可变集合 |
| `dict(d)` | 创建一个字典。d 必须是一个 (key, value) 元组序列。 |
| `frozenset(s)` | 转换为不可变集合 |
| `chr(x)` | 将一个整数转换为对应的字符 |
| `ord(x)` | 将一个字符转换为它的整数值（Unicode 码点） |
| `hex(x)` | 将一个整数转换为十六进制字符串 |
| `oct(x)` | 将一个整数转换为八进制字符串 |
| `bool(x)` | 将对象 x 转换为布尔值（`True` 或 `False`） |
| `bytes([source[, encoding[, errors]]])` | 将对象转换为不可变字节序列 |
| `bytearray([source[, encoding[, errors]]])` | 将对象转换为可变字节数组 |
| `memoryview(obj)` | 返回给定参数的内存视图对象（不复制数据） |
| `bin(x)` | 将一个整数转换为一个二进制字符串 |
| `ascii(x)` | 返回对象的 `ASCII` 表示，非 `ASCII`字符会被转义 |

#### 1.2.1.10 条件控制

**条件判断关键词**：

| 关键字 / 函数 | 说明 | 示例 |
| --- | --- | --- |
| `if` | 条件判断语句，当条件为 True 时执行代码块 | `if x > 0:` |
| `elif` | 多条件判断分支（else if） | `elif x == 0:` |
| `else` | 所有条件不满足时执行 | `else:` |
| `pass` | 空语句，占位用，保证语法完整 | `if x > 0: pass` |
| `match` | 结构化模式匹配（Python 3.10+，类似 switch） | `match x: case 1: ...` |

**条件判断示例**：

```python
if x > 0:
    print("x is positive")
elif x == 0:
    print("x is zero")
else:
    print("x is negative")
```

**match...case**（Python 3.10+）：

`match` 后的对象会依次与 `case` 后的内容进行匹配，如果匹配成功，则执行匹配到的表达式，否则直接跳过，`_` 可以匹配一切，相当于 `switch` 的 `default`

```python
match x:
    case 1:
        print("x is 1")
    case 2:
        print("x is 2")
    case _:
        print("x is neither 1 nor 2")
```

#### 1.2.1.11 循环控制

**循环关键词**：

| 关键字 / 函数 | 说明 | 示例 |
| --- | --- | --- |
| `while` | 当条件为 True 时，执行循环体 | `while x > 0:` |
| `for` | 遍历可迭代对象（如列表、元组、字符串等） | `for item in iterable:` |
| `break` | 终止当前循环 | `break` |
| `continue` | 跳过当前循环，继续下一次循环 | `continue` |
| `else` | 循环正常结束（未被 break）时执行 | `for i in range(3): ... else: ...` |
| `range(start, stop[, step])` | 生成整数序列，取值：左开右闭，常与 for 循环配合使用 | `range(0, 5)` |
| `enumerate()` | 遍历时同时获取索引和值 | `for i, v in enumerate(list):` |
| `zip()` | 同时遍历多个可迭代对象 | `for a, b in zip(list1, list2):` |
| `pass` | 空语句，占位用，保证语法完整 | `for i in range(5): pass` |

**while 循环**：

如果 `while` 后面的条件语句为 `false` 时，则执行 `else` 的语句块。

``` python
while <expr>:
    <statement(s)>
else:
    <additional_statement(s)>
```

**for 循环**：

`for...else` 语句用于在循环结束后执行一段代码，当循环执行完毕后，会执行 `else` 子句中的代码，如果在循环过程中遇到了 `break` 语句，则会中断循环，此时不会执行 `else` 子句。

```python
for <variable> in <sequence>:
    <statements>
else:
    <statements>
```

#### 1.2.1.12 推导式

`Python` 推导式是一种强大且简洁的语法，适用于生成列表、字典、集合和生成器，可以从一个数据序列构建另一个新的数据序列的结构体

**列表推导式**：

列表推导式是用 `[]` 中括号将各部分括起来

语法：

```python
[表达式 for 变量 in 列表] 
[out_exp_res for out_exp in input_list]

或者

[表达式 for 变量 in 列表 if 条件]
[out_exp_res for out_exp in input_list if condition]
```

示例：

```python
>>> names = ['Bob','Tom','alice','Jerry','Wendy','Smith']
>>> new_names = [name.upper()for name in names if len(name)>3]
>>> print(new_names)
['ALICE', 'JERRY', 'WENDY', 'SMITH']
```

**字典推导式**：

字典推导式是用 `{}` 大括号将各部分括起来

语法：

```python
{ key_expr: value_expr for value in collection }
或
{ key_expr: value_expr for value in collection if condition }
```

示例：

```python
listdemo = ['Google','Runoob', 'Taobao']
# 将列表中各字符串值为键，各字符串的长度为值，组成键值对
>>> newdict = {key:len(key) for key in listdemo}
>>> newdict
{'Google': 6, 'Runoob': 6, 'Taobao': 6}
```

**集合推导式**：

集合推导式是用 `{}` 大括号将各部分括起来

语法：

```python
{ expression for item in Sequence }
或
{ expression for item in Sequence if condition }
```

示例：

```python
>>> setnew = {i**2 for i in (1,2,3)}
>>> setnew
{1, 4, 9}
```

**元组推导式（生成器表达式）**：

元组推导式返回的结果是一个生成器对象。元组推导式是用 `()` 圆括号将各部分括起来

语法：

```python
(expression for item in Sequence)
或
(expression for item in Sequence if condition)
```

示例：

```python
>>> a = (x for x in range(1,10))
>>> a
<generator object <genexpr> at 0x7faf6ee20a50>  # 返回的是生成器对象

>>> tuple(a)       # 使用 tuple() 函数，可以直接将生成器对象转换成元组
(1, 2, 3, 4, 5, 6, 7, 8, 9)
```

#### 1.2.1.13 迭代器与生成器

**迭代器**：

迭代器是一个可以记住遍历的位置的对象。迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。

- 迭代器只能往前不会后退。
- 迭代器有两个基本的方法：
  - `iter()`:创建迭代器对象
  - `next()`：输出迭代器的下一个元素
- 字符串，列表或元组对象都可用于创建迭代器
- 把一个类作为一个迭代器使用需要在类中实现两个方法 `__iter__()` 与 `__next__()`

示例：

```python
>>> list=[1,2,3,4]
>>> it = iter(list)    # 创建迭代器对象
>>> print (next(it))   # 输出迭代器的下一个元素
1
>>> print (next(it))
2
>>>

# for 循环遍历列表 
list=[1,2,3,4]
it = iter(list)    # 创建迭代器对象
for x in it:
    print (x, end=" ")

# 类创建一个迭代器，StopIteration 异常用于标识迭代的完成，迭代10次后停止执行。
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self
 
  def __next__(self):
    if self.a <= 10:
      x = self.a
      self.a += 1
      return x
    else:
      raise StopIteration
 
myclass = MyNumbers()
myiter = iter(myclass)
 
for x in myiter:
  print(x)
```

**生成器**：

在 `Python` 中，使用了 `yield` 的函数被称为生成器（`generator`）。

`yield` 是一个关键字，用于定义生成器函数，生成器函数是一种特殊的函数，可以在迭代过程中逐步产生值，而不是一次性返回所有结果。

跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器。

当在生成器函数中使用 `yield` 语句时，函数的执行将会暂停，并将 `yield`后面的表达式作为当前迭代的值返回。然后，每次调用生成器的 `next()` 方法或使用 `for` 循环进行迭代时，函数会从上次暂停的地方继续执行，直到再次遇到 `yield` 语句。这样，生成器函数可以逐步产生值，而不需要一次性计算并返回所有结果。

示例：

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1
 
# 创建生成器对象
generator = countdown(5)
 
# 通过迭代生成器获取值
print(next(generator))  # 输出: 5
print(next(generator))  # 输出: 4
print(next(generator))  # 输出: 3
 
# 使用 for 循环迭代生成器
for value in generator:
    print(value)  # 输出: 2 1
```

### 1.2.2 with 关键字

`with` 关键字为我们提供了一种优雅的方式来处理文件操作、数据库连接等需要明确释放资源的场景。

`with` 是 `Python` 中的一个关键字，用于上下文管理协议（Context Management Protocol）。它简化了资源管理代码，特别是那些需要明确释放或清理的资源（如文件、网络连接、数据库连接等）。

`with` 语句的优势：

1. 自动资源释放：确保资源在使用后被正确关闭
2. 代码简洁：减少样板代码
3. 异常安全：即使在代码块中发生异常，资源也会被正确释放
4. 可读性强：明确标识资源的作用域

语法：

```python
with expression [as variable]:
    # 代码块
```

- expression 返回一个支持上下文管理协议的对象
- as variable 是可选的，用于将表达式结果赋值给变量
- 代码块执行完毕后，自动调用清理方法

`with`的工作原理：

`with` 语句背后是 `Python` 的上下文管理协议，该协议要求对象实现两个方法：

1. `__enter__()`：进入上下文时调用，返回值赋给 `as` 后的变量
2. `__exit__()`：退出上下文时调用，处理清理工作

示例：

```python
# 文件操作
with open('example.txt', 'r') as file:
    content = file.read()
    print(content)
# 文件已自动关闭
```

```python
# 数据库操作
import sqlite3

with sqlite3.connect('database.db') as conn:
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM users')
    results = cursor.fetchall()
# 连接自动关闭
```

```python
#线程锁
import threading

lock = threading.Lock()

with lock:
    # 临界区代码
    print("这段代码是线程安全的")
```

```python
#临时修改系统状态
import decimal

with decimal.localcontext() as ctx:
    ctx.prec = 42  # 临时设置高精度
    # 执行高精度计算
# 精度恢复原设置
```

**自定义的上下文管理器**：

类实现方式

```python
class Timer:
    def __enter__(self):
        import time
        self.start = time.time()
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        import time
        self.end = time.time()
        print(f"耗时: {self.end - self.start:.2f}秒")
        return False

# 使用示例
with Timer() as t:
    # 执行一些耗时操作
    sum(range(1000000))
```

使用 `contextlib` 模块

```python
from contextlib import contextmanager

@contextmanager
def tag(name):
    print(f"<{name}>")
    yield
    print(f"</{name}>")

# 使用示例
with tag("h1"):
    print("这是一个标题")
```

### 1.2.3 函数

#### 1.2.3.1 自定义函数

- 函数代码块以 `def` 关键词开头，后接函数标识符名称和圆括号 `()`。
- 任何传入参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数。
- 函数的第一行语句可以选择性地使用文档字符串 — 用于存放函数说明。
- 函数内容以冒号 : 起始，并且缩进。
- return [表达式] 结束函数，选择性地返回一个值给调用方，不带表达式的 return 相当于返回 None。

语法：

```python
def 函数名（参数列表）:
    函数体
```

示例：

```python
def max(a, b):
    if a > b:
        return a
    else:
        return b
 
a = 4,b = 5
print(max(a, b))
```

`python` 函数的参数传递：

- 不可变类型：类似 `C++` 的值传递，如整数、字符串、元组。如 fun(a)，传递的只是 a 的值，没有影响 a 对象本身。如果在 fun(a) 内部修改 a 的值，则是新生成一个 a 的对象。

- 可变类型：类似 `C++` 的引用传递，如 列表，字典。如 fun(la)，则是将 la 真正的传过去，修改后 fun 外部的 la 也会受影响

`python` 中一切都是对象，严格意义我们不能说值传递还是引用传递，我们应该说传不可变对象和传可变对象。

**参数**：

调用函数时可使用的正式参数类型：

- 必需参数：必需参数须以正确的顺序传入函数。调用时的数量必须和声明时的一样
- 关键字参数：使用关键字参数允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值。
- 默认参数：调用函数时，如果没有传递参数，则会使用默认参数
- 不定长参数：函数能处理比当初声明时更多的参数，声明时不会命名
  - 一个星号 `*` 的参数会以元组(tuple)的形式导入，存放所有未命名的变量参数
  - 两个星号 `**` 的参数会以字典的形式导入，存放所有未命名的变量参数
- 单独出现星号 `*`的形参，则星号 `*` 后的参数必须用关键字传入
- 强制位置参数(Python3.8+)： 单独斜线`/`的形参，则斜线`/`之前的形参必须使用指定位置参数，不能使用关键字参数的形式。

```python
# 一个星号 * 的参数会以元组(tuple)的形式导入
def printinfo( arg1, *vartuple ):
   "打印任何传入的参数"
   print ("输出: ")
   print (arg1)
   print (vartuple)
 
# 调用printinfo 函数
printinfo( 70, 60, 50 )
```

```python  
# 两个星号 ** 的参数会以字典的形式导入
def printinfo( arg1, **vardict ):
   "打印任何传入的参数"
   print ("输出: ")
   print (arg1)
   print (vardict)
 
# 调用printinfo 函数
printinfo(1, a=2,b=3)
```

单独出现星号 `*`，则星号 `*` 后的参数必须用关键字传入

```python
# 声明函数时，参数中星号 * 可以单独出现
def f(a,b,*,c):
    return a+b+c

f(1,2,c=3) # 正常
```

```python
#形参 a,b 必须使用指定位置参数，c,d 可以是位置形参或关键字形参，而 e 要求为关键字形参:
def f(a, b , /, c, d *, e):
    print(a, b, c, d, e)

# 调用
f(1, 2, c=3, d=4, e=5)  # 正常
f(1, 2, d=4, c=3, e=5)  # 正常
f(1, 2, 3, d=4, e=5)  # 正常
```

#### 1.2.3.2 内置函数

**print**：`print` 默认输出是换行的，如果要实现不换行需要在变量末尾加上 `end=""`

**type**：`type` 函数查看变量的类型，不会认为子类是一种父类类型

**isinstance**：函数查看变量的类型，会认为子类是一种父类类型

**id**: `id` 函数用于获取对象内存地址。

### 1.2.4 模块

`Python` 中的模块（Module）是一个包含 `Python` 定义和语句的文件，文件名就是模块名加上 `.py` 后缀。

模块可以包含函数、类、变量以及可执行的代码。通过模块，我们可以将代码组织成可重用的单元，便于管理和维护。

模块的作用:

- 代码复用
- 命名空间管理
- 代码组织

#### import 语句

想使用 Python 源文件，只需在另一个源文件里在脚本的顶端执行 import 语句，语法如下：

```python
import module1[, module2[,... moduleN]
```

模块的搜索路径:

1. 当前目录。
2. 环境变量 `PYTHONPATH` 指定的目录。
3. `Python` 标准库目录。
4. `.pth` 文件中指定的目录。

#### from … import 语句

`Python` 的 `from` 语句让你从模块中导入一个指定的部分到当前命名空间中，语法如下：

```python
from modname import name1[, name2[, ... nameN]]
```

```python
from fibo import fib, fib2
fib(500)
```

把一个模块的所有内容全都导入到当前的命名空间，不推荐，容易引起命名冲突

```python
from … import * 语句
```

内置的函数 `dir()` 可以找到模块内定义的所有名称

#### 模块别名`as`

```python
import numpy as np  # 将 numpy 模块别名设置为 np
from math import sqrt as square_root  # 将 sqrt 函数别名设置为 square_root
```

#### 标准模块

| 模块名 | 功能描述 |
| --- | --- |
| math | 数学运算（如平方根、三角函数等） |
| os | 操作系统相关功能（如文件、目录操作） |
| sys | 系统相关的参数和函数 |
| random | 生成随机数 |
| datetime | 处理日期和时间 |
| json | 处理 JSON 数据 |
| re | 正则表达式操作 |
| collections | 提供额外的数据结构（如 defaultdict、deque） |
| itertools | 提供迭代器工具 |
| functools | 高阶函数工具（如 reduce、lru_cache） |

#### 包

包是一种管理 `Python` 模块命名空间的形式，采用"点模块名称"。

比如一个模块的名称是 `A.B`， 那么他表示一个包 A中的子模块 B 。

**注意**:

- 当使用 `from package import item` 这种形式的时候，对应的 item 既可以是包里面的子模块（子包），或者包里面定义的其他名称，比如函数，类或者变量

- 形如 `import item.subitem.subsubitem` 这种导入形式，除了最后一项，都必须是包，而最后一项则可以是模块或者是包，但是不可以是类，函数或者变量的名字。

如果包定义文件 `__init__.py` 存在一个叫做 `__all__` 的列表变量，那么在使用 `from package import *` 的时候就把这个列表中的所有名字作为包内容导入。

```python
# file:sounds/effects/__init__.py 中包含如下代码
__all__ = ["echo", "surround", "reverse"]
```

### 特殊变量 `__name__`

在 `Python` 中，`__name__` 和 `__main__` 是两个与模块和脚本执行相关的特殊变量。

`__name__` 和 `__main__` 通常用于控制代码的执行方式，尤其是在模块既可以作为独立脚本运行，也可以被其他模块导入时。

1.`__name__` 变量

`__name__` 是一个内置变量，用于表示当前模块的名称。

`__name__` 的值取决于模块是如何被使用的：

- 当模块作为主程序运行时：`__name__` 的值被设置为 `"__main__"`。
- 当模块被导入时：`__name__` 的值被设置为模块的文件名（不包括 `.py` 扩展名）。

2.`__main__` 的含义

`__main__` 是一个特殊的字符串，用于表示当前模块是作为主程序运行的。

`__main__` 通常与 `__name__` 变量一起使用，以确定模块是被导入还是作为独立脚本运行。

3.常见模式

这种模式允许模块在被导入时不会执行某些代码，而只有在作为独立脚本运行时才会执行这些代码

在 Python 中，常见的做法是在模块的末尾添加以下代码块：

```python
if __name__ == "__main__":
    # 这里的代码只有在模块作为主程序运行时才会执行
    main()
```

```python
# example.py
def greet():
    print("来自 example 模块的问候！")

if __name__ == "__main__":
    print("该脚本正在直接运行。")
    greet()
else:
    print("该脚本作为模块被导入。")
```

### 作用域

`Python` 的作用域一共有 4 种，分别是：

有四种作用域：

- L（Local）：最内层，包含局部变量，比如一个函数/方法内部。
- E（Enclosing）：包含了非局部(non-local)也非全局(non-global)的变量。比如两个嵌套函数，一个函数（或类） A 里面又包含了一个函数 B ，那么对于 B 中的名称来说 A 中的作用域就为 `nonlocal`。
- G（Global）：当前脚本的最外层，比如当前模块的全局变量。
- B（Built-in）： 包含了内建的变量/关键字等，最后被搜索。

`Python` 查找变量时的顺序是： `L –> E –> G –> B`。

- `Local`：当前函数的局部作用域。
- `Enclosing`：包含当前函数的外部函数的作用域（如果有嵌套函数）。
- `Global`：当前模块的全局作用域。
- `Built-in`：`Python` 内置的作用域。

**注意**：`Python` 中只有模块（`module`），类（`class`）以及函数（`def`、`lambda`）才会引入新的作用域，其它的代码块（如 `if/elif/else/`、`try/except`、`for/while`等）是不会引入新的作用域的，也就是说这些语句内定义的变量，外部也可以访问

`全局变量`

在函数外部定义的变量，可以在整个文件中被访问。在函数外部定义的变量对所有函数都是可见的，除非函数内部定义了同名的局部变量。

`局部变量`

在函数内部定义的变量，仅在函数内有效，函数外无法访问。局部变量优先级高于全局变量，因此如果局部变量和全局变量同名，函数内部会使用局部变量。

当内部作用域想修改外部作用域的变量时，就要用到 `global` 和 `nonlocal` 关键字

``` python
# 内部函数修改全局变量
num = 1
def fun1():
    global num  # 需要使用 global 关键字声明
    print(num) 
    num = 123
    print(num)
fun1()
print(num)
```

```python
# 内部函数修改外部函数的变量
def outer():
    num = 10
    def inner():
        nonlocal num   # nonlocal关键字声明
        num = 100
        print(num)
    inner()
    print(num)
outer()
```

### 面向对象

#### 类的属性和方法

`私有属性`

`__private_attrs`：两个下划线开头，声明该属性为私有，不能在类的外部被使用或直接访问。在类内部的方法中使用时 `self.__private_attrs`。

`方法`

在类的内部，使用 `def` 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 `self`, 且为第一个参数，`self` 代表的是类的实例。

`self` 的名字并不是规定死的，也可以使用 `this`，但是最好还是按照约定使用 `self`

`私有方法`

`__private_method`：两个下划线开头，声明该方法为私有方法，只能在类的内部调用 ，不能在类的外部调用。`self.__private_methods`。

`专有方法`

- `__init__` : 构造函数，在生成对象时调用
- `__del__` : 析构函数，释放对象时使用
- `__repr__` : 打印，转换
- `__setitem__` : 按照索引赋值
- `__getitem__`: 按照索引获取值
- `__len__`: 获得长度
- `__cmp__`: 比较运算
- `__call__`: 函数调用
- `__add__`: 加运算
- `__sub__`: 减运算
- `__mul__`: 乘运算
- `__truediv__`: 除运算
- `__mod__`: 求余运算
- `__pow__`: 乘方

#### 继承

基类名必须与派生类定义在一个作用域内。除了类，还可以用表达式，基类定义在另一个模块中时这一点非常有用

```python
class DerivedClassName(BaseClassName):

class DerivedClassName(modname.BaseClassName):
```

`多继承`

``` python
class DerivedClassName(Base1, Base2, Base3):
```

**注意**：圆括号中父类的顺序，若是父类中有相同的方法名，而在子类使用时未指定，`python`从左至右搜索 即方法在子类中未找到时，从左到右查找父类中是否包含方法。

`方法重写`

`super()` 是用来解决多重继承问题的，直接用类名调用父类方法在使用单继承的时候没问题，但是如果使用多继承，会涉及到查找顺序（`MRO`）、重复调用（钻石继承）等种种问题。

`MRO` 就是类的方法解析顺序表, 其实也就是继承父类方法时的顺序表。

```python
class Parent:        # 定义父类
   def myMethod(self):
      print ('调用父类方法')
 
class Child(Parent): # 定义子类
   def myMethod(self):
      print ('调用子类方法')
 
c = Child()          # 子类实例
c.myMethod()         # 子类调用重写方法
super(Child,c).myMethod() #用子类对象调用父类已被覆盖的方法
super().myMethod() #python3单继承简写，用子类对象调用父类已被覆盖的方法
```

`子类继承父类构造函数`

如果在子类中需要父类的构造方法就需要显式地调用父类的构造方法，或者不重写父类的构造方法。

- 子类不重写 `__init__`，实例化子类时，会自动调用父类定义的 `__init__`
- 子类重写了`__init__` 时，实例化子类，就不会调用父类已经定义的 `__init__`
- 子类重写了`__init__` 时，要继承父类的构造方法，可以使用 `super` 关键字

```python
super(子类，self).__init__(参数1，参数2，....)

父类名称.__init__(self,参数1，参数2，...)
```
