# React学习

Facebook  出版，在2013年5月开源

## React 和 Vue之间的对比

### 组件方面

- 什么是模块化：从  代码（js）角度去分析问题，把我们编程时的业务逻辑分割到不同的模块中去，这样方便代码的重用；
- 什么是组件化：从  UI  的角度分析问题，把一个页面拆分为互不相干的组件。完成一个项目的开发，会用到大量的组件，如果想实现一个相似的界面，直接把现有的组件拿过来用即可，这样方便了  UI  组件的重用；
- 组件化的好处：方便  UI  组件的重用，组件就是一系列元素的集合；
- Vue如何实现组件化：通过  .vue  文件，浏览器本身不识别  .vue  模板文件，在运行前都会编译成真正的元素组件
  - template:  UI  结构
  - Script：业物逻辑和数据
  - Style：UI  的样式
- React如何实现组件化：在  React  中实现组件化的时候，根本没有  .vue  这样的模板文件，而是使用  JS  代码的形式，去创建任何想要的组件；
  - React  中的组件都是在  JS  文件中直接定义的
  - React  组件，并没有把一个组件拆分为三部分，而是全部使用  JS  来实现一个组件，（结构、样式、行为、业务逻辑都混在  JS  中一起编写出来的）

### 开发团队

- Vue：第一版，主要是有作者  尤雨溪  专门维护的，当  Vue  升级到  2.x  的时候，也有了自己的团队在进行维护和更新
- React：React  是由  Facebook  前端官方团队进行维护和更新；因此，React 的维护团队，技术更为雄厚

### 社区方面

- Vue：Vue  相对于  React，诞生较晚，有些坑并没有人踩过，可能会造成自己造轮子
- React：由于  React  诞生的比较早，所以社区资源更为强大。一些常见的问题、坑、以及最优解决方案，在社区、博客等平台就能找到

### 移动App开发体验方面

- Vue：通过  Weex  这门技术迁移到移动  App  上
- React：通过  ReactNative  这门技术迁移到移动  App  上

### 为什么学习React

- 设计很优秀，是基于组件化的，方便我们  UI  代码重用
- 开发团队实力强悍，不容易断更
- 社区强大，很对问题都能找到解决方案
- 通过  ReactNative  无缝衔接到移动  App  的开发

## React中的几个核心概念

### 虚拟DOM

- DOM  和  虚拟DOM的区别
  - DOM是浏览器中  JS  提供的功能，我们只能通过浏览器提供的  API  来操作  DOM  对象
  - 虚拟DOM是程序员手动模拟实现的，类似于浏览器中的  DOM，本质的区别就是虚拟  DOM  是由程序员实现的

- 为什么要实现虚拟  DOM
  - DOM的本质：就是用  JS  表示的  UI  元素，因为  JavaScript  是由  js语法 、DOM 、BOM  组成的
- 什么是虚拟DOM
  - 本质：使用  JS  模拟  DOM  树
  - 目的：实现  DOM  节点的高效更新

### Diff算法

- tree  diff：新旧  DOM  树，逐层对比，对比整个  DOM  树，把所有层、所有节点全部对完成必然能找到需要更新的节点
- component  diff：在对比每一层的时候，组件之间的对比，如果两个组件类型相同，则暂时认为这个组件不需要被更新，如果组件类型不同，则立即将就组建移除，新建一个组件，替换被移除的组价
- element  diff：在组件中，每个元素也需要对比，那么元素级别的对比，就叫做  element  diff
- key：这个属性，可以把页面上的  DOM  和  虚拟DOM中的对象，做一层关联关系

### jsx语法

React  官方，提出了一套  JSX  语法规范，能够让我们在  JS  文件中，书写类似于  HTML  那样的代码，快速定义虚拟  DOM  结构

- jsx：符合  xml  规范的  JS  语法

- jsx原理：jsx在内部运行的时候，也是先把类似于  HTML  这样的标签转化为`React.createElement()`的形式。不会把  HTML  标签直接渲染到页面上，通过`React.createElement()`渲染到页面上
- jsx是对程序员友好的语法糖
- js文件中，不识别标签外的尖括号，需要安装相关的语法转换工具`cnpm i babel-preset-react -D`

