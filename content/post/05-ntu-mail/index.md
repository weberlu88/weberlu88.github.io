---
title: NTU Mail 綁定轉發/寄信功能到 Gmail 上
description: 問了N個人如何設定，沒想到是學校的教學手冊寫錯...
date: 2021-09-20
slug: ntu-mail-bind-google
image: 
draft: true
categories:
    - 教學
---


## 背景知識

- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie/SameSite
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie
- https://www.youtube.com/watch?v=GPz7onXjP_4

![](img-set-cookie.png)

## 實測結論

不行! 後端無法透過 request 取得 iframe 內嵌銀行網頁的 cookie。

下圖中可以看到兩個不同網域的 cookie，我們建在本機的釣魚網站是 https://127.0.0.1:5000，網路銀行的網站則是 https://www.digistarbank.com.tw (iframe)，因為還未登入所以只有兩個 cookie (language、sessionId)，他們在 firefox 瀏覽器的屬性為:
- samesite = None (在 chrome 中則是空白，因為銀行網站沒有主動設定所以連 none 都沒有)
- secure = false (同上)
- httpOnly = true (在 chrome 中同為 true)

## 發現和釋疑

- 我以為 cookie 中的 secure 屬性只要該網站是 https 就會被添加上去，事實上不是，需要特別由 set-cookie 設置。可參考背景知識中 set-cookie 的連結。
    - 疑點: 若第三方網頁允許第三方 cookie，Secure attribute 是要設置在第三方網頁上嗎?
    - 疑點: 若第三方網頁允許第三方 cookie，Samesite attribute 是要設置在第三方網頁上嗎?
- httpOnly 會禁止 JS 傳送和存取 cookie? 所以數位星辰銀行不論在前後端都無法 accesss 自己設置的 cookie?

## 其他成功取得第三方 cookie 的案例

要不要找個允許第三方cookie的網頁來實測一下第三方cookie到底是如何運作的? 引用現成的教學文也可。