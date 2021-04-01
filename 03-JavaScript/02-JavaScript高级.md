#  3JavaScript高级学习

## 类

```javascript
class 类名 {
    constructor (uname, age) {
        this.uname = uname
        this.age = age
    }
    sing (song) {
        // 类名中的方法
        console.log(this.uname + song)
    }
}

var dag = new 类名（参数一，参数二）
```

- 通过  class  关键字创建类，类名习惯首字母大写
- 类里面有一个  constructor  函数，用来接收传递过来的参数，同时返回实例对象
- constructor  函数，只要  new  生成实例，就会调用这个函数，如果没有就会自动生成
- 生成实例时，必须使用  new  关键字
- 多个函数或者方法之间不需要逗号分割

### 类的继承

```javascript
class Father {
    constructor () {
        
    }
    money () {
        console.log(100)
    }
}

class Son extends Father{
    
}

var son = new Son()
son.money()
```

### super关键字

```javascript
class Father {
    constructor (x, y) {
        this.x = x
        this.y = y
    }
    sum () {
        console.log(this.x + this.y)
    }
}

class Son extends Father{
    constructor (x, y) {
        super(x, y)
    }
    sum () {
        super.sum() // 就是调用父类中的普通函数
    }
}

var son = new Son(1, 2)
son.sum()
```

- super 关键字用于访问和调用对象父类上的函数
- 可以调用父类的构造函数，也可以调用父类中的普通函数

![](/Volumes/career/04_note/studyNotes/00-images/class-super.png)

这里的  super  关键字，既可以传到父类中，也可以自己用

### 面向对象和类的三个注意点

- 在  ES6  中类没有变量提升，所以必须先定义类，才能实例化对象
- 类里面共有的属性和方法一定要加  this
- this  指向问题
  - constructor  里面的  this  指向创建的实例对象
  - 方法里面的  this  指向这个方法的调用者



## 构造函数

构造函数是一种特殊的函数，主要用来初始化对象

### new  做的四件事

- 在内存中开辟一个新的空对象
- 让  this  指向这个空对象
- 执行构造函数里面的代码，给这个对象添加属性和方法
- 返回这个新对象（所以构造函数里面不需要  return）

###  成员

构造函数中的属性和方法叫做**成员**

```javascript
function Star(uname, age) {
    this.uname = uname
    this.age = age
    this.sing = function () {
        
    } 
}

Star.sex = '男'

let dag = new Star(a, 18)
```

**静态成员**

在构造函数本身上添加的成员，只能通过构造函数来访问

- 通过  `Star.sex = '男'`  来添加成员
- 通过  `Star.sex`  来访问

**实例成员**

通过构造函数内部的  this  添加的成员，只能通过实例化对象来访问

- 通过  `this.uname = uname`  来添加成员
- 通过  `dag.uname`  来访问



## 原型

原型是  对象

构造函数通过原型对象分配的函数是对所有对象共享的

```javascript
const Star(x, y) {
    this.x = x
    this.y = y
}

Star.prototype.sing = function () {
    
}
```

- 通过  prototype  给构造函数  Star  添加共享的方法
- 一般公共属性定义到构造函数里面，公共方法定义到原型对象上

### 对象原型

![](/Volumes/career/04_note/studyNotes/00-images/__proto__.png)

### constructor

如果我们以对象的形式重新给原型对象**赋值**，那么构造函数的原型对象上就没有  constructor  这个属性了，我们需要重新指回原来的构造函数

```javascript
Star.prototype = {
    constructor: Star,
    sing: function () {},
    movie: function () {}
}

// 重新赋值，使得原来  prototype 上的属性和方法全都没有了，所以需要  constructor  指回 Star
```



### 构造函数  prototype  和  constructor  的关系-----原型链

![](/Volumes/career/04_note/studyNotes/00-images/constructor-prototype-relation.png)

### 原型链

![](/Volumes/career/04_note/studyNotes/00-images/__proto__chain.png)

## 继承

- 继承属性用  `父.call(子, 参数1、参数2)`  等方法
- 继承方法用  原型对象

