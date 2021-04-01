# JavaScript基础学习

- JavaScript严格区分大小写
- `0x`  开头是  16进制
- `0`  开头是  8进制
- `0b`  开头是 2进制   少有浏览器支持

## 变量

<img src="H:\06-Web前端\06-笔记\00-images\var.png" alt="变量" style="zoom:60%;" />

<img src="H:\06-Web前端\06-笔记\00-images\totalvar.png" alt="变量小结" style="zoom:60%;" />

变量的数据类型：只有右边的值确定后，才能确定

### 变量销毁

- 全局作用域下，当关闭浏览器按钮时，变量会自动销毁
- 局部作用域下，函数执行完后，变量会自动销毁

## 标识符

在JavaScript中，我们可以自主命名的称为标识符

- 变量名，函数名，属性名都属于标识符
- 标识符命名规则
  - 可以有字母、数字、下划线、$
  - 不能以数字开头
  - 不能是关键字或保留字
  - 采用驼峰命名法

## 数据类型

数据类型就是字面量类型，一共有6中类型：String、Number、Boolean、Null、Undefined、Object

String、Number、Boolean、Null、Undefined是简单数据类型，或者基本数据类型

Object属于复杂数据类型，或者应用数据类型

- `typeof  变量名`  用来检查一个变量的数据类型

<img src="H:\06-Web前端\06-笔记\00-images\vartype.png" style="zoom:60%;" />

### String字符串

- 在字符串中  `\`  可以转义字符

- `\n`  表示换行
- `\t`  制表符

### Number数字型

包括整数和浮点数

- 最大值  `Number.MAX_VALUE`，超过这个最大值，返回无穷大  Infinity
- 大于零的最小值，也就是最小整数  `Number.MIN_VALUE`，想要真正的最小值，加上  负号
- NAN  是一个特殊的数字  `Not A  Number`
- JavaScript计算基本的整数运算，可以保证正确，但是浮点数就不容易精确

### Boolean布尔类型

用来做逻辑判断

- true  计算当  1
- false  计算当  2

### Null

null专门表示一个空对象

`typeof null `   返回  object

### undefined

声明未赋值就是  `undefined`

为生命就赋值直接用会报错  `xx is not defined`



## 强制数据类型转换

类型转换主要是指：string，number，Boolean

- 转为字符串
  - 调用  toString  方法  `let b = a.toString()` ，返回值为字符串，需要新变量接收；不改变  a  本身的数据类型。注意：null  和  undefined  没有  toString方法
  - 调用  String  函数    `let a = String(a)`   把  a  当参数，传递给String函数中。注意：null  和  undefined可以使用  String  函数，会 直接转化为  `"null"`  和  `"undefined"`
- 转化为数字型
  - 字符串  ->  数字
    - 使用  Number  函数
    - 如果是纯数字的字符串，直接转化为数字
    - 如果字符串有非数字内容，则直接转换为  NaN
    - 如果字符串为空或者是空格，则转化为  0
  - 布尔值  ->  数字
    - 使用  Number  函数
    - true  转为  1
    - false  转为  0
  - null  ->  数字
    - 使用  Number  函数
    - null  转为  0
  - undefined  ->  数字
    - 使用  Number  函数
    - undefined  转为  NaN
  - 使用  parseInt  和  parseFloat  函数
    - 专门用来对付字符串的
    - 开头是数字，后边是字母的字符串  例如  `128px`
    - 如果对非字符串使用这两个方法，会先将其转为字符串，在转为数字，所以，布尔型用此方法会使NaN
    - 可以用  parseInt  函数取整
    - 第二个参数表示  进制  可以是   8，10，16
- 转化为布尔值
  - 数字型  ->  Boolean
    - 除了  0  和  NaN，其余的都为  true
  - 字符串  ->  Boolean
    - 除了空字符串，其余的都为  true
  - null，undefined  ->  Boolean   都是  false
  - 对象也会转为  true



## 运算符

运算符也叫操作符，通过运算符可以对一个或者多个值进行运算并获取运算结果，例如  `typeof  `  就是运算符

- `typeof`  返回值是字符串，返回值为  String、Number、Boolean、Undefined、Object
- 算数运算符  `+ - * / %  ++  --`
  - 当对非  number  类型的值进行运算时，会先转化为  number  类型，在进行运算
  - null  进行计算，本身为 0 
  - NaN  进行计算，结果都为  NaN
- 赋值运算符  `=  +=  -=  *=  /=  %=`
- 比较运算符  `==  ===  !=  !==  <  >  <=  >=  ?`
  - 数值情况
    - 如果关系成立返回  true，不成立返回  false
  - 非数值情况
    - 对于非数值进行比较，会将其转化为**数字**进行比较
    - 任何数和  NaN  比较都是  false
    - 如果符号两侧的值都是字符串，不会将其转化为数字进行比较，而会比较字符串中字符的  Unicode  编码，一位一位进行比较
  - NaN  不和任何值相等，包括自己
    - `isNaN()`  检查一个值是不是  NaN
  - 全等于不会类型转换

- 逻辑云算符  `&&  ||  !`
  - 为任意数据类型，连续两次取反，即可将其转化为布尔值
  - 逻辑中断   非布尔值运算
    - ` 1 && 2`  1为真，返回2      1  为假，返回  1
    - `1 || 2`  1为真，返回1      1  为假，返回  2
- 类型运算符  `typeof  instanceof`
- 位运算符  `& | ~  ^  <<  >>  >>>`



## 流程控制

### 条件

- if
- 条件分支语句  switch

### 循环

- for
- while
- do  while

### break  continue

- break  跳出循环
- continue  跳出当前循环

## 节点

|          | nodename  | nodeType | nodeValue |
| -------- | --------- | -------- | --------- |
| 文档节点 | #document | 9        | null      |
| 元素节点 | 标签名    | 1        | null      |
| 属性节点 | 属性名    | 2        | 属性值    |
| 文本节点 | #text     | 3        | 文本内容  |





## 数组--经典算法思路

### 把数组转化为字符串

```javascript
// 思想：遍历拼接

