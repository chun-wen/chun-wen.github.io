---
title: 2023-05-20-筆記-Throttle and Debounce
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 1862233687
---
前言：
記錄一下 `Debounce` 跟 `Throttle` 


<!-- more -->
---
參考資料：
- [JS中的debounce与throttle](https://juejin.cn/post/6844903760334946312)
- [Day25-認識與實作 Debounce 和 Throttle](https://ithelp.ithome.com.tw/articles/10297948)
- [JavaScript 节流 - Web前端工程师面试题讲解](https://www.youtube.com/watch?v=Li8BFRzuUg0)
- [LeetCode Throttle Editorial](https://leetcode.com/problems/throttle/editorial/)

---

## Outline
1. Definition of Debounce and Throttle
2. How to write Debounce and Throttle function
3. Which situation will you use
4. Reference


### Debounce
簡單來說 `Debounce` 會監聽時間內連續處發事件的最後一次觸發事件。若事件一直不段重複處發，則時間會一直重新計算！像是 input 框的`autoComplete` 
[Codepen](https://codepen.io/chunwen/pen/VwErzKM?editors=1011)

```
function debounce(func, delay = 1000){
   let timer = null;
   return function(...args){
      if(timer){
         // 釋放記憶體
         clearTimeout(timer);
      }
      
      timer = setTimeout(() => {
          // 執行 func 
          func.apply(this, args);
      }, delay)
   }

}


window.addEventListener('scroll', debounce(function(e){
   console.log(e);
}, 1000))
```
這邊其實就是用到閉包概念，內部函式會訪問外部函數的作用域。


### Throttle
而 `Throttle` 指的是第一次執行時並不會延遲，而當第二次開始只要使用者一段時間內連續觸發，在 `throttle` 延遲時間內只會執行最後一次。
[Codepen](https://codepen.io/chunwen/pen/PoyOjGp?editors=0010)

```
function throttle(func, delay) {
    // 記下最後一次呼叫的參數
    let lastArguments = null;
    let shouldCall = true;
  
    function execute(){
        if(lastArguments && shouldCall){
            func(...lastArguments);
            lastArguments = null;
            shouldCall = false;
  
          // purpose for delay
          setTimeout(() => {
              shouldCall = true;
              execute();
          }, delay)
        }
    }
  
    return function(...args){
        lastArguments = args;
        execute();
    }
  };

window.addEventListener('scroll', throttle(function(e){
   console.log(e);
}, 1000))
```

### Use case 
1. Debounce   ex: autoComplete
2. Throttle   ex: mouseMove、scrollDown