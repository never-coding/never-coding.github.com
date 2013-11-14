---
layout: post
title: "gitignore失效的解决办法"
description: ""
category: 
tags: ['gitignore']
---
{% include JB/setup %}

有时候当你添加完gitignore配置之后会发现它并不起作用，这是因为你所需要忽略的文件已经被add过，或是之前被add过。也就说已经被git所追踪（tracked），解决这个问题很简单，只需要执行下面这个命令清除这个文件的缓存就行了：

```
git rm --cached your_file
```

然后再commit一次。也可用管道一次把.gitignore中的文件全部弄出去：

```
cat .gitignore | xargs git rm --cached
```
