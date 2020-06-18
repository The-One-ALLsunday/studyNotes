# React学习

## 在react中使用react

1.运行`cnpm i react react-dom -S`安装包

- react：专门用于创建组件和虚拟DOM的，同时组件的生命周期都在这个包中
- react-dom：专门进行DOM操作，最主要的应用场景，就是`ReactDOM.render()`

2.在`index.html`页面上创建容器:

```html
<!-- 容器，将来使用react创建的虚拟dom元素，都会被渲染到指定的容器中-->
<div id="app">
    
</div>
```

3.导入包

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
```

4.创建虚拟DOM元素

```javascript
const myH1 = React.createElement('h1'， null, '这是一个h1')
/**
	参数1：元素标签名；
	参数2：元素属性；
	参数3：元素子节点
	参数n：其他子节点
*/
```

5.把虚拟DOM渲染到页面上

```javascript
ReactDOM.render(myH1, document.getElementById('app'))
/* 第二个参数是一个容器元素 */
```

思考：再创建一个div元素，用于包裹myH1元素

```javascript
/* 创建myH1的同时，也创建一个div,把myH1作为myDiv的第四个参数  */
const myDiv = React.createElement('div', null, '我是div', myH1)

/* 渲染myDiv */
React.render(myDiv, document.getElementById('app'))
```

## 使用babel启用JSX语法

1.安装插件

`cnpm i babel-core babel-loader babel-plugin-transform-runtime -D`

`cnpm i  babel-preset-env babel-preset-stage-0 -D`

2.安装能够识别转换jsx语法的包

`cnpm i babel-preset-react -D`

3.添加配置文件

```json
{
    "presets":["env", "stage-0", "react"],
    "plugin":["transform-runtime"]
}
```

4.在webpack中配置第三方loader

## jsx中混合写入js表达式，要把js写进{ }中

- 渲染数字、字符串、布尔值

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

let a = 10
let str = 'dengbo'
let boo = true

ReactDOM.render(<div>
        {a + 2}  结果为  12  可以计算
        {str}    结果为  dengbo
        {boo ? '条件为真' ：'条件为假'}  结果为  条件为真   可以使用布尔值进行判断或计算
    </div>, document.getElementById('app'))
```

- 渲染属性绑定

```jsx
let title = '我是title'

ReactDOM.render(<div title="{title}"></div>, document.getElementById('app'))
```

- 渲染元素

```jsx
let h1 = <h1>我是h1</h1>

ReactDOM.render(<div>
    {h1}
    </div>, document.getElementById('app'))
```

- 渲染jsx数组元素对象

```jsx
const arr = [
    <h1>我是h1</h1>,
    <h2>我是h2</h2>
]

ReactDOM.render(<div>
    {arr}
    </div>, document.getElementById('app'))

结果为：直接把数组中的元素渲染到界面上，虽然能正常显示，但是会出现问题，没有设置key
```

- 渲染普通数组

```jsx
方法一：外部for循环

const arrStr = ['路飞', '索隆', '娜美', '罗宾']

/* 先声明一个空数组，用forEach遍历旧数组，把每一项都用标签包裹，依次push到新数组中*/
const newArr = []
arrStr.forEach(item => {
    let tmp = <h2 key={item}>{item}</h2>
    newArr.push(tmp)
})

ReactDOM.render(<div>
    {newArr}
    </div>, document.getElementById('app'))
```

```jsx
方法二：内部for循环
数组的map方法：把数组中的每一项经过处理后，必须使用return对操作后的数组进行返回
const arrStr = ['路飞', '索隆', '娜美', '罗宾']
ReactDOM.render(<div>
    arrStr.map(item => <h3 key={item}>{item}</h3>)
    </div>, documentElementById('app'))
```

**数组中直接被map或者forEach控制的元素需要加key属性**

## 在jsx中添加类和label标签的for属性

- 添加类名用  className  代替  class
- label中用  htmlFor  代替  for  

## React中创建组件的方式

### 单独封装组件时如何省略后缀名

在Webpack中，配置resolve节点

```javascript
{
    resolve: {
        extensions:['.js', '.jsx', '.json']
    }
}
```

### 组件封装用@符号表示绝对路径

在webpack中，配置resolve节点

```javascript
{
    resolve: {
        alias: {
            '@': path.join(__dirname, './src ')
        }
    }
}
```

### 构造函数创建的无状态组件

- 如果在一个组件中 return 一个  null  则表示此组件时空的，什么都不会渲染
- 在组件中，**必须**返回一个合法的的jsx虚拟DOM元素

