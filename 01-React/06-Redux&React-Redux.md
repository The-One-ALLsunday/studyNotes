# Redux & react-redux

使用redux和react-redux初始化项目

项目src目录

```markdown
src
  |--actions
  |  |--register.js
	|--reducers
	|  |--auth.js
	|  |--index.js
	|--App.js
	|--index.js
	|--register.jsx
```

- actions目录

```javascript
import axios from 'axios'

export const registerRequestAction = (data) => {
  
  return dispatch => {
    return axios.post('/api/users', data)
  }
}
```

- reducers目录

```javascript
// auth.js


export function auth(state = {}, action) {
  switch(action.type) {
      
    default: return state;
  }
}


// index.js
import { combineReducers } from 'redux'
import auth from './auth'


const rootReducer = combineReducers({
  auth,
})

export default rootReducer
```

- App.js文件

```jsx
import React, { Fragment } from 'react'


const App = () => {
  
  
  return (
  	<Fragment>
    	Hello
    </Fragment>
  )
}
```

- index.js文件

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'

import logger from 'redux-logger'
import thunk from 'redux-thunk'
import { composeWithDevTools } from 'redux-devtools-extension'

import { createStore, applyMiddleware } from 'redux'
import { Provider } from 'react-redux'
import rootReducer from './reducer'

const store = createStore(rootReducer, composeWithDevTools(applyMiddleware(logger, thunk)))

ReactDOM.render(
	<Provider store={store}>
  	<App />
  </Provider>
  ,document.getElementById('root'));
```

- register.jsx

```jsx
import React, { Fragment } from 'react'
import { connect } from 'react-redux'
import { bindActionCreators } from 'redux'
import { registerRequestAction } from './actions/register'

class Register extends React.Component {
  
  this.state = {
    data: {
      name: 'zs',
      age: 'ls'
    }
  }
  
  componentDidMount() {
    this.props.registerRequestAction(this.state.data)
  }
  
  render() {
    return (
    	<Fragment>
      	
      </Fragment>
    )
  }
}

const mapDispatchToProps = dispatch => {
  registerRequestAction: bindActionCreators(registerRequestAction, dispatch)
}

export default connect(null, mapDispatchToProps)(Register)
```

