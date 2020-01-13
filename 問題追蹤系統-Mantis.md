<table>
    <tr>
        <td>問題追蹤系統-Mantis</td>
    </tr>
</table>

## 第零章 目的使用
1.  可使用於開發的專案指派。
2.  可使用於資訊單位客服反映系統。
3.  可以用於CRM管理系統。

## 第一章 安裝使用
#### Step1：免費空間註冊
000webhost 是一家長期提供免費 PHP 與 MySQL 網頁空間的主機商，其背後 Hostinger 這家公司所支持的，其提供免費的主機空間已經長達十年以上。
> 網址：https://www.000webhost.com/

> 特色：永久免費、無廣告

#### Step2：下載Mantis安裝檔案
Mantis是一個很容易安裝的網頁介面問題追蹤系統，協助產品的錯誤追蹤。它需要的環境包括PHP, MYSQL與網頁伺服器，也算容易維護。
> 網址：https://www.mantisbt.org/download.php

![Alt text](https://imgur.com/ukZKFt0.png)


#### Step3：將檔案放置到000webhost
可使用FTP到下面的檔案管理位置將資料上傳，我是直接選擇拖曳上去，算是很方便，大概15分鐘左右即上傳完成。
使用畫面如下
1. 到000webhost的管理者頁面
2. 選擇檔案上傳
3. 將下載解壓縮後的檔案拉上去
4. 回到圖片一可以執行安裝畫面。
![Alt text](https://imgur.com/FIA9qwh.png)
![Alt text](https://imgur.com/Z8ZSFQX.png)
![Alt text](https://imgur.com/R9QVmV2.png)

#### Step4：安裝MYSQL
可到管理者頁面的DB管理頁面，點選新增一個資料庫，會取得資料庫的的DB_NAME與DB_USER，等等再安裝的時候需要指定。
![Alt text](https://imgur.com/IoubNDh.png)

#### Step5：安裝Mantis
到圖片一的首頁進行安裝，建立/設定DataBase
設定帳號、密碼、資料庫名稱-->此為使用圖片四的名字與USER。
我的是使用localhost即可安裝，
記得要先去安裝MYSQL才會有ADMIN的帳號密碼。
此步驟最多問題，可上網查看，通常應該是檢查設定即可。
![Alt text](https://imgur.com/5SX4NmB.png)

## 第二章 測試使用
#### 設定環境
1. 使用A,B兩個專案。
2. 使用user1,user2歸屬到A與B專案

> 文件可參考:https://csie.ntut.edu.tw/sdrc/files/course/20061201/Mantis.pdf

#### 測試結果
1. 專案如設定為不公開，可以達到權限相互看不到反映的資料。
2. 回覆者反映的問題可以自動寄信到使用者信箱。
3. 可以彙總出EXCEL整理問題現況。
4. 可以有三層架構:管理者、開發者、反映者。
5. 可以夾帶檔案與圖片。
6. 免費空間如果頻繁使用會出現
   > #1226 - User ‘id4725367_wp_a62abd88e79bf7abd573b5f9f75fb999’ has exceeded the ‘max_queries_per_hour’ resource (current value: 15000)  由於這是免費託管，因此將會受到限制。但是，000webhost免費託管平台上的可用內容經常被垃圾郵件發送者濫用。
   
###### 整體來說功能算完整且安裝容易，如熟悉環境的還大概60分鐘即可架站完成。
