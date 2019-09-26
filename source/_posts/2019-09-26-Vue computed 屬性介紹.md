---
title: Vue computed 屬性介紹
date: 2019-09-26 22:48:20
tags:
   - vue 
   - ironman
categories:
   - vue
---

參考資料：
[Vue.js Core 30天屠龍記(第5天)](https://ithelp.ithome.com.tw/articles/10218592)
[官網計算屬性和偵聽器介紹](https://cn.vuejs.org/v2/guide/computed.html#%E4%BE%A6%E5%90%AC%E5%99%A8)
   
<!-- more -->
## 前言
開始前，我們先幫大家複習一下，這幾天介紹的內容（如下圖），若對於指令語法仍有疑問。大家可以自行到官網參考指令介紹喔！[連結提供](https://cn.vuejs.org/v2/api/index.html#%E6%8C%87%E4%BB%A4)
![](https://i.imgur.com/q51LoQ1.png)

-----
開始今天主題介紹前，還記得我們在之文章說過`Vue的Mustache語法嗎？`若還不太清楚可以參考這篇文章[Day5 Vue模板語法、V-text、V-html、V-once介紹](https://ithelp.ithome.com.tw/articles/10218592)
### Mustache語法
簡述：我們可以在HTML上撰寫兩個大括號，就可以很方便的將`實體內資料`綁定到畫面上。但是 `Mustache語法本質上是用於簡單運算。`

我們若遇到需要較為複雜的邏輯運算時候，這時候又全都寫在HTML上，便會造成程式難以閱讀和管理。
官網範例如下：
```html
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```

因此，為了解決複雜的邏輯運算問題，我們需要使用`computed屬性`來幫我們解決問題！

### Computed
用途：主要用來處理複雜邏輯運算。如：資料計算
寫法：`{ [key: string]: Function | { get: Function, set: Function } }`
寫法範例如下：
```javascript
computed: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    }
  }
```
特性：
1.computed 底下宣告的方法必須是function，且會`return`一個值。
2.computed沒有參數可以帶，預設為一個唯獨屬性（預設僅有getter）

範例：
[練習連結](https://jsbin.com/xeselayajo/3/edit?html,js,output)
HTML部分
```html
<div id="app">
    <input type="text" v-model="message">
    <p> Original message: "{{ message }}"</p>
    <p> Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```
JavaScript部分
```javascript
var vm = new Vue({
      el: '#app',
      data: {
        message: 'Hello chunwen!'
      },
      computed: {
        // a computed getter
        reversedMessage: function () {
          // `this` points to the vm instance
          return this.message.split('').reverse().join('')
        }
      }
    });
```

### Computed屬性：getter(讀取)、setter(寫入)
上面特性有提到，`computed`屬性中預設為`getter(讀取)`，但如果我們今天想要針對Computed運算出來的結果進行更動的話，該怎麼處理呢？
我們先來看原始範例（沒有setter）：
[練習連結](https://codepen.io/chunwen/pen/WNeWxPO?editors=1011)
HTML部分
```html
<div id="app">
    <div>firstName: <input v-model="firstName" type="text"></div>
    <div>lastName: <input v-model="lastName" type="text"></div>
    <div>fullName: <input type="text" v-model="fullName"></div>
</div>
```
JS部分
```javascript
var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'chunwen',
        lastName: 'YU'
      },
      computed:{
        fullName(){
          return this.firstName +' '+ this.lastName;
        }
      },
});
```
說明：你可以試著更動`fullName`欄位，這時你會發現`firstName`跟`lastName`這兩個欄位值並不會更動，這時候你可能會好奇我們不是用v-model綁定實體內資料了嗎？為何畫面資料沒有進行更動呢？
並且跳出下面圖片錯誤
![](https://i.imgur.com/0oBItbW.png)
> 原因：就是因為Computed預設為一個唯獨屬性（僅有getter）

如果我們想要針對Computed運算出來的結果進行更動的話，我們可以將上面範例加入`setter屬性`，改寫範例如下：
[連結](https://codepen.io/chunwen/pen/ExYJgPJ?editors=1011)
HTML部分
```html
<div id="app">
    <div>firstName: <input v-model="firstName" type="text"></div>
    <div>lastName: <input v-model="lastName" type="text"></div>
    <div>fullName: <input type="text" v-model="fullName"></div>
</div>
```
JS部分
```javascript
   computed:{
        fullName:{
        //getter
        get(){
          return this.firstName +' '+ this.lastName;
        },
        //setter
        set(val){
          console.log(val)  //觀察更新數值
          var name = val.split(' '); //將數值切分成兩部分
          this.firstName=name[0];
          this.lastName=name[1];          
        }
        }
      },
```
這時我們Computed出來的資料就可以進行變動摟～