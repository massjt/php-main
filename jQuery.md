## jQuery
> 快速简洁的js库

    易上手
    强大的选择器
    解决浏览器兼容
    完善的事件机制
    出色的Ajax封装
    丰富的UI

    特性与工具方法: 链式操作、回调函数、迭代器、延迟对象、队列。。。

【一库在手，天下我有】

**版本**

jQuery 分 2 个系列版本 1.x 与 2.x，主要的区别在于 2.x 不再兼容 IE6、7、8浏览器，这样做的目的是为了兼容移动端开发。由于减少了一些代码，使得该版本比 jQuery 1.x 更小、更快。

`$(document).ready`

    等页面的文档中的节点都加载完毕，再执行后续的代码，因为我们在执行代码的时候，可能会依赖页面的某一个元素，我们要确保这个元素真正的的被加载完毕后才能正确的使用。

```javascript
$(document).ready(function(){

})
```

- jQuery对象与js对象不同

    jQuery对象转化成DOM对象

```javascript
var $div = $('div') //jQuery对象
var div = $div[0] //转化成DOM对象
div.style.color = 'red' //操作dom对象的属性
// 也可用 get方法  div = $div.get(0)
```

- DOM对象转换成jQuery对象
> 如果传递给$(DOM)函数的参数是一个DOM对象，jQuery方法会把这个DOM对象给包装成一个新的jQuery对象,即将普通的dom对象转化为jQuery对象，就可使用jQuery的方法了

## 选择器
> 网页中的任何操作都是以节点为支撑的，如何找到指定节点是开发的重点

- 支持 css1-3选择器写法
> class id element

- 层级选择器
> a b a~b a+b a>b

- 基础筛选选择器

    $(':first') 匹配第一个元素
    $(':last') 匹配最后一个元素
    $(':not(selector)') 过滤
    $(':eq(index)') 匹配集合中选择索引值为index的元素
    $(':gt(index)') 
    $(':lt(index)') 
    $(':even')  匹配索引值为偶数的元素，从0开始计数

- 内容筛选选择器

    $(':contains(text)')    选择所有包含指定文本的元素
    $(':empty')     选择所有没有子元素的元素(包含文本节点)
    $(':has(selector)')     选择元素中至少包含指定选择器的元素

- 属性选择器

    $('div[name=p]')..
    常用选择表单上

    $('input:disabled')
    $('input:checked')
    $('option:selected').removeAttr('selected')

- 特殊的选择器 $(this)
this，表示当前的上下文对象是一个html对象，可以调用html对象所拥有的属性和方法。
$(this),代表的上下文对象是一个jquery的上下文对象，可以调用jQuery的方法和属性值。

**jQuery的属性与样式**

- .attr()与.removeAttr()
- html()与.text()
- val() 获取与设置表单值
- addClass 添加一个样式类名
- removeClass 删除样式
- .toggleClass 切换样式
- .css设置样式，可传入对象

```css
$('.seventh').css({
        'font-size'        :"30px",
        "background-color" :"#40E0D0",
        "border"           :"1px solid red"
    })
```

- 数据存储
    $.data()
    $xx.data

## DOM操作偏
> 删除节点、插入节点、复制节点、查找节点、包裹节点、替换节点

- 节点创建于属性处理

```javascript
$("<div id='test'>XXX</div")
```
- 节点插入

    append appendTo
    after   before
    prepend prependTo
    insertAfter insertBefore

- 节点删除 

    ① remove处理
        注意: remove可过滤

```javascript
$("button:last").on('click', function() {
    //找到所有p元素中，包含了3的元素
    //这个也是一个过滤器的处理
    $("p").remove(":contains('3')")
})
```

    ② empty()处理

    ③ detach()
    该方法不会把匹配的元素从jQuery对象中删除，因而可以在将来使用这些匹配的元素

```javascript
p = $("p").detach();
```

- clone()克隆节点
> 处理dom克隆，复制所有匹配的元素集合，注意: 如果节点有事件或者数据之类的其他处理，需要clone(true)传递一个布尔值true用来指定，即不仅只是克隆节点结构，还把附带的事件与数据给一并克隆了

- DOM替换replaceWith()和replaceAll()

    .replaceWith(HTML字符串、DOM元素、jQuery对象)用来替换选中的节点A

```javascript
$("p:eq(1)").replaceWith('<a href="xx">xxx</a>');
```

    .replaceAll(): 用集合的匹配元素替换每个目标元素

```javascript
$('<a></a>').replaceAll(target)
```

- wrap()包裹方法

```javascript
$('p').wrap('<div></div>');
// <div> <p> p元素 </p> </div>
```

- wrapAll()给集合中的元素用其他元素包裹起来

```javascript
$('p').wrapAll('<div></div>')
```

- unwrap() 删除包裹

    将匹配元素集合的父级元素删除，保留自身(和兄弟元素，如果存在) 在原来的位置

- wrapInner 给集合中匹配的元素的内部，增加包裹html结构

## jQuery遍历

- children
    匹配集合中的第一级子元素

```javascript
$('div').children('.selected')
```

- find 
    查找后代元素

- parent
    匹配的父级元素

