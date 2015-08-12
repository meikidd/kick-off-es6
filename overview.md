# ES6 Overview


## What's ES6


### ES6 or ECMAScript 2015 ?
[ECMAScript 6](http://www.ecma-international.org/ecma-262/6.0/)（以下简称ES6）是JavaScript语言的下一代标准，已经在2015年6月正式发布了。

ECMA-262 标准 第6版。计划以后每年发布一次标准，使用年份作为标准的版本。因为当前版本是在2015年发布的，所以又称ECMAScript 2015。

ECMA - European Computer Manufacturers Association(欧洲计算机制造商协会)

ECMA-262 被 ISO 国际标准化组织采纳为 [ISO/IEC 16262:2011](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=55755)

ES6 不包含 DOM、BOM

### Where can I use
- node.js / io.js
- browser
- anywhere else 
  - NW.js (node-webkit)
  - Electron (atom-shell)
- ES6 兼容性 [对比表格](http://kangax.github.io/compat-table/es6/)

## Well-known Features

### let and const

#### let 命令
原来的 javascript 中没有块级作用域，只有函数级作用域。ES6 中新增了 let 命令，使用 let 命令代替 var 命令声明变量，具有块级作用域。

- 函数级作用域

```
function test() {
  var hello = 'world';
  console.log(hello);
}
test(); // 'world'
console.log(hello); // Error: hello is not defined
```

- 块级作用域

`var` 命令

```
if(true) {
  var hello = 'world';
  console.log(hello); // 'world'
}
console.log(hello); // 'world'
```
  
`let` 命令

```
if(true) {
  let hello = 'world';
  console.log(hello); // 'world'
}
console.log(hello); // Error: hello is not defined
```

#### const 命令
使用 const 命令声明常量

```
const STATUS_NOT_FOUND = 404;
```
常量的值为只读，不能修改

```
STATUS_NOT_FOUND = 200;
// SyntaxError: "STATUS_NOT_FOUND" is read-only
```

### Template String
- 传统的字符串

```
var name = 'es6';

var sayhello = 'hello, \
my name is ' + name + '.';

console.log(sayhello); 
```
输出：

```
hello, my name is es6.
```

- ES6 模板字符串

```
var name = 'es6';

var sayhello = `hello,
my name is ${name}.`;

console.log(sayhello);
```
输出(多行)：

```
hello,
my name is es6.
```

### Arrow Function
允许使用 `=>` 定义函数，箭头函数自动绑定当前上下文 this。

```
x => x+1
```
等同于匿名函数

```
function (x) {
  return x + 1;
}
```

- 多个参数：

```
(a,b) => a+b
```
```
function (a, b) {
  return a + b;
}
```

- 多行函数体：

```
(a,b) => {
	console.log(a + b);
	return a + b;
}
```
```
function (a, b) {
	console.log(a + b);
	return a + b;
}
```

### Promise
原生的 Promise 实现，不再需要 `bluebird` 或 `Q+`。

### Generator
Generator 生成器允许你通过写一个可以保存自己状态的的简单函数来定义一个迭代算法。

Generator 是一种可以停止并在之后重新进入的函数。生成器的环境（绑定的变量）会在每次执行后被保存，下次进入时可继续使用。generator 字面上是“生成器”的意思，在 ES6 里是迭代器生成器，用于生成一个迭代器对象。

```
function *gen() {
    yield 'hello';
    yield 'world';
    return true;
}
```
以上代码定义了一个简单的 generator，看起来就像一个普通的函数，区别是function关键字后面有个*号，函数体内可以使用yield语句进行流程控制。

```
var iter = gen();
var a = iter.next();
console.log(a); // {value:'hello', done:false}
var b = iter.next();
console.log(b); // {value:'world', done:false}
var c = iter.next();
console.log(c); // {value:true, done:true}
```
当执行gen()的时候，并不执行 generator 函数体，而是返回一个迭代器 Iterator。迭代器具有 next() 方法，每次调用 next() 方法，函数就执行到yield语句的地方。next() 方法返回一个对象，其中value属性表示 yield 关键词后面表达式的值，done 属性表示是否遍历结束。generator 生成器通过 next 和 yield 的配合实现流程控制，上面的代码执行了三次 next() ，generator 函数体才执行完毕。

### Class
在 JavaScript 中引入 OO 面向对象。实际上是语法糖，只是看上去更面向对象而已。也有观点极力反对 Class，认为 Class 隐藏了 JavaScript 本身原型链的语言特性，使其更难理解。

- ES5

```
function Point(x,y){
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
}
```

- ES6

```
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '('+this.x+', '+this.y+')';
  }

}
```

### Module
JavaScript 一直没有标准的模块体系，社区主流解决方案有 CommonJS 和 AMD，分别用于服务器端和浏览器端，浏览器端还有 seajs 遵循的 CMD。

CommonJS

```
exports.firstName = 'mei';
exports.lastName = 'qingguang';
exports.year = 1988;

// or

module.exports = {
	firstName: 'mei',
	lastName: 'qingguang',
	year: 1988
}

// or

module.exports = function() {
	// do something
}
```

AMD

```
define(['./a', './b'], function(a, b) { // 依赖必须一开始就写好
	a.doSomething()
	// 此处略去 100 行
	b.doSomething()
	// ...
	
	exports.action = function() {};
}) 
```

CMD

```
define(function(require, exports, module) {
	var a = require('./a')
	a.doSomething()
	// 此处略去 100 行
	var b = require('./b') // 依赖可以就近书写
	b.doSomething()
	// ... 
	
	exports.action = function() {};
})
```

ES6 Module

- export

```
export var firstName = 'mei';
export var lastName = 'qingguang';
export var year = 1988;

// or

var firstName = 'mei';
var lastName = 'qingguang';
var year = 1988;

export {firstName, lastName, year};

// or

export default function() {
	console.log('My name is mei qingguang');
};
```

- import

```
import {firstName, lastName, year} from './profile'

console.log(firstName, lastName, year)

// or

import * as Profile from './profile'

console.log(Profile.firstName, Profile.lastName, Profile.year)

// or

import sayMyName from './profile' 

console.log(sayMyName())
```

## 运行环境

### node.js io.js

## 编译器

### Babel

### Who's using Babel

## ES6 in AMS

