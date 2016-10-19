---
layout: post
title:  "Deep clone and shallow clone"
date:   2016-10-19 15:58:22 +0800
categories: dependence
---

#Deep cloone and shallow clone

## 简介
- 术语： Deep clone 深拷贝； Shallow Clone 浅拷贝

- 这个概念面向的对象是谁？

    答： Object. 任何对象，它可能的类型有Array, Date, RegExp, Boolean, Number, String以及 Object（所有自定义的对象全都继承于Object）。 注意没有Function类型奥。

- 为什么会有 Deep Copy？

    答： 
    - 此对象要传递给函数，怕被函数修改
    - 想修改此对象，怕影响原来的对象
    
- 有什么例子吗？
    
    答：
    
    - ES6的assign： Shallow Copy
    - ES5中的freeze： ShallowCOpy
    -
## 参考
- [Understanding Object Cloning in Javascript - Part. II](http://blog.soulserv.net/understanding-object-cloning-in-javascript-part-ii/)
- [JavaScript 如何完整实现深度Clone对象？](https://www.zhihu.com/question/47746441)
