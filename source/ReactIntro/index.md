---
title: React Intro
date: 2020-02-28 03:57:21
---

# React
## 介紹
* 基於 javaScript 建立的函式庫
* 模擬 DOM 元素的運作模式
* 以 **Virtual DOM** 模式處理 DOM 元素的變化
    * 在記憶體裡模擬 DOM 結構
    * 最後顯示到真實的 DOM 只有結果
    * 在進行真實的 **DOM render** 時
        * 會先判斷改變的部位，針對那部分做 **render**
    * render 時，預設會把此 DOM 裡包含的 全部 **re-render**
* 封裝成 **React Component** 
    * 可獨立執行， 以 Component 做最小單位 
        * Component 內的元素獨立執行，不會影響到外部
    * 可結合(Composable)
        * Component 可互相交流、做組合，產生新的 Component
    * 可重用（Reusable）
        * 因為是獨立執行，所以可以在任何的場合做使用
    * 可維護（Maintainable）
        * 以最小功能為基準做的 **Component** ，去掉複雜性可供維護
* 事先把 **Component** 全都組成 **Virtual DOM** ， 調整好變化再去做 render 的動作
* 建立 **jsx** 語法糖， 簡化開發

## 語法
* 建立 Component for **ES6**
    1. 繼承 **React.Component** or **React.PureComponent**
    2. 實做 render 
        ```js
        class App extends React.Component {
            render() { 
                return (
                    //...
                ); 
            } 
        }
        ```
  
* render 到 html 頁面
    ```js
    ReactDOM.render(< ReactDom />, document.getElementById("XXX"));
    ```
    
    
* `state` 、 `props` 、 `ref`
    * state
        * 針對會改變 **React DOM** 狀態 的設定參數，
        * 先在 constructor 設定 this.state
           ```js
           this.state.key = value
           ```
               
        * 當要重新設定狀態時，呼叫 `this.setState({key:value})`，會觸發 **re-render** ， 重新設定 **React DOM** 
        * state 只會在 Class 內部運轉
        > PS. 沒在 constructor做宣告的話，會出錯
    * props
        * 因為 **React DOM** 的封閉、可重複使用特性 ， 外部需要跟 **React DOM**  溝通時，透過 `props` 設定參數
        * `props` 可傳遞的參數由建立  **React DOM** 的建立者，做 設定、開放
        * `props` 是**唯讀屬性**，只能讀不能複寫，也不能建立新值
        * 當參數傳入時，會觸發 **re-render**
        * 可在內部class任意使用
            ```js
            // js
            React.createElement(
                DEMO,
                {
                    value:"123456",
                    value2:1111
                },						
            );
            // jsx
            <DEMO value="123456" value2=1111 />
            ```
                    
        * JSX的部分會直接轉成
            ```javascript
            props={
                value:"123456",
                value2:1111
            }
            ```
            
    * ref
        * 以原生的 dom  ，ref 就是 JS  document.getElementById()
        * 以 React DOM ，就是會獲得被 new 出來的  實例
        * 會使用通常是 在 render 時無法做的動作 或是 針對 DOM 做特定操作
            * 官方說法是 `input.foucs()` 、 `input.value` 、 `video.play()`
        * 在 constructor 宣告參數 this.XXX
        * 在指定 tag 上加入 `ref ={this.XXX}`		
        * 使用方式:
            * callback
                ```jsx                
                <Component  ref={(ref)=>{ this.ref = ref}} />
                ```
                
            * 呼叫 React.createRef() -> **react 16.3**
                ```js
                class App extends React.Component {
                    constructor(props){
                        super(props);
                        //在 constructor
                        this.ref = React.createRef();
                    }
                    //在 render
                    render() { 
                        return (
                            <Component  ref={this.ref}/>
                        ); 
                    } 
                }             

                ```                
                 
## life cycle	
* ver 16.x
* 分四階段 `Mounting (載入中)`、 `Updating (更新中)` 、 `Unmounting(卸載中)` 、 `error(錯誤)`
    * Mounting
        * 元件建立的流程，還未再入到實體網頁時
        * 流程
            1. constructor
                * 物件建立時會啟用的地方
                * 只會執行一次
            2. componentWillMount -> `17 will remove`
                * 觸發時機
                    * 建立 Component 時
                * 只會執行一次
                * 物件移除再建立也不會執行(指的是從 react DOM 上移除，不是 new 一個新的)
            3. static getDerivedStateFromProps(nextProps, prevState)  -> `16 new`
                * 觸發時機 
                    * 在傳入 new props 尚未更新 props ， 已更新 state 以及將要 render之前
                    * 用 `this.setState()` 觸發 re-render ， 會先更新完 state 再觸發 `getDerivedStateFromProps`
                * 事件說明
                    * 判斷是否要用 props 更新 state
                    * 回傳 obj 更新 state ， return null 維持原樣
                * 參數
                    * nextProps
                        * 最新的 props
                    * prevState
                        * 更新前的 state
            4. render
                * 觸發時機
                    * 建立 物件時
                    * 呼叫 this.setState()
                    * 從上面傳 props 時
                * 事件說明
                    * 設定 react element 的地方
                    * return boolean | null 則代表無元件顯示
                    * return react element (jsx)
                    * 呼叫後 ，尚未顯示在網頁上，要把 react virtual DOM 轉成 **實體 DOM**
            5. componentDidMount
                * 觸發時機
                    * 元件掛載到實體網頁時
    * Updating
        * 元件畫面更新的流程，再觸發 re-render 會啟用
        * 流程
            1. componentWillReceiveProps(nextProps) -> `17 will remove`
                * 觸發時機
                    * 從上面傳下來的 props 發生變動時
            2. getDerivedStateFromProps
                * 同 mounting
            3. shouldComponentUpdate(nextProps, nextState)
                * 觸發時機
                    * 在 `componentWillReceiveProps` &  `getDerivedStateFromProps` 之後
                * 事件說明
                    * 判斷 React Component 是否該更新畫面
                    * return true updating 持續進行 
                    * return false  updating 中斷，將不觸發 re-render
                * 參數
                    * nextProps
                        * 新的 props
                    * nextState
                        * 新的 state
            4. componentWillUpdate（nextProps, nextState)  -> `17 will remove`
                * 觸發時機
                    * render 之前
                * 事件說明
                    * 將要 render
                * 參數
                    * nextProps
                        * 新的 props
                    * nextState
                        * 新的 state
            5. render
                * 同 mounting
            6. getSnapshotBeforeUpdate(prevProps, prevState) -> `16 new`
                * 觸發時機
                    * render 之後 ， 尚未更新到實體網頁
                * 事件說明
                    * 取得更新前的數據
                    * 回傳直將會變成`componentDidUpdate`第三個參數
                    * 沒有回傳值，`return null`
                    * 有使用到此事件，需要再加入`componentDidUpdate`，否則會報錯
                * 參數
                    * prevProps
                        * 舊的 props 
                    * prevState
                        * 舊的 state
            7. componentDidUpdate(prevProps, prevState, snapshot)
                * 觸發時機
                    * 更新實體畫面之後
                * 事件說明
                    * 已經完成實體畫面更新
                * 參數
                    * prevProps
                        * 舊的 props 
                    * prevState
                        * 舊的 state
                    * snapshot
                        * 由前面`getSnapshotBeforeUpdate`的回傳值
    * Unmounting
        * 流程
            1. componentWillUnmount
                * 觸發時機
                    * 元件要被移除之前
    * error
        * 流程
            * getDerivedStateFromError
            * componentDidCatch
                
			

		