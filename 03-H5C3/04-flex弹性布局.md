# flex布局

flexible box  译为  弹性布局，任何容器都可以指定为flex布局

- 当我们为父盒子设为  flex  布局以后，子元素的  float、clear、vertical-align属性将失效
- 父盒子叫  容器，子元素叫  项目

布局原理：

- 就是通过给父盒子添加  flex  属性，来控制子盒子的位置和排列方式

## 给容器添加常见属性

- flex-direction：设置主轴方向
  - 默认主轴方向就是  x  轴方向，水平向右   row、row-reverse
  - 默认侧轴方向就是  y  轴方向，垂直向下   column、column-reverse
- justify-content：设置**主轴**上的子元素排列方式
  - center
  - space-around   平均分配剩余空间
  - space-between  先两边贴边，然后分配剩余空间      **重点**
- flex-wrap：设置子元素是否换行
  - 默认的子元素是不换行的，如果子元素装不开，就会缩小子元素的宽度，放在一行上
  - nowrap  不换行
  - wrap  换行
- align-items：设置侧轴上的子元素的排列方式（单行）
  - center  侧轴居中             **重点**
  - stretch  拉伸
    - 子盒子不要给高度
- align-content：设置侧轴上子元素的排列方式（多行）
  - 适用于子元素**换行**的情况下
  - center
  - space-between
  - space-around
- flex-flow：符合属性，相当于同时设置了  flex-direction  和  flex-wrap
  - flex-flow：row  wrap

## flex布局子项常见属性

- flex：子项目所占份数
  - 默认是  0
  - 从剩余空间分配
- align-self：控制自己在侧轴的排列方式
- order：子项的排列顺序（前后顺序）
  - 数值越小，排列越靠前，左右移动
  - 默认为  0
  - 和  z-index  不一样



## flex: 0 1 auto表示什么意思

三个参数分别对应的是 `flex-grow`, `flex-shrink` 和 `flex-basis`，默认值为 0 1 auto

- `flex-grow` 属性定义项目的放大比例，默认为 0，即如果存在剩余空间，也不放大。
- `flex-shrink` 属性定义了项目的缩小比例，默认为 1，即如果空间不足，该项目将缩小。
- `flex-basis` 属性定义了在分配多余空间之前，项目占据的主轴空间（main size）

### 求最终left、right的宽度

样式说明

- 父元素 container 的 width 为 600px
- left 元素 `flex-grow` 为 1，`flex-shrink` 为 2，`flex-basis` 为 500px
- right 元素 `flex-grow` 为 2，`flex-shrink` 为 1，`flex-basis` 为 400px

结题

left 和 right 的主轴空间和大于父元素的宽度 超了 300px

> 500 + 400 = 900 - 600 = 300

总权重为

> 2 * 500 + 1 * 400 = 1400

超出了 所以是收缩 则分别的收缩长度

> left：300 * 2 * 500 / 1400 = 214.28
> right: 300 * 1 * 400 / 1400 = 85.72

最终宽度

> leftWidth：500 - 214.28 = 285.72
> rightWidth：400 - 85.72 = 314.28







