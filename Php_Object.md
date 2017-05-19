## 对象基础

主要内容:

- 类和对象: 声明类及实例化对象
- 构造方法: 自动加载对象
- 基本数据类型和类的类型: 为什么类型很重要
- 继承: 为什么需要继承以及如何使用继承
- 可见性: 整合对象接口并保护类中的方法和属性不受干涉

### 类和对象

1. 理解类和对象之间奇妙的关系

类是用于生成对象的代码模板，使用`class`关键字和一个任意的类名来声明类。类名可以是任意数字和字母的组合，但不能以数字开头，和类关联的代码必须用大括号括起来。

对象是根据类中定义的模板所构造的数据，对象可以被说成是类的"实例"，生成对象需要`new`操作符。

```php
class ShopProduct {
    // 类体
}
$product1 = new ShopProduct();
$product2 = new ShopProduct();

// $product1 和 $product2是由同一个类生成的相同类型的不同对象
```

> 打个比方: 把类当做生产塑料鸭子的机器的一个铸模，那么对象就是这台机器生产的鸭子。物品的类型由它们压制出来的模具决定，看起来一样，但它们是不同的个体，即不同的实例。

在php脚本中创建的每个对象有唯一的身份，php会在一个进程内重复使用这些身份来访问这些对象。(通过打印对象可证明)

2. 设置类中的属性
> 类可定义被称为**属性**的特定变量，也加**成员变量**,用来存放对象之间互不相同的数据。

定义: 与标准变量相似，但必须在声明和赋值前加一个关键字，关键字决定了属性的作用域。

通过`->`字符连接对象变量和属性名来访问属性变量。

php没有强制所有的属性都要在类中声明，可动态的增加属性到对象，但这并不是一个好的做法，基本上不用。

如果对象具有在内部处理属性数据的能力，将会非常有利于编程，即可以使用方法.

3. 使用方法
> 属性可以让对象存储数据，类方法可以让对象执行任务

```php
public function myMethod ($argument, $another) {
    // ...
}
```

调用方法时，必须使用一对大括号(即使没有传递任何参数给该方法，类似于函数调用)

`$this` 伪变量把类指向一个对象实例，可以理解为 "当前实例"来替换`$this`

由于初始化时每次都要多行代码去赋值，过于麻烦，其次无法保证在初始化时对象每个属性都被设置了，因此需要一个当类实例化时可被自动调用的类方法，即构造方法。

**创建构造方法**

创建对象时，构造方法(也称为构造器)会被自动调用，通过方法`__construct()`实现

此时，实例化和设置只需一条语句就可完成，属性皆被初始化，在使用对象时，也该确定它的类型，即在声明方法时，可以强制规定参数的对象类型。

4. 参数和类型

**在面向对象开发中，"专注特定任务，忽略外界上下文"是一个重要的设计原则**

**一个类专注于处理一个任务**

**类型提示**

    将类名放在需要约束的方法参数之前

```php
public function write( ShopProduct $shopProduct) {
    // ...
}
// 有了参数的类型提示，就不再需要使用参数前对其进行类型检查
```

类型提示不能用于强制规定参数为某种基本数据类型，比如字符串和整型。如果要处理基本数据类型，则要使用如`is_int`这类的检查函数，但可以强制规定使用数组作为参数:

```php
function setArray( array $storearray ) {
    $this->array = $storearray;
}
```

5. 继承
> 继承是从一个基类得到一个或多个派生类的机制，继承的类称为**子类**，子类可以增加**父类**(也称超类)之外的新功能,因此子类也称为父类的“扩展”

继承可避免功能重复

使用继承:

```php
class CdProduct extends ShopProduct {

}
```
① 构造方法继承

```php 
class CdProduct extends ShopProduct {
    
    function __construct ($params) {
        parent::__construct();
        $this->xx = xx;
    }
}
```

② 直接覆盖
```php
class CdProduct extends ShopProduct {
    
    function getSummaryLine ($params) {
        $base = parent::getSummaryLine();
        $base .= "xxxxxx";;
        return $base;
    }
}
```

③ public、private、protected管理类的访问
> 类中的元素可以被声明为public、private或protected

    在任何地方都可以访问`public`属性

    只能在当前类或子类中访问`private`方法或属性，即使在子类中也不能访问

    可以在当前类或子类中访问`protected`方法或属性

用处: 可见性关键字允许我们只公开类中客户需要的部分，这给对象设置提供了一个清晰的接口

**访问方法: getter 和 setter**
> 客户端程序员需要使用类中保存的值时，通常比较好的做法是不要允许直接访问属性，而是提供方法来取得需要的值，称为访问方法，也称getter和setter

