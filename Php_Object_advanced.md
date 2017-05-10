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