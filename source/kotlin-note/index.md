---
title: kotlin-note
date: 2020-04-25 23:30:13
---

### var & val
* var  
    * 變數，內容可更改
* val
    * 常數，給值時定型，就不可在更改了，改了會出錯
* 宣告時 `val | var name[:Type] = value`
    * 給定宣告類型
        * 可以不用給初始值
        * 必須要設定好類型
        * 還未給值時無法使用
        * 說明
            ```kt
            var i:Int
            i = 10
            ```
    * 自動轉換類型
        * 一定要設定好初始值
        * 變數類型由值來決定
        * 說明
            ```kt
            var i ＝ 10
            ```
    * PS. 類型決定好後不能再用**自動轉換**來更改
### 基本類型
* Number Type
    * 整數
        * Long : -2^63-1 ~ 2^63
        * Uint : 2^32
        * Int : -2^31-1 ~ 2^31
        * Short : -2^15-1 ~ 2^15
        * Byte : -2^7-1 ~ 2^7
    * 浮點數
        * Float : -2^31-1 ~ 2^31
        * Double : -2^63-1 ~ 2^63
    
* String Type
    * char
        * 字元
        * 只能容納一個符號
        * 以 **'** 包起來
    * String
        * 字串
        * 字元的集合體
        * 以 **"** 包起來
    * Template Literals
        * 字串板模
        * 以一個字串為模型，把變數塞進來
        * 要塞進來的變數前面要帶 **$** name
        * 如要做運算需加 **{arg...}**

    ```kt
    var c:Char = 'F'
    var s1:String = "Hello"
    var s2 = "World"
    var i = 10;
    var j = 20;

    println("$s1 $s2 , i + j = ${i+j}")
    ```
### Function
* 函式 `fun為關鍵字`
* 宣告為 `fun name(arg1:Type...)[:ReturnType]{ .... }`
* 可重複使用的邏輯
* 需呼叫才會啟用，呼叫為 `name(arg1,arg2)`
* 可設定外部變數帶入，在()裡面設定
    * 多個參數以 **,** 隔開
    * 帶入參數需要設定帶入類型 `arg:Type`
* 非全域變數，無法直接使用
* 由 **{** 開始 ， **}** 結束
* 做完即結束，返回呼叫的地方
* 可有或沒有返回值
    * 有返回值需設定 **Return Type**
* 只有返回值可以用等號 = 把動作寫完
```kt
fun testFn(arg:Int):Int{
    return 10
}

//return this is xxx
fun testFn2(v:Int) = println("this is ${v}")
```

### 存取修飾 Access Modifier
* public - 完全公開
* internal - 只有此 ＊.kt 可看到
* protected - 自己 ＋ 繼承者可看到
* private - 只有自己
> PS.預設為 public

### oject 
* class 關鍵字
* 物件的草圖
* 聲明為 `class name {}`
* 建構子分主、副
    * 主建構子
        * 只能有一個，為建立物件默認選項
        * 寫在 `class name[constructor(arg:Type ....)]`
        * 實作部分寫在 class 內部，加上`init{}`
    * 副建構子
        * 可以根據不同條件分配多個建構子
        * 寫在 class 內部，加上`constructor(){}`
        * 若要繼承主建構子的動作 ，`constructor():this(arg){}`
* proterty
    * 包含 getter & setter
    * 無設定有是單存變數存取
    * 有設定在變數下方做設定
        * set(value)
            * 以 function 的方式，帶入設定值
            * `set(value){ }`
        * get()
            * 以 function 的方式，將變數丟出去
            * `get(){ retrun name }`
        * field
            * 指向變數自己本身
            * 使用此欄位，變數需要初始值
* 繼承 inherit 
    * 關鍵字 **open**，寫在 class 前面
    * 有關鍵字才允許繼承
    * 繼承者要在聲明最後加上 `class sub constructor():FatherClass`
    * override
        * 關鍵字 **open**，寫在 fun 前面
        * 有關鍵字才允許 override
        * 關鍵字 **override**，當繼承者想要使用時，寫在 fun 前
```kt
open class human(){
    var sex:String = "man"
        set(value) {
            field = value
        }
        get() = field
    var age:Int = 0

    init{

    }

    open fun speak(v:String) = println(v)
    open fun see(v: String) = println(v)
}
class User:human() {
    var name = ""
    var userName
        get() = "~$name~"
        set(v){
            name = v
        }

    override fun speak(v: String) {
        println("I'm speaking....")
        super.speak(v)

    }

    override fun see(v: String) {
        println("I'm seeing....")
        super.see(v)

    }
}
```


### if...else
* 是 Statement(陳述句) 也是 Expression(表達式)
* 作為表達式時，一定要有 else
```kt
    var ifi = 20
    var ifj = 3
    //Statement
    if (ifi == 10){
        ifj = 20
    }
    else{
        ifj = 40
    }
    println("ifi = $ifi so ifj=$ifj")

    //Expression
    var if2i = 20
    var if2j = if(if2i == 20){
        60
    }else{
        70
    }

    println("if2i = $if2i so if2j=$if2j")
```

#### when
* 是 Statement(陳述句) 也是 Expression(表達式)
* 類似 switch ... case
* 作為表達式時，一定要有 else
```kt
    var wi = 10;
    var wj = 0;

    when(wi){
        0 ->{
            wj = 4
        }
        10 ->{
            wj=10
        }
        else ->{
            wj = 20
        }
    }
    println("Statement when: wi = $wi so wj=$wj")

    var w2i = 10
    var w2j = when(wi){
        0 ->{
                14
        }
        10 ->{
            1
        }
        else ->{
            30
        }
    }
    println("Expression when: w2i = $w2i so w2j=$w2j")
```



### in 
* 在 Control Flow 裡代表判斷指定項目是否存在於目標裡
* 返回 true | false

### as
* 把變數轉成指定類型
* 無法轉會出錯

### is
* 判斷變數類型是否與指定相似
* 返回 true | false