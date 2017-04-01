## php基础
> php的优点之一是可以把php代码直接嵌入到HTML页面中，要让代码完成任务，必须把页面传递给php引擎进行解释，但是web服务器并不传递所有的页面，只传递具有特定文件扩展标识的页面(一般为.php)，在php引擎看来，页面中的每行都可能是php命令，都需要处理，效率低下，所以引擎需要一种方法来确定页面中哪些部分是php代码。

1. 在web中界定php代码

    默认语法: `<?php ?>`
    短标签语法形式如 `<? ?>`，需要开启 `short_open_tag`指令
    其他两种风格不讲

2. 嵌入代码块

    php代码与非php代码可以多次交替出现

3. 注释

    优点: 有利于记忆，有利于团队合作
    ① 单行c++语法       //
    ② 多行c语法         /* */

4. 向浏览器输出

    - `print`
    - `echo`
    - `printf`
    - `sprintf`

    `print`和`echo`都是语言结构,`print`和`echo`唯一区别: `print`仅支持一个参数

    `printf` 输出格式化字符串，即输出静态文本和一个或多个变量存储的动态信息组成的混合产物
    `integer printf(string format [, mixed args])`
    `format`中占位变量通过占位符表示
    常用占位符: 
    `%d` 有符号的十进制整数
    `%u` 无符号的十进制整数
    `%f` 浮点数
    `%s` 字符串

    `sprintf` 与 `printf`功能相同，但它将输出赋给一个字符串，而不是直接呈现到浏览器

例子:

```php
print $test;
print("<p>xxx $test </p>");
print "<p>dddd</p>";

echo $test;

printf("Bar inventory: %d", 100);
printf("%d bottles of %f", 100, 100.11);

$cst = sprintf("$%.2f", 43.2);
```

5 . 数据类型

> 具有相同特性的数据的统称

- 标量数据类型,能够表示单项信息

    ① 布尔型
    ② 整型
    ③ 浮点型
    ④ 字符串型

- 复合数据类型,用于将多个相同类型的项聚集起来，表示为一个实体

    ① 数组
    ② 对象

- 特殊类型,null

    在下列情况下一个变量被认为是 NULL：
    - 被赋值为 NULL
    - 尚未被赋值
    - 被 unset()

- 强制类型转换

    - (array)
    - (bool)或(boolean)
    - (int)或(integer)
    - (object)
    - (real)或(double)或(float)
    - (string)

- 自动类型类型

- 类型相关函数

    - gettype() 获取类型
    - settype() 转换类型

- 类型标识符函数

    `is_array()`,`is_bool()`,`is_float()`,`is_integer()`,`is_null()`,`is_numeric()`,`is_object()`,`is_resource()`,`is_string()`,`is_scalar()`
    `is_name`

6. 标识符
> 是变量、函数和其他各种用户定义对象通用的术语,由一个或多个字符组成，必须以字母或下划线开头。

    - 标识符区分大小写
    - 可是任意长度
    - 不能与任何PHP预定义关键字相同


