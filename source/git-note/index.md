---
title: git-note
date: 2020-05-02 00:17:01
---

#### Git 作業流程
* Git就是一個大倉庫，它為每個專案去建立一個倉庫，
* 把每次提交過的訊息儲存起來，當有需要的時候可以提取處來做更改建立新版本
* 大致分類:
    * 工作區(Working Directory):
        * 已建立git 資料夾(git init)
        * 尚未做任何git動作的區塊
        * 當 git add "file name"指定檔案將會被送進暫存區
    * 暫存區(Staging Area):
        * 別稱 index，通常會放置在 .git/index裡
        * 當 git add 後，會進入到此區
        * 在提交(commit)之前，所屬版本都是同一個
        * 此區不會因為"工作區"修改而改動，但是會去判別是否有改動過(use "git status")
        * 此區的改動不會去影響已經提交(commit)過的檔案
        * 當在此區的檔案同樣會有一份在儲存庫("Repository")裡，其目的，是代表此儲存區在"可提領"(git reset)狀態，可供編輯
        * 在提交(commit)之後，此區檔案將被清空，儲存庫的區域將被封裝，打開下一個可用區域
    * 儲存庫(Repository):
        * 保存每一次提交過的代碼
        * 提交一次，就是一個版本
        * 版本不會被複寫，就算提取(reset)比較早的版本，提交(commit)之後，還是會建立新的版本
        * 此區以樹狀型式來做儲存分為 "master"、"branch"
    * HEAD:
        *  指標類的物件，用來指向目前在那個版本儲存區(分支)

---
 
#### --since --until 、--after --before  差在哪?
查了資料，沒有特別去解釋這部分，好像就是一樣的，既然這樣，為何要多這部分出來
是因為可以讓查詢變得更細麼?
	
---
 
#### 何謂CVCS
**Centralized Version Control Sysyem** 集中式版控(版本控制)管理系統<br>
把每個版本資料集中在一台 Server上，讓用戶去通過這台 Server去查看

---
 
#### 何謂DVCS
**Distributed Version Control System**分散式版控管理系統
每個 client 都會 clone Server ，把資料從Server 複製一份到本地端<br>
當 主Server 有問題時，可以藉由 client端的 clone Server 來恢復 Server資料

---
 
#### Git 儲存方式
在專案裡， Commit(Version 1) ，執行快照(SnapShot)，<br>
就像是拍照一樣，去記錄當前檔案的資訊，<br>
而當下一次的 Commit(Version 2)，執行快照(SnapShot)，<br>
這時會去判斷 Version 1 裡的檔案是否有被變動過，<br>
有，進行 Version 2 的快照，<br>
無，留下 Version 1 快照連結，<br>
當抓取 Version 2，會透過此連結去抓取 Version 1 的檔案資訊

---
 
#### Git 的 三態三域
* 三態， 三種狀態 committed(已提交) 、 modified(已修改) 、 staged(已預存)
* 三域 ， 三個區域對應三種狀態
    * 預存區(staging area) - staged:
        * 又稱index
        * 是一個資訊檔，專們記錄下一次要commit的檔案資訊
    * 工作目錄(working area) - modified :
        * 是從 Git Directory 裡克隆(clone)某一版出來到硬碟裡，目的是要來做修改編輯用的
    * Git 資料夾(Git Directory) - committed:
        * commit 後會把資料檔案放入的位置
        * 放入後將不會再被修改，成為此專案的一個版本
        * 可以提取但只會用複製的方式去做，並不會改動到資料夾裡的版本
   
---
      
