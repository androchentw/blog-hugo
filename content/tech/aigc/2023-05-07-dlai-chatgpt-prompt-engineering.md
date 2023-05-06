---
draft: true
title: "ChatGPT 實戰 10 招 - DeepLearning.AI Prompt 免費課程"
url: dlai-chatgot-prompt-engineering
# date: 2023-05-06T08:30:00+08:00
date: 2023-05-07T09:00:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - aigc
  - chatgpt
  - productivity
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-05-07-dlai-chatgpt-prompt-engineering-1-overview.jpg?raw=true
series: aigc
---

## Overview

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-05-07-dlai-chatgpt-prompt-engineering-1-overview.jpg?raw=true">
<p align="center"><sub><sup>
  DLAI ChatGPT Prompt Engineering
</sup></sub></p>

2023-04-28 (五) 左右，AI 大師吳恩達與 DeepLearning.AI 合作推出免費 1.5 小時線上課程: [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/)。相信已經很多人也被心得文資訊轟炸過一輪。

先說結論:

1. 不需要在意太多別人的文章，包含我的這一篇，重要的是**自己動手實作**。(雖然我也一向不寫太詳細的操作文 😂)。2023-05-06 的活動: [2023 Generative AI (AIGC 詠唱者年會)](https://hackmd.io/@ejc/2023gaiconf/https%3A%2F%2Fhackmd.io%2F%40ejc%2F2023gaiconf) 當中，也有各種非理工的實作應用，值得大家多加參考。
2. 大膽地說，**所有現代社會人都應該學習 ChatGPT 及其應用，以提高生產力**。這一波的發展下來，普遍的共識是 AI 將會成為比手機與電腦更為普及的存在。如果你認同手機與電腦是當代社會吸收資訊及工作不可或缺的工具，那就沒有理由不學習 AI 的使用方式。AI 互動學成為未來 10 年後的一門基礎教育課，可能都不為過。
3. 反過來說，不學又怎麼樣？ 20 年後的話，可能就像出門都用雙腳走路，不使用任何電器、不搭乘交通工具。可以過著一個清閒的自然生活，但同時也失去了探索更多地區的體驗。雖然不會真的怎麼樣，但也有點可惜。

這個課程適合的客群 TA:

1. 💪 希望更進一步提升自己使用 ChatGPT 等 LLM 的生產力。
2. 🕒 願意投資時間 (2 ~ 4小時) 理解並運用。課程 9 章共 1.5 小時左右，加上吸收理解的時間，就算當作一個週末的英文聽力也好。
3. 💻 具備一點程式基礎。課程會搭配線上 Jupyter Notebook & Python SDK。

我想特別鼓勵一下**沒有程式基礎的朋友，不用擔心**。因為影片裡都有程式範例，也有解說，就算聽不懂也可以一鍵執行。而且你會發現高階語言已經不如以往的程式一般可怕，當作英文文章去讀即可。在我這一輩的台灣社會，習慣用文組/理組來區分能力。事實上完全不需要畫地自限，負面自我暗示。不如說，**ChatGPT 等 LLM 的誕生，為文組人帶來實作能力強化的好處**。畢竟，你也不會說出「因為我是文組的，所以我學不會使用手機跟電腦」吧 😂

另一層面，你可以將程式語言視為是一種「**更有結構、邏輯性更強的語言**」。透過這個機會學習一種語言表達的方式，是非常適合且有效率的。用人話來說，就是「學了程式語言之後，我才發現自己平常講話的邏輯是多麼模糊不清」。不懂的地方就問 ChatGPT，持續學習！所有的學習都不會白費 👍

你能透過這篇文章學到:

1. 📝 30% 理論統整。我會重點摘要幾個關鍵字成 mindmap，便於作為課程心得提醒。
2. 🛠️ 60% 實戰技巧。我喜歡將實戰技巧化為 cheatsheet，便於日後應用。
3. 💡 10% 應用發想。最重要的是腦力激盪的部分。

🤔 Q: ChatGPT 可以應用在你的工作與生活中，哪些流程?

💪 A: 思考自己拿 ChatGPT / AI 用來做些什麼? 效果如何? 還有什麼地方可以發揮潛力?

<!--more-->

## 前情提要

1. 課程目標: 激發你對新應用的**想像力**。
2. **明確指示**: 將 LLM 視為 "**聰明但不清楚任務細節的人**"。

我本身的工作是在做開發維運的流程優化，所以會習慣從流程的觀點切入。內容也不會跟課程完全一樣。

建議重點還是放在各位的**日常實務**。在未來的使用過程中，可以時常回想自己是否有做到這些。

以下附上課程摘要心智圖，可以參考[此 gist](https://gist.github.com/androchentw/a49e672eed4f1089f4aaf76f6509dfd0)，搭配 [markmap](https://markmap.js.org/repl) 進行呈現。

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-05-07-dlai-chatgpt-prompt-engineering-1-summary.jpg?raw=true">
<p align="center"><sub><sup>
  1-Summary mindmap
</sup></sub></p>

## 02 準則 Guidelines

[02 準則](https://learn.deeplearning.ai/chatgpt-prompt-eng/lesson/2/guidelines)

### 1. 清晰且具體的指示

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-05-07-dlai-chatgpt-prompt-engineering-2-1.jpg?raw=true">
<p align="center"><sub><sup>
  2-1
</sup></sub></p>

> 1. 寫出清晰且具體的指示 write **clear and specific instructions**.
>
> 2. 清晰不等於簡短 clear != short.

實戰技巧

1. 分隔符號 Use delimiters (```, ===, ...) 以避免 prompt injections
2. 結構化輸出 structured output (HTML, JSON, markdown, ...)
3. 例外處理 Exception Handling
4. 示範成功 Few-shot prompting

整合範例

```prompt
Q: What is [user2]'s response?

* Delimiter: Answer in a consistent style. Content is within >>>
* Structured output: Respond in markdown format
* Exception Handling: If there are no contents available, just respond "NA"

>>>
[user1] What is ETL?

[user2] First extract, then transform, then load.

[user1] What is ELT?
>>>
```

### 2. 思考時間

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-05-07-dlai-chatgpt-prompt-engineering-2-2.jpg?raw=true">
<p align="center"><sub><sup>
  2-2
</sup></sub></p>

> 給模型思考的時間 Give the model time to think.

1. 不要給太過複雜的指示。
2. 或是切分成數個小的任務。
3. 或是請 ChatGPT 列出任務列表，再自行手動調整。
4. 讓 ChatGPT 自己想出答案，再跟既有答案比較，並進行評估。

```prompt
* Perform the following actions

Step 1. 
Step 2. 
Step 3.

Using the following format:

* Text: <text to summarize>
* Summary: <summary>
* Translation: <summary translation>

Text to summarize: <{text}>
```

### 3. 模型限制 Model Limitation

1. **幻覺** Hallucination: 「一本正經的瞎掰」。
2. 對策: 先找相關資訊 > 再基於前述內容回答。

## 03 迭代 Iterative

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-05-07-dlai-chatgpt-prompt-engineering-3-1.jpg?raw=true">
<p align="center"><sub><sup>
  3-1 Iterative Prompt Development: 敏捷迭代！
</sup></sub></p>

> 不需要去在意什麼 "30 個完美 prompt" 的文章。

1. 第一次執行的 prompt 並不重要，重要的是**過程**。瞭解如何用更好的過程來開發，並取得正確的 prompts。
2. 減少迭代次數，而不是記憶多少 prompt。因為每次的需求都會不太一樣。
3. 透過指定字數, 格式等**特定規格**，以更精準地達到你要的結果。

## 04 摘要 Summarizing

1. 客製化摘要 Summarize: 為不同對象總結不同內容 (運輸 / 定價部門)
2. 流程應用範例: 為個別客戶評論進行總結 (迴圈 `for` loop)

## 05 推理 Inferring

> 從客戶評論中，取得商品評價細節

1. 情感分析 Sentiment analysis
2. 萃取資訊 Extract information
3. 推理文章主題 + 比對判斷關鍵字 Inferring


## 06 轉化 Transforming

1. 翻譯 Translate
2. 校對 Proofread: 文法, 拼字檢查
3. 語氣轉換 Change tone

```prompt
proofread and correct this review. Make it more compelling. 
Ensure it follows APA style guide and targets an advanced reader. 
Output in markdown format.
Text: ```{text}```
```

## 07 擴寫 Expanding

## 08 聊天機器人 Chatbot

## 09 結論 Conclusion

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-05-07-dlai-chatgpt-prompt-engineering-9-1.jpg?raw=true">
<p align="center"><sub><sup>
  數據 > 資訊 > 知識 > 洞察 > 智慧. <a href="https://random-blather.com/2014/04/28/information-isnt-power/" target="_blank">David Somerville</a>
</sup></sub></p>

最後分享一張我很喜歡的圖。為什麼要強調需要動手實作呢? 因為看完**別人的文章，終究只是資訊**而已。要能夠成為自己可以應用的知識，甚至從中發現洞察，關鍵步驟就是**透過實作，與自己的既有知識產生連結**。

持續學習，共勉之 💪

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)
2. [如何善用 AI 加速知識循環](https://blog.androchen.tw/ai-accelerate-knowledge-revolution)

### Murmur

* 2023-05-06: 不斷學習!