### call()方法实现属性继承

两个作用

- 调用函数
- 改变  this  指向，是把调用者（Father）的  this  改变为当前环境下的  this

继承父构造函数属性

```javascript
function Father(uname, age) {
    this.uname = uname
    this.age = age
}

function Son(uname, age, score) {
    Father.call(this, uname, age)
    this.score = score
}

const li = new Son('li', 15, 88)
```



### `Son.prototype = new Father()`实现方法继承

原理：

![](/Volumes/career/04_note/studyNotes/00-images/inherit_prototype.png)



实现：

```javascript
// 实现方法继承  new 一个 father 相当于创建了一个 father 的实例对象
Son.prototype = new Father()
// 这样的直接赋值，会使Son里面的prototype中的constructor指向father，所以需要修改constructor的指向
Son.prototype.constructor = Son
```



## ES5新增方法

### 数组方法

 迭代（遍历）方法：forEach()  some()  filter()  every()  map()  **括号里面是个函数**

#### forEach()----遍历数组

```javascript
let arr = [1, 2, 3]
let sum = 0
arr.forEach(function (value, index, array) {
    console.log('每个数组元素' + value)
    console.log('每个数组元素的索引' + index)
    console.log('数组本身' + array)
    
    sum += value
})

value：1,2,3
index：0,1,2
array：[1, 2, 3]

sum : 6
```

#### filter()----筛选数组

- 返回一个新数组

```javascript
let arr = [12, 34, 33, 46, 65]
var newArr = filter(function (value, index, array) {
    return value > 12
})

newArr = [34, 33, 46, 65]
```

#### some()----查找元素

- 返回  true  或者  false   只查找第一满足条件的值

```javascript
let arr = [12, 34, 45, 56, 67]
let flag = arr.some(function (value, index, array) {
    return value === 34
})

flag: true
```



### 字符串方法

str.trim()

### 对象方法

#### Object.keys(obj)查找对象属性

Object.keys(obj)    返回值：由属性名组成的数组

```javascript
let arr = Object.keys(obj)
```

#### Object.defineProperty()重新定义属性

- `Object.defineProperty(obj, prop, descriptor)`
  - 第三个参数以对象的形式书写，有四个参数
    - value：设置属性的值，默认为undefined
    - writable：值是否可以重写。true  |  false  默认是  false
    - enumerable：目标属性是否可以被枚举。true  |  false  默认是  false    **遍历时是否能显示出来**
    - configurable：目标属性是否可以被删除或是否可以再次修改特性 。true  |  false 默认是  false

```javascript
let o = {
    id: 1
    name: 'dag',
    age: 45
}

Object.defineProperty(o, 'county', {
    value: 'china'
})

Object.defineProperty(o, 'id', {
    writable: false     // id  是不可以修改，true的话可以修改
})
```

#### 删除对象中的属性值

```javascript
let obj = {
    demo: '小样'
}

delete obj.demo
```





## 函数进阶

### 函数的定义和调用

#### 自定义函数--命名函数

- `function dag() {  }`

#### 函数表达式--匿名函数

- `let dag = function () {   }`

#### new关键字定义

- `let dag = new Function('arg1', 'arg2', '函数体')`  函数体以字符串的形式



### 函数的调用方式

- 普通函数

```javascript
function fn() {
    
}

fn()
fn.call()
```



- 对象的方法

```javascript
let o = {
    sayHi: function() {
        
    }
}

o.sayHi
```



- 构造函数

```javascript
let function Dag(uname, age) {
    this.uname = uname
    this.age = age
    this.sayHi = function() {
        
    }
}

new Dag()
```



- 绑定事件函数

```javascript
btn.onclick = function () {}

// 点击了按钮就调用了
```



- 定时器函数

```javascript
setInterval(function() {}, 1000)

// 这个函数每隔1秒调用一次
```



- 立即执行函数

```javascript
(function () {  })()

// 立即执行函数是自动调用
```

### 各种函数的this指向

