---
title: Promise 簡述
date: 2020-06-05 00:43:17
categories:
- jsNote
tags:
- 教學
- JavaScript
- 前端
- es6
---

* 一種機制，可控制回傳值送出的時機
    * 生命週期 PromiseStatus
        * pending
            等待中
        * fulfilled
            已完成，成功
        * rejected
            已完成，失敗
* 實作 `new Promise(cb(resolve,reject))`
    * 回傳參數回兩個 fn ，對應 **fulfilled** 、 **rejected**
    * resolve - fulfilled
    * reject - rejected
* fulfilled 、 rejected 會有特定 fn 來回傳接收的資訊
    * then(cb(data))
        在 fulfilled 回傳 Fn 的成功結果，對應 resolve Fn
    * catch(cb(err))
        在 rejected 回傳 Fn 的失敗結果，對應 reject Fn
* 當程式在 Promise 裡完成後，根據狀態傳給對應 Fn， **資料會儲存在 Promise**，等待呼叫