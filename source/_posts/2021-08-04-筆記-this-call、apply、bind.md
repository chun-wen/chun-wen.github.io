---
title: '2021-08-04-[筆記]this:call、apply、bind'
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 3302669428
---
前言：
`call`、`apply`、`bind` 這三個方法可以改變 Function 內的動態 `this`。

<!-- more -->
---
參考資料：
JavaScript 核心篇
[[JavaScript] 函數原型最實用的 3 個方法 — call、apply、bind](https://realdennis.medium.com/javascript-%E8%81%8A%E8%81%8Acall-apply-bind%E7%9A%84%E5%B7%AE%E7%95%B0%E8%88%87%E7%9B%B8%E4%BC%BC%E4%B9%8B%E8%99%95-2f82a4b4dd66)
[JavaScript - call，apply，bind](https://ithelp.ithome.com.tw/articles/10195896)
[[筆記] 了解function borrowing和function currying ─ bind(), call(), apply() 的應用](https://pjchender.blogspot.com/2016/06/function-borrowingfunction-currying.html)

---
### 使用時機：
都是用再明確指定 `this` 的時候。

### Call

```jsx
let family ={
  name:"小明",
  age:25
}

function fn(para1,para2){
  console.log(this,para1,para2);
}

fn(1,2); // window,1,2
fn.call(family,3,4); // {name: "小明", age: 25} 3 4
```

我們可以看到透過 `call` 方法，我們將函式內的 `this` 取代為外部傳入的 `family` 物件

### Apply
與 `call` 差異只在於 `apply` 必須傳入陣列，如過不是傳入陣列資料則會顯示下面錯誤訊息

```jsx
let family ={
  name:"小明",
  age:25
}

function fn(para1,para2){
  console.log(this,para1,para2);
}

 fn.apply(family,[5,6]);  // {name: "小明", age: 25} 5,6
// fn.apply(family, 6,7); //   Uncaught TypeError: CreateListFromArrayLike called on non-object
```

### Bind
與上面兩者差異在於 Bind 是回傳一個回呼函式

```jsx
function fn(para1,para2){
  console.log(this,para1,para2);
}

let temp = fn.bind(family,7,8);
temp(); //{name: "小明", age: 25} 7 8
```

### 差異
- apply 用在當函式傳入數量不固定，且是陣列
- bind  會回傳一個包裹函式，當我們執行這個函式時，同時也會將帶入 bind 的 arguments 一起帶進 Function 中。

### 補充

在非嚴格模式下，`null` 、`undefined` 將會被置換成全域變數，反之則不會

```jsx
// 嚴格模式
"use strict";

function fn(para1,para2){
  console.log(this,para1,para2);
}

fn.call(null,3,4); // null,3,4
fn.apply(undefined,[5,6]); // undefined,5,6
let temp = fn.bind(null,7,8); // null,7,8
temp();

// 非嚴格模式
function fn(para1,para2){
  console.log(this,para1,para2);
}

fn.call(null,3,4); // window,3,4
fn.apply(undefined,[5,6]); // window,5,6
let temp = fn.bind(null,7,8); // window,7,8
temp();
```

### 實際應用場景
1. 我們在取 callBack Function 的 this 時候，都會拿不到正確的 this。

```jsx
var vm = "全域";

var family = {
  vm: "小明",
  callName: function () {
    console.log('1',this); 
    // 其呼叫方式的是直接在全域下呼叫，所以不管所定義的位置在哪裡，都會指向全域
    setTimeout(function () {
      console.log(this,this.vm); // 全域
    }, 1000);
  },
};
family.callName();
```

1. 過往作法，是在外層直接指定 `const self = this`

```jsx
var vm = "全域";
var family = {
  vm: "小明",
  callName: function () {
    const self = this;
    console.log('1',self ); 
    setTimeout(function () {
      console.log(self,self.vm); // 小明
    }, 1000);
  },
};
family.callName();

```
1. 直接使用 bind 綁定

```jsx
var vm = "全域";

var family = {
  vm: "小明",
  callName: function () {
    console.log('1',this); 
    setTimeout(function () {
      console.log(this,this.vm); // 小明
    }.bind(this), 1000);
  },
};
family.callName();
```
