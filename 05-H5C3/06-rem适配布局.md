# rem适配布局

## rem基础

### rem单位

- rem（root  em）是一个相对单位，类似于  em  ，em是父元素字体大小

- rem  是相对于  html  元素的字体大小

## 媒体查询

媒体查询可以根据不同的屏幕尺寸变成不同的样式

媒体查询是（media  query）

- 语法规范

```html
@media mediatype and | not |only (media, feature) {
	css-code
}
```

- 用  @media   开头，注意  @  符号
- mediatype   媒体查询类型
  - all
  - print  打印机
  - screen  屏幕，电脑屏幕，手机屏幕，平板电脑
- 关键字  and  not  only
- media  feature  媒体特征，必须有包含  小括号
  - width
  - min-width
  - max-width
  - 最大值和最小值是包括**等于号**的

实例：

```html
@media screen and (max-width: 800px) {
	<!-- 这句话的意思就是：在屏幕上，并且，最大像素是800px -->	
}
```



**引入资源**

```html
<link rel="stylesheet" media="mediatype and | not| only (media feature)" href="a.css"></link>
```





## less基础

Leaner  Style  Sheets  是  CSS  的扩展语言，也称为  CSS  预处理器

一个  less  文件导入到另一个  less  文件

```less
@import "文件名"
```



### less  使用

大小写是敏感的   不能有特殊符号  不能数字开头

变量引用的时候也需要  `@`   符号

```less
/* 定义变量 */
@变量名：值;
```

### less 编译

vs  code  安装插件  Easy  Less   保存  less  文件后可自动生成  css  文件，引用  css  文件即可

### less  嵌套

子元素的样式直接写到父元素里面

```less
/* 如果有伪类选择器、伪类、交集选择器     记得要和 & 一块使用*/   

.nav {
    a {
        &:hover {
            color: green;
        }
    }
}
```



### less  运算

任何数字、颜色或者变量都可以参与运算，less  提供了`+`、`-`、`*`、`/`运算

- 运算符左右必须有空格
- 对于两个不同单位的值得运算，最终以第一个值得单位为准
- 如果两个值只有一个有单位，则运算结果就使用这个单位

## rem  实际开发适配方案

- 按照设计稿与设备宽度的比例，动态计算并设置  HTML  跟标签的  font-size  的大小；（媒体查询）
- CSS  中，设计稿中元素的宽、高、相对位置等取值，按照同等比例换算成  rem  为单位的值

## rem  适配方案技术使用

### 技术方案一

- less
- 媒体查询
- rem

第一步：根据媒体查询和划分的份数，计算出  HTML  跟标签的字体大小

第二步：`width:44rem / @baseFont`

**页面元素**大小取值

- 页面元素  rem  的值  =    页面元素值（px）/    (屏幕宽度  /  划分的份数)
- 屏幕宽度  /  划分的份数    就是  html  中  font-size  的值的大小     html  中字体大小的值是基准不变



### 技术方案二

- flexible.js
- rem

flexible默认划分10等份





