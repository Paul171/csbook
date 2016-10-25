---
layout: default
permalink: networking-dns.html
title: "網路概論: DNS"
---

# 網路概論: DNS

* [DNS 網域名稱系統](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D%E7%B3%BB%E7%BB%9F)：用來處理 Domain Name 和 IP 地址的轉換
* 本機可用 Domain Name 和 IP 對應檔案 /etc/hosts
* 但是本機不可能預先存好全世界的對照表，我們需要基於分散式的 DNS 通訊協定
  * Domain Name 組成:  sub-domain.your-domain(.second-level-domain).top-level-domain
  * https://en.wikipedia.org/wiki/Domain_name
  * http://www.iana.org/domains/root/db
* 用戶通常使用 ISP 的 DNS，例如中華電信 168.95.1.1，或自己改成 Google 的 8.8.8.8
  * Resolver -> DNS -> 如果找不到，該 DNS 會從 root nameserver 往下 query，直到找到負責該 zone 的 server
  * 第一次查詢後，就會快取起來，可以設定 TTL 時間
* 查詢流程：[root nameserver](https://zh.wikipedia.org/wiki/%E6%A0%B9%E7%B6%B2%E5%9F%9F%E5%90%8D%E7%A8%B1%E4%BC%BA%E6%9C%8D%E5%99%A8) -> .org/.com/.tw nameserver -> your domain nameserver
* How to register your domain?
  * https://www.namecheap.com
  * http://godaddy.com/
  * [TWNIC](http://www.twnic.net.tw/)
  * 有很多域名營運商。注意，域名營運商、DNS 和 Hosting Provider 是分開的。
* 生活情境
  * 誰註冊了這個 Domain Name: Whois
  * 標售哄抬現象 http://www.inside.com.tw/2011/04/07/domain-name-front-runnng
  * 網路好像故障了，瀏覽器無法連線，但是可以 ping ip address 這是什麼情況? 可能是中華電信的 DNS 壞了。
  * 牆內的 DNS 污染
  * 釣魚網站: 利用網址很像、畫面弄成一樣騙你輸入帳號密碼
  * Domain 忘記續約：[TP Link](http://thehackernews.com/2016/07/tp-link-router-setting.html)、[Sony](http://eq2wire.com/2014/07/15/sonyonline-net-domain-expires-shenanigans-ensue-for-all-soe-games-websites/)
* DNS 設定
  * A record, CNAME, MX record...etc 等
  * PTR 反解: 不過通常懶的設定
* DNS 3-party service
  * AWS S53
  * http://dyn.com/
  * 有很多
* CLI 工具
  * whois
  * nslookup
  * dig
    * dig alphacamp.co
    * dig -t mx alphacamp.co
    * dig @a.root-servers.net. alphacamp.co
    * dig @ns1.cctld.co alphacamp.co
    * dig @DEE.NS.CLOUDFLARE.COM alphacamp.co
  * Authoritative answer/ AUTHORITY 表示這個答案是從負責該網域的主機回傳的

## 購買 Domain Name 和設定 DNS

* 推薦在 NameCheap 買網域，請點這個 referral URL 註冊:  https://www.namecheap.com/?aff=91800 讓 ALPHACamp Dojo 賺 15% 傭金
* 假設購買 example.com，可以讓 1. Nameserver 代管 DNS，或改用 2. Linode 的 DNS：
* 讓 NameCheap 代管 DNS：
  * Advanced DNS -> Domain Nameserver Type 選 Namecheap Default
  * Advanced DNS -> Host Records -> Manage -> ADD RECORDS
    * 新增 A Record，設定 host 是 @ 指向你的 server ip (這表示 example.com )
    * 新增 A Record，設定 host 是 www 指向你的 server ip (這表示 www. example.com 

## 補充資料

* DNS 原理入门 http://www.ruanyifeng.com/blog/2016/06/dns.html
* Learning DNS http://shop.oreilly.com/product/0636920040088.do
