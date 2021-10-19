---
title: react-router note
date: 2020-06-15 03:19:09
---

# What

- 控制 Url 使其只會在 **本地端(Local)** 作用
- 以 **Url 路徑** 來管理 Components 的組成

# How

## Install

> npm install react-router-dom

## Basic

```js
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

export default function App() {
  return (
    <Router>
      <div>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/topics">Topics</Link>
          </li>
        </ul>

        <Route path="/about">
          <About />
        </Route>
        <Route path="/topics">
          <Topics />
        </Route>
        <Route path="/">
          <Home />
        </Route>
      </div>
    </Router>
  );
}
```

### Router

- 路由器，控制 Url 的導向位置
- 並監視其變化，判斷會符合那個 **Route**
- 所有的路由行為皆在路由器裡實現
- 沒有加裝 **Switch** ：
    - 舊 Component 會先 **Unmount** 
    - 新 Component 再 **Mount**
- 有加裝 **Switch** ：
    - 同樣類型、並有相同的 **key** or 尚未設定 **key**  ，會被判定為相同的 Component ， 進行 Update
    - 非上述狀況，一律參照`未加裝 Switch `
- 分為：
  - BrowserRouter
    - 預設以 **Domain Url/** 為 root
  - HashRouter
    - 預設以 **Domain Url/{hashType}/** 為 root

#### BrowserRouter

- basename : string
  - 設定 **root Url**
  - 預設為 **Domain Url/**
- getUserConfirmation : func
  - 自定切換 Url 時的 Confirm
  - 需要帶有 `<Prompt/>`，才會執行
  ```js
  // msg = 確認訊息
  // cb = 是否跳轉畫面，true： 跳轉 ，false:取消
  const confrimChange = (msg, cb) => {
    const allowChange = window.confirm(msg);
    cb(allowChange);
  };
  ```
- forceRefresh : bool
  - 在切換 Url 時，會 Refresh 網頁，代表會向 Server 再要一次資料
  - 預設為 false
- keyLength: number
  - 設定 object location.key 長度
  - 預設長度為 6
- children : node
  - 要實現的路由規則

#### HashRouter

- basename : string
  - 設定 **root Url**
  - 預設為 **Domain Url/{hashType}/**
- getUserConfirmation : func
  - 自定切換 Url 時的 Confirm
  - 需要帶有 `<Prompt/>`，才會執行
  ```js
  // msg = 確認訊息
  // cb = 是否跳轉畫面，true： 跳轉 ，false:取消
  const confrimChange = (msg, cb) => {
    const allowChange = window.confirm(msg);
    cb(allowChange);
  };
  ```
- hashType : string
  - 設定 `window.location.hash` 的表示方法
  - 型態：
    - slash
      > Domain Url/#/{action}
    - noslash
      > Domain Url/#{action}
    - hashbang(ajax crawlable)
      > Domain Url/#!/{action}
- children : node
  - 要實現的路由規則

### Route

- 路由，設定好路徑(path)，當 Url 符合到 Route，觸發設定好的動作
- 如在同一個 **Route match** ，當 **path** 為 array:
    - 以 **key** 值去判斷是否為同一個 Component
    - 不是同一個會把舊 Component Unmount
    - 再 mounting 新的 Component
- 如有多個 Route，讀取規則:
  - 由上至下
  - 把有符合到的 Route 給 render 出來
  - 未符合到的 Route return null
- 假如在樹狀同一個節點、不同的 Route 裡，指定相同的 Component：
  - 設定 `key`， 會被當成不同的 Component ，即有兩個一樣的 Component
  - 未設定 `key`，會被當成相同的 Component ，每一次切換只是在 Update Component
- render method:
  - 當以 **func** 設定時，會把以下三種物件包成 props object：
    - location
    - history
    - match
  - component : func | class
    - 當 Url 有 match 到才會觸發
    - 以 **React.createElement** 建立新的 `React Element`
  - render : func
    - 當 Url 有 match 到才會觸發
  - children : func | component
    - 不管 Url 是否 match 皆會觸發
      - 不符合， props.match == null
      - 符合， props.match != null
    - 有裝 `<Switch>` 只會 match 時顯示
    - 以 Component 形式呼叫，只會 match 時顯示
    ```jsx
        <Route
            exact
            path="/children"
            children={(props) => {
                return (
                <SampleClass
                    key="children"
                    cb={cb}
                    {...props}
                />
                );
            }}
            />
        <Route
        path="/component"
        component={(props) => {
            return <SampleClass cb={cb} {...props}/>;
        }}
        />

        <Route
        path="/render"
        render={(props) => {
            return (
            <SampleClass key="redner" cb={cb} {...props} />
            );
        }}
        />
    ```

- path : **string | string []**
    - 設定匹配的路徑
    - 以[path-to-regexp@^1.7.0](https://github.com/pillarjs/path-to-regexp/tree/v1.7.0)為準
    - 設定帶參數：
        - 格式：
            - /action/{:param id}(?)
        - 會在 match.param.{param id} 取得
        - **?** 是代表參數是可選擇要不要加入
        - 沒有 **?** ，代表如要 match 必須要輸入完整參數
- exact : **bool**
    - 預設為 false
    - 設為 **true** 指定的 Route path ：`完全 match` 才會觸發 render
    - 設為 **false** 指定的 Route path ： `部分 match` 就會觸發 render
    - 精準部分不包含尾端 `/` 、 path 的大小寫
- strict : **bool**
    - 預設為 false
    - 設為 **true** 指定的 Route path ：會判斷到尾端是否有加`/`
    - 設為 **false** 指定的 Route path ：單純判別到路徑名
- sensitive : **bool**
    - 預設為 false
    - 設為 **true** 指定的 Route path  ： 會去判斷大小寫
    - 設為 **false** 指定的 Route path  ： 不會去判斷大小寫

```js
// /about [x]match
// /about/tony [o]match ,id=tony
<Route path="/about/:id">
    <About  />
</Route>

// /about [o]match
// /about/tony [o]match ,id=tony
<Route path="/about/:id?">
    <About  />
</Route>

// /about [o]match
// /about/ [o]match 
// /about/tony [x]match 
<Route exact path="/about/">
    <About  />
</Route>

// /about [x]match
// /about/ [o]match 
// /about/tony [o]match 
<Route  strict path="/about/">
    <About  />
</Route>


// /about [o]match
// /About/ [x]match 
// /ABOUT [x]match 
<Route  sensitive path="/about/">
    <About  />
</Route>
```
   


### Redirect
- 觸發後，移至指定Url，渲染該Route 的 Component
- 預設以覆蓋當前記錄 `history stack`，**非新增**
- 參數
    - to : **string** | **object**
        - string : 轉址路徑
        - object : 轉址詳細設定
            - pathname :  **string** 
                - 轉址路徑
            - search : **string**
                - 會在 Url 帶入額外的 query string
                - Component 的 **this.props.loaction.search**找到傳入參數
            - hash : **string**
                - 會在 Url 帶入 hash 參數
                - 可以在 Component 的 **this.props.loaction.hash**找到傳入參數
            - state : **object**
                - 轉址後欲帶入的物件參數
                - 可在 Component 的 **this.props.loaction.state**找到傳入參數
    - push : **bool**
        - 預設 **false**
        - 設為 **true** 轉址以**新增 history stack**方式進入記錄
        - 設為 **false** 轉址以**覆蓋 history stack**方式進入記錄
    - from : **string**
        - 指定會觸發轉址的 Url
        - 未設定，則每次檢視到都會觸發
        - 在有加裝 <Switch>時：
            - 在 **from** 設定額外參數會被帶入 **to**
            - **to** 的 pathname 沒有設定對應參數的話，則會被忽略
    - exact : **bool**
    - strict : **bool**
    - sensitive : **bool**
        - 功效同 [Route](#Route)
```js
    // /render3/12 change to /about/12
   <Switch>
        <Redirect from="/render3/:id" to={{pathname:"/about/:id" }} />
    </Switch>
    // /render or /render2 change to /about?utm=your+face
    //  /about's component this.props.location.state.param1 = "hello"
    <Route
        path={["/render", "/render2"]}
        render={(props) => {

        return <Redirect to={
            {
                pathname:"about" , 
                search:"?utm=your+face" ,
                state:{
                    param1:"hello"
                }
            }
            } />;
        }}
    />
```

### Link
- 建立 Url 導向連結
- to : **string | object**
    - 設定要導向的Url 
    - string : 導向路徑，
        - 可在 Url 的後面帶入 Query Stirng`(?)` or hash param `(#)`
    - object : 導向詳細設定
        - pathname :  **string** 
            - 導向路徑
            - 不可帶入其他參數設定，帶入不會有效果
        - search : **string**
            - 會在 Url 帶入額外的 query string
            - Component 的 **this.props.loaction.search**找到傳入參數
        - hash : **string**
            - 會在 Url 帶入 hash 參數
            - 可以在 Component 的 **this.props.loaction.hash**找到傳入參數
        - state : **object**
            - 轉址後欲帶入的物件參數
            - 可在 Component 的 **this.props.loaction.state**找到傳入參數
- replace : **bool**
    - 預設 **false**
    - 設為 **true** 導向以**新增 history stack**方式進入記錄
    - 設為 **false** 導向以**覆蓋 history stack**方式進入記錄

### Switch
- **Route** 的集合
- 只會 render **第一個** match到的 Route
- location : **object**
    - 可植入自定的 location 
    - 會在 match 到時，放入指定的 Component 的 this.props
- children : **node**
    - 放入Switch 管理的 Route or Redirect
    - 會繼承從 Switch 那邊的 **location**
### history

### location

### match
