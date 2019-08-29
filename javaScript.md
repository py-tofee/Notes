# JavaScript
#### 一. call, apply, bind

区别：在JavaScript中，call、apply和bind是Function对象自带的三个方法，都是为了改变函数体内部 this 的指向。
apply 、 call 、bind 三者第一个参数都是 this 要指向的对象，也就是想指定的上下文；
apply 、 call 、bind 三者都可以利用后续参数传参；
bind 是返回对应 函数，便于稍后调用；
apply 、call 则是立即调用。

#### 1. call & apply
call() 方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。
可以使用 call 来实现继承：写一个方法，然后让另外一个新的对象来继承它（而不是在新对象中再写一次这个方法）


apply() 方法调用一个具有给定this值的函数，以及作为一个数组（或类似数组对象）提供的参数。


**语法**
```
function.call(thisArg, arg1, arg2, ...)
```

```
function.apply(thisArg, [argsArray])
```
**参数**

```
// 如果不指定this值，那么this值默认会被绑定为全局对象
// 如果在严格模式下，this的值将会是undefined
if(thisArg == undefined|null)
 this = window
if(thisArg == number|boolean|string)
 this == new Number()|new Boolean()| new String()
```


**用法**

可以使用apply合并数组
```
var arr1 = [1,2],arr2 = [3,4]
Array.prototype.push.apply(arr1, arr2); // arr1 -> [1,2,3,4]
```
使用 call 方法调用父构造函数
```
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

var cheese = new Food('feta', 5);
```
#### 2. bind
bind()方法返回一个原函数的拷贝，并拥有指定的this值和初始参数

**语法**
```
function.bind(thisArg[, arg1[, arg2[, ...]]])
```
**用法**

```
this.x = 9; // this --> window

var module = {
    x: 81,
    getX: function () {return this.x}
}
module.getX(); // 81

var retrieveX = module.getX;
retrieveX(); // 9 --> 此时this指向全局的window对象

var boundGetX = retrieveX.bind(module);
boundGetX(); // 81
```


