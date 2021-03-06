## 对象与设计

- 设计基础: 设计什么？
- 类的内容: 决定一个类中包含什么?
- 封装: 在类的接口后面隐藏实现和数据
- 多态: 使用一个共同的父类，允许在运行时透明地替换特定的子类
- UML: 使用图表来描述面向对象结构

面向对象的系统由一系列类组成，决定系统中这些类的角色是非常重要的，而类由方法组成，必须决定哪些方法应该放在一起。类与类之间常常通过继承关系联系起来以便遵循公用的接口。因此这些接口或类型应该是设计系统时首先要考虑。

面向对象和过程式编程的一个核心区别是如何**分配职责**

过程式编程表现为一系列命令和方法的连续调用，控制代码根据不同的条件执行不同的职责，这种自上向下的控制方式导致了重复和相互依赖代码遍布于整个项目，

**面向对象编程则将职责从客户端代码中移到专门的对象中，尽量减少相互依赖**
> 以下是面向对象设计

- 职责

    过程式代码忙于处理细节，而面向对象只需一个借口即可工作，并不考虑实现的细节。

- 内聚

    是一个模块内部各个成分之间相关联程度数量。

- 耦合

    当系统各部分代码紧密绑在一起时，就会产生紧密耦合，这时在一个组件中的变化会迫使其他部件随之改变。

- 正交/选择类

    我们该如何定义类？ 最好的办法是让一个类只有一个主要的职责，并且任务要尽可能独立。

- 多态

    多态或称类切换，是面向对象的基本特性之一。若代码中存在大量条件语句，就说明需要多态.

- 封装

    是对客户端代码的隐藏数据和功能

- 忘记细节

    要让代码中的结构和关系来引导你，为了强调接口，我们按抽象类而不是具体的子类来思考。

    "为接口而不是实现而编程"

- 四个标志性方向:

    如果改变一个地方的代码，是否要同时修改另一个地方的代码呢？若需要，则这两处代码很可能本应放在同一个地方

    类知道的太多

    万能的类，类的职责过多

    条件语句，类中频繁的进行特定条件的判断，特别是多个地方出现，就说明这个类需要拆分成两个或者更多。


- UML图
> 图形化语法来描述面向对象系统
