---
layout: default
permalink: database-2.html
title: 資料庫:進階篇
---

# 資料庫:進階篇

## Demo 資料準備(以下是 user 一對多 events 的情境)

* 執行 `sqlite3 demo2.db`


        CREATE TABLE events (id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, name TEXT, capacity INTEGER, user_id INTEGER);
        CREATE TABLE users (id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT, name TEXT);
        INSERT INTO users (name) VALUES ('ihower');
        INSERT INTO users (name) VALUES ('john');
        INSERT INTO users (name) VALUES ('roy');
        INSERT INTO events (name, capacity, user_id) VALUES ('rubyconf',100, 1);
        INSERT INTO events (name, capacity, user_id) VALUES ('jsconf', 200, 1);
        INSERT INTO events (name, capacity, user_id) VALUES ('cssconf', 150, 2);
        INSERT INTO events (name, capacity, user_id) VALUES ('htmlconf', 300, NULL);

## 跨 Tables 進行 Joining 查詢

* Inner joining 合併兩張 tables，接不起來就不要
   * SELECT * FROM events INNER JOIN users ON events.user_id = users.id;
   * 或 SELECT * FROM events, users WHERE events.user_id = users.id;
   * Rails ActiveRecord 的 join 方法預設是用 INNER join
   * Outer joining 合併兩張 tables，接不起就填  NULL
     * SELECT * FROM events LEFT OUTER JOIN users ON events.user_id = users.id;
   * 因為有多張 tables 在 SQL 時，column 最好必須加上 table name 當作 prefix (特別是有重複的 column name 時，在 WHERE 條件裡可能會無法判斷)，而且可以加上別名 AS。
     * SELECT events.id AS event_id, events.capacity AS ec, events.name FROM events INNER JOIN users ON events.user_id = users.id WHERE ec=100;
 * Rails ActiveRecord 的 includes 方法(當沒有 WHERE 過濾條件時)則採用另一種  SQL 策略來作 Outer joining:
   * SELECT * FROM events;
   * 透過程式組合出所有的 user_id 成為 (1, 2, 3, 5, 9, 11, 14)
   * SELECT * FROM users WHERE users.id IN (1, 2, 3, 5, 9, 11, 14);

