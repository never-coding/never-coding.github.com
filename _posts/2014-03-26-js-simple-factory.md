---
layout: post
title: "JS设计模式-简单工厂模式"
description: ""
category: 
tags: ['js', '设计模式']
---
{% include JB/setup %}

摘自：http://www.alloyteam.com/2012/10/commonly-javascript-design-patterns-simple-factory-pattern/

简单工厂模式是由一个方法来决定到底要创建哪个类的实例, 而这些实例经常都拥有相同的接口. 这种模式主要用在所实例化的类型在编译期并不能确定， 而是在执行期决定的情况。 说的通俗点，就像公司茶水间的饮料机，要咖啡还是牛奶取决于你按哪个按钮。
简单工厂模式在创建ajax对象的时候也非常有用.
之前我写了一个处理ajax异步嵌套的库，地址在 https://github.com/AlloyTeam/DanceRequest

这个库里提供了几种ajax请求的方式，包括xhr对象的get, post, 也包括跨域用的jsonp和iframe. 为了方便使用, 这几种方式都抽象到了同一个接口里面.

```js
var request1 = Request('cgi.xx.com/xxx' , ''get' );
request1.start();
request1.done( fn );

var request2 = Request('cgi.xx.com/xxx' , ''jsonp' );
request2.start();
request2.done( fn );
```

Request实际上就是一个工厂方法, 至于到底是产生xhr的实例, 还是jsonp的实例. 是由后来的代码决定的。
实际上在js里面，所谓的构造函数也是一个简单工厂。只是批了一件new的衣服. 我们扒掉这件衣服看看里面。
通过这段代码, 在firefox, chrome等浏览器里，可以完美模拟new.

```js
  function A( name ) {
    this.name = name;
  }

  function ObjectFactory() {
    var obj = {}, Constructor = Array.prototype.shift.call( arguments );
    obj.__proto__ =  typeof Constructor .prototype === 'number'  ? Object.prototype : Constructor.prototype;
    var ret = Constructor.apply( obj, arguments );
    return typeof ret === 'object' ? ret : obj;
  }

  var a = ObjectFactory( A, 'svenzeng' );
  alert ( a.name );  //svenzeng
```

这段代码来自es5的new和构造器的相关说明。可以看到，所谓的new，本身只是一个对象的复制和改写过程，而具体会生成什么是由调用ObjectFactory时传进去的参数所决定的。