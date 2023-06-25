## fs文件系统模块

fs模块是Node.js官方提供的，用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。如

​	fs.readFile( ) 用来读取指定文件中的内容

​	fs.writeFile( ) 用来向指定的文件中写入内容

##### 在javascript代码中，使用fs模块来操作文件，需要使用如下的方式先导入：const  fs  =  require( ' fs ' )

#### 1.读取指定文件中的内容

##### 	fs.readFile( path[ , options ] , callback ) 

​	参数1:必选参数，字符串，表示文件的路径

​	参数2，可选参数，表示以什么编码格式来读取文件

​	参数3，必选参数，文件读取完成后，通过回调函数拿到读取的结果

![image-20230224092022901](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230224092022901.png)

​	可以判断err对象是否为null，来判断文件是否读取成功

#### 2.向指定的文件写入内容

##### 	fs.writeFile( file , data [ , options ] , callback )

​	参数1:必选参数，需要指定一个文件路径的字符串，表示文件的存放路径

​	参数2:必选参数，表示要写入的内容

​	参数3:可选参数，表示以什么格式写入文件内容，默认值是utf-8

​	参数4:必选参数，文件写入完成后的回调函数

![image-20230224094444911](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230224094444911.png)

​	可以判断err对象是否为null，判断文件是否写入成功

![image-20230307203037238](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230307203037238.png)

#### 3.路径动态拼接的问题

在使用fs模块操作文件时，如果提供的操作是以 ./ 或../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。因为代码在运行的时候，会以执行node命令时所处的目录，动态拼接出被操作文件的完整路径。如果要解决这个问题，可以提供一个完整的文件存放路径。

使用__dirname表示当前文件所处的目录

![image-20230307230616124](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230307230616124.png)



## path路径模块

path.join ( )方法，用来将多个路径片段拼接成一个完整的路径字符串

path.basename ( )方法，用来从路径字符串中，将文件名解析出来

##### 在javascript代码中，使用path模块来操作文件，需要使用如下的方式先导入：const  path  =  require( ' path ' )

#### 1.路径拼接

##### path.join ( [...paths] )

​	...path< string >路径片段的序列

​	返回值：< string >

![image-20230307231710343](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230307231710343.png)

注意 ../ 会抵消一层路径

#### 2.获取路径中的文件名

##### path.basename ( path[ , ext ] )

​	path < string >必选参数，表示一个路径的字符串

​	ext < string >可选参数，表示文件拓展名

​	返回值：< string > 表示路径中的最后一部分

![image-20230310162524085](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230310162524085.png)

#### 3.获取路径中的文件拓展名

##### path.extname ( path )

​	path < string >必选参数，表示一个路径的字符串

​	返回值：< string > 返回得到的拓展名字符串

![image-20230310162953307](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230310162953307.png)



## HTTP模块

http模块是Node.js官方提供的，用来创建web服务器的模块。通过http模块提供的http.createServer ( )方法，就能方便的把一台普通的电脑，变成一台Web服务器，从而对外提供Web资源服务。

![image-20230314110131551](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230314110131551.png)

![image-20230314110217985](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230314110217985.png)

![image-20230314110537313](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230314110537313.png)

#### 1.创建web服务器的基本步骤

##### 	导入http模块： const  http = require ( 'http' )

##### 	创建web服务器实例： const  server = http.createServer ( )

##### 	为服务器实例绑定request事件，监听客户端的请求

![image-20230314111203512](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230314111203512.png)

##### 	启动服务器

![image-20230314111503595](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230314111503595.png)

#### 2.req请求对象

只要服务器接收到了客户端的请求，就会调用通过server.on ( )为服务器绑定request事件处理函数

如果想在事件处理函数中，访问与客户端相关的数据或属性，可以使用如下的方式

![image-20230314163535706](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230314163535706.png)



![image-20230318161040906](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230318161040906.png)



## 模块化

解决一个复杂问题时，自顶向下逐层把系统划分成为若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

#### Node.js中根据模块来源的不同，将模块分为了3大类，分别是：

内置模块（内置模块是由Node.js官方提供的，例如fs , path , http等）

自定义模块（用户创建的每个 .js文件，都是自定义模块）

第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）



##### Node.js遵循了CommonJS模块化规范，CommonJS规定了模块的特性和各模块之间如何相互依赖

##### CommonJS规定：

​	每个模块内部，module变量代表当前模块

​	module变量是一个对象，它的exports属性（即module.exports）是对外的接口

​	加载某个模块，其实是加载该模块的module.exports属性。require ( )方法用于加载模块



#### 1.加载模块

使用require ( ) 方法，可以加载需要的内置模块，用户自定义模块，第三方模块进行使用。

