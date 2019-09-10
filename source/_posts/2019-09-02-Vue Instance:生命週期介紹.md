---
title: Vue Instance/生命週期介紹
date: 
tags:
   - vue 
categories:
   - vue
---


參考資料：
[Summer-Vue Instance介紹](https://cythilya.github.io/2017/04/11/vue-instance/)
- - - -
## Vue Instance(實體)
每個 Vue.js 的應用程式都是從`Vue建構式 (vue constructor) `建立`根實體 (root vue instance) `開始，再一個個將元件搭建上去而來的。
* Vue的實體是透過`new`關鍵字來建立

<!-- more -->

### 建立Vue Instance
使用 vue constructor 建立 vue instance「vm」，vm 為 view model 的簡稱
```javascript
var vm = new Vue({
    //option object
});
```
### 建立Vue Instance寫法2
```javascript
new Vue({
  el: '#app',
  data() {
    return {
      isShowing: false 
    }
});
```
#### 小結論
兩者寫法都是可行，差異僅在於`是否賦予一個值到變數上`，而這個變數是可以用來以後取值使用。老師也說到後面章節（Vue Cli）會比較多時後使用寫法2。原因就是不太需要使用該變數做任何操作
補充：同一個頁面上`可以建立兩個以上的Vue實體`在是沒有問題，只有巢狀會出錯

## Vue實體基本屬性(43分40秒開始)
![](https://i.imgur.com/EEJQMXF.png)圖片來源：五倍紅寶石Vue實戰課程
### el&data
* el：就是用來綁定網頁dom元素與Vue實體可以控制的範圍的`媒介`
> 但，當實體沒有el屬性，就只能透過`vm.$mount()`來進行手動掛載  
> 備註：  
> 1.這用法很少用，所以知道就好 [文章參考](https://kknews.cc/code/eykopbz.html)  
> 2.vm是指上面圖片宣告的變數（這邊是可以自定義）  
* Data: 用來存放實體綁定的資料
實體內：透過this.XXX 取得資料
實體外：透過Hello.$data.value 取得資料  ` Hello這個變數是可以自行命名`
>實體外指的就是下方Hello實體物件範圍外
在子元件內時，須以 **function**的形式來來回傳。 
```javascript
var Hello = new Vue({
      el: '#app',
      data: {
        value: 'Hi Vue!'
      }
    });
Hello.$mount().value  //"Hi Vue!"
```
> 備註：Data內屬性不可由＄或＿開頭 如：$abc、＿abc  

### 傳入選項物件
當實體（Vue instance）被創建後，物件可以傳入包含el、data、methods、watch、mounted、props、computed
```javascript
var vm = new Vue({
    el: '#app',
    data: {
    message:"hello vue.js!"
     },
    methods:{ //略    
}
});

```
### 擴充建構式
```javascript
var component = Vue.extend({
    data: function(){
    return{ 
     message:'hello '
     }
   },
});
var cp = new component();
console.log(cp.message) //hello
```
> data選項，需要注意`在Vue.extend()中它必須是函數`  

## Vue 元件實體生命週期(Instance Lifecycle Hooks)
Vue.js 提供實體生命週期鉤子 (instance lifecycle hooks)，讓我們在 instance 不同時期做一些事情。示意圖如下 [完整版請參考官網](https://cn.vuejs.org/v2/guide/instance.html#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE%E7%A4%BA)
![](https://i.imgur.com/7PMY4RZ.png)
### Vue生命週期hooks 說明：
![](https://i.imgur.com/bYvFdBi.png)
圖片來源：五倍紅寶石Vue實戰課程
### Vue執行順序：
![](https://i.imgur.com/XoDkgjK.png)
圖片來源：五倍紅寶石Vue實戰課程
補充：
> Q1：vm.$mount() 圖片中`vm`指的是我們自行命名變數？**對**  
> Q2：如果要透過 ajax / fetch 取得 API 回傳資料交給 Vue.js 處 理理時，應該在哪個階段執⾏？  
> Ａ：created階段之後都ok(包括created、beforeMount 與 mounted)，因為元件實體已經被建立，我們可以取得data資料。老師建議放created階段，不建議在放在mounted 因為資料若為空陣列網頁畫面可能會有一段空白，但可以用loading圖蓋過. [六角問答](https://www.udemy.com/vue-hexschool/learn/lecture/10271478#questions/7853862)  

###  Lifecycle hook functions 使用
引用Summer部落格上內容[Summer-Vue Instance介紹](https://cythilya.github.io/2017/04/11/vue-instance/)
```javascript
var vm = new Vue({
  beforeCreate: function() {
    //vue instance 被 constructor 建立前
    console.log('beforeCreate');
  },
  created: function() {
    //vue instance 被 constructor 建立後，在這裡完成 data binding
    console.log('created');
  },
  beforeMount: function() {
    //綁定 DOM 之前
    console.log('beforeMount');
  },
  mounted: function() {
    //綁定 DOM 之後
    console.log('mounted');
  },
  beforeUpdate: function() {
    //資料更新，但尚未更新 DOM
    console.log('beforeUpdate');
  },
  updated: function() {
    //因資料更新，而更新 DOM
    console.log('updated');
  },
  beforeDestroy: function() {
    //移除 vue instance 之前
    console.log('beforeDestroy');
  },
  destroyed: function() {
    //移除 vue instance 之後
    console.log('destroyed');
  }
});

```

### 保留 `keep-alive` 才會跳出來下面alert
```javascript
activated () {
    alert(`activated! ${this.text}`);
  },
  deactivated () {
    alert(`deactivated! ${this.text}`);
  },
```





