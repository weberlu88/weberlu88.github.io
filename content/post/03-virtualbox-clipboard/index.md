---
title: VirtualBox 無法共用剪貼簿的萬年老 Bug
description: 以 Kali linux 作為示範
date: 2021-09-14
slug: virtualbox-clipboard
# image: matt-le-SJSpo9hQf7s-unsplash.jpg
categories:
    - 教學
    - Linux
    - VM
---

Kail linux 官網提供了很詳細的[安裝教學文件](https://www.kali.org/docs/virtualization/install-virtualbox-guest-vm/)，我們可以從virtualbox 的設定中看到我們開啟了 Shared Clipboard 功能。倘若你實際上卻無法與 host 主機共用剪貼簿，那就恭喜跟我一樣碰到 virtualbox 的老問題了。

> 也有可能是 Kail linux ISO 的問題，因為我同台 host 也裝了 ubuntu、centOS 的 vm 卻沒有此狀況。

![開啟雙通道](img-setting1.png)
![有裝GuestAddition](img-setting2.png)

還沒解完...明天再戰