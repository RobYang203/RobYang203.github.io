---
title: css-qlist
date: 2020-04-13 18:30:40
---

### at-rule
* 提供規則告訴 CSS 應該做什麼事
* 分 `Regular Rules (常規規則)` ＆ `Nested Rules (巢狀規則)`
    ```css
    /* Regular Rules */
    @[rule keyword] (rule)

    /* Nested Rule */
    @[rule keyword] {
        /* Nested Statements */
    }
    ```
#### Media Queries
* 一種 `Nested Rules`
* 開頭為 `@Media` 
    ```css
    @Media (Media Fratures | Media Types) {
        /* Style */
    }
    ```
* Media Fratures
    * 針對裝置的一些特徵做判斷
    * 可量化的都可以加上 `min` | `max`
    * 設定時需加上 **()**
    * 分類
        * Viewport/Page Deminsions - 視窗或頁面尺寸
            * width - 寬
            * height - 高
            * orientation - 螢幕方位
                * portrait - 直向
                * landscape 橫向
        * Display Quality - 顯示品質
            * resolution
            * 
        * Color - 顯示顏色
            * color - 判斷裝置顯示顏色 ， 0 為黑白
        * Interation - 互動模式
            * pointer - 判斷指標裝置 
                * none - 沒有
                * coarse - 粗糙
                * fine - 精準

* Media Types 
    * 裝置判斷
    * 分類
        * all - 全部
        * screen - 螢幕裝置
        * print - 列印裝置(包含預覽列印看到的)
        * speech - 朗讀裝置，針對可以「讀出」頁面的設備。
* 邏輯判斷
    * 根據不同條件組成的判斷式
    * 分類
        * AND
        * OR - 用 `,`表示
        * NOT
        * ONLY
    ```css
    /* 判斷是螢幕裝置*/
    @media screen {
        body{
            background: #c0c0c0;
        }
    }
    /* 判斷是螢幕裝置 和 寬最小要是 300px  或是 高最大是 500px*/
    @media screen and (min-width:300px) , (max-height:500px){
        body{
            background: #ff0000;
        }
    }
    /* 判斷是不螢幕裝置*/
    @media not screen {
        body{
            background: #00ff00;
        }
    }
    ```

### css 的順序
### 關於偽元素
### 關於符號 +
### 關於符號 >
### 關於赴號 ~
### 關於 view-port
