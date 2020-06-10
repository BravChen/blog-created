---
title: 深拷贝 & 浅拷贝
date: 2020-05-08 15:07:06
tags:
slug: a0000005
---

## 浅拷贝一个对象

概念：浅拷贝的内容只会拷贝第一层，所以对象内的属性还是指向相同的地址，还是都会被改变。

**普通浅拷贝**

```js
let objA = {
    name: {
        x: 'a'
    }
}
let objB = Object.assign({}, objA)
objB.name.x = 'b'
console.log(objA.name) // {x: "b"}
```

**ES6的浅拷贝**

```js
let objA = {
    name: {
        x: 'a'
    }
}
let objB = {...objA}
console.log(objB) // {name: {x: "b"}}
```

## 普通深拷贝

满足以下条件

1. 这个对象没有复杂的对象，例如：日期、正则、函数、循环、引用、普通对象之外的所有对象

2. 这个对象没有 undefined

代码：

```js
JSON.parse(JSON.stringify(data))
```

> 这个方法不适用于复杂对象



<!-- ## 递归? -->