---
layout: default
permalink: object-oriented-programming.html
title: 物件導向 Object-Oriented Programming
---

# 物件導向 Object-Oriented Programming

範例程式 Sample Code: https://github.com/ihower/intro-to-programming-code (JavaScript、Ruby 和 Swift)

### Why 物件導向? Why 應用程式適合物件導向? 

* 演算法和資料結構：正確性和高效能
* 物件導向：追求 擴充性、維護性、修改彈性、可讀性、可測性。將程式碼適當安排組織的一種設計方式
* 參考投影片 https://www.slideshare.net/ihower/classes-objects-oop p.8 ~ 19
 * Wikipedia 條目: http://zh.wikipedia.org/wiki/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1

## 什麼是物件導向?

 * 可自訂你的 Data Type 類型
   * 有屬性 
   * 有方法
 * 將高相關的資料和他們方法包裹封裝在物件裡面
   * Object = Identify + Behavior + State
 * 以物件為基礎的思考方式    
   * 將世界看作是物件之間一系列的自然互動 (?) 
   * 物件導向是一種用物件來組織程式的方式，不是要映射現實世界。物件是軟體中經常是抽象的概念，而不一定是具體的東西。
 * 不同狀態的物件互相傳遞訊息來通信的方式就是物件導向
   * OOP = objects + messages

### 如何創造物件?

   * 直接創造出來，主流語言只有 JavaScript 支援物件 Literal 寫法
     * 範例 oo-object.js
   * 大多數語言使用 Class-based 基於類別的方式 (JavaScript 要新版的 ES6 才支援)：
     * Class (類別)：定義了某一種物件所擁有的屬性和方法。類別是抽象的事物，而不是其所描述的特定物件。例如 Person 類別表示所有的人。
     * Instance (實例)：由類別產生的物件
     * 建構式，用類別建構出實例時，會執行的方法。用來產生出有不同屬性的不同的物件
     * 範例程式: oo-class.rb 和 oo-class.swift
   * Prototype 基於原型，例如 JavaScript
     * 新物件在初始化時以原型物件為範本獲得屬性
     * 任何物件都可以關聯為另一個物件的原型 (Prototype)
     * 範例程式: oo-prototype.js

### 物件導向的三個機制：封裝(encapsulation)、多型(polymorphism)、繼承(inheritance)

 * 封裝
   * 不需要關心內部結構，只需根據公開介面進行操作
   * 程式只依賴物件的公開介面，而不依賴內部結構
   * 好處是內部的結構可以根據架構需求而修改，而不會影響到其他程式。
   * 範例程式: 
     * oo-encap-no.js 和 oo-encap-yes.js
     * oo-encap-no.rb 和 oo-encap-yes.rb
 * 多型
   * 可以把很多不一樣的東西，當作同一種東西來處理。例如箱子有很多種，打開的實作方式各有不同(有的有鎖、有的沒鎖)，但是這些箱子都有提供「打開」這個介面可以操作。下命令的人只需要知道呼叫這個指令即可。
   * 不需要擔心確切的資料類型，只要介面一致就可以操作
   * 沒有多型的話，單一函數就會充滿根據資料類型的判斷的 if-else，變得難以擴充
   * 範例程式:  oo-poly-no.js 和 oo-poly-yes.js
 * 用繼承來達成多型，以類別為主的物件導向語言，也比較愛用繼承
   * 單一繼承，同時繼承了介面(規格)和實作
     * 範例程式: oo-inheritance.rb 和 oo-inheritance.swift
   * 多重繼承
     * Java、Swift、Obj-C: 可以繼承多重介面(叫做 interface 或 protocol，介面指的是方法名稱和參數列)，但實作部分(指的是方法裡面的程式)則沒有辦法多重繼承，範例程式: oo-protocol.swift
     * Ruby: 用 mix-in 可以繼承多重實作，範例程式: oo-mixin.rb
 * 動態語言更常用 Duck Typing 來達成多型。靜態語言則堅持型別檢查，因此必須滿足繼承條件，才可以達成多型。
   * http://zh.wikipedia.org/wiki/%E9%B8%AD%E5%AD%90%E7%B1%BB%E5%9E%8B
   * 動態語言沒有辦法在 compile-time 做 Type Checking，因此有可能在 run-time 呼叫方法時，才發現 No Method Error 等型別錯誤。
   * 靜態語言會在編譯時會檢查物件的型別，例如參數會限制一定是哪一種類別產生出來的物件。動態語言則不會檢查，採用 Duck typing，一直到真正執行的時候如果 type 不合(例如字串和整數相加)才會發生錯誤
   * 範例程式:  oo-ducktype.rb 和 oo-typecheck1.swift, oo-typecheck2.swift

