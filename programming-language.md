---
layout: default
permalink: programming-language.html
title: 程式語言:基礎篇
---

# 程式語言:基礎篇

> 範例程式 Sample Code: <https://github.com/ihower/intro-to-programming-code> (JavaScript、Ruby 和 Swift)

## 什麼是程式語言

* 程式語言用來描述電腦如何工作
  * Powerful
    * 可以處理超多資料、每秒數億次操作(operations)
  * Stupid
    * 每個操作很簡單機械、沒有見解或理解
    * 自然語言會不明確，甚至有錯誤仍然可以理解。但是程式語言需要很精確，有明確的 syntax 語法
      * syntax: 程式語言需要固定語法結構讓電腦可以了解
      * syntax error: 初學者常見的基礎錯誤，對該程式語言不夠了解，或是不小心多加或少加 } { ( ) end 等等
* 不同的程式語言有不同的抽象化方式，用來增加效率
* 低階語言：機器語言、組合語言
  * 程式碼寫起來很費事，但電腦跑起來很快
  * 不同硬體的 CPU 指令集不一樣，例如 Intel x86 和 ARM 不一樣、64位元和32位元也不一樣
  * 執行一行一行的 code instructions，例如將資料從記憶體搬進 CPU 暫存器，接著叫 CPU 進行計算，然後將結果從暫存器搬回記憶體
    * [Wikipedia: Machine code](http://en.wikipedia.org/wiki/Machine_code)
    * [Wikipedia: Assembly language](http://en.wikipedia.org/wiki/Assembly_language)
    * [組語範例](http://ccckmit.wikidot.com/as:msexample)
    * 不同 CPU 的機器碼、組合組言是不一樣的，例如 [Intel x86](https://zh.wikipedia.org/zh-tw/X86) 和 [ARM](https://zh.wikipedia.org/wiki/ARM%E6%9E%B6%E6%A7%8B) CPU。還有分 32位元或64位元。
* 高階語言
  * C 語言、Java 語言、PHP/Python/Ruby 等等
  * 透過結構化程式設計，開發比較好寫，包括 function 子程式、程式碼區塊、for迴圈以及while迴圈等等結構
  * Source Code 純文字檔案經過編譯後(Compile)轉成二進位的機器碼  
  * [第一個C語言編譯器是怎樣編寫的？](http://news.cnblogs.com/n/533687/)
* 為何有不同的程式語言？
  * 效率的定義(是執行快? 還是開發快? )：機器語言 -> 組合語言 -> C 語言 -> Java 語言 -> 動態語言
  * 程式語言設計者的設計哲學不同，有些喜歡設計功能多、程式碼比較有表現力。有些喜歡設計功能進可以必要少，比較簡單但打比較多字。
  * 自然語言會形塑你的思考，程式語言也是一樣，出自 [沙皮爾-沃爾夫假說](http://zh.wikipedia.org/wiki/%E8%96%A9%E4%B8%95%E7%88%BE-%E6%B2%83%E5%A4%AB%E5%81%87%E8%AA%AA)
  * 因應開發不同類型的軟體，有不同的語言設計
  * [因為上帝要阻止人類興建巴別塔](https://zh.wikipedia.org/wiki/%E5%B7%B4%E5%88%A5%E5%A1%94)
* General-purpose 程式語言都是[圖靈完備](http://en.wikipedia.org/wiki/Turing_completeness) (i.e. 跟[圖靈機](http://zh.wikipedia.org/wiki/%E5%9B%BE%E7%81%B5%E6%9C%BA)可以辦到的事情等價)
  * 圖靈用數學證明了機器(任何演算法系統)能夠解決問題的極限
  * [電影「模仿遊戲」](https://zh.wikipedia.org/wiki/%E6%A8%A1%E4%BB%BF%E6%B8%B8%E6%88%8F)

## 如何選擇程式語言

<a href="http://carlcheo.com/wp-content/uploads/2014/12/which-programming-language-should-i-learn-first-infographic.png" target="_blank"><img src="http://carlcheo.com/wp-content/uploads/2014/12/which-programming-language-should-i-learn-first-infographic.png" width="600"></a>

* 各種排名 
  * <http://www.sitepoint.com/whats-best-programming-language-learn-2015/>
  * <http://www.inside.com.tw/2014/11/21/these-programming-skills-will-earn-you-the-most-money>
  * <http://www.greycampus.com/blog/programming/highest-paying-programming-languages-in-2016>
* 電腦軟體可以分成
  * 系統軟體：作業系統、程式語言、編譯器、嵌入式系統等等，不希望有任何效能損耗，需要了解硬體、操控硬體，例如記憶體空間
  * 應用軟體：各種 App、桌面軟體、手機軟體、Web 應用等，效能上可以有 trade-off，好寫好改 vs. 程式執行效能，來因應變來變去的商務需求
* 重點發展
  * C 語言: 自組語之後，最重要的開發效率進步。可用 Pointer 指標操作記憶體，是開發系統程式 (System Programming)、作業系統、編譯器等等工具必備語言。經過編譯可以移植到不同硬體上。
  * C++:  多了一大堆功能和物件導向的超級複雜版 C 語言，大型軟體如 Google Chrome, Qt, WebKit, V8, HHVM 或是效能要求高的遊戲等等，用 C++ 比較多。
  * Java: 提供跨平台 VM、物件導向，開始不行用 Pointer 指標了 (保護開發者不會搞錯記憶體)，導入 GC 記憶體垃圾自動回收。後端很多企業軟體和 middleware 使用，近年則託 Android 在 mobile 世界也佔有一席之地。
  * Objective-C 和 Swift，蘋果專用，也把 C 的 Pointer 拿掉了。
  * Perl/Ruby/Python 動態語言，從 scripting 的需求到 web application 時代的興盛
  * PHP 因為 Web 而發明
  * JavaScript 託瀏覽器的福佔領了世界，近年來用 Node.js 擴展到後端
  * .NET 體系: 跟 Java 一樣的 VM 設計，多語言 VB.NET, C#, ASP.NET, F# 等等
  * Scala/Clojure/JRuby: 建構在 JVM 上
  * Go/Rust 新一代類 C 語言，保護指標
  * Erlang 和 Haskell 等 FP 語言
  * R 統計語言
* 別人用什麼?
  * Java: Google, Oracle
  * Swift, Objective-C: Apple
  * C#: Microsoft
  * PHP: wikipedia, vimeo, facebook
  * Ruby: airbnb, shopify, github, twitter, groupon, basecamp, hulu+
  * Python: youtube, quora, google, instagram, pinterest
* 有許多概念和功能是跨程式語言都有的，只是 ecosystem (衍生出來的套件、社群和支援)不一樣，擅長的情境不一樣，一般來說：
  * 開發系統程式(例如作業系統)，適合 C 語言
  * 開發 Web 後端應用，適合 PHP/Ruby/Python/Node.js 
  * 開發 Web 前端應用，得用 JavaScript
  * 開發 Android 應用，得用 Java
  * 開發 iOS 應用，得用 Swift 或 Objective-C
* 「程式語言」和「程式語言的實作」是不一樣的
  * JavaScript 的語法標準叫做 http://zh.wikipedia.org/wiki/ECMAScript
  * JavaScript 的實作有很多，包括 Chrome 用的 V8、Firefox 用 SpiderMonkey、Safaria 用 WebKit
  * Ruby 則有 CRuby(MRI)、JRuby、Rubunius
  * PHP: Zend 和 HipHop (HHVM by facebook)
  * Objective-C 則謹此 Apple 一家
  * .NET 微軟和 Mono
  * Java: HotSpot (Oracle) 和 OpenJDK
* 選擇語言的衡量因素
  * 社群支援: 用的人多嗎? 可以找到學習資源嗎? 找的到人問嗎?
  * 開發難易度: 開發你要的 app 適合嗎? 開發 chat app? 開發 mobile app? 不同應用適合不同的語言
  * 你身邊有的資源，誰可以幫助你? 例如 ALPHCamp 教 Swift 跟 Ruby、JavaScript，沒有教 C#、PHP
* 跨平台? Virtual Machine 和 Bytecode?
  * Web 跨平台 vs. Java 跨平台有何不同?
* [抽象滲漏法則](http://local.joelonsoftware.com/wiki/The_Joel_on_Software_Translation_Project:%E6%8A%BD%E8%B1%A1%E6%BB%B2%E6%BC%8F%E6%B3%95%E5%89%87)
* 論「使用哪一種程式語言真的不重要，只要能解決問題」？
  * [程式語言沒什麼好學的？](http://www.ithome.com.tw/voice/92041)
  * 為什麼要背九九乘法表?

## 程式語言的分類：動態語言和靜態語言

* 動態語言 v.s. 靜態語言: 
  * 變數的資料類型，是什麼時候決定 (Binding) ? run-time 或 compile-time?
  * 靜態語言需要宣告變數類型
  * JavaScript, Ruby, PHP, Python 是動態語言
  * Swift, Java, C#, C++, C 是靜態語言
  * 優缺點? 1. 開發效率 v.s. 執行效率 2. compile 時可以檢查類型錯誤
  * 近年來由於編譯器的進步，例如類型推導等技術讓靜態語言開發的效率也提升了，因此又看漲了。動態語言陣營也發展出有 type 的用法 [TypeScript](http://www.typescriptlang.org/), [flow](http://flowtype.org/)，和 Ruby 3.0 的 soft type。

以下節錄自 <https://ihower.tw/rails4/intro.html>

為什麼開發伺服器端應用程式，使用動態語言(Ruby、Python、PHP、Perl等)比起靜態語言(Java、C++等)有更好的優勢呢？

靜態語言和動態語言的差別在於，前者的變數型別需要事前宣告，後者則是執行期才動態決定。實務上，就看程式需不需要事前編譯這個動作了。

著名的”人月神話”一書作者Fred Brooks曾說：「一個程式設計師一天能產生的程式碼行數是差不多的，無論什麼程式語言」。因此一個具有表達能力的高階程式語言，就會比低階的程式語言能完成更多功能。相較於靜態程式語言，使用更高階的動態腳本語言可以幫助我們：

* 用更少程式碼做更多事情，大大增加生產力
* 更快因應客戶開發需求，敏捷開發

不過，動態語言也不是沒有缺點：

* 執行效能是絕對比不上靜態語言的
* 沒有編譯期可以檢查型別錯誤

但是，我們知道現在的電腦越來越快、越來越便宜、上網越來越容易、記憶體越來越多、硬碟越來越大。另外，行動裝置也越來越多，需要搭配的網路服務需求也增加了。這些趨勢告訴我們有更多的軟體的需求，另一方面由於硬體效能的增強，人力開發成本比起軟體的執行期的效能，也越來越重要。同樣一個程式，用動態語言執行的效能已經可以達到實用(例如每秒可以處理50~500個的HTTP請求，也可以透過增加伺服器來擴展架構)，也許用靜態語言後的執行速度可以再快一倍，但是卻需要十倍以上的時間來開發，這件事情是不是值得呢？

在硬體資源有限的行動裝置及嵌入式系統上，仍是靜態語言的天下，這一點需要更多時間才有動態語言的生存空間。

沒有編譯期可以檢查型別錯誤的問題，也隨著單元測試和TDD(Test-driven development)測試驅動開發等敏捷最佳實務而逐漸降低重要性。而大部分的Bug會出自於商業邏輯錯誤，而不是型別錯誤上。


## 安裝 JavaScript Runtime

* 直接用 Chrome 的 Inspector Console
* 透過 homebrew  http://brew.sh/ 安裝 Node.js
  * `brew install node`
  * 用 node 即可執行 JS Code
* 使用 Mac 內建的 Webkit JavaScript
  * `/System/Library/Frameworks/JavaScriptCore.framework/Versions/A/Resources/jsc`

## 資料類型 Data Type   
   
* Primitive Data Type 基本資料類型: 
  * String
  * Number
    * Float (雙精確度 64 位元格式 IEEE 754 值)，JavaScript 只支援這種
      * [浮點數](https://zh.wikipedia.org/wiki/%E6%B5%AE%E7%82%B9%E6%95%B0)，可表示任意長度的實數，缺點是輸入與儲存的值不一定精確、計算後的結果可能會有誤差
     * 例如 `0.1 + 0.2 == 0.3 // false in js`，更多 http://0.30000000000000004.com/
    * [Integer](https://en.wikipedia.org/wiki/Integer_(computer_science)) 整數: 電腦內部用[補數表示法](https://zh.wikipedia.org/wiki/%E4%BA%8C%E8%A3%9C%E6%95%B8)轉成二進位儲存 
    * Decimal 固定整數部分和小數部分的位數，可以精準表示，但缺點是無法描述很大或很小的數字
  * Boolean
  * Struct 具有屬性的複合資料類型 (JavaScript 無，Swift 有)
  * JavaScript 中只有 undefined 、 null 、 boolean 、 number 、 string 五種Primitive type
* Reference/Object Data Types 參考資料類型，包括：
  * 程式語言內建的 Data Type (資料結構、容器)，最常見是：
    * Array 有序容器，用整數當作索引
    * Hash (或稱作 Map 或 Dictionary ) 一種 Key-Value 的容器，用字串當作索引
  * 程序員自訂的複合資料類型。例如 C 語言的 struct 結構，在物件導向語言中則是類別 Class 和物件 Object。在 Introduction to Programming Language (進階篇) 會提到
* Strong-Typing 強型別 vs. Weak-Typing 弱型別: 會不會自動轉型，例如數字相加或字串相加時
  * JavaScript 是弱型別，因此 == 和 === 運算子是不一樣的
  * Ruby 是強型別
* 程式語言都會內建有轉型的 API 方法 (可以 google 到作法)
  * 字串轉數字
  * 數字轉字串
  * 字串拆成一個字一個字的 Array
  * 陣列組合回一個字串
  * Hash 轉成 Array
  * Array 轉成 Hash
* 熟習程式語言內建提供哪些操作資料的 API 是基本功
  * [Ruby#String](http://ruby-doc.org/core-2.2.3/String.html)
  * [Ruby#Array](http://ruby-doc.org/core-2.2.3/Array.html)
  * [Ruby#Hash](http://ruby-doc.org/core-2.2.3/Hash.html)
  * [JS#String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
  * [JS#Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
  * [Swift#String](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/StringsAndCharacters.html)
  * [Swift#Collection](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/CollectionTypes.html)

## 變數和作用域 Variable and Scope 

* 值 Value 
  * 不可變的 Primitive data: String, Number, Boolean
  * 或是一種根據屬性(State)識別的 Reference/Object 物件 (叫做 Value Object)
* 變數 Variable，變數就像個標籤指向記憶體中的資料
  * 像一個 Box 帶著一個 Value，可以方便變更這個 Value
  * `=` assignment operator 表示指派一個新資料給這個變數
  * 修改 Primitive data 和 Reference/Object data 的變數，有什麼要注意的：

        var a = 1 
        var b = a // 這時 a,b 指向記憶體中的同一份資料
        a = 2 // b 仍為 1，而 a 換指記憶體中的另一份資料了
 
        var a = [1,2,3]
        var b = a 
        a[0] = 2
        // a 和 b 的陣列都改了
        // 範例程式 var1.rb 和 var2.rb
  * 注意看文件有些 API 是「回傳新的副本」、有些是「In-place」做修改(mutate)
    * 例如同樣是字串  JS 的 a.concat(b) 是回傳一個新字串，a 不變。而 Ruby 的 a.concat(b) 則是直接修改 a。這兩種 API 方式的優缺點是什麼? 為什麼程式語言有時候會同時提供兩種作法? 
  * 比較 Primitive data 和Reference/Object data 的變數，有什麼不一樣?
  * 如何複製 Reference/Object data? 
* 常數 Constant
  * 有些程式語言沒有，例如 Python、JavaScript (ES5)
  * 有些程式有，但是可以改! 例如 Ruby
* 變數命名風格
  * [Camel-Case](http://zh.wikipedia.org/wiki/%E9%A7%9D%E5%B3%B0%E5%BC%8F%E5%A4%A7%E5%B0%8F%E5%AF%AB): Java, Objective-C 用這個慣例 
  * Underscore: Ruby 用這個慣例
  * [匈牙利命名法](http://zh.wikipedia.org/wiki/%E5%8C%88%E7%89%99%E5%88%A9%E5%91%BD%E5%90%8D%E6%B3%95) (已過時)
* [Statement 和 Expression](https://zh.wikipedia.org/wiki/%E9%99%B3%E8%BF%B0_(%E7%A8%8B%E5%BC%8F))
  * Statements 代表動作或指令，不回傳結果而且僅僅運作於它們的副作用上面
  * Expression 是用變數、函式方法和 Value 執行出一個回傳結果
  * 舉例
    * 大部分的程式語言中，控制流程例如 if else 是 statement。而 Ruby 設計成是 expression (事實上，在 Ruby 裡面都是 expression)
    * Python 2 的 print 是 statement，而 Python 3 的 print 變成 expression
    * Python 中 assignment 是 statement，在 JavaScript 和 Ruby 裡面是 expression
  * expression vs. statement
    * expression 表現力強，例如在 Ruby 裡面，可以將 if else 的結果直接 assign 給一個變數
    * 如果 assignment 也是 expression，就可以放到 if 的 condition 裡面。但是不推薦這樣寫，因為人眼會搞混 a == 1。在 Java 裡面直接不允許非 Boolean 在 condition 裡。 Python 也不行。 `if ( a = 1 ) { ... }`
  * Short-circuit evaluation 是最常見的 Expression
   
        c = a || b
        d = a && b
        your_display_name = user.nickname || user.full_name        
  * 需要注意多個 expressions 的優先順序：x && y || z 和 x && ( y || z ) 是不一樣的
    
## 控制流程 Control Flow

* 分支
  *` if (condition) { ... } else { ... }`
  * `if (condition1) { ... } else if (condition2) { ... }`
  * Ruby 寫成 `elsif`
  * case/switch
* 迴圈
  * `while (condition) { ... }`
  * `for..in` (整數遞增或迭代容器內容的一種 while 迴圈) (參考範例程式 for.js)
  * 範例程式 for.js

## 函式 Function

* 可以 reuse 的子程序
  * DRY
* 容易理解: 透過函數的命名可以更清楚知道意圖
* function 和 procedure
  * 早期細分成有回傳值沒有副作用的 function 函式和無回傳值有副作用的 procedure (或 sub-routine) 子程序
  * 已現代實作觀點來看，已經沒有區別
* return 除了放在最後一行，也可以提前返回
  * 有時候用 [Guard](http://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html) 寫法會比較清楚，也就是提早 `return`
* Recursive function 遞迴函數
  * 寫一個計算階層的 function (範例程式 recursive.js)
* 參數傳遞方式  (範例程式 call-by-value-and-object.js)
  * Primitive data type 和 Reference/Object Data Types 不一樣
  * http://en.wikipedia.org/wiki/Evaluation_strategy
  * call by value 
  * call by address 
  * call by object (Javascript, Ruby)
* function v.s. method
  * 其實一樣。只是 function 傾向指 global 的 function。而 method 指物件裡面的函式。
* Argument v.s. Parameter
  * 中文經常翻作「參數」，只是 Argument 比較傾向表示「當作參數的那個變數」
* 可以支援不定參數列，但不同程式語言用不同語法
* 參數可以有預設值 (JavaScript 要 ES6 之後才支援，一般程式語言都有這個功能)

##  作用域 Variable Scope 

* 範例程式 scope.js
* Variable Scope 指的是變數可以被存取到的範圍 Visibility and lifetimes of variables and parameters
* 一般分成 Local variable 和 Global variable
  * 宣告在 function 裡面的 Local variable，只可以在該 function 內存取的到
  * Global variable 則是不管在程式哪裡，都可以存取的到
  * Ruby 還有 Instance variable scope 和 Class variable scope，之後教 Ruby 的物件導向會學到。 
* 避免變數名稱衝突(naming collisions)
* 避免使用全域變數
  * 在 JavaScript 如果少了 var 宣告會變成全域變數 (這是語言設計的錯誤，請體諒他的作者只有[十天](https://en.wikipedia.org/wiki/JavaScript)的時間設計這個語言給 Netscape 瀏覽器)
* 記憶體管理 Automatic memory management
* 不同語言有不同的 namespace 機制跟方式，盡量減少最上層的 Global Variable 數量 (why?)
  * 例如 jQuery 的方法都在 $ 裡
  * 例如 Ruby 用 module

## 參考資料

* [Standford University: Computer Science 101](https://lagunita.stanford.edu/courses/Engineering/CS101/Summer2014/courseware/z54/)
* [代碼之髓：編程語言核心概念](http://www.ptpress.com.cn/Book.aspx?id=38891)
* [松本行弘的程式世界：成為一流程式設計師的14種思考術](http://www.books.com.tw/products/0010476366)
* 演算法的樂趣, 基峰
* [Introduction to Programming with Ruby](http://www.gotealeaf.com/books/ruby)
* [Object Oriented Programming with Ruby](http://www.gotealeaf.com/books/oo_ruby)
* [Seven Languages in Seven Weeks](https://pragprog.com/book/btlang/seven-languages-in-seven-weeks)
* Ruby 物件導向設計實踐