---
title: es6上手实践
date: 2017-11-28 14:56:34
categories: es6
tags:
  - es6
---

## 1、解构赋值
### a、对象解构赋值
场景：从form表单抽取数据，同时对属性进行重命名和设置默认值
``` js
let person = {
    name: 'xiaoming',
    age: 18
}
const { school: paramName = 'Peking univisty' } = person
console.log({ paramName })
```
### b、函数参数的解构赋值
将函数参数设置成对象，并可设置参数默认值
``` js
function fun ({x = 0, y = 1} = {}) {
    return [x, y]
}
console.log(fun())
console.log(fun({x: 'a'}))
console.log(fun({x: 'a', y: 'b'}))
```
```js
function fetch (url, {body = '', method = 'GET', headers = {}} = {}) {
    console.log(method)
}
fetch('http://google.com', {})
fetch('http://google.com')
```
<!-- more -->
### c、输入模块的指定方法, 并可以进行重命名
``` js
const { SourceMapConsumer, SourceNode: sNode } = require("source-map");
```

### d、遍历map结构
- 任何部署了 Iterator 接口的对象，都可以用for...of循环遍历。Map 结构原生支持 Iterator 接口，配合变量的解构赋值，获取键名和键值就非常方便
- 在需要key、value的对象结构时，尽量多用Map

``` js
const map = new Map
map.set('name', 'xiaoming')
map.set('age', 18)

for (let [key, value] of map) {
    console.log(key + ' is: ' + value)
}
```

## 2、函数的rest参数&数组的扩展运算符
把这两个放在一起比较，是因为它们本身就有相同点和关联性
- 都有三个点（...），关联的都是一个数组，但rest参数的形式是（...参数名），扩展运算符就是三个点（...）
- rest参数将函数多余的参数放入这个数组中，扩展运算符则是将数组转换成逗号分隔的参数序列
- 扩展运算符可以看作是rest参数的逆运算

```js
function add (...values) {
    let sum = 0
    for (let val of values) {
        sum += val
    }
    console.log(sum)
}

let param = [1, 2, 3]
add(1, 2, 3)
add(param)
add(...param)
```

## 3、扩展运算符的应用
### a、替代apply方法，将数组转为函数的参数
```js
function sum (x, y, z) {
    let sum = x + y + z
    console.log(sum)
}
let params = [1, 2, 3]
sum.apply(null, params)
sum(...params)
```

### b、将一个数组添加到另一个数组的尾部
```js
let arr1 = [1, 2, 3]
let arr2 = [4, 5, 6]
arr1.push(...arr2)
console.log(arr1)
```
### c、复制数组
```js
let arr1 = [1, 2, 3]
let arr2 = [...arr1]
console.log(arr2)
```

### d、合并数组
```js
let arr1 = [1, 2, 3]
let arr2 = [4, 5, 6]
[...arr1, ...arr2]
```
### e、任何 Iterator 接口的对象，都可以用扩展运算符转为真正的数组
```js
let nodeList = document.querySelectorAll('div');
let array = [...nodeList];
```

## 4、将类数组对象转换为真正数组的方法
```js
let nodeList = document.querySelectorAll('div');

# 传统方法：
let arr1 = Array.prototype.slice.call(nodeList)

# 扩展运算符方法：
let arr2 = [...nodeList]

# Array.from()方法 
let arr3 = Array.from(nodeList)
```