let arr = ['pink', 'blue', 'dag', 'db']

let str = ''
for (let i = 0; i < arr.length; i++) {
    str += arr[i] + '|'
}
consolt.log(str)
```

### 数组中新增元素

#### 通过修改  length  长度新增数组元素

```javascript
let arr = ['red', 'green', 'blue']
arr.lenght = 4
// 修改了长度，就会空出一个empty，类型是 undefined
arr[3] = 'dag'
```

#### 修改索引号

```javascript
// 追加元素
let arr = ['red', 'green', 'blue']

arr[3] = 'dag'
```

### 筛选数组

思想：声明一个新数组，遍历旧数组，设置条件，符合条件的放入新数组中

### 删除指定数组元素

思想：声明一个新数组，遍历旧数组，设置条件，符合条件的放入新数组中

### 翻转数组

```javascript
// 声明一个新数组
// 得到旧数组的最后一个索引号  arr.length - 1，再得到新数组的第一个索引号 newArr.length
// i-- 遍历旧数组
// 两个索引号互换

let arr = ['red', 'green', 'blue']
let newArr = []
for (let i = arr.length - 1; i >= 0; i--) {
    newArr[newArr.length] = arr[i]
}
```

### 数组排序（冒泡排序）

```javascript
// 外层循环是趟数，内层循环是次数
长度 - 趟数 - 1 = 次数   arr.length - i -1 = j

for (let i = 0; i <= arr.length - 1; i++) {
    for (let j = 0; j <= arr.length - i - 1; j++) {
        if (arr[j] > arr [j + 1]) {
            let temp = arr[j]
            arr[j] = arr[j + 1]
            arr[j + 1] = temp
        }
    }
}
```

## 函数

函数就是封装了一段可重复使用的代码块

return   返回给函数的调用者  还有终止函数的功能

没有返回值就是  undefined

## 作用域

作用域：就是代码名字在某个范围内起作用和效果    主要是  变量

- 全局作用域
- 局部作用域（函数作用域）

作用域链：内部函数访问外部函数的变量，采取的是链式查找的方式来决定取那个值，js在预编译时访问的

## 预解析

js引擎：先预解析，然后执行

- 变量预解析
- 函数预解析  函数本身全部放到最前边

### 预解析步骤

- 函数作用域

  - 创建AO对象
  - 找形参和变量声明，将变量和形参名当作AO对象属性名值为undefined
  - 实参形参相统一
  - 在函数体里找函数声明，值赋予函数体

  ```javascript
  function fn(a, c) {
    console.log(a); // function a() {}
    var a = 123;
    console.log(a); // 123
    console.log(c); // function c() {}
    function a() {};
    if (false) {
      var d = 678;
    };
    console.log(d); // undefined
    console.log(b); // undefined
    var b = function () {}; // 非函数声明
    console.log(b); // function() {}
    function c() {};
    console.log(c); // function c() {}
  };
  fn (1, 2);
  AO {
    a: undefined, 1， function a(){},
    c: undefined, 2， function c() {},
    d: undefined,
    b: undefined,
  }
  ```

- 全局作用域
  - 创建GO对象

## 对象

### 创建对象

- `let obj = {}`
- `let obj = new Object()`
  - 追加属性
  - obj.name = 'dag'
  - obj.sayHi = function () {    }
- 构造函数

### 使用对象

- `obj.name`
- `obj['name']`
- `obj.sayHi()`  记得加小括号

### 遍历对象

```javascript
for (let k in obj) {
    console.log(obj[k])
    // k  是属性
    // obj[k]  是属性值
}
```





## 构造函数

封装对象的函数叫构造函数     构造函数不用  return   必须使用  new  调用

new  会做的四件事

- new  在内存中创建了一个空对象
- this  指向这个空对象
- 执行代码，添加属性和方法
- 返回这个新对象

创建对象

```javascript
function 构造函数名() {
    this.属性 = 值;
    this.方法 = function () {    }
}

