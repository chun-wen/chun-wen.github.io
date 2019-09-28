---
title: Vue computed VS watch VS method
date: 2019-09-28 10:22:04
tags:
   - vue 
   - ironman
categories:
   - vue
---
參考資料
1.[用範例理解 Vue.js #6：Computed vs Methods](https://ithelp.ithome.com.tw/articles/10191808)
2.[計算屬性緩存vs 方法](https://cn.vuejs.org/v2/guide/computed.html#%E8%AE%A1%E7%AE%97%E5%B1%9E%E6%80%A7%E7%BC%93%E5%AD%98-vs-%E6%96%B9%E6%B3%95)
<!-- more -->
-----
### 第一部分：computed VS watch
OK，我們首先簡單複習一下，這兩者的特性。
Computed:適合用來處理複雜邏輯運算。
Watch:會去監聽特定變數，當變數產生變動時，就會執行某個動作。
範例：
HTML部分
```html
    <div id="app">
    {{ fullName }}
    <br>
    <input type="text" v-model="firstName">
    <br>
    <input type="text" v-model="lastName">
  </div>
```
JavaScript寫法一(使用Watch)
```javascript
var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'chunwen',
        lastName: 'YU',
        // 我們需要手動設定初始值
        fullName: 'chunwen YU'
      },
      watch: {
        // 參數可以自行命名（更新資料,原始資料）
        firstName: function (newValue,rawValue) {
          // console.log('資料:',newVal,rawValue)
          this.fullName = `${newValue} ${this.lastName}`
          console.log(this.fullName)
        },
        lastName: function (newValue) {
          this.fullName = `${this.firstName} ${newValue}`
        },
      },
    });
```
JavaScript寫法二(使用Computed)
```javascript
var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'chunwen',
        lastName: 'YU',
      },
      computed:{
        fullName(){
           return `${this.firstName} ${this.lastName}`
        }
      }
    });
```
#### 小總結
1.我們可以發現使用Computed寫法時，並不需要在`data預先定義好fullName的資料初始值`
2.相對watch而言，computed寫法更為簡便
#### 使用時機
1.`watch`適合用來觀察資料變動
2.如果你的某個變數是依賴其他變數⽽來（如範例：fullName會觀察firstName與LastName），這時候就適合使用`computed`


-----


### 第二部分 computed VS methods()差異
開始前，簡單複習一下methods()特性
會與`v-on`一起使用：主要目的：用來定義內部資料使用的函式方法
範例： [練習連結](https://jsbin.com/sajemotici/1/edit?html,js,console,output)
HTML部分
```html
<div id="app">
    <input type="text" v-model="message">
    <div>reversedMessage: {{ reversedMessage }}</div>
    <div>reversedMessage: {{ reversedMessage }}</div>
    <div>reversedMessage: {{ reversedMessage }}</div>
   
    <hr>
    <div>reversedMessage_method(): {{ reversedMessage_method() }}</div>
    <div>reversedMessage_method(): {{ reversedMessage_method() }}</div>
    <div>reversedMessage_method(): {{ reversedMessage_method() }}</div>
  </div>
```
JavaScript部分
```javascript
 var vm = new Vue({
      el: '#app',
      data: {
        message: 'Hello 5xRuby!'
      },
      methods: {
        reversedMessage_method:function() {
          console.log('methods');
          return this.message.split('').reverse().join('');
        }
      },
      computed: {
        reversedMessage: function () {
          console.log('computed');
          return this.message.split('').reverse().join('');
        }
      }
    });
```
執行結果如下
![](https://ithelp.ithome.com.tw/upload/images/20190928/20114645QxxRA0Yrjt.png)
#### 小結論
我們從圖片中觀看這兩者運行結果，的確一樣。但是，我們打開console.log後，就可以發現只要資料一進行跟動methods()就會執行一次，但computed卻不會。`這也就是為何我們要HTML要寫三次的原因`~~(Kuro老師說重要的事情要講三次XD)~~

> 1.computed會將data中的資料進行cache緩存，當資料變動時候再一起更動
> 2.Method則會在data改變時候，直接進行更動。缺點：需要耗費較高效能

### 總結：methods、computed、watch使用時機
1.methods: 這是需要主動觸發，且可以多次重複觸發
2.Computed: 當資料需要複雜運算時
3.Watch: 監控特定資料變化的 function 就放這裡

