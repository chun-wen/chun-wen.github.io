---
title: 筆記-React State Structure
tags:
  - react
categories:
  - react
abbrlink: 255909720
---
前言：
`React` state 結構設計會影響到在撰寫 `Component` 是否會出現一些 UI side effect，如何設計變是很重要的課題。本文整理
官方網站重點以作紀錄。
<!-- more -->
---
參考資料：
- [Choosing the State Structure](https://react.dev/learn/choosing-the-state-structure)

---
## Principles for structuring state
1. group related state
2. flatten deep structure
Like below sample
https://codesandbox.io/s/infallible-sound-843s74?file=/App.js

3. Do not mirror props in state
   Reason: If you pass default props and give it to useState initial value, it will cause components `only render first time`

> If you need to do this, I think you should rename props like initial value to differ from props value and this will clarify new values props are ignore
> Q: Do you know why when user change select color not change ?
> https://codesandbox.io/s/iwgppc?file=/Clock.js&utm_medium=sandpack


1. avoid duplicate state
It's like you put same object in two place just like below 
```jsx=
const initialStatus =[
    {
        key: 'finish', value: 1
    },
    {
        key: 'pending', value: 2
    },
    {
        key: 'fail', value: 3
    }
]
function app(){
    const [status, setStatus] = useState(initialStatus);
    // this is duplicated
    const [selectedStatus, setSelectedStatus] = useState(initialStatus[0]) 
    // we should use index instead like this 
    const [selectedId, setSelectedId] = useState(0) 
    
}
```

> This will cause ui abnormal (you have to remember state is isolated and therefore each time when react reRender it will create a new state object)

### Recap and Remind
- For UI patterns like selection, keep ID or index in state instead of the object itself.
- Avoid redundant and duplicate state so that you don’t need to keep it in sync.
- Don’t put props into state unless you specifically want to prevent updates.