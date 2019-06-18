---
title: '[ES6系列-06]展开操作符 Spread Operator 就像解压到这里'
date: 2019-06-18 10:13:41
tags:
categories:
---

【原创】码路工人 Coder-Power

#### 大家好，这里是码路工人有力量，我是码路工人，你们是力量。

[github-pages](https://codermonkey.github.io/CoderPower/)  
[博客园cnblogs](https://www.cnblogs.com/CoderMonkie/)

---

#### 在前面的文章中，介绍了`...`在获取剩余参数中的作用。它的主要任务还是作为展开运算符。

---

# 1.它能展开数组

数组是`JavaScript`中重要的类型，经常要用到数组操作，`ECMAScript6`中也添加了很多方便的方法，这里不讲数组对象新增的方法，只说说展开操作符常用的用途。好处自己体会。

## 1.1 浅拷贝一个数组
```javascript
/* eg.0
 * Array Copy Example
 */
 //----------------------------------------

const src = ["The Rolling Stones", "U2", "Oasis"]
const des = [...src]

console.log(des)

// (3) ["The Rolling Stones", "U2", "Oasis"]
//   0: "The Rolling Stones"
//   1: "U2"
//   2: "Oasis"
//   length: 3
//   __proto__: Array(0)

 //----------------------------------------
```

这直接省去了数组循环啊。

## 1.2 合并两个数组

### 合并的同时还可以另外添加其它元素

<!-- more -->

```javascript
/* eg.1
 * Array Merge Example
 */
 //----------------------------------------

const src1 = ["Still loving you", "You and I"]
const src2 = ["Love of my life", "Life is too short"]
const des = ["Always some where", ...src1, ...src2]

console.log(des)

// (5) ["Always some where", "Still loving you", "You and I", "Love of my life", "Life is too short"]
//      0: "Always some where"
//      1: "Still loving you"
//      2: "You and I"
//      3: "Love of my life"
//      4: "Life is too short"
//      length: 5
//      __proto__: Array(0)

//----------------------------------------
```

# 2.它能展开JSON对象

```javascript
/* eg.2
 * Spead JSON Object Example
 */
 //----------------------------------------

const person = {
    name: "Coder Monkey",
    age: 18
}

const student = {
    ...person,
    major: "Computer Science"
}

console.log(student)

// {name: "Coder Monkey", age: 18, major: "Computer Science"}
//   age: 18
//   major: "Computer Science"
//   name: "Coder Monkey"
//   __proto__: Object

//----------------------------------------
```

# 3.它甚至还能展开一个普通的字符串
## 只不过展开后就不再是一个字符串了

## 3.1 字符串展开为Json对象

```javascript
/* eg.3
 * 
 */
 //----------------------------------------

let wxName = "Coder-Power"

console.log({ ...wxName })

// {0: "C", 1: "o", 2: "d", 3: "e", 4: "r", 5: "-", 6: "P", 7: "o", 8: "w", 9: "e", 10: "r"}
//   0: "C"
//   1: "o"
//   2: "d"
//   3: "e"
//   4: "r"
//   5: "-"
//   6: "P"
//   7: "o"
//   8: "w"
//   9: "e"
//   10: "r"
//   __proto__: Object

//----------------------------------------
```


## 3.2 字符串展开为数组

```javascript
/* eg.4
 * 
 */
 //----------------------------------------


let wxName = "Coder-Power"

console.log([...wxName])

// (11) ["C", "o", "d", "e", "r", "-", "P", "o", "w", "e", "r"]
//   0: "C"
//   1: "o"
//   2: "d"
//   3: "e"
//   4: "r"
//   5: "-"
//   6: "P"
//   7: "o"
//   8: "w"
//   9: "e"
//   10: "r"
//   length: 11
//   __proto__: Array(0)

//----------------------------------------
```

# 4.脑洞时刻

## 4.1 数组能展开为对象吗？

```javascript
/* eg.5
 * 
 */
 //----------------------------------------

const bands = ["Beatles", "Scorpions"]

const obj = { ...bands }

// {0: "Beatles", 1: "Scorpions"}
//   0: "Beatles"
//   1: "Scorpions"
//   __proto__: Object

//----------------------------------------
```

是不是觉得数组与对象不能交叉展开，竟然...没错，它可以！
惊不惊喜，意不意外？

（数组下标`index`作为了对象的键`key`。）

## 4.2 那如果从对象展开为数组呢？

当然也是可以的了吗？事实就是这么残酷，代码无情地抛出了异常。

```javascript
/* eg.6
 * 
 */
 //----------------------------------------

const objBands = { '0': 'Beatles', '1': 'Scorpions' }
const arrBands = [...objBands]
console.log(arrbands)

// VM180:2 Uncaught TypeError:
//   object is not iterable (cannot read property Symbol(Symbol.iterator))

//----------------------------------------
```

最后，不能由对象或数组展开为字符串，不再例证了吧。

---

> 思考：都哪些是可以用`...`展开的呢？

上面的示例中，数组可以展开，对象可以展开，甚至连字符串都可以。
根本原因是，它们都是可迭代的，也就是实现/继承了`iterable`。

---

# 5.一句话总结

自认为可以总结一句话，就能让大家理解好展开操作符`...`，

**就是把它看作就地解压缩**。

以上。

---

希望对你能有帮助，下期再见。

欢迎关注分享，一起学习提高吧。  
QRCode/微信订阅号二维码  
![CoderPowerQRCode](http://images.cnblogs.com/cnblogs_com/CoderMonkie/1483738/o_CoderPower_QRCode.jpg)

---