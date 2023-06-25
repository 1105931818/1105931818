## javascript的组成

##### 1，javascript语法（ECMAScript）

​	ECMAScript : ECMAScript规定了JS的编程语法和基础核心知识，是所有浏览器厂商共同遵守的一套JS语法工业标准。

##### 2，页面文档对象模型（DOM）

​	文档对象模型（Document Object Model，简称DOM），是W3C组织推荐的处理可扩展标记语言的标准编程接口。通过DOM提供的接口可以对页面上的各种元素进行操作。

##### 3，浏览器对象模型（BOM）

​	BOM（Browser Object Model，简称BOM）是指浏览器对象模型，它提供了独立于内容的，可以与浏览器窗口进行互动的对象结构。通过BOM可以操作浏览器窗口，比如弹出框，控制浏览器跳转，获取分辨率等。



#### javascript输入输出语句

|      方法      |              说明              |  归属  |
| :------------: | :----------------------------: | :----: |
|  alert（msg）  |        浏览器弹出警告框        | 浏览器 |
| console（msg） |    浏览器控制台打印输出信息    | 浏览器 |
| prompt（msg）  | 浏览器弹出输入框，用户可以输入 | 浏览器 |



## 变量的使用

##### 1.声明变量

 	var age；  / /声明一个名称为age的变量

​	 var是一个JS关键字，用来声明变量（variable）。使用该关键字声明变量后，计算机会自动为变量分配内存空间

##### 2.赋值

​	 age = 18；  

##### 3.变量的初始化

​	 var age = 18；

##### 声明变量特殊情况

|            情况             |         说明         |   结果    |
| :-------------------------: | :------------------: | :-------: |
| var age;  console.log(age); |     只声明不赋值     | undefined |
|      console.log(age);      | 不声明不赋值直接使用 |   报错    |
| age = 18；console.log(age)  |     不声明只赋值     |    18     |

##### javascript是一种弱类型或者说动态语言。这意味着不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。同时也意味着相同的变量可用作不同的类型；



## 数据类型

#### 数据类型的分类

JS把数据类型分为两类：

##### 1.简单数据类型（Number，String，Boolean，Undefined，Null）		

| 简单数据类型  |              说明              |  默认值   |
| :-----------: | :----------------------------: | :-------: |
|    Number     |  数字型，包含整型值和浮点型值  |     0     |
| StringBoolean |           布尔值类型           |   false   |
|    String     |           字符串类型           |    “ ”    |
|   Undefined   | var a；声明了变量a但是没有赋值 | undefined |
|     Null      |          var a = null          |   null    |

​	1.数字型

​		数字前面加0表示八进制，加0X表示十六进制。

​		Number.MAX_VALUE 数字型的最大值

​		Number.M IN_VALUE 数字型的最小值

​		infinity代表无穷大，大于任何数值。- infinity代表无穷小，小于任何数值

​		NaN，Not a number代表一个非数值	

​	2.字符串

​		JS可以用单引号嵌套双引号，或者双引号嵌套单引号

| 转义符 | 解释说明 |
| :----: | :------: |
|  \ n   |  换行符  |
|  \ \   |   斜杠   |
|  \ '   |  单引号  |
|  \ "   |  双引号  |
|  \ t   | tab缩进  |
|  \ b   |   空格   |

​		多个字符串之间可以使用+进行拼接，其拼接方式为字符串+任何类型=拼接之后的新字符串

##### 		数据类型转换

##### 				转换字符型

|        方式        |             说明             |          案例           |
| :----------------: | :--------------------------: | :---------------------: |
|    toString ( )    |          转成字符串          | var n=1;n.toString ( ); |
| String ( )强制转换 |          转成字符串          |  var n=1;String ( n);   |
|   加号拼接字符串   | 和字符串拼接的结果都是字符串 |    var n=1;(n+" ");     |

​		推荐使用第三种，隐式转换

##### 				转换数字型

|          方式          |             说明             |         案例         |
| :--------------------: | :--------------------------: | :------------------: |
|      parselnt ( )      | 将string类型转换为整数数值型 |  parselnt ( '78' )   |
|     parseFloat ( )     | 将string类型转换为浮点数值型 | parseFloat ( '8.2' ) |
|       Number ( )       |   将string类型转换为数值型   |   Number ( '12' )    |
| js隐式转换（减 乘 除） |     利用算术运算隐式转换     |       '12' - 1       |

​		parselnt ( '120px' )会去掉px这个单位

##### 		转换为布尔型

​		Boolean（）函数。代表空，否定的值会被转换为false，如‘ ’，0，NaN，null，undefined。其余值都会转换为true

##### 2.复杂数据类型（object）



## Javascript操作符

#### 1.运算符

##### 	算术运算符

​		浮点数在算数运算里面会有问题

##### 	递增和递减运算符

##### 	比较运算符

​		== 会默认转换数据类型，=== 全等 要求值和数据类型都一致

##### 	逻辑运算符

| 逻辑运算符 |    说明     |     案例      |
| :--------: | :---------: | :-----------: |
|     &&     | 逻辑与，and |  true&&false  |
|    ｜｜    | 逻辑或，or  | true\|\|false |
|     ！     | 逻辑非，not |     !true     |

​		短路运算：当有多个表达式（值）时，左边的表达式可以确定结果时，就不再继续运算右边的表达式的值

​		表达式1&&表达式2，如果第一个表达式为真，则返回表达式2。如果第一个表达式为假，则返回表达式1

​		表达式1｜｜表达式2，如果第一个表达式为真，则返回表达式1。如果第一个表达式为假，则返回表达式2

##### 	赋值运算符

##### 	运算符优先级

| 优先级 |   运算符   |    顺序    |
| :----: | :--------: | :--------: |
|   1    |   小括号   |    （）    |
|   2    | 一元运算符 | ++，--，！ |
|   3    | 算术运算符 |            |
|   4    | 关系运算符 |    > >=    |
|   5    | 相等运算符 |            |
|   6    | 逻辑运算符 | 先&&后｜｜ |
|   7    | 赋值运算符 |     =      |
|   8    | 逗号运算符 |     ，     |



