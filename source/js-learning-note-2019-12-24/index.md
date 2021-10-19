---
title: JSLearningNote_2019-12-24
date: 2020-03-02 23:56:45
---

https://hackmd.io/oQy-dejbQn2Ene5ebQJanQ?both

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

### arguments 
* 在 `function` 裡，自帶的參數
* 在 `function` 範圍內輸入 **arguments**，就可以讀取呼叫此函數所帶入的參數
* Arguments object
    * 屬於`偽陣列`
    * 以 object 模仿 array
    * 有自帶的 length
    * 可以用 `array.prototype.slice.call(argument)`轉成 array
    * 帶入多少參數 `arguments.length` 就有多長
```js
function testArgFnc(a,b,c){
    console.log(arguments);
    var argList = Array.prototype.slice.call(arguments);
    console.log(argList);    
}

//arguments.length = 2
testArgFnc(1,2);
//arguments.length = 5
testArgFnc(1,2,4,5,3);
```

### spread `...`
* 展開語法
* 能使 `array , object , string`，展開為單個數值
    * 能把展開的數值分配給 array or object
    * array 是一個`array[index]`為單位
    * object 是以 `key:value`為單位
    * string 是`一個字`為單位
* 在建立 `function`時，設定參數時可用 `...Arags` 接住參數
    * 會以**陣列**方式呈現
* 在呼叫`function`時可用 `...args`，展開分配給 `function`
    >`p.s object 不行，會報錯`
```js

var a = [1,2,3,4,5];
console.log("this is a");
console.log(a);
var clone_a = [...a];
console.log("clone_a");
console.log(clone_a);


var b= {a:1,b:"test"};
console.log("this is b");
console.log(b);
var clone_b = {...b};
console.log("clone_b");
console.log(clone_b);


var c = "testString";
console.log("this is c");
console.log(c);
var cloneArray_c = [...c];
console.log("cloneArray_c");
console.log(cloneArray_c);
var cloneObject_c = {...c};
console.log("cloneObject_c");
console.log(cloneObject_c);


function funcSpread(...args){
    console.log(args);
}
function funcCallSpread(args){
    console.log(args);
    console.log(arguments);
}
/*
    [Array(5)]
        0: (5) [1, 2, 3, 4, 5]
        length: 1
        __proto__: Array(0)
*/
funSpread(a);
//1
funcCallSpread(...a);
```
### syntax parsers
* 語法分析
* js 的編譯是`直譯式(Interpreted)`，解析語法是逐字讀取
* 如果該字元沒有相對意義的時候會產生錯誤
* js 核心編譯引擎會自動幫你在它認為的句尾上自動加上分號

### function overloading
* js 沒有真正意義上的 overloading
* 因為是`直譯式`兩個相同 `function name `宣告時，後面會蓋掉前面的
* js呼叫 `function`，給的參數數量可以不用給到全部
* 以上述特性可以去模擬 overloading
```js
function funcOverloading(a,b,c){
    if(arguments.length === 0)
        return "no arg";
    if(arguments.length === 1)
        return a;
    if(arguments.length === 2)
        return a + "-"+ b;
    if(arguments.length === 3)
        return a + "-"+ b + "-"+ c;

}
//no arg
funcOverloading();
//1
funcOverloading(1);
//1-2
funcOverloading(1,2);
// 1-2-3
funcOverloading(1,2,3);

```
### Execution Context
* `直譯式語言`則是必須依賴`執行環境 (execution context)`
* 單執行序
* 以堆疊的方式保存所有的`執行環境`
    * 後面建立的會在上面
    * 當程式結束後`執行環境`就會被移除
* 會有很多個`執行環境 `
* 一開始會自動建立一個`global context (全域執行環境)`
    * `global context`只會有一個
    * `global context` 會一直存在
* 每個`函式(function)`會建立一個`function context(執行環境)`
* 生成`執行環境`時會有兩階段
    * 建立階段
        * 建立 `scope chain`
        * 宣告變數 & 函式 = **hoisting**
        * 綁定 **this**
        * 建立 `Outer Environment`
    * 執行階段
        * 賦值給變數
![](https://i.imgur.com/pPuFspr.png)

### hoisting
* 提昇
* 在`執行環境(Execution Context)`進入`執行階段(Execution Phase)`前，對此環境的`變數 ＆ 函數`先進行宣告
* 相當於把`變數 ＆ 函數`往上拉到程式碼最上層一樣
* `變數`提昇只單純做宣告動作，不會進行賦值，所以初始值會是**undefined**
```js
//success
testHoisting();
function testHoisting(){
    //undefined
    console.log(a);

    var a = 10;
}

//undefined
console.log(testVarFuncHoisting);
//error Uncaught TypeError: testVarFuncHoisting is not a function
testVarFuncHoisting();
var testVarFuncHoisting = function(){
    //undefined
    console.log(a);
    var a = 10;
};

```
### Immediatelty Invoked Function Expression `(IIFE)S` 
* 定義完馬上就執行的`JavaScript function`
```js
//Function Statement
function testIIFES(){
    console.log("test IIFEs");
}();

//Function Expression
var testIIFES2 = function(){
    console.log("test IIFEs2");
}();


```
### Operator ()
* Function declaration
    * 定義函式
* Function Call
    * 呼叫 Function時 
    * `()`裡面可以帶入函式參數(arguments)
* Grouping
    * 在一個 **Experssion**有多個**Operator**，對`()`裡的內容會優先執行

###  () + IIFES
* 在程式執行時就可以執行`匿名函式`
* 宣告`匿名函式`無變數承接是會出錯的
* 在`匿名函式`外面加上 **()**，可防止出錯
* 函式執行完後直接釋放記憶體
* 可以想像 `()` 就是在執行一個 空 function 只會 **return**參數
```js 
function testParentheses(a){
    return a;
}
var t = 1 + testParentheses(2+8) * 2 ;
console.log(t);//22

```
```js
(function(){
    console.log("test IIFEs3");
}());
```