---
title: git-command-note
date: 2020-05-02 00:16:49
---


## Git 指令
#### git init
在指定資料夾初始化 git，建立 .git (隱藏的)資料夾

---
####  git status
檢視目前 git資料夾的狀態，分為:	
* Changes to be commited:
> 以追蹤，待上傳檔案
* Changes not staged for commit:
> 以追蹤檔案，但修改過
* Untracked files:
> 尚未追蹤的檔案
* 額外指令: 
> -s:
* 以一行來顯示目前每個檔案狀態
>EX: 
>> AM UnTrackedFile.txt
<br>PS. AM表示兩個區域範圍
* 左邊是 Stage(預存區)，右邊是 Working Directory
    * A = Add
    * M = Modify
    * ? = UnTracked
				

---

####  git add
把指定資料加入暫存區 EX: git add "file name"
指令: 
* git add . : 
> 把目前所在位置包含子目錄全加進暫存區
* git add all :
> 把目前專案所有檔案加入暫存區

---
 			
####  git commit
提交暫存區檔案，讓資料可以儲存讓git管理
* git commit -m "commit info"<----添加此次上傳註解
* 無註解的話，會跑出編輯視窗叫你填寫
    * window:預設編輯器
    * linux:vim
* 不需要註解:
    git commit --allow-empty -m ""
* 額外指令:
    1. -a:
        直接忽略git add，把所有檔案直接提交到 staging Area
    2. --amend
        1. 修改上一次的commit資料

---
 	
####  git log
* 檢視提交紀錄
* 會有的資訊:
    * commit編號(亂碼"Secure Hash Algorithm")，假如目前 HEAD在這裡的話會顯示(HEAD -> master)
    * Author 作者(E-mail)
    * 日期
    * 註解
		
---
 	
* 額外指令:
    * --oneline 把每筆資料，以一行來顯示
    >commit編號(7-8碼) HEAD是否在這 註解&#60;br>
    >f9a2f8d (HEAD -> master) Test Commit 20181105_12:35
    
    * --graph 把目前commit的資料以樹狀圖表示
    
    * --author="name" 尋找作者
    
    * --grep="XXX" 尋找commit的註解裡包含的字
    
    * -S="關鍵字" 尋找檔案內容裡包含關鍵字
    
    * --since --until 查詢時間內的檔案，從日期~時間
    * --after --before 同上
    
    * -p or --patch
    ```
    顯示每次 commit 的跟上一次commit的差別 & 修改的內容 ，
    後面會顯示 diff的內容，
    可以多加 -p -數量，
    決定要顯示幾筆，沒加就是全部
    ```
    * --stat
    ```
    在顯示每筆commit的最後都會有修改的統計
    commit ca82a6dff817ec66f44342007202690a93763949 (HEAD -> master, origin/master,origin/HEAD)
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Mon Mar 17 21:52:11 2008 -0700

        changed the verison number					<---備註

        Rakefile | 2 +-								<---修改的檔案以及修改動作 +是增加 -是減少
        1 file changed, 1 insertion(+), 1 deletion(-)  <---統計
    ```
    * --pretty
    > 更換顯示紀錄格式
    ```
    EX:
    --pretty=oneline
        以一行解決一筆顯示
    --pretty=format:"%h - %an, %ar : %s" (Commit hash)-(Author name),(Author date, relative):(Subject)
        自訂顯示格式
    ```
  
---
 	
####   git rm
刪除在管檔案
* 已有下指令 **EX: add or modified** 尚未commit必須先做完，否則會出現 error
    * error: the following file has changes staged in the index:
    * error: the following file has local modifications:
* 未託管(Untracked)檔案無法用此指令，否則會出現 error
    * fatal: pathspec 'UnTrackedFile.txt' did not match any files
* 刪除在 git status會顯示 **deleted:    FileName**
> 並非未刪除，是還沒commit做好這次的紀錄
* 額外指令:
    * --cached
    > 在暫存區時，退回託管狀態，變成未託管(Untracked)
