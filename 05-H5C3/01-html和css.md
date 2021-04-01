# html学习

## HTML简介

Hypertext    Markup  Language    超文本标记语言

### 历史

- 1993年6月：HTML第一个版本发布
- 1995年11月： HTML 2.0
- 1997年1月：HTML 3.2（W3C推荐）
- 1999年12月：HTML 4.01（W3C推荐）
- 2000年底：XHTML 1.0（W3C推荐）
- 2014年10月：HTML 5（W3C推荐）

现在广泛使用的有99年的HTML 4.01，2000年的XHTML 1.0，以及14年的HTML 5，为了让浏览器知道我们的网页是那种类型的，往往需要在网页开始之前加上`<!doctype html>`，此声明是`HTML 5`，避免同一网页在不同的浏览器中出现怪异模式

## 产生乱码的原因

编码和解码采用的字符集不同

常见字符集

- ASC标签
- ISO-8859-1
- GBK
- GB2312
- UTF-8
- ANSI    自动以系统的默认编码来保存文件

## 标签

`<meta />`   元标签  自结束标签    设置元数据

- name属性
  - keywords    关键字
  - description    描述
- content属性，用来描述name

可以使用  meta  标签做请求重定向 5是时间，url为去向

`<meta http-equiv="refresh" content="5;url=http://www.baidu.com"/>`

我们使用标签，只关心语义

- 标题标签
- 段落标签
- 换行标签  `<br />`
- 水平线标签 `<hr />`
- 实体
- 图片标签
  - src属性：设置一个外部图片的路径
  - alt属性：可以用来设置图片的描述，图片不能显示的时候，也可以供搜索用。搜索引擎可以通过alt属性，来识别不同的图片
  - width
  - height
  - 图片格式：
    - JPEG   支持颜色多，可以压缩，不支持透明，用来保存色彩照片
    - png     支持颜色多，支持复杂透明
    - gif       支持颜色少，只支持简单的透明，支持颜色单一，使用动态图
- `<iframe></iframe>`内联框架   可以通过  src  属性引入一个  html  页面
- 超链接
  - href  属性：指向链接跳转的目标地址
  - target 属性：可以用来指定打开链接的位置  _blank值在新窗口打开
  - 可以用  id  来设置锚点      href=“#id”  即可点击链接后，到达该锚点
  - 可以使用  href  属性，打开计算机默认电子邮件客户端  href=“tomail：邮箱”

- `em`
- `strong`
- `i`
- `b`
- `cite`   表示参考内容
- `q`      表示一个短引用
- `blockquote`    表示一个块引用
- `sup `   上标 
- `sub`   下标
- `del`
- `ins`   会自动添加下划线
- `pre`   预标签   用于代码格式
- `code`      pre   和   code   通常一块使用
- 列表标签
  - 无序列表   `ul   li`
  - 有序列表   `ol   li`
  - 定义列表   `dl   dt    dd`
  - 

## 属性

属性只能写在开始标签中，以键值对的形式

一个标签可以使用多个属性，但是需要用空格隔开

- title   提示信息

## XHTML规范

- HTML不区分大小写，一般使用小写
- HTML中的注释不能嵌套
- HTML标签必须结构完整
- HTML标签可以嵌套，但是不能交叉使用
  - 标签中的属性必须有值，且必须加引号，值最好使用双引号

## 块元素

- `div`
- `p`                  不可以包含块元素
- `h1`
- `br`

## 行间块状元素

- `span`           不可以包含块元素
- `a`                 可以包含任何元素，除了本身
- `img`

# HTML学习

## Web标准

Web标准是由  W3C 组织和其他标准化组织制定的一系列标准的集合。W3C（万维网联盟）是国际最著名的标准化组织

- 为什么需要  web  标准：浏览器不同，他们显示的页面或者排版就有些许差异，有以下优点
  - 让  Web  发展前景更广阔
  - 内容能被广泛的设备访问
  - 更容易被搜索引擎搜索
  - 降低网站流量费用
  - 是网站更容易维护
  - 提高页面浏览速率

- web  标准的构成
  - 结构
  - 表现
  - 行为

## HTML标签

### HTML语法规范

