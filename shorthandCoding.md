> 原文：[19+ JavaScript Shorthand Coding Techniques](https://www.sitepoint.com/shorthand-javascript-techniques/)                     
> 本文原链接：https://segmentfault.com/a/1190000011229633
# 1 使用三目运算符
使用三目运算符，可以更简洁地把if else写成一行
```JavaScript
const x = 20;
let answer;
if (x > 10) {
    answer = 'greater than 10';
} else {
    answer = 'less than 10';
}
```
```JavaScript
const answer = x > 10 ? 'greater than 10' : 'less than 10';
```
# 2 短路求值
当你把一个变量的值赋给另一个变量，如果你要求原变量不能是空或者未定义，你有一长一短两种写法
```JavaScript
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
     let variable2 = variable1;
}
```
```JavaScript
const variable2 = variable1  || 'new';
```
# 3 声明变量的简写
```JavaScript
let x;
let y;
let z = 3;
```
写成
```JavaScript
let x, y, z=3;
```
（译者注：其实现在standard风格不推荐声明简写）
# 4 if的简写
```JavaScript
if (likeJavaScript === true)
//简化为
if (likeJavaScript)
```
> 注意：这两个例子不严格相等，`likeJavaScript`还可能是其他“为真”的值，参考[这里](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)
```JavaScript
let a;
if ( a !== true ) {
// do something...
}
//简化为
let a;
if ( !a ) {
// do something...
}
```
# 5 JavaScript for循环简写
```JavaScript
for (let i = 0; i < allImgs.length; i++)
//简化为
for (let index of allImgs)
//译者拓展，用于循环key，不推荐在数组使用
for (let index in allImgs)
```
# 6 短路求值
其实就是第二点...
# 7 十进制指数
可能你早就知道了，这是一个不用在末尾写一堆0的方法。例如1e7代表1后面跟7个0，也就是十进制的1000000。
```JavaScript
for (let i = 0; i < 1e7; i++) {}

// All the below will evaluate to true
1e0 === 1;
1e1 === 10;
1e2 === 100;
1e3 === 1000;
1e4 === 10000;
1e5 === 100000;
```
# 8 对象属性的缩写
ES6提供的方法让你更简单地创建对象字面量，如果属性名和值一样的话，你可以如下缩写
```JavaScript
const obj = { x:x, y:y };
// 等同于
const obj = { x, y };
```
# 9 用箭头函数让代码更简洁
```JavaScript
function sayHello(name) {
  console.log('Hello', name);
}

setTimeout(function() {
  console.log('Loaded')
}, 2000);

list.forEach(function(item) {
  console.log(item);
});
// 简化为
sayHello = name => console.log('Hello', name);

setTimeout(() => console.log('Loaded'), 2000);

list.forEach(item => console.log(item));
```
另外，注意箭头函数里的this和普通函数不同
# 10 箭头函数的隐形return
```JavaScript
function calcCircumference(diameter) {
  return Math.PI * diameter
}
// 简化为
calcCircumference = diameter => Math.PI * diameter
```
注意：这个情况下返回的必须是一行语句，如果返回对象要加`()`，多行语句还是用`{}`和`return`吧
# 11 默认参数
ES6允许你的函数有默认参数了，赶紧用起来
```JavaScript
function volume(l, w, h) {
  if (w === undefined)
    w = 3;
  if (h === undefined)
    h = 4;
  return l * w * h;
}
// 简化为
volume = (l, w = 3, h = 4 ) => (l * w * h);

volume(2) //output: 24
```
# 12 反引号与模板字符串
```JavaScript
const welcome = 'You have logged in as ' + first + ' ' + last + '.'

const db = 'http://' + host + ':' + port + '/' + database;
// 简化为
const welcome = `You have logged in as ${first} ${last}`;

const db = `http://${host}:${port}/${database}`;
```
# 13 结构赋值
引入一个组件之后你还要一个一个拆出来？现在不用了！
```JavaScript
const observable = require('mobx/observable');
const action = require('mobx/action');
const runInAction = require('mobx/runInAction');

const store = this.props.store;
const form = this.props.form;
const loading = this.props.loading;
const errors = this.props.errors;
const entity = this.props.entity;
```
```JavaScript
import { observable, action, runInAction } from 'mobx';

const { store, form, loading, errors, entity } = this.props;
// 你还可以更改变量名
const { store, form, loading, errors, entity:contact } = this.props;
```
# 14 反引号与多行字符串
```JavaScript
JavaScriptconst lorem = 'Lorem ipsum dolor sit amet, consectetur\n\t'
    + 'adipisicing elit, sed do eiusmod tempor incididunt\n\t'
    + 'ut labore et dolore magna aliqua. Ut enim ad minim\n\t'
    + 'veniam, quis nostrud exercitation ullamco laboris\n\t'
    + 'nisi ut aliquip ex ea commodo consequat. Duis aute\n\t'
    + 'irure dolor in reprehenderit in voluptate velit esse.\n\t'
// 简化为
const lorem = `Lorem ipsum dolor sit amet, consectetur
    adipisicing elit, sed do eiusmod tempor incididunt
    ut labore et dolore magna aliqua. Ut enim ad minim
    veniam, quis nostrud exercitation ullamco laboris
    nisi ut aliquip ex ea commodo consequat. Duis aute
    irure dolor in reprehenderit in voluptate velit esse.`
```
# 15 扩展运算符
可以代替一些数组操作，并且比数组操作更灵活
```JavaScript
// joining arrays
const odd = [1, 3, 5];
const nums = [2 ,4 , 6].concat(odd);

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = arr.slice()
```
```JavaScript
// joining arrays
const odd = [1, 3, 5 ];
const nums = [2 ,4 , 6, ...odd];
console.log(nums); // [ 2, 4, 6, 1, 3, 5 ]

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
```
译者：扩展运算符就等于把内容摊开，你可以简单理解为把`[]`去掉
跟concat()不同，你可以在数组任何地方使用扩展运算符展开
```JavaScript
const odd = [1, 3, 5 ];
const nums = [2, ...odd, 4 , 6];
```
也可以结合结构赋值使用
```JavaScript
const { a, b, ...z } = { a: 1, b: 2, c: 3, d: 4 };
console.log(a) // 1
console.log(b) // 2
console.log(z) // { c: 3, d: 4 }
```
# 16 强制参数（其实又跟11一样）
```JavaScript
function foo(bar) {
  if(bar === undefined) {
    throw new Error('Missing parameter!');
  }
  return bar;
}
// 简化为
mandatory = () => {
  throw new Error('Missing parameter!');
}

foo = (bar = mandatory()) => {
  return bar;
}
```
# 17 Array.find
你可能用for循环写过一个find函数，但是ES6已经引入了这个新特性！
```javascript
const pets = [
  { type: 'Dog', name: 'Max'},
  { type: 'Cat', name: 'Karl'},
  { type: 'Dog', name: 'Tommy'},
]

function findDog(name) {
  for(let i = 0; i<pets.length; ++i) {
    if(pets[i].type === 'Dog' && pets[i].name === name) {
      return pets[i];
    }
  }
}
// 简化为
pet = pets.find(pet => pet.type ==='Dog' && pet.name === 'Tommy');
console.log(pet); // { type: 'Dog', name: 'Tommy' }
```
(译者：find跟filter的区别是filter返回数组，find只返回找到的第一个)
# 18 Object [key]
你知道`foo.bar`可以写成`foo['bar']`吗？当然，不是知道这种用法就该这么用，但是这么写可以让你重用一些代码。
以下是一个简单的验证函数
```javascript
function validate(values) {
  if(!values.first)
    return false;
  if(!values.last)
    return false;
  return true;
}

console.log(validate({first:'Bruce',last:'Wayne'})); // true
```
这个函数完美地完成了他的任务，但是当你有很多表单需要验证，而且格式和规则都不同的时候，你就需要一个通用的验证函数了。
```javascript
// object validation rules
const schema = {
  first: {
    required:true
  },
  last: {
    required:true
  }
}

// universal validation function
const validate = (schema, values) => {
  for(field in schema) {
    if(schema[field].required) {
      if(!values[field]) {
        return false;
      }
    }
  }
  return true;
}


console.log(validate(schema, {first:'Bruce'})); // false
console.log(validate(schema, {first:'Bruce',last:'Wayne'})); // true
```
# 19 双重按位非
双重按位非的效果等于Math.floor()
```javascript
Math.floor(4.9) === 4  //true
// 相当于
~~4.9 === 4  //true
```
注意注意，这条确实不利于其他人看懂，需要合作的项目勿用，用了记得加注释
# 20 由你来补充 ？
# 21 那我来补充一条吧！双重*
```javascript
3 ** 3 === 3 * 3 * 3
//a ** b就是a的b次方，也不用调用Math的方法了
``` 