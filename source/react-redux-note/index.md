---
title: react-redux-note
date: 2020-05-16 16:59:40
---


# React Redux 筆記

### 建立流程
* index 進入點
    * 載入 `store`
    * 建立 Provider component
* 建立 store
    * 需要有 **reducer**
* reducer
    * state 初始化的地方
    * 根據 **action**，處理對有動作回傳 `Redux State`
* action creator
    * action 的格式，包含 **type** & **ployload**
    * 以 `dispatch` 送入，傳送給 **reducer**
* mapStateToProps
    * 接收 `Redux State`，並準備送入指定的 Component
* mapDispatchToProps
    * 客製化 dispatch ， 以 props方式傳入

### 呼叫流程
1. 在指定 Component 呼叫 dispatch ，資料送入 store
2. 把 dispatch 的 actionCreator 送入 reducer
3. reducer 根據 action，做出動作，回傳`Redux State`
4. 觸發 mapStateToProps 調整格式送入 指定 Component，出發 `props render`


