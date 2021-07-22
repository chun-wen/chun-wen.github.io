---
title: '2021-07-23-[筆記]搭配 loader.css 實作一個簡單遮罩效果'
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 2606147343
---
前言：
前端透過 AJAX 呼叫 API 時，在等待資料回傳時為了增加使用者體驗效果，我們可以在傳輸資料這段時間增加遮罩效果，讓使用者不能操作其他功能、同時增加使用者回饋效果。

<!-- more -->
---
參考資料：
[[Day 06]loader.css - 就算loading中，也要很美觀才行](https://ithelp.ithome.com.tw/articles/10185191)

---

1. 我們需要一個 `div` ，來製造出遮罩範圍

```html
// HTML部分
<div class="loading">
      <div class="loader-inner ball-pulse"></div> 
      //這邊 Class 是引用 loader.css class
</div>
```

```scss
//CSS部分
.loading {
    background-color: black;
    opacity: 0.5;
    position: absolute; //位置漂浮在網頁上
    top: 0;  //如此位置會固定在左上角
    left: 0;
    width: 100vw; //可視寬度
    height: 100vh; //可視高度
    z-index: 999;
    animation: closeLoading 3s 1 ease-out forwards; //遮罩上新增動畫漸層效果
    @keyframes closeLoading {
        0% {
            opacity:1
        }
				50% {
						opacity: 0.5;
				}
				100% {
						opacity: 0;
				}
    }
}
```

1. 我們需要替遮罩增加旋轉效果

```jsx
因為我們有使用套件，所以可以直接使用
$('.loader-inner').loaders();
```

3. 完整程式碼

```jsx
// 利用 async 語法製造函式內同步執行
async function exportExcel(url, postData) {
    // 將<div> 直接加入 DOM 中
    $("#body").prepend(`<div class="loading">
        <div class="loader-inner ball-pulse">
          </div>
    </div>`)
    $('.loader-inner').loaders();
    await axios.post(url, postData, { responseType: 'blob' }).then((res) => {
        ..... 程式碼執行
    }).catch((error) => {
        if (error.response) {
            alert(error.response.data);
        } else {
            alert(error.message);
        }
    });
    //在將 DIV 移除
    $(".loading").remove();

}
```