| 调用方式     | this指向                                     |
| ------------ | -------------------------------------------- |
| 普通函数     | window                                       |
| 构造函数     | 实例对象，原型对象里面的方法也是指向实例对象 |
| 对象方法调用 | 该方法所属对象                               |
| 事件绑定方法 | 绑定事件对象                                 |
| 定时器函数   | window                                       |
| 立即执行函数 | window                                       |



### 改变this指向

是把调用者（Father）的  this  改变为当前环境下的  this  (Son)

#### call()方法

- `调用者.call(指向, arg1, arg2)`

```javascript 
let o = {
    
}
function fn() {
    
}

fn.call(o)
```



 #### apply()方法

- `调用者.apply(指向, [arg1, arg2])`  数组是伪数组

```javascript
let o = {
    
}
function fn() {
    
}

fn.apply(o)

// 经典应用
let arr = [1, 44, 55, 66]
let max = Math.max.apply(Math, arr)

max: 66
```



#### bind()方法

- `调用者.bind(指向, arg1, arg2)`
- 不会调用原来的函数
- 返回值：**bind不会改变原函数的this指向**，返回值是原函数的拷贝，返回值的this指向  bind(this)  中的this

```javascript
let o = {
    
}
function fn() {
    
}

let f = fn.bind(o)
f()
```



#### call  apply  bind  的区别

**call  和  apply没有返回值  bind有返回值**

![](/Volumes/career/04_note/studyNotes/00-images/this.png)



## 严格模式

为脚本开启严格模式

- `'use strict'`  或者  `"use strict"`  记得加引号
- 消除代码运行的一些不安全之处，保证代码运行的安全
- 提高编译器效率，增加运行速度
- 为未来新版本的JavaScript做好铺垫

为个别函数开启严格模式

```javascript
function fn() {
    'use strict'  
}
```



### 改变

- 变量先声明再使用
- 不能删除已经命名好的变量
- 全局作用域下  this  指向  undefined，而不再是  window
- 构造函数不加  new  调用会报错，不再是  window



## 高阶函数

高阶函数是对其他函数操作的函数，也就是**接收函数作为参数**或将**函数作为返回值输出**

经典就是**回调函数**

## 闭包

闭包是函数： 一个函数有权访问另外一个局部作用域的变量

被访问的变量所在的函数叫做**闭包函数**

```javascript
function fn() {
    var num = 10
    function fun() {
        console.log(num)
    }
    fun()
}
fn()

```



```javascript
function fn() {
    var num = 10
    
    return function () {
        console.log(num)
    }
}

var f = fn()
f()
```



### 经典案例----使用闭包动态给小li添加索引号---立即执行函数

- `(function () { })()`
- `(function () {} ())`

立即执行函数就是一个小闭包，因为立即执行函数里面的任何一个函数都可以使用  `i`  这个变量

```javascript
var lis = document.querySelectotAll('li')

for (var i = 0; i < lis.length; i++) {
    (function (i) {
        lis[i].onclick = function () {
            console.log(i)
            lis[i].index = i 	
        }
    })(i)
}
```

### 产生闭包的情况

- 函数之间是父子关系，函数里面套函数，子函数可以使用父函数的局部变量
- 函数之间是兄弟关系，闭包函数要  return  出来一个新的函数，用新的变量接收调用，这样  return  的那个函数就可以使用闭包函数的局部变量





## 递归

一个函数在内部可以调用其本身，那么这个函数就是递归函数

递归里面必须加退出条件，如果没有  return  容易发生**栈溢出**

```javascript
function fn() {
    fn()
}
fn()
```

### 递归求阶乘

```javascript
function fn(n) {
    if (n == 1) {
        return 1
    }
    return n * fn(n-1)
}

fn()
```

### 斐波那契数列（兔子序列）

```javascript
function fb(n) {
    if (n == 1 || n == 2) {
        return 1
    }
    return fb(n - 1) + fb(n - 2)
}
```



## 浅拷贝和深拷贝--复杂数据类型才有的

### 浅拷贝

对象级别的只拷贝地址，修改一个都会变

