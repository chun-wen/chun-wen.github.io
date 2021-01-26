---
title: 2021-01-26-out、void、ref說明
tags:
  - Asp.net
  - C#
categories:
  - C#
---
今天在撰寫專案時，突然忘記`out`使用方式，索性今天晚上複習一下其他參數修飾詞。
<!-- more -->
---
參考資料：
[C# Method - Main、void、ref、out、overloading - 教學筆記](https://adon988.logdown.com/posts/1179503)
[[C#] Out 與 ref 差異](https://dotblogs.com.tw/erictsaiblog/2015/05/10/151238)
---
### void
當method不回傳值時，就必須使用 `void`類型
```C#
namespace demo
{
  class Test
  {
    static void Hello(){
      console.WriteLine("11");
    }
  }
}

```

### Reference
必須先給定初始值，會將變數記憶體位置傳給`Methods`
```C#
namespace demo
{
  class Test
  {
    static void Hello(){
      int a = 10;
      Calculate(ref a);
      console.WriteLine(a); //100
    }

    static void Calculate(ref int a)
    {
      a = a *10;
    }

  }
}

```
### Out
不需給定初始值，但必須在程式結束前需要初始化參數(給值)
```C#
namespace demo
{
  class Test
  {
    static void Hello(){
      Calculate(out a);
      console.WriteLine(a); //33
    }

    static void Calculate(out int a)
    {
      a = 33;
    }

  }
}

```

### 小結論
1. ref 需要將參數初始化而Out 不需要
2. Out 與 ref 都是以 By Reference 作為參數傳遞
3. ref 需要在執行前初始化參數(給值)而 out 是在程式結束前需要初始化參數(給值)

