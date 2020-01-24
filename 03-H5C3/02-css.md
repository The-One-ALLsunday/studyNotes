# CSS学习

Cascading  Style  Sheet（层叠样式表）

## 行间样式



## 内联样式



## 外联样式



## css语法

- 选择器   和   声明块组成

## 选择器

- 通配选择器

- 元素选择器

- 属性选择器

- 类选择器

- id  选择器

- 并集选择器

- 交集选择器

  - span.p3

- 子代选择器

  - div > span

- 后代选择器

- 兄弟选择器

  - div + span    是紧挨着  div  后边的  span
  - div  ~   span   是紧挨着  div  后边的所有  span

- 结构伪类选择器

  - a  元素   LVHA

  - :hover

  - ::selection     p  标签使用，文字选中时的样式

    

- 伪元素选择器
  - 首字母
    - :first-letter
  - 首行
    - :first-line
  - ::before  和   ::after
    - 通常结合 content  使用
- 子元素选择器
  - 最前边的是p的话，就意味着  必须是  p  元素，同时也是第一个元素
  - :first-child
  - :last-child
  - :nth-child                even  偶数     odd   奇数
  - :first-of-type
  - :last-of-type
  - :nth-of-type
- 否定伪类选择器
  
  - p:not(.dag)   所有  p  标签，除了类为  dag  的
- 选择器优先级规则
  - 内联样式    1000
  - id  选择器   100
  - 类和伪类     10
  - 元素             1
  - 通配             0
  - 继承             无

## 继承

不可以继承

- 背景相关的样式
- 边框相关的样式
- 定位相关的样式

可以继承的

- font-size
- color

## 字体

- 衬线字体                      serif
- 非衬线字体                  sans-serif
- 等宽字体                      monospace
- 草书字体                      cursive
- 虚幻字体                      fantasy