# **Vue2**

##### 一套用于构建用户界面的渐进式javaScript框架

### 初识Vue

1.想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象

2.容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法

3.容器里的代码被称为「Vue模版」

4.Vue实例和容器是一一对应的

5.真是开发中只有一个Vue实例，并且会配合着组件一起使用

6.{{ xxx }}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性

7.一旦data中的数据发生改变，那么页面中用到该数据的地方会自动更新



### Vue模版语法

#### 插值语法

​	功能：用于解析标签体内容

​	语法：{{ data }}

#### 指令语法

​	单向数据绑定：v-bind 

​		数据只能从data流向页面

​	双向数据绑定：v-model

​		数据不仅能从data流向页面，还可以从页面流向data

​		只能应用在表单类元素上 value，因此v-model:value 可以简写为：v-model

​	功能：用于解析标签（包括：标签属性，标签体内容，绑定事件。。。）

​	语法：绑定标签属性   v-bind:标签属性 = " data "    简写 :标签属性 = " data "



### MVVM模型

M：模型（model），对应data中的数据

V：视图（View），模版DOM

VM：视图模型（View Model）：Vue实例对象

data中所有的属性，最后都出现在了VM身上。VM身上所有的属性及Vue原型上所有属性，在Vue模块中都可以直接使用



### 数据代理

Object.defineproperty方法所添加的数据不能被遍历

​	enumerable:true 控制属性是否可以遍历，默认值false

​	writable:true 控制属性是否可以被修改，默认值false

​	configurable:true 控制属性是否可以被删除，默认值false

​	get:function( ) { }当有人读取person的sex属性时，get函数（getter）就会被调用，返回值为sex的值

​	set:function( ) { }当有人修改person的sex属性时，set函数（setter）就会被调用，会收到修改值

##### 通过一个对象代理对另一个对象中属性的操作（读/写）

![image-20230323145428478](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230323145428478.png)

##### Vue中的数据代理：

​	通过vm对象来代理data对象中属性的操作（读/写）

Vue中数据代理的好处：

​	更加方便的操作data中的数据

基本原理

​	通过Object.defineproperty( )把data对象中所有属性添加到vm上

​	为每一个添加到vm上的属性，都指定一个getter/seter

​	在getter/setter内部去操作（读/写）data中对应的属性



### 事件处理

##### 事件的基本使用

​	使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名

​	事件的回调需要配置在methods对象中，最终会在vm上

​	methods中配置的函数，不要用箭头函数，否则this就不是vm了

​	methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象

​	@click = "demo" 和 @click = "demo ( $event )" 效果一样，但后者可以传参

##### 事件修饰符

​	prevent：阻止默认事件

​	stop：阻止事件冒泡

​	once：事件只触发一次

​	capture：使用事件的捕获模式

​	self：只有event.target是当前操作的元素时才触发事件

​	passive：事件的默认行为立即执行，无需等待事件回调执行完毕

​	修饰符可以连续写

##### 键盘事件

1.常用的按键别名：

​	回车	=>	enter

​	删除	=>	delete ( 捕获删除和退格键 )

​	退出	=>	esc

​	空格	=>	space

​	换行	=>	tab（特殊，必须配合keydown使用 ）

​	切换大小写	=>	caps-lock 

​	上	=>	up

​	下	=>	down

​	左	=>	left

​	右	=>	right

2.Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名）

3.系统修饰键（用法特殊）：ctrl , alt , shift  , meta

​	(1)配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发

​	(2)配合keydown使用：正常触发事件

4.也可以使用keyCode去指定具体的按键（不推荐）

5.Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名



### 计算属性computed

##### 定义：

​	通过已有属性计算得来一个新属性

##### 原理：

​	底层借助了Object.defineproperty方法提供的getter和setter

get函数什么时候执行

​	（1）初次读取时会执行一次

​	（2）当依赖的数据发生改变时会被再次调用

##### 优势：

​	与methods实现相比，内部有缓存机制（复用），效率更高，调试方便

##### 备注：

​	（1）计算属性最终会出现在vm上，直接读取使用即可

​	（2）如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变

##### 计算属性不能开启异步任务去维护属性



### 监视属性watch

当被监视的属性变化时，回调函数自动调用，进行相关操作

监视的属性必须存在，才能进行监视

监视的两种写法：

​	（1）new Vue时传入watch配置

​	（2）通过vm.$watch监视

#### 深度监视

​	（1）Vue中的watch默认不监测对象内部值的改变（一层）

​	（2）配置deep:true可以监测对象内部值改变（多层）

备注：

​	（1）Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以

​	（2）使用watch时根据数据的具体结构，决定是否采用深度监视



### computed和watch之间的区别

​	（1）computed能完成的功能，watch都可以完成

​	（2）watch能完成的功能，computed不一定能完成。例如：watch可以进行异步操作

##### 两个重要的小原则

​	（1）所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象

​	（2）所有不被Vue所管理的函数（定时器的回调函数，ajax的回调函数，Promise的回调函数等），最好写成箭头函数，这样this的指向才是vm 或 组件实例对象



### 绑定样式

##### 1.class样式

​	写法	：class="xxx" xxx可以是字符串、对象、数组

##### 2.style样式

​	写法	：style="{ fontSize:xxx }" 其中xxx是动态值

​				：style="[ a,b ]" 其中a,b是样式对象



### 条件渲染

##### 1.v-if

​	写法：

​		（1）v-if=“表达式”

​		（2）v-else-if=”表达式“

​		（3）v-else=”表达式“

​	适用于：切换频率较低的场景

​	特点：不展示的DOM元素直接被移除

​	注意：v-if可以和 :v-else-if , v-else 一起使用，但要求结构不能被打断

##### 2.v-show

​	写法：v-show=“表达式”

​	适用于：切换频率较高的场景

​	特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉

##### 3.备注：使用v-if时，元素可能无法获取到，而使用v-show一定可以获取到



### 列表渲染

##### v-for指令

​	1.用于展示列表数据

​	2.语法：v-for="(item , index)  in  xxx"  :key="yyy" 

​	3.可遍历：数组，对象，字符串，指定次数

##### key的作用与原理

![image-20230327121440493](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230327121440493.png) 

![image-20230327121820796](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230327121820796.png)

##### 1.虚拟DOM中key的作用

​	key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据新数据生成新的虚拟DOM，随后Vue进行新虚拟DOM与旧虚拟DOM的差异比较

##### 2.对比规则

