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



### 3、`useReducer` 的实现原理

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



### 4、`fiber`

1. `fiber` 出现之前存在的问题
   1. `virtualDom` 在递归调用时会一直占用主线程，不能中断操作
   2. `JavaScript` 是单线程的，不能同时执行多个任务
   3. `JavaScript` 的执行与UI渲染时互斥的
   4. 导致卡顿
2. `fiber` 如何解决
   1. `fiber` 放弃递归
   2. 利用浏览器空闲时间执行比对任务
3. 什么是 `fiber`
   1. `fiber` 是一个执行单元
   2. 每一个 `jsx` 中节点的构建是一个执行单元
   3. 是 `JavaScript` 对象，单向链表，`child`、`return`、`sibling`
4. `fiber` 工作方式
   1. `render` 阶段：构建 `fiber` 对象，生成链表结构，可中断
      - 构建 `root` 的 `fiber` 节点
      - 使用 `requestIdleCallback` 利用空闲时间构建 `fiber` 节点
   2. `commit` 阶段：构建 `dom`，不可中断



### 5、生命周期

> 引用：[React 生命周期](https://juejin.cn/post/6844903842430074893)

- `fiber` 之前

  ![img](D:\资料\juejin-blog\javascript\images\reactjs-1.jpg)



- `fiber` 之后

  ![img](D:\资料\juejin-blog\javascript\images\reactjs-2.jpg)