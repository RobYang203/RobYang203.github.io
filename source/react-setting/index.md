---
title: react_setting
date: 2020-03-25 22:48:37
---

## React 設定
### 下載套件
* dev 環境
	* @babel/core
		* babel 核心 api
	* @babel/preset-env
		* 轉譯 es2015
	* @babel/preset-react
		* 轉譯 jsx
	* babel-loader
		* babel 轉譯工具
	* @babel/plugin-proposal-class-properties
		* 可以在 class 內宣告 Arrow function
		* 在 `.babelrc`要加上屬性
	* style-loader 
	* css-loader

* react
* react-dom 

### webpack 設定
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
		publicPath:"/"//編譯後資源儲存的位置
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
			},
			{
				test:/\.css$/,//判斷是否為".css"
				loader:["css-loader","style-loader"],//編譯器，把符合條件的檔案，編譯成指定樣式
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
### .babelrc 設定
* 語法轉譯器
* 對 jsx 進行轉譯
* 參數 
    * presets 
        * 預設轉譯器
    *  env 
        * 針對環境設置
```json
{
    "presets": [
      [
        "@babel/preset-env",
        {
          "targets": {
            // 設定需要翻譯 es2015 的瀏覽器最低版本
            "edge": 17,
            "firefox": 60,
            "chrome": 67,
            "safari": 11.1
          },
          // 設定針對 es6 有用到的套件在導入
          "useBuiltIns": "usage"
        }
      ],
      "@babel/preset-react"
    ],
    "plugins": ["transform-class-properties"]
}
```


