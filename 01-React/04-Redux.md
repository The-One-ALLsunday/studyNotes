# Redux学习

## 工作流程







## react-redux

### 安装相关依赖

- `yarn add redux`
- `yarn add react-redux`

### 构建 store 和  reducer

- 创建reducer/index.js文件，构建reducer来响应  actions
- 创建store/index.js文件，通过createStore方法，把我们的reducer传入进来
- 在app.js中引入store

### 搭建页面结构

- 创建一个组件，名字叫ComA，里面放一个button按钮
- 创建另一个组件，名字叫ComB，里面放一个div，用来显示数字
- 在app.js中引入两个组件

**文件**

reducer/index.js

```jsx
// 接收两个参数，第一个参数是：state，第二个参数是：action
const initState = 10
export.reducer = (state=initState, action) => {
    return state
}
```

store/index.js

``` jsx
//
import {createStore} from 'redux'
import {reducer} from '../reducer'

export default createStore(reducer)
```

app.js

```jsx
import React from 'react'
import './App.css'
import store from './store'
// 引入A和B组件
import ComA from './page/ComA'
import ComB from './page/ComB'

function App() {
    return <div className="app">
    	<!-- 注册组件 -->
        <ComA />
        <ComB />
    </div>
}

export default App
```

ComA/index.js

```jsx
import React from 'react'


export default class ComA extends React.Component{
    render() {
        return (
        	<button>+</button>
        )
    }
}
```

ComB/index.js

```jsx
import React from 'react'


export default class ComB extends React.Component{
    render() {
        return (
        	<div>1</div>
        )
    }
}
```

创建好组件A和B，把这两个组件引入到app.js中