**使用**

- 如果想要使用  jsx  语法，需要先安装语法转换工具`cnpm i babel-preset-react -D	`，然后在`.babelrc`中添加语法配置
- jsx语法本质：还是使用  React.createElement()  的形式实现的，并没有把用户写的  HTML  直接渲染到页面上
- 如果要在  jsx  语法内部，书写  JS  代码，那么所有的  JS  代码都必须写到`{  }` 中
- 当编译引擎，在编译  jsx  代码时，如果遇到了`<  >`就当成  HTML  代码去编译，如果遇到了`{  }`就当成  JS  代码去编译
- 在`{  }`内部可以书写任何符合  JS  代码规范的代码
- 在  jsx  中，如果想要为元素添加`class`属性，那么必须写成`className`，因为`class`在  ES6  中是一个关键字；和`class`类似，label  标签的  `for`  属性需要替换为`htmlFor`
- 在  jsx  语法创建  DOM  的时候，所有的节点必须有唯一的根元素进行包裹
- 如果要写注释了，也必须写到`{  }`中，且至少占三行，看着像对象的形式，注释单独在第二行



## React中的组件

在  React  中，构造函数就是一个最基本的组件

如果想要把组件放到页面中，可以把构造函数的名字，当做组件的名称，以  HTML  标签引入即可

注意：React  在解析所有的标签的时候，是以首字母来区分的，如果标签的首字母是小写，那么就按照普通的  HTML  标签来解析，如果标签的首字母是大写，就按照组件的方式去解析渲染

结论：组件的首字母，必须大写

### 函数组件

```jsx
以扩展运算符，通过属性传参
组件需要用 props 进行接收  props只读，不可修改

function Hello(props) {
    return <div>
    	<h1>通过props进行组件间的传参{ props.name }</h1>
    </div>
}

var person = {
    name: '邓波',
    age: 18,
    gender: '男',
    address: '河南'
}

ReactDOM.render(<div>
    	<Hello {...person}></Hello>
    </div>, document.getElementById('app'))
```

### 类组件

```jsx
class Hello extends React.Component {
    constructor(props) {
        super(props)
    }
	render() {
		return <div>
        	<h1>通过类创建的组件--{ this.props.address }</h1>
        </div>
	}
}

ReactDOM.render(<div>
    	<Hello address="河南"></Hello>
    </div>, document.getElementById('app'))
```

### 有状态组件和无状态组件

- 通过  function  关键字创建出来的组件没有状态，没有生命周期函数
- 通过  class  关键字创建出来的组件有状态，有生命周期函数
- 两者最本质的区别就是：是否有  state  属性
- 有私有数据就用有状态组件，没有私有数据推荐使用无状态组件

## React中组件的生命周期

- 概念：在创建组件，到加载，到页面运行，以及组件被销毁的过程中，总是伴随着各种各样的事件，这些组件在特定的时期，触发事件，统称为组件的生命周期

- 组件的生命周期分为三个部分

  - 组件创建阶段：这个阶段有一个显著的特征，只执行一次

    > componentWillMount函数：组件将要被挂载，此时还没有开始渲染虚拟  DOM
    >
    > render函数：第一次开始渲染真正的虚拟  DOM，当  render  函数执行完，内存中就有了完整的虚拟DOM
    >
    > componentDIdMount函数：组件完成了挂载，此时组件已经显示在了页面上，当这个函数执行完，组件就进入了运行阶段

  - 组件运行阶段：这个阶段有一个显著的特征，根据组件  state  和  props  的改变，有选择性的触发0次或者多次

    > componentWillReceiveProps函数：组件将要接收新属性，此时，只要这个方法被触发，就证明父组件为子组件传递了新的属性值
    >
    > shouldComponentUpdate函数：组件是否需要被更新，此时组件尚未被更新，但是  state  和  props  已经是最新的了
    >
    > componentWillUpdate函数：组件将要被更新，此时，尚未开始更新，内存中的  DOM  树还是旧的
    >
    > render函数：此时，又要重新根据最新的  state  和  props  重新渲染一颗内存中的虚拟  DOM  树，当  render  函数调用完毕，内存中的旧  DOM  树，已经被新的  DOM  树替换了，此时，页面还是旧的
    >
    > componentDidUpdate函数：此时，页面又被重新渲染了，state  和虚拟  DOM  树和页面已经完全保持同步

  - 组件销毁阶段：这个阶段有一个显著的特征，只执行一次

    > componentWillUnmount函数：组件将要被卸载，此时组件还可以正常使用

