# BOM学习

- 浏览器对象模型
- 把【浏览器】当做一个【对象】来看待
- BOM  的顶级对象时  window
- BOM  学习的是浏览器窗口交互的一些对象
- BOM  是浏览器厂商在各自浏览器上定义的，兼容性差，最初是由  NetScape  公司提出的

![](H:\06-Web前端\05-笔记\00-images\BOM-part.png)

- window  对象浏览器的顶级对象，具有双重角色

- 它是  JS  访问浏览器窗口的一个接口
- 它是一个全局对象。定义在全局作用域的变量、函数都会变成  window  对象的属性和方法。window通常省略

## window  对象的常见事件



### 窗口加载事件

```javascript
window.onload = function () {
    
}
// 或者
window.addEventListener('load', function () {
    
})
// 触发条件：a链接、刷新、前进后退  前进后退会缓存
```

window.onload是窗口（页面）加载事件，当文档内容完全加载完成会触发该事件（包括图像、脚本文件、CSS、文件等），就调用的处理函数。

- 有了窗口加载事件，就可以把  JS  代码写到页面上边了。
- window.onload  传统注册事件方式只能写一次，重复写多个，只会执行最后一个
- 使用监听的方式，就没有限制

```javascript
document.addEventListener('DOMContentLoaded', function () {
    
})
```

- 使用  DOMContentLoaded  事件触发时，仅当DOM加载完成，不包括样式表、图片、flash等等
- ie 9
- 页面图片很多时，很好
- 加载更快，主要的标签加载完成后就会执行

```javascript
window.addEventListener('pageshow', function (e) {
  e.persisted  // 返回的为true，就是说这个页面是来自于缓存 
})
```

- 这个事件在页面显示时触发，无论页面是否来自缓存

### 调整窗口大小事件

- 当浏览器窗口发生变化时，就会加载这个事件
- 响应式布局

```javascript
window.onresize = function () {
    
}

window.addEventListener('resize', function () {
    
})
```

获取浏览器窗口宽度：`window.innerWidth`

## 定时器

### setTimeout()

- `window.setTimeout(function () , 1000)`
- 定时器属于  window  ，但是可以省略
- 只执行一次

### clearTimeout()

- window  可以省略
- 括号里写定时器的名字，所以，想要停止定时器，就必须要给定时器起一个名字
- `clearTimeout(timer)`
- 注意局部变量，使用全局变量的话  `let timer = null`  让定时器为空对象



### setInterval()

- `window.setInterval(function () , 1000)`
- window  可以省略

- 无休止执行函数

### clearInterval()

- window  可以省略
- 括号里写定时器的名字，所以，想要停止定时器，就必须要给定时器起一个名字
- `clearInterval(timer)`
- 注意局部变量，使用全局变量的话  `let timer = null`  让定时器为空对象



## JS中的执行队列

JS  是单线程

![](H:\06-Web前端\05-笔记\00-images\asyn-task.png)

### 执行机制

- 先执行主线程执行栈
- 后执行异步任务
- 异步任务一个个执行，执行完就清空任务队列，如果有多个异步任务，先交给异步进程处理

![](H:\06-Web前端\05-笔记\00-images\asyn-task1.png)

### 事件循环

even  loop

![](H:\06-Web前端\05-笔记\00-images\even-loop.png)

由于主线程不断的重复获得任务，执行任务、在获取任务、再执行，这种机制被称为**事件循环**

### js中的异步任务

js  中的异步任务通过回调函数来实现

- 普通事件：如  click、resize等
- 资源加载：如  load、error等
- 定时器：如  setTimeout、setInterval等



## loaction对象

window  对象给我们提供了一个  location  属性，用于获取或这只窗体的  URL，并且可以用于解析  URL。因为这个属性返回的是一个对象，所以我们将这个属性称为  location  对象

### URL

统一资源定位符（Uniform  Resource  Locator，URL）是互联网标准资源的地址。互联网上的每个文件都有一个唯一的  URL，它包含的信息指出文件的位置以及浏览器应该怎么处理它。

**格式**

```
protocol://host[:port]/path/[?query]#fragment

http://www.itcast.cn/index.html?name=andy&age=18#link
```

| 组成     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| protocol | 通信协议，通常的用http，ftp，maito，https                    |
| host     | 端口号可选，省略是使用方案的默认端口号如  http  的默认端口号为80 |
| path     | 路径由零或多个 / 符号隔开的字符串，一般用来表示主机上的一个目录或文件地址 |
| query    | 参数  用键值对的形式，通过  &  符号分割                      |
| fragment | 片段  #  后面内容  常见于链接  锚点                          |

### location对象的属性

| location对象属性  | 返回值                              |
| ----------------- | ----------------------------------- |
| location.href     | 获取或设置整个  URL                 |
| location.host     | 返回主机（域名）www.itheima.com     |
| location.port     | 返回端口号  如果未写返回空字符串    |
| location.pathname | 返回路径                            |
| location.search   | 返回参数                            |
| location.hash     | 返回片段 #后面内容 常见于链接和锚点 |