##   Javascript流程控制

流程控制主要有三种结构，分别是顺序结构，分支结构和循环结构。

#### 分支结构

##### 	if语句

​		if（条件表达式）{

​			执行语句1

​		} else {

​			执行语句2

​		}

##### 	三元表达式

​		条件表达式 ？表达式1 ：表达式2

​		如果条件表达式结果为真，则返回表达式1的值。条件表达式结果为假，则返回表达式2的值。

##### 	switch语句

​		switch（表达式）{

​			case  value1:

​				执行语句1；

​				break；

​			case  value2:

​				执行语句2；

​				break；

​			。。。

​			default：

​				执行最后的语句；

​		}

​	注意：表达式的值和case的值相匹配的时候是全等，必须是值和数据类型一致

#### 循环结构

##### 	for循环

​		for（初始化变量；条件表达式；操作表达式）{

​			循环体

​		}

##### 	while循环

​		while（条件表达式）{

​			循环体

​		}

##### 	do...while循环

​		该循环会先执行一次代码块，然后对条件表达式进行判断。

 		do {

​			循环体

​		}while（条件表达式）

##### 	continue关键字用于立即跳出本次循环，继续下一次循环

##### 	break关键字用于立即跳出整个循环



## javascript数组

#### 数组的创建方式

​	利用new创建数组，var 数组名 = new  Array（）；//创建了一个空数组

​	利用数组字面量创建数组，var 数组名 = [ ' ' , ' ' ....];

##### 数组中可以存放任意类型的数据

​	push( )

​	pop( )

​	shift( )

​	unshift( )

​	splice( )

​	sort( )

​	reverse( )

​	filter( )



## javascript函数

##### 声明函数

function  函数名（）{

​	函数体

}

##### 函数形参和实参个数不匹配问题

如果实参的个数和形参的个数一致，则正常输出结果

如果实参的个数多于形参的个数，会取到形参的个数

如果实参的个数小于形参的个数，多于的形参定义为undefined

##### 函数返回值注意事项

return终止函数，后面的代码不会执行

return只能返回一个值，如果有多个值，值返回最后一个值，可以通过数组返回多个值

如果函数没有return，则返回undefined

##### arguments的使用

当我们不确定有多少个参数传递时，可以用arguments来获取。在javascript中，arguments实际上它是当前函数的一个内置对象。所有函数都内置了一个arguments对象，arguments对象中存储了传递的所有实参。

##### arguments展示形式是一个伪数组，因此可以进行遍历。伪数组具有一下特点：

​	具有length属性

​	按索引方式存储数据

​	不具有数组的push，pop等方法



## javascript作用

通常来说，一段程序代码中所用到的名字并不总是有效和可用的，而限定这个名字的可用性的代码范围就是这个名字的作用域。作用域的使用提高了程序逻辑的局部性，增强了程序的可靠性，减少了名字冲突。

##### var a = b = c = 9 ;相当于var a = 9 ; b = 9 ; c = 9 ; b和c没有声明直接赋值

##### 如果在函数内部没有声明直接赋值的变量也属于全局变量，函数的形参也可以看做是局部变量

#### 作用域链

只要是代码，就至少有一个作用域

写在函数内部的局部作用域

如果函数中还有函数，那么在这个作用域中就有可以诞生一个作用域

根据在内部函数可以访问外部函数变量的这种机制，用链式查找决定哪些数据能被内部函数访问





## javascript预解析

javascript解析器在运行javascript代码的时候分为两步：预解析和代码执行

##### 预解析分为变量预解析（变量提升）和函数预解析（函数提升）

变量提升：把所有的变量声明提升到当前的作用域最前面，不提升赋值操作

函数提升：把所有的函数声明提升到当前作用域的最前面，不调用函数



## javascript对象

在javascript中，对象是一组无序的相关属性和方法的集合，所有的事物都是对象，例如字符串，数值，数组，函数等。

#### 创建对象

##### 利用字面量创建对象

​	利用{ }里面包含了表达这个具体事物（对象）的属性和方法

​	var obj = {

​		name : 'mzk' ,

​		age : 18 , 

​		sex : '男' , 

​		sayHi : function( ) {

​			alert('hi~') ; 

​		}

​	}

​	里面的属性或者方法我们采取键值对的形式，多个属性或者方法中间用逗号隔开，方法冒号后面跟的是一个匿名函数

​	调用对象的属性：对象名 . 属性名 或者 对象名 [ '属性名' ]

​	调用对象的方法：对象名 . 方法名（）

##### 利用new Object创建对象

​	var obj = new Object ( ) ;

​	obj . name = 'mzk' ;

​	obj . sayHi = function ( ){

​		alert('hi~') ; 

​	}

​	利用等号赋值的方法添加对象的属性和方法，每个属性和方法之间用分号结束

##### 利用构造函数创建对象

是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与new运算符一起使用。我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面。

​	function 构造函数名（形参）{

​		this . 属性 = 值；

​		this . 方法 = function（形参）{

​		}

​	}

​	var 对象名 = new  构造函数名（实参）；

​	对象名 . 方法（实参）；

​	构造函数名字首字母要大写，构造函数不需要return就可以返回结果

​	利用构造函数创建对象的过程称为对象的实例化

##### new关键字的执行过程

​	1.在内存中创建一个新的空对象

​	2.this指向这个新的对象

​	3.执行构造函数里面的代码，给这个新对象添加属性和方法

​	4.返回这个新对象

#### 遍历对象属性

for...in语句用于对数组或者对象的属性进行循环遍历

for（变量k in 对象）{

​	循环体；

​	变量k输出得到的是属性名。对象[变量k]得到的是属性值

}



## javascript内置对象

javascript中的对象分为3种：自定义对象，内置对象，浏览器对象

内置对象就是指javascript语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是最基本而必要的功能（属性和方法）	

javascript提供了多个内置对象：Math，Date，Array，String等

##### Math数学对象不是一个构造函数，不需要new来调用，直接使用里面的属性和方法

##### 检测是否为数组

​	数组名  instanceof  Array 

​	Array.isArray ( 参数 ) 

