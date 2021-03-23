---
title: 2020-12-07-SQL SERVER FOR XML PATH語法介紹
tags:
  - SQL
  - Asp.net
categories:
  - SQL
abbrlink: 3967556948
---
工作上最近一直遇到將不同 `ROW`的抹個欄位值合併起來，記錄一下
<!-- more -->
---
參考資料：
[[食譜好菜] SQL Server 使用「FOR XML」語法做欄位合併](https://dotblogs.com.tw/supershowwei/2016/01/26/145353)
---
情境：
今天我需要將不同 `ROW`的抹個欄位值合併起來，改如何做呢？

```C#
SELECT U.ID,
(SELECT ',' + C.ColumnGroupBy
FROM Table AS C
WHERE C.ID = U.ID
FOR XML PATH('')) AS TEMP 
FROM TABLE_U U
```

加上過濾Distinct 和移除多餘 `,`
```C#
SELECT DISTINCT U.ID,
STUFF((SELECT ',' + C.ColumnGroupBy
FROM Table AS C
WHERE C.ID = U.ID
FOR XML PATH('')) AS TEMP 
FROM TABLE_U U,1,1,'')
```

[參考連結](https://social.msdn.microsoft.com/Forums/en-US/a04bac03-3f72-402f-a7ee-7f7e82b74ed7/remove-null-or-blank-in-stuff-sql?forum=transactsql)

> 補充:
`STUFF` 用法：
STUFF(原字串, 起始位置, 移除長度, 替換字串)
