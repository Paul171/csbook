---
layout: default
permalink: web-design.html
title: 程式設計基礎
---

# 網頁設計

* 參考資料
  * <http://www.theodinproject.com/web-development-101>
  * <http://www.theodinproject.com/introduction-to-web-development>
  
## HTML/CSS
		
* HTML
 * 了解 HTML/CSS/JavaScript 在網頁中的角色
 * 學會使用正確的結構化標籤
 * HTML4 
   * a, br, div, em, strong, h1, h2, h3, img, table...etc
 * HTML5 structural tags
   * section, article, main...etc
 * HTML Form 標籤
   * 各式 input, submit...etc
   * http://nativeformelements.com/
 * 認識 SEO
* CSS
 * 為何分離 HTML and CSS?
 * 各種 selectors, properties, values
 * CSS 權重
 * CSS Selectors
 * CSS Box Model
 * CSS Layout
   * float
   * position: static, absolution, relative, fixed...etc
   * flexbox 
* 使用 Chrome DevTools 觀察除錯
* 部署至 Github Page
* 參考教材內容
  * http://marksheet.io/
  * http://howtocodeinhtml.com/
  * http://learn.shayhowe.com/html-css/ 入門 HTML/CSS
    * http://zh-tw.learnlayout.com/ 參考
  * http://www.htmldog.com/guides/html/beginner/  入門 HTML
  * http://www.htmldog.com/guides/html/intermediate/ 
  * http://www.htmldog.com/guides/html/advanced/
  * http://www.htmldog.com/guides/css/beginner/ 入門 CSS
  * http://www.htmldog.com/guides/css/intermediate/
* 作業
  * 練習 http://www.codecademy.com/en/skills/make-a-website
  * 練習 http://www.codecademy.com/en/tracks/web
  * 看完 Treehouse: HTML Form
  * 練習 Udacity: Intro to HTML/CSS: Final project (用 bootstrap 拆 mockup 的練習)
  * A HTML/CSS project at github page
    * build google.com ? http://www.theodinproject.com/web-development-101/html-css
    * 加強表單 Form 的練習 (參考 http://howtocodeinhtml.com/ )

## RWD 和 Bootstrap
 
* 介紹使用 [Bootstrap](http://getbootstrap.com/)
* RWD 設計和 Media Query
* CSS3 http://www.htmldog.com/guides/css/advanced/ 
  * 如何套用現成的 Bootstrap Theme，例如 http://bootswatch.com/
    * http://code.divshot.com/themestrap/
    * http://startbootstrap.com/template-overviews/clean-blog/
    * http://www.bootstrapstage.com/sb-admin/

## jQuery

* 什麼是 DOM?
* http://www.codecademy.com/en/tracks/jquery
* http://try.jquery.com/     
 * 線上練習環境
   * http://jsbin.com/ 或 https://jsfiddle.net/
 * jQuery
   * 官網文件 http://api.jquery.com/
   * 版本1.x 2.x 的差異
   * 用途
     * 定位 selectors & Traverse
     * 修改 DOM manipulation
     * 綁事件 Event
     * 動畫 animate
     * API 串接 Ajax
 * Selector
   * by tag
   * by class
   * by id
   * by attribute https://api.jquery.com/category/selectors/attribute-selectors/
   * Filter https://api.jquery.com/category/selectors/basic-filter-selectors/
 * Traverse 常用於從 $(this) 出發去找目標
   * parents
   * parent
   * closest
   * first
   * last
   * prev
   * next
   * find 找下多層
   * children 只找下一層而已
   * filter
 * DOM manipulation
   * 插入
     * append
     * prepend
     * after
     * before
     * appendTo
     * prependTo
     * insertAfter
     * insertBefore
   * remove
   * attr 
     * 例如超連結的 attr("href")
   * text
   * html
   * val  
     * 針對 input, select and textarea 的 value 資料
   * css
   * toggleClass
     * addClass
     * removeClass
   * toggle
     * show
     * hide
   * slideToggle
     * slideDown
     * slideUp
   * fadeToggle
     * fadeIn
     * fadeOut
   * animate
 * Event
   * ready
   * on
     * Direct event v.s. Delegated event
     * http://jsbin.com/tinopojeni/1/edit?html,js,output
   * click
   * trigger 指定事件
   * Mouse events: click, focusin, mousedown, mousemove, mouseover, mouseenter, dbclock, focusout, mouseup
   * Keyboard Events:  keypress, keydown, keyup
   * Form events: blur, select, change, focus, submit
   *  bubble up 特性
     * 如何阻止超連結 # 作用? event.preventDefault()
     * 停止往上傳遞事件 event.stopPropagation()

### 參考資料

 * Udacity: JavaScript Basic
 * Udacity: Intro to jQuery
 * CodeSchool: Try jQuery

### Example Code:

* https://github.com/ihower/rails-exercise-ac5/blob/master/app/views/welcome/jquery.html.erb (ac5) 
* https://github.com/ihower/rails-exercise-ac6/blob/master/app/views/welcome/jquery.html.erb (ac6) 
* https://github.com/ihower/rails-exercise-ac7/blob/master/app/views/welcome/jquery.html.erb (ac7)
     
     
## jQuery Ajax

* Ajax = JavaScript 送 Request，然後處理 response，過程中瀏覽器不會跳一整頁。
* facebook and twitter timeline example: it's JSON including HTML
* append 第三方圖片，用 img src (但這不算是 ajax)
* Debugging with Chrome DevTools


### jQuery 的 Ajax 用法

官方文件 http://api.jquery.com/category/ajax/

* jQuery $.ajax
 
       $.ajax( <url>, { success: function(res) {  $(<selector>).html(res) } } )
       $.get(<url>, function(res) { ... })
       $.ajax( <url>, { data: { foobar: 1 },  success: function(res) {  $(<selector>).html(res) } } )
* Ajax Error handling (e.g. timeout)

       $ajax(<url>, { success: function(res){ ... }, error: function(request, error_type, error_message) { ... } } )
       $ajax(<url>, { success: function(res){ ... }, error: function(request, error_type, error_message) { ... } , timeout: 3000 } )

* Add ajax loading status? 
  * beforeSend 
   * complete
 * 小心動態插入的 element 會沒有綁到 event。要使用  Delegated Event
 * Ajax Form

       $('form').on("submit", function(e) { 
          e.preventDefault();
          $.ajax( <url>, { type: 'POST', data: { "foo":  $("#foo").val() }    }); 
   * 其中 `data: $('form').serialize() `
     * https://api.jquery.com/serialize/
   * 注意: 無法處理檔案上傳
   * 再補上 success callback 把 form 移掉等等
 * JSON Response
   * $.ajax 加上 
     * dataType: 'json' 代表 parse the response as JSON
     * contentType: 'application/json' 跟 server 說要 JSON 格式
     * success callback 的 response 變成 json object 了
     * codeschool 這裡手動組 HTML
     * ajax url 可以換成 $('form').attr('action') 
   * $.getJSON(url, function(data){ ... } )
   * $.getJSON(url, function(data){ ... } ).error(function(e){...} )


關於 jQuery Ajax，推薦以下兩個教材：

 * Udacity: Intro to Ajax
 * codeSchool: jQuery The Return Flight


     