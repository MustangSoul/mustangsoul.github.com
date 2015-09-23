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