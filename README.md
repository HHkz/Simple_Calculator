# AMI_Calculator

是支持自定义函数的简单计算器，是编译原理小练习。欢迎使用。

# 1 功能

## 1.1 包含

在C++中包含`src/AMI_Calcu.hpp`即可

本库的所有内容均在命名空间`AmiCal`下。

## 1.2 主要接口

|接口|功能|
|:---:|:---:|
|`double etod(const std::string& _expr)`|将`_expr`中的表达式计算为双精度实数|
|`int32_t etoi(const std::string& _expr)`|将`_expr`中的表达式计算为32位整数|
|`float etof(const std::string& _expr)`|将`_expr`中的表达式计算为单精度实数|
|`int get_error_code(const std::string& _expr)`|对`_expr`执行一遍运算程序，并返回其发生的首个错误之错误码。如无错误发生，返回0|
|`void insert_function(const std::string &id, double(*f)(const std::vector<double>&))`|插入一个自定义函数，一次运行有效|
|`void insert_macro(const std::string &macro, const std::string &value)`|插入一个自定义宏，一次运行有效|

## 1.3 表达式

### 1.3.1 常数

以下是可被接受的常数值类型：

1. `十进制数串`，形如`123`, `114514`
2. `十进制数串.十进制数串`，形如`123.456`, `0.123`
3. `.十进制数串`，形如`.123`

### 1.3.2 算符

以下是可被接受的运算符类型：

