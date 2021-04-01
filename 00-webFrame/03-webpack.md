# webpack学习

## REM

rem  (root em, 根em)，它是  CSS3  的新字体单位，是一个相对单位，看它名字的写法，就知道它的相对于根元素字体大小。

- 假如根元素的字体大小为  16px，这个  16px  就是  `1rem`。如若它的一个后代元素的字体大小为  32px  时，此时，我们不仅可以给这个元素设置`font-size: 32px`  还可以写成  `font-size: 2rem`。
- 在后续的使用中，不仅仅只用在字体中，元素的宽度也可以使用  `rem`  这个相对单位。例如可以给一个元素的宽度设置为`width: 2rem`。还是，如果根元素字体大小为  16px，那么这个元素的宽度就是  32px。
- 目前，除了  IE8  以及更早的浏览器，所有浏览器都可以使用这个单位。
- 在需要适配各种移动端设备时，推荐使用  rem  单位代替  px。

 

## webpack

### 网页中常见的静态资源有哪些？

- JS
  + .js .jsx .coffee .ts(TypeScript 类 C#)

- CSS
  + .css .less .sass .scss

- Images
  + .jpg .png .gif .bmp .svg

- 字体文件
  + .svg .ttf .eot .woff .woff2

- 模板文件
  + .ejs .jade .vue

### 网页中引入的静态资源多了会有什么问题？

- 加载慢：当静态资源多了，会发起很多的二次请求，这时候，我们网页的加载速度就慢了
- 会出现很多静态资源的前后依赖关系

### 如何解决上述问题

- 把图片合并成精灵图、把  CSS   或  JS  合并压缩一下
- 把图片转换为  base64  编码格式
- **使用  webpack  去解决静态资源的依赖问题**

### 什么是webpack

webpack 是前端的一个项目构建工具，它是基于 Node.js 开发出来的一个前端工具；借助于webpack这个前端自动化构建工具，可以完美实现资源的合并、打包、压缩等诸多功能。

- 工作方式：把一个项目当做整体，通过给定的主文件（index.js），webpack从这个文件，找到项目的所有依赖文件，使用合适的loader处理，最后打包成一个浏览器可以识别的JavaScript文件。通常这个 js 文件叫做  `bundle.js`

**可以做什么**

- 处理文件之间的依赖关系
- 解决  js  兼容问题，能够把  ES6  语法转换成低级别的语法，供浏览器识别
- 控制资源的处理方式。通过第三方  loader  和  plugin，可以对代码进行压缩以及 css  预处理
- 代码拆分异步加载
- 稳定生产部署，根据开发环境和生产环境自定义打包方式

![](D:\05_note\studyNotes\00-images\webpack.png)

## webpack中的基本概念

参照：[概念](https://www.webpackjs.com/concepts/)

- 入口(entry)

- 出口(output)
- 解析器(loader)
- 插件(plugin)
- 模式(mode)

## webpack的使用

### 安装

webpack最新版本已经是4.43.0，想要使用最新版本，需要同时安装一下两个包

```shell
npm i webpack -D
npm i webpack-cli -D
```

为了工作方便，我们可以选择全局安装

```shell
npm i -g webpack
npm i -g webpack-cli
```

### mode

通过选择 `development` 或 `production` 之中的一个，来设置 `mode` 参数，你可以启用相应模式下的 webpack 内置的优化

```js
module.exports = {
  mode: 'production'
}
```

### js入口和出口

在项目中创建一个名为  `webpack.config.js`  文件，`webpack.comfig.js`  文件与  `index.js`  文件同级，在同一目录下

#### 单出入口文件打包

详情请参照：[单出口打包配置](https://www.webpackjs.com/configuration/output/#output-filename)

```javascript
const path = require('path')

module.exports = {
    // 配置项目入口文件
    entry: path.join(__dirname, './src/index.js') // index.js就是项目初始化的那个index文件
    // 项目打包出口
    output: {
        path: path.join(__dirname, './dist'),  // 项目输出路径
        filename: 'bundle.js'                  // 输出js文件名称
	}
}
```

#### 多出入口文件打包  

详情请参照：[多出口打包配置](https://www.webpackjs.com/configuration/output/#output-filename)

```javascript
const path = require('path')

module.exports = {
    // 配置多项目入口文件
    entry: {
        fileNameOne: './index_dev.js',
        fileNameTwo: './index_prod'
    },
    output: {
        path: path.join(__dirname, './dist')
        filename: '[name].js'
    }
}
```

### html的入口和出口

想要使用  `index.html`  作为模板文件，需要下载一个插件，这里用到了一个插件，事实上，webpack  中为开发者准备了许多的插件，详情请参考：[webpack中的所有插件](https://www.webpackjs.com/plugins/hot-module-replacement-plugin/)

```shell
npm i html-webpack-plugin -D
```

下面是配置：

```javascript
// 导入 在内存中生成页面的webpack插件
const htmlWebpackPlugin = require('html-webpack-plugin')

// 在module.exports配置plugins节点

module.exports = {
    
    plugins: [ // 插件配置节点
    new htmlWebpackPlugin({ // 创建一个 htmlWebpackPlugin 的实例对象
      template: path.join(__dirname, './src/index.html'), // 指定模板页面路径
      filename: 'index.html' // 指定内存中生成的HTMl文件名称
    })
  ],
}
```

### loader

[webpack中的所有loader](https://www.webpackjs.com/loaders/)

安装

```shell
npm i style-loader css-loader -D
npm i less-loader less -D
npm i sass-loader node-sass sass fibers -D
npm i url-loader file-loader -D

npm i babel-core babel-loader babel-plugin-transform-runtime -D   // 这里的babel-loader建议用7.1.5版本
npm i babel-preset-env babel-preset-stage-0 -D
```

在  module.exports  中的  module  节点中配置loader

```javascript
// test 后边是正则表达式，表示以什么后缀名结尾的文件
// use 后边的安装的各种loader，用来解析执行前边test文件，执行顺序为，最后一个loader执行完毕，依次交给前一个loader解析执行   

module.exports = {
     module: { // 用来配置 非JS文件对应的loader的
        rules: [ // 就是这些 非 JS 文件 和 loader 之间的对应关系
          { test: /\.css$/, use: ['style-loader', 'css-loader'] }, // 创建处理 css 文件的 loader 匹配规则
          { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] }, // 配置处理less文件的规则
          { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }, // 配置 处理 scss 文件的规则
          { test: /\.jpg|png|gif|bmp$/, use: 'url-loader' }, // 配置 处理 样式表中图片的 loader规则
          { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ }, // 添加转换JS文件的loader，其中，必须把 node_modules 目录设置为 排除项，这样，在打包的时候，会忽略node_modules 目录下的所有JS文件；否则项目运行不起来！
          { test: /\.ttf|woff|woff2|eot|svg$/, use: 'url-loader' }, // 处理 样式中字体文件路径的问题
        ]
  },
}
```

另外，在使用  babel  时，需要在与  webpack.config.js  同级目录下创建  `.babelrc`  文件，具体配置如下，详情请参考[babel官网](https://www.babeljs.cn/docs/configuration)

```js
{
  "plugins": ["transform-runtime"],
  "presets": ["env", "stage-0"]
}
```

### resolve

alias节点配置，详情请参照：[alias配置](https://www.webpackjs.com/configuration/resolve/#resolve-alias)

```javascript
// resolve下的alias节点表示，遇到vue结尾的文件，用vue包中dist目录下的vue.js解析执行

module.exports = {
    
    resolve: {
        alias: {
            'vue$': 'vue/dist/vue.js'
        }
    }
}
```

### 根据不同环境配置开发环境和生产环境

externals配置，详情请参照：[externals配置](https://www.webpackjs.com/configuration/externals/)

```javascript
module.exports = {
    // 生产模式
    config.when(process.env.NODE_ENV === 'production', config => {
    	config.entry('app').clear().add('./src/index_prod.js')

		config.set('externals', {
            axios: 'axios'
        })
	})
    // 开发模式
    config.when(process.env.NODE_ENV === 'development', config => {
        config.entry('app').clear().add('./src/index_dev.js')
    })
}


// 生产模式中配置的 externals 节点表示，用到axios这个包时，不直接加载这个包，而是直接去window全局对象中寻找，这个时候我们往往会用CDN的资源直接引入到html文件中。这是一个优化，避免把所有的第三方资源都打包到一起，而导致文件体积过大的问题
```

### 前端解决跨域问题之配置代理服务器

在  module.exports 中配置  devServer  节点，详情请参照：[配置代理服务器](https://www.webpackjs.com/configuration/dev-server/#devserver-proxy)

```javascript
// 当我们以 /api开头 发起网络请求时，代理会去请求target目标网址

module.exports = {
    devServer: {
        proxy: {
            '/api': {
                target: 'http://127.0.0.1:3000',
                pathRewrite: {'^api': ''}
            }
        }
    }
}
```

### 启用热更新

详情请参照：[devServe的相关配置](https://www.webpackjs.com/configuration/dev-server/)

第一步：安装包  `npm i webpack-dev-server -D`

第二步：配置  package.json  文件

```json
"scripts": {
    "dev": "webpack-dev-server"
}
```

第三步：在终端中运行  `npm run dev`

启用热更新有两种方式

**方式一：**在  webpack.config.js  文件中配置以下内容

```javascript
const webpack = require('webpack')

module.exports = {
    plugins: [
        new webpack.HotModuleReplacementPlugin()
    ],
    devServer: { // webpack-dev-server运行时候的指令， 这种配置方式和 -- 指令，只能二选一
    //  --open --port 3000 --host 127.0.0.1 --hot
    open: true, // 自动打开浏览器
    port: 3000, // 指定端口号
    host: '127.0.0.1', // 指定Ip地址
    hot: true // 启用热更新, 这里的 hot 指令，需要配合 一个 热更新的 webpack 插件才能正常使用
  }
}
```

**方式二：**在  package.json文件中配置以下内容

```json
"scripts:" {
    "dev": "webpack-dev-server --open --port 3000 --host 127.0.0.1 --hot"
}
```

## loader 和 plugin

### loader

用于对模块源码的转换，loader描述了webpack如何处理非javascript模块，并且在build中引入这些依赖。

loader是文件加载器，能够加载资源文件，并对这些文件进行一些处理，诸如编译、压缩等，最终一起打包到指定的文件中。

- 处理一个文件可以使用多个loader，loader的执行顺序和配置中的顺序是相反的，即最后一个loader最先执行，第一个loader最后执行
- 第一个执行的loader接收源文件内容作为参数，其它loader接收前一个执行的loader的返回值作为参数，最后执行的loader会返回此模块的JavaScript源码

### plugin

目的在于解决loader无法实现的其他事，从打包优化和压缩，到重新定义环境变量，功能强大到可以用来处理各种各样的任务。

- 在webpack运行的生命周期中会广播出许多事件，plugin可以监听这些事件，在合适的时机通过webpack提供的API改变输出果。

### loader 和 plugin的区别

- loader是一个转换器：将A文件进行编译形成B文件，这里操作的是文件，比如将 A.scss 转换为 A.css，是单纯的文件转换过程。
- plugin是一个插件扩展器：针对webpack打包的过程，它不直接操作文件，而是基于事件机制工作，会监听webpack打包过程中的某些事件钩子，执行任务。plugin 比loader 强大，通过plugin 可以访问 compliler和compilation过程，通过钩子拦截 webpack 的执行。

## webpack优化策略

weback资料第五章

### webpack4本身的优化

- V8 带来的优化(for of 替代 forEach、Map 和 Set 替代 Object、includes 替代 indexOf)
- 默认使用更快的 md4 hash 算法
- webpacks AST 可以直接从 loader 传递给 AST，减少解析时间
- 使用字符串方法替代正则表达式

### 速度优化

#### 速度分析

- 插件：speed-measure-webpack-plugin
- 作用：
  - 分析整个打包总耗时
  - 每个插件和loader的耗时情况

#### 解决方案

- 多进程/多实例:并行压缩
  - 方案1：使用 parallel-uglify-plugin 插件
  - 方案2：uglifyjs-webpack-plugin 开启 parallel 参数
  - 方案3：terser-webpack-plugin 开启 parallel 参数
- 分包
  - 使用 html-webpack-externals-plugin
  - 进一步分包：使用 DLLPlugin 进行分包，DllReferencePlugin 对 manifest.json 引用。思路：将 react、react-dom、redux、react-redux 基础包和业务基础包打包成一个文件
- 缓存
  - babel-loader 开启缓存
  - terser-webpack-plugin 开启缓存
  - 使用 cache-loader 或者 hard-source-webpack-plugin
- 缩小构建目标
  - 不解析 node_modules中的js，css等资源
- 减少文件搜索范围
  - 优化 resolve.modules 配置(减少模块搜索层级)
  - 优化 resolve.mainFields 配置
  - 优化 resolve.extensions 配置
  - 合理使用 alias

### 体积优化

#### 体积分析

- 插件：webpack-bundle-analyzer
- 作用
  - 依赖第三方模块文件大小
  - 业务组件代码大小

### 解决方案

- Scope Hoisting：作用域提升，webpack 会把引入的 js 文件“提升到”它的引入者顶部。ES6异步导入`import (../bundle.js);`，不回提升。
  - 插件：
  - 优点
    - 代码量明显减少
    - 内存占有量减少
    - 运行速度提升
- Tree-shaking：1 个模块可能有多个方法，只要其中的某个方法使用到了，则整个文件都会被打到 bundle 里面去，tree shaking 就是只把用到的方法打入 bundle ，没用到的方法会在 uglify 阶段被擦除掉。
  - 使用：webpack 默认支持，在 .babelrc 里设置 modules: false 即可 · production mode的情况下默认开启
  - 要求：必须是 ES6 的语法，CJS 的方式不支持要求：必须是 ES6 的语法，CJS 的方式不支持
  - 优点
    - tree shaking 就是只把用到的方法打入 bundle ，没用到的方法会在 uglify 阶段被擦除掉

- 公共资源分离
  - 插件：
  - 优点
    - 
- 图片压缩
  - 解析器： image-webpack-loader
  - 优点
    - 有很多定制选项
    - 可以引入更多第三方优化插件，例如pngquant
    - 可以处理多种图片格式
- 动态Polyfill：浏览器原生不支持es6，es7等新特性，可以用ployfill实现
  - 插件：
  - 优点
    - 浏览器兼容处理
  - 缺点
    - 包含所有补丁，不管项目是否用到，都全量引用
- 删除无用的CSS
  - 思路：PurifyCSS: 遍历代码，识别已经用到的 CSS class
  - uncss: HTML 需要通过 jsdom 加载，所有的样式通过PostCSS解析，通过 document.querySelector 来识别在 html 文件里面不存在的选择器
  - 插件：purgecss-webpack-plugin 和 mini-css-extract-plugin