- HTML  标签是由尖括号包围的关键词
- HTML  标签通常是成对出现的，开始标签和结束标签
- 有些特殊的  HTML  标签是单个标签，最好自结束

### 标签关系

- 包含
- 并列

### HTML的基本结构标签（骨架标签）

骨架标签：有四个

```html
<html>
    <head>
        <title>键盘敲烂，工资过万</title>
    </head>
    <body>
        写代码是一件非常快乐的事
    </body>
</html>
```

### <!DOCTYPE>标签

文档声明标签，作用就是告诉浏览器使用哪种  html  版本来显示网页

`<!DOCTYPE html>`

### lang语言

用来定义当前文档的显示语言，中文网站还是英文网站，并不影响文档里面的字符，不管是什么，都可以写英文和中文

**提倡**：zh-CN

- en  就是英文
- zh-CN  就是中文

`<html lang="en"></html>`

### charset字符集

字符集是多个字符的集合，以便计算机能够识别和存储各种文字

`<meta charset="utf-8" />`

常见的：GB2312、BIG5（繁体中文）、GBK（国标）、UTF-8（万国码）

### HTML常用标签

#### 语义标签

- 标题标签  `<h1></h1>  --  <h6></h6>`
- 段落标签  `<p></p>`

- 换行标签  `<br />`

#### 文本格式化标签

推荐使用后者，语义更强烈

- 粗体：`<b></b>`  `<strong></strong>`
- 斜体：`<i></i>`  `<em></em>`
- 下划线：`<u></u>`  `<ins></ins>`
- 删除线：`<s></s>`  `<del></del>`

#### 无语义常用标签

- div  块状   **大盒子**
- span  行间块状  **小盒子**

#### 图像标签和路径

src  是属性，路径加文件名

- 图像标签：`<img src="图像URL"  width="500" />`

图片标签的其他属性

| 属性   | 属性值   | 说明                                       |
| ------ | -------- | ------------------------------------------ |
| src    | 图片路径 | 必须属性                                   |
| alt    | 文本     | 替换文本，图片不能显示时出现               |
| title  | 文本     | 提示文本，鼠标放在标签上边，显示出来的文字 |
| width  | 像素     | 图片的宽                                   |
| height | 像素     | 图片的高                                   |
| border | 像素     | 图片的边框                                 |

**注意**

- 属性不分先后顺序，属性之间用空格隔开
- 属性以键值对的形式书写，`key="value"`

**路径**

相对路径：同一级路径、上一级路径、下一级路径  `/`

绝对路径：通常从磁盘开始  `\`

#### 超链接标签

`<a href="跳转目标" target="目标窗口的弹出方式">百度</a>`

| 属性   | 作用                                                         |
| ------ | ------------------------------------------------------------ |
| href   | 用于指定链接目标地址的URL，当为标签添加了这个属性，他就具有超链接的功能 |
| target | 用于指定超链接的打开方式，\_self为默认值，\_blank为在新窗口打开 |

**链接分类**

- 外部链接：`<a href="http://www.qq.com">腾讯</a>`
- 内部链接：`<a href="./index.html"></a>`

- 空链接：`<a href="#"></a>`  `<a href="javascript:;"></a>`
- 下载链接：`<a href="./smile.zip"></a>`  通常是  `.exe .zip`  文件类型
- 网页元素链接：在网页中的元素，如文本、图像、表格、音频、视频都可以加超链接
- 锚点链接：点击链接，可以快速定位到页面中的某个位置
  - 在链接文本的  href  属性中，设置属性值的名字  `<a href="#app">跳到app处</a>`
  - 在目标位置的标签，添加  id  属性  `<h1 id="app">我是app，会跳到我这里来</h1>`

#### HTML中的注释和字符

**注释标签**--`<!-- -->`

**特殊字符**

| 特殊字符 | 描述     | 代码    |
| -------- | -------- | ------- |
| 空格     | 空格     | \&nbsp; |
| <        | 小于号   | \&it；  |
| >        | 大于号   | \&gt    |
| ©        | 版权     | \&copy; |
| ￥       | 人民币   | \&yen;  |
| &        | 和号     | \&amp;  |
| 上标     | 上标     | \&sup;  |
| 下标     | 下标     | \&sub;  |
| 注册商标 | 注册商标 | \&reg;  |

#### 表格标签

**表格作用：**以前用来布局页面，现在用来显示、展示数据

```html
<table>表
    <tr>行
        <td rowspan="跨行合并">单元格1</td>
        <td colspan="跨列合并">单元格1</td>
    </tr>
