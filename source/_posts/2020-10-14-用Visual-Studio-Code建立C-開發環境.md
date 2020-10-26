---
title: '2020-10-14-用Visual Studio Code建立C#開發環境'
date: 2020-10-14 23:23:52
tags:
  - C#
  - Asp.net
categories:
  - C#
---
記錄第一次在Vs Code上安裝 `.Net Core`的過程。
<!-- more -->
---
參考資料：
[利用 Visual Studio Code 建立 C# 專案 :-: C# 專案開發入門的八堂課](https://www.youtube.com/watch?v=Mg_MtwKDgek&feature=youtu.be)

---
1. 安裝時，可以先到官網看一下需要安裝什麼套件[在 macOS 上安裝 .NET Core](https://docs.microsoft.com/zh-tw/dotnet/core/install/macos)
2. 由官網得知，`.NET Core` 是由`執行時間`和 `SDK` 所組成
執行時間是用來執行 .NET Core 應用程式，SDK 是用來建立 .NET Core 應用程式和程式庫。
3. 下載網址 https://dotnet.microsoft.com/download/dotnet-core/3.1
4. 安裝完成後可以在終端機執行 
`dotnet new console`就可以建立專案摟～

### Bug
- 若遇到dotnet command not found，請先注意指令是否有拼錯。

- 出現It was not possible to find any installed .NET Core SDKs C# 問題
解決方式：在json.setting中加入
```javaScript
{    
  "omnisharp.useGlobalMono": "never"
}
```
[連結](https://github.com/OmniSharp/omnisharp-vscode/issues/4134)




