# DOM学习

- 文档对象模型
- DOM  就是把【文档】当做一个【对象】来看待
- DOM  的顶级对象是  document
- DOM  主要学习的是操作页面元素
- DOM  是  W3C  标准规范

## Web API

Web  API是浏览器提供的一套操作浏览器功能也页面元素的  API

## DOM树

![](/Volumes/career/04_note/studyNotes/00-images/dom-tree.png)



## 获取元素--查

主要有以下几种方式

- 根据  **ID**  获取
  - `let id = document.getElementById('id')`
    - 严格区分大小写
    - 返回的是元素对象
- 根据**标签名**获取
  - `let lis = document.getElementsByTagName('li')`
    - 返回的是**伪数组**形式的元素对象
    - 如果没有元素返回空数组
  - `let ol = document.getElementsByTagName('ol')`   `ol.[0].getElementsByTagName('li')`
    - 如果同时出现  ul  和  ol  而只想要  ol  中的  li
- 通过H5新增方法获取
  - `let boxes = document.getElementsByClassName('box')`
  - 只返回页面中的第一个元素对象
    - `let box = document.querySelector('.box')`  类
    - `let dag = document.querySelector('#dag')`  ID
    - `let li = document.querySelector('li')`  标签
  - 返回页面中所有的元素对象
    - `let boxes = document.querySelectorAll('.box')`  类
    - 。。。

- 特殊元素获取
  - 获取  body  元素
    - `let bodyEle = document.body`
  - 获取  html  元素
    - `let html = document.documentElement`



## 事件

### 事件基础

事件三要素：事件源、事件类型、事件处理程序

#### 常见鼠标事件

| 鼠标事件    | 触发条件         |
| ----------- | ---------------- |
| onclick     | 鼠标点击左键触发 |
| onmouseover | 鼠标经过触发     |
| onmouseout  | 鼠标离开触发     |
| onfocus     | 获得鼠标焦点触发 |
| onblur      | 失去鼠标焦点触发 |
| onmousemove | 鼠标移动触发     |
| onmouseup   | 鼠标弹起触发     |
| onmousedown | 鼠标按下触发     |

#### mouseover和mouseenter的区别

- `mouseover`  鼠标经过自身盒子会触发，经过子盒子也会再次触发，因为有事件冒泡
- `mouseenter`  鼠标只有经过自身时才会触发。没有事件冒泡
  - 与  `mouseenter`  搭档鼠标离开事件  `mouseleave`  也没有事件冒泡



### 事件高级

#### 注册事件

给元素添加事件，称为注册事件或者是绑定事件

有两种方式：

- **传统方式**

![](/Volumes/career/04_note/studyNotes/00-images/event-on.png)

- **监听注册方式**  ie9

![](/Volumes/career/04_note/studyNotes/00-images/event-addeventlistener.png)

```javascript
let btn = document.querySelector('button')

btn.addEventListener('click', function () {  }, true)

// 有三个参数：
// arg1：事件类型
// arg2：处理函数
// arg3：布尔值    true 是捕获阶段   false 是冒泡阶段
```



- **传统监听方式**  不推荐  ie9以前才使用

![](/Volumes/career/04_note/studyNotes/00-images/event-tradition.png)

#### 删除事件

- **传统事件解绑**  `btn.onclick = null`

```javascript
let btn = document.querySelector('btn')

btn.onclick = function () {
    alert(11)
    btn.onclick = null
}
```

- **监听事件解绑**

```javascript
let btn = document.querySelector('btn')

btn.addEventListener('click', function fn() {
    alert(22)
	btn.removeEventListener('click', fn)
})

// 或者如此
let btn = document.querySelector('btn')

function fn () {
    alert(22)
    btn.removeEventListener('click', fn)
}
btn.addEventListener('click', fn)
```



- 传统监听方式

```javascript
let btn = document.querySelector('btn')

btn.attachEvent('onclick', fn)

function fn() {
    alert(33)
    btn.detachEvent('onclick', fn)
}
```



#### DOM事件流--捕获 和 冒泡

事件流描述的是从页面中接收事件的顺序。

事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流

![](/Volumes/career/04_note/studyNotes/00-images/event-spread.png)

- 事件冒泡：IE  最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到  DOM  最顶层节点的过程
  - son  ->  father  ->  body  ->  html  ->  document
- 事件捕获：网景最早提出，由  DOM  最顶层节点开始，然后逐级向下传播到最具体的元素接收的过程
  - document  ->  html  ->  body  ->  father  ->  son

![](/Volumes/career/04_note/studyNotes/00-images/event-capture-bubbing.png)



**注意**

- JS  代码中只能执行捕获或者冒泡其中的一个阶段
- onclick  和  attachEvent  只能得到冒泡阶段
- addEventListener(type, listener, useCapture)  第三个参数是  true  就是捕获阶段，false  就是冒泡阶段
- 实际开发中很少使用事件捕获，更关注事件冒泡
- 有些事件是没有冒泡的  onblur  onfocus  onmouseenter  onmouseleave

