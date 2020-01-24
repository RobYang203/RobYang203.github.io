---
title: Hexo教學
date: 2020-01-24 22:29:20
categories:
- Hexo
tags: 
- Hexo
- 教學

---

# Hexo

##  說明
* 可以自動建立一個 Blog 
* 可以把生成的 Blog 檔案放在 Git Page 裡
* 安裝 `(需要先安裝 npm)`
    > npm install -g hexo-cli
* 有多種指令可以來對 Blog 作設定

## Hexo 命令 
> `[content]` 裡的內容代表可以省略
* > hexo init [project name] 
    *  初始化          
        1. **project name** : 這 Blog 專案的名稱 
        2. 有填寫的話，會建立一個 **project name** 的資料夾 
        3. 沒有填寫的話，則會在當下資料夾建立專案 *(非空白會報錯)*

*  hexo g[enerate]
    *  編譯檔案為 **html 文件**
    *  編譯後會新增 **public資料夾** 在 `專案根目錄`
* hexo clean
    * 清除編譯後的 **public資料夾**
* hexo d[eploy]
    * 部屬到指定的 Server
    * 要在 _confing.yml 的 deploy 選項設定
* hexo s[erver]
    * 以本機啟動 Server
    * 默認 Url : `localhost:4000`

* hexo new [layout] < title >
    * 建立新文章
    * 內建三種 [layout](#Layout)
    * 預設為 post **layout**



## _config.yml
* 針對這專案 blog 的設定
* 格式
    * 以 **key： `[空白]` value** 
    * **value** 跟 **:** 之間一定要空白，不然會報錯
``` yml
    url: https://robyang203.github.io/
    root: /TestBlog2
```
* 分類 `目前有用到的`
    * Site
        * Blog 資訊
    ``` yml
        title: TestBlog2    # 部落格名稱
        subtitle: ''    
        description: ''     # 描述
        keywords:
        author: Tony    #作者
        language: en    #語系
        timezone: ''
    ```
    * URL
        * Blog 路由設定
    ``` yml
    url: https://robyang203.github.io/ # Domain
    root: /TestBlog2 # 此網站的根目錄
    permalink: :year/:month/:day/:title/ # 文章固定網址
    permalink_defaults:
    pretty_urls:
    trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
    trailing_html: true # Set to false to remove trailing '.html' from permalinks
    ```
    * Extension
        * 額外添加插件，目前用到 theme
    ``` yml
    theme: Next 
    ```
    * Deploymemt
        * 部署到哪個地方 ， 目前使用 **Github-Pages**
    ``` yml
    deploy:
        type: git #類型
        repo: git@github.com:RobYang203/TestBlog2.git #要部署到哪個 repo
        branch: gh-pages #repo 的分支
    ```

    
## Layout
* 預設三種，提供不同的寫作模式
    * post
        * 會發佈在主頁 **(Home)** 上
        * 會在 **source/_post** 資料夾下新增 `<title>.md`檔
    * page
        * 獨立新增一頁，路徑會是 domain/title
        * 會在 **source/** 路徑 ，新增 `<title>` 資料夾，裡面會預設放有 `index.md` 
    * draft
        * 草稿類型，不會顯示在頁面上

# Categories & Tags
* 可提供文章分類的功能
* **Categories** 每篇文章只能有一個 ， **Tags** 可以有多個
* 只能在 Post文章有
* 新增 **Page** 來保存 
> hexo new page [ tags | categories ]
* 再新增文章加入 `type`
``` markdown
    ---
    title: new Page Namw
    date: 2017-05-27 13:47:40
    type: ["tags" | "categories"] 
    ---
```
* 之後當新增文章時，在資訊頁面添加上
``` md
    ---
    title: Page
    date: 2017-05-26 12:12:57
    categories: 
    - category1
    tags:
    - tag1
    - tag2
    - tag3
    ---
```

# NexT 主題
* 從 [HexT Github](https://github.com/theme-next/hexo-theme-next/releases)下載
* 下載後解壓縮，命名資料夾 `Next`
* 移置 `ProjectName/theme` 資料夾下
* 設定 _config.yml， **theme** 改為 `Next` 
 ``` yml
    theme: Next 
 ```
##  部屬到 Github 上

* 修改 `_config.yml`  **deploy 選項**
    * type 類型
    * repo 儲存庫
    * branch 分支
``` 
    deploy:
        type: git 
        repo: git@github.com:yourusername/yourprojectname.git
        branch: gh-pages
```

* 設定完後，輸入 `hexo d` 會自動 push 到指定的 **github branch**

## Q-List
* Q.更新文章後發現內容沒變
> A. 有變動文章時會有機率被 cache ，所以最好更新文章後清一次

* Q. 