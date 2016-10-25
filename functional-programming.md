---
layout: default
permalink: functional-programming.html
title: 函數式程式設計 Functional Programming
---

# 函數式程式設計 Functional Programming

進階篇討論的重點在於如何組織程式碼，達成易讀、好測試、好擴充、好維護的程式

> [論「為什麼學校教不出好的程式設計師？」](https://www.facebook.com/softdevtools/posts/305785376123355)
> 丁光光: 我覺得這是個paradigm shift。我高中的時候，寫程式就意味著搞懂data structure, 搞懂algorithms, 會用程式語言；如果你還能用數學分析程式執行步驟，你就是老師心目中的超級好學生。當時，寫程式是一種「藝術」，所以，D. E. Knuth的The Art of Programming才會引領整個Computer Science達20年。而能寫出看起來「無懈可擊」、「無法增減一行程式碼」的程式，才是眾人心中的「神」。但現在，寫程式成為一種「工程」。我們除了使用的工具不一樣之外，我們其實跟木匠沒有什麼差別。能夠在空中畫出未來程式的模樣並取得客戶的確認，能夠跟一大群具有同樣技藝的人合作、並在每個專案中發展idioms並建立code review的標準，能夠從架構中切分出任何片段、撰寫、測試還要能不會搞砸系統。而這些能力，只有實作的經驗能夠教導你。而且，這些都是這十年來才被看重的能力。我那些在大學裡教書的同學，就我所知，沒有人瞭解這一塊的重要性，也就沒有人能夠教導。

Pure 純粹 (Pure) 的 Functional Programming Language 雖然過於學術不是主流，但是有一些功能已經廣泛被其他程式語言所之支援，包括：

###  匿名函式 (叫做 anonymous function, code block, 或 lambda )

* First-class Function 函數也是一種資料類型 http://en.wikipedia.org/wiki/First-class_function
  * 範例程式: fun.js 和 fun.rb
* Higher-Order Functions (可將函數當作參數傳遞)，常見用途包括: 1. pre- and post-processing 2. callback function
     * 非常多的 JS 內建 API 使用，例如 forEach (針對容器的 for 迴圈) 
     * 範例程式 
       * callback-simple.js
       * higher-order-fun-pre-post-processing.js
       * higher-order-fun-callback1.js
       * higher-order-fun-callback2.js
       * higher-order-fun-return.js
 

* Closure 特性，函式內可以讀取到函數外的變數，但是不會覆蓋掉，是個非常方便好用的 scope 特性。


    // 範例程式 closure.js
    var foo = 1;
    var bar = function() {
      console.log("inside foo: " + foo);
    }

    bar(); // foo 是多少?

    var baz = function() {
      var foo = 2
      console.log("inside foo : " + foo);
    }
    baz(); // foo 是多少?
    console.log("outside foo: " + foo); // foo 是多少?

* 有些程式語言的 function 定義就帶有 Closure 特性，例如 JavaScript, Scala, Swift。有些則需要用不同的語法，例如 Ruby, Objective-C
     * 在 JavaScript 中:  `function foo() { .... }` 和 `var foo = function() { ... }` 兩者都有 Closure 特性
     * 在 Ruby 中: `def foo` 則沒有 Closure 特性，要 `do ... end` 才有
   * Swift Closure 的 `func` 就有 Closure 特性 https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Closures.html

### Combinator functions: 處理容器的基本三招

 1. filter 2. map 3. reduce (or fold) 很多其他操作都是基於此。這三招又叫作 Combinators，是厲害的 reusable 建構演算法可以組合出複雜的運算。
   * Map https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
   * Filter https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
   * Reduce https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
   * 範例
     * 沒有用 Combinator 之前 combinator-no.js
     * 用了 Combinator 變成 combinator-yes.js
     * 串接綜合應用 combinator-demo.js


### FP 的補充資料
   * 那些 Functional Programming 教我的事 投影片 https://ihower.tw/blog/archives/6513
   * Functional Programming for Java Developers 讀書摘要 https://ihower.tw/blog/archives/6305
