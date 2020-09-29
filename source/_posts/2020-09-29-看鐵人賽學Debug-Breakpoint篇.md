---
title: 2020-09-29-看鐵人賽學Debug-Breakpoint篇
date: 2020-09-29 22:35:49
tags:
   - chrome
   - debug
categories:
   - web
---
今天紀錄Debug-Breakpoint篇，內容整理自[[Day 12] Sources - Breakpoints](https://ithelp.ithome.com.tw/articles/10244199)

<!-- more -->
---
參考資料：
[[Day 12] Sources - Breakpoints](https://ithelp.ithome.com.tw/articles/10244199)
---
### Source斷點
> 右鍵點擊行號可以看到其他標記
* `Add logpoint` – 如同插入一個 console.log
* `Add conditional breakpoint` – 可以加入條件，執行結果不如預期時才中斷
*  `Never pause here` – 可用來跳過 debugger

1. `logpoint`,可以直接在Source上修改程式且重整夜還是會保留。

### DOM斷點
> 直接右鍵點擊可以看到三種斷點
* Subtree modifications – 該節點內的發生變化，如子節點的新增或刪除
* Attribute modifications – 節點本身的 attribute 有新增、刪除、修改
* Node removal – 該節點被移除，同時 DOM 斷點也會消失。

### EventListener 
綁定事件如:Mouseleave、keydown。操作方法可以參考資料來源。

### Exception
出現錯誤時暫停。
目的：能在錯誤出現的當下，檢查是否有不預期的錯誤發生。

