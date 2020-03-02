---
title: eclipse-setting
date: 2020-01-26 16:31:11
---

## 下載 Eclipse
* 官網下載, [**eclipse-install**](https://www.eclipse.org/downloads/)
* 執行 **eclipse-install**
> 要執行之前，需要安裝**JDK**

## 安裝套件
* 打開 eclipse ，選擇 **Help** -> Install New Software
* `Work With`選擇 **http://download.eclipse.org/releases/lasest-version**
* 找到 **`Web, XML, Java EE and OSGi Enterprise Development`** 展開
    * Web
        * 選擇 
            * Eclipse Java EE Developer Tools
            * Eclipse Java Web Developer Tools
            * Eclipse Web Developer Tools
            * Eclipse XML Editors and Tools
        * 安裝
    > **P.S.** 沒安裝的話，再新增專案會找不到 **Web** 選項
    * Server
        * 選擇 
            * JST Server Adapters
            * JST Server Adapters Extensions
        * 安裝
    > **P.S.** 沒安裝的話，新增專案會找不到 **Tomcat** 選項


## 安裝 Tomcat
* 在[Tomcat官網](https://tomcat.apache.org/)下載
    * 選擇 **Binary Distributions** > Core
    * 解壓縮
* 打開 Eclipse ，在新增專案裡找到 **Server**資料夾，選擇 **Server**
* 進入後選擇 **Apache** > **Tomcat version Server** 
* 在 **`Tomcat installation directory`** 選擇下載的 Tomcat Server
* **JRE 版本**選擇現有的版本


## 手動下載 & 掛載  Spring Framework
* 下載網址: https://repo.spring.io/release/org/springframework/spring/
* 選擇版本
* 選擇 **spring-version.RELEASE-dist.zip**
* 在 **Project Explorer** 選擇設定的 `project name` ， 右鍵 `Bulid Path` > `Configure Build Path`
* 選擇 **Libraries** > **Add External JARS**，選擇下載好的 `Spring Framework` > `libs` 底下所有的 jar檔 
