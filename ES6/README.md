# 部分ES6语法概要（Babel下的ES6兼容性与规范）

[附：Babel在实际的开发中使用，一份关于ES6部分的规范](https://github.com/ouvens/es6-code-style-guide)

>对照表
<table>
<tr>
  <td>ES6</td> <td>支持</td>
</tr>
<tr>
  <td>箭头函数</td> <td>支持</td>
</tr>
<tr>
  <td>类的声明和继承</td> <td>部分支持，IE8不支持</td>
</tr>
<tr>
  <td>增强的对象字面量</td> <td>支持</td>
</tr>
<tr>
  <td>字符串模板</td> <td>支持</td>
</tr>
<tr>
  <td>解构</td> <td>支持，但注意使用方式</td>
</tr>
<tr>
  <td>参数默认值，不定参数，拓展参数</td> <td>支持</td>
</tr>
<tr>
  <td>let与const	</td> <td>支持</td>
</tr>
<tr>
  <td>for of</td> <td> IE不支持</td>
</tr>
<tr>
  <td>iterator, generator</td> <td>不支持</td>
</tr>
<tr>
  <td>模块 module、Proxies、Symbol</td> <td>不支持</td>
</tr>
<tr>
  <td>Map，Set 和 WeakMap，WeakSet</td> <td>不支持</td>
</tr>
<tr>
  <td>Promises、Math，Number，String，Object 的新API</td> <td>不支持</td>
</tr>
<tr>
  <td>export & import</td> <td>不支持</td>
</tr>
<tr>
  <td>Promises、Math，Number，String，Object 的新API</td> <td>不支持</td>
</tr>
<tr>
  <td>export & import</td> <td>支持</td>
</tr>
<tr>
  <td>生成器函数</td> <td>不支持</td>
</tr>
<tr>
  <td>数组拷贝</td> <td>支持</td>
</tr>
</table>

在es6的新特性中，一些复杂结构的仍然不支持对es5转换的兼容，具体可以看下面的实例~

### 1.1 箭头操作符

箭头操作符可以简洁的描述一个函数

```js
// ES6
var fn= v => console.log(v);
```
转换后
```js
 // ES6
"use strict";

var fn = function fn(v) {
  return console.log(v);
};
```
该用法可以放心使用。  


### 1.2 类的声明和继承
```js
//类的定义
class Animal {
  //ES6中新型构造器
  constructor(name) {
    this.name = name;
  }
  //实例方法
  sayName() {
    console.log('My name is '+this.name);
  }
}
//类的继承
class Programmer extends Animal {
  constructor(name) {
    //直接调用父类构造器进行初始化
    super(name);
  }
  program() {
    console.log("I'm coding...");
  }
}
//测试我们的类
var animal=new Animal('dummy'),
wayou=new Programmer('wayou');
animal.sayName();//输出 ‘My name is dummy’
wayou.sayName();//输出 ‘My name is wayou’
wayou.program();//输出 ‘I'm coding...’
```
转换后
```js
//类的定义
'use strict';
var _get = function get(_x, _x2, _x3) { var _again = true; _function: while (_again) { var object = _x, property = _x2, receiver = _x3; desc = parent = getter = undefined; _again = false; if (object === null) object = Function.prototype; var desc = Object.getOwnPropertyDescriptor(object, property); if (desc === undefined) { var parent = Object.getPrototypeOf(object); if (parent === null) { return undefined; } else { _x = parent; _x2 = property; _x3 = receiver; _again = true; continue _function; } } else if ('value' in desc) { return desc.value; } else { var getter = desc.get; if (getter === undefined) { return undefined; } return getter.call(receiver); } } };
var _createClass = (function () { function defineProperties(target, props) { for (var i = 0; i < props.length; i++) { var descriptor = props[i]; descriptor.enumerable = descriptor.enumerable || false; descriptor.configurable = true; if ('value' in descriptor) descriptor.writable = true; Object.defineProperty(target, descriptor.key, descriptor); } } return function (Constructor, protoProps, staticProps) { if (protoProps) defineProperties(Constructor.prototype, protoProps); if (staticProps) defineProperties(Constructor, staticProps); return Constructor; }; })();
function _inherits(subClass, superClass) { if (typeof superClass !== 'function' && superClass !== null) { throw new TypeError('Super expression must either be null or a function, not ' + typeof superClass); } subClass.prototype = Object.create(superClass && superClass.prototype, { constructor: { value: subClass, enumerable: false, writable: true, configurable: true } }); if (superClass) Object.setPrototypeOf ? Object.setPrototypeOf(subClass, superClass) : subClass.__proto__ = superClass; }
function _classCallCheck(instance, Constructor) { if (!(instance instanceof Constructor)) { throw new TypeError('Cannot call a class as a function'); } }
var Animal = (function () {
  //ES6中新型构造器
  function Animal(name) {
    _classCallCheck(this, Animal);
    this.name = name;
  }
  //类的继承
  //实例方法
  _createClass(Animal, [{
    key: 'sayName',
    value: function sayName() {
      console.log('My name is ' + this.name);
    }
  }]);
  return Animal;
})();
var Programmer = (function (_Animal) {
  _inherits(Programmer, _Animal);
  function Programmer(name) {
    _classCallCheck(this, Programmer);
    //直接调用父类构造器进行初始化
    _get(Object.getPrototypeOf(Programmer.prototype), 'constructor', this).call(this, name);
  }
  //测试我们的类
  _createClass(Programmer, [{
    key: 'program',
    value: function program() {
      console.log("I'm coding...");
    }
  }]);
  return Programmer;
})(Animal);
var animal = new Animal('dummy'),
  wayou = new Programmer('wayou');
animal.sayName(); //输出 ‘My name is dummy’
wayou.sayName(); //输出 ‘My name is wayou’
wayou.program(); //输出 ‘I'm coding...’
```
转换过程使用了Object.defineProperty，在ie8下不兼容，除此外可以任意使用  

### 1.3 增强的对象字面量
```js
//通过对象字面量创建对象
var human = {
  breathe() {
    console.log('breathing...');
  }
};
var worker = {
  __proto__: human, //设置此对象的原型为human,相当于继承human
  company: 'freelancer',
  work() {
    console.log('working...');
  }
};
human.breathe();//输出 ‘breathing...’
//调用继承来的breathe方法
worker.breathe();//输出 ‘breathing...’
```
转换后
```js
//通过对象字面量创建对象
'use strict';
var human = {
  breathe: function breathe() {
    console.log('breathing...');
  }
};
var worker = {
  __proto__: human, //设置此对象的原型为human,相当于继承human
  company: 'freelancer',
  work: function work() {
    console.log('working...');
  }
};
human.breathe(); //输出 ‘breathing...’
//调用继承来的breathe方法
worker.breathe(); //输出 ‘breathing...’
```
这个可以任意使用  

### 1.4 字符串模板
```js
//产生一个随机数
var num=Math.random();
console.log(`your num is ${num}`);
```
转换后
```js
//产生一个随机数
"use strict";

var num = Math.random();
console.log("your num is " + num);
```  

### 1.5 解构
```js
var [name,gender,age]=['wayou','male','secrect'];//数组解构
console.log('name:'+name+', age:'+age);//输出： name:wayou, age:secrect
```
转化后
```js
'use strict';

var name = 'wayou';
var gender = 'male';
var age = 'secrect';
//数组解构
console.log('name:' + name + ', age:' + age); //输出： name:wayou, age:secrect
```
此方法可以使用。但是尽量不要使用 var [a, b] = getVal(); 的方式，尽管getVal返回一个数组。因为此时会用到isArray，IE8上不能支持。  

### 1.6 参数默认值，不定参数，拓展参数

* 参数默认值
```js
function sayHello(age, name='dude'){
    console.log(`Hello ${name}`);
}
sayHello(12);
```
转换后
```js
'use strict';

function sayHello(age) {
    var name = arguments.length <= 1 || arguments[1] === undefined ? 'dude' : arguments[1];

    console.log('Hello ' + name);
}
sayHello(12);
```
* 不定参数
```js
//将所有参数相加的函数
function add(...x){
  return x.reduce((m,n)=>m+n);
}
//传递任意个数的参数
console.log(add(1,2,3));//输出：6
console.log(add(1,2,3,4,5));//输出：15
```
转换后
```js
//将所有参数相加的函数
"use strict";
function add() {
  for (var _len = arguments.length, x = Array(_len), _key = 0; _key < _len; _key++) {
    x[_key] = arguments[_key];
  }
  return x.reduce(function (m, n) {
    return m + n;
  });
}
//传递任意个数的参数
console.log(add(1, 2, 3)); //输出：6
console.log(add(1, 2, 3, 4, 5)); //输出：15
```
* 扩展参数
```js
var people=['Wayou','John','Sherlock'];
//sayHello函数本来接收三个单独的参数人妖，人二和人三
function sayHello(people1,people2,people3){
  console.log(`Hello ${people1},${people2},${people3}`);
}
//但是我们将一个数组以拓展参数的形式传递，它能很好地映射到每个单独的参数
sayHello(...people);//输出：Hello Wayou,John,Sherlock
//而在以前，如果需要传递数组当参数，我们需要使用函数的apply方法
sayHello.apply(null,people);//输出：Hello Wayou,John,Sherlock
```
转换后
```js
'use strict';
var people = ['Wayou', 'John', 'Sherlock'];
//sayHello函数本来接收三个单独的参数人妖，人二和人三
function sayHello(people1, people2, people3) {
  console.log('Hello ' + people1 + ',' + people2 + ',' + people3);
}
//但是我们将一个数组以拓展参数的形式传递，它能很好地映射到每个单独的参数
sayHello.apply(undefined, people); //输出：Hello Wayou,John,Sherlock
//而在以前，如果需要传递数组当参数，我们需要使用函数的apply方法
sayHello.apply(null, people); //输出：Hello Wayou,John,Sherlock
```
参数默认值，不定参数，拓展参数都可以完全使用  

### 1.7 let与const

let和const完全支持，将都会被转为var，但是要理解let、var、const的区别。  

### 1.8 for of
```js
var someArray = [ "a", "b", "c" ];

for (v of someArray) {
    console.log(v);//输出 a,b,c
}
```
转换后
```js
"use strict";

var someArray = ["a", "b", "c"];

var _iteratorNormalCompletion = true;
var _didIteratorError = false;
var _iteratorError = undefined;

try {
  for (var _iterator = someArray[Symbol.iterator](), _step; !(_iteratorNormalCompletion = (_step = _iterator.next()).done); _iteratorNormalCompletion = true) {
    v = _step.value;

    console.log(v); //输出 a,b,c
  }
} catch (err) {
  _didIteratorError = true;
  _iteratorError = err;
} finally {
  try {
    if (!_iteratorNormalCompletion && _iterator["return"]) {
      _iterator["return"]();
    }
  } finally {
    if (_didIteratorError) {
      throw _iteratorError;
    }
  }
}
```
这里IE下面没有throw，所以无法支持  

### 1.9 iterator, generator
```js
var ids = {
  *[Symbol.iterator]: function () {
    var index = 0;

    return {
      next: function () {
        return { value: 'id-' + index++, done: false };
      }
    };
  }
};
```
转换后
```js
'use strict';

function _defineProperty(obj, key, value) { if (key in obj) { Object.defineProperty(obj, key, { value: value, enumerable: true, configurable: true, writable: true }); } else { obj[key] = value; } return obj; }

var ids = _defineProperty({}, Symbol.iterator, function () {
  var index = 0;

  return {
    next: function next() {
      return { value: 'id-' + index++, done: false };
    }
  };
});
```
不建议使用，转换后仍需要浏览器支持  

###1.10 模块 module、Proxies、Symbol
```js
// point.js
module "point" {
  export class Point {
    constructor (x, y) {
      public x = x;
      public y = y;
    }
  }
}
``` 
完全不支持，import也不支持，解析报错，所以建议不使用，使用原来的require  


### 1.11 Map，Set 和 WeakMap，WeakSet

Map，Set 和 WeakMap，WeakSet在es5中都没有对应的类型与之对应，所以均不支持转换，由浏览器决定兼容性  


### 1.12 Promises、Math，Number，String，Object 的新API

不做语法转换，由浏览器决定兼容性  

### 1.13 export & import
```js
export function myModule(someArg) {
  return someArg;
}
```
转换后
```js
"use strict";

Object.defineProperty(exports, "__esModule", {
  value: true
});
exports.myModule = myModule;

function myModule(someArg) {
  return someArg;
}
```  

```js
import * as baz from 'myModule';
```
转换后
```js
'use strict';

function _interopRequireWildcard(obj) { if (obj && obj.__esModule) { return obj; } else { var newObj = {}; if (obj != null) { for (var key in obj) { if (Object.prototype.hasOwnProperty.call(obj, key)) newObj[key] = obj[key]; } } newObj['default'] = obj; return newObj; } }

var _myModule = require('myModule');

var baz = _interopRequireWildcard(_myModule);
```
所以可以使用export和import等方法来进行模块的加载处理依赖，同时export使用到了defineProperty，IE8兼容性存在问题。  

### 1.14 生成器函数
```js
function* foo() { };
var bar = foo();
bar.next(); // Object {value: undefined, done: true}
```
转换后
```js
"use strict";

var marked0$0 = [foo].map(regeneratorRuntime.mark);
function foo() {
  return regeneratorRuntime.wrap(function foo$(context$1$0) {
    while (1) switch (context$1$0.prev = context$1$0.next) {
      case 0:
      case "end":
        return context$1$0.stop();
    }
  }, marked0$0[0], this);
};
var bar = foo();
bar.next(); // Object {value: undefined, done: true}
```
regeneratorRuntime在IE下面不能支持，所以不建议使用。

ES6新特性用到的就这些，其它的基本由浏览器本身决定。这部分代码Babel会像处理es5代码一样，不进行加工处理。对于部分ES6的语法，Babel会解析抛错，即使不抛错也不进行处理，建议不使用。 1.15 数组拷贝
```js
const items = [1,2,3];
const itemsCopy = [...items];
```
转换后
```js
"use strict";

var items = [1, 2, 3];
var itemsCopy = [].concat(items);
```