#### 事件对象

![](/Volumes/career/04_note/studyNotes/00-images/event-object.png)



处理兼容性问题：e  =  e ||  window.event



##### 事件对象常见的属性和方法

| 事件对象属性和方法      | 说明                                                    |
| ----------------------- | ------------------------------------------------------- |
| e.target                | 返回触发事件的元素对象    标准                          |
| e.srcElement            | 返回触发事件的元素对象    非标准ie6-8                   |
| e.type                  | 返回事件类型  click  mouseover  不带  on                |
| e.cancelBubble  =  true | 该属性阻止冒泡  非标准ie6-8                             |
| e.returnValue           | 该属性阻止默认事件（默认行为）非标准ie6-8  不让链接跳转 |
| e.preventDefault()      | 该属性阻止默认事件（默认行为）标准                      |
| e.stopPropagation()     | 阻止冒泡  标准                                          |



##### 阻止事件冒泡的两种方式

- e.stopPropagation()
- e.cancelBubble  =  true

##### 事件委托

**事件委托原理**：不再给每个子节点单独设置监听器，而是将监听器设置在父节点上，然后利用冒泡的形式影响每个子节点

```javascript
<ul>
    <li>1</li> 
		<li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
</ul>

let ul = document.querySelector('ul')
// 给父节点设置  监听事件，通过事件冒泡的形式，影响小li  点击一下小li，会向上冒泡
ul.addEventListener('click', function (e) {
    e.target.style.backgroundColor = 'pink'
    alert('发生冒泡')
})
```



##### 禁用右键菜单和禁止选中文字--鼠标事件

禁用右键菜单-----contextmenu

```javascript 
document.addEventListener('contextmenu', function () {
    e.preventDefault()
})
```

禁止选中文字-----selectstart

```javascript
document.addEventListener('selectstart', function () {
    e.preventDefault()
})
```



##### 鼠标事件对象

event  对象代表事件的状态，跟事件相关的一系列信息的集合。现阶段我们主要用的鼠标事件对象  MouseEvent

和键盘事件对象  KeyboardEvent

| 鼠标事件对象 | 说明                                      |
| ------------ | ----------------------------------------- |
| e.clientX    | 返回鼠标相对于浏览器窗口可视区的  X  坐标 |
| e.clientY    | 返回鼠标相对于浏览器窗口可视区的  Y  坐标 |
| e.pageX      | 返回鼠标相对于文档页面的  X  坐标    ie9+ |
| e.pageY      | 返回鼠标相对于文档页面的  Y  坐标    ie9+ |
| e.screenX    | 返回鼠标相对于电脑屏幕的  X  坐标         |
| e.screenY    | 返回鼠标相对于电脑屏幕的  Y  坐标         |

##### 常用键盘事件

- 三个事件的执行顺序  keydown  ->  keypress  ->  keyup

| 键盘事件   | 触发条件                                                     |
| ---------- | ------------------------------------------------------------ |
| onkeyup    | 按键弹起时触发--不区分大小写：字母大小写的ASCII值一样        |
| onkeydown  | 按键按下时触发--不区分大小写：字母大小写的ASCII值一样        |
| onkeypress | 按键按下时触发  不识别功能键  ctrl  shift等<br />区分大小写：字母大小写的ASCII值不同 |

- 键盘事件对象

| 键盘事件对象 | 说明              |
| ------------ | ----------------- |
| e.keyCode    | 返回按键的ASCII值 |



##### 跟随鼠标移动案例

![](/Volumes/career/04_note/studyNotes/00-images/mousemove-angel.png)



## 元素及属性操作--改

### 改变普通元素内容--可读写

div  span  标签里边的内容

- `element.innerText`
  - 非标准，不识别  html  标签，去除空格和换行

```javascript
let btn = document.querySelector('.btn')
let div = document.querySelector('div')

btn.onclick = function () {
    div.innerText = '2020-01-19'
}
```



- `element.innerHTMl`   
  - w3c推荐，识别  html  标签，保留空格和换行

```javascript
let div = document.querySelector('div')

div.innerHTML = '<strong>今天是：</strong>晴天'
```



### 改变元素属性

src  href  alt  title等

```javascript
let btn_ldh = document.getElementById('ldh')
let btn_zxy = document.getElementById('zxy')
let img = document.querySelector('img')

btn_ldh.onclick = function () {
    btn_ldh.src = 'img/ldh.jpg'
    btn_ldh.title = '刘德华'
}

btn_zxy.onclick = function () {
    btn_zxy.src = 'img/zxy.jpg'
    btn_zxy.title = '张学友'
}
```



### 改变表单元素属性

type  value  checked  selected  disabled

- 修改value，从而修改表单的文字内容

```javascript
let btn = document.querySelector('.btn')
let input = document.querySelector('input')

btn.onclick = function () {
    input.value = '被点击了'
    btn.disabled = true
}
```



