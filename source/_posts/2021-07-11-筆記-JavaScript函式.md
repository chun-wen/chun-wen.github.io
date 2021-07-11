---
title: '2021-07-11-[筆記]JavaScript函式'
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 543804941
---
前言：
主要就紀錄一下目前 JavaScript 常用，但自己又不熟悉的筆記。
<!-- more -->
---
參考資料：
[重新認識 JavaScript: Day 10 函式 Functions 的基本概念](https://ithelp.ithome.com.tw/articles/10191549)
[When to use a function declaration vs. a function expression](https://www.freecodecamp.org/news/when-to-use-a-function-declarations-vs-a-function-expression-70f15152a0a0/)

---

### 函式是什麼？
將可以重複被調用的`程式碼`  包在 `{}`  中。函式可以被呼叫，而依照函式定義方式，又可以分為下面幾種。
1. 函式宣告式 (Function Declaration)
2. 函式表達式 (Function Expression)

```jsx
function Declaration(){
   console.log("函式宣告式")
}

const expression = function (){
   console.log("函式表達式")
}
expression();

const Test = function TestB(){
   console.log(Test,TestB)
}
Test();
console.log(Test,TestB) // TestB is not defined，因為他只能在函式內被調用
```

### 使用時機
我在看這兩種寫法時候，我其實一直很好奇為何要使用 `Function Expression` 寫法？我自己明明就用 `Function Declaration` 用得很順，而且他也具備 Hoisting 優點，我什麼時候會使用到它呢？

直到我看到這篇，雖然不能滿足我的好奇，但至少給了我一些想法。

1. `Function Expression` 我們很清楚它可以直接在全域被調用。
2. `Function Declaration` 可以限制被調用的作用域。

補充：在 Airbnb 規範下，是不建議使用函式陳述式 (宣告式)，主要原因在於 `hoisting` 的問題在大型專案中可能會影響到其它程式碼的運行

[https://github.com/airbnb/javascript#functions--declarations](https://github.com/airbnb/javascript#functions--declarations)

### 立即函式(IIFE)
顧名思義就是立即執行，很常用在`限制變數作用域`。寫法如下：

```jsx
// 匿名函式
(function(){
   console.log("立即函式");
})();

// 具名函式
(function IIFE(){
   console.log(IIFE);
})();
IIFE(); // IIFE is not defined

let result = (function IIFE(param){
   console.log(1, param);
    return param;
})("Test");
console.log(2, result); //Test

```