#### Git 工具
* git config
    設定一些組態變數的的地方，這些會儲存到三個地方
    * /etc/gitconfig
        * 這裡包含 User 以及 respositores 的資料設定，
        * 如果輸入 git config --system ，設定就會儲存到這裡
        * 因為它是系統設定，需要有管理者的權限
    * ~/.gitconfig or ~/.config/git/config
        * 這裡是個人化設定，
        * 只會影響到 user 本身， 
        * 輸入 git config --global ，
        * 影響到關於此 User 的所有 respositores
    * config(.git/config)
        * 這設定是預設選項，放在 Git Directory 
        * 輸入 git config --local  
        * 可強制讀寫當前的設定
        * 會影響到的是目前正在使用的 repositore 
    * 由上往下，後來者覆蓋前面的設定，所以優先設定會是 "config"
    * 在Windows 這三部分分別儲存在
        *  .gitconfig
            C:\Users\UserName
        *  /etc/gitconfig
            在 window vista以上 ，則會在  C:\ProgramData\Git
  
---
           
#### Git Status
在Git 的目錄裡，會先判斷兩種狀態
* Untracked
    * 在新加入 or 被移除的 檔案，狀態都是 Untracked，代表目前此檔案不被Git所管，被編輯、移除，Git 都不會偵測到
    * 也無法復原 Untracked 的檔案
* Tracked
    被追蹤中的檔案，會去偵測此檔案目前的狀態，一共有三種狀態
    *  Unmodified
        * 此狀態通常會是在，commit 之後，Tracked 的檔案，直接歸到 Unmodified<br>
        * 從別的 server 上 clone過來的檔案，一開始也會是 Unmodified<br>
    *  Modified
        * 只要尚未 commit ，並且在 Tracked 狀態裡，只要改動過檔案，就會被劃分到 Modified
        * 但改動過的檔案會有一份改動之前的版本留在 Statged
        * 如果沒有在重新"git add"，commit的版本會是改動之前的檔案
    *  Staged 
        * 此狀態代表尚未 commit ，是下一次 commit的預備區
        * Untracked 轉移到  Tracked 會直接劃分此區
        * Modified 的檔案需要重新轉移到這裡，否則 commit的檔案會是修改前的檔案
```
打個比方，每一次 commit 都是一集連續劇的其中之一的場景， staged 是舞台 、file 是演員，
演員要開演上舞台，所以要 (add)，把演員(file)推上舞台，
但因應不同的需求，演員需要換服裝，所以下場換(Modified)，
再上場(add)，當這幕結束時，卡(commit)
```

---
 
#### 甚麼是 origin/master , origin/HEAD		
*  origin :
    > 遠端名，在 remote時會建立，假如 remote時不戴 shortname，就會預設 origin
*  master:
    >branch 名，通常在 init 時，就會建一個 master 的 branch
*  HEAD:
    >當前已 commit 的指針
*  幾個和起來的意思就是，
    * origin/master
        *  遠端的 master branch
    * origin/HEAD
        *  遠端當前 commit 
#### 關於 遠端同步
*  把本地資料送到 指定的 遠端 git repo
    *  未同步前
        *  本地 HEAD 高於 FETCH_HEAD
    *  HEAD 同步
        *  git merge FETCH_HEAD
*  把遠端資料 同步回本地
    *   git fetch &#60;remote shortname&#62;
        *  將遠端資料拉回本地
        *  資料尚未同步，此時遠端  FETCH_HEAD 高於 HEAD		
    *  HEAD 同步
        *  git merge FETCH_HEAD

---
 
#### 關於 FETCH_HEAD & HEAD
*  FETCH_HEAD
    *  遠端 repo 的指針
    *  判斷目前位在哪個 遠端的 branch
*  HEAD
    *  本地 repo 的指針
    *  判斷目前位在哪個 本地的 branch
        
>PS.  不是下載後，就算本地，而是要經過 merge 才會讓資料進入本地的 repo

---
 
#### Err
*  warning: LF will be replaced by CRLF
    * 原因:
        > 因為 Window 的換行符號是 CRLF， git add 時，會去轉換成 LF，在提出(checkout)時，轉回 CRLF
    > PS. 不希望 checkout時轉換的話，**git config --global core.autocrlf input**(預設為 true)
        
> PS. CRLF：ASCII 13, \r\n 進行換行，對於 git 中浪費了更多的字元組成換行	
    LF：ASCII 10, \n 僅為換行符號