```javascript
let obj = {
    name: dag,
    age: 45,
    family: {
        hobbies: 'son'
    }
}

let o = {}

// 第一种拷贝方式---遍历
for (k in obj) {
    o[k] = obj[k]
}
// 第二种拷贝方式---es6语法糖
Object.assign(o, obj)
```



### 深拷贝

深拷贝的内容会在内存空间重新开辟一块内存空间，与原来就不是同一个东西了

用到递归的原理

```javascript
let obj = {
    id: 1,
    name: dag,
    age: 45,
    msg: {
        hobbies: 'son'
    },
    color: ['pink', 'purple']
}

let o = {}

// 封装一个函数
function deepCopy(new, old) {
    for (k in old) {
        var item = old[k]
        if (item instanceof Array) {
            new[k] = []
            deepCopy(new[k], item)
        } else if (item instanceof Object) {
            new[k] = {}
            deepCopy(new[k], item)
        } else {
            new[k] = item
        }
    }
}
```



## 正则表达式

- 两个模式之间加  `|`  表示或者，意思就是两种模式都行

### 创建

```javascript
let regexp = new RegExp(/123/)

let regexp = /123/

reg.text('123')
```



### 边界符

- `/^abc/`  以  abc  开头
- `/^abc$/`  精确匹配   必须是  abc

### 字符类

- 字符组合  `/[a-zA-Z0-9_-]/`   26个英文字母任何一个字母返回都是 true    只能是一个
- 内部取反  `/[^a-zA-Z0-9_-]/`   不能包含里面的字符

### 量词符

用来设定某个模式出现的次数   要写在某个模式的**后面**

花括号的量词中间**不能有空格**

- `/^(abc){3}$/`   这表示  abc  整体重复3次

| 量词  | 说明                           | 使用         |
| ----- | ------------------------------ | ------------ |
| *     | 重复零次或更多次     >=0       | /^a*$/       |
| +     | 重复一次或更多次     >=1       | /^a+$/       |
| ？    | 重复0次或者一次       0 \|\| 1 | /^a?$/       |
| {n}   | 重复n次                        | /^a{3}$/     |
| {n,}  | 重复n次或更多次                | /^a{3,}$/    |
| {n,m} | 重复n到m次                     | /^a{3, 16}$/ |

### 表单验证

```javascript
//  失去焦点开始验证

var uname = document.querySelector('.uname')
var span = document.querySelector('span')
uname.onblur = function () {
    if (reg.text(this.value)) {
        // 正确的
        span.className = 'right'
        span.innerHTML = '用户名格式输入正确'
    } else {
        // 错误的
        span.className = 'wrong'
        span.innerHTML = '用户名格式输入不正确'
    }
}
```

### 预定义类

![](/Volumes/career/04_note/studyNotes/00-images/reg.png)

### 正则表达式的匹配问题[switch]

- `g`  全局匹配
- `i`  忽略大小写
- `gi`  全局匹配  +  忽略大小写

## 防抖函数和节流函数

### 防抖函数

当持续触发事件，一定时间内没有再触发事件，事件处理函数才会执行一次。如果设定时间到来之前又一次触发了事件，就重新开始计时。

- 定时器
- 闭包

举个🌰

```javascript
<input type="text" id="input" />
  
// 防抖函数
const debounce = (delay) => {
  let timer;
  return (value) => {
    clearTimeout(timer);
    timer = setTimeout(() => {
      console.log(value);
    }, delay);
  };
};

let input = document.getElementById('input');
let debounceFn = debounce(1000);
input.addEventListener('keyup', e => {
  debounceFn(e.target.value);
});

```

### 节流函数

当持续触发事件的时候，保证一段时间内 只调用一次事件处理函数，一段时间内，只做一件事情

举个🌰

```javascript
<input type="button" id="button" />

const throttleFn = (callback, delay) => {
  let timer;
  return () => {
    if (!timer) {
      timer = setTimeout(() => {
        callback();
        timer = null;
      }, delay)；
    };
  };
};

const fn = () => {
  console.log(Math.random());
};

documnet.getElementById('button').onclick = throttleFn(fn, 1000);
```

















