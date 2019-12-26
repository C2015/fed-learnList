题目来源 @ConardLi 大神在掘金发表的[一名【合格】前端工程师的自检清单](https://juejin.im/post/5cc1da82f265da036023b628)。看到评论说希望能有答案，而自己又正好需要系统的补全前端知识地图。

题目顺序有些微调，把相关题目放在一起。

简单的答案会直接写到对应的题目下面，而篇幅过长的答案会写入 issues；如果网上已有的答案将会直接粘贴对应的连接。答案有误欢迎大家指出，与君共勉，一起成长。



---

## 一、JavaScript 基础

> 前端工程师吃饭的家伙，深度、广度一样都不能差。

### 变量和类型

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
  这题难度有点大，看不明白可以先跳过。[从Chrome源码看JS Object的实现](https://zhuanlan.zhihu.com/p/26169639)
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

###### 10.出现小数精度丢失的原因，`JavaScript`可以存储的最大数字、最大安全数字，`JavaScript`处理大数字的方法、避免精度丢失的方法

<details><summary><b>答案</b></summary>
<p>

[JavaScript 浮点数陷阱及解法](https://github.com/camsong/blog/issues/9)
</p>
</details>

### 原型和原型链


##### 1.理解原型设计模式以及JavaScript中的原型规则


##### 2.instanceof的底层实现原理，手动实现一个instanceof


##### 4.实现继承的几种方式以及他们的优缺点


##### 5.至少说出一种开源项目(如Node)中应用原型继承的案例


##### 6.可以描述new一个对象的详细过程，手动实现一个new操作符


##### 7.理解es6 class构造以及继承的底层实现原理


### 作用域和闭包


##### 1.理解词法作用域和动态作用域


##### 2.理解JavaScript的作用域和作用域链


##### 3.理解JavaScript的执行上下文栈，可以应用堆栈信息快速定位问题


##### 4.this的原理以及几种不同使用场景的取值


##### 5.闭包的实现原理和作用，可以列举几个开发中闭包的实际应用


##### 6.理解堆栈溢出和内存泄漏的原理，如何防止


##### 7.如何处理循环的异步操作


##### 8.理解模块化解决的实际问题，可列举几个模块化方案并理解其中原理


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

