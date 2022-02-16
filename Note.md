# ---------陣列相關---------

## 將篩選後的資料放進新的集合中
範例 :

    ClearCollect(
        NewTable,
        Filter(
           設備清單_NotRemoved,
           categoryList1.Selected.Title in Title
        )
    )
* 說明 :
Title 是 '設備清單_NotRemoved' 其中一個欄位，
用 'categoryList1'這個下拉選單所選擇的值篩選 '設備清單_NotRemoved' 這個Collect，再把結果吐到NewTable

## 設定下拉選單的Items
* ['Test1','Test2'] 或是設定其他資料來源，如 : 作業系統.Title

## 抓取陣列第一筆資料
* First([List])或使用Lookup含式

# ---------判斷式相關---------

## if 判斷式
    If([布林],為true做的事,為false做的事);

## 判斷Array 是否為空
    IsEmpty([Array])

## 判斷文字輸入控制項是否為空白
    IsBlank([ControlWithText])

## 字元長度
    Len([Text])

## 判斷List 的 Count
    CountRows([List])

# ---------轉型相關---------

## 轉文字
    Text(12)

## 轉日期
    DateValue('2021-01-01')

# ---------資料篩選---------

## Filter
    Filter(
       設備清單_NotRemoved,
       categoryList1.Selected.Title in Title
    )

* 說明 :
查單或多筆紀錄

## Search
(Filter 也能做到Search 的事情，故不多做說明)

* 說明 :
查單或多筆紀錄

## Lookup
資料表

|  Title  |  Price  |  Tax  |
|  ----  | ---- |  ----  |
|  藍芽耳機  |  2000  |  100  |
|  手機充電線  |  500  |  25  |

* 1.在電子產品List搜尋Title 等於 '藍芽耳機'，並回傳第一筆結果的價格欄位
範例 : LookUp(電子產品List,Title = '藍芽耳機',Price) ，結果 =>  2000

* 2.在電子產品List搜尋價格大於1500，並回傳第一筆結果，Price+Tax欄位
範例 : LookUp(電子產品List,Price > 1500,Price+Tax) ，結果 =>  2100

* 3.搜尋Title 等於 '藍芽耳機'
LookUp( 電子產品List, Title = '藍芽耳機' )

* 說明 :
回傳單筆紀錄

## 如何抓今天的日期
    Today()

# 其他

## Alert (有三種)
    Notify( '欄位未填寫完整:' & errorMsg ,NotificationType.Error,3000);
    Notify( '欄位未填寫完整:' & errorMsg ,NotificationType.Information,3000);
    Notify( '欄位未填寫完整:' & errorMsg ,NotificationType.Success,3000);

## 更新DataSource 的資料
先用Filter 或Lookup 含式把資料撈出來，在使用Patch更新
範例 :

    ClearCollect(
        作業系統_remved,
        Filter(
            作業系統,
            是否刪除 = 0,Title = ItemList作業系統_4.Selected.Title
        )
    );

    If(IsEmpty(作業系統_remved),true,
        Patch( 作業系統, First(作業系統_remved), { 是否刪除: 1});
    );

    If(IsEmpty(作業系統_remved),true,
        Patch( 作業系統, Default(作業系統), { Title: 'test',是否刪除: 1});
    );

## 更新資料來源
    Refresh(作業系統);

## 切換畫面
    Navigate(主功能頁,ScreenTransition.Fade);

## 設定變數(只有全域變數)
    Set(test,'123');

## 設定控制項的預設值
說明 : 控制項的內容需以塞變數的方式設定
範例 :

    If( ItemID > 0,
      varMacAddress,
      ''
    )

## 下載
Download('https://www.123.com.tw')

## 離開應用程式
Exit()