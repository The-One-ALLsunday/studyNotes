# React Hook学习

## useEffect

- componentDidMount, componentDidUpdate, componentWillUnmount
- 副作用：DOM操作、数据请求、组件更新
- useEffect为什么在组件函数内部执行，可以获取props和state，采用闭包的形式
- 无阻塞更新
- useEffect（回调函数，数组（可以不写））
- 多个useEffect使用

使用：点击按钮使`count`加1

- 第一个参数是回调函数，用于编写业务
- 第二个参数是一个数组
  - 不传数组的情况下，当页面初始挂在后，以及数据更新后都会实时***数据和状态***
  - 传一个数组时，会***同步更新该数组中的状态和数据***
    - 传一个***空数组***，第一次初始挂载时，会执行。之后不管状态和数据怎样变化，都不会执行里面的回调函数 

```jsx
import { useEffect, useState } from 'react'
import { Button } from 'antd'


export default () => {
  const [count, setCount]= useState(0)
  const [num, setNum] = useState(0)
  
  // 第一个useEffect
  useEffect(() => {
    console.log(count)
    
    return () => {
      // 这里return的函数，就是componentWillUnmount生命周期函数,当另外一个组件更换本组件时，本组件就会卸载，才会触发这个生命收期函数。只要一个组件执行了componentWillUnmount函数，就会触发这个return函数
    }
  }, [xxx])
  
  // 第二个useEffect
  useEffect(() => {
    setNum(num + 1)
  }, [num])
  
  const handleChange = () => {
    setCount(count + 1)   // 这个事件里让 count  加1
  } 
  
  return (
  	<>
    	<h1>使用useEffect</h1>
      <h2>{ count }</h2>     // count 在这里显示
      <Button onClick={handleChange}></Button>
    </>
  )
}
```

## useRef

作用：

- 获取DOM元素
- 存取变量，返回一个Ref对象，里面有一个current属性

1、获取DOM元素

```jsx
import { useRef } from 'react'
import { Button, Input } from 'antd'

export default () => {
  const inputRef = useRef(null)
  
  const handleChange = () => {
    console.log(inputRef.current.value)  // inputRef.current 是Input元素本身，后边的.value可以拿到Input中输入的值
  }
  
  return (
  	<>
    	<h1>useRef使用</h1>
    	<Input type="text" inputRef={inputRef} />
    	<Button onClick={handleChange}></Button>
    </>
  )
}
```

2、存取变量

```jsx
import { useRef } from 'react'
import { Button, Input } from 'antd'


export default () => {
  const inputRef = useRef(null)
  const save = useRef({value: '123'})
  
  const handleChange = () => {
    save.current.value = inputRef.current.value   // save中的对象值，等于输入框中的值
    console.log(save.current.value)
  }
  
  return (
  	<>
    	<Input type="text" inputRef={inputRef} />
    	<Button onClick={handleChange}></Button>
    </>
  )
  
}
```

## useContext

1、一个页面上使用了useContext

```jsx
import { useContext, createContext, useEffect, useRef } from 'react'
import { Input, Button } from 'antd'
	
const MyContext = createContext()  // 创建一个容器

// 子组件
const ChildContext = () => {
  let count = useContext(MyContext)  // 使用useEffect接收provider中的value值
  
  return (
  	<h1>我是子组件：{ count }</h1>
  )
}

// 父组件
export default () => {
  const [count, setCount] = useState(0)
  const inputRef = useRef(null)
  
  
  const handleChange = () => {
    setCount(inputRef.current.value)
  }
  return (
  	<>
    	<MyContext.Provider value={count}>  // 把父组件的count传递给子组件
    
    		<ChildContext></ChildContext>
    	</MyContext.Provider>
    
    	<Input type="text" inputRef={inputRef}  />
    	<Button onClick={handleChange}></Button>
    </>
  )
}
```

2、两个页面写useContext

目录：

```jsx
- MyContext.jsx
- ChildContext.jsx
- FatherContext.jsx
```

容器：MyContext文件

```jsx
import { createContext } from 'react'

export let Mycontext = createContext()
```

子组件：ChildrenContext文件

```jsx
import { useContext } from 'react'
import { MyContext } from './MyContext'

export default () => {
  let count = useContext(MyContext)
  
  return (
  	<h1>我是子组件：{count}</h1>
  )
}
```