</table>
```

**表头单元格**（table header）--  `<th>  </th>`   加粗居中

**表格头部单元格**（table head）--  `<thead>  </thead>`  内部必须有  `tr`  标签

**表格结构单元格**(table body)  --  `<tbody>  </tbody>`

**表格属性**

| 属性名      | 属性值              | 描述                                  |
| ----------- | ------------------- | ------------------------------------- |
| align       | left、center、right | 表格相对周围元素的对齐方式            |
| border      | 1或""               | 单元格是否有边框                      |
| cellpadding | 像素                | 单元格边沿与内容之间的空白，默认1像素 |
| cellspacing | 像素                | 单元格之间的空白，默认2像素           |
| width       | 像素值或百分比      | 表格宽度                              |
| height      | 像素或百分比        | 表格高度                              |



#### 列表标签

**1、无序列表**

```html
<ul>
	<li></li>
  <li></li>
</ul>
```

**2、有序列表**

```html
<ol>
    <li></li>
    <li></li>
</ol>
```

**3、自定义列表**

```html
<dl>
    <dt></dt>
    <dd></dd>
</dl>

<!-- dl中只能使用dt和dd -->
```

#### 表单标签

用来收集用户信息，与用户交互

组成：表单域、表单控件、提示信息

**表单域**

```html
<form action="http://127.0.0.1:3000/demo.html" method="GET" name="form1">
    
</form>
```

**表单元素**

- 输入表单元素  **单标签**

- 选择表单元素
-  textarea文本域元素：多行文本输入

**表单元素属性**

| 属性      | 属性值       | 描述             |
| --------- | ------------ | ---------------- |
| type      | text、button | 表单类型         |
| name      | 自定义       | 表单名称         |
| value     | 自定义       | 表单值           |
| checked   | checked      | 是否被选择被选中 |
| maxlength | 正整数       | 最大字符长度     |

表单元素常与  `label`  标签一起使用：使用场景，点击文字定位到相应表单

```html
<form>
    <input type="text" name="">
    <input type="button" name="">
    <input type="file" name="">
    <input type="hidden" name="">
    <input type="image" name="">
    <input type="password" name="">
    <input type="radio" name="">     单选，有一个相同的名字
    <input type="checkbox" name="">  复选，有一个相同的名字
    <input type="reset" name="">
    <input type="submit" name="">
</form>
```



**选择表单元素**

```html
<form>
    <select>
        <option selected="selected"></option>    默认选中
    </select>
</form>
```



**文本域表单**

```html
<form>
    <textarea rows="5" cols="50">   可以写五行，每行50字符
    
    </textarea>
