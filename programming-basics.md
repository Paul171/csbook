---
layout: default
permalink: programming-basic.html
title: 程式設計基礎
---

# 程式設計基礎

 * 目標讀者: 程式設計初學者
 * 目的: 了解程式語言基本語法，包括標準輸出輸入、控制流程、變數、資料類型(數字、字串)、函式、陣列、雜湊、物件、檔案
 * Example Code:
   * <https://github.com/ihower/programming-basics>
   * <https://github.com/yangliyi/programming-basics-in-ruby>
 * 使用環境
   * Mac: 使用內建的 Ruby 和編輯器 <https://www.sublimetext.com/>
   * Non-Mac: 可使用 <https://c9.io/> 開一個 Custom 的 workspace

## 1. 基本元素: 輸入、計算、輸出

 * 標準輸出
   * print
   * puts
 * 什麼是變數: 讓電腦(記憶體)記住值(value)，就像一個 Box
   * = assignment operator
 * 資料型別
   * 整數 Integer (不可以有小數)
   * 浮點數 Float (可以存放小數)
   * 字串 String
     * 如何換行?
     * 如何逸出 " 和 '
 * 算術運算子 + - * / %
 * 標準輸入
   * gets
   * 讀進來的資料都是字串
 * 註解
 * 常見錯誤
   * Syntax Errors
   * Type Errors，例如
     * 數字和字串的相加
   * Logic Errors，例如
     * 整數除整數還是整數
 * Exercises
   * 變數交換: 假設有 a,b 兩個變數，請交換兩者的值
   * 使用者輸入名字，輸出 "Hello, 名字"
   * 使用者輸入直角三角形的寬和高，輸出三角形的面積

##  2. 控制流程

 * Conditional Control 條件控制
   * 布林 Boolean 資料型別: true 或 false
   * 關係運算子 == != < > <= >=
   * 邏輯運算子&& ||  !
 * Control Flow 控制流程
   * if else
 * Exercises
   * 使用者輸入一個數字 x，請判斷是否正數、零或負數，以及是不是偶數
   * 使用者輸入 x,y,z，請根據以下的 decision tree 輸出結果
     * 當 x < 0 輸出 "A"
     * 當 x > 0
       * 當 y > 0
         * 當 z > 0 輸出 "B"
         * 當 z < 0 輸出 "C"
       * 當 y < 0
         * 當 z > 0 輸出 "D"
         * 當 z < 0 輸出 "E"
     * 使用者輸入 x,y,z，請輸出三個數中最大的數
     * 使用者輸入 x,y,z，請從大到小重新輸出

## 3. 迴圈結構

 * while loops
   * 手動中斷 break
   * 提前進去下一個迴圈 continue
 * 常見錯誤:  while 的終止條件沒有滿足，變成無窮迴圈
 * Exercises
   * 求 1~100 所有偶數的和
   * 輸入一個數字 N，輸出 N * N 乘法表，例如輸入 12，輸出
     * 0 x 0 = 0
     * 0 x 1 = 0
     * ......
     * 12 x 11 = 132
     * 12 x 12 = 144
   * 輸入一個數字 N，請檢查是不是質數
     * Hint: 從 2 開始到 N/2 不斷去除這個數字，如果可以整除就表示不是質數


## 4. 資料結構: 陣列 Array

 * 數字 index 的容器
 * 一維陣列
 * 二維陣列
 * for loops 走訪
 * Exercises:
   * 給定一陣列內含數字，輸出最大值
   * 使用者不斷輸入數字存進 Array，最後輸出總和、平均、最大值、最小值
   * 建構一個陣列有一百個的元素，內容是 0, 1, 4, 9, 16, 25...... 每個元素是該索引的平方
   * 給定一陣列內含數字，請輸出 0~9 中不見的數字。例如 arr = [2,2,1,5,8,4]，輸出 [0,3,6,7,9]
   * 實作[選擇排序法](https://zh.wikipedia.org/wiki/%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F)

## 5. 資料結構: 雜湊 Hash

 * 又叫做 Dictionary
 * key-value 的容器
 * for loops 走訪
 * Exercises:
   * 給定一 Hash，輸出有最大 value 的 key
   * 給定一 Hash，輸出 value 是偶數的 keys

## 6. 函式 Function

 * Exercises
   * 實作一個 function 可以輸入陣列，回傳總和
   * 實作一個 function 回傳階乘數 (請用遞迴)

## 7. 資料結構: 物件 Object

 * 內建的 Object
   * [String](http://ruby-doc.org/core-2.3.0/String.html)
     * 將字串拆解成陣列
   * [Float](http://ruby-doc.org/core-2.3.0/Float.html)
     * 四捨五入
   * [Array](http://ruby-doc.org/core-2.2.3/Array.html)
     * 將陣列串接成字串
       * push
     * delete_at
   * [Hash](http://ruby-doc.org/core-2.2.3/Hash.html)
     * keys
     * values
 * 透過 Class 類別來自訂 Object
 * Exercises
   * 自訂一個 Person 物件，屬性有 first_name, last_name, height, weight，定義一個 method 是 greet 輸出 "Hi, <first_name> <last_name>"  和另一個 method 是 bmi 輸出 BMI

## 8. 檔案處理

 * Why? 資料持久化
 * 開檔讀取
 * 寫入檔案
 * Exercises
   * 給定 words.txt，計算每個單字出現的次數
   * 給定 hash of array，輸出 CSV 檔案

## 9. App 應用

 * 利用檔案儲存資料來製作一個 Todo program
   * 檔案 todos.txt 每一行代表一個 Todo，格式例如
     * 寫作業
     * 買東西
     * 吃飯
   * 執行這個 program 時，讀取這個檔案，並顯示目前所有 Todos 和數量
   * 輸入 add XXX，則會新增這一筆，編號累加
   * 輸入 remove 編號則會刪除這一筆
   * 輸入空白則會離開，並存檔

## 參考資料

 * [啊哈C！蹲馬桶就能看懂程式的邏輯訓練](http://www.books.com.tw/products/0010630098)
 * [Exercises for Programmers](https://pragprog.com/book/bhwb/exercises-for-programmers)
 * [Computer Science Programming Basics in Ruby](http://shop.oreilly.com/product/0636920028192.do)
 * [Swift 程式設計入門](http://www.books.com.tw/products/0010668967)

