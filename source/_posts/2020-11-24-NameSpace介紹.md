---
title: 2020-11-24-NameSpace介紹
tags:
  - C#
  - Asp.net
categories:
  - C#
---
今天認識NameSpace
<!-- more -->
---
參考資料：
[T003_Methods_Static_namespace](https://ithandyguytutorial.blogspot.com/2017/11/t003methodsstaticnamespace.html)
---
### NameSpace
可以包含 NameSpace 、 Class 、 InterFace 、 enum

```C#
using System;
using AA = androidWebApi.Test //使用 NameSpace 別名
namespace androidWebApi.Controllers
{
   public class uploadController : ApiController
    {

    }
}

```