​	（1）旧虚拟DOM中找到了与新虚拟DOM相同的key：

​				 若虚拟DOM中内容没变，直接使用之前的真实DOM

​				 若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM

​	（2）旧虚拟DOM中未找到与新虚拟DOM相同的key

​				 创建新的真实DOM，随后渲染到页面

##### 3.用index作为key可能会引发的问题

​	（1）若对数据进行：逆序添加，逆序删除等破坏顺序操作

​				 会产生没有必要的真实DOM更新  ===> 界面效果没问题，但效率低

​	（2）如果结构中还包含输入类的DOM

​				 会产生错误DOM更新 ===> 界面有问题

##### 4.开发中如何选择key

​	（1）最好使用每条数据的唯一标识作为key，比如id，手机号，身份证号，学号等唯一值

​	（2）如果不存在对数据的逆序添加，逆序删除等破坏顺序操作，仅用于渲染列表用于展示，如果index作为key是没有问题的



### 监测数据改变的原理

##### 1.vue会监视data中所有层次的数据

##### 2.如何监测对象中的数据

​	通过setter实现监视，且要在new Vue时就传入要监测的数据

​		（1）对象中后追加的属性，Vue默认不做响应式处理

​		（2）如需给后添加的属性做响应式，请使用如下API：

​					Vue.set( target , propertyName/index , value )

​					vm.$set( target , propertyName/index , value )

##### 3.如何监测数组中的数据

​	通过包裹数组更新元素的方法实现，本质就是做了两件事

​		（1）调用原生对应的方法对数组进行更新

​		（2）重新解析模版，进而更新页面

##### 4.在Vue修改数组中的某个元素一定要用如下方法

​	（1）使用这些API：push( ) , pop( ) , shift( ) , unshift( ) , splice( ) , sort( ) , reverse( )

​	（2）Vue.set( ) 或 vm.$set( )

##### 特别注意：Vue.set( ) 和 vm.$set( ) 不能给vm或vm的根数据对象添加属性



### 收集表单数据

##### 若：< input  type=" text " / >，则v-model收集的是value值，用户输入的就是value值

##### 若：< input  type=" radio " / >，则v-model收集的是value值，且要给标签配置value值

##### 若：< input  type=" checkbox " / >，

​	1.没有配置input的value属性，那么收集的就是checked（勾选  or   未勾选，是布尔值）

​	2.配置input的value属性

​		（1）v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）

​		（2）v-model的初始值是数组，那么收集的就是value组成的数组

##### 备注：v-model的三个修饰符

​	lazy：失去焦点再收集数据

​	number：输入字符串转为有效的数字

​	trim：输入的值首尾空格过滤



### 过滤器

##### 定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理

##### 语法：

​	1.注册过滤器：Vue.filter( name , callback ) 或 new Vue{ filters:{ } }

​	2.使用过滤器：{{ xxx | 过滤器名 }} 或 v-bind：属性=“ xxx | 过滤名 “

##### 备注：

​	1.过滤器也可以接收额外参数，多个过滤器也可以串联

​	2.并没有改变原本的数据，是产生新的对应的数据



### 内置指令

##### v-bind：单向绑定解析表达式

##### v-model：双向数据绑定

##### v-for：遍历数组/对象/字符串

##### v-on：绑定事件监听，可简写为@

##### v-if：条件渲染（动态控制节点是否存在）

##### v-else：条件渲染（动态控制节点是否存在）

##### v-show：条件渲染（动态控制节点是否展示）

##### v-text：向其所在的节点中渲染文本内容，替换掉节点中的内容

##### v-html：向指定节点渲染包含html结构的内容

​	与插值语法的区别：

​		（1）v-html会替换掉节点中所有的内容

​		（2）v-html可以识别html结构

​	严重注意：v-html有安全性问题

​		（1）在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击

​		（2）一定要在可信的内容上使用v-html，永远不要用在用户提交的内容上

![image-20230328231800143](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230328231800143.png)

##### v-cloak指令（没有值）：

​	1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性

​	2.使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题

##### v-once指令（没有值）：

​	1.v-once所在节点在初次动态渲染后，就视为静态内容了

​	2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能

##### v-pre指令（没有值）：

​	1.跳过其所在节点的编译过程

​	2.可利用它跳过：没有使用指令语法，没有使用插值语法的节点，会加快编译



### 自定义指令

1.定义语法

​	（1）局部指令：

​			new  Vue ( { 

​				directives:{ 

​						指令名：{

​							bind( element , binding ){  },

​							inserted( element , binding ){  },

​							update( element , binding ){  }

​						}

​					}

​			 } ) 或者

​			new  Vue ( { 

​				directives:{

​						指令名( element , binding ){  }

​				}

​			 } )

​	（2）全局指令：

​			Vue.directive( 指令名 ，{

​					bind( element , binding ){  },

​					inserted( element , binding ){  },

​					update( element , binding ){  }

​			} ) 或者

​			Vue.directive( 指令名 ，回调函数 )

2.配置对象中常用的3个回调

​	（1）bind：指令与元素成功绑定时调用

​	（2）inserted：指令所在元素被插入页面时调用

​	（3）update：指令所在模版结构被重新解析时调用

3.备注

​	指令定义时不加v-，但使用时要加v-

​	指令名如果是多个单词，要使用kebab- case命名方式



### 生命周期

生命周期回调函数，生命周期函数，生命周期钩子

Vue在关键时刻帮我们调用的一些特殊名称的函数

生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的

生命周期函数中的this指向vm 或 组件实例对象

![image-20230330110153715](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230330110153715.png)

![image-20230330143402832](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230330143402832.png)

##### 常用的生命周期钩子

​	1.mounted：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】

​	2.beforeDestroy：清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】

##### 关于销毁Vue实例

​	1.销毁后借助Vue开发者工具看不到任何信息

​	2.销毁后自定义事件会失效，但原生DOM事件依然有效

​	3.一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程



# Vue组件化编程

### 模块与组件、模块化与组件化

 组件：实现应用中局部功能代码和资源的集合

![image-20230330172036636](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230330172036636.png)

![image-20230330172108013](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230330172108013.png)



### 非单文件组件

#####  Vue中使用组件的三大步骤：

##### 	1.定义组件

​		使用Vue.extend( options )创建，其中options和new Vue( options )时传入的那个options几乎一样，但也有区别：

​		 （1）el不要写----最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器

​		 （2）data必须写成函数----避免组件被复用时，数据存在引用关系

