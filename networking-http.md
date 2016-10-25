---
layout: default
permalink: networking-http.html
title: "網路概論: HTTP"
---

# 網路概論: HTTP


* Internet and Web 的意思有差別嗎?
* Hypertext Transfer Protocol 超文本傳輸協議，身為 Application Developer 最需要了解的通訊協定
* 歷史： [Tim Berners-Lee](https://zh.wikipedia.org/wiki/%E8%92%82%E5%A7%86%C2%B7%E4%BC%AF%E7%BA%B3%E6%96%AF-%E6%9D%8E), [CERN](https://zh.wikipedia.org/wiki/%E6%AD%90%E6%B4%B2%E6%A0%B8%E5%AD%90%E7%A0%94%E7%A9%B6%E7%B5%84%E7%B9%94)，他發明了 HTTP、URL 和 HTML。例如  「http://」這個符號就是他發明的。
  * HTTP/1.1 in 1999
  * HTTP/2 in 2015
* Request & Response lifecycle 
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

###  URL (Uniform Resource Locator)

* [What every web developer must know about URL encoding](http://blog.lunatech.com/2009/02/03/what-every-web-developer-must-know-about-url-encoding)
* 認識 URL 的組成，例如 http://www.example.com/home
  * URL scheme: http
  * Host: www.example.com
  * URL path: /home
  * Port number:  http 預設是 80，https 預設是 443。可自訂例如 http://www.example.com:3000
* 認識 Query Strings/Parameters，例如 http://www.example.com?search=ruby&results=10
  * ? 保留符號，query string 的開頭
  * & 保留符號，分隔
  * Parameter Name/Value:  search=ruby 和 results=10
  * GET/POST 都可以用，但 GET 比較常見，GET Request 也只能用這種方式傳參數給伺服器
  * 限制: 
    * Query strings 有長度限制 (因為整個 URL 長度有限制) 
    * 不適合傳 sensitive information 例如帳號密碼，因為太明顯了
    * 空白和特殊字元必須做逸出 encoded 
* URL Encoding
  * http://en.wikipedia.org/wiki/Percent-encoding
  * Space 變 %20
  * `!` 變 %21
  * `+` 變 %2B
  * `#` 變 %23
  * 其他還有 / ? : @ &
* 工具
 * Command Line Tools
   * curl
   * wget
    * https://github.com/jkbrzt/httpie  (brew install httpie)
 * 瀏覽器可使用 Browser Inspector 觀察和 Debug
   * Google Chrome
   * Firefox
 * 安裝 Browser Extension 可以測試 HTTP request 發送
  * Postman
  * REST Client

## HTTPS (TLS/SSL)

* 原理介紹 https://segmentfault.com/a/1190000004523659
* Cryptographic protocol called TLS https://cattail.me/tech/2015/11/30/how-https-works.html
* 如何弄 SSL 憑證
  * 產生 CSR request 憑證簽章要求
  * openssl req -new -newkey rsa:2048 -nodes -keyout server.key -out server.csr
    * 其中 Common Name 必須是你的 domain name，例如 exercise.ihower.tw。如果是 wildcard certificate 則用 *.ihower.tw
   * 這會產生兩個檔案 server.csr 和 server.key 
* 將 .csr 檔案丟給憑證機構做申請，最後會拿到 .crt key
  * 過程會需要認證你真的擁有這個 domain，通常會要求你設定一個特別的 CNAME
  * 也可以自己簽發，只是瀏覽器會警告
    * openssl x509 -in staging.csr -out staging.crt -req -signkey staging.key -days 365
 * 將 crt key 跟 server.key 設定到 HTTP Server
* 生活情境：移除 CNNIC 憑證
  * https://blog.longwin.com.tw/2010/02/remove-cnnic-ssl-ca-linux-2010/
  * http://kusowhu.net/mac-os-x-%E4%B8%8B%E5%88%A0%E9%99%A4cnnic%E8%AF%81%E4%B9%A6/

### HTTP/2

* HTTP/2 需要搭配 TLS/SSL 加密連線
  * 前身是 Google 的 SPDY
   * 語意 (Request/Response 格式) 和 HTTP/1.1 一樣沒有改
  * 改了底層連線實作，允許一個 TCP connection 可以同時傳輸多個 requests，大大加速效能
   * [你的網站升級到 HTTP/2 了嗎？](https://blog.alphacamp.co/2016/07/12/http2/)


## 瀏覽器的 Request/Response Lifecycle

以下出自 Coursera Startup Engineering 課程：

From HTTP Request to Rendered Page:

1. You begin by typing a URL into address bar in your preferred browser or clicking a link.
2. The browser parses the URL to find the protocol, host, port, and path (example).
3. If HTTP was specified, it forms a HTTP request.
4. To reach the host, it first needs to translate the human readable host into an IP address,and it does this by doing a DNS lookup on the host.
5. Then a socket needs to be opened from the user’s computer to that IP address, on the port specified (most often port 80 for HTTP).
6. When a network connection is open, the HTTP request is sent to the host. The details of this connection are specified in the 7-layer OSI model.
7. The host forwards the request to the server software (most often Apache/Nginx) configured to listen on the specified port.
8. The server inspects the request (most often only the path), and the subsequent behavior depends on the type of site.
• For static content:
– The HTTP response does not change as a function of the user, time of day, geographic location, or other parameters (such as HTTP Request headers).
– In this case a fast static web server like nginx can rapidly serve up the same HTML/CSS/JS and binary files (jpg, mp4, etc.) to each visitor.
– Academic webpages like http://startup.stanford.edu are good examples of static content: the experience is the same for each user and there is no login.
• For dynamic content:
– The HTTP response does change as a function of the user, time of day, geographical location, or the like.
– In this case you will usually forward dynamic requests from a web-server like nginx (or Apache) to a constantly running server-side daemon (like mod_wsgi hosting Django or node.js behind nginx), with the static requests intercepted and returned by nginx (or even before via caching layers).
– The server-side web framework you use (such as Python / Django, Ruby / Rails, or node.js / Express) gets access to the full request, and starts to prepare a HTTP response. A web framework is a collection of related libraries for working with HTTP responses and requests (and other things); for example, here’s the Express request and response APIs, which allow programmatic manipulation of requests/responses as Javascript objects.
– To construct the HTTP response a relational database is often accessed. You can think of a relational database as a set of tables similar to Excel tables, with links between rows (example database schema).
– While sometimes raw SQL is used to access the database, modern web frameworks allow engineers to access data via so-called Object-Relational Mappers (ORMs), such as sequelize.js (for node.js) or the Django ORM (for Python). The ORM provides a high-level way of manipulating data within your language after defining some models. (Example models / instances in sequelize.js).
– The specific data for the current HTTP request is often obtained via a database search using the ORM (example), based on parameters in the path (or data) of the request.
– The objects created via the ORM are then used to template an HTML page (server-side templating), to directly return JSON (for usage in APIs or clientside templating), or to otherwise populate the body of the HTTP Response. This body is then conceptually put in an envelope with HTTP Response headers as metadata labeling that envelope.
The web framework then returns the HTTP response back to the browser.
9. The browser receives the response. Assuming for now that the web framework used server-side templating and return HTML, this HTML is parsed. Importantly, the browser must be robust to broken or misformatted HTML.
10. A Document Object Model (DOM) tree is built out of the HTML. The DOM is a tree structure representation of a webpage. This is confusing at first as a webpage may look planar rather than hierarchical, but the key is to think of a webpage as composed of chapter headings, subsections, and subsubsections (due to HTML’s ancestry as a descendant of SGML, used for formatting books).
11. All browsers provide a standard programmatic Javascript API for interacting with the DOM, though today most engineers manipulate the DOM through the cross-browser JQuery library or higher-level frameworks like Backbone. Compare and contrast JQuery with the legacy APIs to see why.
12. New requests are made to the server for each new resource that is found in the HTML source (typically images, style sheets, and JavaScript files). Go back to step 3 and repeat for each resource.
13. CSS is parsed, and used to annotate each node in the DOM tree with style information on how it should render. CSS controls appearance.
14. Javascript is parsed and executed, and DOM nodes are moved and style information is updated accordingly. That is, Javascript controls behavior, and the Javascript executed on page load can be used to move nodes around or change appearance (by updating or setting CSS styles).
15. The browser renders the page on the screen according to the DOM tree and the final style information for each node.
16. You see the webpage and can interact with it by clicking on buttons or submitting forms. Every link you click or form you submit sends another HTTP request to a server, and the process repeats.

## 參考資料

* HTTP 協議入門 http://www.ruanyifeng.com/blog/2016/08/http.html
* 你應該知道的HTTP基礎知識 http://www.jianshu.com/p/e544b7a76dac
* Introduction to HTTP https://launchschool.com/books/http/read/introduction
* 圖解 HTTP
* Coursera Startup Engineering
