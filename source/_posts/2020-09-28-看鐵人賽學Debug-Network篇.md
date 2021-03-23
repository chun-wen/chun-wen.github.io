---
title: 2020-09-28-看鐵人賽學Debug-Network篇
tags:
  - chrome
  - debug
categories:
  - web
abbrlink: 3096729793
date: 2020-09-28 23:20:02
---
今天學習認識Chrome面板中的ＮetWork,文章內容整理自[[Day 15] Network - Overview & Settings](https://ithelp.ithome.com.tw/articles/10245891)
<!-- more -->
---
參考資料：
[[Day 15] Network - Overview & Settings](https://ithelp.ithome.com.tw/articles/10245891)
---
### 整理筆記如下
1. 預設Network Log會按照執行順序排列
2. Preserve log用來保留`Network Log紀錄`,可以避免在畫面跳轉時清掉`Network Log紀錄`
3. Disable cache 用來模擬第一次使用者登入
4. Throttling 可以用來模擬低網速環境問題
5. Import/Export HAR file 用來分析網頁效能問題
因為下載檔案為.har格式，所以可以直接用這個網站開啟[HAR Analyzar](https://toolbox.googleapps.com/apps/har_analyzer/)

