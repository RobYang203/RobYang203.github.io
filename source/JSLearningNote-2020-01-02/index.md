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

### 閉包(Closure)
* 當建立好 **excution context**，會把`scope`需要的參數都整理好
* 變數是從 **外部** 引入時，數據會保存在此 `scope`
* 把**非local variables**，拉進**excution context**
* 確保數據的隱密性
* 減少外部影響
* 作為一個區域內的公用參數使用
    ```js

    function testClosure(message) {
        setTimeout(function timer() {
            console.log(message);
        }, 1000);
    }
    
    testClosure('Hello, 閉包!');

    function testClosure2(a){

        return function(){
            console.log("closure = " , a);
        };
    }
    var ans = testClosure2(10);
    ans();//closure = 10
    ```

### 柯里化(Currying)
* 將 n 個參數的 function ， 拆解成 1 個參數 n 個 function 
* 即一個步驟，一個 function
* 假如不是結尾，function return next function ，以 **closure** 帶入需要此階段的結果
    ```js
    // x + y
    function normalFn(x,y){
        console.log("normalFn x+y : ",x+y);
    }
    function curryingFn(x){
        console.log("curryingStep1 x: ",x); 
        return function(y){
            console.log("curryingStep2 x+y : ",x+y); 
        };
    }

    normalFn(2,3);
    var step1 = curryingFn(2);

    step1(3);//5
    step1(4);//6
    ```

### Pure function
* 相同的輸入，相同的輸出
* 不會有額外的**副作用(Side Effect)**
* 可移植、可測試
* 不會因為外在環境的變化而改變**function**邏輯

    ```js

    var a = 10;
    function impureFnc(b){
        return a + b;
    }
    impureFnc(5);//15

    function pureFnc(a,b){
        retrun a + b;
    }
    pureFnc(5,10);//15
    ```