---
title: Vue Router介紹
date: 2019-09-20 10:57:22
tags:
  - vue
categories:
  - vue
---
參考資料：
[vue-router的兩種模式的區別](https://juejin.im/post/5a61908c6fb9a01c9064f20a)
[官方文件](https://router.vuejs.org/zh/installation.html)
<!-- more -->
- - - -
Vue Router就是由前端模擬的路由，跟過去不同的是，換頁通常會由後端處理。而Vue Router存在就是為了實現SPA（單頁式應用），當我們切換畫面時候就不需要向後端發出請求。
![](https://i.imgur.com/1eCr3wR.png)
## 安裝方式
一、方法一
1.`npm install vue-router` 
不用寫成這樣`npm install vue-router --save` 
因為，Npm5.0.0版本後，安裝的套件會預設自動加入dependency 
 [連結說明](https://stackoverflow.com/questions/19578796/what-is-the-save-option-for-npm-install)

2.接著在終端機中輸入 `npm run serve `
補充：使用`npm run dev`，會出錯因為`package.json`沒有這行指令
[vue开发----npm run dev 报错：missing script:dev](https://blog.csdn.net/qq_32107121/article/details/84378217)
原因：
`npm run dev`是Vue CLI2指令
`npm run serve`則是Vue CLI3指令 
> 兩者不可以混用喔！  

3.接著要在router.js啟用`Vue.use(VueRouter)`

二、方法二
創建新的檔案時( vue create project)，就直接勾選`Vue router`，Vue就會幫我們直接新增`router.js`

以上兩種方式，都可以安裝Vue Router

## 路由配置介紹
### 組件名詞介紹
`<router-view></router-view>`         呈現路由配置元件
`<router-link></router-link>`         路由路徑
`main.js`           進路點
Vue Components（如：app.vue檔）      分頁內容 

### 路由配置教學
配置路由會在`router.js`、`main.js`、`app.vue`這三個檔案設定
ㄧ、router.js
主要負責處理路由檔案配置管理。
![](https://i.imgur.com/7W3tlCY.png)補充：
1.@是絕對路徑，`src` 目錄的縮寫 
2.export default 是 ES6 的模組匯出概念

二、main.js
Webpack進入點
![](https://i.imgur.com/YIo2sMP.png)
三、app.vue
在這被拿來當作`首頁使用`，若有其他預設首頁可以自行更換
![](https://i.imgur.com/3mnsdwG.png)

### 巢狀路由
寫法其實跟一般路由配置相同，差異點僅在於巢狀路由會新增一個children配置底下分頁路由，以下就由我簡單示範一下。
一、Page.vue檔案：
說明：我們會在要配置路由主頁，新增路由配置
![](https://i.imgur.com/GeZ89AK.png)
二、Router.js檔案：
說明：所有路由檔案路徑配置都是在router.js檔案下，新增巢狀僅是在特定頁面下新增`children:[ { } ]而已`
```javascript
{
     path:'/page',//對應的虛擬路徑
     name:'分頁',//元件呈現的名稱
     component:Page,//對應元件
     children:[
{
     path:'',//如果沒有填入入徑，元件child1預設會是主頁
     name:'child1',
     component:child
},
{
     path:'child2',
     name:'child2',
     component:child2
]
},
```
### 動態路由
#### 前置作業：
1.安裝 Vue-axios [NPM安裝連結](https://www.npmjs.com/package/vue-axios)
2.安裝 random Api   [連結](https://randomuser.me/documentation)
#### 使用目的：
切換不同id時候，置換對應內容。開發時候會由後端提供定義好的id，前端在拿來套用切換即可。應用在後端權限控制上 [參考文章](https://www.itread01.com/content/1537269627.html)
參考文件：[路由對象屬性介紹](https://router.vuejs.org/zh/api/#%E8%B7%AF%E7%94%B1%E5%AF%B9%E8%B1%A1)
寫法拆解如下：
ㄧ、Router.js檔案
![](https://i.imgur.com/4qG7Evd.png)
二、分頁：child3.vue
![](https://i.imgur.com/dmqRhBS.png)
三、Main.js
![](https://i.imgur.com/vdsK6Ny.png)

### 同一個頁面載入不同元件
補充：router-view
「我們可以透過 vue-router 的設定檔來定義整體網站的路由規則，利用 router-view 來定位子路由組件渲染的出口，並可允許訂定多組具名 router-view 來一次顯示多個子組件於單一子路由中。」
白話文：父組件中會包含 router-view` 作為子組件的渲染出口!`
ㄧ、index.js
![](https://i.imgur.com/NRL2TcJ.png)說明：補充1，因為child1如果不填寫入徑，會預設上層項目。故，我們要將上層`”name”`隱藏
二、App.vue
這邊可以視為首頁，換句話說就是整個 vue 包在最外層的父元件
![](https://i.imgur.com/uEYGd4v.png)
三、Menu.vue 和 page.vue
![](https://i.imgur.com/xl1pHaP.png)
#### 問題詢問
我把檔案做了以下調整
1.App.vue檔中，我移除`<router-view name=“menu”></router-view>`
2.在page.vue中新增 `<router-view name=“menu”></router-view>`
結果畫面只出現child1分頁內容，為何？
![](https://i.imgur.com/bwmgHkd.png)
A：因為如果我把`<router-view name=“menu”></router-view>`放在page.vue中，我們會把menu變成page 的子組件，因此畫面上不會出現。
如果更改為下面範例：
```javascript
{
  path: '',
  name: 'child 1',
  components:{
    default: child,
    menu: Menu,
  },
},
```
畫面就可以成功出現摟
![](https://i.imgur.com/htGJGpi.png)

##### 小結論
router-view
白話文：父組件中會包含 router-view`作為子組件的渲染出口!`
參考文章：[跟著 Vue 闖盪前端世界](https://dotblogs.com.tw/wasichris/2017/03/06/235449)
![](https://i.imgur.com/rsBF7wn.png)

### 常用Vue Router 參數設定
#### Router建構選項
[參考文件](https://router.vuejs.org/zh/api/#router-%E6%9E%84%E5%BB%BA%E9%80%89%E9%A1%B9)
* mode
可以將路由中#移除，但建議還是保留預設狀態即可（原因是因為移除後，就必須和後端配合路由切換）
* linkActiveClass
可以將標籤className替換
```javascript
export default new VueRouter({
    mode:'history',  
// 可以將路由中#移除，但必須提醒若將#移除就不是前端模擬路由。
// 而是後端切換路由，因此後端路徑也必須重新配置
    linkActiveClass:'active',  //標籤className替換
    routes: [
        {
            path: '/index',    //對應的虛擬路徑
            name: 'home',     //元件呈現的名稱
            component: Home,  //對應元件
        },
    ]
});
```
#### 切換路徑方法
[文件參考](https://router.vuejs.org/zh/guide/essentials/navigation.html)
![](https://i.imgur.com/2aSL90S.png)
補充說明：
* 為何官網上寫`router.push(‘/page/child2’)`，而我們這邊卻使用
`this.$router.push(‘/page/child2’)`呢？
Ａ：原因在於我們在main.js中，有先執行了 vue.use(....)，因此外部資源會被掛載到 vue 內。所以就可以使用 this 來呼叫這些資源
* 比較：
`router.push()`  會向history添加新記錄，當用戶點擊瀏覽器後退按鈕時，則回到之前的URL。 
`router.replace()`   不會向history添加新記錄










