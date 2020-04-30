---
title: android-lifecycle
date: 2020-04-30 00:03:06
---
## Android 的 APP 生命週期(life cycle)
* App 整體是由一個或多個的 Activity ，所組成的
	* 最根本是一個 ***Task**
	* 裡面排序這個需要用到的  **Activity**
    * 假如 Activity 沒有設定 singleTask，同個 Activity 有可能會有多個
* Activity 代表的是一個畫面的活動，會有開始、結束，整個循環就是生命週期
    * 假如想要增加些指令在某個生命週期階段，必須要 @Override Activity 的生命週期方法
        1. 資源分配
            * onCreate() -建立資訊
            > 開始建立程式， 通常程式都會在此撰寫
            * onDestroy() - 釋放資源
            > 結束 Activity
        2. 可見 與 不可見
            * onStart() - 可見
            > 建立後、還未顯示
            * onStop() - 不可見
            > 畫面準備消失，接續 onPause()			
            * onRestart() - 可見
            >  還未 onDestroy() ，且從別的 Activity 切回此 Activity
        3. 螢幕控制權
            * onResume() - 可控
            >  當從 onPause 切回來時，所啟動的
            * onPause() - 不可控
            >  有其他的 Activity 開啟 或要結束應用程式 

    * Activity 狀態
        1. Active
            1. 當 App 啟動時，顯示在畫面時，所處的狀態
            2. Adnroid 本身只會有一個 Activity在當前執行，如有其他的 Activity則會在背景待命
            
        2. Paused
            1. 畫面按下時、退到背景前，所處的狀態
            2. 只要畫面不是當下的 Activity 都會歸類到這個狀態
                EX: 
                    Alert、Toast
                這些不屬於畫面的東西，當下的 Activity 就會退到 Paused
        3. Stopped
            已不在畫面上的時候
        4. Dead
            1. 尚未被啟用 or 被手動停止 or 被系統回收
* 一個 app 就是一個 process ，一個 process 會存有 多個 Activity
* Android 記憶體不足時，系統回收順序
    1. 非系統的 Receiver 
    2. 非激活狀態的(Stopped)， 
        * Activity
        * Service
        * Intent 
        * Receiver
    3. service 服務
    4. 關閉背景執行的 Activity
    5. 當下激活的 Activity