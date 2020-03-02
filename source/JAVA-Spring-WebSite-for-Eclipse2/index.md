---
title: JAVA-Spring-WebSite-for-Eclipse2
date: 2020-02-14 00:46:21
---

## JAVA-Spring WebSite for Eclipse for JavaConfig 設定

### Web <-> Server 

* 設定 WebInitializer.java
    * 設定 `DispatcherServlet`

        ``` java
        @Configuration
        public class WebAppInitializer implements WebApplicationInitializer{

            @Override
            public void onStartup(ServletContext servletContext) throws ServletException{
                System.out.println("MVC WebAppInitializer StartUp!");
                AnnotationConfigWebApplicationContext appContext = new AnnotationConfigWebApplicationContext();
                appContext.register(WebMvcConfig.class);
                
                ServletRegistration.Dynamic dispather =servletContext.addServlet(
                        "SpringDispatcher", new DispatcherServlet(appContext));
                dispather.setLoadOnStartup(1);
                dispather.addMapping("/");
                
            }
            
        }

        ```
* 設定 WebConfig
    * 加上 `annotation`

        ``` java
        @Configuration
        @EnableWebMvc
        @ComponentScan("com.test ")//設定要掃描的 Component package
        public class WebMvcConfig extends WebMvcConfigurerAdapter{
        ```
    * 設定將要載入的`bean`

        ``` java
        //設定從 Controller 返回 String or ModelAndView 提取 view 的解析器
        @Bean(name = "viewResolver")
        public InternalResourceViewResolver getViewResolver() {
            InternalResourceViewResolver viewResolver = new InternalResourceViewResolver();
            viewResolver.setPrefix("/WEB-INF/views/");
            viewResolver.setSuffix(".jsp");
            return viewResolver;
        }


        ```
    * 有需要接收 json 格式 ，需加載`mappingJackson2HttpMessageConverter`，否則會出現 ERROR:`Completed 415 UNSUPPORTED_MEDIA_TYPE`

        ```java
        @Bean
        public RequestMappingHandlerAdapter getRequestMappingHandlerAdapter(
                @Autowired MappingJackson2HttpMessageConverter mappingJackson2HttpMessageConverter,
                @Autowired ContentNegotiationManager mvcContentNegotiationManager) {
            RequestMappingHandlerAdapter requestMappingHandlerAdapter = new RequestMappingHandlerAdapter();
            requestMappingHandlerAdapter
                    .setMessageConverters(Collections.singletonList(mappingJackson2HttpMessageConverter));
            requestMappingHandlerAdapter.setContentNegotiationManager(mvcContentNegotiationManager);
            return requestMappingHandlerAdapter;
        }

        @Bean
        public MappingJackson2HttpMessageConverter mappingJackson2HttpMessageConverter() {
            return new MappingJackson2HttpMessageConverter();
        }
        ```
* 設定 Controller
    * 建立 Controller.java
        ```java
        @Controller
        public class Controller {
        
        ```
    * 針對 url 設定 `RequestMapping`
        * 由頁面初始化時觸發
        * 前端接資料由 **jsp** 方式去接
        * 回傳 string，代表指定頁面
        * 需要帶值傳遞，回傳 **ModelAndView class**
        * 有參數要帶入加上 `@RequestParam` annotation

        ```java
        @RequestMapping("/edit")
        public ModelAndView editCustomerForm(@RequestParam Long id) {
            System.out.println("action edit");
            Customer customer = customerService.get(id);
            ModelAndView mv = new ModelAndView("edit_customer");
            mv.addObject("customer", customer);
            return mv;
        }
        ```
    * 以 api 方式呼叫，設定
        * `RequestMapping`需帶入
            * value : api url
            * method : 回傳方式 POST or GET
        * 回傳自定格式需加上 `@ResponseBody` annotation
        
        ```java
        @RequestMapping(value = "/hello.action",method = RequestMethod.POST)
        @ResponseBody
        public User jsontest(@RequestBody UseInfo use) {
            System.out.println("received jsontest");
            
            Date dNow = new Date( );
            SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd hh:mm:ss");
            User u= new User(use.getName() ,ft.format(dNow) ,use.getPrice());
            return u;
            
        }
  
      ```
* 要讓 `Tomcat Server`在啟動時，自動的讀取 `WebInitializer`
    * 設定 `SpringServletContainerInitializer.java`

        ```java
        //設定 onStartup要啟動的 class
        @HandlesTypes({WebApplicationInitializer.class})
        public class SpringServletContainerInitializer implements ServletContainerInitializer{
            public  SpringServletContainerInitializer() {
                
            }
            
            @Override
            public void onStartup(@Nullable Set<Class<?>> webApplicationInitializerClasss, javax.servlet.ServletContext servletContext) throws javax.servlet.ServletException{
                System.out.println("MVC StartUp!");


            
            }

        }

        ```
    * 建立 `javax.servlet.ServletContainerInitializer` 
        * 在專案按右鍵 > Build Path > Configure Build Path 
        * 選擇 Source
        * 在 src底下建立 /resources/META-INF/services/ 資料夾
        * 新增檔案 `javax.servlet.ServletContainerInitializer`(無附檔名)
            * 加入內容

                ```
                com.test.config.SpringServletContainerInitializer
                ```
    * 不建立 `javax.servlet.ServletContainerInitializer` 會無法啟動  **SpringServletContainerInitializer**   

    



