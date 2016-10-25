---
layout: default
permalink: data-structure-algorithm.html
title: 資料結構和演算法
---

# 資料結構和演算法


##  結構化程式設計 Structured programming

* 1960 年代: http://zh.wikipedia.org/wiki/%E7%BB%93%E6%9E%84%E5%8C%96%E7%BC%96%E7%A8%8B「結構化程式設計（Structured programming），一種編程典範。它採用子程式、程式碼區塊、for迴圈以及while迴圈等結構，來取代傳統的 goto。希望藉此來改善電腦程式的明晰性、品質以及開發時間，並且避免寫出麵條式代碼。」
  * Goto: http://zh.wikipedia.org/wiki/Goto
* 程式從可以隨便跳來跳去的 goto 寫法，變成限制成三種流程控制：循序(prodecure)、分歧(if-else)、反覆(while loop)。因此演算法也是由這三大基礎結構所構成。
* 現今的程式語言幾乎都有這些特性，成為「常識」：流程控制(Flow control)和函數(function)
* [演算法](https://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95)是一種有次序、明確定義和可行，最終會結束、有輸出的可執行步驟
* 什麼是「計算性思維? Computational Thinking」
  * 歐巴馬成為第一位寫程式的美國總統，用Javascript！
    * https://studio.code.org/s/frozen/stage/1/puzzle/1
  * http://blog.orangeapple.tw/posts/what-is-computational-thinking/
* 演算法常用結構化形式來描述解決問題的詳細步驟
  * http://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95 求最大值演算法
  * http://www.ithome.com.tw/news/92882
    * http://studio.code.org/s/frozen/stage/1/puzzle/1
  * Big-O 評估演算法複雜度，又分成時間複雜度和空間複雜度
    * https://codility.com/media/train/1-TimeComplexity.pdf
    * https://github.com/ro31337/bigoposter
  * 演法算差異的經典案例: [排序演算法](http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)
    * http://www.sorting-algorithms.com/
    * https://www.youtube.com/watch?v=kPRA0W1kECg
    * 例如: Ruby 提供 Array#bsearch O(logn) 和 Array#select O(n)
  * 資料結構定義資料之間的相互關係，是設計演算法的載體，資料輸入輸出和設計演算法步驟時，都會對應於使用的資料結構。而不同的資料結構有不同的特性: http://bigocheatsheet.com/
    * 最基本常用 Array 和 Hash (Map)
      * 例如: 輸入一個數列，請找出其中重複的數字。資料結構用 Array 還是 Hash 就會造成效能上的差異。 (參考範例程式 array_vs_hash.rb)
    * 特殊的 Array 容器: Stack 和 Queue
    * 面試愛考 Linked List 和 Tree
    * 最短地圖路徑問題用到 Graph 
  * 推薦: 改變世界的九大演算法 http://www.books.com.tw/products/0010644994
* (有些)工作面試很愛考演算法題目，特別是較有規模的公司必考
  * 解題基本策略
    * 先很快的用暴力解(Brute-force)，先別擔心演算法效率
    * 然後再最佳化，找出哪些步驟是多餘重複的計算
  * 需要花時間練習熟悉題型
    * http://www.coderbyte.com/
    * https://leetcode.com/
    * Cracking the Coding Interview, 6/e http://www.tenlong.com.tw/items/0984782850?item_id=1006149
  * 就算你是大神，碰到這種公司(例如 Google)不練習也是 GG
    * https://twitter.com/mxcl/status/608682016205344768
    * http://osherove.com/blog/2011/4/5/my-google-rejection-letter.html
* 設計演算法有沒有什麼設計模式呢? 這些在學校演算法的進階課會教
  * https://en.wikipedia.org/wiki/Brute-force_search 窮舉
  * https://en.wikipedia.org/wiki/Greedy_algorithm 貪婪
  * https://en.wikipedia.org/wiki/Divide_and_conquer_algorithms 分治
  * https://en.wikipedia.org/wiki/Dynamic_programming 動態規劃

## 演算法的極限：計算理論

* 推薦書: 電腦也搞不定, 天下文化
* 不能計算的問題: 例如停機問題 https://zh.wikipedia.org/wiki/%E5%81%9C%E6%9C%BA%E9%97%AE%E9%A2%98
* 問題可以計算，但是算法耗費太多資源或時間(已知最佳解就是指數時間 O(2^N)，而非多項式時間內)，因此不切實際，只能用最佳化逼近解
  * 2^N 太恐怖了，當 N = 100 時，就比大霹靂以來的微秒數還要多
  * 這就作 NP 類型的問題 
    * 例如河內塔步驟，假設有 N 個的環，那麼最佳解的移動步驟是 2^N - 1，原始版本和尚要移動 64 個環根本就不可能。其他像是西洋棋必勝策略也是 NP 類型問題
* 已知有指數時間解，但是不確定有沒有更好的多項式時間解
    * 這就作 NP-Complete 類型的問題 https://zh.wikipedia.org/wiki/NP%E5%AE%8C%E5%85%A8
    * 例如 旅行推銷員問題等種排程、批配、排課問題 https://zh.wikipedia.org/wiki/%E6%97%85%E8%A1%8C%E6%8E%A8%E9%94%80%E5%91%98%E9%97%AE%E9%A2%98
* 於是 [P = NP]( https://zh.wikipedia.org/wiki/P/NP%E9%97%AE%E9%A2%98) 嗎? 


## 補充閱讀

* [Computer Science Field Guide: Algorithms](http://www.csfieldguide.org.nz/en/chapters/algorithms.html)
* [Computer Science Field Guide: Programming Languages](http://www.csfieldguide.org.nz/en/chapters/programming-languages.html)
* [Computer Science Field Guide: Data Representation](http://www.csfieldguide.org.nz/en/chapters/data-representation.html)
* 閱讀 https://codility.com/media/train/1-TimeComplexity.pdf 了解「時間複雜度」
  * 範例的語法是 Python，其中 for i in xrange(n): 等同於 Ruby 的 for i in 0..n-1

