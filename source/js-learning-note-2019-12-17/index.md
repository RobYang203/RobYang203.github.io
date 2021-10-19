---
title: JSLearningNote_2019-12-17
date: 2020-03-02 23:56:34
---

https://hackmd.io/yY9M-aGiTuCI0ioZfrN7Vw

### Primitive type & Object type
* 在賦值給變數時會決定好是什麼type
* 賦值給變數
    * 會把數據放在一個記憶體位置，再把記憶體位置丟給變數
* **Primitive type** 原始型別
    * 唯一值，不會被其他變數參考`call by value`
    * 型別
        * Number
        * String
        * Boolean
        * Null
        * Undefined

* **non-Primitive type** 非原始型別
    * 非唯一值，所有變數可共同參考`call by referance`
    * 型別
        * Object
        * Array
        * Regx
        * Function
        * Date

### call by value
* 賦值給變數時，會新建數據

### call by referance
* 賦值給變數時，會直接把記憶體位置丟給變數

```js
//call by value
var i = 1;
var b = i;
i = 4;

//i=4,b=1
console.log("i="+ i + ",b="+ b);

//call by referance
var g = {
    age:10,
    sex:"man"
};

var h = g;

g.age = 20;
g.sex = "woman";


console.log("this is g object");
//{age: 20, sex: "woman"}
console.log(g);
console.log("this is h object");
//{age: 20, sex: "woman"}
console.log(h);
```

### deep copy
* 深拷貝
* 把**變數a**的值經過特殊處理丟給**變數b**
    * 建立全新的物件
* 兩個變數的記憶體位置是不一樣的，兩個變數之間毫無關連
* 使用 `Object.assign`
    ```js
    //只能複製一層
    var a = { 
        ages: 
        { 
            value: 10 
        },
        sex:"man"
    };

    var b = Object.assign({} , a);
    console.log("b value is ");
    console.log(b.sex);//man
    console.log(b.ages);//10

    a.sex = "woman";
    a.ages.value = 20;
    console.log("after change a age , b value is ");
    console.log(b.sex);//man
    console.log(b.ages);//20
    ```
* 使用 `JSON.stringify` & `JSON.parse`
    *  不過無法拷貝 Function、Set、Map…等型態
    ```js
    // 轉成 JSON string 在轉成全新的物件，可深拷貝所有層
    var a = { 
        ages: 
        { 
            value: 10 
        },
        sex:"man"
    };

    var b = JSON.parse(JSON.stringify(a));
    console.log("b value is ");
    console.log(b.sex);//man
    console.log(b.ages);//10

    a.sex = "woman";
    a.ages.value = 20;
    console.log("after change a age , b value is ");
    console.log(b.sex);//man
    console.log(b.ages);//10
    ```

### shallow copy
* 淺拷貝
* 把**變數a**的值直接丟給**變數b**，不做額外處理
    * 僅只會把**變數a**的記憶體位置丟給**變數b**
* 參考到的會是同一個物件，動a會連b的值一起變
```js
var a = {
    age:10,
    sex:"man"
};

var b = a;
console.log("b value is ");
console.log(b);

a.age = 20;
console.log("after change a age , b value is ");
console.log(b);
```

### this
* js 的關鍵字
* 代表物件本身
* 最外層的 **this** 即是 `global object`
* 有建立新物件 **this**的參考指向才會轉成該物件
* 當function 沒有綁定物件時，內部 **this**會直接參考 `global object`
```js
console.log(this);//global object
function gFunc(){
    console.log(this);//global object
}
gFunc();

this.name = "Mr.w";
var a = {
    name : "Mr.A",
    callName:function(w){
        console.log("a name is " + this.name);//Mr.A
        console.log("w name is " + w.name);//Mr.A
        function changeName(){
            console.log("Start change name");
            console.log(this);//global object
            this.name = "Mr.Change";
        }
        changeName();
        console.log("w name is " + w.name);//Mr.A
        console.log("a change name is " + this.name);//Mr.A
    }

};
//a.callName(this);
console.log("===========================");
var c = {
    name : "Mr.C",
    callName:function(){
        console.log("c name is " + this.name);//Mr.A
        a.callName(this);
        
    }

};
c.callName();
```