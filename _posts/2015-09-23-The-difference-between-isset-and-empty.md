---
layout:     post
title:      "函数 isset() & empty() 的区别"
subtitle:   "PHP语法"
date:       2015-09-23 19:00:00
author:     "Geekzhou"
header-img: "img/post-bg-04.jpg"
---

![思维导图](http://www.geekzhou.com/bimg/2015092321.png)

##函数映射表

***

|变量值|isset()返回值|empty()返回值|
|-|
|<span style = "color:red">NULL</span>|<span style = "color:red">0</span>|<span style = "color:red">1</span>|
|false|1|1|
|array()|1|1|
|0|1|1|
|"0"|1|1|
|赋过值的非上述变量|1|0|
|未赋值的变量|0|1|

***

##总结

1.判断变量是否被赋过值的方式

有两种方案可以选择,一种是使用isset()来判别,一种是使用!empty()来判别.二者的区别为当变量($a)的值设为<span style = "color:green">array(),flase,0,"0"</span>时,<span style = "color:blue">$a明明被赋过值，但是!empty()返回的是0.</span>这样就没有达到辨别变量是否被赋值的初衷,因此,

<span style = "color:red">判断变量是否被赋过值时,必须使用isset()函数.</span>

2.isset(NULL) 返回的值为 0 的原因

首先确定未定义的变量返回什么值.执行下面的代码:
    $lab = $undefined_variable;

    if($lab == 0) {

        echo '$lab == 0,true!';echo "<br>";
    }
    if($lab == NULL) {

        echo '$lab == NULL,true!';echo "<br>";
    }
    if($lab == false) {

        echo '$lab == false,true!';echo "<br>";
    }
    if($lab === 0) {

        echo '$lab === 0,true!';echo "<br>";
    }
    if($lab === NULL) {

        echo '$lab === NULL,true!';echo "<br>";
    }
    if($lab === false) {

        echo '$lab === false,true!';echo "<br>";
    }

结果为:

$lab == 0,true!

$lab == NULL,true!

$lab == false,true!

$lab === NULL,true!

因此可以确定:<span style = "color:red">未定义变量的返回值为NULL.</span>
因此,isset(NULL)返回的值为0的原因为:NULL是未定义变量返回的值.

3.扩展

###相等符号(==)和全等符号(===)对输入的0,null,false返回的结果不同容易导致的问题

以strpos()函数为例,执行以下代码:

    $string = 'ABCDEFG';

    $res1 = strpos($string,'ABC');
    $res2 = strpos($string,'XYZ');

    if(!$res1) {

        echo '1';
        echo "<br>";
    }

    if(!$res2) {

        echo '2';
        echo "<br>";
    }

    if($res1 !== false) {

        echo '3';
        echo "<br>";
    }

    if($res2 !== false) {

        echo '4';
        echo "<br>";
    }

结果为:

1

2

3

由实验结果可知.<span style="color:red">此类判断的条件必须使用全等符号,相等符号会产生逻辑错误.</span>

(只要两个变量的值相同就称为相等,而全等必须要两个变量的值和类型都相同才可以.)

###易由 isset()函数的返回值 导致的逻辑问题

如果输入的变量被赋过值,isset()返回true.
如果输入的变量没有被赋过值,isset()返回false.

执行下面的代码:
    $val = 6;
    $res = isset($val)? : 'none';

    if($res === true) {
        echo '$res = true';
    }
    if($res === 6) {
        echo '$res = 6';
    }

结果为$res = true.
因此,<span style = "color:red">当在三目运算符的条件部分isset()函数时,不能省略中间的参数.</span>

