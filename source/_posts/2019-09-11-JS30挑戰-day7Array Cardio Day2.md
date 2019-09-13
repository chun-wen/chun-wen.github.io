---
title: JS30挑戰-Day7-Array Cardio Day2
date: 2019-09-14
tags:
   - JavaScript
   - JavaScript30天挑戰 
categories:
   - JavaScript
---

參考資料：
[操作陣列的20種方法](https://hsiangfeng.github.io/javascript/20190421/1216566123/)
[Alex直播影片](https://youtu.be/OdNA37WSwzc?list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&t=613)
[JS時間取得方法筆記](https://chun-wen.github.io/2019/09/13/date%E7%89%A9%E4%BB%B6%E4%BB%8B%E7%B4%B9/#more)
[Demo練習](https://chun-wen.github.io/JavaScript30/07%20-%20Array%20Cardio%20Day%202//index-chunwen.html)
<!-- more -->
- - - -
### some
回傳 true or false，差異僅在 every() 需完全符合，some() 僅需要部分符合
```javascript
constans=people.some(y => newDate().getFullYear()-y.year>=19)
console.log(ans); //true
```

### every
用來檢查所有陣列是否符合條件，僅會回傳一個值true或false
```javascript
constans = people.every(function(year){
return newDate().getFullYear()-year.year>=19;
})
console.log(ans);
```

### find
適合用來搜尋是否有符合資料，僅會回傳第一筆資料
```javascript
constans = comments.find(id=>id.id===823423)
console.log(ans)
```

### findIndex
尋找第一個符合條件的序號
```javascript
constans = comments.findIndex(id => id.id === 823423 )
console.log(ans) //1
```

### slice
>目的：不要動到原始資料
```javascript
constans = comments.slice(0,1)
constans2 = comments.slice(2)
constans3 = [...ans,...ans2]
console.log(ans3)
```

### splice
```javascript
constans = comments.splice(1,1);
console.log(ans)
```
[今日影片重點整理](https://youtu.be/OdNA37WSwzc?list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&t=2226)

### 補充：複製物件介紹
[影片講解](https://youtu.be/OdNA37WSwzc?list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&t=3098)
```javascript
    let obj1 = { count: 1 };
    let obj2 = obj1;
    let obj3 = Object.assign({}, obj1)
    obj1.count = 5;
    let obj4 = JSON.parse(JSON.stringify(obj1))

console.log(obj1.count + obj2.count + obj3.count + obj4.count) 
// 5+5+1+5 =16
```

### 心得
1.解構賦值概念
2.取得資料時盡量不要對原始資料進行更動
3.splice、slice比較
4.取得時間方法整理 [JS時間取得方法筆記](https://chun-wen.github.io/2019/09/13/date%E7%89%A9%E4%BB%B6%E4%BB%8B%E7%B4%B9/#more)