![](../00-images/React-lifecircle.png)

组件生命周期表格

![](../00-images/React-Lifecircle-table.png)

### 组件生命周期执行顺序

- Mounting
  - constructor()
  - componentWillMount()
  - render()
  - componentDidMount()
- Updating
  - componentWillReceiveProps(nextProps)
  - shouldComponentUpdate(nextProps, nextState)
  - componentWillUpdate(nextProps, nextState)
  - render()
  - componentDidUpdate(prevProps, prevState)
- Unmounting
  - componentWillUnmount()



## React中绑定this并传参的几种形式

### 通过绑定事件.bind(this)传参

```jsx
点击按钮 把msg修改为参数a中的值

class Args extends React.Component{
    constructor(props) {
        super(props)
        
        this.state = {
            msg: '修改这里'
        }
    }
    
    render() {
        return <div>
          <h1>通过事件绑定和bind()函数传参</h1>
          <input type="button" value="按钮" onClick={this.changeMsg.bind(this,a)}></input>
        </div>
    }
	changeMsg(a) {
        this.setState({
            msg: a
        })
    }
}


ReactDOM.render(<div>
    	<Args></Args>
    </div>, document.getElementById('app'))
```

### 在构造函数constructor中绑定并传参

- 相对于第一种：这个函数可以多次复用，而不是只在  input  中用一次，每次都得用  bind(this)  做后缀

```jsx
点击按钮  修改msg为 arg1 + arg2

class Args extends React.Component{
    constructor(props) {
        super(props)
        
        this.state = {
            msg: '修改这里'
        }
        this.changeMsg = this.changeMsg.bind(this, arg1, arg2)  重点句子
    }
    
    render() {
        return <div>
          <input type="button" value="按钮" onClick={this.changeMsg}></input>
        </div>
    }
    
    changeMsg(arg1, arg2) {
        this.setState({
            msg: arg1 + arg2
        })
    }
}


ReactDOM.render(<div>
    	<Args></Args>
    </div>, document.querySelector('#app'))
```



### 通过箭头函数

```jsx
点击按钮， 修改msg值为  a + b

class Args extends React.Component{
    constructor(props) {
        super(props)
        
        this.state = {
            msg: '修改这里'
        }
    }
    render() {
        return <div>
       	  <input type="button" value="按钮" onClick={() => {this.changeMsg(a,b)}}></input>
        </div>
    }
    changeMsg(a, b) {
        this.setState({
            msg: a + b
        })
    }
}
                      
ReactDOM.render(<div>
            <Args></Args>          
     </div>, document.querySelector('#app'))
```



## React中的双向数据绑定

React中只支持，把数据从  state  传输到页面上，不支持自动实现页面上的数据保存到  state  上。只是实现了数据的单项绑定

**注意**：如果为表单，提供  value  属性绑定，那么，必须同时为表单元素绑定  readOnly  或者  onChange  事件

- 如果提供了  readOnly  属性，那么这个表单元素只读，不能修改
- 如果提供了  onChange  事件，那么这个表单的元素值可以修改，但是要自己定义修改逻辑



```jsx
class Compo extends React.Component{
    constructor(props) {
        super(props)
        
        this.state = {
            msg: '实现双向数据绑定'
        }
    }
    render() {
        return <div>
         <input type="button" value={this.state.msg} onChange={this.txtChange}></input>
        </div>
    }
    txtChange = (e) => {
        为了实现页面到state数据传递  这里需要对msg重新赋值，那么就需要拿到页面上文本框上的值
        this.setState({
            msg: e.target.value
        })
    }
}


ReactDOM.render(<div>
    	<Compo></Compo>
    </div>, document.getElementByID('app'))
```