</form>
```



# CSS

层叠样式表（Cascading Style Sheets）

css由选择器和一个或者多条声明构成

## CSS样式风格

- 展开格式
- 小写
- 空格

## CSS基础选择器

单个组成

- 标签选择器
- 类选择器
- id选择器
- 通配符选择器

## CSS字体属性

用于定义：字体系列（宋体）、大小、粗细、文字样式（斜体）

```css
font-family: 'Microsoft YaHei';
font-size: 20px;
font-weight: 700;
font-style: italic;
```

### 字体复合属性简写

```css
font: font-style font-weight font-size/line-height font-family;
```

**size  和  family **不能省略

## CSS文本属性

用于定义文本外观：颜色、对齐、装饰、缩进、行间距

```css
color: pink;
text-align: center;  水平  左中右
text-decoration: underline; 下划线，删除线（line-through），上划线(overline)，none
text-indent: 2em;  em是相对于当前元素文字大小决定的，如果当前元素字体没有大小，则按照父元素字体
line-height: 
```

## CSS引入方式

- 行内样式表（行内式）
- 内部样式表（嵌入式）
- 外部样式表（链接式）

### 三种引入方式总结

| 样式表 | 优点             | 缺点         | 使用情况 | 控制范围 |
| ------ | ---------------- | ------------ | -------- | -------- |
| 行内   | 权重高           | 结构样式混写 | 少       | 一个标签 |
| 内部   | 部分结构样式分离 | 没有彻底分离 | 较多     | 一个页面 |
| 外部   | 完全结构样式分离 | 需要引入     | 最多     | 多个页面 |

## emmet语法

前身Zen coading

- 快捷生成标签
- 快速生成多个标签
- 父级关系 `>`
- 兄弟关系 `*`
- 带有类名
- 自增  `$`
- 标签内生成内容  `{}`

- 像素宽
- 像素高

- 快速格式化

## CSS复合选择器

- 后代选择器：`ol li`
- 子选择器:   `ol > li`
- 并集选择器:  `ol,ul`
- 交集选择器: `div.myclass`
- 伪类选择器：

  - 链接伪类选择器

    - `a:link`
    - `a:visited`
    - `a:hover`
    - `a:active`

  - 结构伪类选择器

  - 表单伪类选择器
  
    - `input:focus`

## CSS元素显示模式

显示模式：以什么方式显示，有的标签独占一行，有的一行可以放多个

- 块元素
- 行内元素

### 块元素

`<h1>--<h6>    <p>    <div>   <ul>    <ol>    <li>`

特点：

- 独占一行
- 宽高、内外边距可以控制
- 宽度默认是容器的100%
- 本身多为容器，里面可以放块元素和行内元素

### 行内元素

`<a>  <strong>  <b>  <em>  <i>  <del>  <s>  <ins>  <u>  <span>`

特点：

- 一行可以显示多个
- 宽高直接设置无效
- 默认宽度为内容本身的宽度
- 行内元素内部之能是文本或者其他行内元素

### 行内块元素

`<img>  <input>  <td>`

特点：

- 一行可以显示多个，中间有缝隙
- 宽高、内外边距可控制
- 默认宽度为内容本身宽度

## CSS背景

可以设置背景颜色、背景图片、背景平铺、背景图像固定

```css
div {
    background-color: transparent | color;
    background-image: url(./deom.jpeg) | null;
    background-repeat: no-repeat | repeat | repeat-x | repeat-y;
    background-position: x  y; x y是坐标，可以跟方位名词，也可以是精确单位
    background-attachment: fixed | scroll
}
方位名词：left center rigth  top center bottom   方位名词的前后无顺序,只写一个，另一个自动居中
精确单位：有先后顺序，只有一个参数，另外一个是居中
混合单位：background-position: 20px center  第一个是x，第二个是y


简写：没有特定顺序
div {
    background: color image repeat attachment position
}
```



## CSS三大特性

### 层叠性

长江后浪推前浪，前浪死在沙滩上

### 继承性

颜色和字号  龙生龙，凤生凤，老鼠的孩子会打洞

- text-
- font-
- line-

### 优先级

- 选择器相同，则执行层叠性
- 选择器不同，则根据权重

**复合选择器会权重叠加，需要计算权重**

| 选择器               | 选择器权重 |
| -------------------- | ---------- |
| 继承、通配           | 0,0,0,0    |
| 元素选择器           | 0,0,0,1    |
| 类选择器、伪类选择器 | 0,0,1,0    |
| ID选择器             | 0,1,0,0    |
| 行内样式             | 1,0,0,0    |
| !important           | 无穷大     |

## CSS盒子模型

布局要学习的三大核心：盒子模型、浮动、定位

**盒子**：边框、外边距、内边距、实际内容

## 外边距合并问题

### 相邻块元素垂直外边距合并

**相邻盒子外边距合并问题**：经过计算两个盒子中间的距离为  300px，但实际上是  200px，以大像素为准

第一个盒子：`margin-bottom: 100px`

第二个盒子：`margin-top: 200px`

```html
<div class="one">第一</div>
<div class="two">第二</div>
```

**解决方案**：只给一个盒子设置  `margin`  值

### 嵌套块元素垂直外边距合并

**嵌套外边距合并塌陷问题**：父盒子和子盒子，同时使用  `margin-top`   会使父盒子跟随子盒子移动

父盒子：`margin-top: 100px`

子盒子：`margin-top: 100px`

```html
<div class="father">
	<div class="son"></div>
