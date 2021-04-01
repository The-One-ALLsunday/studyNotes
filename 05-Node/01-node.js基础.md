# node.js基础

作者：Ryan Dahl

## 基本结构

```javascript
// 创建服务器

// 1、加载核心模块
var http = require('http')
var fs = require('fs')
var template = require('art-template')

// 2、创建服务器
var server = http.createServer()

// 3、注册request请求事件,响应客户端请求
server.on('request', function (req, res) {
    // 响应头 text/plain 普通文本  text/html html文本
    res.setHeader('Content-Type', 'text/plain; charset=utf-8')
    res.setHeader('Content-Type', 'image/jpeg')
    res.write('hello')
    res.write(' dengbo')
    // 响应要有结束
    res.end()
    
    // 使用fs文件操作核心模块
    fs.readFile(./路径，function (err, data) {
        if (err) {
            res.setHeader('Content-Type', 'text/plain; charset=utf-8')
            return res.end('文件读取失败，请稍后重试！')
        } else {
            res.setHeader('Content-Type', 'text/html; charset=utf-8')
            res.end(data)
        }
    })
    
})

// 4、绑定端口号，启动服务器
server.listen(3000, function () {
    console.log('服务器启动成功')
})
```

### require()作用：加载并执行文件中的代码；拿到被加载文件模块导出的接口对象

+ 相对路径的`./`不能省略

### exports默认是一个空对象

### **request**请求对象

+ 用来获取当前客户端的一些请求数据或者请求报文信息，例如请求路径
- `request.url`可以拿到用户请求的路由地址
- `requset.query`用来获取查询字符串数据
- `request.method` 用来获取当前请求方法

### **response**响应对象

+ 响应对象可以用来给客户端发送响应信息
+ `res.write('相应数据')`      可以写多次，但是写完一定要end
+ `res.end()` 结束响应
+ response响应的内容信息在浏览器中显示
+ 响应的内容只能是**二进制**数据或者**字符串**  需要用`.toString()`方法转换
  	+ 通常我们使用`res.end()`方法直接自结束响应内容，有两个**好处**
  	+ `res.end()`支持两种类型：**二进制数据**和**字符串**
  	+ 所以用了`res.end()`后通常不再需要自己转换为我们认识的字符串

## 为什么学习node.js

- 企业需求

  	+ 具有服务端开发经验更好
  	+ front-end
  	+ back-end
  	+ 全栈开发工程师
   + 基本的网站开发能力
     	* 服务端
          	* 前端
              	* 运维部署

  + 案例：多人社区

## node.js 是什么

- node.js是构建于Chrome V8引擎之上的一个JavaScript运行时环境
  	+ 不是一门语言
  	+ 不是库、不是框架
  	+ 简单说，node.js可以脱离浏览器解析执行JavaScript代码
  	+ 代码只是具有特定格式的字符串而已
  	+ 引擎认识代码，并且帮我们去解析执行代码
  	+ Google Chrome的V8引擎是目前公认的解析执行JavaScript代码最快的
  	+ node.js的作者把Google Chrome 中的V8引擎移植了出来，开发了一个独立的JavaScript运行时环境
- node.js使用事件驱动和非阻塞IO模型使它更轻量和高效
  	+ 事件驱动
  	+ 非阻塞I/O模型（异步）
  	+ 轻量和高效
- npm是世界上最大的开源库生态系统
  	
+ 绝大多数JavaScript相关包都存放在了npm上，这样做的目的是为了让开发人员更容易的装包
  	
 - 浏览器中的JavaScript

    + ECMAScript
      	* 基本的语法
      	* if
      	* var
      	* function
      	* Object
      	* Array
      	* String
      	* 。。。

   + BOM
   + DOM

