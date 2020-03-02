---
title: JSLearningNote_2019-12-17
date: 2020-03-02 23:56:34
---
### Primitive type & Object type
* 在賦值給變數時會決定好是什麼type
* 賦值給變數
    * 會把數據放在一個記憶體位置，再把記憶體位置丟給變數
* **Primitive type** 原始型別
    * 唯一值，不會被其他變數參考`call by value`
* **Object type** 物件型別
    * 非唯一值，所有變數可共同參考`call by referance`

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

### shallow copy

### this
* function 的 this 會綁定建立時為於在何處的物件的本體