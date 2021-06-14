---
title: Clean Code系列-原則
tags:
  - JavaScript
categories:
  - JavaScript
  - CleanCode
abbrlink: 1773690215
---
前言：
近期在開發公司內部產品系統時，寫完後再進行功能測試時，往往會遇到蠻多 bug ，一方面是自己未考慮周全，另一方面也是因為自己在撰寫上有些壞習慣。因此，希望藉由 Clean Code 這本書協助自己撰寫 JavaScript 本質上優化、讓程式能夠更具可靠性。而此系列文章就是用來紀錄 Clean Code 這本書相關重點內容。
<!-- more -->
---
參考資料：
[Clean Code學派的風格實踐：開發可靠、可維護又強健的JavaScript](https://www.books.com.tw/products/0010886265?loc=M_0009_020)
---
## Clean Code 原則
### 1. 可靠性

- 正確性：需求是否明確？如：Email驗證
- 穩定性：不同條件下，相同 Function 能否穩定提供一樣效果？
- 彈性：是否有容錯率？發生非預期錯誤能否可以繼續使用？

### 2.  效率

- 時間：使用者等待時間是否過長？
- 空間：上傳下載檔案大小限制能否壓縮？

### 3. 可維護性

- 適應性：能否依據不同情境自適應呢？
- 熟悉性：不同 programmer 是否能輕易接手？

### 4. 可用性

- 易讀性：所有使用者能否簡單直覺了解 Function 目的？
