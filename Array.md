## 数组
> 学习目标:创建数组、输出数组、测试数组、添加和删除数组元素、定位数组元素、遍历数组、确定数组大小和元素唯一性、数组排序、数组合并/拆封/接合/分解

PHP 中的数组实际上是一个有序映射。映射是一种把 values 关联到 keys 的类型,每个元素由一个特殊的标识符来区分，称为键(key),通过键来获取其相应的值。

无论关联键或数值键，都依赖数组指针，其如同书签，告诉你正在检查的数组的位置

若不指定具体的键，直接书写值，称为索引数组，默认索引为0，1，2，，，

1. 创建及访问数组

```php
array( key => value, ...)
// 键(key) 可以是 int 或 string
// value可是任意类型
// 最后一个数组单元之后的逗号可以省略

//php5.4后，用[] 替代 array()
// 键名相同 则后面覆盖前面的值
```

key的强制转换:
- 包含有合法整型值的字符串会被转换为整型。例如键名 "8" 实际会被储存为 8。但是 "08" 则不会强制转换，因为其不是一个合法的十进制数值。
- 浮点数也会被转换为整型，意味着其小数部分会被舍去。例如键名 8.7 实际会被储存为 8。
- 布尔值也会被转换成整型。即键名 true 实际会被储存为 1 而键名 false 会被储存为 0。
- Null 会被转换为空字符串，即键名 null 实际会被储存为 ""。
- 数组和对象不能被用为键名。坚持这么做会导致警告：Illegal offset type。

访问数组通过 []

用[]也可新建/修改

- list()提取数组
```php
$test = ['mark', 'alex', 'mike'];
list($mark, $alex, $mike) = $test;
```

- 用预定于的值范围填充数组
```php
$die = range(1, 10);
$even = range(0, 20, 2);
```

- 测试数组

用`is_array()`判断某个特定的变量是否为一个数组

2. 输出数组
> 输出数组内容最常用的方法是迭代处理各个数组键，并输出相应的值

`foreach`迭代，`print_r`打印，作调试用

3. 添加和删除数组元素
> php为扩大或缩小数组提供了一些函数，如果希望模仿各种队列的实现，这些函数会更加方便

队列和栈是一种数据结构，队列: 删除元素与加入元素的顺序相同，称为先进先出，即FIFO;
栈: 删除元素的顺序与加入时的顺序相反，称为先进后出，即LIFO

- 数组头添加元素
`array_unshift()`

- 在数组尾部添加元素
`array_push`

- 从数组头部删除元素
`array_shift`

- 从数组尾删除元素
`array_pop`

4. 定位数组元素

- `in_array`检查数组中是否存在某个值，找到该值返回true，否则返回false

```php
boolean in_array(mixed needle, array haystack [,bool $strict = FALSE])
// 在大海(haystack)中搜索针(needle),没有设置strict则使用宽送比较，即类型，默认needle是区分大小写的
```

- 搜索关联数组键

`array_key_exists()`检查数组里是否有指定的键名或索引,返回true,否则返回false

- 搜索关联数组值

`array_search` — 在数组中搜索给定的值，如果成功则返回首个相应的键名

```php
mixed array_search ( mixed $needle , array $haystack [, bool $strict = false ] )
// strict参数是进行严格比较
```

- 获取数组键

`array_keys` — 返回数组中部分的或所有的键名,可指定值，返回键名

```php
$array = array(0 => 100, "color" => "red");
print_r(array_keys($array));

$array = array("blue", "red", "green", "blue", "blue");
print_r(array_keys($array, "blue"));
```

- 获取数组值

`array_values()` 返回 数组中所有的值,并自动为返回的数组提供数字索引。

5. 遍历数组

- 获取当前数组键

`key()` 返回数组中当前单元的键名

- 获取当前数组值

`current()` 函数返回当前被内部指针指向的数组单元的值

- 获取当前数组键和值

`each` — 返回数组中当前的键／值对并将数组指针向前移动一步

- 移动数组指针

    `next()`
    `prev()`
    `reset()`
    `end()`

- 向函数传递数组值
> `array_walk()`函数将数组中的各个元素传递到用户自定义函数

6. 确定数组的大小和唯一性

- 确定数组的大小

`count()`计算数组中的单元数目，若第二个参数设为1，则递归对数组计数

