---
title: '[CSS布局基础]居中布局的实现方式总结'
date: 2019-06-20 17:06:54
tags: [CSS]
categories: [CSS]
---

【原创】码路工人 Coder-Power

#### 大家好，这里是码路工人有力量，我是码路工人，你们是力量。

[github-pages](https://codermonkey.github.io/CoderPower/)  
[博客园cnblogs](https://www.cnblogs.com/CoderMonkie/)

---

#### 做Web开发少不了做页面布局。码路工人给大家总结一下水平居中，垂直居中，水平垂直居中的布局实现。

---

# 1.水平居中

#### 通过以下四种方式，将实现下图中的效果

![Horizontal-Center][Horizontal-Center]

## 1.1 利用父级 **`text-align: center;`** 加子级 **`display: inline-block;`**（只要是`inline-`的都可以）实现子元素水平居中

<!-- more -->

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-h-center-1.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .parent {
            text-align: center;
        }
        .child {
            display: inline-block;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 1.2 利用弹性布局 **`flex`**，将父级设为 **`display: flex;`** 加 **`justify-content: center;`** 实现子元素水平居中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-h-center-2.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .parent {
            display: flex;
            justify-content: center;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 1.3 利用相对布局加平移，将子级设为 **`position: relative;`** 加 **`left: 50%;`** 加 **`transform: translateX(-50%);`** 实现子元素水平居中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-h-center-3.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .child {
            position: relative;
            left: 50%;
            transform: translateX(-50%);
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 1.4 将子元素左右间距设为 **`auto`** 实现子元素水平居中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-h-center-4.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .child {
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

---

# 2. 垂直居中

#### 通过以下四种方式，将实现下图中的效果

![Vertical-Center][Vertical-Center]

## 2.1 利用 **`table-cell`** ，将父级设为 **`display: table-cell;`** 加 **`vertical-align: middle;`** 实现子元素垂直居中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-v-center-1.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .parent {
            display: table-cell;
            vertical-align: middle;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 2.2 利用弹性布局 **`flex`**，将父级设为 **`display: flex;`** 加 **`align-items: center;`** 实现子元素垂直居中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-v-center-2.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .parent {
            display: flex;
            align-items: center;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 2.3 利用相对布局加平移，将子级设为 **`position: relative;`** 加 **`top: 50%;`** 加 **`transform: translateY(-50%);`** 实现子元素垂直居中

子元素的左上角顶点固定到父元素的垂直中点，  
然后再以自身的一半向上平移，实现垂直居中。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-v-center-3.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .child {
            position: relative;
            top: 50%;
            transform: translateY(-50%);
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 2.4 通过绝对布局加 margin ，将父级设为 **`position: relative;`** ，加子元素设上下左右均为 **`0`** 并且 **`margin: auto 0;`** 实现子元素垂直居中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-v-center-4.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .parent {
            position: relative;
        }
        .child {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            margin: auto 0;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

---

# 3. 水平垂直居中

#### 通过以下四种方式，将实现下图中的效果

![Both-Center][Both-Center]

#### 上面分别列举了水平居中与垂直居中的4种实现方式，那么要实现水平+垂直的居中，就很容易了，把上面的组合起来就可以。为了统一好看，我们还是列举4个代码样例片段吧。

## 3.1 与前文的第一种对应

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-h-center-1.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .parent {
            text-align: center;
            
            display: table-cell;
            vertical-align: middle;
        }
        .child {
            display: inline-block;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 3.2 与前文的第二种对应

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-h-center-1.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .parent {
            display: flex;
            justify-content: center;
            align-items: center;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 3.3 与前文的第三种对应

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-h-center-1.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .child {
            position: relative;
            left: 50%;
            top: 50%;
            transform: translateX(-50%) translateY(-50%); 
            /* translateX 与 translateY 要写在一个 transform 里 */
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

## 3.4 与前文的第四种对应

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>layout-h-center-1.html</title>
    <style>
        /* 为了不影响理解，对于布局非关键的样式单独放在这里 */
        body {
            background-color: lightgray;
        }
        .parent {
            background-color: lightblue;
            width: 500px;
            height:400px;
        }
        .child {
            background-color: lightyellow;
            width: 300px;
            height:200px;
        }

        /* 布局关键样式在这里 */
        .parent {
            position: relative;
        }
        .child {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            margin: auto;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child"></div>
    </div>
</body>
</html>
```

---

列举了这么多，大家都掌握了吗？

其实也不必全部掌握，上面的布局实现，以 **`flex`** 实现方式作为重点。  
这里主要总结几种方式，没有过多纠结其中细节。

码路工人认为，将来的话 **`flex`** 与 **`grid`** 布局方式会成为主流。这两个不是哪个好的问题，而是相互补充，**`flex`** 简单说就是一行一列（实际上里面也有很多），**`grid`** 的话就理解为类似 **`Bootstrap`** 的栅格吧，多行多列。

建议布局方面的话，学习 **`flex`** 跟 **`grid`** 。码路工人作为转前端的新手，**`CSS`** 知识浅薄，就暂时不献丑了。以后，也可以做个 **`CSS3基础`** 的学习系列。不过暂时呢，还是要把我们的 **`ES6基础系列`** 写完。（感觉有太多事情要做有木有？。。）

以上。

---

希望对你能有帮助，下期再见。

欢迎关注分享，一起学习提高吧。  
QRCode/微信订阅号二维码  
![CoderPowerQRCode](http://images.cnblogs.com/cnblogs_com/CoderMonkie/1483738/o_CoderPower_QRCode.jpg)

---

[Horizontal-Center]:data:image/png;base64,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

[Vertical-Center]:data:image/png;base64,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

[Both-Center]:data:image/png;base64,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wQAAaDAAABoMAAA0GAAADQYAABoMAIAGAwAADQYAQIMBAIAGAwCgwQAAQIMBANBgAAA02F8EAAAaDACABgMAAA0GAECDAQCABgMAoMEAAECDAQDQYAAAoMEAAGgwAADQYAAANBgAAA0GAAAaDACABgMAAA0GAECDAQCABgMAoMEAAECDAQDQYAAAoMEAAGgwAAAaDAAANBgAAA0GAAAaDACABgMAAA0GAECDAQCABgMAoMEAAECDAQDQYAAANFiDAQDQYAAANBgAAGgwAAAaDAAANBgAAA0GAAAaDACABgMAAA0GAECDAQCABgMAoMEAAGgwAADQYAAANBgAAGgwAAAaDAAANBgAAA0GAAAaDACABgMAAA0GAECDAQDQYAAAoMEAAGgwAADQYAAANBgAAGgwAAAaDAAANBgAAA0GAAAaDACABgMAoMEaDACABgMAoMEAAECDAQDQYAAAoMEAAGgwAADQYAAANBgAAGgwAAAaDAAANBgAAA0GAECDAQCABgMAoMEAAECDAQDQYAAAoMEAAGgwAADQYAAANBgAAGgwAAAaDACABgMAAA0GAECDAQCABgMAoMEAACBVDSZJkpn3/wPDgcH/4CA+cgAAAABJRU5ErkJggg==