---
title: 2020-09-30-看鐵人賽學Debug-Network-Filter篇
tags:
  - chrome
  - debug
categories:
  - web
abbrlink: 2885820487
date: 2020-09-30 21:22:27
---
今天筆記內容整理自[[Day 16] Network - Filter & Search Requests](https://ithelp.ithome.com.tw/articles/10246590)
<!-- more -->
---
參考資料：
[[Day 16] Network - Filter & Search Requests](https://ithelp.ithome.com.tw/articles/10246590)
---
### Filter
Filter可以幫助我們過濾過多的request，快速找到需要的請求！

#### By Properties
![圖示](https://i.imgur.com/o57rt8L.png)
非常強大！最前方加`-`，就是剔除意思！
> 常見條件如下
* domain
* is
* larger-than
* method
* status-code
* Cookie系列 如 `set-cookie-domain`



