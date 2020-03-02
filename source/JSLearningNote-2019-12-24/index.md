---
title: JSLearningNote_2019-12-24
date: 2020-03-02 23:56:45
---

# 2019-12-24  Learning

### array
* 以 `[]` 為空陣列
* 是一種`似列表(list-like)`的物件
* 具有**長度(length)**
* 每格位置可存放資訊
    * 資訊包括 
        * 物件 **(object)**
        * 基礎類型 **(number 、 string 、 boolean )**
        * 陣列 **(array)**
        * 函式 **(function)**
* 一個陣列裡可以存放不同的資訊

``` javascript
    var i = [
        0,//number
        'greeting',//string
        false,//boolean
        {
            name : "tony"
        },//object
        [1,2,3,4],//array
        function(){
            console.log("Hello JS!")
        }//function
    ];

    //印出陣列
    console.log(i);

    //遍歷陣列資訊
    i.map((item)=>{
        console.log(item);
    });
```

### arguments && spread

### function overloading

### syntax parsers

### white space

### semicolon

### Immediatelty Invoked Function Expression `(IIFE)S` 

### Safe code
