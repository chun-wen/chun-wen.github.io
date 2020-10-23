---
title: 2020-10-19-.Net Framework簡介
date: 2020-10-19 22:28:41
tags:
  - C#
  - Asp.net
categories:
  - C#
---
簡介`.Net Framework`
<!-- more -->
---
參考資料：
從零開始學Visual C#2015程式設計
---
`.Net Framework`包含兩大元件，CLR(共通語言執行環境)、和類別庫(Class Library)
前者是應用程式執行的環境，後者則是提供Using類別

### C#特點
- `C#`是一個物件導向語言(OOP)，微軟稱他為`Visual C#`
- 基於`.Net框架`的程式語言。
- 編譯式語言

### C#運作流程
1. Source Code
2. 轉譯(編譯器)
3. 中繼語言(MSIL) 目的可以跨語言(C#/C++/VB)
4. CLR           一個虛擬元件，用來運行.Net
5. 電腦看得懂的語言

### C#跟.Net關係
C#是一個程式語言， `.NET`則是平台框架

### Asp.net 
基於`.Net Framework`框架中所提供的Web應用程式類別庫，封裝在 `System.Web.dll` 檔案中
檔名叫 `.cshtml`

### 方案與專案差異
- 方案檔名是`.sln`
- 專案檔名是`.csproj`


### 命名空間
相同性質

`[]`：宣告陣列用
`<>`:使用泛型會使用到
```C#
string[] args
```


