---
title: '2021-07-12-[筆記]JavaScript閉包'
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 3097947559
---
前言：
閉包概念從字面上蠻難直接理解，但我們可以簡單理解成他就是內層函數可以取得外層變數，並且同時造成全域變數污染問題。
`重新認識 JavaScript: Day 19 閉包 Closure`，這篇文章可以關注下方討論內容。會讓你有更清晰的理解。

<!-- more -->
---
六角學院-JavaScript核心篇
[重新認識 JavaScript: Day 19 閉包 Closure](https://ithelp.ithome.com.tw/articles/10193009)
[鐵人賽：另一種方式介紹 JavaScript 閉包](https://wcc723.github.io/javascript/2017/12/13/javascript-closure/)

---
### 閉包
補充一下 `Scope Chain` 概念
- 內層可以讀取外層變數，但外層不能讀取內層變數。當外層找不到變數時，會ㄧ直往外尋找直到 `Global`

```jsx
//直接拿 Kuro 老師範例
function outer() {
  var b = a * 2;
  function inner(c) {
    console.log(2,a, b, c);
  };
  inner(b * 3);
}
var a = 1;
outer(a);
```

子函式可以使用父函式變數，優點
- 變數作用域切割是以 `Function` 為單位，因此變數不會污染 Global(範圍鏈概念)
- 當持續被呼叫時，記憶體不會被釋放直到不使用

```jsx
function Parent(){
   var money = 1000;
   return function(price){
      money = money + price;
      return money;
   }
}

Parent()(100); //1100

//範例2 FROM KURO老師
var msg = "global."
function outer() {
  var msg = "local."
  function inner() {
    return msg;
  }
  return inner;
}
var innerFunc = outer;
var result1 = innerFunc();
console.log( result1 ); 
// ƒ inner() {
//   return msg;
//  }

//範例3 改寫範例2
var msg = "global."
function outer() {
  var msg = "local."
  return function inner() {
    return msg;
  }
}

var innerFunc = outer();
var result1 = innerFunc();
console.log( result1 ); //local.
```

### 為何我們要使用到閉包？
剛看到一個蠻好的範例，FROM KURO 老師文章
今天我們有一個計時器，我們要做累加動作。

```jsx
var count = 0;

function counter(){
  return ++count;
}

console.log( counter() );   // 1
console.log( counter() );   // 2
console.log( counter() );   // 3
```

這樣寫法的確OK，但我們今天如果有兩個計時器，就會需要第二個全域變數。如此會造成程式碼發生不可避免問題。