### location对象方法

| location对象方法   | 返回值                                                       |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 跟href一样，可以跳转页面（也称为重定向），有记忆功能，能后退 |
| location.replace() | 替换当前页面，以为不记录历史，所以不能后退页面               |
| location.reload()  | 重新加载页面，相当于刷新按钮或者  f5  如果参数为true强制刷新Ctrl + f5 |



## navigation对象

navigation  对象包含有关浏览器的信息，它有很多属性，我们常用的是  userAgent，该属性可以返回由客户机发动服务器的  user-agent  头部的值

下面的代码可以实现自动判断是  PC端打开页面还是移动端打开页面，并自动响应适当的页面

![](H:\06-Web前端\05-笔记\00-images\match-pc-iPhone.png)

## history对象

window  对象给我们提供了一个  history  对象，与浏览器历史记录进行交互。该对象包含用户（在浏览器窗口中）访问过的  URL

| history对象方法 | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| back()          | 可以后退功能                                                 |
| forward()       | 前进功能                                                     |
| go(参数)        | 前进后退功能  参数如果是 1 前进 1 个页面，如果是 -1 后退 1 个页面 |



## 元素偏移量  offset  系列

offset  翻译过来就是偏移量，我们使用  offset  系列相关属性可以动态的得到该元素的位置（偏移）、大小等

- 获得元素距离**带有定位父元素**的位置
- 获得元素自身的大小（宽度和高度）
- 注意：返回的数值都不带单位

| offset系列属性        | 作用                                                         |
| --------------------- | ------------------------------------------------------------ |
| element.offsetParent  | 返回作为该元素带有定位的父级元素，如果父级都没有定位则返回body |
| element.offsetTop     | 返回元素相对带有定位父元素上方的偏移                         |
| element.offsetLeft    | 返回元素相对带有定位父元素左边框的偏移                       |
| element.offsetWidth   | 返回自身包括padding、border、content的宽度，返回值不带单位   |
| element.offsetHeitght | 返回自身包括padding、border、content的高度，返回值不带单位   |

### offset  和  style的区别

| offset                                        | style                                         |
| --------------------------------------------- | --------------------------------------------- |
| offset可以得到任意样式表总的样式 值           | style只能得到行内样式表中的样式值             |
| offset系列获得的  数值  是没有单位的          | style.width获得的是带有单位的字符串           |
| offsetWidth包括padding+border+width           | style.width获得不包括padding和border的值      |
| offsetWidth等属性是只读属性，只能获取不能赋值 | style.width是可读写的属性，可以获取也可以赋值 |
| 所以，想要获取元素大小位置，用offset更合适    | 所以，想要给元素更改值，则需要用  style       |

## 元素可视区  client  系列

client  翻译过来就是客户端，我们使用  client  系列的相关属性来获取元素可视区的相关信息。通过  client  系列的相关属性可以动态的得到该元素的边框大小，元素大小等

| client系列属性       | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.clientTop    | 返回元素上边框的大小                                         |
| element.clientLeft   | 返回元素左边框的大小                                         |
| element.clientWidth  | 返回自身包括padding、content的宽度，不含边框，返回值不带单位 |
| element.clientHeight | 返回自身包括padding、content的高度，不含边框，返回值不带单位 |



## 元素滚动  scroll  系列

scroll  翻译过来就是滚动的，我们使用  scroll  系列的相关属性可以动态的得到该元素的大小、滚动距离等

| scroll系列属性       | 作用                                           |
| -------------------- | ---------------------------------------------- |
| element.scrollTop    | 返回被卷去的上侧距离，返回数字不带单位  非页面 |
| element.scrollLeft   | 返回被卷去的左侧距离，返回数值不带单位  非页面 |
| element.scrollWidth  | 返回自身实际的宽度，不含边框，返回数值不带单位 |
| element.scrollHeight | 返回自身实际的高度，不含边框，返回数值不带单位 |

- 宽高返回的是真正内容的大小：**内容溢出，占了多少就返回多少**

## 页面卷去头部

- `window.pageXoffset`
- `window.pageYoffset`

## 三大系列总结

| 三大系列大小对比    | 作用                                                         |
| ------------------- | ------------------------------------------------------------ |
| element.offsetWidth | 返回自身包括padding、border、content的宽度，返回值不带单位   |
| element.clientWidth | 返回自身包括padding、content的宽度，不含border、返回值不带单位 |
| element.scrollWidth | 返回自身实际的宽度，不含border，返回值不带单位               |

### 主要用法

- offset系列经常用于获得元素位置  offsetLeft  offsetTop
- client经常用于获取元素大小  clientWidth  clientHeight
- scroll经常用于获取滚动距离  scrollTop  scrollLeft
- 注意页面滚动的距离通过  window.pageXoffset  获得

## 动画基本原理

- 获得盒子当前位置
- 让盒子在当前位置加上移动的距离和方向
- 利用定时器  `setInterval`  不断重复







