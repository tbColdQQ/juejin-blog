### 1、`new` 关键字的实现

```javascript
function newImpl (Cl) {
  var obj = {}
  var args = Array.prototype.slice.call(arguments, 1)
  obj.__proto__.contructor = Cl
  obj.__proto__ = Cl.prototype
  Cl.apply(obj, args)
  return obj
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

