---
title: "Auto-GPT & AgentGPT 有多神? AI 全自動完成任務 - 簡介篇"
url: auto-gpt-agentgpt-introduction
# date: 2023-04-14T20:30:00+08:00
date: 2023-04-15T12:00:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - aigc
  - chatgpt
  - autogpt
  - agentgpt
  - productivity
  - agile
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/zh-tw/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-1-architecture.png?raw=true
series: aigc
---

## Overview

<img style="width:100%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/zh-tw/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-1-architecture.png?raw=true">
<p align="center"><sub><sup>
  Auto-GPT / AgentGPT 的 自動 AI 機制
</sup></sub></p>

在 ChatGPT 釋出約 4 個月後，運用 AI 自動完成任務的架構 [Auto-GPT](https://github.com/Torantulino/Auto-GPT) 與 [AgentGPT](https://agentgpt.reworkd.ai/) 問世。

意思是，只要你提供 "**目標 Goal**"，他就能透過反覆 (**拆解任務 > 實作 > 驗證**) 的迭代過程，最終**自動完成任務**。

能使 Auto-GPT 如此厲害的關鍵在於:

1. 🧠 運用 LLM 理解需求，展開任務
2. 🌐 可連網，即時查詢最新資訊
3. 💾 支援長期記憶儲存資料，突破 ChatGPT token 上限

今天就來拋磚引玉，從以下 4 點分享一下一些觀察總結。

1. 🔥 火力展示
2. ☠️ 危險注意: 💰 預算控管
3. 👀 需求/審核/階段檢視的重要性
4. 🚀 善用 Agile/Lean Startup "MVP" 概念, 打造你的專屬火箭

🤔 Q: Auto-GPT 能做到什麼程度?

💪 A: 思考自己拿 AI 用來做些什麼? 效果如何? 還有什麼發揮潛力?

<!--more-->

## 🔥 火力展示

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/zh-tw/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-2-agentgpt.png?raw=true">
<p align="center"><sub><sup>
  AgentGPT 範例 Web 介面
</sup></sub></p>

詳細幾個範例可見以下幾篇文章:

1. [INSIDE](https://www.inside.com.tw/article/31315-auto-gpt)
2. [遠見](https://www.gvm.com.tw/article/101720)
3. [數位時代](https://www.bnext.com.tw/article/74834/gpt-autogpt-36kr)
4. [電腦王](https://www.techbang.com/posts/105416-chatgpt-ai-autogpt)

我拿 AgentGPT 問 "Build modern startup landing page 打造現代新創一頁式網站", 就開始自動產生以下任務:

1. Generate a list of modern landing page designs from popular startup websites
2. Identify key design elements and features that are common among the selected designs
3. Create a prototype landing page incorporating the identified design elements and features

然後就從第一個任務開始，列出知名的 modern landing page designs 列表如 Airbnb, Uber, Spotify, ...。雖然細節可能不一定是你原先想要的，但我覺得非常值得作為解題思路的參考。

Auto-GPT 與 AgentGPT 兩者使用的詞彙與步驟有所不同，但大同小異:

* Auto-GPT: Goal -> N Thought > (Reasoning, Criticism > Next Action, System) -> Result
* AgentGPT: Goal -> N Task > (Thinking > Executing) -> Result

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/zh-tw/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-3-auto-gpt.png?raw=true">
<p align="center"><sub><sup>
  Auto-GPT 範例 指令介面
</sup></sub></p>

另外，[BabyAGI 的 Task-driven Autonomous Agent](https://twitter.com/yoheinakajima/status/1640934493489070080) 有將原理畫出來，我也發了一支 PR 提供[繁體中文翻譯](https://github.com/yoheinakajima/babyagi/blob/main/docs/README-zh-tw.md)。大家有興趣也可以參考一下。

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/zh-tw/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-4-babyagi.png?raw=true">
<p align="center"><sub><sup>
  BabyAGI 架構原理
</sup></sub></p>

## ☠️ 危險注意: 💰 預算控管

現在看起來有一件事情可以確定，那就是 Auto-GPT 提供的連續模式，真的會**刷爆你的信用卡**。

所以記得先去 OpenAI API 上面設定預算上限。

## 👀 需求/審核/階段檢視的重要性

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/zh-tw/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-5-programmer-joke.jpg?raw=true">
<p align="center"><sub><sup>
  經典程式語言笑話 - 看到西瓜買 1 顆，看到橘子買 10 顆
</sup></sub></p>

這讓我想起一個經典的程式語言笑話:

> 老婆跟老公說「去超市看到西瓜買 1 顆，有看到橘子的話買 10 顆」。
>
> 結果最後老公買了 10 顆西瓜。
>
> (註解: 因為老公 "有看到橘子"，所以買了 10 顆西瓜；但老婆的需求是希望買 10 顆橘子)

如先前在 [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks) 一文提到的「**精準提問**」，「**精準說明需求**」將更是未來的關鍵。因為這直接影響到你會不會看到 10 顆西瓜，或是其他你不預期的行為。

## 🚀 善用 Agile/Lean Startup "MVP" 概念, 打造你的專屬火箭

<img style="width:100%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/zh-tw/tech/aigc/2023-04-15-auto-gpt-agentgpt-introduction-6-mvp.jpg?raw=true">
<p align="center"><sub><sup>
  <a href="https://startupbasics.com/minimum-viable-product" target="_blank rel="noopener noreferrer">startup basics</a> - Lean Startup MVP 概念 滑板車 -> 汽車
</sup></sub></p>

看完以上內容，想必有 Agile software engineering 敏捷軟體開發相關經驗的朋友肯定不陌生。

要如何避免「**花費大量時間與成本，最後卻打造出用戶不需要的產品**」，就是 Agile 與 Lean Startup 的強項。

所謂的 MVP 指的是 **最小可行產品 (Minimum Viable Product)**，以滑板車與汽車為例，指的就是在交付產品給你的關鍵目標客戶時，採取的迭代方式:

* ❌ 不應該: 車輪 > 底盤 > 門 > 汽車
* ✅ 應該: 滑板車 > 腳踏車 > 機車 > 汽車

原因非常簡單，因為若你的客戶需要解決的痛點是「不想走路，想要有更快更便利的交通工具」，那滑板車可能在 2 週後就能交付給他；而汽車在完全組裝成汽車前，都是無法交付/使用的零件。真的能拿來用，可能都半年後了，而那時你的客戶也許已經有另外的需求。

所以也許，我們也可以在多種層面上運用 Auto-GPT。這裡想到幾個:

1. 設定 MVP，階段性設定最小目標，並檢視成果，然後反覆迭代。
2. 學習 Auto-GPT 如何拆解任務，再反向利用在平常 Agile breakdown: Epic > Story > Task 的過程。

## 你怎麼看?

下一篇，我將分享自己實作 Auto-GPT, AgentGPT 之間的使用心得評比。

你希望看到什麼應用呢?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)
2. [ChatGPT 實戰 - 3 招加速知識產出](https://blog.androchen.tw/chatgpt-knowledge-production)
3. [如何善用 AI 加速知識循環](https://blog.androchen.tw/ai-accelerate-knowledge-revolution)

### Murmur

* 2023-04-15: 驚人的發展速度，真的是 AIGC 元年 🤣