​		备注：使用template可以配置组件结构

##### 	2.如何注册组件

​		（1）局部注册：靠new  Vue的时候传入components选项

​		（2）全局注册：靠Vue.component( ‘组件名’ ，组件 )

##### 	3.编写组件标签：<组件名></组件名>

##### 几个注意点

##### 	1.关于组件名

​		一个单词组成：首字母大小写

​		多个单词组成：kebab-case命名和CamelCase命名

​		备注：

​			（1）组件名尽可能回避HTML中已有的元素名称

​			（2）可以使用nam e配置项指定组件在开发者工具中呈现的名字

##### 	2.关于组件标签

​		第一种：< school >< /school >

​		第二种：< school/ >	(不使用脚手架时，< school/ >会导致后续组件不能渲染)

##### 	3.一个简写方式

 		const school = Vue.extend( options )可简写为：const  school = options



##### 关于VueComponent

​	1.组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的

​	2.我们只需要写<组件名/>或<组件名></组件名>，Vue解析时会帮我们创建组件的实例对象，即Vue帮我们执行的：new  VueComponent( options )

​	3.特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent

​	4.关于this指向

​		（1）组件配置中：data函数，methods中的函数，watch中的函数，computed中的函数，它们的this均是【VueComponent实例对象 】

​		（2）new  Vue( )配置中：data函数，methods中的函数，watch中的函数，computed中的函数，它们的this均是【Vue实例】

​	5.VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）

##### 一个重要的内置关系：VueComponent.prototype.__ proto __ === Vue.prototype

##### 为什么要有这个关系：让组件实例对象（vc）可以访问到Vue原型上的属性、方法。

![image-20230331090947006](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230331090947006.png)



## Vue CLI （command line interface)

#### vue由vue核心和模版解析器组成

#### 关于不同版本的Vue

​	1.vue.js与vue.runtime.xxx.js的区别

​		（1）vue.js是完整版的Vue，包含核心功能+模版解析器

​		（2）vue.runtime.xxx.js是运行版的Vue，只包含核心功能，没有模版解析器

​	2.因为vue.runtime.xxx.js没有模版解析器，所以不能使用template配置项，需要使用render函数接收到的createElement函数去指定具体内容



#### render函数

render( createElement ){

​		return  createElement( "元素标签，如：h1" , " 元素内容 " )

}



#### Vue脚手架隐藏了所有webpack相关的配置，若想查看具体的webpack配置，请执行：vue  inspect > output.js

使用vue.config.js可以对脚手架进行个性化定制



#### 脚手架文件结构

node_modules：项目依赖文件夹

public：（一般放置一些静态资源，放置在public文件夹中的静态资源，webpack进行打包的时候，会原封不动打包到dist文件夹中）

​		favicon.ico：页签图标

​		index.html：主页面

src

​		assets：存放静态资源（组件共用的静态资源，在webpack打包的时候，会把静态资源当做一个模块，打包到JS文件里面）

​				logo.png

​		component：存放非路由组件（全局组件）

​		App.vue：汇总所有组件

​		main.js：程序入口文件

.gitignore：git版本管制忽略的配置

babel.config.js：babel的配置文件

package.json：应用包配置文件

README.md：应用描述文件

package-lock.json：缓存性文件，包版本控制文件



#### ref属性

1.被用来给元素或子组件注册引用信息（id的替代者）

2.应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象VueComponents



#### 配置项props

功能：让组件接收外部传过来的数据

1.传递数据：<Demo name="xxx" / >

2.接收数据：

​	（1）只接收：props：[' name ']

​	（2）限制类型：props：{ name:Number }

​	（3）限制类型、限制必要性、指定默认值：

​			props：{

​					name:{

​							type:String,  //类型

​							required:true,  //必要性

​							default:"xxx"  //默认值

​					}

​			}

备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据



#### mixin（混入，混合）	

功能：可以把多个组件共用的配置提取成一个混入对象

使用方式：

​	定义混合

​	使用混合	

​		（1）全局混合：Vue.mixin( xxx )

​		（2）局部混合：mixins: [ 'xxx' ]



#### 插件plugins

功能：用于增强Vue

本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据

定义插件：

​	对象.install = function( Vue , options ){

​		//添加全局过滤器

​		Vue.filter( ... )



​		//添加全局指令

​		Vue.directive( ... )



​		//配置全局混合

​		Vue.mixin( ... )



​		//添加实例方法

​		Vue.prototype.$myMethod = function ( ){ ... }

​		Vue.prototype.$myProperty = xxx

​	}

使用插件：Vue.use( )



#### scoped样式

作用：让样式在局部生效，防止冲突



#### TodoList案例

##### 组件化编码流程

1.实现静态组件：抽取组件，使用组件实现静态页面效果

2.展示动态数据

​	（1）数据的类型、名次是什么

​	（2）数据保存在哪个组件

3.交互----从绑定事件监听开始

##### props适用于

1.父组件 ==> 子组件通信

2.子组件 ==> 父组件通信（要求父组件先给子组件一个函数）

##### 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的

##### props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做



### webStorage

##### 1.存储内容大小一般支持5MB左右（不同浏览器可能不一样）

##### 2.浏览器端通过Window.sessionStorage和Window.localStorage属性实现本地存储机制

##### 3.相关API：

​	（1）xxxxxStorage.setItem( "key" , "value" )。该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值

​	（2）xxxxxStorage.getItem("key")。该方法接受一个键名作为参数，返回键名对应的值

​	（3）xxxxxStorage.removeItem("key")。该方法接受一个键名作为参数，并把该键名从存储中删除

​	（4）xxxxxStorage.clear()。该方法会清空存储中的所有数据

##### 备注

​	（1）sessionStorage存储的内容会随着浏览器窗口关闭而消失

​	（2）localStorage存储的内容，需要手动清除才会消失



#### 组件自定义事件

##### 1.一种组件间通信的方式，适用于：子组件 ===> 父组件

##### 2.使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（事件的回调在A中）

##### 3.绑定自定义事件

​	（1）第一种方式：在父组件中< Demo  @shanghai="test" / >或< Demo  v-on:shanghai="test" >

​	（2）第二种方式：在父组件中< Demo  ref="demo" >

​										mounted( ){

​												this.$refs.demo.$on("shanghai" , this.test)

​										}

​	（3）若想让自定义事件只触发一次，可以使用once修饰符，或$once方法

