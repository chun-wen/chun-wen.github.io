---
title: Vue Component(元件) props、emit介紹
date: 2019-10-02 21:06:00
tags:
   - vue 
   - ironman
   - component
categories:
   - vue
---
參考資料
- [Vue.js Core 30天屠龍記(第23天): props 屬性](https://ithelp.ithome.com.tw/articles/10208500)
- [官網監聽子組件事件](https://cn.vuejs.org/v2/guide/components.html#%E7%9B%91%E5%90%AC%E5%AD%90%E7%BB%84%E4%BB%B6%E4%BA%8B%E4%BB%B6)
<!-- more -->
-----
### 元件溝通方式
元件與元件之間的溝通方式主要有下面幾種
1.props in, emit out
2.event bus
3.$parent、$children
4.Vuex

我們今天主要會專注在`props`、`emit`這一種最常用的方式做介紹，而其餘內容將在日後慢慢介紹。

### props介紹與使用
- 用途：父層元件若要將內容傳遞進去子層元件就需要用到`props`這個屬性。
- 寫法：`v-bind:props-in="msg"`，其中，`props-in`是自定義屬性、`msg`則會去實體內尋找
命名注意：HTML 屬性需要使用 kebab-case ，全小寫並使用分隔符號( - )來設定 
如：`props-in`  [參考資料](https://ithelp.ithome.com.tw/articles/10208500)
- 為何需要props屬性？
還記得，我們昨天有提到元件內的data必須是function型式，確保每個子元件資料的獨立性嗎？正因為這樣，我們也不能透過父元件直接修改子元件內容，因此父元件才需要用到`props`這個屬性，來將外層資料傳遞進去子元件中。

-----

範例：[練習連結](https://jsbin.com/hacuvam/edit?html,js,output)
HTML部分
```html
<div id="app">
    <h1>{{msg}}</h1>  //取得實體內資料：Msg of Parent!
    <hr>
    <my-component v-bind:parent-msg="msg"></my-component>  
    //透過自定義屬性：`parent-msg`，將實體內資料：Msg of Parent!傳入元件中
</div>
```
JavaScript部分
```html
 //x-template
 <script type="text/x-template" id="my-component">
    <div class="component">
      <div> ParentMsg: {{ parentMsg }} </div>   
      <div> ChildMsg: {{ msg }} </div>      
    </div>
  </script>
```
JavaScript部分
```javascript
 //global register
 Vue.component('my-component', {
      props: ["parentMsg"],
      template: '#my-component',
      data: function () {
        return {
          msg: 'Msg of Child!'
        }
      }
    });

    // Vue instance
    new Vue({
      el: '#app',
      data: {
        msg: 'Msg of Parent!'
      }
    });
```
圖解：
![](https://ithelp.ithome.com.tw/upload/images/20191002/20114645VUYYWBJtdi.png)
畫面如下
![](https://ithelp.ithome.com.tw/upload/images/20191002/20114645kiYLRY5ttS.png)

-----

### 利用props傳入靜態屬性、動態屬性
- 靜態傳入寫法：不需要加入v-bind  
寫法：`props-in="靜態傳入"`，會傳入純文字  (註：props-in是自定義名稱)
- 動態傳入寫法：需要加入 v-bind  
寫法：`v-bind:props-in="動態傳入"` 或是 `:props-in="動態傳入"`（註：冒號不能省略)
範例： [練習連結](https://jsbin.com/vaxoder/1/edit?html,js,output)
```html
<div id="app">
    <hr>
    <my-component parent-msg="靜態傳入"></my-component>
    <my-component :parent-msg="msg"></my-component>
  </div>
  <script type="text/x-template" id="my-component">
    <div class="component">
      <div> ParentMsg: {{ parentMsg }} </div>       
    </div>
  </script>
```
圖片如下：
![](https://ithelp.ithome.com.tw/upload/images/20191002/20114645jpkjTWn5Rp.png)


-----
### emit介紹
- 目的：當我們今天子元件內容要將資料傳遞到父元件時，就需要使用`emit`這個屬性。
- 備註：會需要使用emit來觸發外層事件，其實是`props單向資料流關係`，關於這個特性，會在明天介紹props使用注意上再來介紹喔！

範例：[練習連結](https://jsbin.com/huliyem/2/edit?html,js,output)
HTML部分
```html
<div id="app">
    <p>Parent: {{ message }}<input v-model="message"></p>
    <hr>
    <p>
  Child:
  <my-component :parent-message="message" @update="selfUpdate"></my-component>
    </p>
  </div>
```
說明：我們在`my-component`上，自定義一個update事件，當子元件update事件觸發時，則會同時觸發父元件`selfUpdate`事件
JavaScript部分
```javascript
   Vue.component('my-component', {
      template: `<div>
                  {{ parentMessage }}
                  <input v-model="message">
                  <button @click="updateText">Update</button>
                </div>`,
      props: {
        parentMessage: String //字串型別
      },
      data() {
        return {
          message: this.parentMessage
        }
      },
      methods: {
        updateText() {
                      //事件名稱 value
          this.$emit('update', this.message); //this.message是指子層的噢！
        }
      }
    });

    new Vue({
      el: '#app',
      data: {
        message: 'hello'
      },
      methods: {
        selfUpdate(val) {
          this.message = val;
        }
      }
    });
```
圖解說明：
![](https://ithelp.ithome.com.tw/upload/images/20191002/20114645rekb6vUcF9.png)

### 結論
這就是我們常講的`props in, emit out`的由來
![](https://ithelp.ithome.com.tw/upload/images/20191002/20114645maXrfGHfDH.png)