### 哪些東西是物件?

   * 在 C 語言中，陣列 Array 只是 Pointer 指標
   * 在 JavaScript, Java 中，Array 也是物件。除了Primitive Data Type 的東西都是物件
   * 在 Ruby 中，所有東西都是物件，包括整數、字串等基本型別
 * 認識 [Literal](http://en.wikipedia.org/wiki/Literal_%28computer_programming%29)
   * 程式語言內建的 Value 表示法，例如最基本的數字 123、字串 "test"
   * 大家都有支援 String, Array,Hash 常用的資料結構 Literal notation
   * JavaScript 則有 Object Literal notation
     * JSON，一種 javascript subset 成為跨語言的資料交換格式

Class-based 的物件導向語言，都是要先定義什麼是類別，然後透過類別產生物件。

### 其他注意事項

 * 參數傳遞方式
   * http://en.wikipedia.org/wiki/Evaluation_strategy
   * call by value
   * call by reference(address) 
   * call by object
 * 物件複製 
   * a = b 將物件 b assign 給變數 a：a,b, 指向同一個物件
   * 通常程式語言會另提供一個 shallow clone/copy 的方式來複製物件
 * OOP 中，很少 global function，function 都定義在物件(透過類別)裡面。相關連的變數也都一起包裹在物件裡面。
   * 比較看看不同程式語言的 OO 設計
   * PHP http://php.net/manual/en/ref.strings.php 非常多 global function
   * Python https://docs.python.org/3/library/functions.html 少數的 global function
   * Ruby http://ruby-doc.org/core-2.2.0/String.html 都是物件方法

## 物件導向設計：設計原則和設計模式

* SOLID http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29
* Design Patterns 設計模式，最有名的即 GoF patterns 
   * 針對特定的情境，提供設計解法(通常是如何設計你的類別)，並且「命名」這些模式讓程序員可以方便溝通和當作命名的元素。
   * [設計模式](http://zh.wikipedia.org/wiki/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%EF%BC%9A%E5%8F%AF%E5%A4%8D%E7%94%A8%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%BD%AFE4%BB%B6%E7%9A%84%E5%9F%BA%E7%A1%80)，例如 Factory, Adapter, Composite, Decorator, Iterator, Observer 這些常見模式
     * 範例: oo-strategy.rb, oo-template.rb
   * 推薦這本 http://www.tenlong.com.tw/items/9867794524?item_id=33235

 * 討論: 為什麼用 OOA&D 和 UML 設計軟體的方式逐漸式微?  

> 別擔心，作為應用程式開發的初學者，我們絕大部分需要的類別設計，都由應用程式框架 (Rails、iOS等) 提供了，只要照著框架的規範寫程式即可，一開始不太需要自己設計全新的類別。隨著大型專案的需求，才會逐步需要這方面的知識進行更好的程式架構調整。

### 其他參考資料

* [物件導向基礎與物件導向設計入門 (PHP the day)](https://docs.google.com/presentation/d/1BOnouihveYVoqmlnf59bDeRMfexCw92AVbEHZO9ir8g/edit?usp=sharing)