##### 添加删除数组元素

​	末尾添加：数组名.push( 参数 )   //push完毕之后，返回的结果是新数组的长度

​	开头添加：数组名.unshift( 参数 )   //unshift完毕之后，返回的结果是新数组的长度

​	末尾删除：数组名.pop(  )   //一次删除一个，不用带参数，返回值为删除的元素值

​	开头删除：数组名.shift(  )   //一次删除一个，不用带参数，返回值为删除的元素值

##### 数组排序

|   方法名   |             说明             |       是否修改原数组       |
| :--------: | :--------------------------: | :------------------------: |
| reverse( ) | 颠倒数组中元素的顺序，无参数 | 改变原来的数组，返回新数组 |
|  sort( )   |     对数组的元素进行排序     | 改变原来的数组，返回新数组 |

​	数组名.sort( function( a , b ){

​		return  a - b ;   //升序，b - a为降序

​	} );

##### 数组索引

|     方法名     |                  说明                  |            返回值            |
| :------------: | :------------------------------------: | :--------------------------: |
|   indexOf( )   | 数组中从前往后查找给定元素的第一个索引 | 存在返回索引号，不存在返回-1 |
| lastIndexOf( ) |  在数组中从后往前查找的最后一个的索引  | 存在返回索引号，不存在返回-1 |

#####  数组转换为字符串

|      方法名      |                说明                |     返回值     |
| :--------------: | :--------------------------------: | :------------: |
|   toString( )    | 把数组转换为字符串，逗号分隔每一项 | 返回一个字符串 |
| join( '分隔符' ) | 把数组中的所有元素转换为一个字符串 | 返回一个字符串 |

#### 基本包装类型

把简单数据类型包装成为复杂数据类型，这样基本数据类型就有了属性和方法

为了方便操作基本数据类型，javascript还提供了三个特殊的引用类型：String，Number和Boolean

##### 字符串的不可变

指的是里面的值不可变，虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间

字符串所有的方法都不会修改字符串本身（字符串是不可变的），操作完成返回一个新的字符串

##### 根据位置返回字符

|       方法名        |            说明             |         使用          |
| :-----------------: | :-------------------------: | :-------------------: |
|   charAt( index )   |     返回指定位置的字符      |   字符串.charAt(  )   |
| charCodeAt( index ) | 获取指定位置处字符的ASCII码 | 字符串.charCodeAt( )  |
|     str[index ]     |     获取指定位置处字符      | 和charAt( index )等效 |

##### 字符串操作方法

|         方法名         |               说明                |
| :--------------------: | :-------------------------------: |
| concat（str1,str2...） |   连接两个或多个字符串，等效于+   |
| substr( start,length ) | 从start位置开始截取到length的个数 |
|   slice( start,end )   |  从start位置开始截取到end的位置   |
| substring( start,end ) |  从start位置开始截取到end的位置   |

##### 字符转换为数组 split（‘分隔符’）



## javascript简单类型与复杂类型

简单类型又叫做基本数据类型或者值类型，复杂类型又叫做引用类型。

##### 简单类型，在存储时变量中存储的是值本身，string , number , boolean , undefined , null。

##### 复杂类型，在存储时变量中存储的仅仅是地址，通过new关键字创建的对象（系统对象，自定义对象），如Object，Array，Date等



#### 堆栈空间分配区别

栈（操作系统）：由操作系统自动分配释放存放函数的参数值，局部变量的值等。其操作方式类似于数据结构等栈；简单数据类型存放到栈里面

堆（操作系统）：存储复杂类型（对象），一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收。

注意：javascript中没有堆栈的概念



## Web APIs的组成

##### 1.页面文档对象模型（DOM）

​	文档对象模型（Document Object Model，简称DOM），是W3C组织推荐的处理可扩展标记语言的标准编程接口。通过DOM提供的接口可以对页面上的各种元素进行操作。

##### 2.浏览器对象模型（BOM）

​	BOM（Browser Object Model，简称BOM）是指浏览器对象模型，它提供了独立于内容的，可以与浏览器窗口进行互动的对象结构。通过BOM可以操作浏览器窗口，比如弹出框，控制浏览器跳转，获取分辨率等。



#### API（Application Programming Interface）

是一些预先定义的函数，目的是提供应用程序与开发人员基于软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节

#### Web API

是浏览器提供的一套操作浏览器功能和页面元素的API（BOM和DOM）



## DOM

文档对象模型（Document Object Model），是W3C组织推荐的处理可扩展标记语言的标准编程接口

##### DOM树

文档：一个页面就是一个文档，DOM中使用document表示

元素：页面中的所有标签都是元素，DOM中使用element表示

节点：网页中的所有内容都是节点（标签，属性，文本，注释等），DOM中使用node表示

**DOM把以上内容都看做是对象**

#### 获取元素

获取过来的DOM元素是一个对象（object）；

##### 根据ID获取：

​	document.getElementById ( )

##### 根据标签名获取：

​	document.getElementsByTagName（ ）返回带有指定标签名的对象的集合

​	注意：因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历。得到的元素对象是动态的

​	还可以获取某个元素（父元素）内部所有指定标签名的子元素

​	element.getElementsByTagName（ '标签名' ）

​	注意：父元素必须是单个对象（必须指明是哪一个元素对象），获取的时候不包括父元素自己

##### 通过HTML5新增的方式获取

​	document.getElementsByClassName( '类名' )    //根据类名返回元素对象集合

​	document.querySelector（‘选择器’）   //根据指定选择器返回第一个元素对象，里面的选择器要加符号

​	document.querySelectorAll( '选择器' )    //根据指定选择器返回所有元素对象集合

##### 特殊元素获取

​	获取body元素

​		document.body

​	获取html元素

​		document.documentElement

#### 事件基础

javascript使我们有能力创建动态页面，而事件是可以被javascript侦测到的行为

事件是由三部分组成，事件源，事件类型，事件处理程序

##### 执行事件步骤

​	1.获取事件源

​	2.绑定事件，注册事件

​	3.添加事件处理程序

##### 常见的鼠标事件

