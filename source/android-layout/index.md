---
title: android-layout
date: 2020-04-29 23:21:34
---
## Layout
### LinearLayout:
* 流水型的排版，分為 `horizontal(垂直)` or `vertical(水平)`
    * horizontal:
        預設元件皆往左對齊，並由上至下排版堆疊
    * vertical:
        預設元件皆往上對齊，並由左至右排版堆疊
### RelativeLayout (Legacy):
* 以指定原件為基準點，來進行排版
* 如未有指定，則以父元件左上角為定位點
* 分為 `靠齊(toXXXOf)`、`對齊(alignXXX)`
    * 靠齊(toXXXOf):
        * 顯示方向以指定元件邊(上、下、左、右)為基準點，顯示在指定邊的旁邊
            * layout_above 上
            * layout_below 下
            * layout_toLeftOf 左       
    * 對齊(alignXXX):
        * 指定邊界方向不得變換(上、下、左、右)
        * layout_alignTop 上
        * layout_alignBottom 下
        * layout_alignLeft 左
        * layout_alignEight 右
    * layout_toRightOf 右
```xml
<RelativeLayout
    android:layout_width="409dp"
    android:layout_height="458dp"
    tools:layout_editor_absoluteX="1dp"
    tools:layout_editor_absoluteY="272dp">
    <EditText
        android:id="@+id/txtName2"
        android:layout_width="wrap_content"
        android:layout_height="40dp"

        android:text="txtName2" />

    <EditText
        android:id="@+id/xxx"
        android:layout_below="@id/txtName2"
        android:layout_width="wrap_content"
        android:layout_height="40dp"
        android:text="xxx" />

    <EditText
        android:id="@+id/yyy"
        android:layout_width="173dp"
        android:layout_height="wrap_content"
        android:layout_alignBottom="@+id/xxx"
        android:layout_marginLeft="-2dp"
        android:layout_marginBottom="-116dp"
        android:text="yyy" />
    </RelativeLayout>
```
### ConstraintLayout:
* 約束布局，算是 RelativeLayout的進階版
* 讓XML Code 扁平化，不會要一直塞不同的 Layout來達成畫面
* 任何元件都是可以被依附的對象，可以同時依附不同的元件
    * 每邊都會有一個依附點，包括 BaseLine(內容顯示底線)
    * 每個元件至少要依附 水平、垂直各一點，約束才算成立
    * 跟依附的元件距離是以 Margin 來做定義的
    * 假如依附對象是父類別，並切有兩個相對的依附點(即:上、下 or 左、右)，依附距離各距離50%長度
        * 想改變長度可以設定 Margin or 調整比例 
            * layout_constraintHorizontal_bias:
            > 左右比例:以 0 - 1 (數值為小數位)，由左至右
            * layout_constraintVertical_bias
            > 上下比例:以 0 - 1 (數值為小數位)，由上至下
            * 可調整非 Margin 設定的區域
    * 如果依附元件消失，可預設 layout_goneMarginXXX 來取代消失的元件
* 有關參數都是以 app:layout_constraint... 為開頭
* margin 預設是6dp
* layout_goneMarginXXX，用來取代消失的依附元件，讓元件本身的位置不至於跑掉
* 長度設定有 any size 、 wrap_content 、  match_constraint
    * any size:
    > 自訂義長度
    * wrap_content:
    > 根據自身內容設定長度
    * match_constraint:
    > 根據被依附的原件來設定長度、須相對兩點都有設定(即:上、下 or 左、右)，否則無用
    >>PS.  0dp  = match_constraint
* android.support.constraint.Guideline
    * 建立一個虛擬的參考線，不會出現在實際的畫面上，僅供依附
    * 分為 Horizontal 、 Vertical，
        * android:orientation:"XXX"來設定方向
        * app:layout_constraintGuide_percent 來設定位置  0 - 1 (數值為小數位)
        * Horizontal:
            橫向參考線
        * Vertical:
            垂直參考線

* android.support.constraint.Group
    * 跟 Guideline 很像 ，不過它建立的是一個容器，用來給元件做依附用的
### DrawerLayout:
* 會提供一個抽屜式的選單列表
* 一定會是在layout的最外層
* 新增之後，用手勢向右邊滑動可以打開選單
* 需要用按鈕打開需要另外設置 **ActionBarDrawerToggle** 來提供選單開關
    * 參數:
        * Activity
            當前 Activity
        * DrawerLayout
            要綁定的 DrawerLayout
        * openDrawerContentDescRes
            打開字串，必須寫在 **string.xml** 裡
        * closeDrawerContentDescRes
            關閉字串，必須寫在 **string.xml**  裡
    ```java
    ActionBarDrawerToggle toggle = new ActionBarDrawerToggle(
                MainActivity.this,dlMenu,tl,R.string.drawer_open,R.string.drawer_close
        );
    DrawerLayout.addDrawerListener(toggle);
    toggle.syncState();//讓左上角的按鈕跟 Drawerlayout同步
    //會有一個 "三"的按鈕顯示在左上角
    ```
        
* setNavigationItemSelectedListener 
    * 設定 drawerlayout 選擇事件
        * 實作 new NavigationView.OnNavigationItemSelectedListener
        * Override onNavigationItemSelected(@NonNull MenuItem menuItem)
