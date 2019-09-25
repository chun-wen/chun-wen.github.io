---
title: Vue指令語法V-if、V-show介紹
date: 2019-09-05 00:40:28
tags:
  - vue
categories:
  - vue
---
[官網資料](https://cn.vuejs.org/v2/guide/conditional.html)
[全部練習範例檔案](https://codepen.io/chunwen/pen/GVQbRB?editors=1010#0)
<!-- more -->
- - - -
## V-if & V-show
用途：條件性地渲染內容。這塊內容只會在`指令的表達式返回truthy值`的時候被渲染。
[練習連結](https://codepen.io/chunwen/pen/OJLqRQZ)
```html
    <h1 v-if="cond1">Yes</h1>
    <h1 v-else>No</h1>
    <hr>
    <h1 v-show="cond1">Yes</h1>

    var vm = new Vue({
      el: '#app',
      data: {
        cond1: true
      }
    });

```

### V-if、V-else切換
```html
<div class="alert alert-success" v-if="isSuccess">成功!</div>
<div class="alert alert-danger"  v-else>失敗!</div>
```
> 備註：V-else元素必須緊跟在帶`v-if`或者`v-else-if`的元素的後面，否則它將不會被識別。  

### 在Template元素上使用`v-if`條件渲染分組
用途：同時綁定多個元素，維護程式碼整潔，且template不會渲染在畫面上。`template 無法與 v-show 共⽤用`
```html
<template v-if="showTemplate">
              <tr>
                <td>1</td>
                <td>安妮</td>
              </tr>
              <tr>
                <td>2</td>
                <td>小明</td>
              </tr>
            </template>
```
### v-else-if切換分頁
```html
<p>使用 v-else-if 做出分頁頁籤</p>
<a class="nav-link" href="#"  @click.prevent="link='a'">標題一</a>
<a class="nav-link" href="#" @click.prevent="link='b'">標題二</a>
<a class="nav-link" href="#" @click.prevent="link='c'">標題三</a>

          <div class="content">
            <!-- 記得要用 邏輯運算子 === 來判斷是否相同  -->
            <!-- ＝是賦予值 -->
            <div v-if="link === 'a'">Ａ</div>
            <div v-else-if="link === 'b'">Ｂ</div>
            <div v-else-if="link === 'c'">Ｃ</div>
          </div>
```

### 用`key`管理可複用的元素
Vue渲染網頁時候，並不會從頭開始渲染而是會複用相同元素，使得載入速度加快。而這時候如果我們想要重新渲染就需要用`key`屬性來添加唯一值
```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="1">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="2">
</template>
```
> 備註：key可以自行命名  
### V-if & V-show差異：
```html
<div class="alert alert-success" v-show="isSuccess">成功!
</div>

<div class="alert alert-danger" v-show="!isSuccess">失敗!</div>

```
說明：
v-if 與 v-show 最大的差別在是否對 `DOM` 操作，`v-if` 會依照條件決定是否將元件渲染⾄至網⾴頁上。
V-show一定會渲染出物件，但是以CSS方式切換顯示與否（display:none），所以當頻繁切換是否顯示時當然使用V-show效能較好。

#### 小結論
結論：
V-if：`操控dom元素`
V-show：`操控display:none`