- node.js中的JavaScript

  	+ 没有**BOM和DOM**
  	+ 只有ECMAScript
   + 在node这个JavaScript执行环境中为JavaScript提供了一些服务器级别的操作API
     	* 文件读写
          	* 网络服务的构建
              	* 网络通信
        	* http服务器
        	* 。。。
  + 核心模块
    * 文件操作模块 `fs`
    * 服务构建模块 `http`
    * 路径处理模块 `path`
    * 路径操作模块`url`
    * 操作系统模块 `os`
* 。。。
  + 第三方模块
      	+ art-template
  + 用户自定义模块   **js文件**
  + node中没有全局作用域，只有模块作用域

## node能做什么

- web服务器后台
- 命令行工具
  	+ git    C语言
  	+ npm    node开发
  	+ hexo   基于node开发
  	+ 。。。
- 游戏服务器 

## 能学到什么

- B/S编程模型
- 模块化编程
- node常用API
- 异步编程
  + 回调函数
  + Promise
  + async
  + generator
- Express  Web开发框架
- ECMAScript6
- 。。。

## 状态码

- 404 Not Found
- 302 临时重定向
- 301 永久重定向     浏览器会记住

## 什么是端口号

所有联网的程序都需要进行网络通信，计算机中只有一个物理网卡，而且同一个局域网中，网卡的地址必须是唯一的。网卡是通过唯一的**ip地址**来进行定位的。

- ip地址用来定位计算机
- 端口号用来定位具体的应用程序
- 所有需要联网通信的软件都必须具有端口号
- 端口号的范围是0-65536之间
- 在一台计算机中，同一个端口号在同一时间只能被一个应用程序占用

## 响应头目录

