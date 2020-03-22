---
title: JSLearningNote_2020-01-02
date: 2020-03-02 23:57:04
---
### Scope
* 程式執行的一個範圍
* 圈定宣告的變數以及函式存取範圍
* 分 `global scope (全域範圍)` & `local scope (區域範圍)` 
* 存取變數由 `內 -> 外`
    * 稱為 `巢狀範疇 (Nested Scope)`
    * 先判斷這變數是否是**在本區域建立的**
    * 不是 **local scope** 則會往一層一層往外層找
    * 最外層是 **global scope**
    * 找到變數時立即停止動作，稱為**shadowing**  
    * 外層無法調用內層的資訊

### Lexical Scope
* 稱為 `語彙範疇`
* 在建立`執行環境(excution context)`時，會去判別哪些變數是 **global(外部)** 或是 **local(本身)**

```js
var va = 'globalA';
var vg = 'globalG';

//local:  vb,va
//global: vg
function testScope(){
    console.log("===== outter func start======");
    var vb = 'outterB';
    var va = '@@clone globalA@@';
    console.log(va,vb,vg);

    testScope2();
    //local:  vc
    //global: va,vb,vg
    function testScope2(){
        console.log("===== inner func start======");
        var vc = 'innerC';
        vb = '@@outterB change in testScope2@@';
        vg = '@@globalG change in testScope2@@';
        console.log(va,vb,vc,vg);
        console.log("===== inner func end======");
    }
    console.log("===== outter func end======");
}

testScope();

console.log(va,vg);
```

### 閉包

### 柯里化

### Pure function