父组件：FatherContext文件

```jsx
import { useState, useRef } from 'react'
import { Button, Input } from 'antd'
import MyContext from './MyContext'  // 引入容器
import ChildContext from './ChildContext' // 引入子组件

export default () => {
  const [count, setCount] = useState(0)
  const inputRef = useRef(null)
  
  
  const handleChange = () => {
    setCount(inputRef.current.value)
  }
  return (
  	<>
    	<MyContext.Provider value={count}>
    		<ChildContext></ChildContext>
    	</MyContext.Provider>
    
    	<Input type="text" inputRef={inputRef}  />
    	<Button onClick={handleChange}></Button>
    </>
  )
}
```

## useMemo

**把组件更新的权利交给我们自己控制**

- 类似于shouldComponentUpdate，在渲染过程中避免重复渲染
- 当状态或者父组件传来的属性发生变化时，更新组件



- useMemo就是用的memoization来提高性能的
- memorization时JavaScript中的一种***缓存***技术

如果我们有CPU密集型操作，我们可以通过将初始操作的结果存储在缓存中来优化使用。如果某一操作必然会再次执行，我们将不再使用CPU，因为相同结果的结果存储在某个地方，我们只是简单地返回结果

- 记住：这个是以空间换速度，所以最好确定你是否值得这么做，有些场景很有必要使用



- `useMemo()`是一个函数，有两个参数，第一个参数是函数，第二个参数是数组
- useMemo(() => {}, [] )
- useMemo和useEffect执行的时间不同，useEffect是在componentDidMount之后执行的，而useMemo是在***组件渲染过程中执行的***

**useMemo和useEffect的执行时机**：useMemo在useEffect之前执行

**把组件更新的权利由我们控制**

```jsx 
import { useMemo, useState } from 'react'
import { Button } from 'antd'


export default () => {
  const [count, setCount] = useState(0)
  
  const ret = useMemo(() => {
    return count
  }, [])                  // 这里为空数组时，就不会重新渲染回调函中监听的状态，但是状态依旧会改变，只是不渲染
  
  const handleChange = () => {
    setCount(count + 1)
    console.log(count)    // 这里记录的count值是会改变的，但是由于useMemo第二个参数是空数组，所以页面不会重新渲染这个状态值 
  }
  
  return (
  	<>
    	<h1>{ret}</h1>   // 渲染过程，用useMemo控制
    	<Button onClick={handleChange}></Button>
    </>
  )
}
```

使用两个**useMemo**

```jsx
import { useMemo, useState } from 'react'
import { Button } from 'antd'


export default () => {
  const [count, setCount] = useState(0)
  const [num, setNum] = useState(0)
  
  const ret = useMemo(() => {
    return {count, num}
  }, [count])  // 在这里只监听count，页面上count的变化与setCount(count + 1)同步。
               // 点击按钮让num变化时，页面不会同步渲染num，因为没有用useMemo监听num，但实际上，num是变化了。多次点击按钮后，此时，再次点击按钮改变count值，页面刷新改变count值的同时也会把内存中的num值渲染出来。   之所以会是这样的结果，是因为缓存技术          
  
  const handleChange = () => {
    setCount(count + 1)
    console.log(count)    // 每次点击按钮，这里的事件是会调用的，内存中的值是跟随事件同步变化的
  }
  const handleChange2 = () => {
    setNum(num+1)
    console.log(num)      // 每次点击按钮，这里的事件是会调用的，内存中的值是跟随事件同步变化的
  }
  return (
  	<>
    	<h1>{ret.count}-------{ret.num}</h1>  // 渲染过程，用useMemo控制
    	<Button onClick={handleChange}></Button>
    
    	<Button onClick={handleChange2}></Button>
    </>
  )
}
```

## useCallback

作用：避免组件重复渲染，提高性能

可以控制组件什么时候需要更新

- 同样用到缓存技术，和useMemo不同的是：useCallback缓存的是一个函数，这个函数可以执行

- useCallback（）有两个参数，第一个参数是个函数，第二个是个数组
- useCallback(() => {}, [])
- 数组为空时，虽然监听的那个状态在页面不会变化，但是useCallback的第一个函数参数时执行了

