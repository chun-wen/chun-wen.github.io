---
title: '2021-07-20-[筆記]Async、Await使用'
tags:
  - JavaScript
categories:
  - JavaScript
---
前言：
`Async`、`Await` 本身是個語法糖，我們多數拿來搭配 `Promise.all` 、 迴圈、 `fetch` 等方法一起使用，讓程式碼看起來更直覺．
<!-- more -->
---
參考資料：
[MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/async_function)
[鐵人賽：JavaScript Await 與 Async](https://wcc723.github.io/javascript/2017/12/30/javascript-async-await/)

---
### 字詞解釋
Async : 就字面上的意思是非同步

Await : 等待

### 歷史
而我們為何要使用這兩個語法糖呢? 
- 目的就是避免同步、非同步程式碼混合情況產生
 `JavaScript` 執行時是從上到下逐行執行，而在這區間撰寫非同步程式碼，會讓觀看程式碼較為不直覺，因此透過 `Async Function` 可以讓函式內的程式碼以非同步執行，但閱讀起來卻又像是同步程式碼。較易維護。

聽起來有點饒舌，我們直接來看 `Code`。

```jsx
// 正常 Promise 寫法如下
function chainPromise(num){
  return new Promise( (resolve,reject) => {
       if(num){
           resolve(`${num} 成功`)
       }
       else{
          reject(`${num}失敗`)
       }
  });
}

chainPromise(1)
 .then(res => {
    console.log(res);
 }).catch(error => {
   console.log(error);
 });

// 2.改用 async、await改寫
async function asyncFunc(){
    const data1 = await chainPromise(1);
    const data2 = await chainPromise(2);
    console.log(data1,data2); 
}

asyncFunc();
console.log("3") 
// 印出順序
// 3
// 1成功 2 成功 
```

小提醒： Async、Await必須搭配使用。不能單獨使用。

### 當遠端資料有錯時，該如何處理?
透過 `try、catch` 包起來，但目前測試下來僅會回傳錯誤狀態。會這樣做是因為，在 `async Function` 中非同步程式碼已經是同步執行，因此只要上面程式碼有誤，下方程式碼就不能執行!

```jsx
function chainPromise(num){
    return new Promise( (resolve,reject) => {
         if(num){
             resolve(`${num} 成功`)
         }
         else{
            reject(`${num}失敗`)
         }
    });
}

// 2.失敗後，後面程式碼就不執行了！
async function asyncFunc(){
    try{
        const data1 = await chainPromise(1);
        console.log(data1);
        const data2 = await chainPromise(0);
        console.log(data2);
        const data3 = await chainPromise(3);
        console.log(data3);
    }
    catch(err){
        console.log("catch",err);
    }
}

asyncFunc();
```

### 使用時機
搭配 Fetch 、 for loop 、 陣列、 Promise ALL 方法使用

1. 使用 Fetch

```jsx
fetch("https://jsonplaceholder.typicode.com/todos/1")
   .then( res => console.log(res.json())) 
// fetch 回傳為 ReadableStream，必須將資料作轉換

// 立即函式 + 箭頭函式
(async () =>{
   await fetch("https://jsonplaceholder.typicode.com/todos/1")
   .then( res => res.json())
   .then( result => console.log(result)); 
})();
```

1. Promise ALL
```jsx
async funtction getData () => {
   const Data = await Promise.all([],[]);
   console.log(Data);
}

getData();
```