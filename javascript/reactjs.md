### 1、`useState` 的实现原理

```javascript 
let state = []
let setters = []
let stateIndex = 0

function createSetter (index) {
  return function (newState) {
    if (state[index] !== newState) {
      state[index] = newState
      render()
    }
  }
}

function useState (initialState) {
  state[stateIndex] = state[stateIndex] ? state[stateIndex] : initialState
  setters.push(createSetter(stateIndex))
  let value = state[stateIndex]
  let setter = setters[stateIndex]
  stateIndex++
  return [value, setter]
}

function render () {
  stateIndex = 0
  setters = []
  ReactDOM.render(<App />, document.getElementById('root'))
}
```



### 2、 `useEffect` 的实现原理

```javascript
function render () {
  stateIndex = 0
  setters = []
  effectIndex = 0
  ReactDOM.render(<App />, document.getElementById('root'))
}

let prevDepsAry = []
let effectIndex = 0

function useEffect (callback, depsAry) {
  if (Object.prototype.toString.call(callback) !== '[object Function]') throw new Error('useEffect函数的第一个参数必须是一个函数')
  if (typeof depsAry === 'undefined') {
    callback()
  } else {
    if (Object.prototype.toString.call(depsAry) !== '[object Array]') throw new Error('useEffect函数的第二个参数必须是一个数组')
    let prevDeps = prevDepsAry[effectIndex]
    let hasChanged = prevDeps ? depsAry.every((dep, index) => dep === prevDeps[index]) === false : true
    if (hasChanged) {
      callback()
    }
    prevDepsAry[effectIndex] = depsAry
    effectIndex++
  }
}
```



3、`useReducer` 的实现原理

```javascript
function useReducer (reducer, initialState) {
  const [state, setState] = useState(initialState)
  function dispatch (action) {
    const newState = reducer(state, action)
    setState(newState)
  }
  return [state, dispatch]
}
```