```jsx
import { useState, useCallback } from 'react'
import { Button } from 'antd'

export default () => {
  const [count, setCount] = useState(0)
  const [num, setNum] = useState(0)
  
  const ret = useCallBack(() => {
    return count
  }, [num])
  // 这里监听num，页面上的num伴随着点击按钮改变num的变化而变化。当多次点击改变count之后，页面上的count是不会变化的，但是当点击改变num时，引起页面重新渲染后，会把内存中的count值渲染出来。
  
  
  const handleChange = () => {
    setCount(count + 1)
    console.log('count': count)
  }
  const handleChange2 = () => {
    setNum(num + 1)
    console.log('num': num)
  }
  
  return (
  	<>
    	<h1>count:{ret()}--------{num}</h1>
    	<Button onClick={handleChange}></Button>
    	<Button onClick={handleChange2}></Button>
    </>
  )
}
```

## uesImperativeHandle

useImperativeHandle  可以让你使用  ref  时定义暴露给父组件的实例值。

在大多数情况下，应当避免使用  ref  这样的命令式代码。  useImperativeHandle  应当与  forwardRef  一起使用

- useImperativeHandle(ref(传递过来的), () => {}, [])
- 自定义暴露给父组件方法和属性

首先：学习forwardRef使用：获取子组件dom

```jsx
import { forwardRef, useRef } from 'react'
import { Button } from 'antd'


const Forward = (props, ref) => {
  return (
  	<>
    	<h3 ref={ref}>微笑</h3>     // 使用ref把自身暴露出来
    	<h4>可可爱爱</h4>
    </>
  )
}

export default () => {
  const h3El = useRef(null)
  
  const handleChange = () => {
    console.log(h3El.current)        // 获取子组件中的dom
  }
  return (
  	<>
    	<Forward ref={h3El}></Forward>
    	<Button onClick={handleChange}></Button>
    </>
  )
}
```

最后把forwardRef和useImperativeHandle结合使用

```jsx
import { forwardRef, useRef, useImperativeHandle, useState } from 'react'
import { Button, Input } from 'antd'

const Imperative = forwardRef((props, refa) => {
  const inputRef = useRef()
  const [count, setCount] = useState(0)
  const [num, setNum] = useState(0)
  
  useImperativeHandle(refa, () => {   // 调用此组件时，暴露的属性和方法
    name: '可爱',                      // 暴露的属性 
    focus: () => {                    // 暴露的方法
      inputRef.current.focus()
    },
    count
  }, [num]) // 监听num值变化, 多次点击按钮改变count值，页面不会变化，但是因为num值变化引起页面重新渲染后，此时页面上count的值就是内存中的值
  
  const handleChange = () => {
    setCount(count + 1)
  }
  const handleChange2 = () => {
    setNum(num + 1)
  }
  
  return (
  	<>
    	<Input type="text" ref={inputRef}></Input>
    	<h3>count{count}-----num{num}</h3>
    	<Button onClick={handleChange}></Button>
    	<Button onClick={handleChange2}></Button>
    </>
  )
})

export default () => {
  const el = useRef(null)
  
  const handleChange = () => {
    console.log(el.current.name)       // 可以获取到Imperative暴露的name属性值
    
    el.current.focus()                 // 执行Imperative暴露的focus方法
    
    console.log(el.current.count)
  }
  return (
  	<>
    	<Imerative refa={el}></Imerative>
    	<Button onClick={handleChange}></Button>
    </>
  )
}
```



## useLayoutEffect

和useEffect作用一样，在组件生成过程中，可以做一些操作

不同之处：

- 执行的时间不同，useEffect是在componentDidMount以后执行的，useLayoutEffect在浏览器执行绘画之前执行（会阻塞，慎用）

```jsx
import { useLayoutEffect, useEffect, useState } from 'react'
import { Button } from 'antd'


export default () => {
  const [count, setCount] = useState(0)
  
  useEffect(() => {
    console.log('useEffect')
    return () => {
      console.log('useEffect-return')
    }
  })
  
  useLayoutEffect(() => {
    console.log('useLayoutEffect')
    return () => {
      console.log('useLayoutEffect-return')
    }
  })
  
  const handleChange = () => {
    setCount(count + 1)   // 状态更新时，触发useEffect和useLayoutEffect的return
  }
  
  return (
  	<h1>{count}</h1>
    
    <Button onClick={handleChange}></Button>
  )
} 

// 结果依次执行的是： useLayoutEffect-return  useLayoutEffect   useEffect-return  useEffect
```

