---
title: Vue Component溝通（$parent、$children）
date: 2019-10-05 19:08:42
tags:
   - vue 
   - ironman
   - component
categories:
   - vue
---
參考資料
- [Vue元件間通訊6種方式](https://www.itread01.com/content/1558210804.html)
- 五倍紅寶石實體課程講義
<!-- more -->
-----

### $parent功能介紹
子元件可以透過this.$parent，來存取父層組件。這種方法用起來就是爽XD，不用在子元件中發送$emit事件，來呼叫父元件。
使用時機：通常使用情境都是在debug上，開發上還是不建議透過子元素來覆寫父層元素。
> 原因：直接透過子元素來覆寫父層元素，`會造成父元件跟子元件耦合過深重`，日後無法單獨把這個子元件拉出來使用。

#### 範例
[連結](https://jsbin.com/bijifaf/1/edit?html,js,output)
HTML部分
```html
<div id="app">
    <my-component  ref="comp1" :parent-msg="msg"></my-component>
</div>
```
JavaScript部分
```javascript
Vue.component('my-component',{
  template:`<div>{{parentMsg}}</div>`,
  props: ["parentMsg"],
  mounted(){
    console.log("$parent",this.$parent.msg);
    
    window.setTimeout(() =>{
          this.$parent.msg="Hello"
    },2000)
  },
})


new Vue({
  el:'#app',
  data:{
    msg:'Msg of Parent'
  }
})
```
說明：我們在兩秒過後，把父層msg`Msg of Parent`，更改為`Hello`


### $children功能介紹
父元件可以透過this.$children，來存取子組件（陣列）。至於為何是陣列，我們可以來複習一下這張圖。圖片中可以發現每個子元件都只會有一個父元素，但是父元素就不同摟，他可能會有`0~無限個子元素。`這也就是為何取出來是陣列原因！
![https://ithelp.ithome.com.tw/upload/images/20191005/20114645rgdC9oRL7N.png](https://ithelp.ithome.com.tw/upload/images/20191005/20114645rgdC9oRL7N.png)

### ref功能介紹
為了不讓`v-if`影響子元件顯示順序，我們可以透過幫子組件設定別名ref，來確保組件順序不受影響。
#### 範例
[練習連結](https://codepen.io/chunwen/pen/oNNNYWR?editors=1011)
HTML部分
```html
<div id="app">
    <my-component2 ref="comp2"></my-component2>
    <my-component3 ref="comp3"></my-component3>

    <hr>
    <div> {{ msg }}</div>
  </div>

```
JavaScript部分
```javascript
    new Vue({
      el: '#app',
      data: {
        msg: 'Msg of Parent!'
      },
      mounted() {
        console.log(this.$children[0]) // VueComponent，my-component3
        console.log('$children2: ', this.$refs.comp2.msg);   //Hi COMP2
        console.log('$children3: ', this.$refs.comp3.msg);  //Hi COMP3
      }
    });
```