![image-20230318164712087](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230318164712087.png)

注意：使用require ( )方法加载其它模块时，会执行被加载模块中的代码。

#### 2.Node.js中的模块作用域

和函数作用域类似，在自定义模块中定义的变量，方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做模块作用域。![image-20230318165816790](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230318165816790.png)

![image-20230318170326865](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230318170326865.png)

![image-20230318170206700](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230318170206700.png)

![image-20230318171157684](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230318171157684.png)

![image-20230318171407467](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230318171407467.png)

##### 注意：require ( )模块时，得到的永远是module.exports指向的对象

#### 3.npm与包

Node.js中的第三方模块又叫做包。由于Node.js的内置模块仅提供了一些底层的API，导致在基于内置模块进行项目开发时效率很低。包是基于内置模块封装出来的，提供了更高级，更方便的API，极大的提高了开发效率。

![image-20230319083810923](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319083810923.png)

![image-20230319084942228](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319084942228.png)

![image-20230319085337984](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319085337984.png)

![image-20230319085655692](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319085655692.png)

![image-20230319085829598](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319085829598.png)

![image-20230319085923010](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319085923010.png)

![image-20230319093843117](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319093843117.png)

![image-20230319094709311](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319094709311.png)

##### 包的分类

使用npm包管理工具下载的包，共分为两大类：项目包，全局包

##### 	1.项目包（node_modules目录中的包）

​		开发依赖包（被记录到devDependencies节点中的包，只在开发期间会用到）

​		核心依赖包（被记录到dependencies节点中的包，在开发期间和项目上线之后都会用到）

![image-20230319095542344](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319095542344.png)

##### 	2.全局包（在执行npm install命令时，如果提供了 -g 参数，则会把包安装为全局包）

![image-20230319095829754](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319095829754.png)

![image-20230319095924835](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319095924835.png)

![image-20230319100535895](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319100535895.png)

#### 4.模块的加载机制

##### 优先从缓存中加载

模块在第一次加载后会被缓存。这也意味着多次调用require ( )不会导致模块的代码被执行多次。

##### 内置模块的加载机制

内置模块是由Node.js官方提供的模块，内置模块的加载优先级最高。

##### 自定义模块的加载机制

使用require ( )加载自定义模块时，必须指定以 ./或 ../开头的路径标识符。

![image-20230319154843510](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319154843510.png)

##### 第三方模块的加载机制

如果传递给require ( )的模块标识符不是一个内置模块，也没有以‘ ./ ’ 或‘ ../ ’开头，则Node.js会从当前模块的父目录开始，尝试从/node_modules文件夹中加载第三方模块

##### 目录作为模块

![image-20230319160158741](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319160158741.png)



## Express

Express是基于Node.js平台，快速、开放、极简的Web开发框架。

本质上是一个npm上的第三方包，提供了快速创建Web服务器的便捷方法。

![image-20230319161329336](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319161329336.png)

##### Web网站服务器：专门对外提供Web网页资源的服务器。

##### API接口服务器：专门对外提供API接口的服务器。

使用Express，我们可以方便、快捷的创建Web网站的服务器或API接口的服务器。

#### 1.监听GET请求

![image-20230319162237854](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319162237854.png)

#### 2.监听POST请求

![image-20230319162356971](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319162356971.png)

#### 3.把内容响应给客户端

![image-20230319162517343](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319162517343.png)

#### 4.获取URL中携带的查询参数

![image-20230319170716008](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319170716008.png)

#### 5.获取URL中的动态参数

![image-20230319174927736](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319174927736.png)

#### 6.托管静态资源

##### express.static ( )

![image-20230319181228372](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319181228372.png)

注意：Express在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录不会出现在URL中

##### 如果要托管多个静态资源目录，请多次调用express.static ( )函数

![image-20230319192548238](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319192548238.png)

##### 挂载路径前缀

![image-20230319194150980](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319194150980.png)



## Express路由

广义上来讲，路由就是映射关系。在Express中，路由指的是客户端的请求与服务器处理函数之间的映射关系。

Express中的路由分3部分组成，分别是请求的类型，请求的URL地址，处理函数

![image-20230319194848140](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319194848140.png)

##### 路由的匹配过程

每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。

在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的URL同时匹配成功，则Express会将这次请求，转交给对应的function函数进行处理。

![image-20230319195303542](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319195303542.png)

![image-20230319195508858](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319195508858.png)

##### 模块化路由

为了方便对路由进行模块化的管理，Express不建议将路由直接挂载到app上，而是推荐将路由抽离为单独的模块。

​	1.创建路由模块对应的 .js 文件

