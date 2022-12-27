---
title: js杂谈
date: 2022-11-10 21:38:58
tags:
---
关于变量let和const
    let:let在块中声明只能在块中被引用，var在块中声明则是全局引用的
        <img src="/images/var全局变量.jpg" width="20%" height="20%"/>   <img src="/images/let局部变量.jpg" width="20%" height="20%"/>
        当然let和var都拥有全局作用域，通过 var 关键词定义的全局变量属于 window 对象，let无法属于window对象。
        在相同的作用域，或在相同的块中，通过 let 重新声明一个 var 变量是不允许的；在相同的作用域，或在相同的块中，通过 let 重新声明一个 let 变量是不允许的。
        <img src="/images/let不能重申1.jpg" width="20%" height="20%"/>
        <img src="/images/let不能重申2.jpg" width="20%" height="20%"/>
        只有在不同的作用域或块中，通过 let 重新声明变量是允许的。
    const:const的作用与let类似，但与之不同的是，const赋予的值不能在后面重新声明，但可以更改常量值的属性。
        注意哦，不止是重新声明无法进行，对于const赋值的数也不能进行更改，如下图。
        <img src="/images/const1.jpg" width="25%" height="25%"/>
        当然，const在另外的作用域或者块中可以重新声明变量
        <img src="/images/运算符1.jpg" width="25%" height="25%"/>
        <img src="/images/运算符2.jpg" width="25%" height="25%"/>
        <img src="/images/运算符3.jpg" width="25%" height="25%"/>

关于typeof运算符：
    <img src="/images/typeof.jpg" width="40%" height="40%"/>