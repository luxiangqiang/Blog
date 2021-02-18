# 【2021 第一期】:日常开发 26 个常见的 JavaScript 代码优化方案

本篇文章整理了在日常开发中 30 个常见的 JavaScript 代码优化方案。

>本文章已在 [Github blog](https://github.com/luxiangqiang/Blog) 收录，也可在掘金社会同步阅读（[戳我]()）。欢迎大伙儿～ Star，文章中若存在不足或者 issues，欢迎在下方或 Github 留言！

## 1、`NUll`、`Undefined`、`''`检查
我们在创建新变量赋予一个存在的变量值的时候，并不希望赋予 `null` 或 `undefined`，我们可以采用一下简洁的赋值方式。
```javascript
if(test !== null || test !== undefined || test !== ''){
  let a1 = test;
}

// 优化后
let a1 = test || ''
```


## 2、`null` 值检查并赋予默认值

```javascript
let test = null;
let a1 = test || '';
```

## 3、`undefined` 值检查并赋予默认值

```javascript
let test = undefined;
let a1 = test || '';
```

## 4、空值合并运算符（`??`）
空值合并操作符（`??`）是一个逻辑操作符,当左侧的操作数为 `null` 或者 `undefined` 时，返回其右侧操作数，否则返回左侧操作数。
```javascript
const test= null ?? 'default string';
console.log(test);

console.log(foo); // expected output: "default string"

const test = 0 ?? 42;
console.log(test); // expected output: 0
```
具体介绍可戳这 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

## 5、声明变量
当我们想要声明多个共同类型或者相同值的变量时，我们可以采用一下简写的方式。
```javascript
let test1;
let test2 = 0;

//  优化后
let test1, test2 = 0;
```

## 6、`if` 多条件判断
当我们进行多个条件判断时，我们可以采用数组 `includes` 的方式来实现简写。
```javascript
if(test === '1' || test === '2' || test === '3' || test === '4'){
  // 逻辑
}

// 优化后
if(['1','2','3','4'].includes(test)){
  // 逻辑处理
}
```
## 7、`if...else`  的简写
当存在一层或两层 `if...else`嵌套时，我们可以使用三元运算符来简写。
```javascript
let test = null;
if(a > 10) {
  test = true;
} else {
  test = false;
}

// 优化后
let test = a > 10 ? true : false;
// 或者
let test = a > 10;
```

## 8、多变量赋值
当我们想给多个变量赋不同的值的时候，我们可以采用一下简洁的速记方案。
```javascript
let a = 1;
let b = 2;
let c = 3;

// 优化
let [a, b, c] = [1, 2, 3];
```

## 9、算术运算简写优化
当我们在开发中经常用到算数运算符时，我们可以使用一下方式进行优化和简写。
```javascript
let a = 1;
a = a + 1;
a = a - 1;
a = a * 2;

// 优化
a++;
a--;
a *= 2;
```

## 10、有效值判断
我们经常会在开发中用到的，在这也简单整理一下。
```javascript
if (test1 === true)
if (test1 !== "")  
if (test1 !== null)

// 优化
if (test1)
```

## 11、多条件(`&&`)判断
我们通常在项目中遇到条件判断后跟函数执行，我们可以使用一下简写方式。
```javascript
if (test) {
 foo(); 
} 

//优化
test && foo();
```

## 12、多个比较 `return`

在 return 的语句中使用比较，可以将其进行缩写的形式如下。

```javascript
let test;
function checkReturn() {
    if (!(test === undefined)) {
        return test;
    } else {
        return foo('test');
    }
}

// 优化
function checkReturn() {
    return test || foo('test');
}
```

## 13、`Switch` 的缩写
遇到如下形式的 switch 语句，我们可以将其条件和表达式以键值对的形式存储。
```javascript
switch (type) {
  case 1:
    test1();
  break;
  case 2:
    test2();
  break;
  case 3:
    test();
  break;
  // ......
}

// 优化
var obj = {
  1: test1,
  2: test2,
  3: test
};

obj[type] && obj[type]();
```

## 14、for 循环缩写

```javascript
for (let i = 0; i < arr.length; i++)

// 优化
for (let i in arr) or  for (let i of arr)
```

## 15、箭头函数

```javascript
function add() {
  return a + b;
}

// 优化
const add = (a, b) => a + b;
```

## 16、短函数调用

```javascript
function fn1(){
  console.log('fn1');
}

function fn2(){
  console.log('fn1');
}

if(type === 1){
  fn1();
}else{
  fn2();
}

// 优化
(type === 1 ? fn1 : fn2)();

```

## 17、数组合并与克隆

```javascript
const data1 = [1, 2, 3];
const data2 = [4 ,5 , 6].concat(data1);

// 优化
const data2 = [4 ,5 , 6, ...data1];
```
数组克隆：

```javascript
const data1 = [1, 2, 3];
const data2 = test1.slice()

// 优化
const data1 = [1, 2, 3];
const data2 = [...data1];
```

## 18、字符串模版

```javascript
const test = 'hello ' + text1 + '.'

// 优化
const test = `hello ${text}.` 
```

## 19、数据解构

```javascript
const a1 = this.data.a1;
const a2 = this.data.a2;
const a3 = this.data.a3;

// 优化
const { a1, a2, a3 } = this.data;
```

## 20、数组查找特定值

数组按照索引来查找特定值，我们可以通过逻辑位运算符 `～` 来代替判断。
>“~”运算符（位非）用于对一个二进制操作数逐位进行取反操作
```javascript
if(arr.indexOf(item) > -1) 

// 优化
if(~arr.indexOf(item))

// 或
if(arr.includes(item))
```

## 21、`Object.entries()`
我们可以通过 Object.values() 将对象的内容转化为数组。如下：
```javascript
const data = { a1: 'abc', a2: 'cde', a3: 'efg' };
Object.entries(data);

/** 输出:
[ [ 'a1', 'abc' ],
  [ 'a2', 'cde' ],
  [ 'a3', 'efg' ]
]
**/
```

## 22、`Object.values()`

```javascript
const data = { a1: 'abc', a2: 'cde' };
Object.values(data);

/** 输出:
[ 'abc', 'cde']
**/
```

## 23、求平方

```javacript
Math.pow(2,3); 

// 优化
2**3；
```

## 24、指数简写

```javascript
for (var i = 0; i < 100000; i++)

// 优化
for (var i = 0; i < 1e4; i++) {
```

## 25、对象属性简写

```javascript
let key1 = '1'; 
let key2 = 'b';
let obj = {key1: key1, key2: key2}; 

// 简写
let obj = {
  key1, 
  key2
};
```

## 26、字符串转数字

```javascript
let a1 = parseInt('100'); 
let a2 = parseFloat('10.1'); 

// 简写 
let a1 = +'100'; 
let a2 = +'10.1';
```