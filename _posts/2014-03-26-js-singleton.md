---
layout: post
title: "JS设计模式-单例模式"
description: ""
category: 
tags: ['js', '设计模式']
---
{% include JB/setup %}

如果你懂闭包，那么直接上示例了，如果不懂，最好先了解下闭包的概念。

代码摘自网络 http://www.alloyteam.com/2012/10/common-javascript-design-patterns/ 如果感觉下面的代码太晦涩，可以直接看连接中的文章，讲的很不错。

```js
var createMask = function(){
  var mask;
  return function(){
       return mask || ( mask = document.body.appendChild( document.createElement('div') ) )
  }
}()
```

<!--more-->
通用版

```js
var singleton = function( fn ){
    var result;
    return function(){
        return result || ( result = fn .apply( this, arguments ) );
    }
}
 
var createMask = singleton(
  function(){
    return document.body.appendChild( document.createElement('div') );
  }
);

```
构造函数版

```js
function Person(){    
  //缓存实例  
  var instance=this;  
  //重写构造函数  
  Person=function(){  
      return instance;  
  }  
  //保留原型属性  
  Person.prototype=this;  
  //实例  
  instance=new Person();  
  //重置构造函数引用  
  instance.constructor=Person;  

  //其他初始化  
  instance.createTime=new Date();  
    
  return instance;  
}
```