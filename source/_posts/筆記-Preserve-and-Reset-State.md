---
title: 筆記-Preserve and Reset State
tags:
  - react
categories:
  - react
abbrlink: 770701894
---
前言：
紀錄一下 `React` 筆記。

<!-- more -->
---
參考資料：
- [Preserving and Resetting State](https://react.dev/learn/preserving-and-resetting-state#recap)

---
React will create React Tree, it make React Dom by JSX 
![react_dom](https://i.imgur.com/2LmgZdm.png)

### Recap
1. React will preserve state when position not change(React Dom Tree not change place)
2. If you want to reset or update you can give key or put component in different structure
3. If you destroy component，React will reset state value
4. We should not contain components in another components
This is because inside components every time will cause reRender issue and otherwise state will not keep anymore 
This leads to bugs and performance problems. 
Just like below 
```jsx=
import { useState } from 'react';

export default function MyComponent() {
  const [counter, setCounter] = useState(0);

  function MyTextField() {
    const [text, setText] = useState('');

    return (
      <input
        value={text}
        onChange={e => setText(e.target.value)}
      />
    );
  }

  return (
    <>
      <MyTextField />
      <button onClick={() => {
        setCounter(counter + 1)
      }}>Clicked {counter} times</button>
    </>
  );
}

```
[codesendbox](https://codesandbox.io/s/recursing-framework-f983s8)
5. Don’t nest component definitions, or you’ll reset state by accident.