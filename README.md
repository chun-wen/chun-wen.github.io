### 常見指令
```git
Step1.建立新文章(參考一)
$ hexo new [layout] <title>    //layout預設為post

Step2.建立分類、標籤
$ hexo new post categories     //建立分類
$ hexo new post tags           //建立標籤

$ hexo generate  //產生靜態檔案
$ hexo deploy    //部署網站
$ hexo clean &&  hexo d -g  
//刪除已生成的靜態頁面及快取檔案，並重新部署
提醒：部署網站前會需要先產生靜態頁面

組合技
$ hexo d -g         //＊指令說明： # 產生靜態檔後部署
$ hexo s -g        //＊指令說明： # 產生靜態檔後預覽
$ hexo clean     //＊指令說明：刪除已生成的靜態頁面及快取檔案
$ hexo new [title]  //＊指令說明：建立新文章
```