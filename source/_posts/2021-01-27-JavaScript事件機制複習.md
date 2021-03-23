---
title: 2021-01-27-JavaScript事件機制複習
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 1363835460
---
記錄一下今天專案上遇到跳窗事件，重複觸發Alert訊息問題。
<!-- more -->
---
參考資料：
[JavaScript 所謂的「停止事件」到底是怎麼一回事？](https://ithelp.ithome.com.tw/articles/10198999)
[重新認識 JavaScript: Day 14 事件機制的原理](https://ithelp.ithome.com.tw/articles/10191970)
[event.preventDefault()跟return false的差別是?](https://yiyingloveart.blogspot.com/2013/08/eventpreventdefaultreturn-false.html)
---
### onclick 和 addEventListener 差異
1. 兩者都可以針對同一個`DOM`綁定不同事件
2. `onclick`若綁定多個事件，只會顯示最後一個綁定的事件，前面事件會被複寫，這在接手前人專案時必須留意。
3. `addEventListener` 也可以綁定多個事件，但不會被前面事件複寫。


### 事件原理
![事件機制](https://i.imgur.com/IdQiL3Z.png)
事件有兩種機制，冒泡和捕捉。而我們有時候將事件綁定放在子元素時，就會造成事件也觸發父層問題。
因此我們可以透過`event.stopPropagation()`來阻止事件冒泡。

而在專案中很常使用`JQuery`的`return false`則會幫我們執行
1. `event.stopPropagation()`
2. `event.preventDefault()`
3.  停止callback function 執行。