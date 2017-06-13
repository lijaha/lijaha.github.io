---
layout: post
author: lijaha
title: ES6函数扩展
description: ES6函数新特性
category: blog
---

#### 1.函数默认值
##### 定义：ES6允许为函数设定默认值，即直接写在参数定义的后面

    示例
    function print(x,y='world'){
      console.log(x,y);
    }
    print('hello');  //hello world
    在ES5中则需要判断传参是否存在，再进行默认值赋值

参数变量是默认声明的，使用let和const再次进行声明会报错，var声明则不会，因为let定义不允许在相同作用域内重复声明一个变量。

#### 2.函数的length属性
##### 定义：函数的length属性将返回没有指定默认值的参数个数

    示例
    //在ES5中获取函数的参数个数需要函数return
    function count(x,y){
      return arguments.length;
    }
    //ES6中新增函数length属性
    (function (x,y){}).length;  //2
    function count(x,y = "world"){
    }
    console.log(count.length);  //1,指定默认值不算进去

#### 3.函数的name属性
##### 定义：获取函数的名称

    var hello = function(){};
    hello.name;  //hello
    //Function构造函数返回的示例name为anonymous
    (new Function()).name;  //anonymous

#### 4.rest参数
##### 定义：rest参数的写法为(...变量名)，用于获取函数多余的变量，可替代arguments，rest参数中的变量是一个数组，arguments是类数组对象需要使用Array.from()方法转换成真正数组。
<br/>

    //示例
    function add(...numbers){
      let count = 0;
      for (let i of numbers){
        count += i;
      }
      return count;
    }
    //或者使用numbers.forEach(x => count += x);
rest参数变量是一个数组，数组特有的方法都可以使用。
rest参数后不能再有其他的参数，rest参数必须为最后一个参数,使用函数属性length获取参数个数，rest参数不计入。

    示例
    function add(a,...numbers,c){
    }  //error
    (function(a,b,...numbers){}).length;  //2,rest参数不算

#### 5.扩展运算符...
##### 定义： 扩展运算符的写法为(...),将一个数组转为用逗号分隔的参数序列

    示例
    console.log(1,...[2,3,4,5],6);  //1,2,3,4,5,6

使用扩展运算符替代apply()方法

    //ES5
    Math.max.apply(null,[4,6,0]);  //Math.max不能接受数组为参数
    Math.max(4,6,0);
    //ES6
    Math.max(...[4,6,0]);

使用扩展运算符合并数组

    //ES5
    var arr1 = [1,2,3];
    var arr2 = [4,5,6,];
    var arr = arr1.concat(arr2);
    //ES6
    var array1 = Array.of(1,2,3);
    var array2 = Array.of(4,5,6);
    var array = [...array1,...array2];

使用扩展运算符可将具有Iterator接口的数据结构转换成真正的数组(ES6数组扩展篇章也有提及)

    [...'hello'];  //将字符串转化成数组
    var NodeList  = [...document.querySelectorAll('p')];//类似数组对象
    var someSet = new Set([4,5,6]);
    var array = [...someSet.keys()];  //Set数据结构
    var someMap = new Map([['name','lijaha'],['age',20]]);
    var array = [...someMap.keys()];  //Map数据结构

#### 6.箭头函数
##### 定义： ES6允许使用箭头( => )定义函数

    示例
    var hello = x => x;
    //如果箭头函数不需要参数或者需要多个参数就用()圆括号代表参数部分
    var hello = () => 1;  //return 1
    var hello = (x,y) => x+y;
    //如果箭头函数的代码块语句多于一句，需要使用大括号{}括起来
    var hello = (x,y) => {return x+y};
    //如果箭头函数返回的是对象，则需要在大括号外加上小括号({})
    var hello = id => ({id: id,name: 'world'});

箭头函数体内的this对象是定义时所在的对象，而不是使用时所在的对象，称为箭头函数的this指向固定化。因为箭头函数内部是没有自己的this(不能作为构造函数，也不能使用apply、call、bind等方法改变this指向)，所以它的this是外层代码块的this。

箭头函数内部没有arguments对象，需使用rest参数代替
    var hello = (...numbers) => {console.log(...numbers)};

#### 7.尾调用优化
#####  定义：指某个函数在最后一步调用另一个函数

    function hello(){
      return hi();
    }  //尾调用的结尾一定是return xx();

函数调用会在内存中形成一个“调用帧”，保存调用位置和内部变量等信息。如果函数A中调用用了函数B，则会在函数A调用帧的上方形成一个B的调用帧，函数B执行完毕后，函数A中的调用帧B才会结束。如果函数B内调用了函数C，就会形成一个C地调用帧，所有的调用帧就会形成一个‘调用栈’。

    //尾调用是函数的最后一步操作，所以不需要保留外层函数的调用帧，外层函数的调用位置和内部变量都不会用到。
    function hello(){
      let m = 1;
      let n = 2;
      return g(m+n);
    }
    //等同于
    function hello(){
      return g(3);
    }
    //等同于
    g(3);
    //上面代码中，如果函数g不是尾调用则函数hello需要保留内部变量m、n以及调用位置等信息，由于函数hello调用函数g后，hello函数就结束了，则可以删除hello()的调用帧，只保留g()的调用帧。

这就叫做‘尾调用优化’，即只保留内层函数的调用帧，如果所有的函数都是尾调用，则可以做到每次执行时调用帧只有一项。

    //只有不再用到外层函数的内部变量，内层函数的调用帧才能取代外层函数的调用帧，实现尾调用优化。
    function hello(a){
      let b = 1;
      function hi(a){
        return a + b;  //使用了hello函数的内部变量b
      }
      return hi(a);
    }

#### 8.尾递归
##### 函数自己调用自己则叫递归，函数在尾部调用自己则称为尾递归

    //使用递归实现阶乘，递归过程会比较耗费内存，因为保存大量的调用帧，容易发生栈溢出。
    function factorial(n){
      if(n == 1) return 1;
      return n*factorial(n-1);
    }
    //使用尾递归
    function factorial(n,total=1){  //使用默认值
      if(n == 1) return total;
      return factorial(n-1,n*total);
    }  //每次只保存一个调用记录
    //一般的递归的复杂度为O(n),使用尾递归的复杂度为O(1)

需要开启严格模式，尾调用优化才会生效，一旦使用尾调用优化，函数的内部对象arguments和caller都会失效，因为整个外层函数调用帧会被删除掉，这两个对象也就不存在了。严格模式下，这两个对象也是不可用的。

    function hello(){
      "use strict";
      hello.arguments;  //error
      hello.caller;  //error
    }

本文章参考阮一峰《ES6 标准入门》