`+`, `-`, `*`, `/`, `\`, `%`, `(`, `)`, `,`

(下述的优先级，数字越大表示越先被计算)

1. `+`运算符是左结合的，返回左右值的算术和。优先级为1。
2. `-`运算符是左结合的，返回左右值的算术差值。优先级为1。  
   表示取相反数的`-`是右结合的，但只要不是在首位使用它，均需要用括号标注。  
   比如，程序处理`-1+3`可以得出正确的结果，但是处理`-1--3`会报出语法错误，须写为`-1-(-3)`才可以得出正确结果
3. `*`运算符是左结合的，返回左右值的算术积。优先级为2。
4. `/`运算符是左结合的，返回左右值的算术商，自动取浮点数。优先级为2。
5. `\`运算符是左结合的，返回左右值的算术商，向下取整。优先级为2。
6. `%`运算符是左结合的，返回左右值的除余数。优先级为2。
7. `(`, `)`用于标示计算优先级，也用于标示参数列表
8. `,`用于分隔参数，左结合，优先级低于任何其他算符。

### 1.3.3 函数

`AMI_Calculator`函数定义为形如`ID(Para1, Para2, ..)`的形式，参数支持任意多个。

#### 1.3.3.1 预定义函数

`AMI_Calculator`提供以下预定函数

|函数|语法|功能|示例|
|:---:|:---:|:---:|:---:|
|`sin`|`sin(double)`|返回参数的弧度-正弦值|`sin(3)`|
|`cos`|`cos(double)`|返回参数的弧度-余弦值|`cos(2)`|
|`pow`/`power`|`pow(double, double)`|返回第一参数的第二参数次幂|`pow(2,2)`|

预定函数在调用时会执行语义检查，如参数个数与定义不匹配，会返回一个警告或者错误。

#### 1.3.3.2 自定义函数

你可以使用接口`insert_function(str, function)`来将一个`std::string`与一个`double(*)(const vector<double>&)`绑定起来。在绑定之后，`AMI_Calculator`即可识别你的自定义函数。

若自定义函数的`std::string`与现有函数产生冲突，以最后一次覆盖为准。

自定义函数不会自动执行语义检查，应在函数体内自行实现。

### 1.3.4 宏

`AMI_Calculator`宏定义为两个`$`之间的字符串。宏在预处理阶段展开为固定的字符串，后交由后端计算。

#### 1.3.4.1 预定义宏

`AMI_Calculator`提供以下预定宏

|宏|展开结果|
|:---:|:---:|
|`e`|`2.718281828`|
|`pi`|`3.141592654`|

#### 1.3.4.2 自定义宏

你可以使用接口`insert_macro(macro, value)`来将一个`std::string`与一个`std::string`绑定起来。在绑定之后，`AMI_Calculator`即可识别你的宏。`macro`中的宏不需要加`$`。

若自定义宏的`std::string`与现有宏产生冲突，以最后一次覆盖为准。

## 1.4 错误处理

`AMI_Calculator`具有简单的错误处理能力。

### 1.4.1 错误信息

1. `Ami000 - Complete`, 返回码`0`。正确完成全部计算过程。只会在`get_error_code`过程中出现。
2. `Ami001 - Lexical error`, 错误码`1`, 词法错误。说明你的串中存在着不符合词法规范的词法单元。在发生此错误之时，`AMI_Calculator`会指出错误串开始的位置和词法单元的词法值。
3. `Ami002 - Syntax error`, 错误码`2`, 语法错误。说明你的串虽然词法正确，但其中存在着不符合语法规范的词法单元组合。在发生此错误之时，`AMI_Calculator`会指出错误词法单元开始的位置和词法单元的词法值。
4. `Ami003 - Math error`, 错误码`3`, 运算过程中错误。很大可能是因为为一个函数传入了错误个数的参数。
5. `Ami0031 - Semantic warning`, 语义警告。你为一个函数传入了过多的参数，程序会删掉参数列表末尾的超出规定个数的参数，但程序仍可以运行。
6. `Ami0032 - Semantic error`, 错误码`3`, 语义错误。你为一个函数传入了过少的参数。
7. `Ami004 - Preprocesser error: undefined macro`, 错误码`4`, 预处理器错误: 未定义宏。你输入了一个未定义的宏。
8. `Ami005 - Preprocesser error: unclosed macro`, 错误码`5`, 预处理器错误: 非闭合的宏符号。你输入了奇数个`$`符号。
9. `Ami100 - Inner error`, 错误码`100`, 这个错误的引发者不是你。看到这个请将你的输入写入`issue`中。

### 1.4.2 错误返回值

一旦触发上述任何错误，所有计算接口的返回值都将统一为：

|接口|错误返回值|
|:---:|:---:|
|`etod`|`NaN`|
|`etof`|`NaN`|
|`etoi`|`0`|

# 2 实现

## 2.1 过程

整个分析过程是工厂式链式过程。

### 2.1.1 预处理

预处理器检查整个串，将串中所有的控制字符转为空格，同时检查所有输入串中的宏，将其展开为合适的形式或报错。

预处理器由三个简单的函数构成，在`Pre_p`中定义。

### 2.1.2 词法分析

词法分析使用确定有限状态自动机完成。

在正常的计算程序中，基于对语法分析稳定性的考虑，词法分析会预先执行一遍来排查词法错误，如无词法错误，即复位词法分析器，与语法分析协同执行词法分析。

### 2.1.3 语法分析

语法分析基于LL(1)文法，使用递归下降预测分析方法执行。

产生式中的终结符号大部分被表现为语法树属性，少部分直接被舍弃。语法树中的节点全是非终结符。

返回一颗语法树。

### 2.1.4 语法树剪枝

去除文法中空产生式导致的`nullptr`子指针，以防在遍历时产生段错误。

由于空产生式只推导至非终结符号的最右侧，所以只需调用`std::vector`的`pop_back`方法即可。

### 2.1.5 语法树求值

使用继承属性求值。求值的实际过程已经写入了语法树节点的类方法中。这一步尤其烧脑，我都不知道自己是怎么写出来的。

语义分析会在此部分协同进行。

## 2.2 规约

### 2.1.1 词法规约

#### 2.1.1.1 正则表达式

#### 2.1.1.2 DFA

由于这个正则实在是太简单，无需通过NFA即可脑补出DFA

### 2.1.2 语法规约

#### 2.1.2.1 产生式

#### 2.1.2.2 FIRST

#### 2.1.2.3 FOLLOW

## 3 其他

### 3.1 错误提交

如发生错误码为`100`的错误提示、由本库引发的C++内部异常或段错误，请将你的输入或操作序列和错误细节写入issue。

不胜感激！

### 3.2 作者

### 3.3 开源协议

本库使用MIT协议开源。协议已附加到库的根目录。