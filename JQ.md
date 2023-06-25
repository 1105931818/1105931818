### URL地址的组成部分

1.客户端与服务器之间的通信协议     http

2.存有该资源的服务器名称       www.xxx.com

3.资源在服务器上具体的存放位置    网址后缀



## JQuery对象 $

javascript中获取DOM对象，DOM对象只有有限的属性和方法。

##### 使用jQuery获取的DOM对象叫jQuery包装集对象（伪数组形式存储）

可以说是DOM对象的扩充。在jQuery的世界中，将所有的对象，无论是一个还是一组，都封装成一个jQuery包装集。

​	var  jQueryObject = $( "#testDiv" );

##### DOM对象转jQuery对象，只需利用$ (  )方法进行包装即可。

##### jQuery对象转DOM对象，只需要取数组中的元素即可。

$ ( "div" ) [ index ]

$ ( "div" ) .get[ index ]



## jQuery的入口函数

$ ( function (  ) { 

​	.......  //此处是页面DOM加载完成的入口

 } ) ;

$ ( document ) . ready ( function (  )  { 

​	........  //此处是页面DOM加载完成的入口

 } ) ;

等着DOM结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jQuery帮我们完成了封装

相当于原生js中的DOMContentLoaded

不同于原生js中的load事件是等页面文档、外部的js文件、css文件、图片加载完毕才执行内部代码



## JQuery选择器

jQuery选择器按照功能主要分为“选择”和”过滤“

##### 基础选择器

​	$ ( " 选择器 " )

![image-20230301155044916](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301155044916.png)

##### jQuery筛选选择器

![image-20230301194458416](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301194458416.png)

##### jQuery筛选方法

![image-20230301194735905](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301194735905.png)



##### 层次选择器

![image-20230222092000876](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230222092000876.png)

##### 表单选择器

![image-20230222093051009](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230222093051009.png)

## 隐式迭代

遍历内部DOM元素（伪数组形式存储）的过程就叫做隐式迭代

给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用

##### jQuery排他思想

![image-20230301214210077](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301214210077.png)

##### 链式编程

![image-20230302082423319](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302082423319.png)



## JQuery效果

##### 显示隐藏：show ( ) , hide ( ) , toggle ( )

##### 滑动：slideDown ( ) , slideUp ( ) , slideToggle ( )

##### 淡入淡出：fadeIn ( ) , fadaOut ( ) , fadeToggle ( ) , fadeTo ( )

 	fadeTo ( [speed] , opacity , [easing] , [fn] )

##### 自定义动画：animate ( )

1.显示语法规范   show ( speed , [ easing ] , [ fn ] )

2.显示参数

​	（1）参数都可以省略，无动画直接显示

​	（2）speed：三种预定速度之一的字符串（“slow”，“normal”，“fast"）或表示动画时长的毫秒数值（如：1000）

​	（3）easing：(Optional)用来指定切换效果，默认是“swing”，可用参数“linear”

​	（4）fn：回调函数，在动画完成时执行的函数，每个元素执行一次

##### 事件切换 ：hover（ [over ,] out ）

（1）over：鼠标移到元素上要触发的函数（相当于mouseenter）

（2）out：鼠标移出元素要触发的函数（相当于mouseleave）

#### 动画或效果队列

动画或者效果一旦触发就会执行，如果多次触发，就会造成多个动画或者效果排队执行

##### 停止排队 stop ( )

​	（1）stop方法用于停止动画或效果

​	（2）stop写在动画或者效果的前面，相当于停止结束上一次的动画

#### 自定义动画animate

animate ( params , [speed] , [easing] , [fn] )

（1）params：想要更改的样式属性，以对象形式传递，必须写。属性名可以不用带引号，如果是复合属性则需要采取驼峰命名法

（2）speed：三种预定速度之一的字符串（“slow”，“normal”，“fast"）或表示动画时长的毫秒数值（如：1000）

（3）easing：(Optional)用来指定切换效果，默认是“swing”，可用参数“linear”

（4）fn：回调函数，在动画完成时执行的函数，每个元素执行一次

![image-20230302145904558](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302145904558.png)





## JQuery DOM操作

##### 1.操作元素的属性

##### 1.1获取属性

![image-20230222094108425](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230222094108425.png)

区别：
	1.如果是固有属性，attr ( )和prop ( )方法均可获取

​	2.如果是自定义属性，attr ( )可获取，prop ( )不可获取

​    3.如果是返回值是boolean类型的属性

​		若设置了属性，attr ( )返回具体值，prop ( )返回true

​		若未设置属性，attr ( )返回undefined，prop ( )返回false

##### 1.2设置属性

​	$ ( " 元素 " ) . attr ( "属性名"，“属性值” )

​	$ ( " 元素 " ) . prop ( "属性名"，“属性值” )

注意：prop不能设置自定义属性

##### 1.3移除属性

​	$ ( " 元素 " ) . removeAttr ( "属性" )

##### 数据缓存data ( )

data ( )方法可以在指定的元素上存取数据，并不会修改DOM元素结构。一旦页面刷新，之前存放的数据都将被移除 

![image-20230302180246500](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302180246500.png)

![image-20230302181004998](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302181004998.png)

![image-20230302181335943](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302181335943.png)





##### 2.操作元素的样式

![image-20230222100429180](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230222100429180.png)

CSS ( ) 方法是添加行内样式，优先级更高

![image-20230302083315617](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302083315617.png)

