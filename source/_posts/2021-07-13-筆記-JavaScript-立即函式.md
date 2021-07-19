---
title: '2021-07-13-[筆記]JavaScript 立即函式'
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 2451288997
---
前言：
立即函式的出現解決了全域變數外洩的問題。

<!-- more -->
---
參考資料：
[立即呼叫的函式介紹-IT幫幫忙](https://ithelp.ithome.com.tw/articles/10193313) 
[談談JavaScript中的IIFEs-PJchen](https://pjchender.blogspot.com/2016/05/javascriptiifesimmediately-invoked.html)
[筆記 進一步談JavaScript中函式的建立─function statements and function expressions](https://pjchender.blogspot.com/2016/03/javascriptfunction-statements-and.html) 
[筆記 為什麼我們要用IIFEs(Immediately Invoked Functions Expressions)](https://pjchender.blogspot.com/2016/05/iifesimmediately-invoked-functions.html)

---

### 立即函式介紹(Immediately Invoked Functions Expressions)
說明：就是用 function expression 的方式建立函式後並立即執行它 
優點：IIFEs 內所定義的變數並不會跑出去這個函式之外而干擾到程式其他的部分

### Function expression寫法：

```jsx
//function expression 
var hello = function (name){
console.log('Hello ' + name); 
};
console.log(hello);
//ƒ (name){console.log('Hello ' + name); }
```

接著，我們只要在程式碼最後面加上`（）`就可以執行勒

```jsx
var hello = function(name){
  console.log('Hello ' + name); 
}('Andy');
console.log(hello) //Hello Andy

(function(){ 
  console.log("Andy")
}());

案例2:
var welcome = function(name){  
   return ('welcome' + name)
}('Andy');
console.log(welcome) //welcomeAndy
```

> 要注意的是，在利用 IIFE 的寫法後，原本的變數 welcome 已經變成函式執行後回傳的「字串」，它已經是字串了，所以我們沒辦法在去執行它！如下範例

```jsx
var sayWelcomeIIFEs = function(name) {  
   return('Welcome ' + name)
}('PJCHEN');
console.log(sayWelcomeIIFEs());
 //sayWelcomeIIFEs is not a function
```

### Function Declaration寫法：

```jsx
// 不可行的做法
// 出現 Function statements require a function name
function(name) {  
 return('Welcome, ' + name);
}

所以，我們可以改成下面這樣：
(function(food){
 console.log('大俠愛吃' + food)
}('薯條'));
//result:大俠愛吃薯條
```

> 最常使用的做法就是用括號 () 把 function(){ ...} 包起來
原理：因為我們只會在括弧內放入expression，如（3+2）。而不會放 statement 在括弧內，所以JavaScript 就會以 expression 的方式來讀取這段函式。

### 補充一下
如果全域變數和IIFE內都有重複變數名呢？那我們該如何取用全域變數呢？ 

Step1.將window當作參數傳入 >>使其成為這個IIFE的區域物件，確保在IIFE內的程式能故意取用到全域的特定變數。

```jsx
var food = '水牛城雞翅';
console.log(food);

(function(global){    
 var food = '雞塊';      
 global.food = '麥脆雞';    
 console.log(food);
})(window);

console.log(food);//水牛城雞翅//雞塊//麥脆雞

```