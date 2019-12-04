题目来源 @ConardLi 大神在掘金发表的[一名【合格】前端工程师的自检清单](https://juejin.im/post/5cc1da82f265da036023b628)。看到评论说希望能有答案，而自己又正好需要系统的补全前端知识地图。

简单的答案会直接写到对应的题目下面，而篇幅过长的答案会写入 issues；如果网上已有的答案将会直接粘贴对应的连接。答案有误欢迎大家指出，与君共勉，一起成长。



---

## 一、JavaScript 基础

> 前端工程师吃饭的家伙，深度、广度一样都不能差。

### 变量和类型

###### 1.`JavaScript`规定了几种语言类型？难度：⭐️

<details><summary><b>答案</b></summary>
	<p>
    
JavaScript语言类型分为两类：基础类型和引用类型；

基础类型： `Number`, `String`, `Boolean`, `Null`, `Undefined`, `Symbol` (ES6新增)；

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

<details><summary><b>答案</b></summary>
<p>
	
> 在我看来，symbol更多是应用于es6规范中，由于它的值唯一的特性，可以解决变量名，属性名冲突的问题，并切Symbol提出了一些属性和方法，用于过渡以及实现一些特殊的用途，比如对象的迭代器，instanceof的拓展等等。

实际使用 `symnol` 主要是使用它的唯一性特性；用来创建 `class` 类的私有属性（ps: 半私有，可以使用 `getOwnPropertySymbols`）。

[手动实现 `Symbol`](https://github.com/mqyqingfeng/Blog/issues/87)。
</p>
</details>

---

###### 4.`JavaScript`中的变量在内存中的具体存储形式

---

###### 5.基本类型对应的内置对象，以及他们之间的装箱拆箱操作

---

###### 6.理解值类型和引用类型

---

###### 7.`null`和`undefined`的区别？难度：⭐️⭐️

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

###### 8.至少可以说出三种判断`JavaScript`数据类型的方式，以及他们的优缺点，如何准确的判断数组类型？难度：⭐️⭐️

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


