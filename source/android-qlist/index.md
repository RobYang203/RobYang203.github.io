---
title: android-qlist
date: 2020-04-24 17:38:24
---
#### 什麼是 gradle-wrapper.properties
為記錄目前 gradle 版本資訊


---
#### 什麼是  `build.gradle(project)`的 classpath
**classpath**在 `build.gradle(project)`的  **dependencies**裡，
表示此專案用的`gradle plugin 版本` <br>

---

#### Q. Error : Could not resolve all artifacts for configuration ':classpath'.
A. 在 `build.gradle(project)`的  **dependencies > repositories**，找不到 classpath，所以要新增 `repository maven`
```groovy
buildscript {
    
    repositories {
        maven { url 'https://maven.aliyun.com/repository/jcenter' }//新增 repository
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.2.1'
        

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
```

---
#### Unknown host 'jcenter.bintray.com'

**dependencies > repositories**，新增 `repository maven{ url 'https://maven.aliyun.com/repository/jcenter' }`

---

#### default activity not found
File > Invalidate Caches / Restart 

---