```javascript
  $('.item').parent(':last').css('border', '1px')
```

- parents() 查出所有的祖辈元素

- closest()  
    从元素本身开始，在DOM 树上逐级向上级元素匹配，并返回最先匹配的祖先元素

- next()

    直接兄弟元素

- prev()

- siblings() 同辈元素

- add()
    将元素追加到匹配的对象中

```javascript
$('#demo1').add('#demo2')
```

- each()
    for循环迭代器，迭代jQuery对象集合中的每一个DOM元素

```javascript
$("li").each(function(index, element) {
     index 索引 0,1
     element是对应的li节点 li,li
     this 指向的是li
})
```


## jQuery事件

- mouseenter（鼠标进入）
    鼠标移出，能很好地解决冒泡问题、

- mouseleave (鼠标离开)

- hover
    同时绑定mouseenter和mouseleave事件

```javascript
$("p").hover(
    function() {
        $(this).css("background", 'red');
    },
    function() {
        $(this).css("background", '#bbffaa');
    }
);
```

- focusin 
    用户点击聚焦时

- focusout 
    失去焦点

- focus blur
    与focusin、focusout

- change

- select

- submit
    注意表单禁止: return false 和 e.preventDefault()

- keydown/keyup

- keypress 与 keydown/keyup区别

    只能捕获单个字符，不能捕获组合键
    无法响应系统功能键（如delete，backspace）
    不区分小键盘和主键盘的数字字符

- on()多事件绑定

```javascript
$('#ele').on('click',function{})
// 空格分离多事件
$('#ele').on('mouseover mouseout',function(){})

$('#ele').on({
    mouseover: function(){},
    mouseout: function(){}
})
```

- on()高级用法
>注意 由on演变出来的方法，如live(1.7后已去掉) delegate  => 事件委托机制

```javascript
<div class="left">
    <p class="aaron">
        <a>目标节点</a> //点击在这个元素上
    </p>
</div>
$("div").on("click","p",fn)
```

- off() 卸载事件
> 通过on方法绑定事件，通过off方法移除该绑定

```javascript
$('elem').off('mousedown')
$('elem').off();
```

- 事件对象的属性和方法

    event.type 获取事件的类型
    event.pageX event.pageY 获取当前相对于页面的坐标
    event.preventDefault() 阻止事件冒泡
    event.which 获取鼠标单击时，单击的是鼠标的哪个键

- trigger 自定义事件

    绑定在on的事件元素，通过trigger方法就可调用了

```javascript
$('#elem').trigger('click')
```

- triggerHandle


## jQuery动画
> 淡入淡出 上卷下拉

- hide()  show() 方法
    hide("fast/slow")
    $('elem').hide(3000).show(3000)

- toggle
    切换隐藏于显示效果

- slideDown() 下拉动画
> 下拉动画从无到有，一开始需要隐藏

- slideUp() 上卷动画
> 从display: block 到 none

**注意: 因为动画是异步的，所以要在动画之后执行某些操作就必须要写到回调函数里**

```javascript
$("button:last").click(function(){
    $('#a').slideUp(3000,function(){
        alert('')
    })
})
```

- slideToggle 上卷下拉切换

- fadeOut
    淡出隐藏(从有到无)

- fadeIn
    淡出显示(从无到有)

- fadeToggle
    淡入淡出切换

- fadeTo( duration, opacity, callback )

（注意fade都是opacity的变换）

- animate动画

    **语法①:** .animate(properties,[ duration ],[ easing ], [ complete ])

    注意: properties 是一个或多个css属性的键值对所构成的Object对象，所用用于动画的属性必须是**数字**

    css的属性如font-size 写成 fontSize

    每个属性能使用'show' 'hide' 'toggle' 定制隐藏和显示动画

    可使用如 '+=50px' 用法

```javascript
$test.animate({
    width: '+=100px',
    height: '+=100px'
})

$test.animate({
    fontSize: "5em",
    width: 'toggle'
}, 2000, function(){
    alert()
})
```

   **语法②**
   .animate( properties, options )

   duration 设置动画执行的时间
   easing   规定使用easing函数，过度使用混动函数
   step     规定每个东阿虎的每一步完成之后要执行的函数
   progress 每一次动画调用的时候会执行这个回调，就是一个进度的概念
   complete 动画完成回调

- stop 停止动画

    .stop() 停止当前动画，剩余动画执行
    .stop(true) 停止所有动画

- $.each方法
> jQ中非常重要的核心方法，，大部分jQ方法内部都会调用each,原因是jQ实例是一个元素集合

    语法:
        jQuery.each(array, callback)
        jQuery.each(object, callback)

```javascript
$.each(['aaa','bbb'], function(index,value){
    // index 是索引 value是数组中的值
    // return false停止迭代
})
```

- $.inArray
> 判断某个元素是否在数组中

    $.inArray( value, array, [fromIndex])

    判断返回值不等于(或大于)-1来判断

- $.trim
> 去除字符串两端的空白字符

- .get
> 对对象集合中获取某个元素对象的操作,从0开始，可写负数

- .index

    从匹配的元素中搜索到给定元素的索引值，从0开始计数