### 改变元素样式

大小、颜色、样式

- 行内样式  `element.style`

```javascript
let div = document.querySelector('div')

div.onclick = function () {
    div.style.backgroundColor = 'pink'
    this.style.width = '250px'
    this.style.color = '#fff'
    this.style.fontSize = '16px'
    this.style.marginTop = '10px'
   
}
```



- 类名样式  `element.className`

```javascript
.change {
    backgroundColor = 'pink'
}

let div = document.querySelector('div')

div.onclick = function () {
    this.style.className = 'change'
    
    // 也可以使用多类名选择器  old表示原来就有的，new表示新添加的
    this.style.className = 'old new'
}
```





### 操作元素总结

![](/Volumes/career/04_note/studyNotes/00-images/opera-element.png)



### 排他思想

首先先排除其他人，然后在设置自己的样式

```javascript
let btns = document.getElementsByTagName('button')

for (let i = 0; i < btns.length; i++) {
    btn[i].onclick = function () {
        // 先清除掉所有的
    	for (let i = 0; i < btns.length; i++) {
            btn[i].style.backgroundColor = ''
        }
        // 再设置自己的
        this.style.backgroundColor = 'pink'
    }
    
}
```



### 自定义属性的操作

H5自定义属性：必须以  `data-`  开头，并且赋值。在  js  中，只能通过  getAttribute  来获取

**获取属性值**   `<div id = "demo" data-index= "1"></div`

- 只能获取内置属性：`element.属性`    `div.id`的值为  demo
- **也可以获取自定义属性：`element.getAttribute('属性')`      `div.getAttrubute('id')`的值为  demo**



**设置属性值**  element.setAttribute('属性'， 值)

- `div.id = 'dag'`
- **`div.setAttribute('data-index', 2)`**

**移除属性**  element.removeAttribute('属性')

- **`div.removeAttribute('data-index')`**

**H5**新增方法

- `div.dataset.index`  可以得到自定义属性值    dataset是一个集合   使用这个集合不用管  `data-`  了



## 节点操作

### 获取节点

- 父节点：`element.parentNode`    找不到  返回为  null	
- 子节点：`element.childNodes`    包含所有的子节点，包括元素节点、文本节点、换行节点
- 子节点：`element.children`         只获取子元素节点  **重点**
- 下一个兄弟节点：`element.nextSibling`  包括元素节点、文本节点、换行节点
- 下一个兄弟元素节点：`element.nextElementSibling`  ie9
- 上一个兄弟节点：`element.previousSibling`  包括元素节点、文本节点、换行节点
- 上一个兄弟元素节点：`element.previousElementSibling`  ie9

**节点层级**

获取第一个子节点：这里的节点是所有的节点，包括元素节点、文本节点、换行节点

- 第一个孩子节点：`parentNode.firstChild`    包括文本节点
- 最后一个孩子节点：`parentNode.lastChild`  包括文节点

获取第一个子元素节点：ie9

- 第一个元素节点：`parentNode.firstElementChild`
- 最后一个元素节点：`parentNode.lastElementChild`

实际开发：

- `element.children[0]`  **重点**



### 创建节点--创建

- `document.createElement('li')`
- `document.innerHTML=  '<a href="">123<a/>'`
- `document.createElement('a')`

### 添加节点--增

第一步：创建元素；第二步：添加元素

- 追加元素节点：`node.appendChild( li )`
- 插入元素节点：`node.insertBefore( li，ul.children[0] )`  agr1：元素，arg2：位置



### 删除节点--删

- `node.removeChild( child )`

- `node.removeChild( ul.children[0] )`

### 复制节点

- `node.cloneNode()`  括号里面是  false  或者  true
- `let li = ul.children[0].cloneNode()`
- 注意：括号里面为空或者是  false  ，只是浅拷贝，只复制标签元素，不复制内容



### 创建节点的三种方式及对比

| 方式                                       | 区别                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| document.write( '<div>123</div>' )         | 页面会重绘，导致原来的内容不存在                             |
| document.innerHTML =  '<a href="">123<a/>' | 大量创建时，字符串拼接，效率低<br />用数组追方式效率最高，结构复杂 |
| document.createElement('a')                | 大量创建时，效率高，结构清晰                                 |



![](/Volumes/career/04_note/studyNotes/00-images/create-element.png)

## 创建增删改查总结--重点核心

### 创建

![](/Volumes/career/04_note/studyNotes/00-images/total-create-element.png)

### 增

![](/Volumes/career/04_note/studyNotes/00-images/total-increase-element.png)

### 删

![](/Volumes/career/04_note/studyNotes/00-images/total-remove-element.png)

###  改

![](/Volumes/career/04_note/studyNotes/00-images/total-modify-element.png)

### 查

![](/Volumes/career/04_note/studyNotes/00-images/total-select-element.png)

### 属性操作

![](/Volumes/career/04_note/studyNotes/00-images/total-attribute.png)