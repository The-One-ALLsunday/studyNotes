# 项目实战总结

## 常用的CRUD思路

**添加**

- 点击显示  添加的对话框

- 点击添加按钮时，进行表单的预验证
- 预验证通过后，发起网络请求，添加记录
- 然后根据状态码判断 是否添加成功，并添加提示消息
- 最后，关闭对话框、刷新数据请求、提示添加成功

**修改**

- 点击显示  修改的对话框
- 根据  id  查询到用户的信息，element-ui  中利用作用域插槽，获取  id
- 根据  id  发起网络请求，拿到该  id  对应的数据
- 新建一个私有数据，用来存储通过  id  发请求拿回来的数据  修改表单的数据源就是请求回来的数据  并进行双向数据绑定
- 监听对话框的关闭事件，重置表单，防止验证表单仍然存在，影响美观
- 点击确定修改按钮之前，先进行表单的预验证
- 预校验通过，发起网络请求，把最新的双向绑定的数据发送过去  ，修改数据
- 根据  状态码  判断是否修改成功，并添加提示消息
- 最后，关闭对话框、刷新数据请求、提示修改成功

**删除**

- 这个需要全局  挂载  到  Vue  的原型对象上
  - `Vue.prototype.$confirm = MessageBox.confirm`

- 点击删除按钮，弹出  确认消息  提示框，询问用户是否执行删除操作。不是对话框 
- 通过  作用域插槽  把  id  传递给删除事件的函数中，根据  id  进行数据删除  
- 询问用户，如果用户确定删除，返回值是  字符串  confirm，点击取消会报错，因此需要使用  catch  捕获错误，这样取消后，返回值是  字符串  cancel，取消删除，要告诉用户  已取消此次删除操作
- 当确定删除，发起网络请求，删除该条数据记录
- 根据  状态码  判断是否删除成功，并添加响应的提示消息
- 最后，提示用户删除成功、刷新数据请求

# 项目优化

## 解决Eslint报错

- 在开发环境中，通过输出面板，找到错误和警告并修改

- 在生产环境中，通过输出面板，找到警告并修改

  - 通过  `babel-plugin-transform-remove-console`  移除代码中的  `console.log()`

  - 因为这个插件，只希望用于生产阶段，而不用于开发阶段，所以需要进行如下配置：

    ```javascript
    const prodPlugins = []
    if (porcess.env.NODE_ENV === 'production') {
        prodPlugins.push('transform-remove-console')
    }
    
    module.exports = {
        plugins: [
            ...prodPlugins
        ]
    }
    ```

    

## 生成打包报告

- 通过命令行方式生成打包报告
  - `vue-cli-service bulid --report`
- 通过可视化面板直接查看报告
  - 通过任务中的**分析**面板

## 为开发模式和生产模式指定不同的打包入口

在  `vue.config.js`  中通过  `configureWebpack(操作对象方式)`  和  `chainWebpack(链式编程方式)`

- 链式编程方式

  ![](H:\06-Web前端\05-笔记\00-images\chainWebpack.png)



## 第三方库启用CDN

默认情况下，通过  `import`  语法导入的第三方依赖包，最终会被打包合并到同一个文件中，从而导致打包成功后，单文件体积过大问题。

为了解决上述问题，可以通过  `webpack`  的  `externals`  节点，来配置并加载外部的  `CDN`  资源。凡是声明在  `externals`  中的第三方依赖包，都不会被打包，直接在  `window`  全局中寻找并使用

- 配置如下：结合生产环境使用

  ![](H:\06-Web前端\05-笔记\00-images\externals.png)



- 然后在  `public/index.html`  中引入  `CDN`  资源， `css`  和  `js`  资源

  **css**

  ![](H:\06-Web前端\05-笔记\00-images\cdncss.png)

  **js**

  ![](H:\06-Web前端\05-笔记\00-images\cdnjs.png)

**CDN中优化Element-UI**

经过上边的处理，只有  `Element-UI`  按需导入的组件文件过大，与上边一样，直接引入  `Element-UI`  的  `CDN`  资源

之前按需导入的  `Element-UI`  组件，在生产环境中，可以直接**注释**掉

## Element-UI组件按需导入

## 路由懒加载

需要三步

- 安装  `@babel/plugin-syntax-dynamic-import`  包

- 在  `babel.config.js`  配置文件中声明该插件

  ```javascript
  module.exports = {
      plugins: [
          '@babel/plugin-syntax-dynamic-import'
      ]
  }
  ```

  

- 将路由改为按需加载形式

  ![](H:\06-Web前端\05-笔记\00-images\vuerouterlazy.png)

## 首页内容定制

不同的打包环境下，首页内容可能会有所不同，我们可以通过插件的方式进行定制，插件配置如下

![](H:\06-Web前端\05-笔记\00-images\indexargs.png)

在  `public/index.html`  首页中，可以根据  `isPord`  的值，来决定如何渲染页面结构：

![](H:\06-Web前端\05-笔记\00-images\indexargs1.png)

# 项目上线

## 通过Node创建web服务器

![](H:\06-Web前端\05-笔记\00-images\projectonline.png)

## 开启gzip配置

![](H:\06-Web前端\05-笔记\00-images\gzip.png)

配置

![](H:\06-Web前端\05-笔记\00-images\compression.png)

## 配置https服务

![](H:\06-Web前端\05-笔记\00-images\https.png)

配置：

![](H:\06-Web前端\05-笔记\00-images\httpsconfig.png)

## 使用pm2管理应用

