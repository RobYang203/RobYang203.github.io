---
title: JSLearningNote_2019-12-10
date: 2020-03-02 23:56:14
---

### 關於 || 運算子
* 用於判斷左右兩側值是否存在
    * 其中一方存在，回傳已存在一方
    * 兩方都存在，回傳左邊的值
* 不存在的定義為
   * null | undefined | false | 0 | ""
```js
const v1 = true;
const v2 = false;
console.log(v1 || v2);// true

const v3 = "";
const v4 = "goood day~";
console.log(v3 || v4);// goood day~

const v5 = 0;
const v6 = 10;
console.log(v5 || v6);// 10

const v7 = {};
const v8 = null;
console.log(v7 || v8);// {}
```

### 關於 Object
* 有關連的變數 or 方法 的集合體 
* **基礎型別**之一   
* 建立物件
   ```js
   var obj1 = {};
   var obj2 = new Object();
   ```
* 在集合體內的`屬性(property)`為**物件成員**
* `屬性`以 `key ＝ value `的形式保存
   * 放入**number or string** 是以 `call by value` ， 放入 **function** or **object**則是 `call by reference`
   * 建立物件屬性方式有 **dot notation** `.` & **bracket notation**`[]`
   ```js
   //變數(call by value)
   obj1["arg"] = 1;
   obj2.arg = 2;

   //function (call by reference)
   obj1["func"] =func1
   obj2.func = func1;

   //因為 function 會提升，所以可以放在後面
   function func1(v){
      console.log("this is func "+ v);
   };
   ```

* 呼叫 
   ```js
   //1
   console.log(obj1["arg"]);
   //2
   console.log(obj2.arg);
   //this is func 1
   console.log(obj1["func"](1));
   //this is func 2
   console.log(obj2.func(2));
   ```

### Operator "."
>  ObjectName.PropertyName
* `Member Access`
* 由左至右
* 可以訪問物件的屬性內容
* 優先度 19 
* 當右邊有等號時，會把右邊值給予該屬性
```js
var obj = {};
obj.arg = 2;
```

### JSON
* JavaScript Object Notation
* 結構化資料(Structured Data)
* 用於傳輸資料
   * 傳輸資料的 MIME Type 是 `application/json`
* 以 JavaScript 物件格式儲存資料
* 只包含基本資料結構，不會有 **function**
* 單筆資料以`{}`包住，多筆資料以`[]`包住單筆資料
* 屬性資料格式是 `"key":value`，key值必須要有**雙引號(")**包住
```json
{
   "human":[//array
      {
         "name":"Tony",
         "age" :29,
         "single": true,
         "height": 176,
         "weight":  70
      },
      {//objecy
         "name":"Ross",
         "age" :19,
         "single": false,
         "height": 166,
         "weight":  50,
         "sex":"female"
      }
   ],
   "car":[
      "Toyota",
      "Mazda",
      "Honda"
   ],
   "acount":1000,//number
   "local":"Taipei"//string
}
```

### Statement(陳述句) ＆ Expression(表達示)
* 程式碼一段功能的單位
* Statement 執行其程式碼**不會有返回值**
```js
try{
   //do something
}catch(e){
   //
}

for(var i = 0 ; i < 10 ;i++){
   //do something
}

if(a > b){
   //do something
}

function StatementFunc(){
   console.log("function Statement");
}
```
* Expression 執行其程式碼**會有返回值**
```js
var i = 10;
//Function Expression
var fExp = function(){
   console.log("function Expression");
}
```