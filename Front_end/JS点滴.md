# JS杂货铺
记录下js学习中的一些小细节小技巧或者常用总结
## 对象
#### 1.方括号的使用

对象里的属性可以是**多词字符串**，直接用点操作就不管用了，因此可以用方括号。

```js
let user = {};
user["likes birds"] = true;//设置也可以用方括号，或者字面量里设置多词字符串
alert(user["likes birds"]);//返回true
```
**计算属性**，在对象字面量中使用方括号，设置变量

```js
let fruit = prompt("Which fruit to buy?", "apple");
let bag = {};
bag[fruit] = 5;// 从 fruit 变量中获取值
```

#### 2.属性的一些操作

##### 属性值简写


```js
let user = {
  name,  // 与 name:name 相同
  age: 30
};
```
属性的名称可以是任何字符串和symbol类型

##### “in”操作符判断属性是否存在

```js
"key" in object
```
##### 删除属性

```js
delete obj.prop
```

##### for...in 循环
遍历一个对象的所有键（key）

```js
for (key in object) {
  // 对此对象属性中的每个键执行的代码
}
```
for...in 循环的顺序，若有整数属性（**不做任何更改**的情况下与一个整数进行相互转换的**字符串**），则以升序排列。如果属性名不是整数，那将按照创建的顺序来排序

#### 3.关于对象的克隆
**浅克隆**：对象里的原始类型属性会直接复制，但里面的对象类型属性只会复制引用。
浅克隆方法：
可以用for...in循环遍历，也可以用下面两种方法

```js
let user = {
name: "John",
age: 30
};
let clone = { ...obj };//用展开运算符
```

```js
let user = {
  name: "John",
  age: 30
};
let clone = Object.assign({}, user);//用Object.assign()
```
Object.assign方法的用法

```js
//Object.assign(dest, [src1, src2, src3...])
//第一个参数 dest 是指目标对象。
//更后面的参数 src1, ..., srcN（可按需传递多个参数）是源对象。
//该方法将所有源对象的属性拷贝到目标对象 dest 中。换句话说，从第二个开始的所有参数的属性都被拷贝到第一个参数的对象中。
//调用结果返回 dest。
//如果被拷贝的属性的属性名已经存在，那么它会被覆盖
let user = { name: "John" };
let permissions1 = { canView: true };
let permissions2 = { canEdit: true };
// 将 permissions1 和 permissions2 中的所有属性都拷贝到 user 中
Object.assign(user, permissions1, permissions2);
// 现在 user = { name: "John", canView: true, canEdit: true }
```
**深克隆**：
用现有的轮子：[_.cloneDeep(obj)](https://lodash.com/docs/4.17.15#cloneDeep)

##### const声明的对象也可以修改

```js
const user = {
  name: "John"
};
user.name = "Pete"; // (*)
alert(user.name); // Pete
//只有把user=...当做一个整体赋值才会报错
```
#### 3.关于this
##### this指向谁？
 this一般在**方法**中，js中的this指向谁取决于执行时==最后一次调用它的那个对象==。就是在点之前的这个对象，即调用该方法的对象。
 
 tip：用this写可靠的代码
 
```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(user.name); // "user" 替代 "this",当user赋值后，本段代码将不可靠
  }

};
```
##### js中的this不受限制

任何方法中都可以有this

在没有对象的情况下调用：
- 严格模式下：this == undefined
- 非严格模式下：this 将会是 全局对象（浏览器中的 window）。这是一个历史行为，"use strict" 已经将其修复了。

##### 箭头函数没有自己的this
箭头函数的this是从外部调用他的方法获取的

##### 一个this的小技巧
对象方法的链式调用
```js
let ladder = {
  step: 0,
  up() {
    this.step++;
    return this;
  },
  down() {
    this.step--;
    return this;
  },
  showStep() {
    alert( this.step );
    return this;
  }
};

ladder.up().up().down().showStep().down().showStep(); // 展示 1，然后 0
```


#### 4.关于构造函数

##### 构造函数干了啥？

```js
function User(name) {
  // this = {};（隐式创建）

  // 添加属性到 this
  this.name = name;
  this.isAdmin = false;

  // return this;（隐式返回）
}
```
**构造器的return**
- 如果 return 返回的是一个对象，则返回这个对象，而不是 this。
- 如果 return 返回的是一个原始类型，则忽略。

#### 5.可选链“？.”
调用一个对象的属性:alert(user.address.street); 若其中address属性并不存在，便会返回一个错误。

使用可选链：==value?.prop==
- 如果 value 存在，则结果与 value.prop 相同，
- 否则（当 value 为 undefined/null 时）则返回 undefined。

变体：
- obj.method?.() —— 如果 obj.method 存在则调用 obj.method()，否则返回 undefined。
- obj?.[prop] —— 如果 obj 存在则返回 obj[prop]，否则返回 undefined。

#### 6.关于symbol类型
两个symbol类型变量就算是描述相同也不一样（类似id）
##### 用symbol创建隐藏属性

```js
let user = { // 属于另一个代码
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // 我们可以使用 symbol 作为键来访问数据

//..这一个代码可以再次创建而互不影响
let id = Symbol("id");

user[id] = "Their id value";
```

symbol属性不参与for...in 循环

##### 全局symbol
- Symbol.for(key)可以查询全局symbol注册表。
 
 该调用会检查全局注册表，如果有一个描述为 key 的 symbol，则返回该 symbol，否则将创建一个新 symbol（Symbol(key)），并通过给定的 key 将其存储在注册表中。

```js
// 通过 name 获取 symbol
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// 通过 symbol 获取 name
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
```

 
- Symbol.keyFor(sym)，它的作用完全反过来：通过全局 symbol 返回一个名字。
 
从技术上说，symbol 不是 100% 隐藏的。有一个内建方法 Object.getOwnPropertySymbols(obj) 允许我们获取所有的 symbol。还有一个名为 Reflect.ownKeys(obj) 的方法可以返回一个对象的 所有 键，包括 symbol。所以它们并不是真正的隐藏。但是大多数库、内建方法和语法结构都没有使用这些方法。
##### symbol注意
- 不能被自动转为字符串
- Object.keys也会被忽略
- Object.assign克隆时，会被克隆









---



