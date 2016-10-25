---
layout: default
permalink: networking-others.html
title: "網路概論: 其他"
---

# 網路概論: 其他

### Telnet

* 最基本的未加密通訊協定，已不常見用來登入伺服器
* BBS 仍在使用：`telnet ptt.cc`
  * 在 PTT 也支援 SSH，可用 `ssh bbs@ptt.cc` 登入
* 也可以用 Telnet 操作 HTTP 和 FTP 等無加密純文字的通訊協定

### 密碼學術語入門

* 編碼 encode 和 decode，例如 [Base64](https://zh.wikipedia.org/wiki/Base64)。泛指用某種方式將文件轉成另一種格式，通常是為了某種相容性，並沒有加密效果。
* 加密 Encryption
  * [對稱式加密](https://zh.wikipedia.org/wiki/%E5%B0%8D%E7%A8%B1%E5%AF%86%E9%91%B0%E5%8A%A0%E5%AF%86)，例如 DES
  * [非對稱式加密或公開金鑰加密](https://zh.wikipedia.org/wiki/%E5%85%AC%E5%BC%80%E5%AF%86%E9%92%A5%E5%8A%A0%E5%AF%86)，例如著名的 RSA
* 簽章和雜湊函式(hash)
  * 早期用 md5
  * 現在用 [SHA](https://zh.wikipedia.org/wiki/SHA%E5%AE%B6%E6%97%8F)


### SSH 和 SFTP

* 預設用 port 22
* 指令
  * ssh
  * scp
* 加密的安全通訊協定
* 產生你的非對稱 Public/Private Key Pair
  *    ssh-keygen -t rsa -C "your_email@youremail.com"
  *    cat ~/.ssh/id_rsa.pub
    
### 其他應用層通訊協定

* SMTP
* VPN 
* FTP 
* BitTorrent 

### Others 主題

* Firewall
* Denial of Service (DoS) Attacks
* DDoS
* CDN 
  * https://www.cloudflare.com/ 免費的 CDN
  * https://aws.amazon.com/tw/cloudfront/ 最方便一般人租用的提供商
  * https://www.akamai.com/ 全世界最大的 CDN 服務提供商

### 3-rd Party Hosting Provider

IaaS、PaaS、BaaS、SaaS 不同層級的網路服務

* Cloud
  * AWS
  * Azure
  * Google Cloud
* VPS ( Virtual Private Server )
  * linode.com
  * digitalocean.com
* PaaS
  * Heroku
  * Google App Engine
* BaaS
  * Parse
  * Firebase