</div>
```

**解决方案**：

- 为父元素定义上边框
- 为父元素定义内边距
- 可以为父元素添加  `overflow: hidden`

## 盒子阴影

`box-shadow: h-shadow  v-shadow  blur  spread  color  inset`

| 值       | 描述                       |
| -------- | -------------------------- |
| h-shadow | 必须  水平  允许负值       |
| v-shadow | 必须  垂直  允许负值       |
| blur     | 可选  模糊距离             |
| spread   | 可选  阴影尺寸             |
| color    | 可选  阴影颜色             |
| inset    | 可选  外部阴影改为内部阴影 |

## 文字阴影

`text-shadow: h-shadow  v-shadow  blur  color`



## CSS浮动

### 传统网页的三种布局方式

- 标准流
- 浮动流
- 定位流

### 为什么需要浮动

​	很多布局效果，只靠标准流无法完成，可以实现块级元素横向排列

### 浮动元素特性

- 浮动后的元素，则该元素具有行内块元素特性

- 浮动的元素之间，没有空隙

## 定位

`position: fixed;`

可以实现某个元素在盒子中任意移动

| 值       | 语义     | 描述                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| static   | 静态定位 | 标准流                                                       |
| relative | 相对定位 | 定位流  相对自己                      占用原来位置           |
| absolute | 绝对定位 | 定位流  父级第一个定位元素  不占用原来位置                   |
| fixed    | 固定定位 | 定位流  浏览器可视窗口          不占用原来位置               |
| sticky   | 粘性定位 | 定位流  浏览器可视窗口          占用原来位置<br />必须添加  top 或 bottom  或  left   或  right |

### 定位叠放次序  --  z-index

### 定位特性

- 行内元素，可以直接设置宽高
- 块级元素，默认是内容宽度和高度

## 元素的显示与隐藏

### display显示隐藏

显示：  `display: block;`

隐藏：  `display: none;`  不占原位置

### visibility显示隐藏

显示：`visibility: visible;`

隐藏：`visibility: hidden;`  保留原位置

### overflow显示隐藏

显示：`overflow: visible;`

隐藏：`overflow: hidden;`

## 精灵图

减少服务器接收和发送请求的次数

```css
background-position: 0 -10px;
```

## 字体图标

## 用户界面样式

### 鼠标样式

`cursor: pointer;`

| 属性值      | 描述           |
| ----------- | -------------- |
| pointer     | 小手           |
| default     | 默认  小白箭头 |
| move        | 移动           |
| text        | 文本           |
| not-allowed | 禁止           |

### 表单轮廓线

`outline: none;`

### 防文本域拖拽

`resize: none;`

## vertical-align

行内或者块

| 属性     | 描述     |
| -------- | -------- |
| baseline | 基线     |
| top      | 顶部     |
| middle   | 垂直居中 |
| bottom   | 底部     |

## 图片底侧空白缝隙问题

原因：图片默认与文字基线对齐

解决方案：

- 使用  `vertical-align`
- 使用  `display: block;`

## 文字溢出省略号

```css
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```

## 多行文本最后一行显示省略号

```css
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;  显示几行文本
-webkit-box-orient: vertical; 子元素排列方式
```

## 常见布局技巧

### margin负值运用

### 文字围绕浮动元素

### 行内块元素巧妙运用

### css三角强化

## CSS初始化



# H5

## H5新特性   IE9+

### 新增标签

- 头部标签  header
- 导航标签  nav
- 内容标签  article
- 区域标签  section
- 侧边栏标签  aside
- 底部标签  footer

### 新增多媒体标签

- 音频标签  audio

```html
<audio src="./ha.mp3" controls></audio>

兼容写法
<audio>
	<source src="./ha.mp3">
</audio>
```

- 视频标签  vidio

```html
<vidio src="./ha.mp4" controls autoplay="autoplay" muted="muted"></audio>
muted 静音

