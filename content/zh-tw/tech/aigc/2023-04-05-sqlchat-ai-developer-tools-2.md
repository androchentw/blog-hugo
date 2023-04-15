---
title: "自然語言 SQL Client + Chatbot - AI 時代開發者工具 2.0"
url: sqlchat-ai-developer-tools-2
# date: 2023-04-04T20:30:00+08:00
date: 2023-04-05T07:00:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - aigc
  - chatgpt
  - productivity
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-05-sqlchat-ai-developer-tools-2-overview.png?raw=true
series: aigc
---

## Overview

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-05-sqlchat-ai-developer-tools-2-overview.png?raw=true">
<p align="center"><sub><sup>
  自然語言 SQL Client + Chatbot - AI 時代開發者工具 2.0
</sup></sub></p>

2023-03-31 [bytebase 推出 SQL Chat](https://www.bytebase.com/blog/sql-chat): 融合 SQL Client 與 Chatbot，可以使用自然語言提出資料庫問題和查詢資料庫。目前支持 MySQL, PostgreSQL。並且提供 [開源 GitHub Repo](https://github.com/sqlchat/sqlchat)，可以自建並連接本地 database。

非常推薦 Data Engineering, Data Science 甚至 Business Analysis 相關領域的朋友去 [SQL Chat 線上環境](https://www.sqlchat.ai/)玩一玩。

我想從兩個層面，結合紅杉資本(Sequoia Capital) 提到的 [Developer Tools 2.0](https://www.sequoiacap.com/article/ai-powered-developer-tools/)，以及最近的職場觀察，探究更深一層的開發者體驗議題。

🤔 Q:

1. AI 能不能寫 SQL?
2. AI 擅長協助什麼樣的 SQL 開發?

💪 A: 思考自己拿 ChatGPT / AI 用來做些什麼? 效果如何? 還有什麼發揮潛力?

<!--more-->

## Text to SQL 應用竄起

前陣子聽不少人 (可能有超過 5 ~ 10 位，普遍認為) 對於 ChatGPT 能不能寫 SQL，一直持反對意見，覺得只能處理簡單場景。我始終相信是時間 + 用法問題。又尤其現在已經有整合的體驗出來，實際上用一用，就會發現「IDE 等級的開發者體驗」跟「貼問題到 ChatGPT」不是同個等級，更不用說是跟人相比了。

我們可以看到，隨著 finetune model 的興起，適合不適合可能都只是時間問題。

Bytebase 自己寫了一篇 blog 整裡了 [7 個 ChatGPT 增強的資料庫工具](https://www.bytebase.com/blog/chatgpt-enhanced-database-tools):

1. [sqlTranslate](https://www.sqltranslate.app/): SQL 翻譯機。可以通過輸入自然語言獲取相應的 SQL 語句，反之亦然。運用 OpenAI API。
2. [AI2sql](https://www.ai2sql.io/): SQL 生成器，可以讓工程師和非工程師輕鬆地編寫 SQL，支援的資料庫包括市場上最流行的資料庫，如 MySQL、PostgreSQL、MongoDB、Oracle 等。運用 GPT-3。
3. Aoi (葵): 可以跑在 Terminal 的 ChatGPT 驅動對話程式。可以進行自然語言對話並執行 SQL 任務。
4. [Bytebase](https://www.bytebase.com/): 官方口號 "Reliable Database CI/CD for Developers", "The GitLab for Database DevOps"，當然也包含了本篇提到的 SQLChat - SQL Client + Chatbot。
5. [DBeaver](https://dbeaver.io/): 一個老牌的 SQL 客戶端，具有 SQL 編輯器、數據和架構遷移能力以及資料庫連接監控等功能。在 2 月初，DBeaver 也導入了 GPT-3，可以將自然語言轉換為 SQL 查詢語句。
6. [OSSInsight](https://ossinsight.io/): 使用 OpenAI 在 GitHub 數據中生成 SQL 查詢的工具，最近推出了一個名為 "Data Explorer" 的新工具，可以通過自然語言提出問題，AI 會為您生成相應的 SQL 查詢。
7. [Outerbase](https://outerbase.com/): 一個於 2023 年 2 月 15 日正式推出的新工具，用戶體驗類似於 Excel 電子表格，並使用 GPT-3 幫助用戶編寫 SQL 查詢和生成儀表板，適用於開發人員和數據分析師。甚至他們還出了自己的 EZQL 😂 直接讓你不再寫 SQL。

有興趣的都可以去玩一下。講回到 SQL Chat，他提供的線上 [Live Demo](https://demo.bytebase.com/?ref=bytebase.com) 加上 [SQL Chat](https://www.sqlchat.ai/)，兩者疊加的開發者體驗實在只有驚艷兩字可以形容。試試看就對了！

<img style="width:80%;" src="https://www.bytebase.com/static/blog/sql-chat/sqlchat-ui.webp">
<p align="center"><sub><sup>
  SQL Chat: 使用自然語言向 Chatbot 取得 SQL query
</sup></sub></p>

### 資料隱私 Data Privacy

關於資料隱私當然也是大家最關注的。在[開源 GitHub Repo](https://github.com/sqlchat/sqlchat) 有寫。至於信不信，有興趣的話撈封包就知道囉。

中文:

1. 所有 database connection configs 都存儲在本地瀏覽器中。還可以透過 settings 以清除數據。
2. 只有資料庫架構將被發送到 OpenAI API，不會發送任何 table data。

英文:

1. All database connection configs are stored locally in your browser. You can also visit settings to clear the data.
2. Only the database schema will be sent to the OpenAI API. No table data will be sent there.

## SQL 效能優化的未來

還有很多人擔心使用 ChatGPT 所寫出來的 SQL 效率不高、不夠優化。

我想說的是，**20 年前寫程式，你必須對記憶體操作和優化非常熟悉**。即便是現在，在工程師界和 Google 齊名的 StackOverflow 論壇原本的意思也是指「堆疊溢位（stack overflow）」，簡而言之就是記憶體破產（根據維基百科：在電腦科學中，當使用過多的記憶體時，會導致呼叫堆疊產生溢位）。

現在，有多少開發人員寫應用程式時會計較**耗用了多少記憶體**？

我認為 SQL 也可能會面臨類似的情況。在未來，我們可能會優先考慮使用更多的空間來換取時間，當空間比起時間和開發人力不值錢時，這種情況就尤其明顯。在這種情況下，SQL 的執行效能優化也許會被其他方法所取代。就像我們

1. 用更高階且簡便的程式語言
2. 形成更有效率的開發
3. 帶來更多的 3rd party library 與蓬勃發展的社群。

更重要的是，這個過程替代掉了最寶貴的人力。

## 使用 Copilot 的教育意義

另外，這也關係到程式碼如何才叫有品質？有時候，我認為這類 Copilot 的**教育意義更大於實質意義**。儘管你說它只能處理簡單的內容，但在職場上，很多人因為**只關注當前的程式碼是否能運作**，而忽略了基本的概念。這種錯誤觀念很常發生。而這樣的 sandbox 和 IDE 解釋環境可以提供絕佳的練習機會。例如

1. 進行 code review
2. 對新開發人員進行教育訓練
3. 使用 mock data 來釐清你的意圖
4. 測試一段 SQL 的真實作用 / 副作用

總而言之，該如何使用這些工具會決定它們的使用價值和適用性。用我自己的話來說，借用保哥的話:

> 如果你的程式寫到連 AI / ChatGPT / Copilot 都看不懂，沒辦法給建議的話，那你可能要先檢討你自己。

## 開放心態是關鍵

另外一個重點是**開放的心態（Open-minded）**。

最近我經常思考一個問題，我認為有一些人會遇到這個問題：他們會問自己為什麼別人可以大幅提高效率，但自己卻無法做到。這就需要更開放地去思考問題。比如說，有可能是:

1. **流程理解不深**: 對於流程的理解沒有全局掌握，就沒辦法分階段解決問題。關於解析流程這點我們之後專門寫一篇給大家講解 （老高上身？）
2. **流程分配不均**：如果你省略了測試，那麼你很可能會發現自己花了大量時間在除錯上。這不是因為 AI 不能幫你測試，而是因為你根本沒有進行測試（I don't always test my code, but when I do, I do it in production）。
3. **抽象化思維不熟**：有時也不一定是 ChatGPT 除錯幫不上忙，而是因為你習慣單點式地「碰一題解一題」，而沒有嘗試去沈澱/理解最近碰到的，都是同一類問題。

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-05-sqlchat-ai-developer-tools-2-meme-hurry.jpg?raw=true">
<p align="center"><sub><sup>
  盲點1 流程理解不深: 專案太趕了所以我們沒空寫測試跟文件 (不良示範)
</sup></sub></p>

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-05-sqlchat-ai-developer-tools-2-meme-debug.jpg?raw=true">
<p align="center"><sub><sup>
  盲點2 流程分配不均: 開發者的一天 = 99% 除錯 (不良示範)
</sup></sub></p>

[The Magic of ChatGPT for SQL Developers: How ChatGPT can Revolutionize the World of Database Management?](https://levelup.gitconnected.com/the-magic-of-chatgpt-for-sql-developers-10b2fe84aea) 一文提到了 6 點適合讓 ChatGPT 協助 SQL 開發者的:

1. 提供語法和代碼示例. Providing syntax and code examples
2. 故障排除 SQL 代碼. Troubleshooting SQL code
3. 生成資料庫性能和使用情況報告. Generating reports on database performance and usage
4. 支持資料庫遷移. Supporting database migration
5. 提供資料庫安全建議. Providing database security advice
6. 數據可視化. Data visualization

一定有一些是我們能用，有些不能用的。而去辨識這些差異，截長補短，就是我們的專業所在了。

## AI 時代的 Developer Tools 2.0

最後我們來看看 [SQL Chat Announce Blog](https://www.bytebase.com/blog/sql-chat) 中提到 紅杉資本(Sequoia Capital) 的 [Developer Tools 2.0](https://www.sequoiacap.com/article/ai-powered-developer-tools/) 一文 (2023-03-22)。

這大圖洋洋灑灑地把 SDLC (Software Development Lifecycle, 軟體開發生命週期) 攤開，左邊是現任者 (incumbent)，中間是挑戰者 (challenger)，右邊再畫了一個大空白圈圈留給 AI 時代帶來的開發工具 2.0 無限想像空間。

這場 "**Copilot for X**" 的 AI 輔助大賽，才剛開始呢。

<img style="width:100%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-04-05-sqlchat-ai-developer-tools-2-dev-ai.png?raw=true">
<p align="center"><sub><sup>
  紅杉資本(Sequoia Capital) 眼中的 <a href="https://www.sequoiacap.com/article/ai-powered-developer-tools/" target="blank">Developer Tool 2.0</a>
</sup></sub></p>

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [ChatGPT 實戰 - 3 招加速知識產出](https://blog.androchen.tw/chatgpt-knowledge-production)
2. [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)
3. [如何善用 AI 加速知識循環](https://blog.androchen.tw/ai-accelerate-knowledge-revolution)

### Murmur

* 2023-04-05: 看到還是忍不住寫了一篇 😂
