---
layout: default
permalink: networking-tcpip.html
title: "網路概論: TCP/IP 和 DNS"
---

# 網路概論: TCP/IP


* 目標讀者: 應用程式初學開發者，特別是 Application Developer
* 目的: 了解網路是如何運作的基礎知識
* 學校會教理論 [OSI 模型](http://zh.wikipedia.org/wiki/OSI%E6%A8%A1%E5%9E%8B)，這堂課使用比較實務的 RFC 1122 模型：
  * Application Layer 例如 HTTP、FTP、SSH 等
  * Transport Layer 例如 TCP、UDP
  * Internet Layer 例如 IP
  * Link Layer 例如 [Ethernet](https://zh.wikipedia.org/wiki/%E4%BB%A5%E5%A4%AA%E7%BD%91)、無線網路 802.11n
* 身為 Application Developer，我們主要在應用層 (Application Layer) 活動，最大宗就是熟悉 HTTP，但仍要基本了解底層是怎麼運作的

## TCP/IP 通訊協定

* 數位網路跟類比電話有什麼不一樣? 封包 Packet 的概念：[封包交換網路](https://zh.wikipedia.org/wiki/%E5%B0%81%E5%8C%85%E4%BA%A4%E6%8F%9B%E7%B6%B2%E8%B7%AF)、[封包](https://zh.wikipedia.org/wiki/%E7%B6%B2%E8%B7%AF%E5%B0%81%E5%8C%85)

![封包](http://linux.vbird.org/linux_server/0110network_basic//packet_total.png)
圖片出處 <http://linux.vbird.org/>

### IP 封包

* 一個IP封包的大小為46~1500bytes
* [IPv4 Address](http://en.wikipedia.org/wiki/IP_address) 用 4bytes 來表示一台電腦(設定在網路卡上)的網路位置
  * Internet/Public 和 Intranet/Private http://en.wikipedia.org/wiki/Private_network 有一些 IP addresses 區段被分配成內網專用
  * [CIDR 表示法](http://zh.wikipedia.org/wiki/%E6%97%A0%E7%B1%BB%E5%88%AB%E5%9F%9F%E9%97%B4%E8%B7%AF%E7%94%B1)：用來表示一整個區段的 IP 位置
  * [NAT](https://zh.wikipedia.org/wiki/%E7%BD%91%E7%BB%9C%E5%9C%B0%E5%9D%80%E8%BD%AC%E6%8D%A2) 的技術，讓我們有更多 IP 可以使用
* [IPv6 Address](https://zh.wikipedia.org/wiki/IPv6) 用 16bytes 來表示網路位置
  * [Apple 要求必須 IPv6 相容](http://shoshino21.logdown.com/posts/736331-send-apple-for-review-ipv6-support-specifically-should-be-in-line-with-what-conditions)
  * 要使用 IPv6，必須 client 端到 server 端中間的網路設備都要支援 IPv6，DNS 也需要設定 AAAA Record 表示 IPv6 位置。Hinet 預設是不支援的，需要另外申請。現代機房(Linode、AWS)則都有支援 IPv6。
  * [IPv6 來了](http://www.ithome.com.tw/article/92043) ???

### TCP/UDP  封包

* IP 封包有地址可以抵達對方電腦，但是一台電腦上有很多不同種類的應用程式，到底這個封包是要給哪一個程式去處理?
* [UDP和TCP封包](http://www.techbang.com/posts/15859-network-architecture-2-arpanet-history-and-introduction-to-mac-ip-dns-concepts-review?page=4)定義了 Port number 來源埠和目的埠。就像不同碼頭，編號從 0~65535，詳見 [TCP/UDP埠列表](https://zh.wikipedia.org/zh-tw/TCP/UDP%E7%AB%AF%E5%8F%A3%E5%88%97%E8%A1%A8)，一台電腦上不同的應用程式就會用不同的 Port。
  * 每一個需要用到網路的程式，都必須跟作業系統登記要一個 Port 來使用。如果你要編號 1024 以下的話，作業系統還會要求你有 root 權限。
* IP 封包並不會保證封包抵達的正確性，[TCP](https://zh.wikipedia.org/wiki/%E4%BC%A0%E8%BE%93%E6%8E%A7%E5%88%B6%E5%8D%8F%E8%AE%AE) 實作了更多步驟來保證資料傳輸的順序、重發遺失的封包、捨棄重複的封包、無錯誤資料傳輸、阻塞/流量控制、確認有建立三方交握，連線已建立才作傳輸等等。UDP 則無。
  * 為什麼 HTTP 使用 TCP，而 Real-Time 視訊串流通訊協定較多用 UDP?  例如 RTSP、RTP、H.323、SIP 等等
* [ICMP](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%81%94%E7%BD%91%E6%8E%A7%E5%88%B6%E6%B6%88%E6%81%AF%E5%8D%8F%E8%AE%AE)
  * ping 指令
  * traceroute 指令
* 網路工具
  * [Wireshark](https://zh.wikipedia.org/wiki/Wireshark)  網路封包擷取
  * ifconfig 指令可以查看網卡資訊

## 補充資料

* [網路架構大概論：歷史、規格、名詞一次搞懂](http://www.techbang.com/albums/107)
* [鳥哥的 Linux 私房菜: 基礎網路概念](http://linux.vbird.org/linux_server/0110network_basic.php)
* [我是一個網卡](http://gold.xitu.io/entry/5763cb427f578500546c91d4)
* [網路非常概論](http://www.slideshare.net/GuanHsiungLiaw/ss-52836041)
* [Khan: Internet 101 影片](https://www.khanacademy.org/computing/computer-science/internet-intro)