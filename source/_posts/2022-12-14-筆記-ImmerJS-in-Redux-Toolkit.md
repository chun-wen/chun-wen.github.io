---
title: 2022-12-14-筆記-ImmerJS in Redux Toolkit
tags:
  - React
  - Redux
  - ImmerJS
categories:
  - React
abbrlink: 4038663728
---
前言：
`Redux Toolkit` 算是專案上很常用到的 Tool，我們過往在對資料進行整理時都會遇到 `Redux` 要求我們資料不能直接 `mutable`，因此我們就必須針對陣列或是物件進行解構
而這樣當然可以 work ，而 `Immer.js` 提供我們一個更好的方式來處理 `mutable` 資料

<!-- more -->
---
參考資料：
[Redux Toolkit 官網介紹](https://redux-toolkit.js.org/usage/immer-reducers#basics-of-immutability)

---
### Redux Rules

- **reducers are *never* allowed to mutate the original / current state values**

```tsx
// illegal
state.value = 123;
```

- old written rules

```tsx
// ✅ This is safe, because we made a copy
return {
  ...state,
  value: 123,
}
```

### Redux with Immer.js

immer.js 提供 `produce` function，接受兩個參數。第一個是， 原本的 `state` (immutable)，第二個是 callback function。在 callback 中他會接受 草稿(未更新) state，而我們可以在這裡進行 mutate 操作。

⇒ 表面上看起來是 mutate 操作，但實際上不是。

而我們在 CreateReducer API 內部已經提供內建 immer.js 

### Immer.js Usaga Patterns

- 記得 mutate 必須是 object 或是 array
- **Immer expects that you will `either *mutate* the existing state`, *or* c`onstruct a new state value yourself and return it`, but *not* both in the same function!**
- Arrow function 不能 return，因為 immer.js 會遇到 `attemped value` 跟 回傳 `value`。他不知道要用哪一個 ⇒ 可是專案這樣寫卻不會錯，我也不知道為什麼
    
    ```tsx
    export const solutionSlice = createSlice({
      name: 'calculator',
      initialState: {
        solutionData: []
      },
      reducers: {
        getSolutionData: (_state, action) => ({ ..._state }),
        setSolutionData: (state, action) => {
          const { solutionData, saleTags } = action.payload;
          return { ...state, solutionData, saleTags };
        }
      }
    });
    ```
    
- 遇到巢狀可以這樣寫
    
    ```tsx
    function objectCaseReducer1(state, action) {
      const { a, b, c, d } = action.payload
      return {
        ...state,
        a,
        b,
        c,
        d,
      }
    }
    
    function objectCaseReducer2(state, action) {
      const { a, b, c, d } = action.payload
      // This works, but we keep having to repeat `state.x =`
      state.a = a
      state.b = b
      state.c = c
      state.d = d
    }
    
    function objectCaseReducer3(state, action) {
      const { a, b, c, d } = action.payload
      Object.assign(state, { a, b, c, d })
    }
    ```
    
- 如果要更新或取代，就必須這樣寫，必須要 `return`

```tsx
const initialState = []
const todosSlice = createSlice({
  name: 'todos',
  initialState,
  reducers: {
    brokenTodosLoadedReducer(state, action) {
      // ❌ ERROR: does not actually mutate or return anything new!
      state = action.payload
    },
    fixedTodosLoadedReducer(state, action) {
      // ✅ CORRECT: returns a new value to replace the old one
      return action.payload
    },
    correctResetTodosReducer(state, action) {
      // ✅ CORRECT: returns a new value to replace the old one
      return initialState
    },
  },
})
```