---
title: [筆記]JavaScript 陣列處理方法
date: 2019-08-26 21:19:59
tags:
   - array
   - JavaScript
type:
   - JavaScript
---

參考資料：
[卡斯伯七種常見陣列處理方法](https://wcc723.github.io/javascript/2017/06/29/es6-native-array/)
[ JavaScript  陣列方法簡介](https://oranwind.org/post-post-22/)
- - - -
在閱讀完卡斯伯老師文章，我將整理文章中處理陣列方法，並搭配自己的練習輔助說明。對了補充說明：陣列處理方式在IE8以前是不支援的！
首先，我們先簡單寫一個陣列
```javascript
var restaurant=[
  {
    option:'taiwanese',
    price:100,
    location:'Taipei'
  },
  {
    option:'Korean',
    price:200,
    location:'Yilan'
  },
  {
    option:'Thailand',
    price:300,
    location:'Taoyuan'
  },
  {
    option:'American',
    price:450,
    location:'Taichung'
  },
  {
    option:'Italian',
    price:900,
    location:'Kaohsiung'
  },
]
```
### forEach（）方法
簡介：會對陣列每個元素都執行一次，但不會有回傳值
```javascript
   var forEach = 
   restaurant.forEach(function (item, index, array) {
            return item; //沒有東西
   })
   console.log(forEach) //undefined

   var forEach = 
   restaurant.forEach(function (item, index, array) {
            item.price = item.price+100;
            // console.log(item.option)
            // console.log(index)
            // console.log(array)
            console.log(item.price); //200 300 400 ....
   })
```
> 說明：item以這裡為範例的話，代表物件中的值  
### map（）方法
簡介：跟forEach相比多了回傳值，並透過函式回傳值組合成一個新的陣列
`適合將原始的變數運算後重新組合一個新的陣列`
特性：
1.如果不回傳則是`undefined`
2,回傳數量等於原始陣列長度
```javascript
var mapArray=restaurant.map(function (item,index,array) { 
            if( item.price=== 900){
            return `${item.option}好貴`
            }
            else{
              // return false   //不符合條件的會回傳false
              // return `${item.option}好便宜`
            }
           });
           console.log(mapArray)
說明：else{}可以選擇return false或 return `${item.option}好便宜`
並用console.log(mapArray)觀察結果
```
> 補充：return 一個值必須使用有一個變數接受資料！  

### filter（）方法
會回傳符合條件的元素，得到一個新陣列。若不符合條件則會得到一個空陣列。適合用在搜尋與過濾資料  `會獲得一個陣列`
```javascript
 var filterArray=
 restaurant.filter(function(item,index,array){
 return item.price>=300; //取得價錢大於300餐廳
 })
 console.log(filterArray) //(3)[{…}, {…}, {…}]

```
### find（）方法
只會回傳一次值，且是第一個滿足條件的元素值，若沒有則會回傳`undefined`
```javascript
var findArray =
restaurant.find(function(item,index,array){
            return item.option==='Thailand'
})

console.log(findArray) 
//{option: "Thailand", price: 300, location: "Taoyuan"}
```
### every（）方法
用來檢查所有陣列是否符合條件，僅會回傳一個值`true`或`false`
```javascript
var everyArray = 
restaurant.every(function (item, index) {
            return item.price >= 100
          });
          console.log(everyArray) //true
```
### some（）方法
都是回傳 true or false，差異僅在 every() 需完全符合，some() 僅需要部分符合。
```javascript
var someArray = 
restaurant.some(function (item, index) {
            return item.price > 300
          });
          console.log(someArray); //true
```
### reduce（）方法
將Accumulator及陣列中每項元素（由左至右）傳入回呼函式，`並產生一個值`
參數介紹：
Accumulator:：
前一個參數，如果是第一個陣列的話，值是以另外傳入或初始化的值
currentValue: 當前變數
currentIndex: 當前索引
array: 全部陣列
```javascript
var reduceArray=
restaurant.reduce(function(accumulator,currentValue,currentIndex,array){
 // console.log(accumulator,currentValue,currentIndex,array);
            return accumulator +currentValue.price
          },0)
console.log(reduceArray); //累加的值為1950

```

- - - -
下面內容為文章內容以外，更新一些常用陣列方法
### Sort（）方法
[Sort影片教學](https://youtu.be/8JzVwrzkUrM?list=PLEfh-m_KG4dYbxVoYDyT_fmXZHnuKg2Fq&t=1324) [MDN參考資料](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
這要用來針對資料進行排序，會return -1、0、1       `會回傳一個陣列`
原理說明：
預設的排序順序是根據字串的 Unicode 編碼位置（code points）而定。
穩定排序：指的是如果比較數值相同，不會調整原始資料順序
用法有兩種：
1.直接針對資料sort（），通常用在value、數值           =>預設升冪排列
2.針對資料進行減法運算（比較推薦使用，如下範例）
```javascript
let ary=[1,110,23,54]
ary.sort((a,b)=>a.year-b.year); // 1,0,-1
```
補充說明：升冪（以a為比較基準點）
```javascript
function compare(a, b) {
  if (在某排序標準下 a 小於 b) {
    return -1;   
  }
  if (在某排序標準下 a 大於 b) {
    return 1;     
  }
  // a 必須等於 b
  return 0;
}
```
補充說明：降冪（以b為比較基準點）
```javascript
function compare(a, b) {
  if (在某排序標準下 b 小於 a) {
    return -1;   
  }
  if (在某排序標準下 b 大於 a) {
    return 1;     
  }
  // b 必須等於 a
  return 0;
}
```
範例（搭配三元運算子）：
```javascript
     let ans = inventors.sort(function(a,b){
     return (a.year > b.year) ? 1: (b.year > a.year) ? -1:0           
})
     console.table(ans);
```
### includes（）
這個語法是ES7提供，會判斷陣列是否包含特定的元素，並以此來回傳true或false。
語法：`arr.includes(searchElement[, fromIndex])`
特性：
1.當fromIndex為負數，並且超過陣列長度則會搜尋整個陣列
2.當fromIndex為正數，並且超過陣列長度則會回傳false
3.當fromIndex為負數，但沒有超過陣列長度則會將`array.length +fromIndex`開始向後搜尋
```javascript
var ary =[1,2,3]
console.log(ary.includes(2))  //true
console.log(ary.includes(4))  //false

[3, 2, 1].includes(3, -3);     //true
[3, 2, 1].includes(3, -2);     //false
```
### indexOf（）
會回傳給定元素於陣列中`第一個被找到之索引`，若不存在於陣列中則回傳 -1。 [MDN介紹](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
語法：
`arr.indexOf(searchElement[, fromIndex])`
特點：
1.fromIndex為正數，則會從左到右開始搜尋
2.fromIndex為負數，則會從陣列尾端開始搜尋，會搜尋到最後一個的索引值為 -1
```javascript
var array = [2, 9, 9];
array.indexOf(2);     // 0
array.indexOf(7);     // -1
array.indexOf(9, 2);  // 2
array.indexOf(2, -1); // -1   出現-1表示搜尋不存在
array.indexOf(2, -3); // 0
```
### slice（）
會回傳一個新陣列物件，為原陣列選擇之 begin 至 end（不含 end）部分的淺拷貝（shallow copy）。而原本的陣列將不會被修改。 [MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
語法：
`arr.slice([begin[, end]])`
特點：
Begin : 預設起始索引為0，若為負數則從最末端開始
End：預設起始索引為0，若為負數則從最末端開始
舉例來說，slice(1,4)提取了陣列中第二個元素至第四個元素前為止（元素索引 1、2 以及 3）來拷貝。
```javascript
var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
var slice =fruits.slice(0,2). //["Banana","Orange"]

```
### splice（）
藉由刪除既有元素並／或加入新元素來改變一個陣列的內容。會回傳一個陣列
[MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
語法：
`array.splice(start[, deleteCount[, item1[, item2[, …]]]])`
特點：
Start 增加/刪除項目的位置，負數代表從後方算起。
deleteCount 刪除的個數，如為0或沒有填寫則不會刪除。
Item… 添加的新項目。
```javascript
var myFish = ['angel', 'clown', 'mandarin', 'sturgeon'];
var removed = myFish.splice(1,2,'chunwen')

console.log(myFish)   //["angel", "chunwen", "sturgeon"]
console.log(removed)  //["clown", "mandarin"]
```
### join（）
將所有的元素連接、合併成一個字串，並回傳此字串 [MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/join)
語法：
`arr.join([separator])`
特點：
Sperator若未傳入參數預設是用逗點隔開`,`
```javascript
var a = ['Wind', 'Rain', 'Fire'];
a.join();      // 'Wind,Rain,Fire'
a.join(', ');  // 'Wind, Rain, Fire'
a.join(' + '); // 'Wind + Rain + Fire'
a.join('');    // 'WindRainFire'
```
### reverse（）
反轉陣列，會改變原本陣列內容！ [MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)
語法：
`a.reverse()`
```javascript
var food=['apple','book','cat'];
var reverseFood = food.reverse();

console.log(food)         //["cat", "book", "apple"]
console.log(reverseFood) //["cat", "book", "apple"]
```


