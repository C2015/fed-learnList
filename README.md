题目来源 @ConardLi 大神在掘金发表的[一名【合格】前端工程师的自检清单](https://juejin.im/post/5cc1da82f265da036023b628)。看到评论说希望能有答案，而自己又正好需要系统的补全前端知识地图。

简单的答案会直接写到对应的题目下面，而篇幅过长的答案会写入 issues；如果网上已有的答案将会直接粘贴对应的连接。答案有误欢迎大家指出，与君共勉，一起成长。



---

## 一、JavaScript 基础

> 前端工程师吃饭的家伙，深度、广度一样都不能差。

### 变量和类型

1.`JavaScript`规定了几种语言类型？

<details><summary><b>答案</b></summary>
	<p>
    JavaScript语言类型分为两类：基础类型和引用类型；

    基础类型： `Number`, `String`, `Boolean`, `Null`,` Undefined`,` Symbol` (ES6新增)；

    引用类型： `Object`；
  </p>
</details>

2.`JavaScript`对象的底层数据结构是什么？

<details><summary><b>Answer</b></summary>
<p>
  
</p>
</details>

3.`Symbol`类型在实际开发中的应用、可手动实现一个简单的`Symbol`

4.`JavaScript`中的变量在内存中的具体存储形式

5.基本类型对应的内置对象，以及他们之间的装箱拆箱操作

6.理解值类型和引用类型

7.`null`和`undefined`的区别

<details><summary><b>Answer</b></summary>
<p class="color: #333;">
	
`undefined` 是 `Undefined` 类型的值，表示未定义。任何变量在赋值前都是 `Undefined` 类型，值为 `undefined` 。由于`undefined` 只是全局作用域下的一个属性（变量），并非关键字。`undefined` **属性的属性特性**

|    属性名    | 属性值 |
| :----------: | :----: |
|   writable   | false  |
|  enumerable  | false  |
| configurable | false  |

  全局作用下的undefined 不能 被重新，而在函数作用域内是可以随意改下undefined 的。这也是建议使用 void 0 来表示 undefined 的来源。

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


8.至少可以说出三种判断`JavaScript`数据类型的方式，以及他们的优缺点，如何准确的判断数组类型

9.可能发生隐式类型转换的场景以及转换原则，应如何避免或巧妙应用

10.出现小数精度丢失的原因，`JavaScript`可以存储的最大数字、最大安全数字，`JavaScript`处理大数字的方法、避免精度丢失的方法


