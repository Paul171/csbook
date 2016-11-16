---
layout: default
permalink: cli.html
title: 命令列 Command Line Interface
---

# 命令列 CLI

* Command Line Interface (CLI) 和 Graphical user interface (GUI) 有什麼差別? 為什麼 geeks 們要用 CLI ?
* Mac 和 Linux 都是 [UNIX-like](https://zh.wikipedia.org/wiki/%E7%B1%BBUnix%E7%B3%BB%E7%BB%9F) 作業系統，這也是為什麼 Web Developer 愛用 Mac 的原因，因為作業系統架構和 CLI 指令跟 Linux 伺服器類似，因此可以跑在 Linux 上的開源軟體(特別是 Web 後端用到的軟體，例如各種資料庫、網站伺服器、Ruby/Python/PHP 程式語言等等) 也都支援 Mac，反而 Windows 支援比較差。
* [Unix 哲學](https://zh.wikipedia.org/wiki/Unix%E5%93%B2%E5%AD%A6): Do One Thing Well：指令只做一件事，但可以透過串接來達成複雜的操作

![history](http://www.oliverelliott.org/static/article/img/Unix_timeline_800.png)

* 名詞釋疑: Terminal, Console 和 Shell
  * Terminal 是指 CLI 的輸入輸出介面程式，例如 mac 內建的 Terminal，或是另外裝的 iTerm2。使用 Terminal 時會需要設定要用哪一種 Shell。
  * Shell 是指和電腦溝通的指令，有分很多種，Unix 上常見使用 Bash Shell、Windows 則是用 PowerShell。Shell 可以只當作是 Shell command 用，但也可以當作 Shell script 使用，就像程式語言一樣。
  * Console 指某特定的指令語言環境，例如 mysql console (輸入 SQL 指令)、irb console (輸入 Ruby 程式)、rails console (輸入 rails 程式)

## Terminal 視窗

* Tab Completion 自動完成
* iTerm 快速鍵秘訣
  * [iTerm - 讓你的命令行也能豐富多彩](http://www.swiftcafe.io/2015/07/25/iterm/index.html)
  * [An Apple Hotkey a day](http://taian.su/2012-10-11-an-apple-hotkey-a-day/)
* Control+c 取消目前指令
* Control+z 中斷目前指令
* Control+a and Control-e 跳到指令最前、最後
* Control+l 清除畫面 (或用 `clear` 指令)

## 一些 Mac/Linux 通用指令

* `date`
* `uname -a`
* `hostname`
* `history`
* `bash --version`
* `uptime` 查電腦開機多久了
* `man` 查指令的文件
  * 按 q 可以離開
* `which` 查詢執行檔的確切位置

## 檔案目錄結構和操作

* 分成檔案 file 和目錄 directory
* 檔名不能有 `/`
* 檔名之中如果有空白 `!$#()[]%&;` 等特殊字元，用的使用需要加上 'quotes' 或用 `\`進行脫逸
* 用 `/` 切隔目錄名，不同於 windows 用 `\`，例如 `C:\`
* 用 `*` 表示萬用字元、用 `?` 表示單一萬用字元、，例如 ls *.png
* absolute path 和 relative path，後者相對於 working directory
  * `.` 表示 current working directory
  * `..` 表示上一層
  * `~` 表示你的 home directory
* The Filesystem Tree
  * `/`  root directory
  * 家目錄：Mac 上是 `/Users/your_username`、Linux 上是 `/home/your_username`
  * `/usr/local` 放自行安裝的系統軟體的目錄
  * `/usr/local/bin` 放上述執行檔的地方
  * `/etc/` 系統設定檔
  * `/var/` 系統 Log
  * `/tmp` 暫存檔案
  * `~/Desktop` Mac 的桌面
  * `~/Download` Mac 的下載目錄
* 檔案不一定需要附檔名，例如 README、LICENSE 等等檔案
* `.` 開頭的檔案，指的是隱藏檔，輸入 `ls` 時不會顯示出來，需要用 `ls -a`
* pwd 顯示目前所在的 working directory
* cd 變更目前的 working directory
  * `cd ..`
  * `cd ~`
  * `cd /`
* `ls` 和 `ls -la`
  * l 代表顯示更多資訊、a 代表顯示隱藏檔
* `cat` 顯示檔案全部內容
* `tail` 顯示檔案最後面的內容
 * `tail -n 500 filename`  最後500行
 * `tail -f filename` 掛著顯示，可用來一直觀察 log
* `mv` 移動或改名
* `cp` 複製
* `mkdir` 新增目錄
* `rmdir` 刪除空目錄
* `rm` 刪除檔案
  * `rm -rf` 強制刪除整個目錄
* `touch` 新增一個空檔案
* `df -h` 檢查硬碟空間
* `grep` 比對檔案內容
 * `tar` 和 `gzip` 打包目錄和解壓縮

> 竟然有人真的[實驗看看 rm -fr /](https://www.youtube.com/watch?v=KIyCYtu3pp0) 會怎麼樣，原來下場這樣...... 是蠻慘的

### Links

* `ln -s` 連結檔案，例如 `ln -s original_file_name link_name`

## 檔案編輯器

* nano
* vi 或 vim

## 使用者權限和檔案權限

* 每個檔案和目錄可以設定屬於哪一個用戶、哪一個群組
* 每個檔案和目錄都有權限設定：(你自己, 群組, 全部使用者) x (讀取, 寫入, 可執行) 共有九碼
* [檔案目錄權限](http://tnrc.ncku.edu.tw/course/93/fedora_core2/page10/p10.htm)
  * Read(可讀)  r 4
   * Read,Write,eXcute  rwx 4+2+1=7
   * Read,eXcute  r-x 4+1=5
   * Read,Write rw  4+2=6
* `chmod` 可以變更 mod
* `chown` 可以變更使用者和群組
* root 和 `sudo` 指令
  * `visudo` 用來編輯誰有 sudo 權限
* `su` 切換使用者

## Process 管理

如同 Mac 上的 Activity Monitor

* `top`
* `ps ax`
* `kill -9`

## 組合技

* standard input (stdin)
* standard output (stdout)
* `;` 可以分隔指令組成一行執行
* `>` Redirection 可以變成 output，例如 `echo "Hello World!" > test.txt` 就把輸入寫到檔案了
* `>>` 可以 append 到檔案後面，例如 `echo "Hello World!" >> test.txt`
* `|`   Pipe 一個 UNIX 指令的輸出，可以是另一個 UNIX 指令的輸入，例如 `cat test.txt | more` 、`ps ax | grep "ruby"`
* `sort` 和 `uniq`

## 網路操作指令

* [如何用Linux命令行管理網絡：11個你必須知道的命令](https://github.com/oldratlee/translations/blob/master/how-to-work-with-network-from-linux-terminal/README.md)
* ping
* traceroute
* dig
* wget (for file)
* curl
 * ssh
   * .ssh/config
* scp

## 環境變數與 Login Script

* [The Rubyist's Guide to Environment ](http://blog.honeybadger.io/ruby-guide-environment-variables/)
* [Understanding *NIX Login Scripts](http://www.sitepoint.com/understanding-nix-login-scripts/)
* 認識  .bash_profile
   * PS1
   * git

## Mac only

* [Eight Terminal Utilities Every OS X Command Line User Should Know](http://www.mitchchn.me/2014/os-x-terminal/)
* [Use your OS X terminal shell to do awesome things](https://github.com/herrbischoff/awesome-osx-command-line)
* `open .` 用 Finder 打開當前目錄
* `open` 檔名，加上 `-a` 參數可以指定用什麼程式打開，例如 `open -a Safari index.html`
* pbcopy 和 pbpaste
* command+tab
* command+w
* command+q
* homebrew 有更多 CLI 工具
  * `brew install youtube-dl`

## 補充資料

* [Unix/Linux 命令参考 ](http://i.linuxtoy.org/files/pdf/fwunixref.pdf)
* [The Command Line Crash Course](http://cli.learncodethehardway.org/book/)
* [INTRODUCTION TO THE COMMAND LINE](https://launchschool.com/books/command_line/read/introduction)
* [Learn the Command Line](https://www.codecademy.com/courses/learn-the-command-line)
* [Treehouse: Console Foundation](https://teamtreehouse.com/library/console-foundations)
* [An Introduction to Unix](http://www.oliverelliott.org/article/computing/tut_unix/)
* [edx: Introduction to Linux](https://www.edx.org/course/introduction-linux-linuxfoundationx-lfs101x-2)
* [The Linux Command Line 簡中版](http://billie66.github.io/TLCL/)
* [Master the command line, in one page](https://github.com/jlevy/the-art-of-command-line)