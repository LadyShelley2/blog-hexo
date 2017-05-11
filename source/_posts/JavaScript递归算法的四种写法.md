---
title: JavaScript递归算法的四种写法
date: 2017-05-11 14:01:43
tags:
---
---
title: 递归算法三种写法(Javascript)
date: 2017-05-11 11:32:12
tags:
-JavaScript
-前端开发
-算法
---

>  转载需提前联系译者，未经允许不得转载。
本篇文章为《JavaScript语言精粹》学习笔记。

# 提纲
《JavaScript语言精粹》函数记忆一章中提到了记忆一节，通过递归的例子说明将中间结果存下来对算法性能的提升，并巧妙利用JavaScript中函数是第一公民、闭包等思想实现了通用的递归，很巧妙，特做笔记以便日后温故而知新。

<!--more--> 

#题目说明

以递归经典题目fabonacci数列为例，公式如下：

$$
F_n=\left\{
    \begin{Array}{ll}
        0 & \textrm{if}n=0;\\
        1 & \textrm{if}n=1;
        F_{n-1}+F_{n-2} & \textrm{if} n\lt2.
    \end{Array}
    \right.
$$

通俗来讲就是第一项为0，第二项为1，之后的每项等于前两项之和，因此数列为

$$
0,1,1,2,3,5,8,13,\ldots
$$

# 第一种写法

最普通的写法

```javascript
function fibonacci(n){
  return n<2?n:(fibonacci(n-1)+fibonacci(n-2));
}
fibonacci(3)
```
这种写法的主要问题在于计算次数，时间复杂度为指数$O(2^n)$

# 第二种写法

用一个数组将中间结果存下来：

```javascript
function f(num){
  var memo = [0,1];
  var innerf = function(n){
    if(typeof memo[n] != 'number'){
      memo[n] = innerf(n-1)+innerf(n-2);
    }
    return memo[n];
  }
  return innerf(num);
}

console.log(f(4))
```

# 第三种写法

从递归树最底层向上算

```javascript
function f(n){
   var memo=[0,1];
   for(var i=2; i<=n; i++){
     if(typeof memo[i] != 'number'){
       memo[i] = memo[i-1]+memo[i-2];
     }
   }
  return memo[n];
}
```

# 第四种写法

封装递归函数

```javascript
var memoizer = function (memo, formula) {
  var recur = function(n){
    if(typeof memo[n]!='number'){
      memo[n]=formula(recur,n);      
    }
    return memo[n];
  }
  return recur;
}

var fabonacci = memoizer([0,1],function(recur,n){
  return recur(n-1)+recur(n-2);
})
```
扩展很简单，求阶乘

```javascript
var factorial = memoizer([1,1],function(recur,n){
  return n*recur(n-1);
})
```