|  鼠标事件   |     触发条件     |
| :---------: | :--------------: |
|   onclick   | 鼠标点击左键触发 |
| onmouseover |   鼠标经过触发   |
| onmouseout  |   鼠标离开触发   |
|   onfocus   | 获得鼠标焦点触发 |
|   onblur    | 失去鼠标焦点触发 |
| onmousemove |   鼠标移动触发   |
|  onmouseup  |   鼠标弹起触发   |
| onmousedown |   鼠标按下触发   |

#### 操作元素

javascript的DOM操作可以改变网页内容，结构和样式，我们可以利用DOM操作元素里面的内容，属性等

##### 改变元素内容

​	element.innerText    从起始位置到终止位置到内容，但它不识别html标签，同时空格和换行也会去掉

​	element.inner HTML    起始位置到终止位置的全部内容，识别html标签，同时保留空格和换行

##### 修改元素属性

元素对象.src  ( src , href , id , alt , title )

##### 表单元素的属性操作

type，value，checked，selected，disabled

##### 样式属性操作

元素对象.style.属性名    行内样式操作

​	注意：JS里面的样式采取驼峰命名法。JS修改style样式操作，产生的是行内样式，权重比较高

元素对象.className    类名样式操作

​	注意：会直接更改元素的类名，覆盖原先的类名

##### 排他思想 

如果有同一组元素，我们想要某一个元素实现某种样式，需要用到循环的排他思想算法：

1.所有元素全部清除样式

2.给当前元素设置样式

##### 获取属性

element.属性      //获取内置属性值（元素本身自带的属性）

element.getAttribute( ' 属性' )         //属性：attribute 。 主要获得自定义的属性（标准）程序员自定义的属性

##### 设置属性值

element.属性 = ‘ 值 ’ ；

element.setAttribute( ' 属性' ，‘ 值 ’)；

##### 移除属性

element.removeAttribute( ' 属性' )；

#### HTML5自定义属性

自定义属性的目的：是为了保存并使用数据。有些数据可以保存到页面中而不用保存到数据库中。

但是有些自定义属性很容易引起歧义，不容易判断是元素的内置属性还是自定义属性。

##### H5规定自定义属性以data- 开头作为属性名并且赋值

##### H5新增element.dataset.属性 或者 element.dataset[ ' 属性 ' ]

##### dataset是一个集合里面存放了所有以data开头的自定义属性，如果自定义属性里面有多个-的单词，我们获取的时候采取驼峰命名法。

data- list- name = ‘ Andy ’ ；             dataset.listName

#### 节点操作

获取元素通常使用两种方式：

1.利用DOM提供的方法获取元素

​	document.querySelectorAll（ ）

​	document.getElementById ( )

​	document.getElementsByTagName（ ）等

​	逻辑性不强，繁琐

2.利用节点层级关系获取元素

​	利用父子兄节点关系获取元素

​	逻辑性强，但是兼容性稍差

##### 节点概述

网页中的所有内容都是节点（标签，属性，文本，注释等），在DOM中，节点使用node来表示。

HTML  DOM树中的所有节点均可通过javascript进行访问，所以HTML元素（节点）均可被修改，也可以创建或删除。

一般地，节点至少拥有nodeType（节点类型），nodeName（节点名称）和node Value（节点值）这三个基本属性。

​	元素节点nodeType为 1

​	属性节点nodeType为 2

​	文本节点nodeType为 3（文本节点包含文字，空格，换行等）

在实际开发中，节点操作主要操作的是元素节点

#### 节点层级 

利用DOM树可以把节点划分为不同的层级关系，常见的是父子兄层级关系

##### 1.父级节点

​	node.parentNode   //得到的是离元素最近的父级节点

##### 2.子节点

​	parentNode.childNodes ( 标准 )   //返回包含指定节点的子节点（包含元素节点，文本节点等）的集合，该集合为即时更新的集合。如果只想要获取里面的元素节点，则需要专门处理。

​	parentNode.children ( 非标准 )	  //是一个只读属性，返回所有的子元素节点。它只返回子元素节点，其余节点不返回。

​	parentNode.firstChild    //返回第一个子节点，包含所有的节点

​	parentNode.lastChild    //返回最后一个子节点，包含所有的节点 

​	parentNode.firstElementChild    //返回第一个子节点,只返回子元素节点，其余节点不返回。

​	parentNode.lastElementChild    //返回最后一个子节点,只返回子元素节点，其余节点不返回。

##### 3.兄弟节点

​	node.nextSibling    //返回返回当前元素的下一个兄弟节点，包含所有的节点

​	node.previousSibling    //返回返回当前元素的上一个兄弟节点，包含所有的节点

​	node.nextElementSibling    //返回返回当前元素的下一个兄弟元素节点

​	node.previousElementSibling    //返回返回当前元素的上一个兄弟元素节点

#### 创建节点

document.createElement ( ' tagName ' )    //创建指定的HTML元素。因为这些元素原先不存在，是根据我们的需求动态生成的，所以也称为动态创建元素节点。

#### 添加节点

node.appendChild ( ' child ' ) 	  //将一个节点添加到指定父节点的子节点列表末尾，类似CSS里面的after伪元素。

node.insertBefore ( child , 指定元素 )     //将一个节点添加到父节点的指定子节点前面，类似CSS里面的before伪元素

#### 删除节点

node.removeChild ( child )     //从DOM中删除一个子节点，返回删除节点，没有子节点会报错。

#### 复制节点（克隆节点）

node.cloneNode( )     //返回调用该方法的节点的一个副本

如果括号参数为空或者false，则是浅拷贝，即只克隆复制节点本身，不克隆里面的子节点。括号参数为true，则是深拷贝，克隆复制节点本身以及里面所有的子节点

#### 三种动态创建元素区别

.document.write ( )

​	是直接将内容写入页面的内容流，但是文档流执行完毕，则会导致页面全部重绘

.element.innerHTML

​	将内容写入某个DOM节点，不会导致页面全部重绘

​	创建多个元素效率较高（不要拼接字符串，采取数组形式拼接），结构稍微复杂

.document.createElement ( )

​	创建多个元素效率稍低一点点，但是结构更清晰

