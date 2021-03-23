---
title: Vue Component(元件)-props.sync 溝通方式
tags:
  - vue
  - ironman
  - component
categories:
  - vue
abbrlink: 1846504743
date: 2019-10-06 17:08:12
---

參考資料
- 五倍紅寶石實體課程
- [[Vue]使用 props.async 同步父子組件之間的傳值](https://medium.com/%E4%B8%80%E5%80%8B%E5%B0%8F%E5%B0%8F%E5%B7%A5%E7%A8%8B%E5%B8%AB%E7%9A%84%E9%9A%A8%E6%89%8B%E7%AD%86%E8%A8%98/vue-%E4%BD%BF%E7%94%A8-props-async-%E5%90%8C%E6%AD%A5%E7%88%B6%E5%AD%90%E7%B5%84%E5%BB%BA%E4%B9%8B%E9%96%93%E7%9A%84%E5%82%B3%E5%80%BC-f7b1d3007836)
- [官網自定義修飾子](https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-%E4%BF%AE%E9%A5%B0%E7%AC%A6)
- [Vue.js Core 30天屠龍記(第26天): 客製事件](https://ithelp.ithome.com.tw/articles/10209183)
<!-- more -->
-----

### .sync VS props、emit
接下來，將透過兩組範例比較，來讓大家知道這兩種元件傳遞的方式差異在哪。

#### props、emit範例
[範例連結](https://jsbin.com/huliyem/3/edit?html,js,output)
HTML部分
```html
<div id="app">
  <p>Parent: {{ message }}<input v-model="message"></p>
  <hr>
  Child:
  <my-component :parent-message="message" @update="selfUpdate"></my-component>
    </p>
  </div>
```
寫法說明：我們會在子元件上註冊一個自定義`update事件`，當子元件update事件觸發時，則會同時觸發父元件`selfUpdate事件`
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
畫面如下
![](https://media.giphy.com/media/Qu7Lk3AqZhPJEotVNH/giphy.gif)

-----


#### .sync範例
[範例連結](https://jsbin.com/wupidon/edit?html,js,console,output)
HTML部分
```html
<div id="app">
      <p>Parent: {{ message }}<input v-model="message"></p>
      <hr>
      Child:
      <my-component :parent-message.sync="message"></my-component>
```
寫法說明：我們可以發現到我們將child元件上的自定義事件移除了，改用`:parent-message.sync="message"綁定`

JavaScript部分
```javascript
Vue.component('my-component', {
      template: `<div>
                  {{ synMsg }}
                  <input v-model="synMsg">
                </div>`,
      props: {
        parentMessage: String
      },
      computed:{
        synMsg:{
          get(){
            return this.parentMessage
          },
          set(val){
            this.$emit('update:parentMessage',val)
          }
        }
      }
    });

    new Vue({
      el: '#app',
      data: {
        message: 'hello'
      }
    });

```
寫法說明：
1.原本在子元件中用`methods來觸發事件`，但使用語法糖後改用computed屬性來進行同步
2.並且把new Vue實體中的methods方法也移除

畫面如下：
![](https://media.giphy.com/media/RfAUBaqtHDDNT5kmPS/giphy.gif)

### 小結論
OK，我們介紹完.sync 修飾符的使用方法，我們來聊聊為何會稱`.sync`為語法糖

從.sync範例中，我們依然可以發現父層元件，依舊透過props將父層資料`message`傳遞進來子元件。而在元件中，我們依然透過`this.$emit`來觸發事件，達到外層資料也同步更新的目的。

這其中最大的差別就是在於，父層元件中 `parent-message.sync` 其實是
```html
v-bind:parent-message=”message” v-on:update:parentMessage=”parentMessage = $event”
``` 
的縮寫。