> PS. 此命令無法影響到儲存庫(Repository)

####  git diff
判斷被託管的檔案差異性
```
L:\Git_Work\Git_Test_20181102>git diff
diff --git a/UnTrackedFile.txt b/UnTrackedFile.txt
index 65ff6f9..3b01642 100644
--- a/UnTrackedFile.txt <--原本
+++ b/UnTrackedFile.txt <---修改
@@ -1,3 +1,2 @@
```
* 當檔案被修改後，被修改的檔案會被移到 Modified，並且保留原本檔案在 staged
* 此指令就是會去判斷這兩個檔案的內容差異
* 兩個數字為一組 - 為舊檔 +為新檔
* 數字是變化起始跟結尾 
    * `-1,3` 就是 舊檔 第1行 - 第3行
    * `+1,2` 就是 新檔 第1行 - 第2行
* 額外指令:
    * --staged
    * --cached
       *  會比較上次 commit的檔案跟 目前在 staged的檔案

---
 		
####  git mv
* 移動檔案 or 重新命名
```
EX:
    git mv FileName NewFileName<---重新命名
    git mv FileName NewAddress/FileName <---移動
```


---
 		

####  git reset &#60;commit id>
退回之前的狀態 or 版本
* 作用於單獨檔案 --> 退回指定檔案 ，狀態變至(UnTracked)
限定在 Working tree，當下的 commit
* 作用於版本 
    * --SOFT <指定版本>
        > 退到 added
    * --MIXED <指定版本>
        > 退到 UnTracked
    * --HARD <指定版本>
        > 檔案完全恢復成指定版本
    *  沒有指令
        > 退回到指定 commit id commit 後的狀態
			
####  git checkout -- &#60;file name>>
Modified 的檔案還原尚未 Modify 時

---
 		
####  git clone &#60;url> &#60;specified dir>
會複製一份指定的 repository 最新的檔案下來到指定資料夾`(包含 .git)`

---
 		
####  git remote
連接指定的 repository  遠端管理

* add &#60; shortname > &#60; url >
    > 加入指定的 url 至本地的 repository shortname是此 url的簡稱
* show &#60;shortname>
    >顯示指定的 remote 資訊
* 額外指令:
    * -v
        >顯示目前有加入多少 remote url

---
 	
####  git fetch &#60;remote shortname> &#60;branch name> :&#60;local new create branch>
把遠端資料同步到本機上，並在現有的 Commit 新開一條分支 origin/master
* remote shortname
    >在 remote 上建立的 遠端簡稱
* branch name
    >在遠端欲要下載下來的分支
* local new create branch
    >下載到指定分支
* 沒有參數以 origin/master 為基準
* 載下來不會做 merge，所以 HEAD 跟 FETCH_HEAD 不會同步

---
 	
####  git pull &#60;remote shortname> &#60;branch name> :&#60;local new create branch>
把遠端資料同步到本機上，資料直接合併為一條 branch
* 同 fetch
* 載下來自動做 merge，所以 HEAD 跟 FETCH_HEAD 會同步

---
 	
####  git push  &#60;remote shortname> &#60;branch name>
把本機上的資料推送到遠端上
	
---
 	
####  git branch
分支管理
* 不帶參數，會顯示目前有多少的 branch
* 參數
    * git branch &#60;branch name>
        > 新建
    * git branch -m &#60;origin branch name> &#60;change branch name>
        > 改名
    * git branch -d &#60;branch name>
        > 刪除，當未合併時，會提醒說未合併，禁止刪除			
    * git branch -D &#60;branch name>
        > 強制刪除

---
 	
####  git checkout &#60;branch name>
* 切換分支
* 沒有指定分支時，切過去會有錯誤
* 參數
    *  git checkout -b &#60;branch name>
        > 判斷有無此分支，沒有會新建再切過去
	
---
 	
####  git gc
處理掉不需要的資源

---
 	
	
