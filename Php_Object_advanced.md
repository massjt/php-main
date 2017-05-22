## 面向对象高级特性

    静态方法和属性: 通过类而不是对象来访问数据和功能

    抽象类和接口: 设计和实现相分离

    错误处理: 异常

    Final类和方法: 限制继承

    拦截器方法: 自动委托

    析构方法: 对象销毁前的清理工作

    克隆对象: 创建对象的副本

    把对象解析成字符串: 创建摘要型方法

    回调: 用匿名函数为组件添加功能

- 静态方法和静态属性
> 我们不仅可以通过对象访问方法和属性，还可以通过类来访问他们，这样的方法和属性称为"静态的"，必须用static关键字来声明

从当前类中访问静态方法或属性，可以使用self关键字。self指向当前类。

静态方法和属性又被称为类变量和属性，因此不能在静态方法中使用伪变量$this

关键字`static`

静态元素特性：

    ① 在代码中任何地方都可用

    ② 类的每个实例都可以访问类中定义的静态属性(注意: 静态方法都通过实例化的对象来访问，静态成员不能访问)，所以可用静态属性来设置值

    ③ 不需要实例对象就能访问静态属性或方法

- 常量属性
> 错误和状态标志经常需要被硬编码(值始终不变)进类中

关键字`const`

类常量一旦设置后就不能改变，按照惯例，只能用大写字母来命名变量,且不能以美元符开头

给已经声明过的常量赋值会引起解析错误

- 抽象类
> abstract class

**抽象类不能被直接实例化，抽象类中只定义(或部分实现)子类需要的方法。子类可以继承它并且通过实现其中的抽象方法，使抽象类具体化**

```php
abstract class ShopProductWriter {
    protected $products = [];
    //....
}
```

大多数情况下抽象类至少包含一个抽象方法。抽象类使用`abstract`关键字声明，**其中不能有具体内容**,可像声明普通类方法那样声明抽象方法，但要以分号而不是方法体结束。

```php
abstract class ShopProductWriter {
    protected $products = [];

    abstract public function write();
}
```

创建抽象方法后，要确保所有子类中都实现该方法，但实现的细节可以先不确定。

如下:

```php
class ErroredWriter extends ShopProductWriter{}
// 程序将会报错
```

**抽象类的每个子类都必须实现抽象类中的所有抽象方法**，或者把他们自身也声明为抽象方法。

    ① 新的实现方法的访问控制不能比抽象方法的访问控制更严格

    ② 新的实现方法的参数个数应和抽象方法的参数个数一样

- 接口(interface)
> 抽象类提供了具体实现的标准，而接口(interface)则是纯粹的模板。接口只能定义功能，而不包含实现的内容。用关键字interface来声明，接口可以包含属性和方法声明，但是方法体为空。

```php
interface Changeable {
    public function getPrice();
}
```

**任何实现接口的类都要实现接口中所定义的所有方法**

```php
class ShopProduct implements Chargebale {
    //...
    public function getPrice() {
        return ($this->price - $this->discount)
    }
    //...
}
// CdProduct 继承自 ShopProduct,另ShopProduct类中已经有一个getPrice()方法，那么实现Chargeable接口还有用吗？ 
// 有用的！ 实现接口的类接受了它的继承的类及实现的接口类型
/*
    即: CdProduct类同时属于:
    CdProduct ShopProduct Chargeable
*/
```

php只支持继承一个父类，因此extends关键字只能在一个类名前

```php
class Consultancy extends TimedService implements Bookable, Chargeable {

}
```

- 延迟静态绑定: static关键字
> 静态方法可用作工厂方法，工厂方法是生成包含类的实例的一种方法。


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

回调，想jQuery中事件处理完毕后，调用的function一样
利用回调，在运行时将于组件的核心任务没有直接关系的功能插入到组件，有了组件回调，就赋予了其他人在你不知道的上下文中扩展你的代码的权利。

常见函数`call_user_func`和`call_user_func_array`

[参考](http://www.cnitblog.com/CoffeeCat/archive/2009/04/21/56541.html)

**匿名函数**也称闭包函数

```php
$message = 'hello';
$example = function () use (&$message) {
    var_dump($message);
};
// 通过use引用匿名函数其父作用域中声明的变量
```

## 对象工具

- 包(package)将代码逻辑分类打包
- 命名空间，5.3开始将代码元素封装在独立的单元中
- 包含路径: 为类库代码设置访问路径
- 类函数和对象函数: 测试对象、类、属性和方法的函数
- 反射 API 一组强大的内置类，可在代码运行时访问类信息

### PHP和包
> 包是一组相关类的集合，可以把系统的一部分和其他部分分隔开来。

```php
// my.php
require_once "useful/Outputter1.php";
class Outputter {
    // 输出数据
}
// 若包含文件为
// userful/Outputter1.php
class Outputter {
    //
}
// 会报错 redeclare class Outputter
```

导致命名冲突是我们不期望看到的，由此php5.3提出了命名空间

1. 命名空间
> 命名空间就是一个容器，可将类、函数和变量放在其中，在类中可以无条件访问这些，在命名空间外，必须导入或引用命名空间，才能访问。

命名空间声明必须在文件中的第一条语句

访问命名空间中方法的三种方式:

```php
namespace com\getinstance\util;
class Debug {
    static function helloWorld()
    {
        print "hello from Debug\n";
    }
}
```

    ① 在命名空间内部调用方法

```php
Debug::helloWorld();
```

    ② 以绝对路径命名空间访问

```php
namespace main;

\com\getinstance\util\Debug::helloWorld();
```

    ③相对路径命名空间访问

```php
namespace main;
// 引入该命名空间
use com\getinstance\util;
util\Debug::helloWorld();
// 注意: 导入com\getinstance\util命名空间，并隐式的为其使用别名util
```

    ④ 导入Debug类本身

```php
namespace main;
use com\getinstance\util\Debug;

Debug::helloWorld();
```

注意: 若此时 main下已经包含Debug类，则会报错 decalare class
**此时命名冲突的问题，可以显式的使用别名解决**

```php
namespace main;
use com\getinstance\util\Debug as uDebug;
class Debug {

}
uDebug::helloWorld();
```

若在命名空间中编写代码，而你想访问的类保存在全局(非命名空间)空间中，那么应在该名称前加反斜杠

```php
// global.php 无命名空间
class Lister {
    public static function helloWorld() {
        print "hello from global\n";
    }
}

//test
namespace com\getinstance\util;
require_once 'global.php';
class Lister {
    public static function helloWord() {
        print "hello from ".__NAMESPACE__."\n";
    }
}
Lister::helloWorld();// 访问本地
\Lister::helloWorld();// 访问全局空间
```