- [响应头查询](https://tool.oschina.net/commons)
- 不同的资源对应的  Content-Type 是不一样的
- 图片不需要指定编码
- **一般只为字符数据指定编码格式**

- `res.setHeader('Content-Type', 'text/plain; charset=utf-8')`
- `res.setHeader('Content-Type', 'text/html; charset=utf-8')`
- `res.setHeader('Content-Type', 'image/jpeg')`
- 。。。



## 代码无分号问题

**不能以`(`和`[`和`**开头

- 推荐书籍《编写可维护的JavaScript》

## 核心模块

### 文件操作--fs

- 读文件内容
  	+ `fs.readFile('./路径', function (err, data) {})`
- 读文件目录
  + `fs.readdir('./路径', function (err, files) {})`
    	* files是一个数组

### 路径操作模块--path

- path.basename
  + 获取一个路径下的文件名（默认包含扩展名）
- path.dirname
  + 获取一个路径中的目录部分
- path.extname
  + 获取一个路径下文件的扩展名
- path.parse
  + 把一个路径转化为对象
    * root
    * dir
    * base
    * ext
    * name
- path.join
  + 当时用路径拼接的时候，使用这个方法
- path.isAbsolute
  + 判断路径是否是绝对路径

### node中的其他成员

`~/dist/a.js`

在每个模块中，除了`require`、`exports`等模块相关API之外，还有两个特殊的成员

- `__dirname`        可以用来获取**当前文件模块**所属目录的绝对路径
  - 拿到的是`~/dist`
- `__filename`      可以用来获取**当前文件**的绝对路径
  - 包括文件本身
  - 拿到的是`~/dist/a.js`

## 客户端渲染和服务端渲染的区别

### 客户端渲染

- 至少请求**两次**
  	+ 第一次： 拿到的是页面字符串
    	  	+ 第二次： 拿到的是动态数据
  	+ 只有拿到页面字符串和动态数据才是完整的web页面
- **好处**
  + 速度快、用户体验好

### 服务端渲染

- 至少请求**一次**

  	+ 在服务端使用模板引擎

  + 服务端直接把**页面**和**数据**渲染好，直接发给客户端
  + 服务端渲染更快，但是如果全部由服务端来做，服务器压力会加大，因此速度可能会慢

- **好处**

  + 有利于 SEO 搜索引擎优化
  + 容易被爬虫抓取到

## node中的模块系统

​	使用node编写应用程序主要就是使用

- ECMAScript语法
- 核心模块
- 第三方模块
- 自己写的文件模块

### 什么是模块化

- 具有文件作用域
- 具有通信规则
  + 加载 `require`
  + 导出

### JavaScript模块化

在node的JavaScript还有一个重要的概念：模块系统

- node中的CommonJS
- 浏览器中的
  + AMD   require.js
  + CMD   sea.js
- ECMAScript 6    开始支持模块化     还没有被广泛使用
- 具有模块作用域
- 使用`require`方法来加载模块
- 使用`exports`接口对象来导出模块中的成员

### 加载`require`

语法

```javascript
var 自定义变量名称 = require('模块')
```

**两个作用**

- 执行被加载模块中的代码
- 得到被加载模块中的`exports`导出的接口对象

#### requrie加载规则

- 优先从缓存加载   避免重复加载，提高模块加载效率
- 判断模块标识符  `require('###')`  路径形式和非路径形式
  + 核心模块                         非路径
  + 第三方模块                     非路径
    * 以`art-template`为例
    * 首先，找到当前文件所属中的    **node_modules**目录
    * 然后，找到 node_modules目录中的   **第三方模块名字**  例如：art-template
    * 然后，再找 art-template 下边的 **package.json**
    * 然后，再找package.json 中的 **main** 属性   main属性记录了第三方模块的入口文件
    * **注意**如果第三方模块中没有package.json文件和main属性，则node会自动找该目录下的`index.js`文件，也就是说index.js会作为一个默认备选项。前提是第三方模块中没有package.json和main属性，才会加载index.js。否则，以package.json和main为准
    * 在如果既没有package.json和main和index.js，则会进入上一级的node_modules目录查找
    * 如果上一级还没有，则继续往上上一级查找
    * 直至当前磁盘根目录还找不到，最后会报错：can   not   find   module  xxx
    * 注意我们的项目中有且只有一个node_modules,并且放在根目录中
  + 自己写的文件模块          路径

### exports导出对象--多个成员

require只能得到exports想给他的成员  目的：防止变量命名冲突的问题

- node中是模块作用域，默认文件中所有成员只在当前文件模块有效
- 对于希望可以被其他模块访问的成员，我们就需要把这些公开的成员都挂载到`exports`接口对象上就可以了

- `exports`是一个对象，可以通过多次为这个对象添加成员的方式实现对外导出多个内部成员
- 想要使用`exports`导出的对象成员**必须使用`.`某个成员**

```javascript
// 有两个文件

// 第一个文件：main.js
var fooExports = require('./foo.js')  // 其中.js可以省略 fooExports是一个对象

// 使用foo.js中的add方法
fooExports.add(1, 2)

// 第二个文件：foo.js
var foo = 'bar'
function add(x, y) {
    return x + y
}
// exports的第一个成员
exports.add = add
// exports的第二个成员
exports.str = 'hello'
// exports的第三个成员
exports.foo = foo
```



### module.exports导出成员--单个成员

如果一个模块需要直接导出某个成员，而非挂载的方式，则必须使用`module.exports = add`的方式

有时候，对于一个模块，我们希望直接导出成员，直接使用成员

- 直接导出一个方法
- 直接导出一个字符串
- 。。。

```javascript
// 有两个文件

// 第一个文件 main.js
var fooExports = require('./foo')   // foo文件的后缀名可以省略


// 第二个文件 foo.js
var foo = 'hello node.js'

function add(x, y) {
    return x + y
}

// 直接导出add方法
module.exports = add
```

**以下情况会覆盖**----只会导出最后一个，后者会覆盖前者

```javascript
module.exports = 'hello'

module.exports = function (x, y) {
    return x + y
}
```

**注意**：module.exports也可以导出多个成员

```javascript
// 通过导出  对象  的方式导出多个成员
module.exports = {
    add: function () {},
    str: 'hello'
}
```

### exports为什么不能 等号（=） 赋值

在node中，每个模块都有一个自己的`module`对象，该`module`对象中，有一个成员叫`exports`,也是一个对象，是一个空对象。

在每个模块的最后有一句这样的代码`return module.exports`

谁`require`这个模块，谁就得到return的`module.exports`

```javascript
module = {
    exports: {
        
    }
}

// 在模块中还有这么一句代码   就是说 exports 等价于 module.exports   他们指向同一个对象
var exports = module.exports

return module.exports
```

**注意**

- 正常情况下导出成员需要这么写`module.exports.foo = 'hello'`
- 使用过程中，我们发现，每次导出接口成员的时候都通过  module.exports.xxx = xxx  的方式很麻烦，点儿的太多了
- 所以，node为了简化我们的操作，专门提供了一个变量`exports`   有隐含一句代码`exports = module.exports`

### exports和module.exports混用

任意一个重新赋值都会与另外一个断开联系

- 需要明白重新赋值会改变   **指向**   而   追加成员  不会改变指向

## npm

- node package manager
- npm是一个网站
- npm是一个命令行工具
  + 只要安装了node就可以使用npm了
- npm也有版本这个概念

```javascript
npm -v
```

- 升级npm：自己升级自己

```javascript
npm install --global npm
```

- 常用命令
  + npm init
    * npm init -y
  + npm install
  + npm install 包名
  + npm install 包名 -D         开发时依赖           下载并保存依赖项
  + npm install 包名 -S          运行时依赖           下载并保存依赖项
  + npm uninstall 包名          只删除，如果有依赖项依然会保存
  + npm uninstall 包名  --save     删除的同时也会把依赖项全部删除
    + 简写：npm un 包名 -S
  + npm --help    查看npm使用帮助
  + npm 命令 --help
    + 查看指定命令的使用帮助

## package.json

- 建议每一个项目都要有一个`package.json`文件（包描述文件，就像产品的说明书）
- 这个文件可以通过`npm init`初始化出来

## Express

作者：TJ

- 处理静态资源
- 模板引擎
- 中间件
- 基本路由
- Express API

原生`http`在某些方面表现不足以应对我们的开发需求，所以我们就需要使用框架来加快我们的开发效率，框架的目的就是提高效率，让我们的代码更高度统一

在node中，有很多开发框架，我们以`express`学习为主

- 封装的http

```javascript
// 1.引包
var express = require('express')
// 2.创建服务器
var app = express()

// 3.响应请求
app.get('/', function (req, res) {
    res.send('hello express!')
})
app.get('/about', function (req, res) {
    res.send('关于我！')
})

// 4.绑定端口号，开启服务器
app.listen(3000, function () {
    console.log('app is running atport 3000.')
})
```

### 在Express中获取表单get请求

Express内置了一个API，可以直接通过`req.query`来获取

```shell
req.query
```

### 在Express中获取表单post请求

在Express中没有内置获取表单post请求体的API，这里需要使用一个第三方包：`body-parser`

安装：

```shell
npm install body-parser --save
```

配置：

```javascript
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

// 配置body-parser,只要加入这个配置，则在req请求对象上会多出来一个属性：body
// 也就是说你可以直接通过 req.body 来获取表单post请求数据了
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.join())
```

使用：

```javascript
app.use(function (req,res) {
    res.setHeader('Content-Type', 'text/plain')
    res.write('you posted:\n')
    // 可以通过 req.body 来获取表单post请求体数据
    res.end(JSON.stringify(req.body, null, 2))
})
```

### Express中间件

- 中间件 middleware

**中间件**：用来处理http请求的一个具体环节（可能要执行某个具体的函数），中间件一般都是通过修改req或者res来为后续的处理函数提供便利使用

**中间件分类**：

- use(function (req, res), next { })   不关心请求方法和请求路径，没有具体的路由规则，任何请求都能进来
- use('请求路径', function (req, res, next) { })   不关心请求方法，只关心请求路径的中间件
- get('请求路径', function (req, res, next) { })     具体路由规则的中间件
- post('请求路径', function (req, res, next) {})    post  和  get    既包含请求方法和请求路径  
- **注意** 相同的请求方法相同的路径只响应第一次的

#### 全局统一处理错误的中间件

- 这个中间件必须有四个参数（err，req， res，next）

```javascript
next(err)