兼容写法
<audio>
    <source src="./ha.mp4">
    <source src="./ha.ogg">
</vidio>
```

### 新增表单

input新增type属性

```html
<input type="search">
<input type="email">
<input type="url">
<input type="date">
<input type="time">
<input type="month">
<input type="week">
<input type="number">
<input type="tel">
<input type="color">
```

### 新的表单属性

| 属性         | 值        | 说明               |
| ------------ | --------- | ------------------ |
| required     | required  | 表单必填           |
| placeholder  | 提示文本  | 表单提示信息       |
| autofocus    | autofocus | 表单自动聚焦       |
| autocomplete | off/on    | 表单记忆           |
| multiple     | multiple  | 可以选多个文件提交 |

# CSS3

## CSS3新特性  IE9+

### 新增选择器

#### 属性选择器

| 选择符        | 简介                                |
| ------------- | ----------------------------------- |
| E[att]        | 选择具有att属性的E元素              |
| E[att="val"]  | 选择具有att属性，且值为val的E元素   |
| E[att^="val"] | 匹配具有att属性且值以val开头的E元素 |
| E[att$="val"] | 匹配具有att属性且值以val结尾的E元素 |
| E[att*="val"] | 匹配具有att属性且值中含有val的元素  |

```css
input[value] {
    
}
```

#### 结构伪类选择器

| 选择符           | 说明                        |
| ---------------- | --------------------------- |
| E:first-child    | 匹配父元素中的第一个子元素E |
| E:last-child     | 匹配父元素中最后一个E元素   |
| E:nth-child(n)   | 匹配父元素中的第n个子元素E  |
| E:first-of-type  | 指定类型E的第一个           |
| E:last-of-type   | 指定类型E的最后一个         |
| E:nth-of-type(n) | 指定类型E的第n个            |

```css
ul li:first-child {
    选择ul中第一个小li
}

ul li:nth-child(even) {
    选择ul中偶数个小li
}
```

**nth-child(n)**：选择某个父元素的一个或多个特定的子元素

- n可以是数字、关键字和公式
- n如果是数字、就是选择第n个子元素，里面数字从1开始
- n可以是关键字：even偶数，odd奇数
- n可以是公式：常见公式如下（如果n是公式，则从0开始，但是第0个元素或者超出了元素的个数被忽略）

| 公式 | 取值                |
| ---- | ------------------- |
| 2n   | 偶数                |
| 2n+1 | 奇数                |
| 5n   | 5   10   15  ...    |
| n+5  | 从第5个开始依次递增 |
| -n+5 | 前5个（包含第五个） |

#### 伪元素选择器

伪元素选择器，可以帮助我们利用  CSS  创建新的标签元素，而不需要标签，从而简化  HTML  结构

| 选择符   | 说明                 |
| -------- | -------------------- |
| ::before | 在元素的前边插入内容 |
| ::after  | 在元素的后边插入内容 |

特性：

- before  和  after创建的元素，属于行内元素
- 新创建的元素在文档中是找不到的，所以我们称为伪元素
- 语法：`element::before{}`
- before  和  after  必须有  content  属性
- 伪元素选择器和标签选择器一样，权重为1

### C3盒子模型

CS盒子模型的宽高就是盒子的宽高，不会变

### 其他特性

#### CSS3滤镜filter  图片模糊

filter  CSS属性将模糊或颜色偏移等图形效果应用于元素

`filter:  函数();`

例如：`filter: blur(5px);`  blur模糊处理  数值越大越模糊

#### CSS3  calc函数

calc()  此函数让你在声明CSS属性值时执行一些计算

`width: calc(100% - 100px);`

## CSS3过渡

`transition: 要过渡的属性  花费的时间  运动曲线  何时开始；`

**谁要过渡给谁加**

**如果想要写多个属性，用逗号分隔**

- 属性：想要变化的  css  属性，宽度高度  背景颜色  内外边距都可以。想要所有属性都过渡，写个  all  就可以
- 花费时间：单位是秒（必须写单位）比如  0.5s
- 运动曲线：默认是  ease（可以省略）
- 何时开始：单位是秒（必须写单位）可以设置延迟触发事件  默认是  0s（可以省略）













