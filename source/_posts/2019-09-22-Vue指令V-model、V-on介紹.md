---
title: Vue指令 V-model、V-on介紹
date: 2019-09-22 13:27:43
tags:
   - vue 
   - ironman
categories:
   - vue
---
## V-model (資料雙向綁定)
參考資料：
[官網表單輸入綁定介紹](https://cn.vuejs.org/v2/guide/forms.html)
[Ch2課堂基礎範本](https://jsbin.com/bafayot/12/edit?html,output)
[參考資料：Summer— data、v-model 與雙向綁定](https://cythilya.github.io/2017/04/14/vue-data-v-model/)
<!-- more -->
- - - -
用途：綁定雙向資料，主要用在四個地方：`<input>`、`<select>`、`<textarea>`、自訂components。`v-model`本質負責監聽用戶的輸入事件以更新數據。
備註：
> 1.V-model會忽略所有表單元素的value、checked、selected的初始值，請記得一定要在data中聲明初始值  
> 2.V-model跟html結構上標籤（如：selected）同時出現時，V-model權重比較高，會優先顯示data中的資料  
### 常見用法介紹
我們直接來看例子吧. [課堂練習範本](https://codepen.io/chunwen/pen/oKMjBx?editors=1010#0)
```html
情境一：單行文字
<input type="text" v-model="message">
<p>Message is {{message}}</p>

情境二：多行文字
<textarea name="" id="" v-model="message"></textarea>
<p>Message is {{message}}</p>

情境三：checkbox
單選
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
複選
<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>
<input type="checkbox" id="john" value="John" v-model="checkedNames">

情境四：radio
<input type="radio" id="one" value="One" v-model="picked">
<label for="one">One</label>
<br>
<input type="radio" id="two" value="Two" v-model="picked">
<label for="two">Two</label>
<br>
<span>Picked: {{ picked }}</span>

情境五：select
單選(傳統寫法)
<select name="" id="" v-model="selected">
<option disabled value="">請選擇</option>
<option value="小美">小美</option>
<option value="可愛小妞">可愛小妞</option>
</select>
<p>小明喜歡的女生是 {{ selected }}。</p>

單選（用v-for製做）
<select name="" id="" v-model="selected2">
<option disabled value="">請選擇</option>
<option v-bind:value="item" 
v-for="item in selectData ">{{item}}
</option>  

//說明：v-model過去綁定通常為靜態，若想改為動態綁定。可以使用v-bind語法來動態綁定
</select>
<p>小明喜歡的女生是 {{ selected2 }}。</p>

複選（只要加multipe就可以～）
<select v-model="multiSelected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<br>
<span>Selected: {{ multiSelected }}</span>

情境六：checkbox值綁定
<div class="form-check">
<input type="checkbox" class="form-check-input" id="sex" v-model="sex" true-value="男生" false-value="女生">
<label class="form-check-label" for="sex">{{ sex }}</label>
</div>
//說明：這用法挺特別，可以留意一下：true-value、false-value

```
參考資料：[Day10 vue.js - v-model 雙向綁定 (2)](https://ithelp.ithome.com.tw/articles/10214919)

Data 格式
```javascript
data:{
  message:'',
  checked:false, 
  checkedNames:[],
  picked: '',
  selected:'',
  selectData: ['小美', '可愛小妞', '漂亮阿姨'],
  selected2: '',
  multiSelected：[],
  sex：'男生',
}
```
### 修飾符（Modifiers）
```html
情境一：lazy（輸入文字不會及時更新）
<input type="text" class="form-control" v-model.lazy="lazyMsg">

情境二：number(轉為純數字)
<pre>{{ age }}</pre>
<pre>{{typeof(age)}}</pre> //string
<input type="number" class="form-control" v-model.number="age">

情境三： trim，刪除前後多餘空白       
<input type="text" class="form-control" v-model.trim="trimMsg">


資料結構：
lazyMsg: '',
age: '',
trimMsg: ''
```

## V-on事件
參考資料：
[官網文件說明](https://cn.vuejs.org/v2/guide/events.html)
[好文推薦：DOM 的事件傳遞機制：捕獲與冒泡](https://blog.techbridge.cc/2017/07/15/javascript-event-propagation/)
- - - -
v-on用途：監聽DOM事件，並執行JavaScript程式碼運行
寫法： `v-on:[事件名] 如 v-on:click=''`
縮寫：`@click=''`
事件名：如click事件(可以使用原來JS事件來撰寫）
> 備註：JS原生事件如change、close、dblclick、focus、blur都可以綁定，但必須注意這些只能監聽原生DOM事件，而用在自定義元素上時，也可以監聽子組件觸發的**自定義事件** [官網API說明](https://cn.vuejs.org/v2/api/#v-on)  

HTML結構 [練習檔案](https://codepen.io/chunwen/pen/gVjoWQ?editors=1011)
```html
情境一：基礎用法
<p>請切換下方 box 的 className</p>
<div class="box" :class="{'rotate': isRotate }"></div>
<hr>
<button class="btn btn-outline-primary" @click="changeRotate">切換 box 樣式</button>

情境二：帶入參數(很重要，表格排序作業有使用到)
<li v-for="item in arrayData" class="my-2">
{{ item.name }} 有 {{ item.cash }} 元

<button class="btn btn-sm btn-outline-primary" @click="storeMoney(item)">儲值</button>
</li>
說明：這邊的storeMoney(item)，參數item會傳入methods中

情境三：事件修飾符(記得把console.log打開來看結果)
常見的如.stop、.prevent、.capture、.self等等
<h6 class="mt-3">事件偵聽器時使用 self 模式</h6>
<div class="p-3 bg-primary" @click.self="trigger('div')">
<button class="btn btn-outline-secondary" @click.self="trigger('button')">按我</button>
</span>
</div>

情境四：按鍵修飾符
共有三種種類
1. {keyCode | keyAlias} - 事件是從特定鍵觸發時才觸發回調
2. 別名修飾 - .enter, .tab, .delete, .esc, .space, .up等
3. 組合修飾符，實現僅在按下相應按鍵時才觸發鼠標或鍵盤事件的監聽器 - .ctrl, .alt, .shift, .meta

<h6 class="mt-3">別名修飾</h6>
<input type="text" class="form-control" v-model="text" @keyup.space="trigger('space')">


情境五：滑鼠事件
.left .right .middle
<div class="p-3 bg-primary">
<span class="box" @click.middle="trigger('Right button')">
</span>
</div>

```
JavaScript結構
```javascript
data:{
    isRotate: false,
    text: '',
},
methods: {
    changeRotate: function() {
      this.isRotate = !this.isRotate;
    },
    storeMoney: function(item) {
      item.cash = item.cash + 500;
    },
    trigger: function(name) {
      console.log(name, '此事件被觸發了')
    }
  }

```

### 問題紀錄：
> Q.官網上有介紹v-on相關用法，我對於id=“example-2”這個例子中這段語法有些疑惑 [連結](https://cn.vuejs.org/v2/guide/events.html#%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E6%96%B9%E6%B3%95)   
```javascript
if (event) {
alert(event.target.tagName)
}
//If（）中不是應該放可以判斷true或false的內容，而這邊放event是什麼意思？
```
A：if ( ) 除了判斷式也可傳入 JavaScript 的所有型別， 這部份屬於真值與假值的概念，之前在Kuro大大文章中有提到這個概念[重新認識JavaScript:Boolean的真假判斷](https://ithelp.ithome.com.tw/articles/10191343) 或直接參考[ＭＤＮ介紹](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)

### 補充this使用時機
1.methods, computed, created, watch 等 Vue 內的方法都是指向同一個 this也就是 Vue 的實例（instance）
2.若使用到處理陣列方法如；filter、forEach、map等等，則需要另外撰寫 `vm = this` 。若沒有使用到這些陣列處理方法，則可以直接使用this
3.data中的資料都`不需要另外撰寫this`，vue會自動讀取資訊如
`data: { isRotate: false,}`
