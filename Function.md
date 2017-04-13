## PHP函数
> 学习创建和调用函数、传递输入、使用类型提示、为调用者返回一个或多个值，以及创建和包含函数库，了解递归函数和变量函数

1. 调用函数
> 标准的PHP发行包中有1000多个标准函数

2. 创建函数

```php
funcion functionName(parameters)
{
    function-body
}

functionName();
```

- 按值传递
(PHP执行前会把整个脚本督导引擎中，因此不要求非得在调用前定义函数，不推荐)

- 按引用传递参数
(函数内对参数所做的修改也可以体现在函数作用域外)

- 默认参数值
① 默认值

```php
function calcTax($price, $tax=2)
{
    $total = $price + ($price * $tax);
    echo $total;
}
```
**默认参数值必须位于参数列表末尾且为常数表达式，而不能指定为函数调用或变量等非常量值**

② 指定可选参数
> 可选参数位于参数列表末尾且为常数表达式

```php
function calcTax($price, $tax="")
{
    $total = $price + ($price * $tax);
    echo $total;
}
```

③ 指定多个可选参数,可以选择性地传递某些参数

```php
function calculate($price, $price2="", $price3="")
{
    echo $price + $price2 + $price3;
}
calculate(10, "", 3);//可以只传递$price和$price3
```

- 使用类型提示
> 强制参数为某个类的对象或者为数组

- 从函数返回值

`return()`

- 递归函数
> 即调用自身的函数
    可以和静态变量一块来用，注意终止条件