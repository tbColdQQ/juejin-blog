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