不同浏览器下，innerHTML效率要比createElement高



## 事件高级

#### 1.注册事件（绑定事件）

##### 1.1注册事件概述

注册事件有两种方式：传统方式和方法监听注册方式

##### 	传统注册方式        特点：注册事件的唯一性，同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面注册的处理函数

##### 	方法监听注册方式addEventListener ( )       特点：同一个元素同一个事件可以注册多个监听器，按注册顺序依次执行

##### 1.2 addEventListener事件监听方式

eventTarget.addEventListener ( type ,  listener [ , useCapture ] )

eventTarget.addEventListener ( )方法将指定的监听器注册到eventTarget（目标对象）上，当该对象触发指定的事件时，就会执行事件处理函数。

该方法接受三个参数：

​	type：事件类型字符串，比如click，mouseover，注意这里不要带on

​	listener：事件处理函数，事件发生时，会调用该监听函数

​	useCapture ：可选参数，是一个布尔值，默认是false



#### 2.删除事件（解绑事件）

##### 2.1删除事件的方式

​	传统注册方式  eventTarget.onclick = null;

​	方法监听注册方式  eventTarget.removeEventListener( type , listener [ , useCapture ] );

![image-20230221103734972](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230221103734972.png)



#### 3.DOM事件流

事件流描述的是从页面中接受事件的顺序

事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流

DOM事件流分为3个阶段：

​	1.捕获阶段

​	2.当前目标阶段

​	3.冒泡阶段

**注意**

  1.JS代码中只能执行捕获或者冒泡其中的一个阶段

2. onclick和addEvent只能的得到冒泡阶段

3. addEventListener ( type ,  listener [ , useCapture ] )第三个参数如果是true，表示在事件捕获阶段调用事件处理程序；如果是false（默认为false），表示在事件冒泡阶段调用事件处理程序。

  4.有些事件是没有冒泡的，比如onblur , onfocus , onmouseenter , onmouseleave



#### 4.事件对象

![image-20230221110832230](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230221110832230.png)

事件对象的常见属性和方法

|   事件对象属性方法    |        说明         |
| :-------------------: | :-----------------: |
|       e.target        | 返回触发事件的对象√ |
|     e.srcElemrnt      | 返回触发事件的对象  |
|        e.type         |   返回事件的类型    |
|    e.cancelBubble     |   该属性阻止冒泡    |
|     e.returnValue     |    阻止默认事件     |
| e.preventDefault ( )  |    阻止默认事件√    |
| e.stopPropagation ( ) |      阻止冒泡√      |

![image-20230221112011184](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230221112011184.png)

跟this非常相似的属性currentTarget

![image-20230221112938346](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230221112938346.png)



#### 5.阻止事件冒泡

##### 5.1阻止事件冒泡的两种方式

事件冒泡：开始时由最具体的元素接收，然后逐级向上传播到DOM最顶层节点

标准写法：利用事件对象里面的stopPropagation ( )方法



#### 6.事件委托（代理，委派）

每个子节点不在单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点



#### 7.常用的鼠标事件

![image-20230221114628960](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230221114628960.png)

![image-20230221114956019](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230221114956019.png)

##### mouseenter鼠标经过触发事件

当鼠标移动到元素上时就会触发，mouseover鼠标经过自身盒子会触发，经过子盒子还会触发。而mouseenter只会经过自身盒子触发，因为mouseenter不会冒泡，

##### mouseleave鼠标离开触发事件同样不会冒泡



##### 鼠标事件对象

event对象代表事件的状态，跟事件相关的一系列信息的集合。现阶段我们主要是用鼠标事件对象MouseEvent和键盘事件对象KeyboardEvent

![image-20230221115551287](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230221115551287.png)

#### 8.常用的键盘事件

![image-20230224095918651](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230224095918651.png)

注意：

​	使用addEventListener不需要加on

​	keydown的执行顺序比keypress执行顺序高

##### 键盘事件对象  .key

键盘事件对象中的key属性可以得到相应键的的ASCII值

​	1.keyup和keydown事件不区分字母大小写

​	2.keypress事件区分大小写

注意：

​	keydown和keypress在文本框里面的特点：事件触发的时候，文字还没有落入文本框



## BOM浏览器对象模型

BOM（Browser Object Model，简称BOM）是指浏览器对象模型，它提供了独立于内容的，可以与浏览器窗口进行互动的对象结构。通过BOM可以操作浏览器窗口，比如弹出框，控制浏览器跳转，获取分辨率等。

##### BOM的构成

window对象是浏览器顶级对象，它具有双重角色

1.它是JS访问浏览器窗口的一个接口

2.它是一个全局对象。定义在全局作用域中的变量，函数都会变成window对象的属性和方法。

#### 1.window对象的常见事件

##### 1.1窗口加载事件

##### 	window.onload = function( ) { };或者 window.addEventListener( "load" , function( ) { } );

​	当文档内容完全加载完成会触发该事件（包括图像，脚本文件，CSS文件等），就调用的处理函数

​	注意：使用传统注册事件只能写一次，如果有多个，会以最后一个为准。使用addEventListener则没有限制

##### 	document.addEventListener( "DOMContentLoaded" , function( ) { } ) 

​	DOMContentLoaded事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等等。

![image-20230226224249380](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226224249380.png)

##### 1.2调整窗口大小事件

window.onresize = function ( ) { };或者 window.addEventListener( "resize" , function ( ) { } );

window.innerWidth当前屏幕的宽度

#### 2.定时器

##### 2.1定时器window.setTimeout ( 调用方法 ，[延迟的毫秒数] );

​	用于设置一个定时器，该定时器在定时器到期后执行函数。

![image-20230224152634584](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230224152634584.png)

​	setTimeout ( )函数也称为回调函数callback

##### 停止setTimeout ( )定时器window.clearTimeout (timeout  ID)

##### 2.2window.setInterval (回调函数，[间隔的毫秒数] )；

​	重复调用一个函数，每隔这个时间，就去调用一次回调函数

![image-20230224162615411](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230224162615411.png)

停止setInterval ( )定时器window.clearInterval ( interval  ID )