- 统计数组元素出现的频度

`array_count_values` 返回一个数组： 数组的键是 array 里单元的值； 数组的值是 array 单元的值出现的次数。

- 确定唯一的数组元素

`array_unique()` 移除数组中重复的值，并返回没有重复值得新数组

7. 数组排序

- 设置数组元素顺序

`array_reverse()` 返回单元顺序相反的数组

- 置换数组键和值

`array_flip()` 交换数组中的键和值，注意 array 中的值需要能够作为合法的键名（例如需要是 integer 或者 string）。如果类型不对，将出现一个警告，并且有问题的键／值对将不会出现在结果里。

如果同一个值出现多次，则最后一个键名将作为它的值，其它键会被丢弃。

- 数组排序

① `sort()`对数组进行排序，各元素按值由低到高的排序，可选第二个参数，可设置比较类型，如作为 数字、字符串等来比较

② `asort()` 功能同`sort()`，但保持键值关系

③ 以逆序对数组元素排序, `rsort()`

④ 保持键值对的逆序, `arsort()`

⑤ 自然排序 `natsort()`

```php
$array2 = array("img12.png", "img10.png", "img2.png", "img1.png");
natsort($array2);
print_r($array2);
/*
Array
(
    [3] => img1.png
    [2] => img2.png
    [1] => img10.png
    [0] => img12.png
)
*/
```

⑥ 不区分大小写的自然排序 `natcasesort()`

⑦ 对数组按照键名排序 `ksort()`,主要用于关联数组

⑧ 以逆序对数组键排序, `krsort()`

⑨ `usort()` 使用用户自定义的比较函数对数组中的值进行排序

8. 合并、拆分、结合和分散数组

① `array_merge()` — 合并一个或多个数组

② 递归追加数组 `array_merge_recursive()`

`array_merge()`与`array_merge_recursive()`相同，区别在于，当输入某个数组中的某个键已经存在于结果数组中时，`array_merge()`会覆盖前面存在的键值对，`array_merge_recursive()`会把两个值合并在一起，形成一个新的数组并以原有键作为数组名

③ 合并两个数组 `array_combine`
> `array_combine` — 创建一个数组，用一个数组的值作为其键名，另一个数组的值作为其值

④ 拆分数组 `array_slice()`

array_slice — 从数组中取出一段,可指定取出位置及偏移量,并返回

```php
array array_slice ( array $array , int $offset [, int $length = NULL [, bool $preserve_keys = false ]] )
//array_slice() 返回根据 offset 和 length 参数所指定的 array 数组中的一段序列
```

⑤ 接合数组 `array_splice()`
> 去掉数组中的某一部分并用其它值取代

```php
array array_splice ( array &$input , int $offset [, int $length = count($input) [, mixed $replacement = array() ]] )
// 把 input 数组中由 offset 和 length 指定的单元去掉，如果提供了 replacement 参数，则用其中的单元取代
```

⑥ 求数组交集`array_intersect`

```php
array array_intersect ( array $array1 , array $array2 [, array $... ] )
// array_intersect() 返回一个数组，该数组包含了所有在 array1 中也同时出现在所有其它参数数组中的值。注意键名保留不变
```

⑦ 求关联数组的交集`array_intersect_assoc`

与`array_intersect`不同的是键名也用于比较

⑧ 求数组差集`array_diff`

```php
array array_diff ( array $array1 , array $array2 [, array $... ] )
//对比 array1 和其他一个或者多个数字，返回在 array1 中但是不在其他 array 里的值
```

⑨ 求关联数组的差集`array_diff_assoc`

与`array_diff`的不同是键名也用于比较

9. 其他有用的数组函数

- 返回一组随机的键 `array_rand`

从数组中取出一个或多个随机的单元，并返回随机条目的一个或多个键。

```php
mixed array_rand ( array $array [, int $num = 1 ] )
// num是随机取出的个数
```
- 打乱数组`shuffle`

- 对数组中的值求和 `array_sum`

若数组中包含其他类型数据(如字符串),这些值将被忽略

- 划分数组 `array_chunk`

```php
array array_chunk ( array $array , int $size [, bool $preserve_keys = false ] )
```
将一个数组分割成多个数组，其中每个数组的单元数目由 size 决定。第三个参数，设为 TRUE，可以使 PHP 保留输入数组中原来的键名