创建组件并为组件传递数据

```jsx
function Hello(props) {
    return <div>我是合法的div---{props.name}</div>
}

const dog = {
    name: '大黄',
    age: 3,
    gender: '雄'
}

ReactDOM.render(<div>
    <Hello {...dog}></Hello>
    </div>, document.getElementById('app'))
```

### 类继承创建的有状态组件

在类中，只能写静态属性和实例属性以及静态方法和实例方法

```jsx
/* 在组件内部必须有render函数 */
class Hello extends React.Component {
    /* render函数中，必须返回合法的jsx虚拟DOM结构 */
	render() {
		return <div>这是通过class关键字创建的组件</div>
	}
}
```

传参

```jsx
class Movie extends React.Component {
    render() {
        return <div>{this.props.name}</div>
    }
}

const user = {
    name: 'zs',
    age: 18,
    gender: '男'
}
ReactDOM.render(<div>
    	<Movie {...user}></Movie>
    </div>, document.getElementById('app'))
```



- class中创建的组件，通过props传递的参数，不需要接收，直接通过`this.props.xxx`即可访问

## CSS启用模块化

当我们把样式独立到一个css文件中，对其引用需要`import cssobj from './index.css'`，但这里的cssobj是一个空对象，需要在webpack中启用css模块化。这样，cssobj这个对象的属性是css文件中的类名，但这个属性不是引用时的类名，属性值是类名。

- css模块化，只针对类选择器和id选择器生效
- css模块化，不会将标签选择器模块化

**注意：**以下第二项基本不用，不如在webpack中开启模块化

通过`:global()`对某一项样式取消模块化

通过`:local()`对某一项样式开启模块化

## 在项目中启用模块化并同时使用bootstrap

为css启用模块化的同时使用第三方以.css结尾的文件样式库，会发生自己跟自己冲突的情况。

这个冲突点在于：我们开启css模块化的同时要排除node_modules中的css文件，这样第三方的样式文件就不能再使用了。

解决方法：我们自定义的样式文件用sass的格式书写，只为sass文件开启模块化



## 在React中绑定事件

在react中有一套自己的事件绑定机制，事件名，采用驼峰命名法

`onClink = { function }`

**方法一：**行内写匿名函数`onClick={function () { console.log('ok') }}`

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

class MyEvent extends React.Component {
    constructor() {
        super()
        this.state = {}
    }
    render() {
        return <div>
        	<button onClick={function () { console.log('ok') }}></button>
        </div>
    }
}

ReactDOM.render(<div>
    	<MyEvent></MyEvent>
    </div>，document.getElementById('app'))
```

**方法二：**调用实例函数

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

class MyEvent extends React.Component {
    constructor() {
        super()
        this.state = {}
    }
    render() {
        return <div>
        	<button onClick={ this.myClickHandLer }></button>
        </div>
    }
    myClickHandler() {
        console.log('2222')
    }
}

ReactDOM.render(<div>
    	<MyEvent></MyEvent>
    </div>，document.getElementById('app'))
```

方法三：标准用法，箭头函数剧名函数

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

class MyEvent extends React.Component {
    constructor() {
        super()
        this.state = {}
    }
    render() {
        return <div>
        	<button onClick={ () => { this.myClickHandler('arg1') } }></button>
        </div>
    }
    myClickHandler = (arg1) => {
        console.log('2222')
    }
}

ReactDOM.render(<div>
    	<MyEvent></MyEvent>
    </div>，document.getElementById('app'))
```



## setState

如果想要修改state中的数据，推荐使用`this.setState({  })`

```jsx
export default class BindEvent extends React.Component {
    constructor () {
        super()
        this.state = {
            msg: '哈哈'
        }
    }
    render() {
        return <div>
        	<button onClick={() => this.show }></button>
        </div>
    }
    show = () => {
        this.setState({
            msg: 123
        })
    }
}
```

### 注意点

- 在  setState  中，只会把对应的 state  状态更新，不会覆盖其它的  state  状态
- `this.setState({  })`  方法是异步的，因此，该方法可能还没执行结束，后续的代码就可能会执行。另外，该方法有第二个参数，是一个回调函数，这个回调函数帮助我们，既可以拿到页面上最新的数据，也可以使用  `this.setState({})`  方法。

```jsx
this.setState({
    msg: '最新数据'
}, function () {
    console.log('ok')
})
```



## 新注释方法

```jsx
//#region 名字（介绍React中绑定事件的标准格式）
//#endregions
```

















