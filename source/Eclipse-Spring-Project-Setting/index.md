---
title: Eclipse_Spring_Project_Setting
date: 2020-02-10 01:22:47
---

##  Eclipse Spring Project Setting
* 打開 Eclipse ，在新增專案裡找到 **Web**資料夾，選擇 **Dynamic Web Project**
* 設定 `project name`，完成
* 手動載入 **Spring Framework**

##  Spring Maven Web Project
* 打開 Eclipse ，在新增專案裡找到 **Maven**資料夾，選擇 **Maven Project**
* 在 **Select an Archetype** 選擇 
    * `Group ID`: **com.apache.maven.archetypes**<br>
    * `Artifact Id`: **maven-archetype-webapp**
* 編輯 `pom.xml` 載入 **Spring Framework**
```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>4.3.14.RELEASE</version>
</dependency>
```
* 確認 JRE 在 JAVA8 以上，否則會有 `springmvc/main/java(missing)`
## WebContent 架構
* META-INF
    * 主要是在打包(.jar .war)時內容會自動建立
    * 存放 **Package**, **額外設定(版本,安全,擴展,服務)**  
    * 主要檔案
        * Manifast.MF
    * 參考資料：
        * https://blog.csdn.net/umi2008/article/details/84211141
* WEB-INF
    * 網站資訊存放區，不過客戶端**不可直接存取**
    * 目錄
        * lib/
        * web.xml
        * classes/

