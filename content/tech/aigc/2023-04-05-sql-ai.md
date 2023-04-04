---
draft: true
title: "自然語言查詢 SQL Client + Chatbot - 談開發者工具 2.0"
url: /sqlchat-client-chatbot-developer-tool-2
# date: 2023-04-04T20:30:00+08:00
date: 2023-04-05T16:30:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - aigc
  - chatgpt
  - productivity
share_img: https://www.bytebase.com/static/blog/sql-chat/sqlchat-ui.webp
series: aigc
---

<img style="width:80%;" src="https://www.bytebase.com/static/blog/sql-chat/sqlchat-ui.webp">
<p align="center"><sub><sup>
  使用自然語言取得 SQL query
</sup></sub></p>

2023-03-31 [bytebase 推出 SQL Chat](https://www.bytebase.com/blog/sql-chat): 融合 SQL Client 與 Chatbot，可以使用自然語言提出數據庫問題和查詢數據庫。目前支持 MySQL, PostgreSQL。並且提供 [開源 GitHub Repo](https://github.com/sqlchat/sqlchat)，可以自建並連接本地 database。

非常推薦 Data Engineering, Data Science 甚至 Business Analysis 相關領域的朋友去線上環境玩一玩。

很多人對於 ChatGPT 能不能寫 SQL, 一直持反對意見。我相信是時間 + 用法問題。又尤其現在已經有整合的體驗出來，實際上用一用，就會發現「IDE 等級的開發者體驗」跟「貼問題到 ChatGPT」不是同個等級，更不用說是跟人相比了。

仔細研究了一下，結合關於 Developer Tool 2.0 與開發者體驗的思考，我想從兩個層面去看。

🤔 Q:

1. AI 能不能寫 SQL?
2. AI 擅長協助 SQL 做什麼?

💪 A: 思考自己拿 ChatGPT / AI 用來做些什麼? 效果如何? 還有什麼發揮空間?

<!--more-->

## AI Text to SQL 逐漸抬頭

<img style="width:80%;" src="https://www.bytebase.com/static/blog/sql-chat/sqlchat-ui.webp">
<p align="center"><sub><sup>
  使用自然語言取得 SQL query
</sup></sub></p>

我們都可以看到，隨著 finetune model 的興起，適合不適合可能都只是時間問題。

1. bytebase - Reliable Database CI/CD for Developers
2. <https://www.ai2sql.io/>: 要錢，但 support 更多 (Oracle PL/SQL, NoSQL - Pandas, MongoDB, BigQuery, MariaDB, Redshift, SnowSQL)
3. <https://www.text2sql.ai/>

[The Magic of ChatGPT for SQL Developers](https://levelup.gitconnected.com/the-magic-of-chatgpt-for-sql-developers-10b2fe84aea)

功能在[定價頁](https://www.bytebase.com/pricing)，一應俱全

1. Change Management
2. SQL Editor
3. Collaboration
4. Data Security & Governance

### 資料隱私 Data Privacy

關於資料隱私當然也是大家最關注的。在[開源 GitHub Repo](https://github.com/sqlchat/sqlchat) 有寫。至於信不信，有興趣的話撈封包就知道囉。

中文:

1. 所有 database connection configs 都存儲在本地瀏覽器中。還可以透過 settings 以清除數據。
2. 只有數據庫架構將被發送到 OpenAI API，不會發送任何 table data。

英文:

1. All database connection configs are stored locally in your browser. You can also visit settings to clear the data.
2. Only the database schema will be sent to the OpenAI API. No table data will be sent there.

## 用法: 優化議題

還有很多人會提到 ChatGPT 寫出來的 SQL 不夠優化，效率很差。

我想說的是，20 年前寫程式，你必須很熟練記憶體操作與優化。
甚至著名的程式論壇，在工程師界與 Google 齊名的 StackOverflow 原本意思就是 "堆疊溢位（英語：stack overflow）"，簡單說就是你記憶體破產了（Wiki: 在電腦科學中是指使用過多的記憶體時導致呼叫堆疊產生的溢位）

現在有多少開發人員，寫應用程式在計較耗用多少記憶體？

SQL 對我來說很有可能也是一樣意思。
總有一天我們

## 用法: 教育意義

甚至有的時候，我都覺得這類 copilot 的教育意義更大於實質意義。
你說他只能處理簡單的，但很常我們在職場上是很多人在犯基本觀念錯誤，就是因為只在意眼前的 code 能動就好，也沒想過去理解他。
這樣的一個 sandbox 與解釋是絕佳的練習場合。不管是在 Code Review 或是 new project landing 給新 developer 做教育訓練，都會是一個特好的方式。

完全可以給他 fake 的 schema，用來釐清你的意圖，或 SQL 該怎麼寫。

總歸一句，怎麼用才會決定你的好用/適用與否。套句保哥提過的，用我的話來說：

> 如果你的程式寫到連 AI / ChatGPT / Copilot 都看不懂，沒辦法給建議的話，那你可能要先檢討你自己。

## Developer Tool 2.0

最後我們來看看 [SQL Chat Announce Blog](https://www.bytebase.com/blog/sql-chat) 中提到 紅杉資本(Sequoia Capital) 的 [Developer Tool 2.0](https://www.sequoiacap.com/article/ai-powered-developer-tools/) 一文 (2023-03-22)。

這場 "Copilot for X" 的 AI 輔助大賽，才剛開始呢。

<img style="width:80%;" src="https://www.sequoiacap.com/wp-content/uploads/sites/6/2023/03/dev-ai-wide-10.png">
<p align="center"><sub><sup>
  Developer Tool 2.0
</sup></sub></p>

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [ChatGPT 實戰 - 3 招加速知識產出](https://blog.androchen.tw/chatgpt-knowledge-production)
2. [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)
3. [如何善用 AI 加速知識循環](https://blog.androchen.tw/ai-accelerate-knowledge-revolution)

### Murmur

* 2023-04-05: 看到還是忍不住寫了一篇 😂