##### 4.触发自定义事件：this.$emit( "shanghai" , 数据 )

##### 5.解绑自定义事件：this.$off( "shanghai" )

##### 6.组件上也可以绑定原生DOM事件，需要使用native修饰符

##### 7.注意：通过this.$refs.demo.$on( "shanghai" , 回调函数 )绑定自定义事件时，回调要么配置在methods中，要么用箭头函数，否则this指向会出问题



## 全局事件总线（GlobalEventBus）

##### 1.一种组件间通信的方式，适用于任意组件间通信

##### 2.安装全局事件总线

​	new  Vue( { 

​		......

​		beforeCreate( ){ 

​				Vue.prototype.$bus = this

​		}

​		......

​	 } )

##### 3.使用事件总线

​	（1）接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的回调留在A组件自身

​			methods:{

​					demo( data ){ ....... }

​			}

​			mounted( ){

​					this.$bus.$on( "xxx" , this.demo )

​			}

​	（2）提供数据：this.$bus.$emit( "xxx" , 数据 )

##### 4.最好在beforeDestroy钩子中，用$off去解绑当前组件所用到的事件



#### 消息订阅与发布

1.一种组件间通信的方式，适用于任意组件间通信

2.使用步骤

​	（1）安装pubsub：npm i pubsub-js

​	（2）引入：import  pubsub  from  "pubsub-js"

​	（3）接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调函数留在A组件自身

​				methods( ){

​						demo( data ){ ...... }

​				}

​				mounted( ){

​						this.pid = pubsub.subscribe( "xxx" , this.demo )

​				}

​				beforeDestroy( ){

​						pubsub.unsubscribe( pid )

​				}

​	（4）提供数据：pubsub.publish( "xxx" , 数据 )



## nextTick（生命周期钩子）

1.语法：this.$nextTick( 回调函数 )

2.作用：在下一次DOM更新循环结束之后执行其指定的回

3.什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行



#### Vue封装的过度与动画

![image-20230405223220484](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230405223220484.png)

1.准备好样式：

​	（1）元素进入的样式

​			v-enter：进入的起点

​			v-enter-active：进入过程中

​			v-enter-to：进入的终点

​	（2）元素离开的样式

​			v-leave：离开的起点

​			v-leave-active：离开过程中

​			v-leave-to：离开的终点

2.使用< transition >包裹要过度的元素，并配置name属性

3.若有多个元素需要过度，则需要使用< transition-group >，且每个元素都要指定key值 



## Vue脚手架配置代理

##### 方法一

在vue.config.js中添加如下配置

	devServer:{
		proxy:"http://localhost:6000"
	}
说明：

​	1.优点：配置简单，请求资源时直接发给前端（8080）即可

​	2.缺点：不能配置多个代理，不能灵活的控制请求是否走代理

​	3.工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器（优先匹配前端资源）

##### 方法二

编写vue.config.js配置具体代理规则



    module.exports = {
      devServer:{
        proxy:{
        	//匹配所有以‘api’开头的请求路径
          '/api':{
          	//代理目标的基础路径
            target:"http://localhost:6000",
            //正则表达，去除代理服务器向服务器发送请求资源的后缀名/api
            pathRewrite:{"^/api" : ""},
            ws:true,  //用于支持websocket,默认为true
            changeOrigin:true //用于控制请求头中的host值 ,默认为	true
          },
          //配置多个代理服务器
          '/demo':{
            target:"http://localhost:6001",
            pathRewrite:{"^/demo" : ""}
          	}
          /* '/foo':{
      					} */
    		}
    	}
    }
    /*
    	changeOrigin设置为true时，服务器收到的请求头中的host为服务器端口
    	changeOrigin设置为false时，服务器收到的请求头中的host为请求端口
    */
 说明：

​	1.优点：可以配置多个代理，且可以灵活的控制请求是否走代理

​	2.缺点：配置略微繁琐，请求资源时必须加前缀 



#### Vue-slot插槽

##### 作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于父组件 ===> 子组件

##### 分类：默认插槽，具名插槽，作用域插槽

##### 使用方式

##### 	1.默认插槽

​			父组件中：

​				< Category >

​						< div > html结构 < /div >

​				< /Category >

​			子组件中：

​				< template >

​						< div >

​							< !-- 定义插槽 -- >

​							< slot >插槽默认内容.....< /slot >

​						< /div >

​				< /template >

##### 2.具名插槽

​			父组件中：

​				< Category >

​						< template  slot="cent" >

​								< div > html结构 < /div >

​						< /template >



​						< template  v-slot=foot" >

​								< div > html结构 < /div >

​						< /template >

​				< /Category >

​			子组件中：

​				< template >

​						< div >

​							< !-- 定义插槽 -- >

​							< slot  name="cont">插槽默认内容.....< /slot >

​							< slot  name="foot">插槽默认内容.....< /slot >

​						< /div >

​				< /template >

##### 	3.作用域插槽

​		（1）理解：数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。（数据在子组件中，但使用数据遍历出来的结构由父组件决定

​		（2）具体编码：

​				父组件中：

​				< Category >

​						< template  slot-scope="dataObj" >

​								< ul >

​										< li  v-for="( data , index )  in  dataObj.data"  :key="index" >{{ data }}< /li>

​								< /ul >

​						< /template >

​				< /Category >

​			子组件中：

​				< template >

​						< div >

​							< !-- 定义插槽 -- >

​							< slot  :data="data">插槽默认内容.....< /slot >

​						< /div >

​				< /template >



# Vuex

专门在Vue中实现集中式状态（数据）管理的一个Vue插件，对Vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信

![image-20230406234318333](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230406234318333.png)

![image-20230406234738906](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230406234738906.png)

##### 多个组件依赖于同一状态和来自不同组件的行为需要变更为同一状态时，使用Vuex

![image-20230407090250132](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230407090250132.png)

![image-20230407171243756](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230407171243756.png)

![image-20230407173728718](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230407173728718.png)

##### 备注：mapActions与mapMutations使用时，若需要传递参数需要：在模版中绑定事件时传递好参数，否则参数是事件对象

#### 模块化+命名空间

![image-20230407233924942](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230407233924942.png)

![image-20230407233956116](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230407233956116.png)



# Vue路由

路由就是一组key-value的对应关系，多个路由，需要经过路由器的管理，key为路径，value可能是function或component

![image-20230407235925774](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230407235925774.png)

![image-20230409192016229](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230409192016229.png)

