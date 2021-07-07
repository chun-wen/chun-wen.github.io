---
title: '2021-07-07-[筆記]JavaScript 原型'
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 1656466032
---
前言：
主要就紀錄一下目前 JavaScript 常用，但自己又不熟悉的筆記。

<!-- more -->
---
參考資料：
[Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)
[該來理解 JavaScript 的原型鍊了](https://github.com/aszx87410/blog/issues/18)

---
### 緣由
要理解 `JavaScript` 原型必須先了解一下 `JavaScript` 發展史。Brendan 為了讓 JavaScript 有繼承機制，因此想到透過調用 Constructor 來設計。註記：`JavaScript` 沒有 `Class` 概念！

```jsx
//建構函數
function Car(name){
   console.log(this); //物件實體
   this.name = name;
}
           //透過 new 創造物件實體
var Temp = new Car("Lexus");
```

但是透過 new 方法，所創造的物件實體。裡面的屬性跟方法是不能共用的。

```jsx
function Car(name){
   console.log(this); //物件實體
   this.name = name;
   this.price = 10000;
}

var Temp = new Car("Lexus");
var TempB = new Car("BMW");

Temp.price = 200000;
console.log(TempB.price, Temp.price);
```

因此，才有了 prototype 的概念！

```jsx
function Car(name){
   this.name = name;
   this.price = 10000;
}
Car.prototype = { color: 'red' }

var Temp = new Car("Lexus");
var TempB = new Car("BMW");

console.log(TempB.color, Temp.color);
```

### 正題
基本上 JavaScript 都是物件，我們可以拿 `Array` 來舉例。

```jsx
let array = [1,2,4];
console.log(array); //如下面附圖
```
![圖片](https://i.imgur.com/T40BQrn.png)
既然他嚴格來說也算物件，那當然也可以用物件方法來建立屬性或方法。

```jsx
let array = [1,2,4];

array.name = "Andy";
console.log(array); 
```

而何謂原型鏈呢？
> 物件會透過 `__proto__` 一直往上尋找物件，直到最上層！一直往上尋找的過程就是指原型鏈！直到最上層為 `Null`  為止

### 名詞解釋
**prototype** 
- 前者是函式上的屬性
**__proto__**
- 後者是物件上的屬性