## useReducer

- useReducer()和redux的reducer是一样的，说白了reducer就是一个函数
- useReducer（）是个函数，有三个参数，第一个参数是reducer，第二个参数是初始值，第三个参数是init函数
- useReducer（）返回值是一个数组，第一个是state，第二个是dispatch
- `const [state, dispatch] = useReducer(reducer, 初始值)`

```jsx
import { useReducer } from 'react'

export default () => {
  const [state, dispatch] = useReducer((state, action) => {
    switch(action.type) {
        case: 'setName':
        	return {
            ...state,
            name: action.name
          }
        case: 'setAge':
        	return {
            ...state,
            age: action.age
          }
      default:
        return state
    }
  }, {name: '微笑', age: 18})
  
  const handleChange = () => {
    dispatch({
      type: 'setName',
      name: '可爱'
    })
  }
  
  const handleChange = () => {
    dispatch({
      type: 'setAge',
      name: '20'
    })
  }
  
  return (
  	<>
    	<h1>姓名是：{state.name}---------年龄是：{state.age}</h1>
    	<Button onClick={handleChange}></Button>
    	<Button onClick={handleChange2}></Button>
    </>
  )
}
```

### 使用useReducer useContext createContext实现redux

目录：

```jsx
- Text1.jsx
- Text2.jsx
- Reducer.jsx
- index.jss
```

Reducer文件

```jsx
import { createContext, useReducer } from 'react'

export const MyContext = createContext()
const reducer = (state, action) => {
  switch (action.type) {
      case 'setName': 
      	return {
          ...state,
          name: action.name
        }
    case 'setAge': 
      return {
        ...state,
        age: action.age
      }
    default:
      return state 
  }
}

const data = { name: '微笑', age: 18 }

export default (props) => {
  const [state, dispatch] = useReducer(reducer, data)
  
  return (
  	<MyContext.Provider value={state, dispatch}>
    	{props.children}
    </MyContext.Provider>
  )
}
```

Text1文件

```jsx
import { useContext } from 'react'
import { MyContext } from './Reducer'

export default () => {
  let {state, dispatch } = useContext(MyContext)
  const handleChange = () => {
    dispatch({
      type: 'setName',
      name: '可爱'
    })
  }
  const handleChange = () => {
    dispatch({
      type: 'setAge',
      name: 20
    })
  }
  
  return (
  	<h1>Text1---name: {state.name}------age: {state.age}</h1>
    <Button onClick={handleChange}></Button>
    <Button onClick={handleChange2}></Button>
  )
}
```

Text2文件

```jsx
import { useContext } from 'react'
import { MyContext } from './Reducer'

export default () => {
  let {state, dispatch } = useContext(MyContext)
  const handleChange = () => {
    dispatch({
      type: 'setName',
      name: '可爱加一'
    })
  }
  const handleChange = () => {
     dispatch({
      type: 'setAge',
      name: 24
    })
  }
  
  return (
  	<h1>Text2---name: {state.name}------age: {state.age}</h1>
    <Button onClick={handleChange}></Button>
    <Button onClick={handleChange2}></Button>
  )
}
```

Index文件

```jsx
import Reducer from './Reducer'
import { Text1 } from './Text1'
import { Text2 } from './Text2'


export default () => {
  
  
  return (
		<>
    	<Reducer>
    		<Text1></Text1>
      	<Text2></Text2>
    	</Reducer>
    </>
  )
}
```







## 自定义hook

自定义hook，和普通的函数没有本质上的区别，都是做一些函数封装，方便使用

注意：

- 自定义hook必须以use开头
- 自定义hook，可以使用我们这些hook（useState，useEffect。。。）来封装

```jsx
import { useState } from 'react'

const useCus = (val, num) => {
  let [count, setCount] = useState(val)
  const add = () => {
    setCount(count + num)
  }
  return { count, add }
}

export default () => {
  let { count, add } = useCus(10, 2)
  const handleChange = () => {
    add()
  }
  return (
  	<>
    	<h1>{count}</h1>
    	<Button onClick={handleChange}></Button>
    </>
  )
}
```

























