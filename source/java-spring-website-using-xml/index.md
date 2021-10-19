---
title: JAVA-Spring WebSite for Eclipse for XML 設定
date: 2020-01-24 23:01:56
---
## JAVA-Spring WebSite for Eclipse for XML 設定
### Web.xml 設定
* 在 `<context-param>` 把 `mvc-config.xml` 設定在**contextConfigLocation**
```xml
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>/WEB-INF/mvc-config.xml</param-value>		
	</context-param>
```
* 在設定 `<listener>`
```xml
    <listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
```
> P.S. 有在 `<context-param>` 設定**contextConfigLocation**，就要設定`<listener>`

### For MVC
* 在 `<servlet>` 設定 **DispatherServlet**，建立**前端控制器(front controller)** 
```xml
	<servlet>
		<servlet-name>translator</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value></param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
```
> 當 `contextConfigLocation` 尚未設定時，預設會讀取 `Servlet名稱- servlet.xml`

* 在 `<servlet-mapping>` 設定 **Controller**條件
```xml
    <servlet-mapping>
		<servlet-name>translator</servlet-name>
		<url-pattern>*.action</url-pattern>		
	</servlet-mapping>
```

* 流程
   1. client request 
   2. servlet-mapping 驗證 url，是否有符合
   3. 連結到 mapping 的 dispatcherServlet  
   4. 根據 dispatcher-servlet.xml 連接到 Controller
