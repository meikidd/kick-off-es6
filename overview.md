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

### Template Strings
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
输出两行：

```
hello,
my name is es6.
```

### Arrow Functions
### Promise
### Generators
### Class
### Module
前端摩尔定理


## 运行环境

### node.js io.js

## 编译器

### Babel

### Who's using Babel

## ES6 in AMS

