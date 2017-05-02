## 基本概念

> 诞生于95年，当初设计的目的就是为了验证前端页面的表单，在拨号上网的年代这绝对是一个令人兴奋的功能，从而流行起来，现在的js已经功能非常全面

一个完整的javascript由三个部分组成:

    ECMAScript(核心)
    DOM(文档对象模型)
    BOM(浏览器对象模型)

我们常见的web浏览器只是ECMAScript实现的宿主环境之一


`<script>`中包含的JavaScript代码将被从上至下依次解释

ECMAScript中的一切(变量、函数名和操作符)都区分大小

按照惯例标识符采用驼峰大小写格式

注释 `// /**/`

**变量:** 松散类型，可以保存任何类型的数据，换句话说每个变量仅仅是一个用于保存值的占位符而已，定义变量时要使用var操作符
（注意: 用var操作符定义的变量将成为定义该变量的作用域中的局部变量）

### 数据类型

    5种简单类型(基本数据类型): Undefined Null Boolean Number String
    1种复合类型: Object

    typeof操作符检测变量，能检测出function类型
   
**undefined**  

undefined类型只有一个值，即特殊的undefined。在使用var声明变量但未对其加以初始化时，这个变量值为undefined

**Null类型**

    只有一个值的特殊类型，null,从逻辑角度看，null值表示一个空对象指针

**Boolean类型**

    true 和 false  两个字面值，之一大小写区分

**Number类型**
    来表示整数和浮点数值

    1. 由于保存浮点数值需要的内存空间是保存整数值的两倍，因此ECMAScript会不失时机的将浮点数值转换为整数值。

        var floatNum1 = 1.0; // 解析为 1

    永远不要测试某个特定的浮点数值,浮点数值计算会产生舍入误差的问题

        if(a + b == 0.3) {// 不要做这样的测试
            alert('you got 0.3.');
        }
     
     2. 数值范围
     	
     		计算得到的结果超过Number.MIN_VALUE 和 Number.MAX_VALUE,将自动转换成 Infinity 和 -Infinity
     		
     `isFinite()` 判断是否有穷
     
     3. NAN

     	Not a Number
     	如 任何数除以0将会返回NaN
     	
     	① 任何设计NaN的操作都会返回NaN
     	② NaN与任何值都不相等
     	
     	`isNaN`
     	
     4. 数值转换
		有三个函数将非数值转换为数值: Number() 、 parseInt() 、 parseFloat()
		
		Number()可用于任何数据类型转换
		
		parseInt()和parseFloat()专门用于把字符串转换为数值
		
		Number()函数转换规则:
			① Boolean转换为 0 或 1
			② 数字值，传入和返回
			③ null 返回 0
			④ undefined 返回NaN
			⑤ 若是字符串，则:
				字符串只包含数字，则转换为十进制数，忽略前导零
				
				字符串包含有效浮点数。。。。
				
				字符串包含16进制数，转化为十进制数
				
				空字符串 => 0
				
				字符串中包含上述格式之外的字符，将转化为 NaN
				
		    ⑥ 若是对象，则调用对象的valueOf()方法，然后依照前面的规则，如果结果是NaN,则调用toSting
		    
		    
	    parseInt()函数会忽略字符串前的空格，直至找到第一个非空字符串，若第一个字符不是数字字符或者负号,将返回NaN,转换空字符串时将会返回NaN.
	    如果第一个字符是数字字符，会继续解析第二个字符，直至解析完或遇到一个非数字字符
	    
    
    
**String类型**

	用单双引号表示，和php相比，单双引号用法完全相同
	
	1. 字符字面量

		也叫转义序列，用于表示非打印字符
		
		\n \t ...
		
	2. 转换字符串

		① toString
		
		② String
		

**Object类型**

	对象是一组数据和功能的集合，对象可通过new操作符后跟要创建的对象类型的名称来创建。
	Object类型是所有它的实例的基础    
 
 
### 操作符
 
**一元加/减 ++ --**
 	
**布尔操作符**

 	! && ||
 	
 	*/%+/
 	
 	注意:
 	如果两个操作数都是字符串，则将第二个操作数与第一个操作数拼接起来
 	
 	如果只有一个操作数是字符串，则将另一个操作数转换为字符串，然后再将两个字符串拼接起来
 	
 	
**关系操作符:**

	< > >= <=
 		
 	如果两个操作符都是字符串，则比较两个字符串对应的字符编码值
 	
 	如果一个操作数是数值，则将另一个操作数转换为一个数值，然后执行数值比较
 	
 	注意: "Brick" < "alphabet"   // true 比较 B 和 a的字符编码
 		 "23" < "3"    // ture, 比较2 和 3的字符编码
 		 "23" < 3      // false  会将23转换为数值比较
 		 
 		 
**相等操作符:**
 	
 	① 相等和不相等---- 先转换，再比较
 	② 全等和不全等---- 仅比较而不转换
 	
 	遵循的比较规则:
 		
 		null 和 undefined 是相等的
 		
 		要比较相等性之前，不能将null 和 undefined转换为其他任何值
 		
**条件操作符**

	（） ？ ：
	
**赋值操作符**

	= *= /= %= += -=
	
**逗号操作符**

	var num1 = 1, num2 = 3;
	

### 语句

	if do-while while for
	
	for-in 枚举对象的属性
	
	break和continue
	
	switch
	
		switch语句可以使用任何类型的数据，每个case的值不一定是常量，可以是变量，甚至表达式
		
		switch在比较值时，使用的是全等操作符，因此不会发生类型转换
		