![image-20230224164551450](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230224164551450.png)

![image-20230224180429775](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230224180429775.png)

##### 2.3this

this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，一般情况下this的最终指向的是那个调用它的对象。

1.全局作用域或者普通函数中this指向全局对象window（注意定时器里面的this指向window）

2.方法调用中谁调用this指向谁

3.构造函数中this指向构造函数的实例

#### 3.JS执行机制

javascript语言的一大特点就是单线程，也就是说，同一时间只能做一件事。单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。这样所导致的问题：如果JS执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

##### 3.1同步和异步

为了解决这个问题，利用多核CPU的计算能力，HTML5提出Web Worker标准，允许javascript脚本创建多个线程。于是，JS中出现了同步和异步。

##### 同步：前一个任务结束之后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的

##### 异步：执行长时间任务时，可以去处理其他事情。

##### 同步任务：都在主线程上执行，形成一个执行栈

##### 异步任务：JS的异步是通过回调函数实现的，一般而言，异步任务有以下三种类型

​	1.普通事件：如click，resize等

​	2.资源加载：如load，error等

​	3.定时器：包括setInterval，setTimeout等

##### 异步任务相关回调函数添加到任务队列中

##### 3.2执行机制

1.先执行执行栈中的同步任务

2.异步任务（回调函数）放入任务队列中

3，一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行

##### 由于主线程不断的重复获得任务、执行任务、再获取任务、再执行、这种机制被称为事件循环（ event loop ）

#### 4.location对象

window对象给我们提供了一个location属性用于获取或设置窗体的URL，并且可以用于解析URL，因为这个属性返回的是一个对象，所以我们将这个属性也称为location对象

![image-20230226091621966](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226091621966.png)

##### location对象的属性

![image-20230226091900547](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226091900547.png)

5秒钟之后跳转页面

![image-20230226094712469](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226094712469.png)

![image-20230226144136728](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226144136728.png)

location对象的方法

![image-20230226144410911](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226144410911.png)

#### 5.navigator对象

navigator对象包含有关浏览器的信息，它有很多属性，我们最常用的是userAgent，该属性可以返回由客户机发送服务器的user-agent头部的值

#### 6.history对象

window对象给我们提供了一个history对象，与浏览器历史记录进行交互。该对象包含用户（在浏览器窗口中）访问过的URL

![image-20230226150245396](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226150245396.png)

![image-20230226150509843](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226150509843.png)





# PC端网页特效

#### 1.元素偏移量offset系列

获得与元素距离带有定位父元素的位置

获得元素自身的大小（宽度高度）

注意：返回的数值都不带单位

![image-20230226151611659](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226151611659.png)

offset与style区别

![image-20230226160649435](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226160649435.png)

#### 2.元素可视区client系列

![image-20230226222112353](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226222112353.png)

立即执行函数 （ function (  ) {   } ）(  ) 或者（ function (  ) {  } (  ) ）

主要作用：创建一个独立的作用域

document.documentElement  //获取html的根元素

window.devicePixelRatio   //物理像素比

![image-20230226223841150](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226223841150.png)

![image-20230226224030425](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226224030425.png)

![image-20230226224446009](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226224446009.png)

![image-20230226224559753](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226224559753.png)

![image-20230226224649517](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226224649517.png)



#### 3.元素滚动scroll系列

![image-20230226224745143](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230226224745143.png)

##### 页面被卷去的头部：window.pageYOffset  

##### 滚动条在滚动时会触发onscroll事件

![image-20230227100028880](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230227100028880.png)

![image-20230227100233599](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230227100233599.png)



#### 4.动画函数封装

核心原理：通过定时器setInterval ( )不断移动盒子位置。

![image-20230227101658060](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230227101658060.png)

##### 简单的函数封装

![image-20230227114619198](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230227114619198.png)

##### 缓动效果原理

​	让盒子每次移动的距离慢慢变小，速度就会慢慢落下来。核心算法：（目标值 - 现在的位置）/ 10  做为每次移动的距离步长

​	注意:步长值需要取整

![image-20230227115851363](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230227115851363.png)

![image-20230227120718573](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230227120718573.png)

##### 动画函数添加回调函数

​	回调函数原理：函数可以作为一个参数。将这个函数作为参数传到另一个函数里面，当那个函数执行之后，再执行传进去的函数，这个过程就叫做回调。

##### 动画函数封装到单独JS文件里面

![image-20230227160858804](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230227160858804.png)

#### 5.常见网页特效案例

##### 节流阀

防止轮播图按钮连续点击造成播放过快。当上一个函数动画内容执行完毕，再去执行下一个函数动画，让事件无法连续继续。

核心实现思路：利用回调函数，添加一个变量来控制，锁住函数和解锁函数。

![image-20230228193203018](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228193203018.png)



## 移动端网页特效

#### 1.触屏事件

移动端浏览器兼容性较好，我们不需要考虑以前JS的兼容性问题，可以放心的使用原生JS书写效果，但是移动端也有自己独特的地方，比如触屏事件touch。

![image-20230228194152947](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228194152947.png)

##### 触摸事件对象（TouchEvent）

TouchEvent是一类描述手指在触摸平面的状态变化的事件。这类事件用于描述一个或多个触点，使开发者可以检测触点的移动，触点的增加和减少。

touchstart，touchmove，touchend三个事件都会各自有事件对象。

![image-20230228195355155](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228195355155.png)

![image-20230228195857014](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228195857014.png)

##### 移动端拖动元素

touchstart，touchmove，touchend可以实现拖动元素。

但是拖动元素需要当前手指的坐标值，我们可以使用targetTouches[0]里面的page X和page Y。

移动端拖动的原理：手指移动中，计算出手指移动的距离。然后用盒子原来的位置 + 手指移动的距离。

手指移动的距离：手指滑动中的位置减去手指刚开始触摸的位置。

注意：手指移动也会触发滚动屏幕所以这里要阻止默认的屏幕滚动e.preventDefault( );

![image-20230228201216670](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228201216670.png)

![image-20230228201509231](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228201509231.png)

![image-20230228201527313](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228201527313.png)

