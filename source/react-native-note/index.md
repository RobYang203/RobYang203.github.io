---
title: react-native-note
date: 2021-01-18 11:29:17
---

# Install

## Requirement

1. xcode
   - 在 App Store or [Apple Developer](https://developer.apple.com/download/more/)
2. android
3. react-native-cli
   - npm install -g react-native-cli
4. watchman
   - brew install watchman

# Create React Native Project

> react-native init < project name >

# 簡介

react native，不像是 web 那樣有相關的`基本元素 (div 、 span 、 li ..etc )`，為了要配合兩個不同的平台所以會把所有的內容以 component 表示

# Document Architecture

```
├── __tests__
├── node_modules
├── android
├── ios
├── app.json
├── babel.config.js
├── App.js
├── index.js
├── metro.config.js
├── package.json
└── yarn.lock
```

# command

# native-base

# react-native navigation

針對 react native 管理 畫面切換的套件

## 安裝
### 需求
- node >= 8
- react-native >= 0.51
### command
> yarn add react-native-navigation

## 啟動 navigation
在`index.js`,打上以下指令
```javascript
Navigation.events().registerAppLaunchedListener(() => {
  // Each time the event is received you should call Navigation.setRoot
  Navigation.registerComponent('Home', () => Component);
  Navigation.setRoot({
      root:{
          component:{
              name:"Home"
          }
      }
  });
});

```

- `registerAppLaunchedListener` 是在啟動APP後會觸發的一次性事件，在此做相關初始化的動作

- `Navigation.registerComponent(component name , react component)`  
把 react component 註冊至 navigation 賦予 **相關代號(component name)**
 
- `Navigation.setRoot(layout)` 設定整體 Layout ，提供以下幾種 Layout:
    - stack
    - Bottom tabs
    - Side Menu
    - External Component

## 常用 Command


# Question

- 編譯 ios 時遇上， `linker command failed with exit code 1 (use -v to see invocation)`  
  遇上情境：作業系統是 `Mac OS 10.14`、 `xcode 10`  
  解決方法：更新 os & xcode 至最新版

- 在 `run react-native run-ios`，遇上 `xcrun: error: active developer path`

* 遇上情境：原本是 `xcode 10` ， 載入 `xcode 12`後，出先這個問題
* 解決方法： 輸入 `sudo xcode-select -switch <Xcode.app 安裝位置> `，重新設定 Xcode 的位置

- 什麼是 react-native link

- 編譯 ios 時遇上

  > Showing All Messages
  > Multiple commands produce 'shoppingcarSkeleton.app/Zocial.ttf'

- 如何啟動 react native debugger 與 ios 模擬器互相連接