![SQL Joins](http://i.stack.imgur.com/rOeAz.jpg)
Visual Representation of SQL Joins: http://www.codeproject.com/Articles/33052/Visual-Representation-of-SQL-Joins

![SQL Joins Better](https://lukaseder.files.wordpress.com/2016/07/venn-join1.png?w=662&h=361)
https://blog.jooq.org/2016/07/05/say-no-to-venn-diagrams-when-explaining-joins/

## Functions

資料庫也有提供一些 Function 可以用在 SQL 裡面：

 * 計算 Aggregations
   * SELECT COUNT(*) AS event_count FROM events;
     * 加上 AS 別名才比較好識別處理
   * MIN 和 MAX
     * SELECT MIN(capacity) as min_capacity FROM events;
     * SELECT MAX(capacity) as max_capacity FROM events;
   * SUM
     * SELECT SUM(capacity) as sum_capacity FROM events;
   * AVG
     * SELECT SUM(capacity) / COUNT(capacity) as avg_capacity FROM events;
     * SELECT AVG(capacity) as avg_capacity FROM events;
 * 分類 GROUP BY (搭配上述 aggregating 使用)
   * 如何計算每個 user 有多少 events?
   * SELECT user_id, COUNT(*) FROM events; 這樣不行，user_id 只會回傳第一筆的 user_id
   * SELECT user_id, COUNT(*) FROM events GROUP BY user_id;
   *  SELECT users.name, COUNT(events.id) FROM events JOIN users ON users.id = events.user_id GROUP BY user_id;  這樣會少了 Roy
   * SELECT users.name, COUNT(events.id) FROM users LEFT JOIN events ON users.id = events.user_id GROUP BY user_id;
   * SELECT users.name, COUNT(events.id) AS c FROM users LEFT JOIN events ON users.id = events.user_id GROUP BY user_id HAVING c > 1 ORDER BY c DESC;  可再加條件和排序
   * WHERE 是給 source tables 的條件
   * HAVING 是 aggregation 後的條件
 * DISTINCT
   * SELECT DISTINCT(user_id) FROM events;
 * 字串
   * http://www.tutorialspoint.com/sqlite/sqlite_useful_functions.htm
 * 時間
   * https://www.sqlite.org/lang_datefunc.html

## Performance Issues

 * Indexes 索引
   * WHERE, ORDER 條件欄位最好都要加上 Index，不然會 full table scan 很慢
   * 可以設成 Unique Index
   * 優缺? write 資料時會比較慢因為要建立索引 (也會增加儲存空間)，但是查詢時會大大加快
   * 將欄位設成 unique 跟設成 unique index 是一樣的
   * 加索引的 SQL 語法:
     * CREATE INDEX events_user_id_idx ON events(user_id);
     * CREATE UNIQUE INDEX xxx_idx ON xxx(yyy);
 * 將資料通通撈出來，用程式語言過濾跟組合就好啦? 這樣就不用學複雜的 joining query 了?
   * Speed
   * Space
 * 小心 N + 1 queries
 * 逆正規化 denormalized

## Security

; DROP TABLE students;--
http://xkcd.com/327/
 * SQL Injection
 * http://zh.wikipedia.org/wiki/SQL%E8%B3%87%E6%96%99%E9%9A%B1%E7%A2%BC%E6%94%BB%E6%93%8A
 * 例如以下的程式 :
   * sql = "SELECT * from events WHERE user_id = " + user_input
   * 那麼 user_input = "; DROP TABLE events; " 你就死了
   * 或是略過使用者認證


## Administration

各家指令都不一樣... XD

 * CLI
   * mysql
   * psql
 * Backup & Restore
   * MySQL: mysqldump 和 mysql 指令
   * PostgreSQL: https://ihower.tw/blog/archives/8152

 * Others Database Features

 * Sub Query (Sub Select)
   * Select 的結果也是 table!
   * 例如: 計算每個使用者的最大活動容量的平均
     * SELECT AVG(mec) FROM ( SELECT MAX(capacity) AS mec FROM events GROUP BY user_id );
 * Trigger
 * Views
   * A view 是一個預先設定好的 select query，可以當作 table 使用
   * 就像是將 sub query 抽出來成為設定好的 view 可以重複使用
 * Database replication
   * Master-Slave
   * Multi-master, Cluster

## NoSQL

https://twitter.com/kgen/status/564459555770220544

 * 除了「關聯式」資料庫，還有其他另類的資料庫系統，泛稱 NoSQL
   * http://zh.wikipedia.org/wiki/NoSQL
   * buzzword?
   * why?
     * 關聯式資料庫當初設計並不是用來跑在 clusters  上的，因此當資料和流量成長時，水平擴充就會遇到挑戰
     * 提供不同於 SQL 的資料存取方式 (例如 schemaless, graph database...etc)，來增加應用程式開發的生產力
 * CAP 定理  http://zh.wikipedia.org/wiki/CAP%E5%AE%9A%E7%90%86
     * RDBMS 在多機器(P)架構下為了維持 C 特性，只能犧牲 A
     * NoSQL 讓你有 tradeoff 的空間，犧牲 C 特性以換得 A
     * 但這不是 C 和 A 二元的選擇，而是 C 和 delay 延遲時間的取捨，你願意容忍多少延遲時間才算作不 Available
 * BASE 特性 (Basically Available, Soft state, Eventual consistency)
 * 也有 NoSQL 犧牲(部分) Durability 的能力，來換取更好的效能
 * Key-value: http://redis.io/ 小型資料結構瑞士刀
     * Example Code: https://github.com/ihower/rails-exercise/tree/redis
     * 各式計數器：流量+1
     * 簡易標記( 例如同一 IP 十分鐘內只算一次 pageview)
     * 排行榜 zadd
     * 自製 Inverted-Index Text Search
     * Pub/Sub 聊天室
     * Job Queue (例如 sidekiq)
 * Document-Oriented: http://www.mongodb.org/  Scheme-free、通用型資料庫
 * Column-Oriented:
     * http://hbase.apache.org/ 分散式、強調超大 Table： billions of rows X millions of columns (PB以上等級)  (Google Big Table 的開源版本，由  Yahoo 推出)
     * http://cassandra.apache.org/ 分散式、最終一致性，高寫入場景 (Amazon Dynamo 的開源版本，由 Facebook 推出)
     * http://www.javaworld.com.tw/roller/ingramchen/entry/consistency
 * Graph: http://neo4j.com/ 圖形資料庫
 * 各大 Cloud 平台的專屬 NoSQL (vendor-lock!)
     * http://aws.amazon.com/dynamodb/
     * https://cloud.google.com/datastore/
     * http://azure.microsoft.com/zh-tw/services/documentdb/
 * Schema 繼承設計
     * STI http://www.martinfowler.com/eaaCatalog/singleTableInheritance.html
     * MTI
         * http://www.martinfowler.com/eaaCatalog/classTableInheritance.html
         * http://www.martinfowler.com/eaaCatalog/concreteTableInheritance.html