### 获取文本框中最新文本的三种方式

- 使用  `document.getElementById()`
- 使用  `ref`
- 使用事件对象参数  e  来拿，得到的是原生的  JS  DOM  对象



## React中共享数据context特性

兄弟传值，共享数据  相当于  Vue  中的  Vuex

**使用步骤**：-----前三个后三个后两个

- 在父组件中，定义一个  function，这个函数有一个固定的名称，叫做  getChildContext，内部，必须返回一个对象，这个对象就是所有组件的  共享数据库
- 使用属性校验，规定一下传递给子组件的数据类型。需要定义一个静态的（static）childContextTypes（固定名称，不要随便改）
  - 安装`cnpm i prop-types -S`
- 组件接收共享数据时，需要先进行属性校验。定义一个静态的（static）contextTypes  对象



## React中的路由

**装包**

- `cnpm i react-router-dom -S`

**按需导入**

- `import { HashRouter, Route, Link } from 'react-router-dom'`
  - HashRouter  表示一个路由的根容器，将来所有跟路由有关的东西，都要包裹在  HashRouter  里面，而且一个网站中，只需要用一次  HashRouter  即可
    - HashRouter  内部，只能有一个根元素
  - Route  表示路由规则，在  Route  有两个重要的属性，path  component
  - Link  表示一个路由链接，就好比  Vue  中的  `<router-link></router-link>`

**演示**

在  react-router  中，没有类似于  view-router  这样的标签，Route  本身就是一个占位坑

```jsx
1.引入的组件
import Home from './Home.jsx'
import Movie from './Movie.jsx'
import About from './About'

class Rot extends React.Component{
    constructor(props) {
        super(props)
        
        this.state = {}
    }
    render() {
        return <HashRouter>    2.开启路由模式
        	<div>
            	连接到组件
                <Link to="/home">首页</Link>   3.链接到相关组件
                <Link to="/movie">电影</Link>
                <Link to="/about">关于</Link>
                
                路由匹配
                <Route path="/home" component={Home}></Route>   4.路由与组件的匹配
                <Route path="/movie" component={Movie}></Route>
                <Route path="/about" component={About}></Route>
            </div>
        </HashRouter>
    }
}

```

### 路由传参

默认情况下，路由中的规则是**模糊匹配**的，如果路由可以部分匹配成功，就会展示这个路由所对应的组件

- 精确匹配：加上第三个属性  `exact`

  ```jsx
  <Link to="/movie"></Link>
  
  <Route path="/movie" component={Movie} exact></Route>
  ```

- 精确匹配并传参并拿到路由中的参数

  ```jsx
  <Link to="moive/top10/10"></Link>
  
  <Route path="/movie/:type/:id" component={Movie} exact></Route>
  
  拿到路由中的参数
  this.props.match.params.type
  this.props.match.params.id
  ```

  ## 错误边界

```jsx
import React from 'react'


export default class ErrorBoundary extends React.Component {
  state = {
    hasError: false,
    error: null,
    errorInfo: null,
  }
	
	/**
	* 子元素发生错误时加载的生命周期函数
	*/ 
	componentDidCatch(error, errorInfo) {
    this.setState({
      hasError: true,
      error,
      errorInfo,
    })
  }

	render() {
    const { error, errorInfo } = this.props;
    if (this.state.hasError) {
      return <div>{ this.props.render(error, errorInfo) }</div>
    } else {
      return this.props.children;
    };
  }
}

import React, { Fragment } from 'react'
import ErrorCom from './ErrorCom' // 可能出错的组件
import ErrorBoundary from './ErrorBoundary'

const Deom = () => {
  
  
  return (
  	<Fragment>
    	<ErrorBoundary render={(err, info) => {info}}>
      	<ErrorCom />
      </ErrorBoundary>
    </Fragment>
  )
}
```





























