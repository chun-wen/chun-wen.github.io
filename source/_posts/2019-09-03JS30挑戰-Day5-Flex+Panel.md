---
title: JS30挑戰-Day5-Flex+Panel
tags:
  - flex
  - JavaScript
  - JavaScript30天挑戰
  - css
categories:
  - JavaScript
abbrlink: 4027575200
date:
---

本篇文章主要紀錄觀看Alex大大直播紀錄後，所做的筆記記錄
[demo連結](https://chun-wen.github.io/JavaScript30/05%20-%20Flex%20Panel%20Gallery/index-chunwen.html)

參考資料：
[Alex直播連結](https://www.youtube.com/watch?v=7hGFTNGommU&list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&index=5)
[JS30紀錄-其他人的筆記](https://shunnien.github.io/2017/12/18/Javascript30days-5/)
<!-- more -->
- - - -
## Css講解
[Flex整理教學](https://chun-wen.github.io/2019/09/03/2019-09-03Flex%E6%8E%92%E7%89%88%E6%95%B4%E7%90%86/#more)
### 使用Flex巢狀結構
小技巧：可以使用`border : 1px solid red`來觀察排版

```css
/* Flex Children，這邊是針對每個p段落再設定flex container*/
    .panel > * {
      margin: 0;
      width: 100%;
      transition: transform 0.5s;
      display: flex;
      justify-content: center;
      align-items: center;
      flex:1;
      border: 1px solid red;
    }
```
補充：`省略.panel > * {justify-content: center;} `示意圖如下
![](https://i.imgur.com/yBHTdgK.png)


## JS開始講解
### 1.動態切換class
[影片連結](https://youtu.be/7hGFTNGommU?list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&t=1524)
[MDN-classList](https://developer.mozilla.org/zh-TW/docs/Web/API/Element/classList) 與 jQuery add/remove/toggle 效果一樣
```javascript
     // class切換
      function clickHandler(e){
        this.classList.toggle('open')
      }
```

### 2.兩段動畫切換
[TransitionEnd 影片教學](https://youtu.be/7hGFTNGommU?list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&t=2362)
Transitionend：
transitionend 事件會在CSS transition  結束後觸發。[MDN資料](https://developer.mozilla.org/zh-CN/docs/Web/Events/transitionend)
注意：TransitionEnd會因為屬性數量不同，而觸發不同次效果。
可以透過`console.log(e)`查看
課堂範例：
```css
.panel {
        transition:
        font-size 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
        flex 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11);
}
```
```javascript
   function changeHandler(e){
        console.log(e)
        if(e.propertyName.includes('flex')){
          this.classList.toggle('open-active')
        }
      }
```
說明：
如果我們不加入`if判斷式`來指定特定propertyName觸發，會造成效果出不來。
原因如下：
1.TransitionEnd會因為屬性數量不同，而觸發不同次效果
2.而我們又使用toggle，如果是觸發偶數屬性則會`先開又被關`，基數則不會

#### 小結論
>建議：若不確定屬性數量，可以使用console.log(e)，印出來屬性數量

#### 撰寫心得：
1.卡在transitionend 事件
2.includes 跟 === 搞混   [陣列處理方法](https://chun-wen.github.io/2019/08/30/2019-08-30-JavaScript%20%E9%99%A3%E5%88%97%E8%99%95%E7%90%86%E6%96%B9%E6%B3%95/)
3.this用法 