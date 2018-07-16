# JavaScript

<!-- ![img](../assets/image/site/code-map.png) -->

![front-end-developer](../assets/image/site/code-dev.gif)

## 常用缩写

* Null, Undefined, Empty 值判断速写(** variable || '' **)

```javascript
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
  let variable2 = variable1
}
// 简写
let variable2 = variable1 || ''
```

* String 转 Number 类型(** +variable **)

```javascript
let n = '12.34'
let m = Number(a) + 10
// 简写
let n = '12.34'
let m = +n + 10
```

* 其他类型转 Boolean 类型(** !!variable **)

```javascript
let a = 'true'
let b = Boolean(a)
// 简写
let a = 'true'
let b = !!a
```

* 一般变量的赋值和判断(** [a, b, c] **)

```javascript
let a = new Array()
a[0] = 'myString1'
a[1] = 'myString2'
a[2] = 'myString3'
// 简写
let a = ['myString1', 'myString2', 'myString3']
```

* `variable ? 'val1': 'val2'`

```javascript
let big
if (x > 10) {
  big = true
} else {
  big = false
}
// 简写
let big = x > 10 ? true : false
```

```javascript
let x
let y
let z = 3
// 简写
let x,
  y,
  z = 3
```

* `++, --, +=, -=, \*=, /=`

```javascript
x = x + 1
minusCount = minusCount - 1
y = y * 10
// 简写
x++
minusCount--
y *= 10
```

* `/^d/`

```javascript
var re = new RegExp('d+(.)+d+', 'igm'),
  result = re.exec('padding 01234 text text 56789 padding')
console.log(result) //"01234 text text 56789"
// 简写
var result = /d+(.)+d+/gim.exec('padding 01234 text text 56789 padding')
console.log(result) //"01234 text text 56789"
```

* arguments

```javascript
function myFunction(myString, myNumber, myObject, myArray, myBoolean) {
  // do something...
}
myFunction('String', 1, [], {}, true)
// 简写
function myFunction() {
  console.log(arguments.length) // Returns 5
  for (i = 0; i < arguments.length; i++) {
    console.log(typeof arguments[i]) // Returns string, number, object, object, boolean
  }
}
myFunction('String', 1, [], {}, true)
```

```javascript
'myString'.charAt(0)

// 简写
'myString'[0] // Returns 'm'
```

```javascript
function x() {
  console.log('x')
}
function y() {
  console.log('y')
}
let z = 3
if (z == 3) {
  x()
} else {
  y()
}
// 简写
function x() {
  console.log('x')
}
function y() {
  console.log('y')
}
let z = 3
;(z == 3 ? x : y)() // Short version!
```

```javascript
for (let i = 0; i < 10000; i++) {}
// 简写
for (let i = 0; i < 1e4; i++) {}
```