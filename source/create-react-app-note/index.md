---
title: create-react-app-note
date: 2020-10-14 16:01:47
---
# 使用 `create-react-app` 建立專案

## 流程
-  建立 `create-react-app` 專案
-  安裝 `react-app-rewired` 修改專案設定
-  安裝 `dotenv-cli` 根據不同環境設定環境變數檔
-  設定 config-overrides.js
    - webpack
        - plugin
        - rules loader
    - devServer
        - 設定 proxy
    - paths
    - jest(暫不需要)
-  設定環境變數檔 **.env**
    - 分類：
        - .env.development
        - .env.production
        - .env
- 修改 package.json
    - scripts
        - build:dev
        - build:prodr
## 建置
> npx create-react-app [**project name**]

## 環境變數

## 安裝 react-app-rewired
修改 `create-react-app` 建置專案的設定
> npm install react-app-rewired --save-dev


