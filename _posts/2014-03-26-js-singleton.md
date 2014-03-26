---
layout: post
title: "JS 单例模式"
description: ""
category: 
tags: ['js', '设计模式']
---
{% include JB/setup %}

如果你懂闭包，那么直接上示例了，如果不懂，最好先了解下闭包的概念
代码摘自网络

```js
var createMask = function(){
  var mask;
  return function(){
       return mask || ( mask = document.body.appendChild( document.createElement('div') ) )
  }
}()
```

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