```php
//使用场景
//先来观察以下代码:
abstract class base {
  //do sth
}
class aClass extends base{
  public static function create(){
    return new aClass();
  } 
}
class bClass extends base{
  public static function create(){
    return new bClass();
  }
}
var_dump(aClass::create());
var_dump(bClass::create());
/*
输出：
object(aClass)#1 (0) { } object(bClass)#1 (0) { }
以上aClass和bClass继承于base这个抽象类，但是在两个子类中同时实现了create()这个静态方法。遵从oop思想，这种重复代码应该放在base这个父类中实现。
改进代码
*/
abstract class base {
  public static function create(){
    return new self();
  } 
}
class aClass extends base{
}
class bClass extends base{
}
var_dump(aClass::create());
var_dump(bClass::create());
/*
现在的代码看起来好像已经符合我们之前的想法，将create()方法放在父类里共用了，那我们来运行下看会发生什么。
Cannot instantiate abstract class base in ...
很遗憾，代码好像并没有按照我们预想的那样去运行，父类中的self()被解析为base这个父类，并非继承与他的子类。于是为了解决这个问题，php5.3中引入了延迟静态绑定这个概念。
延迟静态绑定
*/
abstract class base {
  public static function create(){
    return new static();
  } 
}
class aClass extends base{
}
class bClass extends base{
}
var_dump(aClass::create());
var_dump(bClass::create());
/*
这个代码与之前的几乎一致，不同点在于将self换成了static这个关键字，static会解析为子类，而非父类，这样就可以解决上面遇到的问题，这就是php的延迟静态绑定。
最后，运行一下代码，得到了最终想要的结果。
object(aClass)#1 (0) { } object(bClass)#1 (0) { }
*/
```

- 错误处理

**异常**,是从PHP5内置的Exception类(或其子类)实例化得到的特殊对象，Exception类型的对象用于存放和报告错误信息

① 抛出异常
联合使用`throw`和`Exception`对象来抛出异常，这会停止执行当前方法，并负责将错误返回给调用代码。

```php
function __construct( $file ) {
    $this->file = $file;
    if ( !file_exists($file) ) {
        throw new Exception( "file '$file' does not exist" );
    }
}
```


那么抛出异常时，客户端代码怎么知道如何处理异常？如果调用可能会抛出异常的方法，那么可以把调用语句放在try子句中。**try子句必须跟着至少一个catch子句才能处理错误**

```php
try {
    $conf = new Conf('');
    // ...
} catch ( Exception $e ) {
    die( $e->__toString );
}

```

② 异常的子类化
> 若创建用户自定义的异常类，可以从Exception类继承。

这样做两个好处:

    ① 可以扩展异常类的功能

    ② 子类定义了新的异常类型，可以进行自己特有的错误处理

- Final类和方法

final关键字可以终止类的继承。final类不能有子类，final方法不能被覆写

也可为某个类方法声明为final, 但final关键字应该放在其他修饰词之前

(谨慎使用final,将会减少代码的灵活性)

- 使用拦截器
> php提供了内置的拦截器(interceptor)方法，可"拦截"发送到未定义方法和属性的消息。

`__get`     访问未定义的属性时被调用
`__set`     给未定义的属性赋值时被调用
`__isset`   对未定义的属性调用isset时被调用
`__unset`   对未定义的属性调用unset时被调用
`__call`    调用未定义的方法时被调用

`__call`方法对于实现委托很有用

```php
class Person {
    private $writer;
    
    function __construct(PersonWriter $writer) {
        $this->writer = $writer;
    }

    function __call( $methodname, $args ) {
        if ( method_exists( $thiss->writer, $methodname ) ) {
            return $this->writer->$methodname( $this );
        }
    }
}
```

- 析造方法(__destruct)
> 对象被垃圾收集器收集前(即对象从内存中删除之前)自动调用，可以用该方法进行最后必要的清理工作。

- 复制对象 __clone()

```php
class CopyMe(){}
$first = new CopyMe();
$second = $first;
// 注意: $first 和 $second 这两个变量包含指向同一个对象的引用，而没有各自保留一份相同的副本
```

PHP提供`clone`关键字达到 “值赋值” 目的，新生成一个对象

```php
class CopyMe(){}
$first = new CopyMe();
$second = clone $first;
// $second 和 $first 现在是两个不同的对象
```

在对象调用clone时，我们可以控制复制什么。通过`__clone`方法来达到目的，当在一个对象上调用`clone`关键字时，其`__clone()`方法就被被自动调用

- 定义对象的字符串值(__toString)

当打印一个对象时，可通过`__toString`方法来控制输出字符串的格式，注意该方法要返回**字符串类型**值

```php
class Person {
    function getName() { return "bob"; }
    function getAge() { return 44; }
    function __toString() {
        $desc = $this->getName();
        $desc .= "age is ".$this->getAge();
        return $desc;
    }
}
$person = new Person();
print $person;
// bob age is 44
```

对于日志和错误报告，__toString()方法会非常有用，也可用于设计专门用来传递信息的类，如Exception类可以把关于异常数据的总结信息写到`__toString`方法中

- 回调、匿名函数和闭包