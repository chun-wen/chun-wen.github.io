---
title: 2020-10-04-看鐵人賽學AJAX-用Chrome Dev觀察Network運作流程
date: 2020-10-04 11:45:32
tags:
   - AJAX
   - JavaScript
categories:
   - JavaScript
---
今天我們將透過Chrome開發者工具來了解非同步請求背後發生什麼事。就讓我們看下去吧！
> 註記：`看鐵人賽文章內容`僅用於紀錄、整理其他參賽者文章，若文章有不合適之處，可以於文章下方留言區告知，我會移除文章。謝謝！
<!-- more -->
---
參考資料：
[AJAX 完整解說系列：使用 Chrome Devtools 檢視請求及回應](https://ithelp.ithome.com.tw/articles/10247837)
[API來源](https://jsonplaceholder.typicode.com)
[transferred-over-network-size](https://stackoverflow.com/questions/62184624/transferred-over-network-size-larger-than-resource-size)
---
前言：
首先，打開[連結](https://cdpn.io/chunwen/debug/XWdvMao/ZoMBazDPyvOk)，再把開發者工具打開後畫面如下：
![圖示](https://i.imgur.com/BUkuVht.png)

> 題外話：
我們可以看到本次請求，下方顯示`Transfer network`是321B，而`Resource`卻只有83B。
看到時滿臉疑問，傳輸時檔案不是會被壓縮大小嗎？怎麼會比原始資料大呢？因此，找了[文章](https://stackoverflow.com/questions/62184624/transferred-over-network-size-larger-than-resource-size)才發現
原來：
1. `Transfer network` 計算大小是以整個請求(包含 url, request headers, request body, response headers and response body)大小加總計算
2. `Resource`只會計算接受到的`Response body`中的`Content-length`

接下來點選XHR連結後，我們可以看到下面幾項類別。
![圖示](https://i.imgur.com/rnI6q59.png)
1. Headers: 請求及回應的標頭。Headers 所挾帶這些資訊，不管是瀏覽器、伺服器都會有一份。
2. Preview, Response：兩者資訊相同，只是Preview比較好閱讀而已。
3. Timing：本次請求至回應所耗費的時間。
4. Cookie：本次請求、回應相關的 Cookie 內容。

### Headers
請求及回應的標頭。Headers 所挾帶這些資訊，不管是瀏覽器、伺服器都會有一份。

#### General
請求的描述內容，如 Request URL、Request Method 、 Status Code

#### Response Headers
回應表頭，由伺服器回傳至瀏覽器端的表頭
* access-control-***: 跨網域資源，包含是否允許跨網域存取、驗證等資訊。
* content-encoding: 後端回應的壓縮檔案方式如: br，代表 Brotli 壓縮格式，常見於壓縮文字檔。
* content-type: 後端回傳的資料格式，現在多為 `application/json; charset=utf-8`
* set-cookie:後端寫入瀏覽器端的 cookie資訊。

#### Request Headers
請求表頭，請求的內容必須符合後端伺服器接受格式。如傳送資料格式、方法等。
> 簡單來說就是必須照 API 文件進行
* method: 請求方法如：POST、 GET 、 PATCH
* accept: 提供給後端了解前端所能接受的資料類型
* user-agent: 提供給後端發出請求的瀏覽器資訊。如行動版或桌機版
* authorization: 驗證資訊。如後台新增產品時就可以夾帶此資訊。
* accept-encoding: 告訴後端伺服器能接受的壓縮格式如：gzip, deflate, br

#### Request Payload、Query String Parameter
當請求時需要帶入更多資源，如上傳資料、取得特定索引時，就會利用到 Request Payload、Query String Parameters。

### Timing
![圖示](https://i.imgur.com/hgTBDR8.png)
網頁開啟後，前端網頁發送請求到瀏覽器接受後端回應資料時間。
* Connection Start: 
  1. 伺服器尚未接受到請求，因此影響這段時間為`網路服務`、`電信商`
* Request/Response: 
  1. Waiting (TTFB): 伺服器接收到第一個字節直到伺服器產生回應的時間，這段取決於`伺服器的距離`、`處理效能`等等。
  2. Content Download: 資源下載的所花費時間，取決於用戶、伺服器兩者的頻寬、距離等因素。