```javascript
var num = 5;
switch(true) {
	case num < 0:
		alert("less than 0");
		break;
		
	case num >=0 && num <= 10:
		alert("between 0 and 10");
		break;
	case num > 10 && num <= 20:
		alert("between 10 and 20");
		break;
	default:
		alert();
}

```

### 函数

	函数可以封装任意多条语句，可在任何地方、任何时候调用执行，通过function关键字来声明，后跟一组参数及函数体。
	
- 理解参数

	ECMAScript不介意传递进来多少个参数，也不在乎传递参数是什么类型
	
	在函数体内通过arguments对象来访问参数数组，从而获取传递给函数的每一个参数
	
- 没有重载                                                                  


 	
## 变量、作用域和内存问题
> ECMAScript变量可能包含两种不同数据类型的值: 基本类型和引用类型。

	引用类型的值是保存在内存中的对象，在操作对象时，实际上是在操作对象的引用而不是实际的对象
	
- 变量赋值

从一个变量向另一个变量赋值基本类型的值，会在变量对象上创建一个新值，然后把该值复制到新变量分配的位置上

复制引用类型的值，这个值的副本实际上是**一个指针**，指向存储在堆中的一个对象


- 传递参数

	ECMAScript中所有函数的参数都是按值传递的
	
- 检测引用类型
> typeof可以检测数据类型，但无法检测 具体哪一种object

	instanceof操作符可检测具体的类型对象
	
	
当代码在一个环境中执行时，会创建变量对象的一个**作用域链**。
作用域链的用途是:保证对执行环境有权访问的所有变量和函数的有序访问

内部环境可以通过作用域链访问所有的外部环境，但外部环境不能访问内部环境中的任何变量和函数，每个环境都可以向上搜索作用域链，以查询变量和函数名

- 没有块级作用域

	声明变量:
	① 使用var,自动添加到最近的环境中
	② 不使用var,该变量会自动被添加到全局环境中
	
- 具有自动垃圾收集机制

## 引用类型

引用类型的值(对象)是引用类型的实例，引用类型是一种数据结构，用于将数据和功能组织在一起，常被称为类

- Object类型

	创建Object类型的实例两种方式:
	① new Object
	② 对象自面量
		
		var person = {
			name : 'nicholas',
			age : 29
		};	
		属性名可为字符串类型
		
	访问对象的属性:
	① 点 .
	② 方括号 []
	
	建议使用.
	
- Array类型

	数组的每一项可以保存任何类型的数据。
	
	创建数组的基本两种方式:
	
	① Array构造函数
	
		new Array() 可省略new操作符
		
	② 数组字面量表示法
	
		[]
		
	数组的项数保存在 length属性中
	
	栈方法:(后进先出)
		push() 接收任意参数，添加到数组末尾，返回修改后的数组长度
		pop() 从数组末尾移除最后一项，减少数组的length值，返回移除的项
		
	队列方法:(先进先出)
		shift() 移除数组中的第一个项并返回该项
		unshift() 在数组前端添加任意个项并返回新数组的长度
		
	重排序:
		sort() reverse()
		
	操作方法:
	
		concat() 基于当前数组，创建一个新数组
		
		slice() 基于当前数组中的一或多个项创建一个新数组
		
		splice() 
		
	位置方法: 
	
		indexof()
		
		lastIndexOf()
		
	迭代方法:
	
		every()
		filter()
		forEach()
		map()
		some()
		
	归并方法:
	
		reduce()
		reduceRight()
		
		
- Date类型

- RegExp类型

- Function类型
> 函数时对象，函数名是指针

	函数声明:
	
	function sum(num1,num2) {
		return num1 + num2;
	}
	
	函数表达式:
	
	var sum = function(num1,num2) {
		return num1 + num2;
	};

	使用不带圆括号的函数名是访问函数指针，而非调用函数
	
	解析器会率先读取函数声明，使其在执行任何代码前可用，函数表达式等到解析器执行到它所在的行，才会被真正的执行 
	
	函数内部有两个特殊的属性: arguments 和 this, arguments对象还有一个名叫callee的属性，指向拥有这个arguments对象的函数
	
```javascript
// 经典阶乘
function factorial(num) {
	if (num <= 1) {
		return 1;
	} else {
		return num * arguments.callee(num-1)
	}
}
```
	
	this引用的是函数据以执行的环境对象
	
	函数属性：
	
		length 和 prototype
		
	函数方法:
	
		apply() 和 call()
		

## 基本包装类型
	
	ECMAScript提供3个特殊的引用类型: 
	Boolean	Number	 String
	
	每当读取一个基本类型值的时候，后台就会创建一个对应的基本包装类型的对象，从而能够让我们能够调用一些方法来操作这些数据
	
## 单体内置对象
> 由ECMAScript实现提供的、不依赖于宿主环境的对象，这些对象在执行前就已存在；

	开发人员不必显式地实例化内置对象，因为他们已经实例化，已经说过如: Object、 Array、String，还有 Global 和 Math
	
	Global对象:
	
	1. URI编码方法
		encodeURI() encodeURIComponent() decodeURI() decodeURIComponent()
		
	2. eval()方法
		就像是一个完整的ECMAScript解析器
		
	Math对象:
	
	1. Math对象属性
		Math.PI
		
	2. min()和max()方法

	3. 舍入方法
		Math.ceil() Math.floor() Math.round()
		
	4. random()方法
     
     
     
     
     
     
     
     
     
     
     
     
     
     
     
      
  
        
        
        
        
        
        
        
        
        
        
        
        
        