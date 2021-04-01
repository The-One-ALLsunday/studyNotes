# babel学习

## babel-register

安装：

- `npm i babel-register -S`  实时转码工具

创建傀儡文件：（main.js）

```javascript
require('babel-register')
require('app.js')    // app为项目入口文件
```

使用node执行main.js文件

```javascript
node main.js
```

