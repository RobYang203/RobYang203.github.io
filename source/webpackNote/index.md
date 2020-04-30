---
title: webpackNote
date: 2020-03-25 23:59:32
---

## Webpack 

#### 為什麼要用 Webpack
> 首先，我們要先了解一點，目前網頁組成就是 html、script、css，就這3樣，沒有別的，瀏覽器也只看得懂這三樣

>那...其他語言 like sass 、 markdown 、 jsx ....etc 瀏覽器要怎麼看呢?
答案就是翻譯阿，就像你聽不懂英文，可以找翻譯幫你翻

>Webpack所做的，就是幫你把這些瀏覽器看不懂的，打包成它看得懂的
	
#### Webpack 的打包
>Webpack 的作用是打包，打包還是要經過翻譯的，這些翻譯的部分會由使用者來自訂
通常會有進入點 **entry.js** ，

>經過它可以把需要打包的檔案給處理好，轉成一個 or 多個檔案

#### 初始化
1. Webpack 是建立在 nodejs 基礎之上的，所以必須要裝 nodejs，並建立 nodejs 專案 
    * npm init
2. 下載 Webpack 套件
    * npm install webpack webpack-cli --save
3. 設定運行指定在 **package.json 的 scripts tag** 
    * "[command name]": "webpack  --mode [mode name]"
        * command name
            * 設定想用甚麼指令呼叫 webpack
            * 執行時呼叫 npm run [command name]
            * test、start 只需要前面加上 npm
        * mode name
            * development
                * 開發模式，編譯出來的檔案會有清楚的斷點提供debug
            * production
                * 正式模式，編譯出來的檔案不會有斷點
    ```json
    "scripts": { 
            "webpack": "webpack  --mode development "
     },
    ```
4. 新增 **webpack.config.js**
    * 此專案 webpack 的設定檔
    * 在裡面宣告 config物件，export 成模組
    ```js
    var path = require('path'); //取得路徑
    var webpack = require('webpack');

    module.exports={
        entry:[//執行點
            "./main.jsx"
        ],
        output:{//編譯輸出點
            path:path.join(__dirname,"dist"),//輸出路徑
            filename:"compiled.js",//編譯後的檔名
            publicPath:"/"//編譯後url位置
        },
        resolve:{//當 import | require 時，會去指定目錄尋找 & 解析
            modules:[
                path.resolve(__dirname,'src'), 'node_modules'//尋找指定資料夾
            ],
            extensions:['.js','jsx','css','scss']//尋找指定副檔名
        },
        module:{//針對不同的語言載入不同的模組 ex:babel、TypeScript，讓其可編譯後輸出成為直譯器所讀的檔案 .js
            rules:[
                {
                    test:/\.(js|jsx)$/,//判斷是否為".js or jsx"
                    loader:"babel-loader",//編譯器，把符合條件的檔案，編譯成指定樣式
                    exclude:/node_modules/
                }
            ]
        },
        devtool:'cheap-module-eval-source-map',
        plugins:[
            new webpack.HotModuleReplacementPlugin(),//在不更新頁面的情況下更新Module
            new webpack.ProvidePlugin({
                React:'react',
                RectDOM:'react-dom'
            }),//建置時，碰到輸入的 key 直接 import，指定 value
            new HtmlWebpackPlugin()//會根據config設定在，路徑 output.path 建立html文件
        ]
    };
    ``` 

#### 參數
* entry - `str array`
    * 進入點，去設定 webpack 解析地進入路徑
* output - `obj`
    * 編譯輸出點
    * 參數
        * path
            * 輸出路徑
        * filename
            * 編譯後的檔名
        * publicPath
            * 編譯後url的位置
* resolve - `obj`
    * 當 import | require 時，會去指定目錄尋找 & 解析
    * 參數
        * modules - `str array`
            * 尋找指定模組位置資料夾
        * extensions
            * 尋找指定副檔名
                > ex: '.js','.jsx','.css','.scss'
* 	module
    * 針對不同的語言載入不同的模組 `ex:babel、TypeScript`，讓其可編譯後輸出成為直譯器所讀的檔案 
    * 參數 - `obj`
        * rules - obj array
            * 指定規則群
            * 參數
                * test
                    * 檢查條件，條件符合執行 loader
                * loader
                    * 編譯器，把符合條件的檔案，編譯成指定樣式
                * exclude
                    * 排除目標資料夾
* devtool - `str`
    * debug 的工具
    * 有七種模式
* plugins -  `obj array`
    * 插件
    * HtmlWebpackPlugin
        * `npm install html-webpack-plugin --save-dev`
        * 根據 webpack.config 設定，導出html文件



## Question 
* Plugin/Preset files are not allowed to export objects, only functions. In K:\Work\TestReact\node_modules\babel-preset-es2015\lib\index.js
    * 原因:
        > babel-loader 版本 在 .babelrc presets 解析的 目標版本錯誤
    * 解決方式:
        > 更換正確目標版本
* ReferenceError: Unknown option: .preset. Check out https://babeljs.io/docs/en/babel-core/#options for more information about options.
    * 原因:
        > .babelrc  參數設錯
* Error: Cannot find module '@babel/core'
    * 原因:
        > 缺少指定套件
    * 解決方式:
        > 安裝上面找不到的套件
        
* Module not found: Error: Can't resolve 'react-dom'
    * 原因:
        > 在 webpack.config.js 的 resolve 少了 node_modules資料夾
* 當安裝完  webpack-cli 後出現
`K:\Work\TestReact2\node_modules\webpack-cli\bin\cli.js:93throw err;ReferenceError: webpack is not defined`
    * 原因:
        > 在 webpack.config.js 裡要宣告 var webpack = require('webpack');

                                