app.use((err, req, res, next) => {
    const err_log = `
===================================================
	错误名：${err.name}
	错误消息：${err.message}
	错误堆栈：${err.stack}
	错误时间：${new Date()}
===================================================\n\n\n`
    fs.appendFile('./err_log.txt', err_log, err => {
        res.writeHeader(500,{})
        res.end('小可爱，服务器正忙，请稍后重试！')
    })
})

err为next传过来的错误对象
```



### Express - CRUD

### 起步

- 初始化
- 模板处理（UI界面）

### 路由设计

| 请求方法 | 请求路径         | get参数 | post参数                       | 备注             |
| :------- | ---------------- | :------ | ------------------------------ | ---------------- |
| get      | /students        |         |                                | 渲染首页         |
| get      | /students/new    |         |                                | 渲染添加学生页面 |
| post     | /students/new    |         | name、age、gender、hobbies     | 处理添加学生请求 |
| get      | /students/edit   | id      |                                | 渲染编辑页面     |
| post     | /students/edit   |         | id、name、age、gender、hobbies | 处理编辑请求     |
| get      | /students/delete | id      |                                | 处理删除请求     |

### 自己编写步骤

- 处理UI框架
- 配置开放静态资源
- 配置模板引擎
- 简单路由：`/`渲染静态页面出来
- 路由设计
- 提取路由模块
- 由于接下来的一系列的业务操作都需要处理文件数据，所以我们要封装student.js
- 先写好students.js结构
  + 查询所有学生列表的API find
  + findById
  + save
  + updateById
  + deleteById
- 实现具体功能
  + 通过路由收到请求
  + 接收请求中的数据（get，post）
    * req.query
    * req.body
  + 调用数据操作API处理数据
  + 根据操作结果给客户端发送响应

### art-template

配置并加载`express-art-template`就可以使用了

#### 子模板

```javascript
// 文件
header.html   // 这个文件也不用有完整的html结构 可以只有标签  <h1>你好</h1>
body.html


