---
title: Changelog
description: 這邊是部落格的 Changelog，描述「Ming's Blog」的版本更新過程，包含新增、調整、或刪除的內容。
path: changelog/
draft: false
template: changelog.html
---

這裡是「Ming's Blog」的版本更新過程，包含新增、調整、或刪除，每當網站有什麼變化就會在這裡留下紀錄。

以下是版本號定義：
- 主版號：表示部落格有了大幅度的改版，目前規劃當網站上線後即為 1.0.0；而當把網站建立出我的個人風格後即為 2.0.0。
- 次版號：表示部落格有新增功能發布，即在網站既有的框架下新增了新的設定，讓網站獲得了成長。
- 修訂號：表示部落格既有功能有更動刪改，例如 CSS 樣式的調整、文章分類的調整等。

以下是依時間倒序排列的 changelogs ，歡迎瀏覽！

---

## Ver. 1.0.0   <span class = "muted flex-right">23.07.24</span>

#### Changed

- 網站部屬上架。

#### Removed

- 從 [pagespeed](https://pagespeed.web.dev/analysis/https-ming-blog-netlify-app/jhem5eqkwf?form_factor=mobile) 測試效能後發現行動裝置端的跑分只有61，發現是引用了 google font 的問題，把它移除之後就拉到91分了，目前效能分數行動裝置91分、電腦92分，還算不錯的分數。

---
## Ver. 0.1.0   <span class = "muted flex-right">23.07.18</span>

#### Added

- 叫回了 Changelog 這個頁面，並調整了時間標示的 CSS 

#### Removed

- 隱藏了當 sidebar 過長時產生的滾動條。

---

## Ver. 0.0.1  <span class = "muted flex-right">23.07.17</span>

#### Changed

- 調整了網站的主題顏色、icon 設計，雖然還是跟「Pin 起來」99% 像 XD
- 調整了預設字體設定，將英文字體預設為"Arial"；中文字體預設為"微軟正黑體"。