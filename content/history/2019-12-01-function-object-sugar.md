---
weight: 20
title: 函数与对象的语法糖一
categories:
  - 前端
tags:
  - JavaScript
  - ES6
date: 2019-12-01 18:32:01
abbrlink: 1932443659
---

## 或语法(`||`)

### 传参案例

```js
function sum(a, b){
    console.log(b)
    return a+b
}
console.log('返回值：'+sum(1))
```

**此时 b 的值是 undefined ，所以结果是 NaN 无法相加，打出的 b 为 undefined**

**为了避免这种情况，可以使用以下写法：**

### ES6写法

如果 a 或 b === undefined，则等于 0 。相当于未传值时的默认值为 0

```js
function sum(a=0, b=0){
    return a+b
}
```

> 其中 `a=0` 相当于 `if(a===undefined){ a=0 }`，b 同理

### ES6之前的写法

如果 b 为真，则 b = b 否则 b = 0 ，a 同理

```js
function sum(a, b){
    a = a || 0
    b = b || 0
    return a+b
}
```

> 其中 `b = b || 0` 相当于 `if(b){ b = b }else{ b = 0 }`

### JS与Python添加数组的区别

JS

每次添加都会重新初始化一个数组

```js
function push(item, array=[]){
    array.push(item)
    return array
}
console.log(push(1))
// 输出: >[1]
console.log(push(2))
// 输出: >[2]
```

Python

只会初始化一次数组

```python
def fn(item, array=[])
    array.append(item)
    return array

fn(1)
# 输出 [1]
fn(2)
# 输出 [1, 2]
```

## 剩余参数

### 1. 之前的JS写法

如果函数需要传入多个未知数量的参数：

```js
function sum(){
    let result = 0
    for(let i=0;i<arguments.length;i++){
        result += arguments[i]
    }
    return result
}
sum(1,2,3,4,5,6,7,8,9,10)
// 输出: 55
```

### 2. 参数区分

如果在传入的多个参数前加一个前缀的参数，可以用以下写法：

```js
function sum(message){
    let result = 0
    for(let i=1;i<arguments.length;i++){
        result += arguments[i]
    }
    return message + result
}
sum('结果是: ',1,2,3,4,5,6,7,8,9,10)
// 输出: 
// 结果是: 55
```

上面的写法就是从第二个参数开始循环将每个参数相加，最后再与第一个参数相加

### 3. ES6 参数区分

ES6 中使用了更简洁的参数区分的写法

```js
function sum(message, ...numbers){
    let result = 0
    for(let i=0;i<numbers.length;i++){
        result += numbers[i]
    }
    return message + result
}
sum('结果是: ',1,2,3,4,5,6,7,8,9,10)
// 输出: 
// 结果是: 55
```

### 4. ES6 参数区分(简化for循环)

下面的案例中使用了 `.reduce((p,v)=>p+v, 0)` 方法简化了 for 循环

```js
function sum(message, ...numbers){
    let result = numbers.reduce((p,v)=>p+v, 0)
    return message + result
}
sum('结果是: ',1,2,3,4,5,6,7,8,9,10)
// 输出: 
// 结果是: 55
```

### 5. ES6 伪数组转数组

```js
function sum(message){
    let args = Array.prototype.slice.call(arguments) // ES5中最便捷的数组转换方式
    let args = Array.from(arguments) // ES6语法
    let args = [...arguments] // ES6语法
    let result = numbers.reduce((p,v)=>p+v, 0)
    return message + result
}
sum('结果是: ',1,2,3,4,5,6,7,8,9,10)
```

> 伪数组：原型链直接指向对象，只有数组的样子，但是没有数组的方法

## 展开语法(Spread syntax)

### 1. 截取数组后半部分内容

截取数组后半部分内容组成新的数组

```js
let array1 = [1, 2, 3, 4, 5, 6]
let [a, b, c, ...array2] = array1
console.log(array2)
// 输出 [4, 5, 6]
```

### 2. 截取数组后半部分内容(简化)

简化前面的参数

```js
let array1 = [1, 2, 3, 4, 5, 6]
let [,,, ...array2] = array1
console.log(array2)
// 输出 [4, 5, 6]
```

### 3. 数组前后追加项

在数组的最前和最后分别追加项

```js
let array1 = [1, 2, 3, 4, 5, 6]
let array2 = [0, ...array1, 7]
console.log(array2)
// 输出 [0, 1, 2, 3, 4, 5, 6, 7]
```

### 拓展：ES6之前的写法

```js
let array1 = [1, 2, 3, 4, 5, 6]
let array2 = [0].concat(array1).concat(7)
console.log(array2)
// 输出 [0, 1, 2, 3, 4, 5, 6, 7]
```
