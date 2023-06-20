---
title: 筆記-React LifeCycle
tags:
  - react
categories:
  - react
abbrlink: 941265307
---
前言：
紀錄一下 `React` 筆記。

<!-- more -->
---
參考資料：
- [請解釋 React 生命週期？](https://www.explainthis.io/zh-hant/interview-guides/react/react-lifecycle)
---
React 的生命週期分為三個主要階段：mounting、updating、unmounting。

## Mounting
在 mounting 階段，元件被創建並添加到 DOM 中。這個階段方法依序是 `constructor`、`render` 和 `componentDidMount`。

- `constructor` 用於宣告( declare )初始化狀態（state）和綁定事件處理函式

```jsx
class Counter extends Component {
  // initial props
  constructor(props) {
    super(props);
    this.state = { counter: 0 };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    // 
  }
}
```

### 注意事項：
1. 不能執行任何 side effects 或是 訂閱 (這個階段是在 render 階段)
2. 唯一一個可以直接指定 `this.state` 方法
3. 必須寫 `super(props)` ⇒ 不然 `this.props` 會 undefined

- `render` 負責生成元件的虛擬 DOM
- 而 `componentDidMount` 則在元件被掛載後觸發，通常用於 data fetching, 事件訂閱和 Dom node 控制

## Updating
在 updating 階段，元件的狀態或屬性發生變化，導致元件需要重新渲染。

方法依序 `getDerivedStateFromProps` 、 `shouldComponentUpdate`、`render`、`getSnapshotBeforeUpdate()` 、`componentDidUpdate` 。
通常 `shouldComponentUpdate` 這階段可以用來做一些效能優化，因為這階段主要是 React 用來判斷是否需要更新。

`render` 和 `componentDidUpdate` 與 mounting 階段的用法類似，負責渲染和更新 DOM。而 `getDerivedStateFromProps` 則允許從新的屬性中更新狀態。


## Unmounting
在 unmounting 階段，元件從 DOM 中被移除。這個階段方法是 `componentWillUnmount`，在元件被卸載之前觸發，常用於清除計時器、取消訂閱或釋放資源等清理工作。