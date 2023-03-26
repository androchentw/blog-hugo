---
title: "來點 SRE - 從 ChatGPT 停機公告，學維運事後剖析"
url: /chatgpt-sre-postmortem
# date: 2023-03-25T06:00:00+08:00
date: 2023-03-25T08:25:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - sre
  - chatgpt
  - aigc
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/tech/sre/2023-03-25-chatgpt-sre-postmortem-cover.png?raw=true
series: sre
---

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/sre/2023-03-25-chatgpt-sre-postmortem-cover.png?raw=true">
<p align="center"><sub><sup>
  來點 SRE - 從 ChatGPT 停機公告，學維運事後剖析
</sup></sub></p>

## Overview 概述

ChatGPT 在美國時間 3/24(週五) 發布了新的一篇 blog，解釋 3/20(週一) ChatGPT 停機的來龍去脈。

每一次的緊急維修，對於系統維運 SRE 來說都是意義非凡。因為這代表你的服務

1. 重要到用戶會關注
2. 必要到每分每秒都在產生價值 (不修復會造成損失)

對於很多企業來說，停機好像是永遠不該發生的事。多半是偷偷改掉不讓用戶發現就過了，怎麼可能大張旗鼓地還發部落格？

從這點就可以看出決定性的差異。

🔎 **透明度，及其帶來的信任是關鍵**。「我們正在修，出於什麼原因-人事時地物，之後能怎麼避免」。好用，相信你能夠盡快修復的信任感 (Trust)，奠基於系統服務的穩定 (Reliability)

❓ 提問: 你的團隊在意這些服務體驗嗎？ 一起來看 OpenAI 怎麼示範 SRE 中的 Postmortem (事後剖析)。

<!--more-->

## 什麼是 SRE 網站可靠性工程

SRE (網站可靠性工程, Site Reliability Engineering) 是 Google 早在十年前就提出並且應用的一種[維運管理方法論](https://blog.cloud-ace.tw/application-modernization/devops/about-sre/):

> SRE is what happens when you ask a software engineer to design an operations function. -- Benjamin Treynor Sloss (Vice President, Engineering, Google)
>
> SRE 就是當你去問一個軟體工程師如何設計一套維運方法的表現。

[Google 有兩本 SRE 的免費電子書](https://blog.androchen.tw/google-sre-books)，非常推薦維運工程師好好研究。

OpenAI 不是第一個這麼做的單位，事實上這已經是西方主流企業的顯學之一。

## ChatGPT 3/20 停機剖析

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/sre/2023-03-25-chatgpt-sre-postmortem-post.png?raw=true">
<p align="center"><sub><sup>
  ChatGPT 在美國時間 3/24(週五) 發布了新的一篇 blog，解釋 3/20(週一) ChatGPT 停機的來龍去脈。
</sup></sub></p>

### Situation Analysis 狀況說明

3/20(週一) ChatGPT 存在開源庫 redis-py 快取的漏洞，導致

1. 部分用戶會看到別人的**聊天標題**
2. 少了幾個小時的歷史訊息
3. 在某 9 小時裡，1.2% 的活躍用戶中，ChatGPT Plus 訂閱者的**付款相關資訊**被意外洩露
4. 包含: 名字、email、付款地址、信用卡號碼**末四碼**及信用卡到期日。完整的信用卡號碼並未曝光。

發現狀況當下 OpenAI 立刻停機進行調查與修復，包括如何復現此狀況，並聯繫受影響的使用者。

### Tech Details 技術細節

簡單來說是 ChatGPT 採用的 Redis Cluster 的 Asyncio redis-py 客戶端，在異常處理時會導致**連線返回錯誤資料**。

Redis 是一個 Cache 快取機制，在後端資料庫 (DB, Database) 跟用戶中間，讓你不用一直去跟 DB 拿資料，這樣 DB 就不會太忙，用戶的存取速度也會大幅提昇。在這個例子中，理應該被拒絕的 request，卻**意外發給了不對的用戶**。如今已透過開源社群的快速 patch 修復。

### Actions 採取措施

OpenAI 也條列了他們已經採取的措施:

1. 大量**測試**，以確保修復。
2. 增加**冗餘檢查**，以確保 Redis Cache 返回給正確的用戶。
3. 改善**日誌 Log**，以識別問題並確認已停止。
4. 識別受影響的用戶，以便**通知**他們。
5. 增加 Redis cluster 的**穩定性和可擴展性**，減少在極端負載下，連線錯誤的可能性。

身為 IT 從業人員，我只能說望塵莫及。

你說差別在哪？基本上光是這 5 個項目，我只能說在我的周遭觀察過的，多半只做了修復單點 bug。「解完就沒事了」「祈禱他不要再發生」。

* 至於要多少測試？「我先手動測一測就好了」
* 回頭改善 Log？「那是別人的事」
* 通知受影響用戶？「我趕快修一修就好」
* 增加穩定性？「那個很複雜現在沒時間作」

如此簡單易懂的道理，實行起來就是如此困難。而我們能做的只是每一次都盡可能引導身邊的同事，一起加入更有系統、有效率解決問題的行列。

### Incident Managment 事件處理

像是 status page 狀態頁面這類非常常見的可觀測性服務，若沒有將自己的服務視為重要的，那就很可能會忽略掉。

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/sre/2023-03-25-chatgpt-sre-postmortem-status-page.jpg?raw=true">
<p align="center"><sub><sup>
  Status Page
</sup></sub></p>

我們很常去談 monitoring 監控的重要性，什麼服務掛了我要自動知道。但是卻很少去談「服務掛了我要怎麼處理、甚至自動修復」。這就牽涉到 **"Incident Managment 事件處理" 與 "Self Repairing 自我修復"**。一個是讓事件受影響的人與環節能被充分討論，找出根因並徹底防範；另一個是如何減少人為操作成分，盡可能自動化。這些都是 SRE 裡會談的東西，也是我們能真正意義上讓服務自動維運的關鍵。

## 運用工程手段，積極尋求解法

在**一週內修復，並公開事後剖析報告，擬定下一步防範措施**。我想這應該比刻意隱瞞，被抓到了之後再「謝謝指教」來得有說服力的多。

人非聖賢，孰能無過。關鍵是**如何不二過**。坦然面對，運用工程手段，積極尋求解法，這些都是再簡單不過的道理，但能如此自然採取行動的，卻總是少數。

有效的維運管理需要有 "**主動和解決問題的思維**"。我想，關鍵在於**心態**:

> **Take ownership and get things done.**

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)
2. [ChatGPT 如何協助人類? 應用 AI 與科幻哲思](https://blog.androchen.tw/chatgpt-applied-ai-sci-fi-reflection)
3. [如何善用 AI 加速知識循環](https://blog.androchen.tw/ai-accelerate-knowledge-revolution)

### Murmur

* 2023-03-25: 態度決定高度、心態決定境界。
  * 這次還是寫了好久(2.5 hr) 😂, 下次再想想看怎麼拆解加速...
