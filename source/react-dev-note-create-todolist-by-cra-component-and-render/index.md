---
title: 建立初始 todo list 畫面 (介紹 component ＆ What is render)
date: 2021-03-22 00:46:49
---

# 目的

建立 todo list 的`初始畫面`

## Step 1. 建立 CRA 專案，[請參照](../react-dev-note-create-environment)

## Step 2. 建立 class component

先上 code

```js
import { Component } from "react";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div>
        <header className="todo-header">
          <input />
          <button>save</button>
        </header>
      </div>
    );
  }
}
export default App;
```
在說 class component ，我們要先了解 component 

### 什麼是 component

它就是封裝了 **一部分畫面的** 結構、樣式 、邏輯，以這樣為`一個單位`

component 擁有以下特性：

- 邏輯獨立性
- 可重複性
- 可組合性
- 封閉性

### 以 class 建立 component

以宣告 es6 class 類別，並繼承自 **React.component**，  
有以下特點：

- 內建 state 機制，保存邏輯相關資訊，並可以
- 並可覆寫`生命週期(Life cycle) `，可在每個生命週期 的 hook 處理相關的事情

又被稱為 **stateful component**

## Step 3. 建立顯示畫面

### 什麼是 render
react component life cycle 之一 ， 更改真實DOM前的最後一個動作  

在 **class component** 裡是`必須`要實作的 function ， return 此 component 的 `react element tree`  

### 什麼是 react element

它是在 react 裡最小的單位，
它並不是 **component** ，也不是 **component 的 instance**，也不是 **virtual DOM**，  
就只是一個`純物件(plain object)`， 描述關於此節點`最終輸出`的畫面內容，

那裡面會包含兩個參數， type and props

- type 來決定是 DOM node or Component
- props 就是關於此 element 屬性的內容

它的建立有兩種：

- 用 **jsx** 就是像 html tag 一樣
- 用 **function** 可以使用 `React.createElement` 來建立