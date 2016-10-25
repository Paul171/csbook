---
layout: default
permalink: programming-language-others.html
title: 字元編碼 Encoding
---

## 錯誤處理 Error Handling

* 程式發生錯誤時如何處理? 兩大處理方式 1. 回傳錯誤碼 2. 拋出例外 Exception
   * 例如: 寫入檔案時空間不足、網路無法連線、除以 0
   * 多數高階語言都有支援 Exception Handling 機制，而 C 和 Go 沒有支援
 * 回傳錯誤碼: 例如函數成功執行回傳 0，出錯回傳非 0
   * 範例 [Error handling and Go](http://blog.golang.org/error-handling-and-go)
 * 一般來說，高階的應用程式比較愛用例外處理(因為 calllstack 比較深，被 call 的程式不一定有處理錯誤的能力)、低階的系統程式愛用錯誤碼(因為你必須處理全部可能的錯誤) 
   * 試比較 Code 可讀性 和 程序員沒有處理 的情況
 * 例外處理的幾個階段
   * try, begin...end 可能會出錯的範圍
   * throw/raise 丟出例外
   * catch/rescue 接收例外。如果沒有補抓到，會往 callstack 上層傳遞 (stack trace)
   * ensure/finaly 無論如何都會執行，用來清理資源
   * 範例程式
     * exception_simple.js
     * exception_callback.js
   * 丟出例外的口語意思是: 這個錯誤我也不知道怎麼處理，我希望有人會處理。如果最後沒有人處理，那就閃退吧! 
 * 錯誤處理也是 API 設計的一部分：有些會提供回傳錯誤碼的形式，有些則是用拋出例外：
   * 例如 Ruby 的 Hash： h[:foobar] 如果沒有值會回傳 nil，但是 h.fetch(:foobar) 則會丟出例外
 * 補充投影片: [如何設計例外處理](http://www.slideshare.net/ihower/exception-handling-designing-robust-software-in-ruby)


## 正規表示法 Regular expression


* 一種精巧比對字串的方式
* [Wikipedia: 正規表示式](http://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)
* 線上工具
  * <http://rubular.com/>
  * <https://regex101.com/>
* 用途舉例：
  * 檢查 "Mississippi" 字串裡面有沒有出現 "ss" ?
  * 找出每段文章中的第三個單字
  * 將文章"開頭"中的 "Dear" 全部用 "Hi" 替換
  * 將文章結尾的"."換成"。"
  * 檢查是否是合法的 Email、URL 自串
* 用法規則
  * `.` 符合任何單一字元
  * `\w` 單字字元
  * `\d` 數字字元
  * `\s` 任何空白
  * `\S` 非空白
  * `^` 行首位置
  * `*` 出現 0 次以上
  * `+` 出現 1 次以上
  * `?` 出現 0 或 1 次
  * `{m,n}` 出現 m 次到 n 次
  * `[a-z]` a 到 z 範圍內的任何單一字元
  * `[^a-z]` 非 a-z 之外的任何單一字元 
* [知道這20個正則表達式，能讓你少寫1,000行代碼](http://www.jianshu.com/p/e7bb97218946)


## 時間處理 Time


* [UTC 時間](http://zh.wikipedia.org/wiki/%E5%8D%8F%E8%B0%83%E4%B8%96%E7%95%8C%E6%97%B6)
* [Unix time 時間](http://en.wikipedia.org/wiki/Unix_time) 計算從 1970-01-01 起跳的秒數，不建議使用這種格式。但有些老派的 API 仍會出現他的蹤影。
  * 新聞 [Apple's 'January 1, 1970' Date Bug](http://www.macrumors.com/2016/02/15/apple-to-fix-january-1-1970-date-bug-ios/)
  * [2038 年問題](https://zh.wikipedia.org/wiki/2038%E5%B9%B4%E9%97%AE%E9%A2%98) (因為 32-bit 的限制)
* 資料交換請用 [ISO 8601 標準格式](https://zh.wikipedia.org/wiki/ISO_8601)
* 時區和日光節約時間的相關問題
  * 只知道時間，不知道時區 -> 無法確定是那一天，不同時區會差一天
  * 只知道時間，不知道確切日期 -> 直接加時間長度可能會不正確，因為可能剛好跨到日光節約時間
  * 結論：用 Date 和 Time 的 library，而不要自己處理，因為日光節約時間[沒有規則](https://www.iana.org/time-zones)


## 資料存續和交換 Data Persistence and Exchange

* 記憶體一關機重開、沒電，資料就不見了，需有一種方式將程式中的資料存進 Disk 硬碟中，永續儲存(Persistence)。例如存成純文字檔案，或是使用資料庫。
* 不同電腦之間，透過網路交換資料，也需要定義資料的格式

### 資料格式有哪些? 
* 程式語言專用的 Marshal 編碼格式，可以支援該程式語言所有的 Data Type，將物件轉成字串文字。
* 跨語言資料格式，支援的 Date Type 有限
   * Human-readable 類型
     * XML
     * JSON
     * YAML
   * Binary 類型
     * [Protobuf](https://github.com/google/protobuf/) (google)
     * [Thrift](https://thrift.apache.org/) (facebook)
     * [Mespack](http://msgpack.org/)
   * 哪一種電腦處理比較有效率? 
   * 哪一種經過長久時間仍能打開讀取?

### 使用資料庫

存成檔案是一種簡單的方法，應用程式更常見的實務作法是採用獨立的資料庫程式，用結構化的格式，提供搜尋、索引、容量能力，或是支援 ACID 操作：

* Persistent 類型
   * Key-Value Storage
   * RDBMS: SQLite、MySQL、PostgreSQL
   * NoSQL
* Non-Persistent Storage，主要是快取用途
   * Memcached
 * 不同資料庫有不同設計 trade-off，包括讀取速度、寫入速度、擴充性和查詢能力
* [為何要使用快取?](https://ihower.tw/rails4/caching.html)
* [Latency Numbers Every Programmer Should Know](https://gist.github.com/jboner/2841832)


## 垃圾回收 Garbage Collection (GC)

 * C 語言需要手動管理記憶體的問題
   * 不心小 free 掉正在使用的記憶體
     * segment fault 閃退
   * 忘記 free 掉: memory leak
     * 吃光記憶體倒站

自動的記憶體管理機制。當一個電腦上的動態記憶體不再需要時，就應該予以釋放，以讓出記憶體，這種記憶體資源管理，稱為[垃圾回收](http://zh.wikipedia.org/wiki/%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6_%28%E8%A8%88%E7%AE%97%E6%A9%9F%E7%A7%91%E5%AD%B8%29)（garbage collection）。垃圾回收器可以讓程式員減輕許多負擔，也減少程式員犯錯的機會。

 * Java, Ruby, JavaScript 都有 GC，一般來說不需要煩惱
   * 還是有可能碰到 memory leak 問題，例如無窮迴圈不斷使用記憶體
 * Objective-C/Swift 不用 GC (OS X 10.8 之後)，使用 Automatic Reference Counting (ARC)
   * strong 變數 vs. weak 變數
   * @autoreleasepool
 * 如何評估 GC 的好壞?
   * Throughput: GC 工作所佔的比例
   * Pause time: 每次跑 GC 造成的暫停時間
 * GC Algorithm
   * Reference count
   * Mark and sweep
   * Generational GC

## 套件管理 Package manager

在程式語言中，一定會用到現成的類別、套件等等。這些來自於：

 * Language core 程式語言本身就有
 * Language build-in library 程式語言內附的標準函式庫，只要載入就可以使用，不需要額外安裝
 * 3-rd party library and framework 需要額外安裝的第三方套件

而當今的程式語言，都有一個套件管理工具(Package manager)，這工具的目的在於：

* 方便安裝和散布上述的這三方套件 
* Dependency 依賴性管理，例如套件A需要套件B 1.1 版、套件C需要套件 B 1.0 版，那麼套件管理工作就會幫你安裝 套件B 1.1 版

例如：

* Ruby 的套件管理工具是 <https://rubygems.org/> 和 <http://bundler.io/>
* Node.js 的套件管理工具是 <https://www.npmjs.com/>
* PHP 的套件管理工具是 <https://getcomposer.org/>
* Swift 可用 <https://cocoapods.org/> (非 Apple 官方)

別跟 homebrew 搞混了，上述的套件管理工具是管理「程式碼」套件，而 homebrew 是我們在 Mac 上管理「Command Line 工具」的套件。之後我們在 Ubuntu Linux 上，還會用一個套件管理工具叫做 `apt-get` 用來在伺服器上安裝軟體。

## 編碼風格 Coding Style

 * 同一件事情，有很多種作法，用哪一種好呢? 
 * 每個程式語言都有各自的寫碼風格
 * 每個開發團隊也有自己偏好的寫碼風格
 * http://udacity.github.io/frontend-nanodegree-styleguide/index.html
 * https://github.com/thoughtbot/guides/tree/master/style

## 開放原始碼 Open Source

* [為什麼很多優秀的軟體公司和開發者願意開源和共享？](https://share.inside.com.tw/posts/27427)
* [開放原始碼](https://zh.wikipedia.org/wiki/%E5%BC%80%E6%94%BE%E6%BA%90%E4%BB%A3%E7%A0%81)
* [自由軟體(Free Software)](https://zh.wikipedia.org/wiki/%E8%87%AA%E7%94%B1%E8%BD%AF%E4%BB%B6) v.s. [開源軟體 (Open Source Software)](https://zh.wikipedia.org/wiki/%E5%BC%80%E6%BA%90%E8%BD%AF%E4%BB%B6) 兩者的理念不同
  * http://www.openfoundry.org/tw/legal-column-list/508-2010-07-15-10-50-34
* 因此授權可概分這兩大門派：
  * [GNU通用公眾授權條款](http://zh.wikipedia.org/wiki/GNU%E9%80%9A%E7%94%A8%E5%85%AC%E5%85%B1%E8%AE%B8%E5%8F%AF%E8%AF%81)：GPL不會授予授權條款接受人無限的權利。再發行權的授予需要授權條款接受人開放軟體的原始碼，及所有修改。且複製件、修改版本，都必須以GPL為授權條款。
  * BSD、MIT、Apache 派：只要你不宣稱這軟體是你製作的，你要做什麼都可以。
* [如何選擇開源許可證？](http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html)

<img src="http://image.beekka.com/blog/201105/free_software_licenses.png" width="800">

* 非軟體程式的文字、音樂、影片等等創作，可以用 [創用CC授權條款](http://creativecommons.tw/license)