new 构造函数名
```



## js内置对象

js中对象分三种：自定义对象，内置对象、浏览器对象

### Math  对象

### Date  对象

- 获取时间戳
  - `Date.now()`
  - `+new Date()`

### 数组对象

- `let arr = new Array(2)`  是说  arr  这个数组的长度为2  有两个空元素
- `let arr = new Array(2, 3)`  是说  arr  这个数组有两个元素   分别是  2  和  3

**判断是不是数组**

- `arr instanceof Array`  判断  arr  是不是数组
- `Array.isArray(arr)`   判断  arr  是不是数组

**添加元素**

- `arr.push('dag')`  返回的结果是数组新长度，原数组也会发生变化
- `arr.unshift('dag')`  返回值是数组新长度，原数组也会发生变化

**删除元素**

- `arr.pop()`  删除数组的最后一个元素，返回值为删除的那个元素，原数组发生变化
- `arr.shift()`  删除数组的第一个元素，返回值为删除的那个元素，原数组发生变化

**数组排序**

- `arr.reverse()`   返回值为颠倒顺序的数组   实质就是把原数组翻转
- `arr.sort()`         就是把原数组按升序或者降序排列后返回

**查找索引**

- `arr.indexOf('dag')`   返回第一个满足条件的索引号   找不到元素的话就返回  -1    **数组去重**
- `arr.lastIndexOf('dag')`  倒着查

```javascript
// 数组去重

// 原理：遍历旧数组，拿着旧数组的元素去和新数组中的元素查找（用indexOf（）方法），把不重复的元素追加到新数组


const arr = ['red', 'green', 'blue']
const newArr = []
for (let i = 0; i < arr.length; i++) {
    if (newArr.indexOf(arr[i]) === -1) {
        newArr.push(arr[i])
    }
}
```

**数组转为字符串**

- `arr.toString()`
- `arr.join('&')`  可以写上想要的分隔符，默认是逗号



### 字符串对象

- 基本包装类型：为什么简单数据类型具有  length  属性，就是默认自动把简单数据类型包装成复杂数据类型

- 字符串的不可变：字符串重新赋值后，虽然看上去内容变了，但实际上是内存地址变了，内存中新开辟了一个空间，所以不要大量的对字符串重新赋值，也不要大量的拼接字符串

- 字符串的所有方法都不会修改字符串本身，操作完成后会返回一个新字符串

**根据字符返回索引**

- `str.indexOf()`

- `str.lastIndexOf()`

  ```javascript
  // 返回一个字符串中特定字符的位置以及次数
  
  // 核心算法：先找出第一个字符出现的位置，然后只要indexOf()的返回值不是-1，就继续往后查找。因为indexOf只能查找的第一个，所以后边的查找，一定是当前索引+1，继续查找
  
  const str = 'sfkjsdfklsjdklgjsa'
  let index = str.indexOf('s')
  let num = 0
  while (index !== -1) {
      console.log(index)
      num++
      index = str.indexOf('s', index + 1)
  }
  console.log('s出现的次数是:' + num)
  ```

  

**根据索引返回字符**--**遍历字符串**

`str.charAt()`

```javascript
let str='slkklsjgks'
for (let i = 0; i < str.length; i++) {
    console.log(str.charAt(i))
}
```

```javascript
// 找出一个字符串中出现最多次数的字符并统计次数

// 核心算法
// 用charAt()，遍历整个字符，把每个字符都存储给对象，如果没有这个属性，就把这个属性的值写为一，如果有就+1
// 遍历对象，找出最大值和该字符
var str = 'sjlkjfklsdjglkasjkl'
var o = {}
for (var i = 0; i <= str.length; i++) {
    var char = str.charAt(i)
    if (o[char]) {
        o[char]++
    } else {
        o[char] = 1
    }
}

var max = 0
var dag = ''
for (k in o) {
    if (o[k] > max) {
        max = o[k]
        dag = k
    }
}

console.log('出现最多的字符是' + dag + '-' + '次数是' + max)
```



## 堆和栈

- JavaScript本身没有堆和栈     内存分为  堆 和 栈

js分为简单数据类型和复杂数据类型

- 简单数据类型   值类型
  - Number、String、Boolean、undefined、null
  - 存放在栈里面
- 复杂数据类型   引用数据类型
  - new 出来的     Array、Object、Function
  - 现在栈里面存放十六进制的地址，然后这个地址指向堆里面的数据



### 简单数据类型传参

- 形参与实参互不干扰

<img src="H:\06-Web前端\06-笔记\00-images\easy-args.png" style="zoom:60%;" />



### 复杂数据类型传参

- 在栈中只有地址的变化

<img src="H:\06-Web前端\06-笔记\00-images\complex-args.png" style="zoom:60%;" />

