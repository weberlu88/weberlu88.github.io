---
title: Hugo tutorial
description: 用 markdown 寫靜態網頁的超懶人工具
date: 2021-09-13
slug: hugo-tutorial
image: img-hugo-logo.png
categories:
    - 教學
---

> 這篇文章將會教你如何用 hugo 的模板建立靜態網站，並且部屬到 github page 上作為你的個人網站。  

## Hugo 是什麼

*"Hugo is a fast and modern static site generator written in Go, and designed to make website creation fun again."*  by [官網](https://gohugo.io/about/what-is-hugo/)

**優點**:
1. 懶人 - Hugo 是一個靜態網頁生成器，使用者不需要對 html、css、js 進行任何操作，不怕套了精美的模板卻改不動。
1. 簡潔 - 使用markdown格式撰寫文章，資源讀取簡單，而且開發時可以 life-reload 頁面。
1. 漂亮 - 有各式各樣的模板供你選擇。

**實用連結**:
- [Hugo - Static Site Generator | Tutorial](https://www.youtube.com/playlist?list=PLLAZ4kZ9dFpOnyRlyS-liKL5ReHDcj4G3)
- [Hugo手把手安裝教學](https://www.demo.off-record.net/21/1/install-hugo/)
- [Hugo 主题 Stack](https://blog.jimmycai.com/p/hugo-theme-stack/)

## Hugo 開發環境安裝 

官網教學:point_right: https://gohugo.io/getting-started/installing/。 

要使用 hugo 來開發不需要安裝 go 只需要安裝 hugo 即可，在 windows 環境下需要用 scoop、choco 在 cmd 中安裝；如果沒有這兩個套件管理工具或不想打指令，也可以從官方 [github release](https://github.com/gohugoio/hugo/releases) 下載 zip 檔，有些模板會用到 extended 版，最後記得將 hugo.exe 的 bin 目錄添加到環境變數中。詳細操作可以參考上方實用連結的YT頻道。

## 建立你的網站

Hugo 使用 CLI(command line interface) 進行網站的本地部屬和打包等功能，常見的指令有
- **hugo new site** <**directory-name**>: 在指定目錄建立新的專案。
- **hugo server**: 在本機(localhost)部屬網站，可以 hot-update 讓你一邊編輯一邊查看成果。
- **hugo**: 根據目錄中的 `config` file 打包(build)專案，打包好的專案會寫入 `/docs` 目錄，記得每次打包前要先刪除舊的 `/docs` 唷，因為這個指令只會覆寫檔案，如果你刪除了一個頁面 hugo 不會幫你在 `/docs` 中刪除他。

每個指令都可以帶相關參數，有關更多指令和參數可參考官網<span class="emojify">:point_right:</p> https://gohugo.io/commands/。

建議使用 VScode、Autm、Sublime 等程式編輯器來開啟專案，這類 ide 都有內建終端機好讓你下 CLI 指令。

### 套用模板

Hugo 的社群提供了各式各樣的模板<span class="emojify">:point_right:</p> https://themes.gohugo.io/。  
Hugo 模板允許大量的客製化，網站的樣式、架構、config 配置取決於模板的設計。挑模板除了考慮美觀，也建議挑個有操作手冊的以便日後的更改和維護。  

比如說這個網站的模板 [hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack) 就有附上 github repo 和中英文文檔，我在更改左右側選單、自訂義css上方便許多。

### 編輯

在 hugo 專案上編輯網頁內容時再簡單不過了，hugo 使用 markdown 文件來記錄網站內容，文章內容放在 `/content` 目錄中，假如說我今天要建立一個新的頁面，則可在 `/content/post` 中新增一個資料夾，檔案格式為:
{{< highlight text >}}
/02-hugo-tutorial  (頁面資料夾)
  |-- index.md     (文章內容)
  |-- img-01.png   (index.md 引用的本地資源)
  |-- img-02.png   (index.md 引用的本地資源)
{{< /highlight >}}

## Github Page 創建及部屬

> 官方文件 <span class="emojify">:point_right:</p> https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages

Github 為使用者提供了靜態網站的 hosting service，分成 project site, user site 和 organization site 幾種網頁，每個 repository 可以建一個 project site，每個帳號可以 host 一個 user site。

- user site 的 repo 名稱要取的跟你的username相同，也是你的網域名稱(domain): `<username>.github.io`。
- user site 的網站連結: `http(s)://<username>.github.io`。

建立好對應的 github repo 後再至 *setting > pages* 開啟網站。這個頁面可以選擇要從 repo 的哪個分支/哪個資料夾部屬網站。

- **預設 main branch**: 就是以前的 master。
- **root folder**: 部屬整個 repo。repo 須放 hugo 專案的 `public` 資料夾。這種配置可將 source code 和 deployed site 獨立分開來，兩個各一個 repo。
- **docs folder**: 部屬 repo 中的 `/docs`。懶人方法是把整個 hugo 專案放在 repo 中，每次 build 好時把 `/public` 改名就可以 commit 了。

最後，我們要修改 hugo 專案的 config 檔，指定專案的網址為 `baseurl: https://<username>.github.io/`，不然無法載入 js、css、img 等資源喔。

{{< css.inline >}}
<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
</style>
{{< /css.inline >}}