// 在body.html中实现继承   这样在body中就可以继承到header中的内容了
{{ include './header.html'}}  // 这里的意思就是把header.html中的<h1>你好</h1>放在这里
```

#### 模板继承

```javascript
// 文件
layout.html   模板文件
son.html    子文件


// 在模板文件layout中
<DOCTYPE html>
    <html>
    	<header></header>
		{{ block 'header'}}{{ /block }}  // 为了让孩子有自己的样式
		<body>
    		{{ block 'content' }}
            	<h1>默认渲染内容</h1>
			{{ /block }}
    	</body>
        {{ block 'footer'}}{{ /block }} //  为了让孩子有自己的js行为
    </html>

              
// 在子文件中son.html
// 先继承
{{ extend './layout'}}
// 写替代h1的内容
{{ block 'content' }}
	<div>
        <h1>子页面的内容</h1>
    </div>
{{ /block }}

// 这样在son中就不用写html的结构   就可以继承layout的html结构
```





## express-art-temlplae





## 回调函数

如果需要获取一个函数中异步操作的结果，则必须通过回调函数来获取

- 获取异步操作的结果

```javascript
function fns(callback) {
    // var callback = function (data) { console.log(data) }
    setTimeout(function () {
        var data = 'hello'
        callback(data)
    }, 1000)
}

fn(function (data) {
    console.log(data)
})
```

## JSON.parse 和 JSON.stringify()的区别

- JSON.parse   从字符串中解析出json对象

```javascript
var db = '{ "name": 'dengbo', "age": 18 }'
var result = JSON.parse(db)
console.log(result)

