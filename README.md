# 前端知识清单

题目来源 @ConardLi 大神在掘金发表的[一名【合格】前端工程师的自检清单](https://juejin.im/post/5cc1da82f265da036023b628)。看到评论说希望能有答案，而自己又正好需要系统的补全前端知识地图。

题目顺序有些微调，把相关题目放在一起。同时对部分题目有所更改 🤔

简单的答案会直接写到对应的题目下面，而篇幅过长的答案会写入 issues；如果网上已有的答案将会直接粘贴对应的连接。答案有误欢迎大家指出，与君共勉，一起成长。

## 系统学习指南

> 切记一定要系统学习，知识清单只是用来差缺补漏的。

**博客推荐：**
1. JavaScript 基础这块推荐去看下 @冴羽 大大的博客，可以帮你系统的学习。[链接地址](https://github.com/mqyqingfeng/Blog)。

**推荐书单：**
1. [JavaScript高级程序设计](https://book.douban.com/subject/10546125/)
2. [深入理解ES6](https://book.douban.com/subject/27072230/)

## 知识清单

---

### 一、JavaScript 基础

> 前端工程师吃饭的家伙，深度、广度一样都不能差。

#### 变量和类型

###### 1.`JavaScript`规定了几种语言类型？难度：⭐️

<details><summary><b>答案</b></summary>
	<p>
    
JavaScript语言类型分为两类：基础类型和引用类型；

基础类型： `Number`, `String`, `Boolean`, `Null`, `Undefined`, `Symbol` (ES6新增),`BigInt`

引用类型： `Object`；
    
  </p>
</details>

---

###### 2.`JavaScript`对象的底层数据结构是什么？难度：⭐️⭐️⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>
  这题难度有点大，看不明白可以先跳过。[从Chrome源码看JS Object的实现](https://zhuanlan.zhihu.com/p/26169639)，[V8中的快速属性访问](https://blog.csdn.net/szengtal/article/details/79054762)
</p>
</details>

---

###### 3.`Symbol`类型在实际开发中的应用、可手动实现一个简单的`Symbol`？难度：⭐️⭐️⭐️

<details>
	<summary><b>答案</b></summary>
<p>
	
> 在我看来，symbol更多是应用于es6规范中，由于它的值唯一的特性，可以解决变量名，属性名冲突的问题，并切Symbol提出了一些属性和方法，用于过渡以及实现一些特殊的用途，比如对象的迭代器，instanceof的拓展等等。

实际使用 `symnol` 主要是使用它的唯一性特性；用来创建 `class` 类的私有属性（ps: 半私有，可以使用 `getOwnPropertySymbols`）。

[手动实现 `Symbol`](https://github.com/mqyqingfeng/Blog/issues/87)。

</p>
</details>

---

###### 4.`JavaScript`中的变量在内存中的具体存储形式? 难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p>
根据变量值得类型区分存储形式：

1. 基础类型使用栈存储；基础类型赋值会从新创建一个基础值。
2. 引用类型使用堆存储；栈中只是存储该对象的在堆中的地址。引用类型赋值只是把堆地址赋给新的变量。

</p>
</details>

---

###### 5.理解值类型和引用类型 难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

[JS基本类型与引用类型知多少](https://juejin.im/post/595616ea5188250da205da91)
</p>
</details>

---

###### 6.`null`和`undefined`的区别？难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p class="color: #333;">
	
`undefined` 是 `Undefined` 类型的值，表示未定义。任何变量在赋值前都是 `Undefined` 类型，值为 `undefined` 。由于`undefined` 只是全局作用域下的一个属性（变量），并非关键字。`undefined` **属性的属性特性**

|    属性名    | 属性值 |
| :----------: | :----: |
|   writable   | false  |
|  enumerable  | false  |
| configurable | false  |

  全局作用下的 `undefined` 不能被重写，而在函数作用域内是可以随意改写 `undefined` 的。这也是建议使用 `void 0` 来表示 `undefined` 的来源

```javascript
window.undefined = 1; // false
function setUndefiend(){
    let undefined = 1;
    console.log(undefined); // 1
    console.log(undefined === void 0); // false
}
setUndefined();
```

  `Null` 类型也只有一个值，就是 `null`，它的语义表示空值，与 `undefined` 不同，`null` 是 `JavaScript` 关键字，所以在任何代码中，你都可以放心用 `null` 关键字来获取 `null` 值。
</p>
</details>

---

###### 7.至少可以说出三种判断`JavaScript`数据类型的方式，以及他们的优缺点，如何准确的判断数组类型？难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p>


|              方法              |                    优点                     |                             缺点                             |
| :----------------------------: | :-----------------------------------------: | :----------------------------------------------------------: |
|             typeof             |        简单，对基础类型检测新能好。         | 只能校验基础类型，而且typeof null === 'object' （JS 设计初的bug） |
| Object.prototype.toString.call |              所有类型都能检测               |             写起来比较繁琐，性能不如 typeof 好；             |
|           instanceof           |              能检测出引用类型               |                      不能检测出基础类型                      |
|          constructor           | 基本能检测所有的类型（除了null和undefined） |                  constructor易被修改,不可靠                  |

[性能对比](https://jsperf.com/js-type-check)

[详情使用方法连接](https://github.com/mqyqingfeng/Blog/issues/28)	
</p>
</details>

---

###### 8.基本类型对应的内置对象，以及他们之间的装箱拆箱操作 难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

### 装箱转换

每一种基本类型 Number、String、Boolean、Symbol 在对象中都有对应的类(null, undefined 除外)，所谓装箱转换，正是把基本类型转换为对应的对象，它是类型转换中一种相当重要的种类。

**注意：** 

1. 装箱机制会频繁产生临时对象，在一些对性能要求较高的场景下，我们应该尽量避免对基本类型做装箱转换。
2. Symbol 是不能直接使用 new 操作符调用的。不过我们可以装箱机制得到一个 Symbol 对象。
3. 每一类装箱对象皆有私有的 Class 属性，这些属性可以用 Object.prototype.toString 获取.

```JS
    var symbolObject = (function(){ return this; }).call(Symbol("a"));

    console.log(typeof symbolObject); //object
    console.log(symbolObject instanceof Symbol); //true
    console.log(symbolObject.constructor == Symbol); //true

    // ==== 也可以使用 Object 函数显示调用装箱能力；
    var symbolObject = Object(Symbol("a"));

    console.log(Object.prototype.toString.call(symbolObject)); //[object Symbol]
    
```
### 拆箱转换

在 JavaScript 标准中，规定了 ToPrimitive 函数，它是对象类型到基本类型的转换（即，拆箱转换）。

对象到 String 和 Number 的转换都遵循“先拆箱再转换”的规则。通过拆箱转换，把对象变成基本类型，再从基本类型转换为对应的 String 或者 Number。

拆箱转换会尝试调用 valueOf 和 toString 来获得拆箱后的基本类型。如果 valueOf 和 toString 都不存在，或者没有返回基本类型，则会产生类型错误 TypeError。

String 类型会优先调用 toString ;

在 ES6 之后，还允许对象通过显式指定 @@toPrimitive Symbol 来覆盖原有的行为。


```JS
    var o = {
        valueOf : () => {console.log("valueOf"); return {}},
        toString : () => {console.log("toString"); return {}}
    }

    o * 2
    // valueOf
    // toString
    // TypeError

    String(o)
    // toString 
    // valueOf 
    // TypeError

    o[Symbol.toPrimitive] = () => {console.log("toPrimitive"); return "hello"} console.log(o + "") // toPrimitive // hello

```
</p>
</details>

---

###### 9.可能发生隐式类型转换的场景以及转换原则，应如何避免或巧妙应用

<details><summary><b>答案</b></summary>
<p>

> 编码时应尽可能地将类型转换表达清楚，以免给别人留坑。类型转换越清晰，代码可读性越高，更容易理解。

`+` 运算符

`-` `*` `/` 强制将其他类型转化为数字类型

`==` 宽松 (loose equals ) 类型转换(ps: 不建议使用，规则真心有点复杂，感兴趣可以去看下 《你不知道的JavaScript 中卷》 1.4章)

**隐式强制类型转换为布尔值**

1. `if(...)`语句中的条件判断表达式
2. `for(...;...;...)`语句中的条件判断表达式(第二个)
3. `while(...)` 和 `do...while(...)` 循环中的条件判断表达式
4. `?:` 中的条件判断表达式
5. 逻辑运算符 `||` 和 `&&` 左边的操作数

| 类型    | Null      | Undefined   | Boolean(true) | Boolean(false) | Number                     | String             | Symbol     | Object     |
| ------- | --------- | ----------- | ------------- | -------------- | -------------------------- | ------------------ | ---------- | ---------- |
| Boolean | false     | false       | -             | -              | [0, NaN] - false<br />true | ''-false<br />true | true       | true       |
| Number  | 0         | NaN         | 1             | 0              | -                          | *StringToNumber*   |            | *拆箱操作* |
| String  | 'null'    | 'undefined' | 'true'        | 'false'        | *NumberToString*           | -                  | TypeError  | *拆箱操作* |
| Object  | TypeError | TypeError   | *装箱操作*    | *装箱操作*     | *装箱操作*                 | *装箱操作*         | *装箱操作* | -          |

</p>
</details>

---

###### 10.出现小数精度丢失的原因，`JavaScript`可以存储的最大数字、最大安全数字，`JavaScript`处理大数字的方法、避免精度丢失的方法 难度：⭐️⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

[JavaScript 浮点数陷阱及解法](https://github.com/camsong/blog/issues/9)
</p>
</details>

---

#### 原型和原型链


##### 1.instanceof的底层实现原理，手动实现一个instanceof 难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

> instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。

因为 instanceof 是个关键字，我们只能写一个函数 instanceofFn 来模拟 instanceof 功能。

```JS
/*
* obj 需要测试的实例
* Constructor 构造函数
*/
var instanceofFn = function (obj, Constructor){
    // 实例的 __proto__ 属性指向构造函数的 prototype 属性。
    return obj.__proto__.constructor === Constructor ? true: false; 
}
function Foo(){};
var foo = new Foo();
var boo = {};

console.log(instanceofFn(foo, Foo)) // true
console.log(instanceofFn(boo, Foo)) //false
```

</p>
</details>

---

##### 2.可以描述new一个对象的详细过程，手动实现一个new操作符 难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

new 作为关键字会进行如下的操作：

1. 创建一个空的简单JavaScript对象（即{}）；
2. 链接该对象（即设置该对象的构造函数）到另一个对象 ；
3. 将步骤1新创建的对象作为this的上下文 ；
4. 如果该函数没有返回对象，则返回this。

```JS

function objectFactory(Constructor){
    var obj = new Object();
    var args = Array.prototype.slice(1)
    obj.__proto__ = Constructor.prototype;
    var ret = Constructor.apply(obj,args);
    return typeof ret === 'object' ? ret: obj;
}

```

</p>
</details>

---

##### 3.创建对象的方法以及他们的优缺点  难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

详细的请看 《JavaScript 高级程序设计》

[JavaScript 深入之创建对象的多种方式以及优缺点](https://github.com/mqyqingfeng/Blog/issues/15)

</p>
</details>

---

##### 4.实现继承的几种方式以及他们的优缺点  难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

详细的请看 《JavaScript 高级程序设计》

[JavaScript深入之继承的多种方式和优缺点](https://github.com/mqyqingfeng/Blog/issues/16)
</p>
</details>

---

##### 5.理解es6 class构造以及继承的底层实现原理 难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

[ES6 系列之 Babel 是如何编译 Class 的(上)](https://github.com/mqyqingfeng/Blog/issues/105)

[ES6 系列之 Babel 是如何编译 Class 的(下)](https://github.com/mqyqingfeng/Blog/issues/106)

</p>
</details>

---

#### 作用域和闭包


##### 1.理解词法作用域和动态作用域  难度：⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

## 作用域

作用域是指程序源代码中定义变量的区域。

作用域规定了如何查找变量，也就是确定当前执行代码对变量的访问权限。

JavaScript 采用词法作用域(lexical scoping)，也就是静态作用域。

### 词法作用域

函数的作用域在函数定义的时候就决定了。JavaScript 采用的是词法作用域。

### 动态作用域

函数的作用域是在函数调用的时候才决定的。

## 示例

```JS
var name ="logic"

function getName(){
  return name;
}

function getNameWrap(){
  var name = 'wind'
  return getName()
}

console.log(getNameWrap()) // 输出 logic 。因为 JavaScript 是词法作用域，在函数定义时就确定了变量的访问。 

```

</p>
</details>

---

##### 2.理解变量对象(活动对象)  难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

变量对象是与执行上下文相关的数据作用域，存储了在上下文中定义的变量和函数。

全局对象：是宿主环境预定义的对象，作为 JavaScript 的全局函数和全局属性的占位符。通过使用全局对象，可以访问所有其他所有预定义的对象、函数和属性。全局上下文中的变量对象就是全局对象，即全局对象是作用域链的头。

执行上下文的代码会分成两个阶段进行处理： 分析(通过 arguments 属性初始化)和执行

### 分析

1. 函数的所有形参
   1. 由名称和对应值组成的一个变量对象的属性创建
   2. 没有实参，属性值设为 undefined
2. 函数声明
   1. 由名称和对应值组成一个变量对象的属性
   2. 如果变量名已经存在，直接替换该属性
3. 变量声明
   1. 由名称和对应值( undefined ) 组成一个变量对象的属性创建
   2. 如果变量名称已经声明的形参或函数相同，则变量声明无效

### 执行

  在代码执行阶段，会顺序执行代码，根据代码，修改变量对象的值。

### 示例

```JS
function foo(a,b){
  var a = 2;
  function c(){};
  var d = function (){}
}
foo(1)
// 分析阶段
AO = {
  arguments:{
    0: 1,
    1: undefined,
    length: 2
  },
  a: 1,
  b: undefined,
  c: reference to function c(){},
  d: undefined
}

// 代码执行
AO = {
  arguments:{
    0: 1,
    1: undefined,
    length: 2
  },
  a: 2,
  b: undefined,
  c: reference to function c(){},
  d: reference to FunctionExpression "d"
}

```

</p>
</details>

---

##### 3.理解JavaScript的作用域链   难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

**定义**： 当查找变量的时候，会先从当前上下文的变量查找，如果没有找到，就从父级（词法层面的父级）执行上下文的变量对象查找，一直找到全局上下文的变量对象，也就是全局对象。由多个执行上下文的变量对象构成的链，就是作用域链。

**用途**： 保证对执行环境有权访问的所有变量和函数的有序访问。

### 函数式如何保存自己的作用域链

函数有一个内部属性 [[scope]] ,当函数创建的时候，就会保存所有的父变量对象到其中。

[[scope]] 可以理解为所有父级变量对象的层级链

### 示例

```JS
function foo(){
  function bar(){
    ...
  }
}

// 函数创建时

foo.[[scope]] = [
  globalContext.VO
]

bar.[[scope]] = [
  fooContext.AO,
  globalContext.VO
]
```

</p>
</details>

---


##### 4.this的原理以及几种不同使用场景的取值  难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

### 显示绑定

call、apply、bind 可以显示的修改函数的 this 指向

### 隐士绑定

1. 全局上下文
   1. this 指向 window,严格模式下为 undefined
2. 直接调用函数
   1. this 指向 window,严格模式下为 undefined
3. 作为对象的方法调用
   1. obj.foo()。 this 指向对象 obj
4. DOM 事件的绑定
   1. onclick和addEventerListener中 this 默认指向绑定事件的元素。
5. new 构造函数绑定
   1. 构造函数中的 this 指向实例对象
6. 箭头函数
   1. 箭头函数没有 this, 因此也不能绑定。
   2. 在箭头函数里的 this 会指向 外层的非箭头函数的 this。

### this 的原理

[JavaScript深入之从ECMAScript规范解读this](https://github.com/mqyqingfeng/Blog/issues/7)

</p>
</details>

---

##### 5.理解JavaScript的执行上下文和执行上下文栈 难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

### 执行上下文

当 JavaScript 代码执行一段可执行代码(executable code)时，会创建对应的执行上下文(execution context)。

执行上下有三个重要属性(也就是前面 3 题所说的内容)

1. 变量对象
2. 作用域链
3. this

**执行代码**

1. 全局代码
2. 函数
3. eval 

### 执行上下文栈

每个函数都会创建执行上下文，执行上下文栈（Execution context stack，ECS）就是 JavaScript 引擎创建出来管理执行上下文的。

执行上下文栈是有全局上下文初始化，由于执行代码首先是全局代码。全局上下文永远在执行上下文栈中的最底下，只有等程序关闭才释放。

#### 示例

``` JS
function foo(){
  function bar(){}
  bar()
}
foo()

// 假设 ECS 是个数组
// 第一步 初始化， 全局代码的上下文 globalContext
ECS = [
  globalContext
]

// 第二步 执行 foo

ECS = [
  globalContext,
  fooContext
]
// 第三步 执行 bar

ECS = [
  globalContext,
  fooContext,
  barContext
]

//第四步 bar 执行完成, 释放 barContext
ECS = [
  globalContext,
  fooContext
]

// 第五步 foo 执行完成, 释放 fooContext
ECS = [
  globalContext
]

```

</p>
</details>

---

##### 6.闭包的实现原理和作用，可以列举几个开发中闭包的实际应用  难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

### 闭包的定义

> 函数与对其状态即词法环境（lexical environment）的引用共同构成闭包（closure）。也就是说，闭包可以让你从内部函数访问外部函数作用域。

1. 从理论角度：所有的函数。因为它们都在创建的时候就将上层上下文的数据保存起来了。哪怕是简单的全局变量也是如此，因为函数中访问全局变量就相当于是在访问自由变量，这个时候使用最外层的作用域。
2. 从实践角度：以下函数才算是闭包：
即使创建它的上下文已经销毁，它仍然存在（比如，内部函数从父函数中返回）
在代码中引用了自由变量

### 闭包的作用

闭包通常用来创建内部变量，使得这些变量不能被外部随意修改，同时又可以通过指定的函数接口来操作。

### 实际应用场景

1. 保护函数内的变量安全：如迭代器、生成器。

2. 在内存中维持变量：如果缓存数据、柯里化。

</p>
</details>

---

##### 7.理解栈溢出和内存泄漏的原理，如何防止 难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

### 栈溢出

代码执行前都会进行编译和创建执行上下文。而管理执行上下文的叫做执行上下文栈。栈有个特点就是**后进先出**。同时执行上下文栈是有大小限制的。当执行上下文栈大小超过限制就会产生栈溢出错误。

[JavaScript深入之执行上下文栈](https://github.com/mqyqingfeng/Blog/issues/4)

#### 如何防止

递归函数很容易出现这种情况，把递归调用的形式改造成其他形式，或者使用加入定时器的方法来把当前任务拆分为其他很多小任务。

**错误示例**

```JS
function add(a,b){
  add(a,b)
}
add(1,2)
```

### 内存泄漏

> JavaScript是在创建变量（对象，字符串等）时自动进行了分配内存，并且在不使用它们时“自动”释放。 释放的过程称为垃圾回收。不在使用，没有释放的内存，称为内存泄漏

#### 3种常见内存泄漏

1. 意外的全局变量
2. 脱离 DOM 的引用
3. 闭包

示例代码

``` JS
// 意外全局变量
function foo(arg) {
    bar = "this is a hidden global variable";
}

// 脱离 DOM 的引用

const button = document.getElementById('button');
document.body.removeChild(button);
// 此时，仍旧存在一个全局的 #button 的引用,button 元素仍旧在内存中，不能被 GC 回收。

// 闭包
(function (){
    let num = 1;
    return function add(a,b){
        return a+b;
    }
})()

```

</p>
</details>

---

##### 8.理解模块化解决的实际问题，可列举几个模块化方案并理解其中原理 难度：⭐️⭐️⭐️⭐️

<details><summary><b>答案</b></summary>
<p>

[ES6 系列之模块加载方案](https://github.com/mqyqingfeng/Blog/issues/108)

</p>
</details>

### 执行机制


##### 1.为何try里面放return，finally还会执行，理解其内部机制


##### 2.JavaScript如何实现异步编程，可以详细描述EventLoop机制


##### 3.宏任务和微任务分别有哪些


##### 4.可以快速分析一个复杂的异步嵌套逻辑，并掌握分析方法


##### 5.使用Promise实现串行


##### 6.Node与浏览器EventLoop的差异


##### 7.如何在保证页面运行流畅的情况下处理海量数据


### 语法和API


##### 1.理解 ECMAScript 和 JavaScript 的关系


##### 2.熟练运用 es5、es6 提供的语法规范，


##### 3.熟练掌握 JavaScript 提供的全局对象（例如Date、Math）、全局函数（例如decodeURI、isNaN）、全局属性（例如Infinity、undefined）


##### 4.熟练应用 map、reduce、filter 等高阶函数解决问题


##### 5.setInterval 需要注意的点，使用 setTimeout 实现 setInterval


##### 6.JavaScript提供的正则表达式API、可以使用正则表达式（邮箱校验、URL解析、去重等）解决常见问题


##### 7.JavaScript异常处理的方式，统一的异常处理方案

---

## 二、HTML和CSS

### HTML

1.从规范的角度理解HTML，从分类和语义的角度使用标签


2.常用页面标签的默认样式、自带属性、不同浏览器的差异、处理浏览器兼容问题的方式


3.元信息类标签(head、title、meta)的使用目的和配置方法


4.HTML5离线缓存原理


### CSS


##### 1.CSS盒模型，在不同浏览器的差异  难度：⭐️

<details><summary><b>答案</b></summary>
<p>

- 定义了盒的四个部分 —— margin, border, padding, and content
- 标准盒模型 
  - 如果你给盒设置 `width` 和 `height`，实际设置的是 *content box*。 padding 和 border 再加上设置的宽高一起决定整个盒子的大小。
- IE盒模型（box-sizing: border-box）
  - 如果你给盒设置 `width` 和 `height`，包含了content box + padding + border

</p>
</details>

2.BFC实现原理，可以解决的问题，如何创建BFC 难度：⭐️⭐️

<details><summary><b>答案</b></summary> 
<p>

- 参考文章 [10 分钟理解 BFC 原理](https://zhuanlan.zhihu.com/p/25321647), [CSS深入理解流体特性和BFC特性下多栏自适应布局](https://www.zhangxinxu.com/wordpress/2015/02/css-deep-understand-flow-bfc-column-two-auto-layout/)

- 特性：具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。
- 如何产生 BFC
  - 浮动元素（非 float: none）
  - 绝对定位元素（position: absolute || fixed）
  - 行内元素（display: inline-block）
  - 表格元素 （display: table-cell || table-caption）
  - overflow 值不为 visible 元素
  - 弹性元素： display: flex
  - 网格元素： display: grid
- BFC 实际用途
  - 清除浮动
  - 解除外边距折叠
  - 自适应布局: 左浮动 + bfc overflow: hidden;

</p>
</details>

---

3.水平垂直居中的方案、可以实现6种以上并对比它们的优缺点 难度：⭐️⭐️
<details><summary><b>答案</b></summary> 
<p>

- 参考文章：[水平垂直居中](https://github.com/yanhaijing/vertical-center)，[16种方法实现水平居中垂直居中](https://juejin.im/post/58f818bbb123db006233ab2a)
- 居中元素定宽高
  - absolute + 负 margin + top:50%; left:50%;
  - absolute + margin:auto + top:0;left: 0;bottom:0; right:0;
  - absolute + cacl(50%- el.width)
- 居中元素不定宽高
  - absolute + transform: translate(-50%, -50%)
  - 父元素设置： wirting-mode: vertical-lr;text-align: center: 子元素包一层设置 wirting-mode: horizontal-tb;text-aligin: center;
  - 父元素设置： line-height: 300px;子元素设置： display: inline-block;
  - 父元素设置： display: table-cell; vertical-align: middle; 
  - 父元素设置： display: flex; justify-content:center;align-items:center;
  - 父元素设置:   display: grid; 子元素设置： align-self: center; justify-self: center;

</p>
</details>

---


4.PostCSS、Sass、Less的异同，以及使用配置，至少掌握一种


5.CSS模块化方案、如何配置按需加载、如何防止CSS阻塞渲染


6.掌握一套完整的响应式布局方案


## 三、计算机基础

> 关于编译原理，不需要理解非常深入，但是最基本的原理和概念一定要懂，这对于学习一门编程语言非常重要

### 编译原理


1.理解代码到底是什么，计算机如何将代码转换为可以运行的目标程序


2.正则表达式的匹配原理和性能优化


3.如何将JavaScript代码解析成抽象语法树(AST)


4.base64的编码原理


5.几种进制的相互转换计算方法，在JavaScript中如何表示和转换


### 网络协议

1.理解什么是协议，了解TCP/IP网络协议族的构成，每层协议在应用程序中发挥的作用


2.三次握手和四次挥手详细原理，为什么要使用这种机制 难度：⭐️⭐️⭐️

<details><summary><b>答案</b></summary> 
<p>

### 为什么会使用机制？

用于保证传输的可靠性

### 三次握手

所谓三次握手(Three-way Handshake)，是指建立一个 TCP 连接时，需要客户端和服务器总共发送3个包。

三次握手的目的是连接服务器指定端口，建立 TCP 连接，并同步连接双方的序列号和确认号，交换 TCP 窗口大小信息。在 socket 编程中，客户端执行 connect() 时。将触发三次握手。

- 第一次握手(SYN=1, seq=x):

  客户端发送一个 TCP 的 SYN 标志位置1的包，指明客户端打算连接的服务器的端口，以及初始序号 X,保存在包头的序列号(Sequence Number)字段里。发送完毕后，客户端进入 SYN_SEND 状态。

- 第二次握手(SYN=1, ACK=1, seq=y, ACKnum=x+1):

  服务器发回确认包(ACK)应答。即 SYN 标志位和 ACK 标志位均为1。服务器端选择自己 ISN 序列号，放到 Seq 域里，同时将确认序号(Acknowledgement Number)设置为客户的 ISN 加1，即X+1。 发送完毕后，服务器端进入 SYN_RCVD 状态。

- 第三次握手(ACK=1，ACKnum=y+1)
  
  客户端再次发送确认包(ACK)，SYN 标志位为0，ACK 标志位为1，并且把服务器发来 ACK 的序号字段+1，放在确定字段中发送给对方，并且在数据段放写ISN的+1。发送完毕后，客户端进入 ESTABLISHED 状态，当服务器端接收到这个包时，也进入 ESTABLISHED 状态，TCP 握手结束。

### 四次挥手

TCP 的连接的拆除需要发送四个包，因此称为四次挥手(Four-way handshake)。

- 第一次挥手(FIN=1，seq=x)

  假设客户端想要关闭连接，客户端发送一个 FIN 标志位置为1的包，表示自己已经没有数据可以发送了，但是仍然可以接受数据。

  发送完毕后，客户端进入 FIN_WAIT_1 状态。

- 第二次挥手(ACK=1，ACKnum=x+1)

  服务器端确认客户端的 FIN 包，发送一个确认包，表明自己接受到了客户端关闭连接的请求，但还没有准备好关闭连接。

  发送完毕后，服务器端进入 CLOSE_WAIT 状态，客户端接收到这个确认包之后，进入 FIN_WAIT_2 状态，等待服务器端关闭连接。

- 第三次挥手(FIN=1，seq=y)

  服务器端准备好关闭连接时，向客户端发送结束连接请求，FIN 置为1。

  发送完毕后，服务器端进入 LAST_ACK 状态，等待来自客户端的最后一个ACK。

- 第四次挥手(ACK=1，ACKnum=y+1)

  客户端接收到来自服务器端的关闭请求，发送一个确认包，并进入 TIME_WAIT状态，等待可能出现的要求重传的 ACK 包。

  服务器端接收到这个确认包之后，关闭连接，进入 CLOSED 状态。

</p>
</details>


3.有哪些协议是可靠，TCP有哪些手段保证可靠交付


4.DNS的作用、DNS解析的详细过程，DNS优化原理


5.CDN的作用和原理


6.HTTP请求报文和响应报文的具体组成，能理解常见请求头的含义，有几种请求方式，区别是什么


7.HTTP所有状态码的具体含义，看到异常状态码能快速定位问题


8.HTTP1.1、HTTP2.0带来的改变


9.HTTPS的加密原理，如何开启HTTPS，如何劫持HTTPS请求


10.理解WebSocket协议的底层原理、与HTTP的区别


### 设计模式


1.熟练使用前端常用的设计模式编写代码，如单例模式、装饰器模式、代理模式等


2.发布订阅模式和观察者模式的异同以及实际应用


3.可以说出几种设计模式在开发中的实际应用，理解框架源码中对设计模式的应用
