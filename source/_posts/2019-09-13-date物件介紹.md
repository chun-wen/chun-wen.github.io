---
title: Javascript-date物件介紹
date: 2019-09-13 23:48:42
tags:
   - JavaScript
categories:
   - JavaScript
---
參考資料：
[MDN-Date](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Date)
[JavaScript Date 時間和日期整理(推薦1)](https://www.fooish.com/javascript/date/)
[PJChen—JavaScript Date Time Method 日期時間](https://pjchender.github.io/2017/12/27/js-javascript-date-time-method-%E6%97%A5%E6%9C%9F%E6%99%82%E9%96%93/)
[JavaScript 初心者筆記](https://ithelp.ithome.com.tw/articles/10214769#response-310945)
[保哥—關於 JavaScript 中 Date 型別的常見地雷與建議作法](https://blog.miniasp.com/post/2016/09/25/JavaScript-Date-usage-in-details)
[Ｗ3C—JavaScript Get Date Methods](https://www.w3schools.com/js/js_date_methods.asp)
<!-- more -->
- - - -
### 前言
本篇要來教大家如何用JS取得時間，並用幾個簡單範例幫助大家清楚實務上該如何操作。開始前，我們必須要來了解一下語法該如何撰寫

### 語法撰寫
首先，我們先介紹建立時間物件寫法：
```javascript
new Date()   //回傳目前時間的物件
接著，我們先在Chrome 開發者工具看，會發現會回傳一個本地時間
// Fri Sep 13 2019 15:54:29 GMT+0800 (台北標準時間)
```
> 提醒：  
Date物件僅能透過new建構子來產生物件喔！  

四種語法：
```javascript
1. new Date();                //回傳目前時間的物件
2. new Date(value);           //需傳入一個整數值
3. new Date(dateString);
4. new Date(year, month[, day[, hour[, minutes[, seconds[, milliseconds]]]]]);
```
範例：
```javascript
1.new Date(); 
// Fri Sep 13 2019 15:54:29 GMT+0800 (台北標準時間)

2.new Date(1568363900509)
// Fri Sep 13 2019 16:38:20 GMT+0800 (台北標準時間)

3.new Date('2019-09-13T08:21:03.989Z')
// Fri Sep 13 2019 16:21:03 GMT+0800 (台北標準時間)

4.new Date(2019,8,13,16,30,4)
//Fri Sep 13 2019 16:30:04 GMT+0800 (台北標準時間)
//month計算由0~11，所以輸入８，才會顯示九月
```
> 提醒：  
> 1.month計算由0~11  
> 2.使用第三種方法傳入String，請使用**ISO 8601 Extended Format**格式  
> 寫法如下：  
```javascript
寫法：
YYYY-MM-DDTHH:mm:ss.sssZ
範例：
2019-09-13T08:21:03.989Z
//Ｔ代表與時間分隔
```
### 取得、設定Date物件方法
* getFullYear（） / setFullYear（）：取得/設定年份（4 位數）
* getMonth（）/ setMonth（）：取得/設定月份（0 - 11）
* getDate（） / setDate（）：取得/設定月份日期 (1-31)
* getDay（）：取得當週日期（0 - 6）
* getHours（）/ setHours（）：取得/設定小時（0 - 23）
* getMinutes（） / setMinutes（）：取得/設定分鐘（0 - 59）
* getSeconds（） / setSeconds（）：取得/設定秒數（0 - 59）
* getMilliseconds（） / setMilliseconds（）：取得/設定毫秒（0 - 999）
* getTime（） / setTime（）：取得/設定自 1970 年 1 月 1 日 00:00:00 以來的毫秒數。
* toDateString（） ：取得具可讀性的日期字串       
如：Fri Sep 13 2019
* toTimeString（） ：取得具可讀性的時間字串  
如："18:04:00 GMT+0800 (台北標準時間)"
* toISOString（）：取得ISO格式字串       
如：2019-09-13T10:02:00.035Z
* toString（） ：取得日期時間的字串
如：Fri Sep 13 2019 18:04:45 GMT+0800 (台北標準時間)

範例：
1.取得目前時間
```javascript
var dayName = ['星期天','星期一','星期二','星期三','星期四','星期五','星期六'];
var currentTime = new Date();
var y = currentTime.getFullYear();
var m = currentTime.getMonth();
var d = currentTime.getDate();
var day = dayName[currentTime.getDay()];
console.log('今天是'+y+'年'+m+'月'+d+'號'+day)
//今天是2019年8月13號星期五
```
2.日期比較
```javascript
//今天日期是否大於2019
var now = new Date().getFullYear();
var compare = new Date().setFullYear(2017)
if(compare < now){
  alert('compare小於2017年')
}
  else {
  alert('compare 大於2017年');
}
```
補充：參考[stack overflow回答](https://stackoverflow.com/questions/492994/compare-two-dates-with-javascript)，若要比較兩者時間，建議使用getTime（）來比較
3.設定日期
```javascript
var now = new Date();  // 建立時間物件
var changeDay = 30;    // 設定要往前或往後幾天
var next = now.setDate(now.getDate() + changeDay)
//now.getDate()用來取得今天是幾號
console.log(now.toDateString()) 
// 把物件轉成字串 Sun Oct 13 2019
```

### 重點筆記
```javascript
Date.now()   //回傳當前的timestamp(毫秒)
new Date()   //回傳目前時間的物件
```
