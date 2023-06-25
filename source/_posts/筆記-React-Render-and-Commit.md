---
title: 筆記-React Render and Commit
tags:
  - react
categories:
  - react
abbrlink: 4145283182
---
前言：
We all know JS is a event trigger language. Therefore, we can found out that `React` Render proccess is some kind of event trigger flow.

<!-- more -->
---
參考資料：
- [Render and Commit](https://react.dev/learn/render-and-commit)


---
We all know JS is a event trigger language. Therefore, we can found out that `React` Render proccess is some kind of event trigger flow.

![react_website](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_ab0decdac63ceb9f19a9ebc0ae7d876e.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1687704010&Signature=vOv6ONN6AUmzZpq0iFZqcKz0r08%3D)

### Step1
There are two reasons for a component to render
1. initial render 
2. when state has been updated

![react_website](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_6fc972fea3e565a6f79892594ec1c337.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1687703959&Signature=MhvYpWfV2cT%2BE8nuuDhKiPbCa6o%3D)


#### What is state?
State is a concept it will only live component ,it helps to remember current value between each render 
[State: A Component's Memory](https://react.dev/learn/state-a-components-memory)


### React render components
> Rendering is React calling your components.
1. first render root component
2. render subsequent renders(process is recursive)


### React commit changes 
> After rendering (calling) your components, React will modify the DOM.
1. initial render, `React` will use `appendChid()` method
2. Re-renders will make dom change at leat as possible

##### Important
React only changes the DOM nodes if there’s a difference between renders.

### Last Step
1. Browser painting
![react_website](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_601f76cbc04c266f759a7e0abed7fdf1.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1687703937&Signature=9GGEMOU7ou0rTyecCZcjD5jisJg%3D)

---
### Conclusion
React trigger 完後會 render， render 後則會接 commit 階段
這時候才會去 appendChild 修改 DOM