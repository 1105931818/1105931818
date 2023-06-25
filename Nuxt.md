# Nuxt.js



## 一、客户端和服务器渲染

#### 1.客户端渲染

前端的JS代码都是在浏览器中运行，所以消耗的是客户端的CPU和内存等资源，减轻了服务器的压力。

缺点是，页面中没有初始数据（查看页面源代码可以看到并没有数据），所以不利于SEO优化。当页面源代码没有数据，百度等网站抓取到的都是没有数据的空页面。

#### 2.什么是SEO

SEO（搜索引擎优化）：让网站，在百度，谷歌等搜索引擎里搜索排名靠前

搜索引擎会从每个网站的页面中抓取核心数据到自己的数据库中，然后当有用户在这些网站上搜索一个关键字，会通过抓取网页的内容和关键字匹配，匹配度好的排在前面。

##### SEO原理：

​	搜索引擎通过爬虫来抓取每个页面的数据，但是抓取时页面并不会执行JS，所以搜索引擎抓取不到任何数据，无法通过搜索引擎搜索出来。

在使用Vue开发项目时，要解决SEO问题，就要使用SSR（服务器端渲染）

#### 3.服务器端渲染（SSR）

代码在服务器端运行，把运行结果返回给前端，前端源代码里面可以查看到数据

![image-20230529172614106](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529172614106.png)





## 二、Nuxt脚手架

#### 1.安装

```js
npx create-nuxt-app '项目名'
或者
yarn create nuxt-app '项目名'
```



#### 2.脚手架项目结构

![image-20230529175117082](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529175117082.png)



#### 3.nuxt脚手架项目

##### 1.components目录下的组件，在pages目录中的页面组件中直接使用即可，项目通过在nuxt.config.js中配置

```js
components: true  //自动在页面组件中引入组件
```

##### 2.nuxt中每个页面都由三个层级的文件组成

（1）布局文件（根组件）：保存在layouts目录中，所有的页面都是布局文件中的子组件

（2）页面组件（页面）：保存在pages目录中，一个文件就是一个路由页面

（3）组件文件（组件）：保存在components中，在每个页面中使用的组件

所有的页面都是由布局文件+页面文件组成，页面文件中还可以有多个组件文件。

##### 3.布局文件

（1）默认是default.vue，它是项目中所有页面的根组件

（2）自定义布局文件，在layouts目录下，创建

（3）在页面文件中使用时，通过 layout: '自定义文件名称 '

（4）布局文件作用：网站通用布局结构

4.error组件

定义在layouts目录中，路由找不到时显示，error组件为页面组件，继承根组件布局，也可以通过 layout: '自定义文件名称 '指定自定义布局





## 三、路由

Nuxt中已经内置了vue-router组件，直接使用即可，不需要写任何代码

Nuxt中不需要配置路由，Nuxt会根据pages目录中的文件结构自动生成路由配置，pages目录下的文件的文件名即为路由名

#### 1.路由切换激活类名

```js
<nuxt-link to="/about">/About</nuxt-link>
```



class： Nuxt-link-active 模糊匹配

class： Nuxt-link-exact-active 精确匹配

#### 2.路径和文件的关系

<img src="/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529202909358.png" alt="image-20230529202909358" style="zoom:200%;" />

#### 3.路由参数

![image-20230529213208941](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529213208941.png)

![image-20230529213122189](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230529213122189.png)





## 四、asyncData

#### 1.Next.js扩展了Vue.js，增加了一个叫asyncData的方法，可以在设置组件的数据之前能异步获取或处理函数。

asyncData可以在服务器或路由更新之前被调用

​	asyncData默认在服务器渲染

​	asyncData在当前所在页面刷新在服务器渲染

​	asyncData在路由跳转时在客户端渲染

​	asyncData返回到数据最终会和data返回的数据合并到一起，供页面使用

##### 注意：

##### 	1.要对渲染环境进行判断，服务器无法进行对浏览器的一些操作。使用process.serve / process.static进行判断，true为服务端，false为客户端

##### 	2.asyncData只能使用在页面组件

##### 	3.asyncData参数为一个对象：{isDev, route, store, env, params, query, req, res, redirect, error}

##### 4.由于asyncData方法是在组件 **初始化** 前被调用的，所以在方法内是没有办法通过 this 来引用组件的实例对象。



#### 2.asyncData发送异步请求

