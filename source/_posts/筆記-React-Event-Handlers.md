---
title: 筆記-React Event Handlers
tags:
  - react
categories:
  - react
abbrlink: 1982926587
---
前言：
紀錄一下 `React` 筆記。

<!-- more -->
---
參考資料：
- [DOM 的事件傳遞機制：捕獲與冒泡](https://blog.techbridge.cc/2017/07/15/javascript-event-propagation/)
- [Responding to Events](https://react.dev/learn/responding-to-events)
---

1. React 事件命名會以 `handle` 開頭
2. Usually defined inside components

### Pitfall
```jsx=
<button onClick={handleClick()}>
```
JavaScript inside the `JSX {}` executes immediately
Therefore, this will not have any interaction with your UI

#### Correct Way
1. inline anonymous function
```jsx=
<button onClick={() => handleClick()}>
```
2. pass a function
```jsx=
<button onClick={handleClick}>
```
3. pass a function
```jsx=
<button onClick={function handleClick(){
   alert('click');  
}}>
```

### Conclusion
1. Don't execute function instead you should pass function


---
### Event handlers as props
1. usually start with `on` and followed by a capital letter
```jsx=
export function PlayButton({ onPress , children}){
   
  return (
     <button onClick={onPress}>
       {children}
     </button>
  )
}

export function App(){
    return(
        <PlayButton onPress={() => alert('hi')}> 
            hihihihihi
        </PlayButton>
    )
}
```

### Event stopPropagation
1. 阻止事件冒泡
2. 要在捕獲階段下 stopPropagation