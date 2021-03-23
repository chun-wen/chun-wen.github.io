---
title: Hexo版本更新教學
tags:
  - Hexo
categories:
  - Hexo
abbrlink: 1226560276
---
本篇文章主要紀錄更新Hexo到5.4版本時，所遇到的一些問題。
<!-- more -->
---
參考資料：
[試著學 Hexo-番外篇之更新 Hexo](https://ithelp.ithome.com.tw/articles/10253367)
[Hexo官網](https://theme-next.js.org/)
---
### 前言
其實一開始我並沒有打算要更新 `Hexo`版本，我只是想替我的網站嵌入`GA`觀察一些文章數據流量。只是不幸地是，正當我以為我將`GA`嵌入後，在終端機上手賤不小心更新 Next主題 `npm install hexo-theme-next@8.0.0`，結果我的網站在執行指令`hexo clean && hexo d -g`發佈時整個就呈現下圖情況。
![示意圖](https://i.imgur.com/tUw0lJ3.png)

後來用關鍵字，`{% extends '_layout.swig' %}` Google一下發現好像是hexo在5.0之後，把`swig`刪除，必須手動安裝。
指令如下：
` npm i hexo-renderer-swig`
但，我在下完指令後，畫面雖然正常多了，但是文章內的內容都消失，看不到了。因此，以下就來說明，我如何更新方法。

### 操作步驟
1. 將 `themes/next` 主題全部刪除

2. 再重新安裝一次hexo cli `npm install -g hexo-cli`
小提醒：Hexo 5.0以後，Node.js 至少要10.13.0以上

3. 接著`npm install`，這樣就可以把 `hexo` 所需檔案下載下來

4. 再來，我們必須下載主題，我用的是 `Next`。一樣在`cmd`上，下`npm install hexo-theme-next@latest`
過往我們是透過`git clone next`主題到資料夾下，現在可以改用`npm`

5. 安裝完後，可以下`hexo-v`看一下目前安裝版本為何

6. 最後，就是客製化調整 `themes/_config.yml` 內配置摟～
這時候你可能會需要安裝一些hexo內部套件或是其他第三方套件，這部分就留給下一篇再來說明。

7. 最後發佈前，建議把`.deploy_git`資料夾全部移除，因為我就發生下面問題
`Error: ENOTEMPTY: directory not empty hexo`，解決方式就是直接移除`.deploy_git`資料夾就可嘍