```js
async asyncData() {
    const {data: {data: topics}} = await axios.get('https://cnodejs.org/api/v1/topics')

    return {
      topics
    }
  }


asyncData() {
  	return axios.get('https://cnodejs.org/api/v1/topics').then(res => topics: res.data.data)
  
}

```



![image-20230530102953214](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230530102953214.png)

![image-20230530112543754](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230530112543754.png)





## 五、中间件

每一次路由切换之前被执行，运行在客户端和服务端

#### 1.创建中间件

![image-20230530160702236](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230530160702236.png)

```js
// 全局注册中间件
  router: {
    middleware: '中间件名'
  }
```

```js
// 在布局文件或页面组件中，注册中间件（局部注册）
export default {
    middleware: '中间件名'
}
```

#### 2.中间件执行顺序

1.全局中间件

2.布局文件中间件

3.页面组件中间件





## 六、插件

插件是一个js文件，项目启动时时会在服务器和客户端都执行一遍，此时注意区分环境。路由切换时不会触发插件

![image-20230530163228367](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230530163228367.png)

#### 1.插件分类

##### 1.默认插件：客户端和服务器都会自动执行

```js
plugins: [
    '~/plugins/插件名'
  或者
  	{ src: '~/plugins/插件名', mode: 'both' }
],
```

##### 2.客户端插件：只在客户端自动执行的插件

在nuxt-config.js中配置

```js
//客户端插件
plugins: [
    { src: '~/plugins/插件名', mode: 'client' }
],
```

##### 3.服务端插件：只在服务端自动执行的插件

在nuxt-config.js中配置

```js
//服务端插件
plugins: [
    { src: '~/plugins/插件名', mode: 'server' }
],
```

##### 或者通过设置插件文件的扩展名xxx .client.js` 或 `xxx .server.js应用，该文件将自动包含在相应客户端或者服务端上。





## 七、Head配置

在开发网站时，为了提升SEO优化，除了SSR，还可以设置网页TDK（Title   Description  Keywords）

##### 在nuxt.config.js中配置TDK

```js
head: {
    title: '京东',
    htmlAttrs: {
      lang: 'en'
    },
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      { hid: 'description', name: 'description', content: '网上购物商城' },
      { name: 'Keywords', content: '手机,数码' },
      { name: 'format-detection', content: 'telephone=no' }
    ],
    link: [
      { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }
    ]
  },
```

##### 在页面中配置TDK

```js
 export default {
    data() {
      return {
        title: 'Hello World!'
      }
    },
    head() {
      return {
        title: this.title,
        meta: [
          {
            hid: 'description',  //覆盖全局配置
            name: 'description',
            content: 'My custom description'
          }
        ]
      }
    }
  }
```





## 八、fetch

fetch 方法用于在渲染页面前填充应用的状态树（store）数据， 与 asyncData 方法类似，不同的是它不会设置组件的数据。

如果页面组件设置了 `fetch` 方法，它会在组件每次加载前被调用（在服务端或切换至目标路由之前）。

Fetch 钩子函数是在服务器端组件实例化后调用的，这使得 fetch 函数可以通过 `this` 来引用组件的实例对象。此时不能传参

通过 fetch 函数我们可以在任何 Vue 组件中预取异步数据，所有的 Vue 组件都可以使用 fetch 函数。比如 /layouts 和 /components 目录下的 vue 组件。



## 九、生命周期

![image-20230531110227062](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531110227062.png)

##### beforeCreated, created在服务器或路由更新时，会在服务器和客户端都执行一次





## nginx

查看nginx的配置信息: brew info nginx

![image-20230531151859795](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230531151859795.png)

#### 启动nginx

open /opt/homebrew/Cellar/nginx/



```js
 server {
        listen       8080;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   静态网站资源目录;
            index  index.html index.htm;
        }
```





## 十、nuxtServerInit

解决页面刷新，vuex数据清空问题

##### 在store/index.js中的actions配置项中使用，只会运行在服务端，在服务器启动或者刷新运行一次，可以通过相关参数读取到请求对象

```js
export const actions = {
    nuxtServerInit({commit}, {req}){
        const server = process.server ? '服务器' : '客户端'
        console.log('nuxtInitServer', server)
        commit('uesr/updateAuth', req.headers.cookie)

        console.log(req.headers.cookie)
    }
}
```





## TypeScript

##### 使用类创建组件

安装`vue-property-decorator `     `vue-class-component`





























































