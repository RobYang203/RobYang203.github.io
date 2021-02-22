---
title: 建立 CRA 開發環境
date: 2021-02-22 19:47:16
---
# 需要工具
## NVM
### 簡述
管理不同 nodejs 版本的工具
### 安裝
```sh
$ brew install nvm
```
### 設定
```sh
$ echo "source $(brew --prefix nvm)/nvm.sh" >> .bash_profile # 把 nvm.sh 路徑放入到 .bash_profile
$ . ~/.bash_profile #更新設定
```

## NodeJS

### 簡述

在本地端可以執行 javascript 的一個開發環境

### 安裝(擇一)
1. [官網](https://nodejs.org/en/)下載安裝
2. Homebrew
``` sh
$ brew search node #尋找可安裝版本
$ brew install node@<version> #安裝
```
3. nvm
``` sh
$ nvm ls-remote #尋找可安裝版本
$ nvm install <version> # 安裝
```

## Yarn
### 簡述
package 管理器，管理專案的 package 

### 安裝 
``` sh
$ brew install yarn # 安裝
```


# CRA 
## 簡述
facebook 推出的官方 reactJS Scaffold ， 讓你站在巨人的肩膀上，降低開發技術需求，建立專案後即可開發

## 安裝 by yarn
-  yarn 版本需高過 0.25
``` sh
$ yarn create react-app <app name> # 安裝 
```


