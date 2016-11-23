---
layout: default
permalink: networking-http.html
title: "網路概論: HTTP"
---

# 網路概論: HTTP


* Internet 和 Web 的差別是?
* Hypertext Transfer Protocol 超文本傳輸協議，身為 Application Developer 最需要了解的通訊協定
* 歷史： [Tim Berners-Lee](https://zh.wikipedia.org/wiki/%E8%92%82%E5%A7%86%C2%B7%E4%BC%AF%E7%BA%B3%E6%96%AF-%E6%9D%8E), [CERN](https://zh.wikipedia.org/wiki/%E6%AD%90%E6%B4%B2%E6%A0%B8%E5%AD%90%E7%A0%94%E7%A9%B6%E7%B5%84%E7%B9%94)，他發明了 HTTP、URL 和 HTML。例如  「http://」這個符號就是他發明的。
  * HTTP/1.1 in 1999
  * HTTP/2 in 2015
* 請求和回應 Request & Response lifecycle 
  * client -> server
  * response 不限 HTML 格式
* 一個 Request 包括
  * Method
  * URL + parameters
  * Headers
  * Message body (for POST requests)
* Request Methods
  * GET: Safe and Idempotent 的讀取動作
  * POST: Non-safe and non-idempotent
    * 常搭配 application/x-www-form-urlencoded Content-Type
  * PUT: Non-safe but Idempotent 
  * PATCH: Non-safe and non-idempotent 
  * DELETE: Non-safe but 
  * [HTTP Verbs: 談 POST, PUT 和 PATCH 的應用](https://ihower.tw/blog/archives/6483)
* 一個 Response 包括
  * Response Headers
  * Response Body：內容物可以是任何格式，例如 HTML 或 JSON。會在 Headers 裡面用 Content-Type 寫出這是什麼格式
* HTTP Headers
  * Headers are just plain text key-value
  * Request Headers
    * Host
    * User-Agent
  * Response Headers 
    * Status
    * Content-Type
    * Content-Length
    * Location (搭配 301 轉向使用)
* HTTP Status Code
  * 2XX: 成功，例如 200
  * 3XX: 轉向，例如 301 (永久) ,302 (暫時)
  * 4XX: 你的問題: 例如 404
  * 5XX: 伺服器的問題: 例如 500
* Stateless 特性
  * 每個 Request/response 都是完全獨立的 (和前後相比) 
  * 那要如何識別使用者? 每個 Request 都要自帶可以識別的資訊，例如瀏覽器使用 Cookies
  * 使用 set-cookie headers
  * Cookies 的限制
* 資料格式
  * HTML 給是人看的，不適合機器 Parse 解析，當然要爬也是可以，只是一來比較麻煩，二來效率也比較差，也有   人嘗試做 http://microformats.org/
   * XML
   * SOAP
   * JSON
   * MessagePack

##  URL (Uniform Resource Locator)

* [What every web developer must know about URL encoding](http://blog.lunatech.com/2009/02/03/what-every-web-developer-must-know-about-url-encoding)
* 認識 URL 的組成，例如 `http://www.example.com/home`
  * URL scheme: `http`
  * Host: `www.example.com`
  * URL path: `/home`
  * Port number:  http 預設是 80，https 預設是 443。可自訂例如 `http://www.example.com:3000`
* 認識 Query Strings/Parameters，例如 `http://www.example.com?search=ruby&results=10`
  * `?` 保留符號，query string 的開頭
  * `&` 保留符號，分隔
  * Parameter Name/Value: `search=ruby` 和 `results=10`
  * GET/POST 都可以用，但 GET 比較常見，GET Request 也只能用這種方式傳參數給伺服器
  * 限制: 
    * Query strings 有長度限制 (因為整個 URL 長度有限制) 
    * 不適合傳 sensitive information 例如帳號密碼，因為太明顯了
    * 空白和特殊字元必須做逸出 encoded 
* URL Encoding
  * `http://en.wikipedia.org/wiki/Percent-encoding`
  * `Space` 變 `%20`
  * `!` 變 `%21`
  * `+` 變 `%2B`
  * `#` 變 `%23`
  * 其他還有 `/` `?` `:` `@` `&`
* 工具
 * Command Line Tools
   * curl
   * wget
   * [httpie ](https://github.com/jkbrzt/httpie) 可用 brew install httpie 安裝
 * 瀏覽器可使用 Browser Inspector 觀察和 Debug
   * Google Chrome
   * Firefox
 * 安裝 Browser Extension 可以測試 HTTP request 發送
  * Postman
  * REST Client

## HTTPS (TLS/SSL)

* 介紹文章
  * [HTTPS科普掃盲帖](https://segmentfault.com/a/1190000004523659)
  * [HTTPS工作原理](https://cattail.me/tech/2015/11/30/how-https-works.html)
* 如何弄 SSL 憑證
  * 產生 CSR request 憑證簽章要求
  * `openssl req -new -newkey rsa:2048 -nodes -keyout server.key -out server.csr`
    * 其中 Common Name 必須是你的 domain name，例如 `exercise.ihower.tw`。如果是 wildcard certificate 則用 `*.ihower.tw`
   * 這會產生兩個檔案 server.csr 和 server.key 
* 將 .csr 檔案丟給憑證機構做申請，最後會拿到 .crt key
  * 過程會需要認證你真的擁有這個 domain，通常會要求你設定一個特別的 CNAME
  * 也可以自己簽發，只是瀏覽器會警告
    * `openssl x509 -in staging.csr -out staging.crt -req -signkey staging.key -days 365`
 * 將 crt key 跟 server.key 設定到 HTTP Server
* 生活情境：
  * [移除 CNNIC 憑證](https://blog.longwin.com.tw/2010/02/remove-cnnic-ssl-ca-linux-2010/)
  * [刪除CNNIC證書](http://kusowhu.net/mac-os-x-%E4%B8%8B%E5%88%A0%E9%99%A4cnnic%E8%AF%81%E4%B9%A6/)

## HTTP/2

請閱讀 [你的網站升級到 HTTP/2 了嗎？](https://blog.alphacamp.co/2016/07/12/http2/) 這篇文章

## 瀏覽器的 Request/Response Lifecycle

> 以下出自 Coursera Startup Engineering 課程

那麼瀏覽器是如何從輸入 URL 網址到把網頁顯示出來？

1. 在網址列輸入網址，或是點網頁上的超連結
2. 瀏覽器解析這個 URL 找出 protocol、host、port 和 path
3. 如果是 HTTP，則組出 HTTP request 封包
4. 查詢 DNS 用 host 找出對應的 IP 位址，組出 IP 封包
5. 組出 TCP 封包並打開一個 TCP connection 到上述 IP 位址和 Port
6. 送出 HTTP Request 封包
7. Web 伺服器(例如 Nginx)接收到 HTTP Request 封包後，解析其中的內容(特別是其中的 path)來決定如何回應：
8. 如果是靜態內容，也就是 HTTP Response 不會根據不同用戶、不同時間等任何因素而改變，例如圖片、影片、CSS、JavaScript 等等。那麼 Web 伺服器會直接將該檔案回傳給瀏覽器。
9. 如果是動態內容，也就是會根據不同登入的使用者、時間等參數來回傳不同內容，那個 Nginx 會將 HTTP Request 交給應用程式處理，例如 PHP、Ruby、Python、Node.js、Java 等程式，由該程式動態地根據不同參數和條件，搭配資料庫來撈取資料，然後組合出 HTML 網頁包成 HTTP Response 經由 Nginx 回傳給瀏覽器。
10. 瀏覽器接收到這個 HTTP Response，開始解析這份 HTML 網頁成為 Document Object Model (DOM) 一種樹狀的資料結構來對應 HTML 的標籤節點。
11. 瀏覽器會依序檢查 HTML 原始碼中，需要下載的資源網址 URL，例如 CSS、圖片、JavaScript 等等，就會再發 HTTP Request 請求下載回來 (依照上述步驟二到九)
12. 如果下載到 CSS 樣式表，就會去裝飾對應的 DOM 節點
13. 如果下載到 JavaScript 程式碼，則會執行它。瀏覽器上的 JavaScript 程式可以操作 DOM 節點，通常會用 jQuery 函式庫來做，來達到一些網頁動態特效。 
14. 直到所有資源都下載完畢，瀏覽器執行完 CSS 和 JavaScript，才算大功告成完成(Page Load)。如果你又點擊網頁上的超連結，則又回到步驟一。


## 參考資料

* [HTTP 協議入門](http://www.ruanyifeng.com/blog/2016/08/http.html)
* [你應該知道的HTTP基礎知識](http://www.jianshu.com/p/e544b7a76dac)
* [Introduction to HTTP](https://launchschool.com/books/http/read/introduction)
* 圖解 HTTP, 人民郵電出版社
* Coursera Startup Engineering
