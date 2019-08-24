---
title: JS30挑戰-Drum Kit
date: 2019-08-24 17:30:54
tags: #JS30
---

# JS30挑戰-Drum Kit
#JavaScript30天挑戰
[Alex直播筆記](https://www.youtube.com/watch?v=f2ttaeDHzwE&list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&index=1)
- - - -
## 功能目的：
透過JS使鍵盤按下後播放出對應按鍵的聲音，並同時產生音效與改變樣式，
並且在按下其它鍵後會關閉該特效並於新按鍵中啟用。

## 第一部分：
我們需要先透過綁定DOM元素，來觸發兩個事件
![](JS30%E6%8C%91%E6%88%B0-Drum%20Kit/1B0A5A35-C30D-40F8-B5AD-02DA643836BB.png)
觀念一：使用立即函式將JS包在script中
觀念二：螢幕捲軸、鍵盤事件、畫面旋轉通常會使用在window事件上
重點：
1.ES6 String template用法 [[[筆記]ES6語法介紹(Let、Const、字串)]]
(`audio[data-key=“${e.keyCode}”]`)
2.keyup、keydown、keypress比較。  [文章介紹](https://medium.com/@yitailin/%E6%AF%94%E8%BC%83-keydown-keypress-keyup-%E7%9A%84%E5%B7%AE%E7%95%B0-4e873ba17e81)
Keyup:鍵盤放開時觸發
KeyDown:鍵盤按下時候觸發（包含不能輸出的符號如:ESC、Enter）
KeyPress:僅觸發可以輸出文字的符號

## 第二部分
影片大約33分開始
![](JS30%E6%8C%91%E6%88%B0-Drum%20Kit/FF4AD8A4-C348-4B6B-AFC8-24B10C659812.png)
找到事件綁定完後，就可以開始撰寫兩個事件function
1.音樂播放事件 `music.play()`
注意：
* 若要連續觸發音樂事件，需要使用`currentTime`
* 另外可以使用`if`判斷式來確保console.log不會跳錯

2.使用classList語法新增className 
>>`dom.classList.add(‘playing’)`（類似jQuery addClass相關用法）

## 第三部分
畫面完成渲染後，我們需要移除className
1.transitionend 用法
注意：
* 使用transitionend時，如果畫面上有不同屬性改變，這時候會重複觸發
因此我們要使用下面語法，找到特定屬性，來移除className
`if (e.propertyName === 'transform')`

2.forEach 用法
3.`Array.from() `可以將類陣列轉為陣列（練習中沒使用到）
[MDN參考資料](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

### 補充：
HTML
1.`<kbd> `HTML標籤  [MDN參考資料](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/kbd)
>>這其實也說明，Html語法其實蠻自由，我們都可以自行創建命名使用喔
`<andy>my name is andy</andy>`
2.`data-*`用法。[[[筆記]HTML5中的資料屬性  data-*(attribute)]]
CSS
`transform: scale(1.1)`>>將樣式放大（常做在hover效果上）
`text-transform: uppercase;`>>將字體轉為大寫
JS
程式碼整理：
將function放到最上面 ，執行事件往下

## 學習心得
1. 程式碼整理
2. 藉由繪圖整理程式撰寫邏輯
3. 學習方式調整為：看完老師直播後，**自己重新撰寫一次**
4. ES6 template string、classList、transitionend、data-*、nodeList