##### 路由分类

（1）后端路由

​		value是function，用于处理客户端提交的请求。工作过程中，服务器接收到一个请求时，根据请求路径找到匹配的函数来处理请求，返回响应数据

（2）前端路由

​		value是component，用于展示页面内容。工作过程中，当浏览器的路径改变时，对应的组件就会显示

#### 基本使用

![image-20230408095956404](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408095956404.png)

![image-20230408100021228](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408100021228.png)

#### 注意

1.路由组件通常存放在pages文件夹，一般组件通常存放在component文件夹

2.通过切换，“隐藏”了的路由组件，默认是被销毁的，需要的时候再去挂载

3.每个组件都有自己$route属性，里面存储着自己的路由信息

4.整个应用只有一个router，可以通过组件的$router属性获取到



#### 嵌套（多级）路由

![image-20230408112928199](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408112928199.png)



#### 路由传参

![image-20230408160229589](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408160229589.png)

![image-20230408160906324](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408160906324.png)

![image-20230408161429998](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408161429998.png)

路由携带params参数时，若使用对象写法，则不能使用path配置项，必须使用name配置

在配置路由的时候，在占位的后面加上一个问号params可以传递或者不传递

![image-20230408164645532](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408164645532.png)

第二种写法只能传递params参数

![image-20230408165810902](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408165810902.png)

#### ![image-20230408181937922](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408181937922.png)

![image-20230410153252392](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230410153252392.png)







![image-20230408202002586](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408202002586.png)

![image-20230408210353329](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408210353329.png)



## 路由守卫

![image-20230409000215241](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230409000215241.png)

![image-20230409000737835](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230409000737835.png)

![image-20230409093927405](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230409093927405.png)

![image-20230430085055189](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230430085055189.png)



### 路由器的两种工作模式

![image-20230409103539315](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230409103539315.png)

npm i connect-history-api-fallback



### 路由懒加载

当打包构建应用时，JavaScript包会变得非常大，影响页面加载

如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了。





![image-20230409103759202](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230409103759202.png)





## 组件通信

#### 1.props

适用场景：父子组件通信

功能：让组件接收外部传过来的数据

注意事项：

​	（1）如果父组件给子组件传递数据（函数）：本质其实是子组件给父组件传递数据

​	（2）如果父组件给子组件传递数据（非函数）：本质就是父组件给子组件传递数据

1.传递数据：<Demo name="xxx" / >

2.接收数据：

​	（1）只接收：props：[' name ']

​	（2）限制类型：props：{ name:Number }

​	（3）限制类型、限制必要性、指定默认值：

​			props：{

​					name:{

​							type:String,  //类型

​							required:true,  //必要性

​							default:"xxx"  //默认值

​					}

​			}

备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据

#### 路由的props

![image-20230408164645532](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230408164645532.png)



#### 2.自定义事件

##### （1）一种组件间通信的方式，适用于：子组件 ===> 父组件

##### （2）使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（事件的回调在A中）

##### （3）绑定自定义事件

​		1）第一种方式：在父组件中< Demo  @shanghai="test" / >或< Demo  v-on:shanghai="test" >

​		2）第二种方式：在父组件中< Demo  ref="demo" >

​										mounted( ){

​												this.$refs.demo.$on("shanghai" , this.test)

​										}

​		3）若想让自定义事件只触发一次，可以使用once修饰符，或$once方法

##### （4）触发自定义事件：this.$emit( "shanghai" , 数据 )

##### （5）解绑自定义事件：this.$off( "shanghai" )

##### （6）组件上也可以绑定原生DOM事件，需要使用native修饰符

##### （7）注意：通过this.$refs.demo.$on( "shanghai" , 回调函数 )绑定自定义事件时，回调要么配置在methods中，要么用箭头函数，否则this指向会出问题

##### （8）子组件非原生DOM节点，所以给子组件添加原生DOM事件会默认为是自定义事件。子组件触发原生DOM事件需要加上修饰符.native，原理是给子组件的根结点添加原生DOM事件，利用了事件委派

##### （9）原生DOM绑定自定义事件没有任何意义，因为没有办法发送$emit函数

##### （10）原生DOM当中的oninput事件，它经常结合表单元素一起使用，当表单元素文本内容发生变化的时候就会触发一次回调，   ：value="msg"   @input="msg = $event.target.value"实现数据的双向绑定v-model的功能

##### （11）v-model实现父子组件数据同步（父子组件通信）

##### 父组件

![image-20230502180749773](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230502180749773.png)

##### 子组件

![image-20230502181047216](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230502181047216.png)

##### v-model实现的原理：通过value与input事件实现，而且还需要注意可以通过v-model实现父子组件数据同步

##### （12）sync属性修饰符，:money.sync="money"相当于父组件给子组件传递props的同时，给当前子组件绑定了一个自定义事件，事件名为update:money。

##### 父组件

![image-20230502212554499](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230502212554499.png)

##### 子组件

![image-20230502212753389](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230502212753389.png)

##### （13）$attrs与$listeners

$attrs属于组件的一个属性，可以获取到父组件传递过来的props数据。对于子组件而言，父组件给的数据可以利用props接收，但是需要注意，如果子组件已经通过props接收的属性，在$attrs属性当中是获取不到的。

![image-20230503000444996](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230503000444996.png)

$listeners也是组件实例自身的一个属性，它可以获取到父组件给子组件传递的自定义事件

![image-20230503000532936](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230503000532936.png)

##### （14）$children与$parent

组件实例自身拥有一个属性$children，可以获取到当前组件当中全部子组件

可以通过$parent属性获取到某一个组件的父组件，可以操作父组件的数据与方法











#### 3.全局事件总线

##### （1）一种组件间通信的方式，适用于任意组件间通信

##### （2）安装全局事件总线

​		new  Vue( { 

​			......

​			beforeCreate( ){ 

​					Vue.prototype.$bus = this

​			}

​			......

​	 	} )

##### （3）使用事件总线

​		1）接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的回调留在A组件自身

​			methods:{

​					demo( data ){ ....... }

​			}

​			mounted( ){

​					this.$bus.$on( "xxx" , this.demo )

​			}

​		2）提供数据：this.$bus.$emit( "xxx" , 数据 )

##### （4）最好在beforeDestroy钩子中，用$off去解绑当前组件所用到的事件



#### 4.pubsub-js（在react框架中使用比较多）

##### 消息订阅与发布