![image-20230302083742119](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302083742119.png)

##### 原生JS中className会覆盖元素原先里面的类名

##### jQuery里面类操作只是对指定类进行操作，不影响原先的类名



##### 3.操作元素的内容

![image-20230222112124261](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230222112124261.png)

![image-20230302181620316](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302181620316.png)

![image-20230302182122399](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302182122399.png)

![image-20230302200944566](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302200944566.png)

parents ( “选择器” )可以返回指定祖先元素

计算结果如果想要保留2位小数，通过toFixed ( 2 )方法







##### 4.创建元素

​	$ ( ' 元素 ' )



##### 5.添加元素

![image-20230222114534057](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230222114534057.png)

注意添加元素的对象是否为jQuery对象

内部添加元素，生成之后，是父子关系

外部添加元素，生成之后，是兄弟关系



##### 6.删除元素

![image-20230222120146655](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230222120146655.png)

html ( )，empty ( )删除匹配的元素集合中所有的子节点

![image-20230302222826848](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302222826848.png)





##### 7.遍历元素

![image-20230222120423399](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230222120423399.png)

调用时要转换为jQuery对象

![image-20230302202508717](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302202508717.png)

![image-20230302203318205](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302203318205.png)

##### jQuery尺寸、位置操作

![image-20230302230730987](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302230730987.png)

![image-20230302234518264](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230302234518264.png)

#####  jQuery位置

位置主要有三个：offset ( )，position ( )，scrollTop ( ) / scrollLeft ( )

（1）offset ( )设置或获取元素偏移

​		offset ( )方法设置或返回被选元素相对于文档的偏移坐标，跟父级没有关系

​		该方法有2个属性left，top。offset ( ).top用于获取距离文档顶部的距离，offset ( ).left用于获取距离文档左侧的距离

​		可以设置元素的偏移：offset ( { top:10 , left: 30 } );

（2）position ( )方法用于返回被选元素相对于带有定位的父级偏移坐标，如果父级都没有定位，则以文档为准

![image-20230303170006015](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230303170006015.png)

（3）scrollTop ( ) / scrollLeft ( )设置或获取元素被卷去的头部和左侧

​		scrollTop ( ) 方法设置或返回被选元素被卷去的头部

![image-20230303171152507](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230303171152507.png)

![image-20230303171431588](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230303171431588.png)

![image-20230305102242082](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230305102242082.png)





## JQuery事件

#### 1.jQuery事件注册

##### 单个事件注册：element.事件 ( function ( ) { } )

##### 事件处理on ( )绑定事件：element.on ( events , [selector] , fn )

​	on ( )方法在匹配元素上绑定一个或多个事件的事件处理函数

​	1.events：一个或多个用空格分隔的事件类型

​	2.selector：元素的子元素选择器

​	3.fn：回调函数

![image-20230305145928338](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230305145928338.png)

![image-20230305153907758](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230305153907758.png)

![image-20230305154524447](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230305154524447.png)

##### 事件处理off ( )解绑事件

​	off ( )方法可以移除通过on ( )方法添加的事件处理程序

![image-20230305180930340](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230305180930340.png)

​	如果有的事件只想触发一次，可以使用one ( )来绑定事件

#### 2.自动触发事件trigger ( )

（1）元素.事件 ( )

（2）元素.trigger ( "事件" )

（3）元素.triggerHandler ( "事件" ) 不会触发元素的默认事件

![image-20230305205957394](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230305205957394.png)



## jQuery事件对象

事件被触发，就会有事件对象的产生

element.on ( events , [selector] , function ( event ) {  } )

阻止默认行为：event.preventDefault ( ) 或者 return false

阻止冒泡：event.stopPropagation ( )



## jQuery对象拷贝

如果想要把某个对象拷贝（合并）给另一个对象使用，此时可以使用$.extend ( )方法

$.extend ( [deep] , target , object1 , [objectN] )

​	1.deep：如果设为true为深拷贝，默认为false浅拷贝

​	2.target：要拷贝的目标对象

​	3.object1：待拷贝到第一个对象的对象

​	4.objectN：待拷贝到第N个对象的对象

​	5.浅拷贝是把被拷贝的对象复杂数据类型中的地址拷贝给目标对象，修改目标对象会影响被拷贝对象。

​	6.深拷贝，前面加true，完全克隆（拷贝的对象，而不是地址），修改目标对象不会影响被拷贝对象。如果里面有不冲突的属性，会合并到一起

注意：

​	如果target里面有 object1相同数据，object1会覆盖掉target的数据



## 多库共存

其他JS库也会用$作为标识符，一起使用时会引起冲突

##### jQuery解决方案

1.把里面的$符号统一改为jQuery

2.jQuery变量规定新的名称：var  自定义名称  =  $.noConflict ( )





## jQuery插件

![image-20230305230552007](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230305230552007.png)

##### 图片懒加载（图片使用延迟加载在可提高网页下载速度，它也能帮忙减轻服务器负载）

当我们页面滑动到可视区域，再显示图片



![image-20230306144621733](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230306144621733.png)



## jQuery AJAX

##### jquery调用ajax方法：$.ajax( { } );

参数：

​	type：请求方式

​	url：请求地址

​	async：是否异步，默认是true表示异步

​	data：发送到服务器的数据

​	dataType：预期服务器返回的数据类型

​	contentType：设置请求头

​	success：请求成功时调用函数

​	error：请求失败时调用函数















































































































