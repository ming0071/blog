---
title: git 基本介紹 
date: 2023-07-29
description: 關於使用 git 的基本介紹，包含 add、commit、push、pull、colone，還有 ssh key 的基本說明。
path: blog/git
draft: false
taxonomies:
  categories: 
    - Coding
  tags: 
    - git
    - github
    - ssh key
---

github 大概是每個工程相關的人都會聽過的東西，但是應該也不少人不清楚它是在做什麼的，其實 git 和 github 是不同的東西 :<br>
- git 是版本控制的功能，就像遊戲可以儲存進度一樣，讓錯誤發生時就可以有回到上一步的機會。
- github 是在雲端上儲存 git repository 的地方，讓使用者可以在不同的設備間合作。

在 windows 要使用 git 需要另外安裝[windows git](https://git-scm.com/download/win)的，下圖中清楚地說明了 git 中常見的基礎指令是在做哪些事情的
<a href="/site/images/blog/git-flow.png" data-fancybox data-caption="git-flow">
  <img src="/site/images/blog/git-flow.png" loading="lazy" alt="git-flow" width="520"/>
</a><br>

以下是使用 git 和上傳 local repository (本地端檔案庫)到 github 的基礎教學。(以下將 repository 簡稱為 repo)

---

## 創建 repository

一開始先在 github 上創建一個新的 repo，創建過程中需要選擇選擇檔案庫是要 private 或 public。<br>
- private 可以不需要再設置 ssh key 就可以上傳
- public 則需要創建 ssh key 來對上傳者進行身分認證，避免公開的 remote repo 任何人都有權限上傳到 remote repo

## 創建 ssh key

一對 ssh key 可以分為 public key (公鑰)和private key (私鑰)，公鑰會放到網站上與私鑰配對使用，例如 github、netlify 等提供上傳服務的網站、伺服器，私鑰則要非常小心，不能夠外流出去，否則他人就有了權限存取、盜用你的資料。

創建一對 ssh key 的方法是右鍵打開選單點選「Open Git Bash here」，所有和 git 相關的指令都是在這裡進行，輸入指令`ssh-keygen`之後終端機上會出現 3 個問題 :
1. key 的路徑要放在哪裡 ?  使用預設路徑按 enter 即可
2. 要設定 passphase 嗎 ? 要的話當使用 ssh key 時就需要在另外輸入密碼，不要的話按 enter 即可
3. 再輸入一次 passphase，若上一步沒輸入按 enter 跳過即可
之後它就會生成一對 ssh key 出來了，螢幕上會出現 ssh key 放的路徑，舉例來說像是`c/users/ming/.ssh/id_rsa.`&`c/users/ming/.ssh/id_rsa.pub`，兩者對應的分別是私鑰及公鑰。

再來把公鑰放到 github 上，之後上傳前會進行匹配，成功就能夠上傳，依據作用的範圍方法有二 :
1. **放到 repository 專案** : 只作用在該專案內。「repository」→「settings」→「Deploy keys」→「Add deploy key」→輸入 title、key，並在 allow write access 打勾。
2. **放到 github 帳戶** : 所有的專案都會被作用。「個人頭像」→「settings」→「SSH and GPG key」→「New SSH key」→輸入 title、key，且選擇Authentication keys{{ ftnt_refs( idxs=[1]) }}。

設定完 ssh key 後就能夠上傳 local repo (本地端檔案庫)到 public 的 remote repo (遠端檔案庫)了。

## git 指令操作

### git init
在資料夾中建立一個 git repo 並初始化檔案庫，讓 git 對這個資料夾做版本控制，只需要執行一次即可，如果是用 colone 就會載入檔案庫，所以不用再執行 init。
```
$ git init
```

### git status
查看資料夾中檔案的已更新狀態，會以紅字表示有更動，綠字表示已加入 git 追蹤，當被 commit 後因為已經存檔就不會再顯示。
```
$ git status
```

### git add
把檔案加到 git 索引內，會因為後段的指令內容而有不同的作用。
```
// 加入單個檔案
$ git add 123.txt
// 加入當下資料夾內的所有檔案
$ git add .
```

### git commit
存檔，把 add 後的 git 狀態加入到 local repo 內。
```
// 會打開文字編輯器
$ git commit
// 不會打開文字編輯器並以 message 作為版本訊息說明
$ git commit -m "message"
```

### git log
查看 commit 的歷程記錄，以時間軸倒序而由上到下排列。
```
$ git log
```

### git branch

```
git branch -M main
```

### git remote
把 github 內的 repo 與 local repo 連結，以 SSH 的方式上傳，裡面的 url 會是`git@github.com:你的帳戶名字/專案名字.git`的形式。
```
// 創建名為 origin 的遠端檔案庫 
$ git remote add origin url
```

### git push
把 local repo 推上 remote repo 
```
// 推上名為 origin 的 remote repo main 分支
$ git push -u origin main
```

### git pull
把 github 上的檔案抓下來到 local 端更新紀錄，所以 push 的時候當 github 上的內容比 local 端的還要新的話，就會跳出錯誤提示避免把內容給覆蓋掉，這時候就先 pull 再 push 就沒問題了。
```
$ git pull
```

### git colone
複製 github 上的專案下來使用，會把 git 紀錄、分支都一起下載下來。
```
$ git colone url
```

## 常用指令

直接使用這一段指令對資料夾內的已更新檔案上傳到 github 上。
```
$ git add .
$ git commit -m "message"
$ git push -u origin main
```

以上是常用的 git 基礎指令介紹，後續的分支可能就另外再搞一篇吧。

## 註腳

{% ftnt( idx = 1 ) %}
[兩個鑰匙之間的差異](https://stackoverflow.com/questions/73673920/do-i-need-authentication-as-well-as-signing-keys-on-github)
Authentication keys 是用於驗證 GitHub 上特定帳戶的憑證，當作 git 指令操作時可以證明是帳戶的擁有者。
Signing keys 是用於證明操作是由本人進行操作的。
{% end %}

---

## 參考

- [【GIT 小教室】SSH Key 的建立與設定](https://www.youtube.com/watch?v=CeC_qyQHiCE)
- [【git教學 #1】15分鐘學會git & github（附實例）](https://www.youtube.com/watch?v=Zd5jSDRjWfA)
- [【Day10】Git 版本控制 - 將檔案 push 到 GitHub 的懶人包](https://ithelp.ithome.com.tw/articles/10271811)
- [30 天精通 Git 版本控管 (01)：認識 Git 版本控管](https://ithelp.ithome.com.tw/articles/10132053)