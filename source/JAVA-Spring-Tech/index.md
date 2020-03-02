---
title: JAVA-Spring Simple Test
date: 2020-01-26 16:20:11
---
## Spring 簡單測試專案
* 新增 **Java Project**
* 建立測試物件
    * 建立 IGun 介面，設定 Gun 系列標準
    * 以 IGun 為基礎，建立 FireGun & IceGun
* 建立 POJO
    * 建立 Role class 
        * 參數
            * name
            * Gun
    * 實作 getter & setter 對 Gun & name
* 建立 Bean.xml 描述物件
    * Role
    * FireGun
    * IceGun
* 在 `main class` 讀取 **Bean.xml** ，建立 Role物件，並呼叫 