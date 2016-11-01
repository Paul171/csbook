---
layout: default
permalink: database.html
title: 資料庫:基礎篇
---

# 資料庫:基礎篇

* 目標讀者: 應用程式初學開發者，特別是 Application Developer
* 目的: 了解關聯式資料庫和 SQL 語法
* 程式語言雖然有提供 ORM 函式庫方便操作資料庫，但是了解 SQL 仍是非常重要的基礎。因為忽略了 SQL 知識，非常可能造成效能問題。
* 以 Web 後端工程師為目標的同學，需要多加熟悉基本 SQL 和資料庫設計
   * 對資料分析應用有興趣的同學，例如製作報表等等，更需要會學習使用進階的 SQL 查詢
* Mobile 應用則可用於離線 App 或本地快取用途

##  Concept

 * Persistent Storage for your application
 * Flexible Query
 * CRUD: Create, Read, Update, Delete
 * RDBMS: Relational Database Management System
   * Schema: 定義 Tables 和 Columns
   * Data: 每一筆資料即 Row
   * Data Type 每個 Column 會定義格式，每家略有不同，以 MySQL 為例：
     * 字串: Varchar, Text
     * 數字: Int, Decimal, Float
     * 二進位: Blob。但是通常不建議把檔案直接塞資料庫，一來資料庫塞太大不容易備份和管理、二來沒有什麼好處，因為你也沒辦法針對二進位檔案進行條件搜尋和過濾。人們對於讀檔案也有心理準備會比較慢。所以通常只會在資料庫裡面紀錄檔案的 metadata 例如檔名、大小、MimeType 等等
     * Boolean
     * Date
     * Time
     * Datetime
   * [SQLite3 Data Type](https://www.sqlite.org/datatype3.html)
   * Data/Entity Integrity 資料驗證
     * NOT NULL
   * 命名慣例: table 複數，名稱都小寫
 * ACID 特性(Atomicity, Consistency, Isolation, Durability)
   * [Wikipedia](http://en.wikipedia.org/wiki/ACID)
 * Transaction 交易
   * [SQLite is Transactional](https://www.sqlite.org/transactional.html)
   * 當有跨 tables，多個 SQL 必須同時完成才是正確狀態，就必須用上 Transaction。例如銀行轉帳的操作。
   * 但是如果使用 Transaction 範圍過大，連線又多：就會 Lock table 或 row 影響其他使用者，造成效能降低 (這就是為什麼售票網站常常當機的原因)
   * 語法 `BEGIN;   .........;  COMMIT;`
   * 一旦完成 COMMIT，所有連線接下來的 SELECT 都會拿到正確的資料。
 * Why RDBMS?
   * Persistent data
   * Handle Concurrency issues (via transaction)
   * Shared database Integration (with integrity constraint)
   * Standard Model for everyone (using SQL)

##  Databases Systems

 * 開源
   * SQLite3 (嵌入式)
     * Mac 上就有內建 sqlite3 指令
     * GUI: [DB Browser for SQLite](http://sqlitebrowser.org/)
     * GUI: [Firefox Add-Ons: SQLite Manager](https://addons.mozilla.org/en-US/firefox/addon/sqlite-manager/)
   * MySQL
     * GUI: [Sequel Pro](http://www.sequelpro.com/)
     * TABLE 又分不同 ENGINE 實作，InnoDB 和  MyISAM
   * PostgreSQL
     * GUI: [pgAdmin](https://www.pgadmin.org/)
     * 非開源: Oracle、MS SQL Server 等等

建議用 Homebrew 來安裝最新版的 SQLite3、MySQL、PostgreSQL

## SQL Part 1

 * Structured Query Language
 * SQL Query 或 SQL Statement
 * 使用 CLI 或 GUI，用 SQL 語言對資料庫進行查詢和操作
 * 分成 DDL 和 DML 兩種
 * 分號結尾!

### Data Definition Language, [DDL](http://zh.wikipedia.org/wiki/%E8%B3%87%E6%96%99%E5%AE%9A%E7%BE%A9%E8%AA%9E%E8%A8%80)

 * 建立、刪除和更名 Database: 每家方法不太一樣
   * 資料庫需注意 encoding
   * SQLite3:  直接在 Terminal 打 `sqlite3 your_db_name.db` 就會打開(或產生)一個資料庫檔案。直接砍掉檔案就是刪除資料庫。
 * 建立 Table
   * `CREATE TABLE events (name VARCHAR(50), capacity INTEGER, date DATE);`
   * `CREATE TABLE IF NOT EXISTS events (name VARCHAR(50));`
   * `CREATE TABLE IF NOT EXISTS events (name VARCHAR(50) NOT NULL);`
   * 預設允許 `NULL`
   * 比較常見用 GUI 進行操作，或在 Rails 裡面用 Migrations 機制
 * ALTER
   * 改名資料表 `ALTER TABLE events RENAME TO events2;`
   * 新增欄位 `ALTER TABLE events ADD COLUMN status VARCHAR(50);`
   * 修改和移除欄位: SQLite3 沒支援，要 workaround: 開一個新 table 把資料複製過去
 * DROP
   * `DROP TABLE IF EXISTS events;`

通常不會讓終端使用者可以動態新建 table 和修改 schema。database schema 比較像是你程式的一部分，你的 source code 會依賴於 schema 設計。另外也有效能的考量，變更 schema 是很耗時的操作，特別是資料量已經很多的情況下，修改 schema 會鎖住整個 table 影響網站運作。

### Data Manipulation Language, DML

 * CRUD
 * 新增資料
   * `INSERT INTO events VALUES ("RubyConf", 100);`
   * `INSERT INTO events (capacity, name) VALUES (200, "JSConf");`  指定欄位和順序
   * `INSERT INTO events (capacity, name) VALUES (300, "COSCUP"), (300, "OSDC.TW");` 一次插入多筆
 * 修改資料
   * `UPDATE events SET capacity=10;`  會全部修改
   * `UPDATE events SET capacity=100 WHERE name="RubyConf";`
   * `UPDATE events SET capacity=100, name="RubyConf 2015" WHERE name="RubyConf";`
   * 會回傳影響到多少筆
 * 刪除資料
   * `DELETE FROM events;` 會全部刪除
   * `DELETE FROM events WHERE name="RubyConf";`

### Queries

 * 查有哪些 tables 和 columns (各家不一樣!)
   * SQLite3: `.tables` 和 `.schema tablename`
   * MySQL: `show tables` 和 `describe tablename`
   * PostgreSQL: `\dt` 和 `\d tablename`
 * 查詢資料
   * `SELECT * FROM events;`
   * `SELECT name, capacity FROM events;`
   * `SELECT events.name, events.capacity FROM events;`
   * 排序 `SELECT name, capacity FROM events ORDER BY created_at;`
   * 分頁 `SELECT name, capacity FROM events ORDER BY capacity DESC, name ASC LIMIT 20 OFFSET 20;`
   * 只要撈一筆的時候用 ORDER BY 搭配 LIMIT 1
 * 條件查詢
   * `SELECT * FROM events WHERE date = '2015-03-15';`
   * `SELECT * FROM events WHERE date = '2015-03-15' OR  date = '2015-03-16';`
   * `SELECT * FROM events WHERE date BETWEEN '2015-03-15' AND '2015-03-30';`
   * `SELECT * FROM events WHERE date = '2015-03-15' AND capacity >= 100;`
   * `SELECT * FROM events WHERE name LIKE '%Ruby%';`
   * `SELECT * FROM events WHERE description IS NOT NULL;`
 * 小心 case insensitive 不同資料庫預設不同。MySQL 是 case insensitive、PostgreSQL 是 case sensitive
 * 條件查詢需要注意有沒有索引 Index
   * 模糊搜尋 LIKE 查詢會 table scan，資料很大時效能會不好
   * 需要用另外的 Full-Text Searching 引擎

## Database Schema Design

 * 資料庫正規化 Normalization
   * 一個去除重複資料的一個設計程序，將該 column 的資料抽出來成另一個新 table
   * [Wikipedia: 資料庫正規化](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%BA%93%E8%A7%84%E8%8C%83%E5%8C%96)
   * Why? 讓資料不會重複和高度一致性，節省空間、增加修改資料時的效率、避免資料不一致的錯誤
     * 舉例: events table 裡有 user 資料
 * 做營運用途(OLTP)的 schema 通常會達到第三正規化
   * 舉例:  [說明資料庫正規化基本概念](https://support.microsoft.com/en-us/kb/283878/zh-tw)
 * 做分析用途(OLAP)的 schema，則會偏好逆正規化的設計。因為不會修改資料，只會查詢。這領域叫做 Data Warehouse 資料倉儲。從 OLTP 資料庫搬資料轉到 OLAP 的過程就做 ETL (Extract-Transform-Load)

### 設計情境:  紀錄「使用者 User」參與多個「活動 Event」

未正規化:

<table class="table table-bordered">
<thead>
<tr>
<th>user name</th>
<th>user city</th>
<th>zipcode</th>
<th>event 1</th>
<th>event 1 date</th>
<th>event 2</th>
<th>event 2 date</th>
<th>event 3</th>
<th>event 3 date</th>
</tr>
</thead>
<tbody>
<tr>
<td>ihower</td>
<td>hsinchu</td>
<td>300</td>
<td>RubyConf</td>
<td>2015/9/11</td>
<td>JSConf</td>
<td>2015/5/1</td>
<td>CSSConf</td>
<td>2016/1/1</td>
</tr>
<tr>
<td>john</td>
<td>taipei</td>
<td>300</td>
<td>RubyConf</td>
<td>2015/9/11</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

一階: 移除重複語意的 columns


<table class="table table-bordered">
<thead>
<tr>
<th>user name</th>
<th>user city</th>
<th>zipcode</th>
<th>event</th>
<th>event date</th>
</tr>
</thead>
<tbody>
<tr>
<td>ihower</td>
<td>hsinchu</td>
<td>300</td>
<td>RubyConf</td>
<td>2015/9/11</td>
</tr>
<tr>
<td>ihower</td>
<td>hsinchu</td>
<td>300</td>
<td>JSConf</td>
<td>2015/5/1</td>
</tr>
<tr>
<td>ihower</td>
<td>hsinchu</td>
<td>300</td>
<td>CSSConf</td>
<td>2016/1/1</td>
</tr>
<tr>
<td>john</td>
<td>taipei</td>
<td>300</td>
<td>RubyConf</td>
<td>2015/9/11</td>
</tr>
</tbody>
</table>

二階: 移除重複語意的 row

users table

<table class="table table-bordered">
<thead>
<tr>
<th>user id</th>
<th>user name</th>
<th>user city</th>
<th>zipcode</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>ihower</td>
<td>hsinchu</td>
<td>300</td>
</tr>
<tr>
<td>2</td>
<td>john</td>
<td>taipei</td>
<td>300</td>
</tr>
</tbody>
</table>

events table

<table class="table table-bordered">
<thead>
<tr>
<th>event id</th>
<th>event</th>
<th>event date</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>RubyConf</td>
<td>2015/9/11</td>
</tr>
<tr>
<td>2</td>
<td>JSConf</td>
<td>2015/5/1</td>
</tr>
<tr>
<td>3</td>
<td>CSSConf</td>
<td>2016/1/1</td>
</tr>
</tbody>
</table>

registrations table

<table class="table table-bordered">
<thead>
<tr>
<th>user id</th>
<th>event id</th>
<th>register_at</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>1</td>
<td>2016-03-16 12:00:00</td>
</tr>
<tr>
<td>1</td>
<td>2</td>
<td>2016-03-16 12:30:00</td>
</tr>
<tr>
<td>1</td>
<td>3</td>
<td>2016-03-17 12:00:00</td>
</tr>
<tr>
<td>2</td>
<td>1</td>
<td>2016-03-18 12:00:00</td>
</tr>
</tbody>
</table>

 三階: 移除不依賴 primary key 的資料

users table

<table class="table table-bordered">
<thead>
<tr>
<th>user id</th>
<th>user name</th>
<th>zipcode</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>ihower</td>
<td>300</td>
</tr>
<tr>
<td>2</td>
<td>john</td>
<td>300</td>
</tr>
</tbody>
</table>

zipcodes table

<table class="table table-bordered">
<thead>
<tr>
<th>zipcode</th>
<th>user city</th>
</tr>
</thead>
<tbody>
<tr>
<td>300</td>
<td>hsinchu</td>
</tr>
<tr>
<td>300</td>
<td>taipei</td>
</tr>
</tbody>
</table>


   * Primary Key 主鍵 （唯一識別欄位ID）
     * 不能 NULL 也不能重複
     * 通常是 Simple ID Column Key (單一 column)，或是  Compound/Composite Key (多個 columns 組成一個 primary key)
     * 如何選擇你的 Primary Key ?
       * Auto incrementing Primary Key (自動遞增的整數)
       * [UUID 通用唯一識別碼](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E5%94%AF%E4%B8%80%E8%AF%86%E5%88%AB%E7%A0%81): 1. 分散式系統喜歡用 2. 或是當作 token URL 功能
       * Natural key (例如身分證字號, ISBN, 國碼 ISO ALPHA-2)
       * 其實 ISBN 不是好的 primary key，因為?
     * 加 primary key 的 SQL 語法：
       * `CREATE TABLE events (id INTEGER NOT NULL PRIMARY KEY, name TEXT, capacity INTEGER);`
     * 加 auto increment primary key 的 SQL (各家語法不一樣，以下是 SQLite3)
       * `CREATE TABLE events (id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, name TEXT, capacity INTEGER);`
   * Foreign Key (Reference Key)
     * 可以是 NULL 或重複
     * 可以提供 Referential integrity (Reference constraint)
       * 確保新增或修改時，要參考的資料存在
       * 刪除資料時，確保沒有其他資料參考我自己
       * [SQLite Foreign Key Support](https://www.sqlite.org/foreignkeys.html)
       * 你的應用程式可以怎麼處理刪除的情況?
         * 不管它
         * 把相關的 foreign key 設成 NULL
         * 先砍掉相關的資料
     * 命名沒有特別規定，通常是 user_id, event_id 等
 * 關聯設計 Associations
   * ER diagram (entity-relationship model) 一種描述關聯的標準圖表 
   * [Wikipedia](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model)
   * [ERD "Crow's Foot" Relationship Symbols Cheat Sheet](http://www.vivekmchawla.com/erd-crows-foot-relationship-symbols-cheat-sheet/)
   * 1 to 1: 比較不常用，通常只是為了節省查詢量，例如把 BLOB 拆開到另一張表
   * 1 to many
   * many to many，需要 joining table
     * 單純的 joining table
     * 帶有資料的 joining table
     * 舉例: user, course 是多對多關係，joining table 是 memberships。如何用 SQL 撈出該課程 ID 9 的所有學生?
       * `SELECT users.* FROM users INNER JOIN memberships ON users.id = memberships.user_id WHERE memberships.course_id = 9 AND memberships.role = 'student'`
   * 也可以有 self-reference 的情況，例如 Tree 結構
   * polymorphic 設計 (Rails 內建功能)

## Migrations

資料庫 Schema 不是一成不變的，會隨著軟體變更升級也會有修改的需要。

 * Schema Migration
   * 紀錄目前的 schema 版本
   * 開機的時候檢查目前程式的版本和資料庫裡面的版本是否相同，不同的話，執行 migration 更新 schema
 * Data Migration
   * 有時候除了改 schema 也需要調整 data 來符合新的 schema 格式
 * Seed Data 種子資料
   * 有一些資料是一開始就必須存在於 database，這樣 app 才能跑