​	2.调用express.Router ( )函数创建路由对象

​	3.向路由对象上挂载具体的路由

​	4.使用module.exports向外共享路由对象

​	5.使用app.use ( )函数注册路由模块

![image-20230319200511940](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319200511940.png)

##### 注册路由模块

![image-20230319202356542](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319202356542.png)

##### 为路由模块添加前缀

![image-20230319203239732](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319203239732.png)



# Express中间件

中间件 ( Middleware )，特指业务流程的中间处理环节

#### Express中间件的调用流程

当一个请求到达Express的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

![image-20230319203807019](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319203807019.png)

#### Express中间件的格式

Express的中间件，本质上就是一个function处理函数

![image-20230319204012427](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319204012427.png)

注意：中间件函数的形参列表中，必须包含next参数。而路由处理函数中只包含req和res。

#### next函数的作用

next函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

#### 定义中间件函数

![image-20230319205048395](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319205048395.png)

#### 全局生效的中间件

客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。

通过调用app.use ( 中间件函数 )，即可定义一个全局生效的中间件

![image-20230319205854272](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319205854272.png)

#### 定义全局中间件的简化形式

![image-20230319210654195](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319210654195.png)

#### 中间件的作用

多个中间件之间，共享同一份req 和 res。基于这样的特性，我们可以在上游的中间件中，统一为req或res对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

#### 定义多个全局中间件

![image-20230319213254917](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319213254917.png)

#### 局部生效的中间件

![image-20230319213615089](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230319213615089.png)

#### 定义多个局部中间件

![image-20230321083809375](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321083809375.png)

##### 注意： **![image-20230321085942080](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321085942080.png)**

#### 中间件的分类

![image-20230321090125891](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321090125891.png)



##### 	1.应用级别的中间件

![image-20230321090227716](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321090227716.png)

##### 	2，路由级别的中间件

![image-20230321090408551](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321090408551.png)

##### 	3.错误级别的中间件

![image-20230321090622785](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321090622785.png)

​	注意：错误级别的中间件，必须注册在所有路由之后

##### 	4.Express内置的中间件

![image-20230321092545317](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321092545317.png)

![image-20230321092701442](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321092701442.png)

![image-20230321093156281](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321093156281.png)

​	在服务端，可以通过req.body来获取JSON格式的表单数据和url-encoded格式的数据

​	如果没有配置任何解析表单数据的中间件，则req.body默认等于undefined

##### 	5.第三方的中间件

![image-20230321104429726](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321104429726.png)

![image-20230321104834975](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321104834975.png)

​	注意：Express内置的express.urlencoded中间件，就是基于body-parser这个第三方中间件进一步封装出来的

#### 自定义中间件

![image-20230321105447488](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321105447488.png)

##### 监听req的data事件

在中间件中，需要监听req对象的data事件，来获取客户端发送服务端的数据。

如果数据量比较大，无法一次性发送完毕，则客户端会把数据切割后，分批发送到服务器。所以data事件可能会触发多次，每一次触发data事件时，获取到数据只是完整数据的一部分，需要手动对接收到的数据进行拼接。

![image-20230321110900809](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321110900809.png)

##### 使用querystring模块解析请求体数据

Node.js内置了一个querystring模块，专门用来处理查询字符串。通过这个模块提供的parse ( )函数，可以轻松把查询字符串，解析成对象的格式

![image-20230321113000110](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321113000110.png)

##### 将解析出来的数据对象挂载为req.body

上游的中间件和下游的中间件及路由之间，共享同一份req和res。因此，我们可以将解析出来的数据，挂载为req的自定义属性，命名为req.body，供下游使用。

![image-20230321115450710](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321115450710.png)

##### 将自定义中间件封装为模块

![image-20230321120932061](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321120932061.png)



## 使用Express写接口

#### 创建API路由模块

![image-20230321144216530](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321144216530.png)

#### CORS跨域资源共享

##### 1.接口的跨域问题

解决接口跨域问题的方案主要有两种：

​	CORS（主流的解决方案）
​	JSONP（有缺陷的解决方案：只支持GET请求）

##### 2.使用CORS中间件解决跨域问题

cors是Express的一个第三方中间件。通过安装和配置cors中间件，可以很方便地解决跨域问题

##### 3.什么是CORS

CORS（Cross-Origin Resource Sharing ，跨域资源共享）由一系列HTTP响应头组成，这些HTTP响应头决定浏览器是否阻止前端JS代码跨域获取资源。

浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了CORS相关的HTTP响应头，就可以解除浏览器的跨域访问限制。

##### 4.CORS的注意事项

![image-20230321171532223](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321171532223.png)

