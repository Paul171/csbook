---
layout: default
permalink: encoding.html
title: 字元編碼 Encoding
---

# 字元編碼 Encoding

* 每個軟體開發者都絕對一定要會的Unicode及字元集必備知識
  *  http://local.joelonsoftware.com/wiki/The_Joel_on_Software_Translation_Project:%E8%90%AC%E5%9C%8B%E7%A2%BC
  * http://www.jianshu.com/p/bd7a6c508c33
* ASCII (1 bytes) http://zh.wikipedia.org/wiki/ASCII
* [亂碼](https://zh.wikipedia.org/wiki/%E4%BA%82%E7%A2%BC)
* Unicode
  * UTF-32 每個字元都是 4 bytes，浪費空間 
  * UTF-16 (2 或 4 bytes，中文為 4 bytes)，是許多程式語言內部儲存的方式 (Ruby 除外)
  * UTF-8 (不定長度 1~4 bytes，中文用 3 bytes)，ASCII 是 UTF-8 的子集，因此廣泛應用在 HTML 上
  * http://en.wikipedia.org/wiki/Comparison_of_Unicode_encodings
  * http://www.w3.org/International/questions/qa-choosing-encodings
* Big5 (2 bytes) 過時了
* [BOM](http://zh.wikipedia.org/wiki/%E4%BD%8D%E5%85%83%E7%B5%84%E9%A0%86%E5%BA%8F%E8%A8%98%E8%99%9F) 標記不建議 UTF-8 使用，造成的問題比當初想要解決的還要多   
