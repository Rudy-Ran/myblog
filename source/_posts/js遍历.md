---
title: JS遍历
date: 2018-12-07 20:35:07
tags: JavaScript
---
JS的遍历操作有多种方式，本篇文章就详细总结一下JS中的各种遍历操作
### 普通for循环操作
```javascript
var arr = ['rudy','bob','tom','jack','mark'];
for(var i=0;i<arr.length;i++){
    console.log(arr[i]);
}
```
### 优化版本for循环操作
```javascript
for(var j=0,len=arr.length;j<len;j++){
    console.log(arr[j]);
}
```
优点是使用一个变量，将数组长度暂存起来，这样就不需要每次循环操作都获取一次数组长度，数据量大时，优化效果明显
### forEach遍历
```javascript
var arr = ['rudy','bob','tom','jack','mark'];
arr.forEach(function(value,i){
    console.log(value);
});
```
实际性能很低，并且不能通过break中断循环，也不能使用return返回到外层
### map遍历
```javascript
var arr = ['rudy','bob','tom','jack','mark'];
arr.map(function(value,i){
    console.log(value);
});

var temp =  arr.map(function(value,i){
    console.log(value);
    return 'Hi! '+value;
});
console.log(temp)
```
对比forEach,map支持return语句,return方式只是将元素组克隆一份，并不改变原数组的值
### for in遍历
```javascript
var arr = ['rudy','bob','tom','jack','mark'];
for(var index in arr){
   console.log(arr[index]);
}
```
效率最低，不建议使用这种方式
### for of遍历
```javascript
var arr = ['rudy','bob','tom','jack','mark'];
for(let val of arr){
   console.log(val);
}
```
对比forEach,它可以正确响应break、continue和return语句 
### filter( )遍历
```javascript
var arr = ['rudy','bob','tom','jack','mark'];
var newArr =  arr.filter(item=>item!='rudy');
console.log(arr,newArr);
```
不改变原数组,对每一个元素执行callback的回调函数，返回符合条件的元素数组
### every( )遍历
```javascript
var arr = [ 1, 2, 3, 4, 5, 6 ]; 
console.log( arr.every( function( item, index, array ){ 
        return item > 3; 
    })); 
//false
```
every()是对数组中的每一项运行给定函数，如果该函数对每一项返回true,则返回true
### some( )遍历
```javascript
var arr = [ 1, 2, 3, 4, 5, 6 ]; 
console.log( arr.some( function( item, index, array ){ 
        return item > 3; 
    })); 
//true
```
some()是对数组中每一项运行指定函数，如果该函数对任一项返回true，则返回true
### keys( ) values( ) entries( )
ES6新增的三种方法,keys()是对键名的遍历,values()是对键值的遍历,entries()是对键值对的遍历
```javascript
var arr = ['rudy','bob','tom','jack','mark'];
for (let index of arr.keys()) {
console.log(index);
}
// 0 1 2 3 4
for (let elem of arr.values()) {
console.log(elem);
}
// 'rudy','bob','tom','jack','mark'
for (let [index, elem] of arr.entries()) {
console.log(index, elem);
}
// 0 'rudy' 1 'bob' 2 'tom' 3 'jack' 4 'mark'
```