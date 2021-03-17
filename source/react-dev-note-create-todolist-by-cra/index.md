---
title: 以 CRA 建立 todo list
date: 2021-02-23 18:05:27
---

# todo list

## Component

在 react 是以 component 為基礎單位

### 特色：

- 封裝性
- 可重複使用
- 可組合
- 單一資料流
- jsx 語法

### 簡介

- component 命名以`大駝峰命名(upper camel case)`，否則會報錯
- html element 對應到 react 的 attributes 的命名：
  - 基本上會以 `小駝峰命名(lower camel case)`
  - class => className
  - for => htmlFor
- style 內容格式是 **js object**
  - attributes 改以`小駝峰命名(lower camel case)`

## jsx 語法

全名為 **javascript XML** ， 是以模擬 html 標籤語法來建立 react element ，來簡化生成時的複雜度

```js
//create react element function
const hello = React.createElement("h1", null, "Hello World");

//jsx
const hello = <h1>Hello World</h1>;
```

## 建立 class component

以 ES6 class 語法糖來宣告並 `extend React.Component`，來建立 component

```js
class App extends Component {
  render() {
    // jsx
    return <div>Hello React</div>;
  }
}
```

### 特色：

- 具有 state 機制，可內部自行控制 component `update` 時機
- 可在 class 內部 override **生命週期** function

### render

- component 的生命週期之一
- 在 class component 內必須實作的 function， 需有返回值
- **返回值**為將要顯示的畫面，其型別可以有：
  - react elements
  - arrays ＆ fragments
  - string or number
  - boolean or null

### virtual dom

- 以 js object 結構 來模擬 `real dom`
- 所有的操作都是針對 virtual dom，在改變完後才判斷是否要更新 `real dom`
- 在 virtual dom 上的變化會映射到  `real dom`

## state & props

### props

- 由 **開發者** 決定`開放`給 **使用者** 從外部傳入內部去影響 component 狀態的參數
- 從外部傳入內部的參數都會放進 `props` 屬性裡，以物件`key-value`保存
- props 其值是被 呼叫此 component 的所決定的
- 屬性是**唯讀**的，不能改動其值，也**不應該**在內部重新賦值給 props
- 能改變 props 值，只有在外部傳入直發生改變時
- 改變時會觸發 component 的 update 流程

### state

- 代表 component 內部的狀態，會影響內部 rendering or data flow
- 封裝在 component 內部， 不會流傳到外部
- 一個純物件參數，`key-value` 形式 ，內容應該是**可序列化**
- 只在 component 內部
- 需要 rendering or data flow 的資料都**應該**放在 state
- 除了**初始化**，否則**不應該**直接改動 state

#### 宣告 初始值

- 在 constructor 宣告 state 初始值

```js
  constructor() {
    super();
    this.state = {
      todoList: [],
    };
  }
```

- 在 class 內部直接宣告

```js
class App extends Component {
  state = {
    todoList: [],
  };
}
```

### this.setState

更新指定 state ， 並觸發 component 的 update 的流程

```js
this.setState(updater, [callback]);
```

- updater 有兩種模式
  - object
    - 是以 key-value 方式來更新指定 state value
  - function
    - 是會接收`當下`的 state & props ，可以以此為參考基礎來進行更新， return `object` 包裹需要更改的值
- `callback` 會在更新流程結束後去執行

```js
//object
this.setState({ text: "hello!" });

//function
this.setState(function (state, props) {
  return {
    text: "hello",
  };
});

//use callback
this.setState(
  function (state, props) {
    return {
      text: "hello",
    };
  },
  function () {
    console.log(this.state);
  }
);
```

#### 注意

- **setState** 是`非同步`
- 一次 update 代表一個`循環(cycle)`
- 假如同一循環同時執行多次 `setState` ， 會依順序更新，但更新循環只會有**一次**
- 如果需要根據當下 state 值去更新，請用 function 來取得當下最即時的 state

## ref
可獲取指定 dom node or react element 內容，
通常是無法透過 dataflow 來控制畫面的變化，從而需要`直接操作`元素本身  
像是以下情境：
  - input value
  - video play
  - scroll 位置  

### 用法 
- 在 constructor 裡使用 `createRef` function 建立 ref 參考
```js
  constructor(props) {
    super(props);
    this.inputRef = createRef();
  }

```
- 在 render function 裡，在指定 component | element 放入 **ref** props
```js
  render() {
    return (
      <div>
        <header className="todo-header">
          <input ref={this.inputRef} />
          <button onClick={this.createTodoItem}>save</button>
        </header>
      </div>
    );
  }

```

## 用 ReactJs 建立 Todo List

### source code

### 功能

- 讀取 todo list
- 新增 todo item
- 刪除 todo item
