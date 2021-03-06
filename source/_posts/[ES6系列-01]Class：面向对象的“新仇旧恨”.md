---
title: '[ES6系列-01]Class：面向对象的“新仇旧恨”'
date: 2019-06-10 20:34:44
tags: [js,javascript,es6]
categories: [JavaScript]
---

【原创】码路工人 Coder-Power

### 大家好，这里是码路工人有力量，我是码路工人，你们是力量。

[github-pages](https://codermonkey.github.io/CoderPower/)
[博客园cnblogs](https://www.cnblogs.com/CoderMonkie/)

---

这是公众号（码路工人有力量）开通后的第二篇，写得还是有待改进吧。  
这次准备写一个关于ES6基础的短文系列，努力尽快更完。  
欢迎关注分享，一起学习提高吧。  
QRCode/微信订阅号二维码  
![CoderPowerQRCode][CoderPowerQRCode]

---

今天主要聊聊JS中的面向对象即类的使用，先来看看ES5中的传统实践，再对比ES6中的便利优雅，面向未来又不忘历史。

# 1. ES5中的类与继承

## 1.1 function 是函数，也是类

先来一段例子代码

<!-- more -->

```javascript
/* eg.1
 * class example in ES5
 */

// Class Definition
function Person(name, gender) {
    this.name = name;
    this.gender = gender;

    Person.PCount++;
}
// Method Definition
Person.prototype.greeting = function(){
    console.log("Hi! I am " + this.name+ ".");
}
// JS also has static methods and properties.
Person.PCount = 0;
Person.GetPCount = function() {
    console.log("Static method called. PCount = " + Person.PCount);
}

// Instance
var p1 = new Person("Tom", "male");
p1.greeting();      // Hi! I am Tom.

var p2 = new Person("Jerry", "male");
p1.greeting();      // Hi! I am Jerry.

Person.GetPCount();      // Static method called. PCount = 2
```

- <font style="color:blue;background-color:lightgray">Person 构造函数</font>

    <code>Person</code> 在这里既是类定义（类名），又是构造器（构造函数）。对于CSharper或者Javaer，这多新鲜，类跟构造函数竟然是同一个东西。（所以到了ES6，写起来就舒服多了，从这里也能看出开发语言的相互学习与特性趋同趋势）

    构造函数：通过 <code>new 类名</code> 来创建一个函数的对象  
    实例：接收到 new 构造函数 创建出来的对象就是实例。

- <font style="color:blue;background-color:lightgray">prototype 原型</font>

    关于 <code>prototype</code> 即原型，用与实现对象的属性继承。有很多优秀的文章介绍原型链的，这里不再展开，或以后再做单独总结。

    其中的关系如下：
    - 构造函数.prototype === 原型
    - 实例.\_\_proto\_\_ === 原型
    - 原型.constructor === 构造函数


- <font style="color:blue;background-color:lightgray">JS类也可以有静态函数和静态属性</font>

    上面也提到了，这里说的构造器就是类名。

    构造器.属性名 = xxx  
    构造器.方法名 = foo(){}

    通过 构造器.属性名/方法名() 来调用。在 eg.1 中实现一个实例自动计数器。

## 1.2 实现好继承还需要抱团才行（组合继承）

ES5中对继承的支持比较弱，或者说面向对象支持比较弱，继承要绕弯子来实现。  
继承的实现方式有：
- <font style="color:blue;background-color:lightgray">通过构造函数继承</font>

  就是在 new 的时候，构造函数里用父类的构造函数调用 call/apply 来传递子类这个对象改变 this 指向。  
  原理上讲，就是用 call/apply，更改了父类构造函数里 this 的指向，实现了冒充继承。

- <font style="color:blue;background-color:lightgray">通过原型链继承</font>

    将子类的 prototype 属性 指向一个父类的新对象:  
    Child.prototype = new Parent();

- <font style="color:blue;background-color:lightgray">混合继承（即用构造函数又用原型链）</font>

  前两种分别有弊端所有混合才成了最佳实践。Talk is cheap, show you the code.

  ```javascript
  /* eg.2
   * extension example in ES5
   */
  
  // Child Class Definition
  function Student(name, gender, schoolName) {
      Person.apply(this, arguments);
      this.school = schoolName;
  }
  Student.prototype = Person.prototype;
  // or: 
  // Student.prototype = Object.create(Person);
  Student.prototype.constructor = Student;
  
  var s1 = new Student("Emily", "female", "Non-Famouse University");
  s1.greeting();                // Hi! I am Emily

  Person.GetPCount.apply(s1)    // Static method called. PCount = 3
  s1.GetPCount();               // Uncaught TypeError: s1.GetPCount is not a function
  ```

  在上面的 eg.2 中，注释里记录了运行结果，大家也可以把代码copy到chrome的Console里回车执行一下来查看。  

  很明显可以看到，Person 的属性和方法被继承了，但是静态属性和静态方法却没有，不能直接调用，不过可以绕路调用也就是仍然用Person，再用apply改变this指向子类。可以发现计数器确实增加了，也就是实例化子类时，父类里面有正常调用。

---

# 2. ES6中的类与继承

既然是ES6系列，ES5自然不是本文重点。回顾完了接下来我们看看ES6。

ES6中的类与继承主要概括为四个关键字：
  - class
  - constructor
  - extends
  - super
  - 除以上之外的补充：static 关键字

## 2.1 终于有了属于JS自己的Class

  ```javascript
  /* eg.3
   * class example in ES6
   */
  
  // Class Definition
  class Person {
      constructor(name, gender) {
          this.name = name;
          this.gender = gender;
  
          Person.PCount++;

          // console.log(new.target.name);
      }
  
      // Methods Definition
      greeting() {
          console.log("Hello! I am " + this.name + ".");
      }
      foo() {
          console.log("bar");
      }
  
      // mock static property
      static get PCount() {
          return Person.Count;
      }
      static set PCount(value) {
          Person.Count = value;
      }
  
      // static method
      static GetPCount() {
          console.log("Static method called in ES6. PCount = " + Person.PCount);
      }
  }
  // static property
  Person.Count = 0
  
  // Instance
  const p1 = new Person("Petter", "male");
  p1.greeting();      // Hello! I am Petter.
  
  const p2 = new Person("Ben", "male");
  p2.greeting();      // Hello! I am Ben.
  
  Person.GetPCount();      // Static method called in ES6. PCount = 2
  ```

- <font style="color:blue;background-color:lightgray">世界大同：class 关键字</font>

  与C#和java里采用了相同的定义方式：class关键字声明一个类。

  类成员方法的定义，有了简便写法，即 <code>方法名(){方法体}</code> ，后面继续定义方法的时候也不需要加逗号之类的分隔。

- <font style="color:blue;background-color:lightgray">构造函数：constructor 关键字</font>

  这样的写法看起来就舒服多了，类是类，构造函数是构造函数。

  类里的构造函数是必须存在的，如果没有显式指定，那么就会生成一个默认的构造函数(如下所示)。怎么样，听起来多么熟悉的味道，对于CShaper/Javaer。

  ```javascript
  ...
  constructor() {}
  ...
  ```

- <font style="color:blue;background-color:lightgray">静态方法：static 关键字</font>

  增加了static关键字，可以在类内部用来声明静态方法。

  静态方法的调用与之前相同，直接 <code>类名.静态方法()</code>

  不能用static在类里定义一个静态属性，但可以用 static get/set 来模拟操作属性。

## 2.1 继承变得很简单

  ```javascript
  /* eg.4
   * extension example in ES6
   */

  // Child Class Definition
  class Student extends Person {
      constructor(name, gender, schoolName) {
          super(name, gender);
          // must call [super] before use [this]
          this.school = schoolName;
      }

      greeting() {
          console.log("Hello! I am " + this.name + " and I am studying in " + this.school + ".");
      }
  }

  const s1 = new Student("Lily", "female", "Non-Famouse College");
  s1.greeting();                // Hello! I am Lily and I am studying in Non-Famouse College.

  Person.GetPCount.apply(s1);   // Static method called in ES6. PCount = 3
  s1.GetPCount();               // Uncaught TypeError: s1.GetPCount is not a function
  ```

- <font style="color:blue;background-color:lightgray">继承：extends 关键字</font>

  ES6中的类与继承其实内部还是用的prototype与constructor实现的，只是增加了语法糖，写起来就简单多了，看起来也是清晰多了。

  在 eg.4 中，我们重写了父类 Person 的 greeting 方法，所以在调用时打印内容不再是父类里的内容。

- <font style="color:blue;background-color:lightgray">调用/访问父类：super 关键字</font>

  通过 super 关键字，可以访问父类的属性或方法。比如在上面的 eg.4 中，重写的 greeting 方法还可以写成：
  ```javascript
  greeting() {
      super.greeting();     // Hello! I am Lily.
      console.log("Hello! I am " + this.name + " and I am studying in " + this.school + ".");
  }
  ```

  需要注意的一点是，在子类的构造函数里，若要给属性赋值（这就用到了 this)，必须要先调用 super，也就是先走父类的构造函数初始化，创建一个空对象（也就是咱们用到的 this），否则报错。

- <font style="color:blue;background-color:lightgray">补充（要实例化的类）：new.target 关键字</font>

  用 new.target 能区分要实例化的是哪个类，比如在实例化子类时，new.target.name 就是子类名字。  
  放开 class Person 的 constructor 的 <code>console.log(new.target.name);</code> 这句，可以确认到以下打印结果：
  ```javascript
  new Person()      // Person
  new Student()     // Student
  ```

---

读到这里，对于 JavaScript 里的类与继承就能一笑泯恩仇了吧。  
希望能有帮助，下篇再见。

---

[CoderPowerQRCode]:data:image/jpeg;base64,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