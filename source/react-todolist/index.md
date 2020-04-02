---
title: reac-todolist
date: 2020-04-02 21:46:10
---
# React ToDoList
### 程式碼
https://github.com/RobYang203/ReactToDoList.git

#### 資料結構
* id - number
* position - number
    * 所處陣列位置
* type - string
    * w = 待辦
    * d = 刪除
    * f = 結束
* date - date string
* description - string
```js
{
    id:0,
    position:0,
    type: 'w',
    date:'2020-03-27T00:00:00',
    description:'do what'
}
```
#### 畫面
* 外框
    * 輸入區
        * 輸入框
        * 確認按鈕
    * 列表區
        * 單筆事項
            * 顯示資料
            * 刪除按鈕
            * 結束按鈕

#### 元件
* App
    * 功能
        * 維護資料
        * 建立 InputArea 
        * 根據資料建立 DoThingItem
        * 接收 DoThingItem 動作來改變資料
    * 流程
        * 在 `constructor` 建立參數
            * **DoThingList**  - 待辦資料陣列
            * **DoThingCompList**- DoThingItem 元件陣列
            * **state.modifyType** 判斷目前執行動作
        * 針對資料建立三種function
            * `insertItem(text)` 
                * 新增代辦事項到**DoThingList**
                * 參數
                    * text - 需要代辦的事項
            * `finishItem(pos , type)`
                * 待辦事項完成
                * 參數
                    * pos - 在**DoThingList**的位置
                    * type - 切換類型 w | f
            * `deletItem(pos)`
                * 刪除代辦事項
                * 參數
                    * pos - 在**DoThingList**的位置
        * 建立 Component
            * `createItemCompList`
                * 根據 **DoThingList** 去建立 DoThingItem
        * 在`getDerivedStateFromProps` 初始化 state 資訊 
        * 在`shouldComponentUpdate` 驗證是否需要 **re-render**
* InputArea
    * 功能
        * 在`輸入區`輸入待辦事項
        * 按下`確認按鈕`，建立一筆資料格式，保存在`外框`並在`列表區`顯示
    * 流程
        * 從 App 傳入 `insertItem function`，供資料回傳
        * 建立 `sendDate function`
            * 當`Add按鈕`按下去時啟動
            * 沒有輸入會跳出警告視窗
            * 有輸入透過`this.props.insertItem`回傳資料
            

* DoThingItem
    * 功能    
        * `列表區` 根據資料建立`單筆事項`
        * 按下`結束按鈕`，判斷目前資料**type**，訊號送至`外框`改變狀態
            * `type = w` 轉 **f**
            * `type = f` 轉 **w**
        * 按下`刪除按鈕`，訊號送至`外框`，回傳**position**刪除指定資料
    * 流程
        * 從 App 傳入 `finishItem function ＆ deletItem function`，供資料回傳
        * 從 App 傳入 data ，為代辦事項資料，供給元件設定
        * * 在 `constructor` 建立參數
            * itemClass - 顯示是否完成的**css class**
                * `""` - 尚未完成
                * `checked` - 以完成
        * 設定 `itemClick function`
            * 當按下代辦事項啟動
        * 設定 `itemDeletClick function`
            * 當按下刪除按鈕時啟動
        * 在`getDerivedStateFromProps` 根據`props.data `初始化 state 資訊     
            * 根據 **data.type** 判斷 **itemClass** 的值 


