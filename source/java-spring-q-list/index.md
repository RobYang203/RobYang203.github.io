---
title: JAVA-Spring-QList
date: 2020-01-30 01:21:11
---
* 關於`Inversion Of Control (IOC)`
    * 控制(流程)反轉
    * 程式整體的架構流程由開發者轉移到第三方來做控制
* 什麼是`依賴 (Dependency)`
    * 當一個類別需要實作其他類別時，就是**依賴(Dependency)** 關係
* 什麼是`Dependency Injection`
    * 可使類別之間的耦合不那麼緊密
    * 對於在類別要使用另外的類別採取**注入**的方式
    * **注入**方式可以是用setter取得...等，採取由外部供應
        * 建構子注入
        * setter注入
        * interface注入
    * 類別裡不主動實作其他類別
* 什麼是`POJO`
* 什麼是`bean`
* 什麼是`JSP`
* 什麼是`JPA`
* 什麼是`hibernate`
* 什麼是`contextConfigLocation`
* `context-param` & `init-param` 區別
* `dispather-servlet.xml` & `applcationContext.xml` 差別
* 在儲存 `web.xml`loading會很久
* 關於在 `Maven Project` 找不到 **Run Server**
* 關於 `The absolute uri: [http://java.sun.com/jsp/jstl/core] cannot be resolved in either web.xml or the jar files deployed with this application`
    > 指定 uri: [http://java.sun.com/jsp/jstl/core] 有重複無法解析，刪除多餘的就可以了
* 關於 Error org.springframework.beans.factory.BeanDefinitionStoreException ...ASM ClassReader failed to parse class
    > JRE 版本跟 Spring版本對不上
* 關於 Java compiler level does not match 
    > 到專案根目錄找`.setting`資料夾(隱藏)，找 `org.eclipse.wst.common.project.facet.core.xml` 修改 java版本

* 關於 Bean property 'name' is not readable or has an invalid getter method
    > 沒有設定變數 `name`的 getter | setter
* 關於 java.lang.ClassNotFoundException: org.springframework.web.WebApplicationInitializer
    > 找不到 WebApplicationInitializer ，是因為用 Maven
    * 解決辦法
        * 在管理資源，在專案右鍵 -> properties -> Deployment Assembly -> 按下Add 
        * 選擇 Java Build Path Entries
        * 選擇 Maven Dependencies  
        * Apply
    * 參考資料
        * https://dotblogs.com.tw/raylee/2019/04/22/104236

* 關於 javax.persistence.PersistenceException: No Persistence provider for EntityManager named
    > 因為沒讀到 persistence.xml ，要放在 `META-INF`資料夾下，資料夾要在`Java Build Path` > `Source`下新增

* 關於 WebAppInitializer class 在 Server 啟動時，沒有被實作
    * Servlet Container 要支援 **Servlet 3.0**
    * 實作 `SpringServletContainerInitializer`
    ``` Java
    @HandlesTypes({WebApplicationInitializer.class})  
    public class SpringServletContainerInitializer implements ServletContainerInitializer{
        @Override
        public void onStartup(@Nullable Set<Class<?>> webApplicationInitializerClasss, javax.servlet.ServletContext servletContext) throws javax.servlet.ServletException{

            
        }
    }
    ```
    * 在 `src`底下新增 `resources` > `META-INF` > `services`
        * 新建檔案 `javax.servlet.ServletContainerInitializer`
        * 內容輸入完整的 `SpringServletContainerInitializer`
   

* Q. Server Tomcat v9.0 Server at localhost failed to start.
    > A. 發現是專案出現 **More than one fragment with the name [spring_web] was found. This is not legal ...”**

* Q. 出現 More than one fragment with the name [spring_web] was found. This is not legal ...”
    > A. 在 web.xml 的 `web-app`加上 `<absolute-ordering />`

* Q. 什麼是 `<absolute-ordering />`
    > A. 請參考 https://openhome.cc/Gossip/ServletJSP/Pluggability.html


    