#### 2.移动端常见特效

![image-20230228205031999](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228205031999.png)

![image-20230228205212652](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228205212652.png)

#### classList属性

classList属性是HTML5新增的一个属性，返回元素类名

该元素用于在元素中添加、移除以及切换CSS类

##### 添加类：  在后面追加类名，不会覆盖之前的类名。注意前面不需要加.

##### element.classList.add（‘ 类名 ’）

##### 移除类：

##### element.classList.remove（‘ 类名 ’）

##### 切换类：存在就去掉类，没有就添加类

##### element.classList.toggle（‘ 类名 ’）

![image-20230228211123430](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228211123430.png)

![image-20230228232433970](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230228232433970.png)

![image-20230301103813106](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301103813106.png)

![image-20230301104113676](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301104113676.png)

![image-20230301110958906](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301110958906.png)

##### click延时解决方案

移动端click事件会有300ms的延时，原因是移动端屏幕双击会缩放（double tap to zoom）页面

解决方案：

1.禁用缩放。浏览器禁用默认的双击缩放行为并且去掉300ms的点击延迟。

##### 	< meta  name = " viewport "  content = " user-scalable = no " >

2.利用touch事件自己封装这个事件解决300ms延迟

​	原理：当我们手指触摸屏幕，记录当前触摸时间

​				当我们手指离开屏幕，用离开的时间减去触摸的时间

​				如果时间小于150ms，并且没有滑动过屏幕，那么我们就定义为点击

![image-20230301112720311](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301112720311.png)

3.使用插件。fastclick插件解决300ms延迟

#### 3.移动端常用开发插件

#### 4.移动端常用开发框架



## 本地存储

##### 本地存储特性

1.数据存储在用户浏览器

2.设置，读取方便，甚至页面刷新不丢失数据

3.容量较大，sessionStorage约5M，localStorage约20M

4.只能存储字符串，可以将对象JSON.stringify ( )编码后存储

#### window.sessionStorage

1.生命周期为关闭浏览器窗口

2.在同一个窗口（页面）下数据可以共享

3.以键值对的形式存储使用

##### 存储数据：sessionStorage.setltem ( key , value )

##### 获取数据：sessionStorage.getItem ( key )

##### 删除数据：sessionStorage.removeItem ( key )

##### 删除所有的数据：sessionStorage.clear ( )



#### window.localStorage

1.生命周期永久生效，除非手动删除否则关闭页面也会存在

2.可以多窗口（页面）共享（同一浏览器可以共享）

3.以键值对的形式存储使用

##### 存储数据：localStorage.setltem ( key , value )

##### 获取数据：localStorage.getItem ( key )

##### 删除数据：localStorage.removeItem ( key )

##### 删除所有的数据：localStorage.clear ( )

![image-20230301150713691](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230301150713691.png)



# Promise

promise是一个构造函数，通过new关键字实例化对象

### new Promise( ( resolve , reject ) => {  } )

promise接收一个函数作为参数，在参数函数中接收两个参数resolve , reject



### promise实例

promise实例有两个属性

​	state：状态

​	result：结果

##### promise的状态

​	1.pending（准备，待解决，进行中）

​	2.fulfilled（已完成，成功）

​	3.rejected（已拒绝，失败）

##### promise状态的改变

​	通过调用resolve( )和reject( )改变当前promise对象的状态

```js
const p = new Promise((resolve , reject) => {
	//resolve()调用函数时，使当前promise对象的状态改为fulfilled
  //reject()调用函数时，使当前promise对象的状态改为rejected
  resolve()
})
```

promise状态的改变是一次性的



##### promise的结果

```js
const p = new Promise((resolve , reject) => {
	//通过调用resolve()，传递参数，改变当前promise对象的结果
  resolve("成功的结果")
})
```



### Promise的方法

##### 1.then

在then的参数函数中，通过形参使用promise对象的结果

```js
const p = new Promise((resolve , reject) => {
  resolve("成功的结果")
})

p.then(
  //当promise的状态是fulfilled时执行
  (value) => {
  	console.log("成功时调用" ,value) //resolve()传递的参数
	} , 
  //当promise的状态是rejected时执行
  () => {
  	console.log("失败时调用")
	}
)
```

##### 2.then函数返回一个新的promise实例，状态是pending

```js
const t = p.then(
  (value) => {
  	console.log("成功时调用" ,value) //resolve()传递的参数
	} , 
  () => {
  	console.log("失败时调用")
	}
).then()
```

##### promise的状态不改变，不会执行then里的方法

##### 在then方法中，通过return将返回的promise实例改为fulfilled状态

##### 3.catch

当promise的状态改为rejected时 和 当promise的执行体中出现代码错误时catch函数被执行

```js
new promise((resolve) , reject) => {
  
}).then(() => {
  //成功时调用
}).catch(() => {
  //失败时调用
})
```



```js
new Promise((resolve , reject) => {
  $.ajax({
    type:"GET",
    url:"xxxxxx",
    success(response){
      resolve(response)
    },
    error(response){
      reject(response)
    }
  })
}).then((response) => {
  
})
```

```js
const getJSON = function(url){
  return new Promise((resolve , reject) => {
    const xhr = new XMLHttpRequest()
    xhr.open("GET" , url)
    xhr.onreadystatechange = handler
    xhr.responseType = "json"
    xhr.setRequestHeader("Accept" , "application/json")
    xhr.send()
    
    function handler(){
      if(this.readyState === 4 && this.status === 200){
          resolve(this.response)
      }else{
          reject(new Error(this.statusText))
      }
    }
  })
}

getJSON("http://xxxxxxxxx").then(
	(data) => {
    console.log(data)
  } ,
  (error) => {
    console.log(error)
  }
)
```

```js
let p = Promise.resolve("foo")  等价于  let p = new Promise(resolve => resolve("foo"))
p.then((data) => {
  console.log(data)  //foo
})
```

```js
let p1 = new Promise((resolve , reject) => {})
let p2 = new Promise((resolve , reject) => {})
let p3 = new Promise((resolve , reject) => {})
let p4 = Promise.all([p1 , p2 , p3])
p4.then(() => {
  //三个都成功 才运行成功的回调
}).catch(error => {
  //如果有一个失败 运行失败的回调
})

```