##### 5.CORS响应头部-Access-Control-Allow-Origin

![image-20230321171905583](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321171905583.png)

##### 6.CORS响应头部-Access-Control-Allow-Headers

![image-20230321172113445](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321172113445.png)

##### 7.CORS响应头部-Access-Control-Allow-Methods

![image-20230321172339144](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321172339144.png)

##### 8.CORS请求的分类

客户端在请求CORS接口时，根据请求方式和请求头的不同，可以将CORS的请求分为两大类

​	简单请求

![image-20230321172648895](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321172648895.png)

​	预检请求

![image-20230321172734414](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321172734414.png)

​	在浏览器与服务器正式通信之前，浏览器会先发送OPTION请求进行预检，以获知服务器是否允许该实际请求，所以这一次的OPTION请求称为“预检请求”。服务器成功响应预检请求后，才会发生真正的请求，并且携带真实数据。

##### 9.简单请求与预检请求的区别

简单请求的特点：客户端与服务器之间只会发生一次请求。

预检请求的特点：客户端与服务器之间会发生两次请求，OPTION预检请求成功之后，才会发起真正的请求。

#### JSONP接口

浏览器端通过< script >标签的src属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做JSONP

##### JSONP不属于真正的AJAX请求，因为它没有使用XMLHttpRequest这个对象

##### JSONP仅支持GET请求，不支持POST，PUT，DELETE等请求



##### 创建JSONP接口的注意事项

如果项目中已经配置了CORS跨域资源共享，为了防止冲突，必须在配置CORS中间件之前声明JSONP的接口，否则JSONP接口会被处理成开启了CORS的接口

![image-20230321200027297](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321200027297.png)

##### 实现JSONP接口的步骤

获取客户端发送过来的回调函数的名字

得到要通过JSONP形式发送给客户端的数据

根据前两步得到的数据，拼接出一个函数调用的字符串

把上一步拼接得到的字符串，响应给客户端的< script >标签进行解析执行

![image-20230321200750967](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321200750967.png)

##### 在网页中使用jQuery发起JSONP请求

调用$.ajax ( )函数，提供JSONP的配置选项，从而发起JSONP请求

![image-20230321211257241](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230321211257241.png)



## 数据库与身份认证

CREATE SCHEMA `new_schema` ;

CREATE TABLE `new_schema`.`user` (
  `id` INT NOT NULL,
  `usename` VARCHAR(45) NULL,
  `password` VARCHAR(45) NULL,
  `status` TINYINT(1) NULL COMMENT '用户的状态码，是一个布尔值\n0表示用户状态正常\n1表示用户被禁用',
  PRIMARY KEY (`id`));

![image-20230322193826214](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230322193826214.png)







# Koa2

lsof  -i:3000 查看3000端口号

kill  -9 删除进程

## app.context

`app.context`是创建`ctx`的原型。您可以通过编辑`app.context`向`ctx`添加其他属性。这对于向`ctx`添加属性或方法非常有用，以在整个应用程序中使用，这些属性或方法可能更高性能（没有中间件）和/或更容易（更少`require()`），而牺牲了更多地依赖`ctx`，这可以被认为是一种反模式。

例如，要从`ctx`向数据库添加引用：

```js
app.context.db = db();

app.use(async ctx => {
  console.log(ctx.db);
});
```

笔记：

- `ctx`上的许多属性都是使用getter、setter和`Object.defineProperty()`定义的。您只能通过在`app.context`上使用`Object.defineProperty()`编辑这些属性（不推荐）。请参阅https://github.com/koajs/koa/issues/652。
- 安装的应用程序目前使用其父母的`ctx`和设置。因此，挂载的应用程序实际上只是中间件组。



## 上下文CTX

Koa Context将节点的`request`和`response`对象封装成一个对象，为编写Web应用程序和API提供了许多有用的方法。这些操作在HTTP服务器开发中经常使用，以至于它们被添加到此级别，而不是更高级别的框架，这将迫使中间件重新实现此常见功能。

*每个*请求都会创建`Context`，并在中间件中作为接收器或thectx标识符引用，如以下片段所示：

```js
app.use(async ctx => {
  ctx; // is the Context
  ctx.request; // is a Koa Request
  ctx.response; // is a Koa Response
});
```

为了方便起见，许多上下文的访问器和方法只是委托给它们的“ctx.request”或“ctx.response”等价物，并且在其他方面是相同的。 例如，`ctx.type` 和 `ctx.length` 委托给 `response` 对象，`ctx.path` 和 `ctx.method` 委托给 `request`。



## 静态资源托管

koa-static



## Koa中的中间件执行栈结构

先进后出































































































































































































