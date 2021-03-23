---
title: Css-transition、animation(animate)動畫效果
date: 
tags:
   - transition
   - Css
categories:
   - Css
---

參考資料：
[Day27：小事之 Transition 與 Animation](https://ithelp.ithome.com.tw/articles/10197303)
[範例](https://codepen.io/chunwen/pen/rRrwKp)
<!-- more -->
- - - -
## Transition
轉場是從 A 狀態，轉變成 B 狀態，中間的過程，就叫轉場
只能定義起始狀態跟結束狀態，中間狀態不能設定
![](https://i.imgur.com/hLg9uIp.png)圖片來源：[Day27：小事之 Transition 與 Animation](https://ithelp.ithome.com.tw/articles/10197303)
有下列幾個屬性：
1.transition-property(屬性) EX：width、height
2.transition-duration(時間)
3.transition-timing-function(特效) EX：ease-out
4.transition-delay(延遲)
預設值：all 0 ease 0

### 使用時機
常用於滑鼠事件（:hover、:active、:focus、click）或鍵盤輸入時觸發 
[範例](https://codepen.io/chunwen/pen/rRrwKp)
>注意：transition效果是寫在`原本A狀態`
>而變化後的屬性則是寫在`B狀態中`如：`.header:hover {height:200px}`
範例
```css
.header{
width:100px;
height:50px;
background:green;
border:1px solid red;
transition:width 3s ease-out 1s;
transition:height 1s; //一秒
}
.header:hover{
width:200px;
height:100px;
}
```
Q：是不是不能同時設定改變多個屬性質? EX：width、height等
A：分開寫不就好了

補充：transition 搭配 transform [範例](https://www.w3schools.com/css/tryit.asp?filename=trycss3_transition_transform)
參考資料：
[Ｗ3cschool](https://www.w3school.com.cn/cssref/pr_transition.asp)
[CSSTransition 轉場效果](https://carlos-studio.com/2017/02/23/css-transition-%E8%BD%89%E5%A0%B4%E6%95%88%E6%9E%9C/)

## animation(動畫效果)
可以自行撰寫動畫 開始、進行間、結束時各階段的變化，適合用來做較細微的動畫表現。但需要明確的指定關鍵影格(@keyframes)的參數。
目前多會直接使用animate.css套件，詳情可以看
 [jquery ch5-33](https://www.udemy.com/jquery-learning/learn/v4/t/lecture/5190570?start=300) 或 [官網](https://daneden.github.io/animate.css/) 
animate用法介紹： [pjchen](https://pjchender.blogspot.com/2015/12/cssanimation-keyframes.html) 

語法如下： [範例](https://www.w3schools.com/css/tryit.asp?filename=trycss3_animation1)
```css
.box{
animation: change 5s ; //八個屬性中至少要有名稱（自行命名）、時間

//正常會寫成這樣
animation: change 5s linear 2s infinite alternate;
}
```

//設定多個狀態，可以非常詳細
```css
@keyframes change{
0%{ background: #4BC0C8;}
20%{ background: #C779D0;}
60%{ background: #FEAC5E;}
80%{ background: #185a9d;}
100%{ background: #4BC0C8;}
}
```

### 載入animate.css語法
使用方式：
1.在head裡面插入連結
```html
<head>
<meta charset="UTF-8">
<title>Animate.css </title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css">
</head>
```

2.在想進行動畫的元素上加上class，一定要先加 animated 再加上要使用的動畫名稱（注意大小寫），如果想要動畫一直動作可以加上 infinite。 [範例](https://codepen.io/chunwen/pen/rRrwKp)
```html
<body>
    <h1 class="animated fadeIn">我是LOGO</h1>
    <h2 class="animated infinite jello">INFINITE</h2>
</body>
```

## animate與transition比較
![](https://i.imgur.com/HGV5BAR.png)圖片來源：[Day27：小事之 Transition 與 Animation](https://ithelp.ithome.com.tw/articles/10197303)
### 差異點
tansition 是當參數改變時觸發，而 animations 則是直接就執行，所以動畫效果需要明確的指定關鍵影格的參數。
