---
title: Vue Component(元件) is動態切換元件
tags:
  - vue
  - ironman
  - component
categories:
  - vue
abbrlink: 3284328793
date: 2019-10-08 21:41:16
---
參考資料
- [官網動態組件介紹](https://cn.vuejs.org/v2/guide/components.html#%E5%8A%A8%E6%80%81%E7%BB%84%E4%BB%B6)
- 五倍紅寶石課程資料
<!-- more -->
-----

### is動態切換元件介紹
用途：最常使用在頁籤切換！
寫法介紹：在元件（component）上，或是HTML標籤上`添加:is屬性`
寫法如下：
```javascript
<component:is="currentView"></component>
<div :is="currentView"></div>
```
> currentView的種類有兩種
1.已註冊組件的名字
2.元件中的選項對象（a component’s options object）附上[範例連結](https://jsfiddle.net/chrisvfritz/b2qj69o1/)

> 說明：`is屬性`只要放在HTML標籤上或是component元件上都是可以的，需要特別注意特定標籤如 `<li>` 、`<tr>`、 `<option> `這類有特別限制上層 DOM 元素必須要是哪幾種的，像 <li> 的外層就只能是 <ol> 或 <ul> 等需要小心。[官網連結](https://cn.vuejs.org/v2/guide/components.html#%E8%A7%A3%E6%9E%90-DOM-%E6%A8%A1%E6%9D%BF%E6%97%B6%E7%9A%84%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)

#### 練習範例：
[練習連結](https://codepen.io/chunwen/pen/mdbPMOa?editors=1010)
HTML部分
```html
<h2 class="mt-3">使用 is 動態切換組件</h2>
    <ul class="nav nav-pills">
      <li class="nav-item">
        <a class="nav-link" 
        href="#"
        :class="{'active': current == 'primary-component'}"   @click.prevent="current = 'primary-component'">藍色元件</a>
      </li>
      <li class="nav-item">
        <a class="nav-link"
        href="#"
        :class="{'active': current == 'danger-component'}"    @click.prevent="current = 'danger-component'">紅色元件</a>
      </li>
    </ul>
    <div class="mt-3">
      <component :is="current" :data="item"></component>
    </div>

```
JavaScript部分
```javascript
Vue.component("primary-component", {
  props: ["data"],
  template: "#primaryComponent"
});
Vue.component("danger-component", {
  props: ["data"],
  template: "#dangerComponent"
});

var app = new Vue({
  el: "#app",
  data: {
    item: {
      header: "這裡是 header",
      title: "這裡是 title",
      text:
        "Lorem ipsum dolor sit amet"
    },
    current: "primary-component"
  }
});
```
圖解：
![https://ithelp.ithome.com.tw/upload/images/20191008/20114645lUXPOkz0vC.png](https://ithelp.ithome.com.tw/upload/images/20191008/20114645lUXPOkz0vC.png)

### keep-alive與元件
當我們透過`<component>`加上`:is屬性`來切換元件時，原本元件內的狀態不會保留，如果我們這時候需要保留就要透過 `<keep-alive></keep-alive>`來為元件保留內部狀態。
[練習連結](https://jsbin.com/nekapeq/1/edit?html,js,console,output)
HTML部分
```html
<div class="left">
    <button @click="currentView = 'channel-1'">Channel 1</button>
    <button @click="currentView = 'channel-2'">Channel 2</button>
    <button @click="currentView = 'channel-3'">Channel 3</button>
  </div>
  <div class="right">
     <keep-alive>
      <component :is="currentView"></component>
     </keep-alive>
  </div>

```
示意圖：
![](https://media.giphy.com/media/iDV04Gg8f9PfZzHpMV/giphy.gif)


