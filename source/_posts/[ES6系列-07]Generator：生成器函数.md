---
title: '[ES6系列-07]Generator Function: 生成器函数'
date: 2019-06-30 19:30:47
tags: [ES6,js,javascript]
categories: [JavaScript]
---

【原创】码路工人 Coder-Power

#### 大家好，这里是码路工人有力量，我是码路工人，你们是力量。

[github-pages](https://codermonkie.github.io/CoderPower/)  
[博客园cnblogs](https://www.cnblogs.com/CoderMonkie/)

---


#### `Generator function 生成器函数`是`ES6`中新增的语法糖，本质上讲，就是以封装成一个遍历器的形式，让编码的你获得程序的执行控制权，通俗地说就是，流程控制上，踹一脚，走一步，不要太暴力~

# 0.前言

要说到生成器函数，就不得不提到`javascript`的异步编程方式演进史。

(不能跑题不能跑题不能跑题)

- 1.普通的回调函数方式（callback）
- 2.事件/发布--订阅者模式（event/publisher--observer）
- 3.Promise
- 4.Generator
- 5.async/await（在ES7/ES2016中正式提出）

<!-- more -->

其中`Promise`是一个里程碑，解决了回调函数嵌套时的`callback hell`回调地狱问题（层级嵌套太多难以阅读与维护）。

而本文主角`Generator`更像是作为一个过渡语法，在推出`async/await`后就基本很少用了。

`async/await`，CSharper转前端，一看就像见到亲人，`C#`中有同样的语法。（#注：C# 5.0 中加入的）

话说语法演化地真是方便啊。在后面的文章中将单独给`Promise`和`async/await`开贴。

# 1.一句话介绍你自己

## 1.1 Talk is cheep, show you the CODE!

```js
/* eg.0
 * Simple Example of Generator-Function
 */
//----------------------------------------

let songs = ["Hero", "Here I am", "The Show"]

// Generator-Function is Here Below：
function *play(songs) {
    for(let i=0; i<songs.length; i++) {
        yield songs[i]
    }
    // 这里可以有return
}

let g = play(songs)

let next = g.next()
console.log(next)   // { value: 'Hero', done: false }

next = g.next()
console.log(next)   // { value: 'Here I am', done: false }

next = g.next()
console.log(next)   // { value: 'The Show', done: false }

next = g.next()
console.log(next)   // { value: undefined, done: true }

//----------------------------------------
```

## 1.2 关于生成器函数的定义

- 第一，函数定义处有个`*`符号。

  `*`既可以紧跟在`function`后面，也可以贴在函数名前。

- 第二，函数内有`yield`关键字

  用以中断处理流程，并可以临时对外提供一个返回值。

- 其它，写法上与普通函数无异

## 1.3 关于生成器函数的使用

- 1.像普通函数一样调用，得到的不是任何具体的返回值，而是一个迭代器。（也可以看作是一个状态机）

- 2.来一脚试试。通过调用得到的迭代器对象上的`next()`方法，开始得到第一个返回值对象。

- 3.一直踹。每一次调用`next()`方法，得到一个结果对象，可以看到上面代码注释中的打印信息。

  其中`value`即当前获得的值，`done`即迭代状态，它只有`ture/false`两种可能，当它变为`true`，即迭代完成。

# 2.主流使用方式

正常的使用方式也即良好的实践吧，应该是配合`promise`来使用的。

来一个简陋的示例：
```js
/* eg.1
 * Simple Example of Generator-Function
 */
//----------------------------------------

function* func() {
    // 这里应该是ajax请求，结果是一个promise对象，简单模拟一下
    yield new Promise(function(resolve,reject){
        resolve('Hello')
    })
    
    // 这里应该是ajax请求，结果是一个promise对象，简单模拟一下
    yield new Promise(function(resolve,reject){
        resolve('World')
    })
}

let g = func()

g.next().value.then((data) => {
    console.log('log-1:', data)
    return g.next().value
}).then((data) => {
    console.log('log-2:', data)
})

// log-1: Hello
// log-2: World

//----------------------------------------
```

#### 这样，就将异步的`ajax`处理简单地以同步的样子书写出来了。

# 3.粗陋的实践

#### 除了可以处理异步，码路工人个人觉得，`Generator`比较适合用在循环处理的场景。其中就实践过类似下面这个处理的例子：

```js
/* eg.2 （part1）
 * My Example of Generator-Function
 */
//----------------------------------------
// 以下代码中都省略掉了检测处理

// 首先来一个Gernerator函数
function *getDateInPeriod(from, to, includEnd=false) {

    let fromDate = new Date(from)
    let toDate = new Date(to)

    if(includEnd) {
        toDate = addDays(toDate, 1)
    } 

    for(let date = fromDate;date < toDate; date=addDays(date, 1)) {
        yield date
    }
}

// 上面调用到了工具函数addDays
function addDays(date, days){
    date = new Date(date.setDate(date.getDate() + days))
    return date
}

//----------------------------------------
```

#### 然后就是使用了，在循环取值的过程中，会有一些业务处理（同步的或异步的）。

```js
/* eg.2 （part2）
 * My Example of Generator-Function
 */
//----------------------------------------

let arrDate = getDateInPeriod('2019-06-06', '2019-06-30', true)

let daysInPeriod = arrDate.next()

while(!daysInPeriod.done) {

    // 这里是一堆其它业务处理

    console.log(daysInperiod)

    daysInPeriod = arrDate.next()

}
console.log(daysInperiod)

//----------------------------------------
```

打印信息结果：

```js
{ value: 2019-06-06T00:00:00.000Z, done: false }
{ value: 2019-06-07T00:00:00.000Z, done: false }
...
{ value: 2019-06-29T00:00:00.000Z, done: false }
{ value: 2019-06-30T00:00:00.000Z, done: false }
{ value: undefined, done: true }
```

上面的例子中，还是同步的方式。也许不是好的用法，但它能告诉你这是一种用法。

# 4.听说过的实践

这个码工没有实践过，大意是，`Generator`函数这个语法糖是按照`yield`将代码分成多个部分，人手工控制执行每一部分，于是，封装一个执行器函数，简化流程控制，使异步编程轻松愉快。

其实，在有了`async/await`后真的没有这个必要了。

（`co.js`就是一个这种`Generator`的执行库）

# 4.其它

除了上面介绍的生成器函数的主要用法，其实还有点其它小特性，码路工人并没有实践过，感觉也不怎么会用到，这里稍作了解即可。

## 4.1 可以接收由`next`传递进的参数。

```js
/* eg.3
 * parameters
 */
//----------------------------------------

function *genFunc(p) {
    console.log(`p is ${p}`)

    let p1 = yield p
    console.log(`p1 is ${p1}`)

    let p2 = yield p1
    console.log(`p2 is ${p2}`)
}


let gen = genFunc(1)
// 第一次next无法传参到Generator函数，应该由最初的函数调用处传递
gen.next(2)

// 从第二步next() 传的参数，在第一个yield处接收
gen.next(3)

```

关于给`yield`传参确实看起来稍微有一点诡异，其实理解了也就不觉得奇怪了。

说明已贴在上面的注释中。

## 4.2 可以有默认的迭代器了

```js
/* eg.4
 * get value by for-of loop
 */
//----------------------------------------

function *foo() {
    for(let i=0; i<6; i++) {
        yield i
    }
}

let gen = foo()

for(let item of gen) {
    console.log(item)
}

// 打印结果：
// 0
// 1
// 2
// 3
// 4
// 5
//----------------------------------------
```

---

## 总结

关于生成器函数`Generator Function`就介绍到这里吧，

这要知道有这个语法糖就可以了，反正以后还真不一定用得到

异步处理主要用到的还是`Promise`跟`async/await`。

&emsp;

以上。

希望对你能有帮助，下期再见。

<center>- END -<center>&emsp;

---

<center>欢迎关注分享，一起学习提高吧。  
QRCode/微信订阅号二维码  
![CoderPowerQRCode](http://images.cnblogs.com/cnblogs_com/CoderMonkie/1483738/o_CoderPower_QRCode.jpg)

</center>
&emsp;

---