// 结果为
{ name: 'dengbo', age: 18 }
```

- JSON.stringify()   从一个对象中解析出字符串

```javascript
var db = '{ "name": 'dengbo', "age": 18 }'
var result = JSON.stringify(db)
console.log(result)

// 结果为
'{"name": "dengbo", "age": 18 }'
```

## package.json和package-lock.json

npm5之前是不会有`package-lock.json`这个文件的

npm5之后才能有这个文件

在安装每个包的过程中，`pageage-lock.json`这个文件会自动生成或者更新

- npm5以后的版本，安装包时不需要加`--save`，就会自动保存包依赖信息
- `package-lock.json`这个文件会自动保存`node_modules`中所有包信息（版本，下载地址）
  + 这样的话，把`node_modules`删除后重新安装**下载速度更快**
- 从文件来看，有一个`lock`锁
  + 这个`lock`使用来锁定版本的
  + 所以这个`package-lock.json`另一个作用就是锁定版本号，防止再次安装时自动升级到最新版

## MongoDB

### 关系型数据库

- 表就是关系    表与表之间存在关系
- 所有的关系型数据库在操作前都需要设计表结构
- 而且数据表还支持约束
  + 唯一的
  + 主键
  + 默认值
  + 非空
  + 。。。

### 非关系型数据库

- 非关系型数据库非常灵活
- 有的非关系型数据库就是键值对儿
- MongoDB是最像关系型数据库   的  非关系型数据库
  + 数据库    ->    数据库
  + 数据表    ->    数组
  + 表记录    ->    文档对象
- MongoDB不需要设计表结构

### MongoDB数据库的基本认知

MongoDB本身相当于最外层的集合

- 数据库      相当于下面的     qq、wechat、qqMusic
- 集合          相当于下面的     users、products、musics               表
- 文档          相当于下面的    每一条数据记录                                   表记录

```javascript
{
    qq: {
        users: [
            {每一条数据，       也叫一个文档},
            {},
            {}
        ],
        products: [
            {},
            {},
            {}
        ]
    },
    wechat: {
        users: [
            {}
        ]
    },
    qqMusic: {
        musics: [
            {每一条数据}
        ]
    }
    
    
}
```

 sudo ln -s /Users/Suvan/data /data

### 使用MongoDB

启动：

```shell
# mongodb 默认使用执行mongod命令所处盘符根目录下的 /data/db 作为自己的数据库存储目录
# 所以需要手动新建一个  /data/db
mongod
```

如果想要修改默认的数据存储路径，可以：

```shell
mongod --dbpath=数据存储目录路径
```

连接：

```shell
mongo
```

退出

```shell
exit
```

### 基本命令

- `mongo`    连上数据库

- `show dbs`     只有数据库有数据才能显示
- `db`   查看当前操作的数据库   默认是test
- `use` 数据库的名字   切换到指定的数据库（如果没有就会自动新建）   也相当于创建并使用数据库
- `show collections`  显示当前数据库的所有集合
- `db.err_log.find()`    查看所有
- `db.err_log.find().pretty()`   美化输出
- 增加数据
- 删除数据
- 修改数据
- 查询数据

### 在node中如何操作MongoDB数据

#### 使用官方的`MongoDB`包来操作

官方文档：https://github.com/mongodb/node-mongodb-native

- 其实就是用   原生方法写

#### 使用第三方 `mongoose` 来操作MongoDB数据库

- `mongoose`是基于官方的`mongodb`包再一次封装





### mongoose基本使用

- 设计schema发布model

```javascript
var mongoose = require('mongoose')

// 1、设计数据库架构
var Schema = mongoose.Schema

///2、连接数据库
mongoose.connect('mongodb://localhost/dag')

// 3、设计文档结构(表结构)
//    字段名称就是表结构的属性名称
//    约束的目的是为了保证数据的完整性，不要有脏数据
var userSchema = new Schema({
    username: { type: String, required: true },
   	password: { type: String, required: true }
})

