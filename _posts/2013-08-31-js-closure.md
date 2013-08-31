---
layout: post
title: "JS闭包定义"
description: ""
category: 
tags: ['闭包']
---
{% include JB/setup %}

闭包在JS中有着举足轻重的地位，应用面也很广。比如现在比较流行的一些JS设计模式或编程模式中，如单例模式。几乎所有流行的JS框架中也都大量采用闭包的方法，如jQuery。另外如果你想要用JS面向对象的方式编程，定义私有属性或方法，你就少不了要用到闭包。

所以这里有必要重新申明一下闭包的定义（采自：[维基百科](http://zh.wikipedia.org/wiki/%E9%97%AD%E5%8C%85_\(%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6\))）：
  
>在计算机科学中，**闭包（Closure）**是**词法闭包（Lexical Closure）**的简称，是引用了自由变量的函数。这个被引用的自由变量将和这个函数一同存在，即使已经离开了创造它的环境也不例外。所以，有另一种说法认为闭包是由函数和与其相关的引用环境组合而成的实体。

<!--more-->
闭包通常出现在将函数当作第一级对象的语言中——在这些语言中，函数可以被当作参数传递，也可以作为返回值返回，就像字符串、整数等简单类型。

---

### 闭包的用途


* 因为闭包只有在被调用时才执行操作，所以它可以被用来定义控制结构。
* 多个函数可以使用一个相同的环境，这使得它们可以通过改变那个环境相互交流。
* 闭包可以用来实现对象系统

---

### 闭包的必要条件

从以上的定义中我们就可以看出，要想使用闭包必须要满足三个条件：

1. 函数
2. 自由变量
3. 自由变量和函数同在

其实如果不理解自由变量没关系。自由变量基本上在闭包的环境中才能成为自由变量。

---

### 例子

说了这么多看几个例子吧，可以把下面的例子拷到你的Chrome或Firefox的控制台执行，用IE6、7、8的让我鄙视下 

(︶⌒︶メ)╭∩╮

例子1：

```js
var count = (function() {
  var i = 0;
  return function() {
    console.log(++i);
  }
})() // 自执行函数

count(); // 输出1
count(); // 输出2
count(); // 输出3
```

例子2（摘自网络 <http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html>）：

```js
var name = "The Window";

var object = {
  name : "My Object",
  getNameFunc : function(){
    return function(){
      return this.name;
    };
  }
};

alert(object.getNameFunc()());
```

例子3（摘自网络 <http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html>）：

```js
var name = "The Window";

var object = {
  name : "My Object",
  getNameFunc : function(){
    var that = this;
    return function(){
      return that.name;
    };
  }
};

alert(object.getNameFunc()());
```

---

### 使用闭包的注意点


1. 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
2. 闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。

