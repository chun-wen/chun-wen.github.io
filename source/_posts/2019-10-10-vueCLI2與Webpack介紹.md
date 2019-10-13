---
title: Vue CLI2與Webpack介紹
date: 2019-10-13 20:46:35
tags:
   - vue 
   - ironman
   - vueCLI
categories:
   - vue
---

參考資料
- 六角Vue課程
- [Vue Cli3官網](https://cli.vuejs.org/guide/installation.html)
- [Kuro’s Blog 初探 Vue-CLI v3.0](https://kuro.tw/posts/2018/07/04/%E5%88%9D%E6%8E%A2-Vue-CLI-3-0/)
<!-- more -->
-----

### 什麼是Vue CLI?
基於Webpack所建置得開發工具（白話文：內建webpack），Vue Cli是一個指令
![https://ithelp.ithome.com.tw/upload/images/20191010/201146452cgeLWRbi5.png](https://ithelp.ithome.com.tw/upload/images/20191010/201146452cgeLWRbi5.png)

### 為何要使用Vue Cli?
1.快速建立 Vue.js 的專案項目環境，並提供開發階段便利的運行環境
2.便於使用各種第三方套件（BS4、Vue Router）
3.可以運行Sass、Babel等編譯工具
4.便於開發SPA

### Webpack簡介
![https://ithelp.ithome.com.tw/upload/images/20191010/20114645ZmbnxU2ZmK.png](https://ithelp.ithome.com.tw/upload/images/20191010/20114645ZmbnxU2ZmK.png)
說明：
Webpack會去監控main.js檔案，當內容有更動時就會自動編譯
而`main.js`就是Webpack進入點，但因為main.js是JS檔，所以無法編譯`.png`、`.vue`、`.sass`檔案，因此需要`loader`工具來協助編譯

既然談到Ｗebpack，我們就來簡單介紹一下他的檔案結構吧！


-----

### Webpack腳本結構
#### .base檔案說明1
![https://ithelp.ithome.com.tw/upload/images/20191010/201146451pcKqzbMwr.png](https://ithelp.ithome.com.tw/upload/images/20191010/201146451pcKqzbMwr.png)
#### .base檔案說明2
![https://ithelp.ithome.com.tw/upload/images/20191010/20114645dzemdx88X2.png](https://ithelp.ithome.com.tw/upload/images/20191010/20114645dzemdx88X2.png)
補充一下：base64：目的將圖片轉為文字編碼方式，加速畫面載入速度。
#### config檔案說明
![https://ithelp.ithome.com.tw/upload/images/20191010/20114645k3X7fmXv8Q.png](https://ithelp.ithome.com.tw/upload/images/20191010/20114645k3X7fmXv8Q.png)
#### 環境變數
主要目的：許多資源在測試機與正式機是不同的，因此可以使用環境變數來切換不同環境。
![https://ithelp.ithome.com.tw/upload/images/20191010/201146451bl7UGcEpG.png](https://ithelp.ithome.com.tw/upload/images/20191010/201146451bl7UGcEpG.png)
> 補充：`process.env`，從哪來？[同學討論連結](https://www.udemy.com/course/vue-hexschool/learn/lecture/10415930#questions/5480948)



-----

### Vue CLI2 安裝
[Vue Cli2參考資料](https://github.com/vuejs/vue-cli/tree/v2#vue-cli--)
安裝步驟：
1.`sudo install -g vue-cli`

2.接著，創建專案`vue init webpack my_project`
例如：`vue init webpack vuewebpack`

3.終端機就會出現下面相關內容（這邊就先按照課堂老師設定）
![https://ithelp.ithome.com.tw/upload/images/20191010/201146456z4F93x5X8.png](https://ithelp.ithome.com.tw/upload/images/20191010/201146456z4F93x5X8.png)
4.接著，會出現下面畫面（依序輸入即可）
![https://ithelp.ithome.com.tw/upload/images/20191010/20114645f13D6W9LDl.png](https://ithelp.ithome.com.tw/upload/images/20191010/20114645f13D6W9LDl.png)
5.安裝成功畫面
![https://ithelp.ithome.com.tw/upload/images/20191010/20114645dT74V1kgjK.png](https://ithelp.ithome.com.tw/upload/images/20191010/20114645dT74V1kgjK.png)
###  資料結構說明
![https://ithelp.ithome.com.tw/upload/images/20191010/20114645OmEYIVAcaa.png](https://ithelp.ithome.com.tw/upload/images/20191010/20114645OmEYIVAcaa.png)
說明：
Dist資料夾內檔案都必須運行在HTTP server喔！

#### Vue.file 檔案結構
![https://ithelp.ithome.com.tw/upload/images/20191010/20114645u1kuavW88T.png](https://ithelp.ithome.com.tw/upload/images/20191010/20114645u1kuavW88T.png)
圖片來源：五倍紅寶石
Vue檔，會包含三個部分（HTML、Script、Style）
Style：
若沒有CSS就不會有喔，另外加上scoped後，就可以將樣式放在特定元件下不會污染全域
```css
<style scoped lang=“scss”>
h3 {
margin:40px00;
}
</style>
```

#### main.js檔案介紹
![https://ithelp.ithome.com.tw/upload/images/20191010/20114645Iq0EyV0tkp.png](https://ithelp.ithome.com.tw/upload/images/20191010/20114645Iq0EyV0tkp.png)


