---
title: Js里的循环
categories:
    - JS
    - loop
tags:
    - Javascript
    - 循环
preview: 100
---
## javascript里数组循环
 
> 重要提示: 对于`es6`新增的`for of`，里面可以使用 `async/ await`,其它几种循环均无法做到。
 
### `for` ：自定义循环
 
> - for循环，根据数组的length手动设置循环条件
 
```javascript
var array = [1,2,3,4,5];
for (var i = 0; i < array.length; i++) { 
    console.log(i,array[i]);
}
/*output*/
/*
  0 1
  1 2
  2 3
  3 4
  4 5
*/
```
 
 
 
### `for in` ：循环索引
 
> - `for in` 算是最常用的循环方式
 
```javascript
var array = [1,2,3,4,5];
for(let i in array) { 
   console.log(i,array[i]); 
};
/*output*/
/*
  0 1
  1 2
  2 3
  3 4
  4 5
*/
```
 
### `forEach` ：循环索引及值
 
> - `array.forEach` 的用法： `array.forEach(function(currentValue, index, arr), thisValue)`
> - 其中 `thisValue` 为回调函数里的 `this` 指向
 
```javascript
var array = [1,2,3,4,5];
array.forEach((item,index,arr)=>{
  console.log(index,item)
})
/*output*/
/*
  0 1
  1 2
  2 3
  3 4
  4 5
*/
```
 
### `for of` ：循环值
 
> - for of循环为 `es6` 的新增循环方法，如下代码，注意输出结果对比和 `for in` 的不同
 
```javascript
var array = [1,2,3,4,5];
for(let i of array){
  console.log(i)
}
/*output其中i直接输出的是数组的值,而不是数组下标*/
/*
  1
  2
  3
  4
  5
*/
```
 
### `array.map` ：循环时，依次修改数组
 
> - `array.map` 的用法： `array.map(function(item, index, arr), thisValue)` , 可以看出和array.forEach非常相似，但不同的是array.forEach只是个循环，没有返回值，而array.map在循环的时候需要指定返回值，也就是说修改在循环的过程中修改array里本次循环的 `value` 值，看下面实例，估计能更好懂一些
> - 简单来说， `array.map` 方法可以修改一个数组每一项的值，并 `返回一个新数组`
 
```javascript
var array = [1, 4, 9, 16];
 
// pass a function to map
const map = array.map(function(item){return item*2});
 
console.log(map);
// output: [2, 8, 18, 32]
```
 
### `array.filter` ：循环时，过滤出自己需要的值
 
> - array.filter的用法： `array.filter(function(item, index, arr), thisValue)` ,其用法和 `forEach` & `map` 一样，但其作用是在循环的过程中过滤掉出数组中我们需要的数据，并 `返回过滤后的新数组`
 
```javascript
var array = [1,4,9,16];
const filter = array.filter(function(item,index,arr){
  return item>=9; // 如果item大于或等于9，则返回true
})
 
console.log(filter);
// output: [9,16] 得到数组里大于或等于9的新数组
```
 
### `小结Tips`
 
对于js中需要掌握的循环基本就上面5种，当然还有一些其他的，但确实不常用
 
主要还是要区别下各自的使用场景：其中 `forEach` 、 `map` 、 `filter` ,这三个是 `用法一样，但功能不一样`
 
而 `forEach` 和 `for in` ，两个都是 `用法不一样，但功能一样` ,但即便功能一样，也有不同点，如下说明：
 
> 1. 首先 `for in` 的循环顺序是依赖于环境的，所以它循环一个数组，不一定是按照顺序依次循环，而 `forEach` 可以避免这个问题
> 2. 还有一个就是循环里包含异步执行问题，请看下面代码，注意输出结果上的区别
 
```javascript
let arr = [1,2,3,4,5]
for(var i in arr){
  setTimeout(()=>{console.log(`delay-i:${i}`)},0)
}
/*output 如下结果会发现输出的都是4，这并不是我们想要的，当然这个问题也可以使用es6的let来解决，将for里的var改成let即可*/
/*
  delay-i:4
  delay-i:4
  delay-i:4
  delay-i:4
  delay-i:4
*/
 
arr.forEach(function(item,index,arr){
  setTimeout(()=>{console.log(`delay-index:${index}`)},0)
})
/*output*/
/*
  delay-index:0
  delay-index:1
  delay-index:2
  delay-index:3
  delay-index:4
*/
```