（1）一种组件间通信的方式，适用于任意组件间通信

（2）使用步骤

​		1）安装pubsub：npm i pubsub-js

​		2）引入：import  pubsub  from  "pubsub-js"

​		3）接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调函数留在A组件自身

​				methods( ){

​						demo( data ){ ...... }

​				}

​				mounted( ){

​						this.pid = pubsub.subscribe( "xxx" , this.demo )

​				}

​				beforeDestroy( ){

​						pubsub.unsubscribe( pid )

​				}

​		4）提供数据：pubsub.publish( "xxx" , 数据 )



#### 5.Vuex



#### 6.插槽

#### Vue-slot插槽

##### 作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于父组件 ===> 子组件

##### 分类：默认插槽，具名插槽，作用域插槽

##### 使用方式

##### 	1.默认插槽

​			父组件中：

​				< Category >

​						< div > html结构 < /div >

​				< /Category >

​			子组件中：

​				< template >

​						< div >

​							< !-- 定义插槽 -- >

​							< slot >插槽默认内容.....< /slot >

​						< /div >

​				< /template >

##### 2.具名插槽

​			父组件中：

​				< Category >

​						< template  slot="cent" >

​								< div > html结构 < /div >

​						< /template >



​						< template  v-slot=foot" >

​								< div > html结构 < /div >

​						< /template >

​				< /Category >

​			子组件中：

​				< template >

​						< div >

​							< !-- 定义插槽 -- >

​							< slot  name="cont">插槽默认内容.....< /slot >

​							< slot  name="foot">插槽默认内容.....< /slot >

​						< /div >

​				< /template >

##### 	3.作用域插槽

​		（1）理解：数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。（数据在子组件中，但使用数据遍历出来的结构由父组件决定

​		（2）具体编码：

​				父组件中：

​				< Category >

​						< template  slot-scope="dataObj" >

​								< ul >

​										< li  v-for="( data , index )  in  dataObj.data"  :key="index" >{{ data }}< /li>

​								< /ul >

​						< /template >

​				< /Category >

​			子组件中：

​				< template >

​						< div >

​							< !-- 定义插槽 -- >

​							< slot  :data="data">插槽默认内容.....< /slot >

​						< /div >

​				< /template >



## 深度选择器

##### Scoped属性的作用

加上scoped的作用是样式只对当前的组件有用

对于某一个组件，如果style添加scoped属性，则当前子组件的结构中都添加上了一个data-v-xxxx自定义属性，在vue中是通过属性选择器，给需要添加的元素添加上样式

##### 子组件的根标签拥有父组件当中一样的自定义属性，如果子组件的根节点和父组件中书写的样式相同，也会添加上相应的样式

注意：

如果父组件的样式已经添加了scoped属性，还想影响子组件的样式，可以使用深度选择器

深度选择器可以实现样式穿透

原生css    >>>

less		/deep/

scss		::v-deep





http://gmall-h5-api.atguigu.cn



后台文档swagger地址

http://39.98.123.211:8170/swagger-ui.html

http://39.98.123.211:8510/swagger-ui.html



首页三级分类GET请求

/api/product/getBaseCategoryList



搜索页POST请求

/api/list



获取商品详情GET请求

/api/item/{skuId}



添加购物车POST请求

/api/cart/addToCart/{skuId}/{skuNum}



购物车列表GET请求

/api/cart/cartList



删除购物车物品DELETE请求

/api/cart/deleteCart/{skuId}



切换商品选中状态GET请求

/api/cart/checkCart/{skuId}/{isChecked}



获取验证码GET请求

/api/user/passport/sendCode/{phone}



获取用户地址信息GET请求

/api/user/userAddress/auth/findUserAddressList



token校验GET请求

/api/user/passport/auth/getUserInfo



注册用户POST请求

/api/user/passport/register



用户登录POST请求

/api/user/passport/login



用户退出登录GET请求

/api/user/passport/logout



获取订单交易页信息GET请求

/api/order/auth/trade



提交订单POST请求你

/api/order/auth/submitOrder?tradeNo={tradeNO}



获取订单支付信息GET请求

/api/payment/weixin/createNative/{orderId}



查询支付订单状态GET请求

/api/payment/weixin/createNative/${orderId}



获取我的订单列表GET

/api/order/auth/{page}/{limit}

















#### mock数据 mock.js

前端mock数据不会和你的服务区进行任何通信



#### uuid游客身份

通过本地存储获取一个uuid

```js
//要生成一个随机字符串，且每次执行不能发生变化，游客身份持久存储
export const getUUID = () => {

    //先从本地存储获取uuid，看本地存储里面是否拥有
    let uuid_token = localStorage.getItem("UUIDTOKEN")

    if(!uuid_token){
        uuid_token = uuidv4()
        localStorage.setItem("UUIDTOKEN" , uuid_token)
    }
    return uuid_token
}
```

在发送请求之前，将uuid写入请求头

```js
//请求拦截器：在发请求之前，请求拦截器可以检测到，可以在请求发送之前做一些事情
requests.interceptors.request.use((config) => {
    //config：配置对象,headers请求头

    if(store.state.detailOptions.uuid_token){
        //请求头添加一个字段
        config.headers.userTempId = store.state.detailOptions.uuid_token
    }

    return config
})
```



### token令牌

![image-20230426193418101](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230426193418101.png)

vuex仓库存储数据不是持久化



生成二维码

npm i qrcode



图片懒加载

https://www.npmjs.com/package/vue-lazyload



表单验证

vee-validate



后台管理项目

https://github.com/PanJiaChen/vue-admin-template

https://github.com/PanJiaChen/vue-element-admin





# 后台项目

build
     ----index.js webpack配置文件【很少修改这个文件】
mock
     ----mock数据的文件夹【模拟一些假的数据mockjs实现的】，因为咱们实际开发的时候，利用的是真是接口

node_modules
     ------项目依赖的模块

public
     ------ico图标,静态页面，publick文件夹里面经常放置一些静态资源，而且在项目打包的时候webpack不会编译这个文件夹，原封不动的打包到dist文件夹里面

src
    -----程序员源代码的地方
    ------api文件夹:涉及请求相关的
    ------assets文件夹：里面放置一些静态资源（一般共享的），放在aseets文件夹里面静态资源，在webpack打包的时候，会进行编译
    ------components文件夹：一般放置非路由组件获取全局组件
    ------icons这个文件夹的里面放置了一些svg矢量图
    ------layout文件夹：他里面放置一些组件与混入
    ------router文件夹：与路由相关的
    -----store文件夹：一定是与vuex先关的
    -----style文件夹：与样式先关的
    ------utils文件夹：request.js是axios二次封装文件****
    ------views文件夹：里面放置的是路由组件

