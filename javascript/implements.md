### 1、`new` 关键字的实现

```javascript
function newImpl (fn, ...args) {
  if (typeof fn !== 'function') {
    throw 'fn must be a function'
  }
  var obj = new Object()
  obj.__proto__ = Object.create(fn.prototype)
  var res = fn._apply(obj, [...args])

  return (typeof res === 'object' && res !== null) || typeof res === 'function' ? res : obj
}
```



### 2、`instanceof` 关键字的实现

```javascript
function instanseofImpl (obj, Cl) {
  var instanceObj = obj.__proto__
  var prototypeObj = Cl.prototype
  while(instanceObj) {
    if (instanceObj === prototypeObj) {
	  return true
	}
	instanceObj = instanceObj.__proto__
  }
  return false
}
```



### 3、类型判断

```javascript
function checkType (obj) {
  if (obj === null) return String(obj)
  var typeStr = Object.prototype.toString.call(obj)
  return typeStr.split(' ')[1].split(']')[0]
}
```



### 4、防抖

```javascript
function debounce (fn, time) {
  let timer = null
  return function () {
    if (timer) clearTimeout(timer)
    timer = setTimeout(() => {
      fn.call(this)
    }, time)
  }
}
```



### 5、节流

```javascript
function throttle (fn, time) {
  let canRun = true
  return function () {
    if (!canRun) return false
    canRun = false
    setTimeout(() => {
      fn.call(this)
      canRun = true
    }, time)
  }
}
```

### 6、 `call` 和 `apply`

```javascript
Function.prototype._call = function (context, ...args) {
  var context = context || window
  context.fn = this
  var res = eval('context.fn(...args)')
  delete context.fn
  return res
}
Function.prototype._apply = function (context, args) {
  var context = context || window
  context.fn = this
  var res = context.fn(...args)
  delete context.fn
  return res
}
```

### 7、 `bind`

```javascript
Function.prototype._bind = function (context, ...args) {
  if (typeof this !== 'function') {
    throw 'this must be a function'
  }
  var self = this
  var res = function () {
    self.apply(this instanceof self ? this : context, [...args])
  }
  if (this.prototype) {
    res.prototype = this.prototype
  }
  return res
}
```