```js
function requestImg(imgSrc){
  return new Promise((resolve , reject) => {
    const img = new Image()
    img.onload = function(){
      resolve(img)
    }
    img.src = imgSrc
  })
}

function timeout(){
  return new Promise((resolve , reject) => {
    setTimeout(() => {
      reject(new Error("图片请求超时"))
    } , 3000)
  })
}

Promise.race([requestImg("images/1.jpg") , timeout()])
  .then(data => {
  document.body.appendChild(data)
}).catch(err => {
  console.log(err)
})
```

done( )和finally( )方法在成功或者失败之后都会执行







## 迭代器iterator

##### 1.迭代器是一个接口，能快捷的访问数据，通过Symbol.iterator来创建迭代器，通过迭代器的next( )获取迭代之后的结果

##### 2.迭代器是用于遍历数据结构的指针（数据库的游标）

```js
const items = ['one' , 'two' , 'three']
const ite = items[Symbol.iterator]()
console.log(ite.next())  //{value:"one",done:"false"} done表示是否遍历完成，false表示遍历继续，true表示遍历完成
console.log(ite.next())  //{value:"two",done:"false"}
console.log(ite.next())	 //{value:"three",done:"false"}
console.log(ite.next())	 //{value:"undefined",done:"true"}

```

##### 

## 生成器generator

##### generator函数，可以通过yield关键字，将函数挂起，为了改变执行流提供了可能，同时为了做异步编程提供了方案

```js
function* func(){
  console.log("one")
	yield 2;
  console.log("two")
  yield 3
  console.log("three")
}
//返回一个遍历器对象,可以调用next()
let fn = func();
console.log(fn.next());  //one {value:2, done:false}
console.log(fn.next());  //two {value:3, done:false}
console.log(fn.next());  //three {value:undefined, done:true}
```

##### generator函数是分段执行的，yield语句是暂停执行，而next( )恢复执行

```js
function* add(){
  console.log("one")
	let x = yield '2'
  console.log("two:" + x)
  let y = yield '3'
  console.log("three:" + y)
  return x + y
}
//返回一个遍历器对象,可以调用next()
const fn = func();
console.log(fn.next());  //one {value:2, done:false}
console.log(fn.next());  //two:undefined {value:3, done:false}
console.log(fn.next());  //three:undefined {value:undefined, done:true}
```

```js
function* add(){
  console.log("one")
  //通过next()给x传值
	let x = yield '2'
  console.log("two:" + x)
  let y = yield '3'
  console.log("three:" + y)
  return x + y
}
//返回一个遍历器对象,可以调用next()
const fn = func();
console.log(fn.next());  //one {value:2, done:false}
console.log(fn.next(10));  //two:10 {value:3, done:false}
console.log(fn.next(20));  //three:20 {value:30, done:true}
```

##### 使用场景：为不具备iterator接口的对象提供了遍历操作

```js
function* objectEntries(obj){
  //获取对象的所有的key保存到数组
  const propKeys = Object.keys(obj)
  for(const propKey of propKeys){
    yield [propkey , obj[propkey]]
  }
}

const obj = {
  name:"mzk",
  age:24,
  sex:"男"
}

//给对象提供iterator接口，并传递函数
obj[Symbol.iterator] = objectEntrise
console.log(obj)

for(let [key,value] of obj[Symbol.iterator](obj)){
  console.log(`${key}:${value}`)
  /*
  name:"mzk",
  age:24,
  sex:"男"
  */
}
```

```js
function loadUI(){
  console.log("初始化页面")
}
function showData(){
  //模拟异步操作
  setTimeout(() => {
    console.log("加载loading....")
    itLoad.next()
  })
}
function hideUI(){
  console.log("数据加载完成")
}

function* load(){
  loadUI()
  yield showData()
  hideUI()
}

let itLoad = load()
itLoad.next()
```



## async异步操作

```js
async function func(){
  let s = await "hello async"
  let data = await s.split('')
  return data  //会自动转换成Promise对象
}
func.then(value => console.log(value)).catch(error => console.log(error))
//如果async函数中有多个await，那么then函数会等待所有的await指令运行完，才去执行
```



```js
async function getNow(url){
  let res = await getJSON(url)
  let arr = await res.data
  return arr[0].now
}

getNow("http://xxxxxxxxx").then(now => console.log(now))
  .catch(error => console.log(error))

const getJSON = function(url){
  return new Promise((resolve , reject) => {
    const xhr = new XMLHttpRequest()
    xhr.open("GET" , url)
    xhr.onreadystatechange = handler
    xhr.responseType = "json"
    xhr.setRequestHeader("Accept" , "application/json")
    xhr.send()
    
    function handler(){
      if(this.readyState === 4 && this.status === 200){
          resolve(this.response)
      }else{
          reject(new Error(this.statusText))
      }
    }
  })
}
```





# Git

##### git  init 初始化仓库

##### git的三个区域（工作区 ，暂存区 ， 仓库区）

（1）工作区：工作目录，书写代码的地方

（2）暂存区，暂存提交代码的地方

（3）仓库区：代码永久存储区

##### 配置全局的用户名和邮箱

```js
git config --global user.name
git config --global user.email
```

##### 查看配置列表

```js
git config --list
```

##### 将工作区代码提交到暂存区（所有文件）

```js
git add .
git add -A
git add -all
```

##### 将暂存区代码提交到仓库区

```js
git commit -m '提交说明'
```

##### 查看文件状态

```js
git status
git status -s //简化
```

##### 查看仓库提交日志

```js
git log
git log --oneline //简化
git reflog 
```

##### 版本回退

```js
git reset --hard版本号

```

##### 创建分支

```js
git branch 分支名  //创建分支
git branch  //查看分支
git checkout 分支名  //切换分支
git merge 分支名  //合并代码
git branch -d 分支名  //删除分支
git checkout -b 分支名 //创建并切换分支
```



![image-20230525011339687](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230525011339687.png)

![image-20230525011207928](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230525011207928.png)





















































