App.vue:根组件
main.js：入口文件
permission.js:与导航守卫先关、
settings：项目配置项文件
.env.development：开发环境的配置文件
.env.producation：上线环境的配置文件

.env.staging：测试环境的配置文件





用户登录POST请求

/admin/acl/index/login



用户退出登录POST请求

/admin/acl/index/logout



获取用户信息GET请求

/admin/acl/index/info



获取品牌管理数据



##### /admin/product/baseTrademark/getTrademarkList

/admin/product/spuImageList





# Vue3

```ts
//构建Vue3项目
使用vite构建  npm init vite@latest
使用vue脚手架构建	npm init vue@latest
```



![image-20230605160009734](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605160009734.png)

#### VUE3的diff算法

1.前序对比算法

2.尾序对比算法

3.新节点如果多出来就挂载

4.旧节点如果多出来就卸载

5.特殊情况乱序

![image-20230605163335502](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605163335502.png)





## 常用的composition API

#### 1.setup

![image-20230528162026038](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230528162026038.png)

##### 注意：通过Suspense和异步组件的配合使用，可以返回一个Promise实例



#### 2.ref函数

![image-20230605165031323](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605165031323.png)

![image-20230528161957808](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230528161957808.png)

![image-20230605165129304](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605165129304.png)

![image-20230605165211712](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605165211712.png)

```ts
//获取DOM元素
<div ref="dom">DIV</div>

const dom = ref<HTMLDivElement>()
//需要在onMounted()之后才能获取到DOM数据
onMounted(() => {
  console.log(dom.value?.innerHTML)
});
```





#### 3.reactive函数

![image-20230528162437276](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230528162437276.png)

```ts
type M = {
  name: string
  age: number
}

const m = reactive<M>({
  name: 'zs'
  age: 24
})
```

##### 注意：使用reactive声明的响应式数据，不能对其直接赋值，否则会破坏响应式数据





#### 4.Vue3中的响应式原理

![image-20230529085805515](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529085805515.png)通过$set和 $delete新增属性和删除属性，数组也可以通过数组的方法修改数组数据。

![image-20230529092504532](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529092504532.png)



通过Reflect.defineProperty代替Object.defineProperty去操作

![image-20230529093352590](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529093352590.png)  



![image-20230529093716350](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529093716350.png)

![image-20230529093825746](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529093825746.png)



#### 5.reactive对比ref

![image-20230529093855860](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529093855860.png)



#### 6.setup的两个注意点

![image-20230529094238572](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529094238572.png)



#### 7.计算属性与监视

![image-20230605202103467](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230605202103467.png)

![image-20230529101026184](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529101026184.png)

![image-20230529103048353](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529103048353.png)

![image-20230529111909985](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529111909985.png)



#### 8.生命周期

![image-20230529114027413](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529114027413.png)



#### 9.自定义hook函数

![image-20230529144418618](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529144418618.png)

#### toRefs实现原理

```ts
const toRefs = <T extends object>(obj: T) => {
  const map: any = {}
  
  for(let key in obj) {
    map[key] = toRef(obj, key)
  }
  
  return map
}
```





## 其它Composition API

#### 1.shallowReactive与shallowRef

![image-20230529150649957](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529150649957.png)

```ts
const m = shallowRef({name: 'zs'})

m.value.name = 'ls'  => 修改不了，只监听到value
m.value = {name: 'ls'}  => 成功修改
```

##### 注意：ref和shallowRef是不能一起写的，不然会影响shallowRef，造成视图的更新，因为ref底层会调用triggerRef()，强制更新页面DOM。reactive与shallowReactive情况同上



#### 2.readonly与shallowReadonly

![image-20230529151300646](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529151300646.png)



#### 3.toRaw与markRaw

![image-20230529155025399](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529155025399.png)

toRaw不能将ref生成的响应式数据转换为普通数据



#### 4.customRef

```ts
function myRef(value){
  let flag = null
  return customRef((track, trigger) => {
      return {
          get(){
              console.log('读取数据')
              track()  //追踪数据的变化
              return value
          },

          set(newValue){
              clearInterval(flag)
              flag = setTimeout(() => {
                 value = newValue
              		console.log('修改数据')
                  trigger()  //通知trigger重新解析模版
              },500)
          }
      }
  })
}
```





#### 5.provide与inject

![image-20230531212351132](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531212351132.png)



#### 6.响应式数据的判断

![image-20230531213354546](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531213354546.png)





## 新的组件

#### 1.Fragment

![image-20230531214236833](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531214236833.png)



#### 2.Teleport

![image-20230531214306640](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531214306640.png)



#### 3.Suspense

![image-20230531220147577](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531220147577.png)

可以搭配promise使用

应用组件中

```js
setup(){
    let isShow = ref(false)
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve({isShow})
        }, 5000)
    })
}

或者

async setup(){
        let isShow = ref(false)

        let p = new Promise((resolve) => {
            setTimeout(() => {
                resolve({isShow})
            }, 5000)
        })
        
        return await p
    }
```





## 其它改动

![image-20230531233523147](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531233523147.png)

![image-20230531233600083](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531233600083.png)

![image-20230531233756354](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531233756354.png)

![image-20230531233954273](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531233954273.png)





## Vue3组件通信

#### vue2组件通信方式

![image-20230531234430052](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531234430052.png)



## Vue3组件通信

#### 1.props

props可以实现父子组件通信，在Vue3中可以通过defineProps获取父组件传递的数据。且组件内部不需要引入defineProps就可以直接使用。

#### 2.自定义事件

##### 在Vue3中自定义组件标签上可以使用原生DOM事件，利用defineEmits方法返回函数触发自定义事件

```ts
const emit = defineEmits(['自定义事件名称'])
const handler = () => {
  emit('自定义事件名称', 传递参数)
}
```

#### 3.全局事件总线

```ts
npm i mitt -S

//引入mitt
import mitt from 'mitt'
const Mit = mitt()
export default Mit

//使用mitt完成全局事件总线
import bus from '文件所在位置'
//组件挂载完毕，添加时间
onMounted(() => {
  bus.on("事件名称" , (接收参数) => {
    	事件回调
  })
})

//使用mitt触发全局事件总线
import bus from '文件所在位置'
const btn = () => {
  bus.emit("事件名称" , 传递参数)
}
```