// 4、将文档结构发布为模型
//    第一个参数：一个大写字母开头的单词作为数据库的名称    数据库名称   User
//              mongoose自动把首字母转为 小写复数       集合名称    users
//    第二个参数：就是上边的架构                        userSchema
var User = mongoose.model('User', userSchema)


// 5、接下来就可以对users为所欲为了

```



- 增加数据

```javascript
// 添加数据
var admin = new User({
    username: 'dag',
    password: '123456'
})

// 保存数据
admin.save(function (err, ret) {
    if (err) {
        console.log('添加失败！')
    } else {
        console.log('添加成功！')
    }
})
```

- 查询数据

```javascript
// 第一个参数是一个对象，表示按条件查询  省略查全部
// { username: 'dag' } 表示 要查询一个  username : dag  的记录
User.find({username: 'dag'},function (err, ret) {
    if (err) {
        console.log('查询失败！')
    } else {
        console.log('查询成功！')
    }
})
find方法返回值为数组
findOne方法返回值是对象

```

- 删除

```javascript
User.remove({username: 'dag'},function (err, ret) {
    if (err) {
        console.log('查询失败！')
    } else {
        console.log('查询成功！')
    }
})
```

- 更新

```javascript
User.findByIdAndUpdate(id, {
    password: '123'
}, function (err, ret) {
    if (err) {
        console.log('查询失败！')
    } else {
        console.log('查询成功！')
    }
})

// 返回值为数组
```

## 异步编程Promise

- throw err
  + 阻止程序执行
  + 把错误消息打印到控制台

推荐书籍：http://es6.ruanyifeng.com/#docs/promise

## 注册登录练习

### 结构

- 一般要有结构，但这个项目只有登录注册，不完整就不写了

### 路由

| 路径      | 方法 | get参数 | post参数                  | 是否需要登录权限 | 备注         |
| --------- | ---- | ------- | ------------------------- | ---------------- | ------------ |
| /         |      |         |                           |                  | 渲染首页     |
| /register | get  |         |                           |                  | 渲染注册页面 |
| /register | post |         | email、nickname、password |                  | 处理注册请求 |
| /login    | get  |         |                           |                  | 渲染登录页面 |
| /login    | post |         | email、password           |                  | 处理登录请求 |
| /logout   | get  |         |                           |                  | 处理退出请求 |



## 登录



## 注册



## 最后零散的重点

- `form`表单上通过`action`和`method`提交的表单数据是**同步请求**

- 服务端重定向针对异步请求无效

- Session就 相当于服务端    cookie就相当于一个凭证

  + Cookie可以保存一些不太敏感的数据，但是不能用来保存用户登录状态

  + 超市 -> 电子柜(服务端)
  + 我(客户端)    (二维码小票（开箱凭证）cookie)  凭证是唯一的，不可重复  一旦丢失，不可找回，状态也就丢失了。  
  + 小票是服务器给的，所以就很安全，不太容易伪造出来    这个时候就可以保存一些敏感的数据到服务端
  + 客户拿着小票就就可以了
  + 简单的说可以用 session 和  cookie  保存用户的登录信息

## `express session`配置使用

默认session数据是默认存储，服务器重启就会消失，一般需要持久化存储

- 安装`cnpm i express-session -S`
- 配置

```javascript
// 在express这个框架中， 默认不支持Session 和  Cookie
// 可以使用第三方中间件：express-session  来解决
// 使用Session，Session是一个对象
//    添加 Session 数据：req.session.foo = 'bar'
//    访问 Session 数据：req.session.foo
app.use(session({
  secret: 'dag',    // 配置加密字符串，会在加密的基础上，把这个字符串一块加密，更安全
  resave: false,
  // 为true时，无论是否使用session，服务端都会给一把钥匙，小票
  saveUninitialized: true
}))
```







