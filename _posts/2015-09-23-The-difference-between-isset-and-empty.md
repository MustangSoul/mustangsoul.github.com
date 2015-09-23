---
layout:     post
title:      "函数 isset() & empty() 的区别"
subtitle:   "PHP语法"
date:       2015-09-23 19:00:00
author:     "Geekzhou"
header-img: "img/post-bg-04.jpg"
---

##函数映射

***

|变量值|isset()返回值|empty()返回值|
|-|
|<span style = "color:red">NULL</span>|<span style = "color:red">0</span>|<span style = "color:red">1</span>|
|false|1|1|
|array()|1|1|
|0|1|1|
|"0"|1|1|
|设置过的非上述变量|1|0|
|未设置的变量|0|1|

***

##总结

1.判断变量是否被设置过

有两种方案可以选择,一种是使用isset()来判别,一种是使用!empty()来判别.二者的区别为当变量($a)的值设为<span style = "color:blue">array(),flase,0,"0"</span>时,$a明明被设置过，但是!empty()返回的是0.这样就没有达到辨别变量是否被设置的初中,因此,

<span style = "color:red">判断变量是否被设置过时,必须使用isset()函数.</span>