#### 4.v-model

 ```ts
 //父组件
 <Child :modeValue='money' @update:modeValue='handler' />
 <Child v-model:modeValue='money' />
 <script setup lang="ts">
   let money = ref(1000)
 </ script>
 
 
 //子组件
 <button @click="add">money + 1</ button>
 
 <script setup lang="ts">
   const props = defineProps(['modeValue'])
 	const emit = defineEmits(['update:modeValue'])
   
   const add = () => {
     emit('handler', 1)
   }
 </ script>
 ```

![image-20230606235328410](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230606235328410.png)

##### 绑定多个v-model

```ts
//父组件
<Child v-model:value='money' v-model:page='page'  />
<script setup lang="ts">
  let money = ref(1000)
	let page = ref('hello')
</ script>


//子组件
<button @click="add">money + 1</ button>

<script setup lang="ts">
  const props = defineProps(['value', 'page'])
	const emit = defineEmits(['update:value', 'update:page'])
  
  const add = () => {
    emit('update:value', 1)
    emit('update:page,"asd")
  }
</ script>
```

#### 5.useAttrs

```ts
import { useAttrs } from "vue"
```

useAttrs方法，可以获取到父组件传递过来的props数据与事件。对于子组件而言，父组件给的数据和事件可以利用props接收，但是需要注意，如果子组件已经通过props接收的属性，在$attrs属性当中是获取不到的。

#### 6.ref与$parent

#### 想让外部访问需要通过defineExpose方法对外暴露

##### ref：可以获取真实的DOM节点，可以获取到子组件实例VC

```ts
//获取DOM元素
<div ref="dom">DIV</div>
<button @click="add">点击</button>

const dom = ref<HTMLDivElement>()

//需要在onMounted()之后才能获取到DOM数据
onMounted(add);

//当需要通过事件去操作DOM时，先声明函数，在传递给onMounted
const add = () => {
  dom.value?.innerHTML = 'hello'
  console.log(dom.value?.innerHTML)
}
```

##### $parent：可以在子组件内获取到父组件的实例

```ts
//子组件
<button @click="add($parent)">money + 1</button>

const add = (parent: any) => {
  console.log(parent.money)
}

//父组件
defineExpos({
  money
})
```

#### 7.Provide与Inject

![image-20230531212351132](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531212351132.png)

#### 8.pinia

##### 集中式管理状态容器，可以实现任意组件之间通信

##### 核心概念：state, actions, getters

##### 选择式API

```ts
npm i pinia
//全局注册大仓库
import { createPinia } from 'pinia'
const store = createPinia()
export default store

import store from './store'
app.use(store)

//创建小仓库
import { defineStore } from "pinia";
//第一个参数为仓库名字，第二个为仓库配置对象
//defineStore方法执行会返回一个函数，函数的作用就是让组件可以获取到仓库数据
const InfoStore = defineStore("info", {
    state:() => {
        return {
            count: 99
        }
    },
    actions:{
      updateSum(){
        this.count ++
      }
    },
    getters: {
        
    }
})
export default InfoStore

//使用仓库
<h2>pinia中的数据{{ infoStore.count }}</h2>
<el-button @click="updateInfo">点击修改仓库数据</el-button>

import InfoStore from '../store/modules/info';

const infoStore = InfoStore()
const updateInfo = () => {
    //可以直接修改仓库的值
    /* infoStore.count++ */

    //可以通过仓库的$patch方法
   /*  infoStore.$patch({
        count: 999
    }) */

    //可以通过调用仓库里的actions配置项里的方法
    infoStore.updateSum()
}
```

##### 组合式API

```ts
//创建小仓库，组合式API
import { defineStore } from "pinia";
import { reactive } from "vue";

const TodoStore = defineStore("todo", () => {

    const todo = reactive([{id: 1, name: 'zs'}, {id: 2, name: 'ls'}, {id: 3, name: 'wu'}])

    return {
        todo,
      	updataTodo(){
            todo.push({id: 4, name:'zl'})
        }
    }
})
export default TodoStore

//使用仓库
<el-button @click="updateInfo">点击修改仓库数据</el-button>

import TodoStore from '../store/modules/todo'
const todoStore = TodoStore()
const updateInfo = () => {
    todoStore.updataTodo()
}
```

#### 9.插槽slot

```ts
//父组件
<Child>
    <div>
      <pre>默认插槽</pre>
    </div>

    <!-- v-slot:child ==> #child -->
    <template #child>
      <div>
        <pre>具名插槽</pre>
      </div>
     </template>
</Child>

//子组件
<!-- 默认插槽 -->
<slot></slot>

<!-- 具名插槽 -->
<slot name="child"></slot>
```

##### 作用域插槽

```ts
//父组件
<Child :list="list">
    <!-- 作用域插槽：就是可以传递数据的插槽，子组件可以将数据回传给父组件，父组件可以决定这些回传的数据是以何种结构在子组件内部展示  -->
    <template v-slot="{ row }">
      <div>
        <h2 :style="{color: row.done ? 'green' : 'red'}">{{ row.name }}</h2>
      </div>
    </template>
</Child>


//子组件
<!-- 作用域插槽 -->
<ul>
   <li v-for="item1 in props.list" :key="item1.id">
       <!-- 可以将数据回传给父组件 -->
       <slot :row="item1"></slot>
   </li>
</ul>
```



### svg图标的使用

```ts
npm i vite-plugin-svg-icons

//在vite.config.ts文件中配置
import { createSvgIconsPlugin } from 'vite-plugin-svg-icons';

 plugins: [
    vue(),
    createSvgIconsPlugin({
      iconDirs: [path.resolve(process.cwd(), 'src/assets/icons')],
      symbolId: 'icon-[dir]-[name]',
    }),
  ],
   
//在入口文件main.ts中引入
import 'virtual:svg-icons-register';

//在组件中使用
//svg：图标外层容器节点，内部需要与use标签结合使用
<svg>
  //xlink:href配置图标文件，属性值前面需要添加#icon-
  <use xlink:href="#icon-SVG文件名" fill="red"></use>
</svg>
```



服务器接口

http://sph-api.atguigu.cn

接口文档

http://39.98.123.211:8510/swagger-ui.html

http://139.198.104.58:8212/swagger-ui.html































































































































































































































































































































































































































































































































