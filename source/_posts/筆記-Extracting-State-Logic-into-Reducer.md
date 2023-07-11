---
title: 筆記-Extracting State Logic into Reducer
tags:
  - react
categories:
  - react
abbrlink: 1197148581
---
前言：
主要就紀錄一下目前 `React` 官網筆記

<!-- more -->
---
參考資料：
- [Extracting State Logic into a Reducer](https://react.dev/learn/extracting-state-logic-into-a-reducer)

---
### Basic Logic
reducer logic is like Declarative and normal way is to change state is imperative way 

### What is Reducer ?
It mainly handle state logic and it receive two parameters 
`currentState` 、 `action` object
```jsx=
dispatch(
// "action" object:
{
  type: 'add',
  message: ''
}
)

```

> Reduce function
```jsx=
function reducerfunction(state, action){
    switch(action.type){
        case 'add':
            return {}
        default:
            return 'default'
    }
}

```

### Notes
React 中 reducer 概念其實跟 Javascript array 方法 reduce 很像。他們都是在拿目前的值跟目前的 action、 接著返回下一個值


### useReducer Hooks 
Will take two parameters
1. reducer function
2. initial state

Returns
1. state value 
2. dispatch function

```jsx=
const [state, dispatch] = useReducer(reducerFunction, initial state)
```


### Reducer writing Hint
- We should only use pure function `not mutate` any more
- Each action describes a single user interaction
- useImmerReducer hooks if you need it 

### Pros 
1. 優點就是可以把 state 邏輯拆開共用，UI 畫面可以更單純處理事件行為
2. 增加可讀性和除錯

### Cons
1. code 必須寫更多行
2. 如果沒有 reduce 概念會看不懂
