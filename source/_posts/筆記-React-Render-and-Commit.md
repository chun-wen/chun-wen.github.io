---
title: 筆記-React Render and Commit
tags:
  - react
categories:
  - react
---
前言：
We all know JS is a event trigger language. Therefore, we can found out that `React` Render proccess is some kind of event trigger flow.

<!-- more -->
---
參考資料：
- [Render and Commit](https://react.dev/learn/render-and-commit)


---
We all know JS is a event trigger language. Therefore, we can found out that `React` Render proccess is some kind of event trigger flow.

![react_website](https://hackmd.io/_uploads/B1ji62rd3.png)

### Step1
There are two reasons for a component to render
1. initial render 
2. when state has been updated

![react_website](https://hackmd.io/_uploads/HJcTZTrdh.png)


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
![react_website](https://hackmd.io/_uploads/SyWMH6SOn.png)

---
### Conclusion
React trigger 完後會 render， render 後則會接 commit 階段
這時候才會去 appendChild 修改 DOM