# WebPack

##### 安装webpack

npm install webpack webpack-cli -d

npm install webpack-dev-server



##### 使用HtmlWebpackPlugin

![image-20230601091650025](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601091650025.png)



##### 使用source map

![image-20230601093542234](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601093542234.png)



##### 使用watch mode（观察模式）

![image-20230601094306485](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601094306485.png)



##### 使用webpack-dev-server

![image-20230601094543263](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601094543263.png)



##### Resource资源

![image-20230601095130426](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601095130426.png)



##### inline资源

![image-20230601101113061](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601101113061.png)



##### source资源

![image-20230601101402861](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601101402861.png)



##### 通用资源类型

![image-20230601102027077](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601102027077.png)



## loader

##### 加载CSS

![image-20230601111802999](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601111802999.png)



#### 抽离和压缩CSS

![image-20230601114057139](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601114057139.png)

```js
//压缩CSS
const CssMinimizerWebpackPlugin = require('css-minimizer-webpack-plugin')
```



#### CSS加载images图像

![image-20230601120748968](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601120748968.png)



#### CSS加载fonts字体

![image-20230601121356782](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601121356782.png)



#### 加载数据

![image-20230601143600090](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601143600090.png)



#### 自定义JSON模块parser

![image-20230601144053470](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601144053470.png)

![image-20230601144214542](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601144214542.png)





## babel-loader

![image-20230601150002922](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601150002922.png)



### 代码分离

![image-20230601151311699](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601151311699.png)

#### 1.入口起点

![image-20230601151408395](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601151408395.png)

#### 2.防止重复

![image-20230601152912287](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601152912287.png)

#### 3.动态导入

![image-20230601154722839](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601154722839.png)

#### 懒加载

![image-20230601160558761](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601160558761.png)

#### 预获取/预加载模块

![image-20230601161620821](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601161620821.png)

##### preload跟懒加载方法类似，推荐使用prefetch





## 缓存

![image-20230601162500487](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601162500487.png)

#### 缓存第三方库

![image-20230601164023185](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601164023185.png)

![image-20230601164752194](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601164752194.png)





#### 公共路径

![image-20230601165355492](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601165355492.png)



#### 环境变量

![image-20230601172733531](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601172733531.png)



#### 拆分配置文件

```js
npx webpack -c ./config/webpack.config.dev.js  //开发环境
npx webpack -c ./config/webpack.config.prod.js  //生产环境
```



#### npm脚本

![image-20230601175351226](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601175351226.png)



#### 提取公共配置

![image-20230601180352366](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601180352366.png)

#### 合并配置文件

![image-20230601181253198](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601181253198.png)

```js
const { merge } = require('webpack-merge')

const commomConfig = require('./webpack.config.common')
const productionConfig = require('./webpack.config.prod')
const developmentConfig = require('./webpack.config.dev')

module.exports = (env) => {
    switch(true){
        case env.development:
            return merge(commomConfig, developmentConfig)
        
        case env.production:
            return merge(commomConfig, productionConfig)

        default: 
            return new Error('No matching configuration was found')
    }
}
```





### source-map

![image-20230601184125651](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601184125651.png)

![image-20230601194811821](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601194811821.png)



#### devServer

![image-20230601214952551](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230601214952551.png)

##### 添加响应头

![image-20230602001851394](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602001851394.png)

##### 开启代理

![image-20230602002133063](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602002133063.png)

##### https

![image-20230602004444285](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602004444285.png)

##### historyApiFallback

![image-20230602005043405](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602005043405.png)

##### 开发服务器主机

![image-20230602005409042](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602005409042.png)

##### 模块热替换与热加载

![image-20230602005510140](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602005510140.png)

![image-20230602005553679](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602005553679.png)

#### eslint

![image-20230602101033611](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602101033611.png)

##### 结合webpack使用

![image-20230602102912034](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602102912034.png)

#### Git-hooks与husky

![image-20230602103756857](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602103756857.png)





## 模块与依赖

![image-20230602113506458](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602113506458.png)

#### 模块解析（resolve)

![image-20230602113545961](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602113545961.png)

#### 外部拓展（Externals)

![image-20230602115314150](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602115314150.png)

```js
 /* 导入外部拓展的方式 */
  externalsType: 'script',

  /* 配置外部扩展模块 */
  externals: {
    jquery: [
  'https://cdn.bootcdn.net/ajax/libs/jquery/3.6.4/jquery.js',
      'jQuery',
    ],
  },
```

#### 依赖图（dependency graph)

![image-20230602141600933](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602141600933.png)



#### PostCSS与CSS模块

![image-20230602143141027](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602143141027.png)

#### 部分开启CSS模块

![image-20230602150507879](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602150507879.png)

![image-20230602150636018](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602150636018.png)



## Web Works

##### 定义一个works

![image-20230602150917876](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602150917876.png)

#### TypeScript

![image-20230602160108864](/Users/houleidai.jqlai/Library/Application Support/typora-user-images/image-20230602160108864.png)























































































































































































































































