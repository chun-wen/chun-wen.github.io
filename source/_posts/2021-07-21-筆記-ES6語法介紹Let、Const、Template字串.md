---
title: '2021-07-21-[筆記]ES6語法介紹Let、Const、Template字串'
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 2208843976
---
前言：
一種語法的出現通常就是為了解決目前現有的問題，而 `ES6` 語法的出現就是要解決 `ES5` 語法上的一些毛病。如全域變數污染問題。
在 `ES5` 以前 變數作用域是以 function 為切割， ES6 後則改為 `{}` 區塊切分。

<!-- more -->
---
參考資料：

[ECMAScript 6 入門電子書](http://es6.ruanyifeng.com/#docs/let#const-%E5%91%BD%E4%BB%A4) 

[Day15-淺談JS版本差異！ES5、ES6](https://ithelp.ithome.com.tw/articles/10206587) [Day26 var 與 ES6 let const 差異](https://ithelp.ithome.com.tw/articles/10209121) 

[Day 05: ES6篇 - let與const](https://ithelp.ithome.com.tw/articles/10185142) 

[ES6 開始的新生活 let, const](https://ithelp.ithome.com.tw/articles/10192432) 

[筆記JavaScript ES6 中使用block-scoped 的 let 宣告變數](https://pjchender.blogspot.com/2017/01/es6-let.html)

---
開始前我們簡單來看一下全域變數值被改變的例子：

```jsx
for(var i = 0 ; i < 3 ; i++) {
   setTimeout(function(){
      console.log("執行第" + i + "次");
   },0);
}
//這邊的變數i 已經是全域變數，我們在 chrome上輸入 window.1 觀察可以發現i=3
.
.
.
.

var i =7;
console.log('2',i);
//如果程式碼後面又有更改 i 的值 就會影響到 i 的值
```

下面我們就來介紹常用ES6語法吧！ 

## 語法特性(下面三點 Let、Const 都適用)
1. 塊級區域（block scope） 

2. 變量不會提升（沒有hoisting效果） 

3. 不允許重複宣告 

### Let 語法(變數宣告)
首先，我們來看一下我們過往宣告變數寫法

```jsx
var name ="Andy";
console.log(name) //Andy
```

新的關鍵字`let`寫法

```jsx
let name="Andy";
console.log(name) //Andy
```

> 我們可以發現上面用法跟過去相似，所以到底let差在哪呢？
讓我們繼續看下去

- 特性1：塊級區域作用域

```jsx
if(true){ 
  var name ="chunwen"; 
}
console.log(name) //chunwen
補充一下：為何console.log可以取值，就是因為 var切分最小單位是 function

if(true){let name ="chunwen"; }
console.log(let);
//let is not defined
// 這邊就可以發現差異了，let僅能在塊級區塊{}內取用
```

> 簡單一句話來說：用 let 所定義的變數只能作用在所屬的 `{ }` 中有效。

- 特性2：不允許重複宣告

```jsx
let name="eddie";
let name="Andy";
console.log(name) //Identifier 'name' has already been declared
```

- 特性3：變量不會提升(無hoisting效果)

其實 `Let` 跟 `Var` 一樣有創造階段，只是 `Var` 在創造階段時會給予一個值 `undefined`
而 `Let` 不會，這是因為 `Let` 有一個稱為暫時性死區的特性（TDZ）

```jsx

console.log(v5); 
let v5 = 5 ;
// Uncaught ReferenceError: Cannot access 'v5' before initialization
```

最後，補充一個實物案例（for迴圈）： 六角JS章節範例

```jsx
<ul class="list">
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>

const listLen = document.querySelectorAll('.list li').length;
for (var i = 0; listLen > i; i++) {
  document.querySelectorAll('.list li')[i].addEventListener('click', function () { alert(i + 1); } )
  //永遠會印出4，因為i是全域變數特性
}
//但如果我們想要印出list中 1、2、3，只要將for迴圈中var改為let就可喔！
```

### Const(常數宣告)
特性：唯讀變數、不能去做修改，除非使用`陣列`或`物件` 
例子：像我們使用AJAX抓取資料來源的url，`不希望url被更動數值`

```jsx
const a =10;
console.log(a) //10 
a=20;
console.log(a) 
//出現下面文字錯誤，原因就是a已經被設定為常數，而不是變數
//Uncaught TypeError: Assignment to constant variable.

此外，使用const一定要賦予值，否則會跳錯
const andy;
console.log(andy);
//Uncaught SyntaxError: Missing initializer in const declaration
```

### Const 在宣告陣列或物件須留意地方

下面寫法不會造成程式碼跳錯： 

這邊之所以不會出錯，引用Ｐ大說法：
[筆記談談JavaScript中by reference和by value的重要觀念](https://pjchender.blogspot.tw/2016/03/javascriptby-referenceby-value.html)

> 在 JS 中陣列（array）和物件（object）都是屬於 reference type，因此實際上我們並沒有把這個常數指向（pointer）另一個東西，它仍然指稱到的是同一個記憶體位置。

```jsx
const arr=["hello","weird world"]
arr.push("goahead")
console.log(arr);  
//["hello", "weird world", "goahead"]
       
const object = { 
   name:"andy", 
   outfit:"nice"
}
object.email = "hsbsbbdn@gmail.com"
console.log(object); 
//{name: "andy", outfit: "nice", email: "hsbsbbdn@gmail.com"}
```

但是，如果使用`object literal` 方式修改物件內容，則會出現錯誤，因為對於對於 JS 引擎來說，就等於是建立了一個新的物件，也就是它會將這個物件存到另一個記憶體位置，意思就是這個常數的值改變了

```jsx
const object = { name: "andy", outfit: "nice" }        
object = { email: "hahahaha@gmail.com" }
console.log(object);  // Uncaught TypeError: Assignment to constant variable
```

### 補充凍結物件（Freeze） 效果：`即使使用非literal object方式`，物件也不能新增、更新、刪除屬性

```jsx
const list=['apple','banana']
const obj = {  name: 'Jack',  favFruits: list,};
const anotherObj = {  name: 'Apple',  avFruits: list,};
Object.freeze(obj);
Object.freeze(obj.favFruits);
list.push('orange'); 
// Uncaught TypeError: Cannot add property 2, object is not extensible
```

### Template 字串寫法
組字串重點在於起手式，`兩個反斜線。 變數必須使用${}`，將變數填入，如下範例：
```jsx
<ul class="list"> </ul>
```

```jsx
const list = document.querySelector('.list');
const picture = 'https://images.unsplash.com/photo-1558980395-be8a5fcb4251?ixlib=rb-1.2.1&auto=format&fit=crop&w=1651&q=80';
const title = "六角學院"
list.innerHTML = `<li>
    <p>${title}</p> <img src="${picture}">
</li>`
```

> 補充：`${ }` 不只可以填入變數也可以加入JS原始碼 如下範例

### 搭配JS函式寫法
```jsx
// 搭配陣列方法map，會回傳一個新的陣列

let jsUrl = `<ul>  
   ${people.map( (person) => {
    `<li>我叫做${ person.name }</li>`
}).join('')}
</ul>`
console.log(jsUrl,teacher);
```

### 撰寫小技巧
1.建議一定要使用emmet功能，加速開發效率 若遇到在html檔案中，想要撰寫javascript時無法用emmet快速產出，則可以參考這篇文章教學。調整`emmet.includeLanguages` 
[文章連結](https://medium.com/harry-xies-blog/%E8%A7%A3%E6%B1%BAvs-code%E4%B8%ADvue%E6%AA%94emmet%E8%AA%9E%E6%B3%95%E5%A4%B1%E6%95%88%E7%9A%84%E6%96%B9%E6%B3%95-5fa0eb5fabd4)