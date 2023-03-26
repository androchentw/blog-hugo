---
title: "ChatGPT 實戰 - 3 招加速知識產出"
url: /chatgpt-knowledge-production
# date: 2023-03-26T12:30:00+08:00
date: 2023-03-26T16:30:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - aigc
  - chatgpt
  - writing
  - productivity
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-03-26-chatgpt-knowledge-production-cover.png?raw=true
series: aigc
---

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-03-26-chatgpt-knowledge-production-cover.png?raw=true">
<p align="center"><sub><sup>
  ChatGPT Prompt 實戰 - 3 招加速知識生產
</sup></sub></p>

## Overview 概述

🤖 相信大家已經開始運用 ChatGPT 與各種 AI 在輔助寫作，提高知識產出效率，快速完成一篇文章撰寫。在很多知識領域，完全可以算是一種典範轉移 (Paradigm Shift) 了。

📝 先前總結了 [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)。這次，我剖析自己寫作過程的 4 大階段:

1. 思: 想法
2. 骨: 大綱
3. 肉: 子題內容
4. 皮: 潤飾

來探討如何加速知識生產。針對不同的情境，分而治之。

<!--more-->

## 為什麼要寫 Blog?

總結原因有三:

1. 我本來就有興趣關注。也可以說是一種小確幸的**成就感**。
2. 輸出就是最好的**消化**。透過文字重新整理自己的思緒。
3. 可以激發不到角度的**討論**，進一步刺激自己的思考。被問問題的時候就是腦子動得最快的時候 😂

把寫 blog 視為是一種知識產出，我想特別推薦 [The Sense of Style](https://www.amazon.com/-/zh_TW/Steven-Pinker-ebook/dp/B00INIYG74/ref=tmm_kin_swatch_0?_encoding=UTF8&qid=&sr=) 的這段描述

> 寫作之難，在於將**網狀的思想**，通過**樹狀的句法**，用**線性的文字**展開 -- 《寫作風格的意識：好的英語寫作怎麽寫》, 史迪芬.平克, 2014
>
> Skillful writers must be sensitive to the ways in which syntax converts a **tangled web of ideas** into a **linear string of words**. -- The Sense of Style: The Thinking Person's Guide to Writing in the 21st Century, Steven Pinker, 2014

## 知識產出的組成結構是?

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-03-26-chatgpt-knowledge-production-time-management.png?raw=true">
<p align="center"><sub><sup>
  知識產出/文章撰寫 時間分配
</sup></sub></p>

歸納了一下，我平常在寫 blog 的組成大致可分 4 大階段:

| 階段佔比 | 主要目標 | 細項任務 |
| --- | --- | --- |
| 10% 點 | 思: 想法 (我想到什麼) | 5% 筆記零散想法 <br /> 5% 重整 |
| 20% 線 | 骨: 大綱 (我想說什麼) | 15% **構思**文章骨架 <br /> 5% 也會依著子題寫一寫，再回來調整 |
| **^50% 面** | 肉: 子題內容 (我想說哪些) | ^30% 查找並**消化**資料，理解/擷取想傳達的 <br /> ^20% 以自己的觀點重新**詮釋** |
| 20% 體 | 皮: 潤飾 | 10% **素材/排版**. 一般作業/找圖/製作/壓縮 <br /> ^10% **社群**貼文: 圖/摘要/互動 |

## 3 招 Prompt 加速知識產出

其中有 3 段是我現在會開始運用 ChatGPT 或其他 AI 來輔助的部分:

### 1. 30% 消化資料

平常很多資訊都是英文，吸收的效率沒有 native speaker 那麼好，所以這部分主要是彙整 + 翻譯 他人文章，讓我可以快速抓到大的框架，再往細節去理解。

值得一提的是，要小心 "**淺層知識**"。 像是 [ReaderGPT](https://chrome.google.com/webstore/detail/readergpt-chatgpt-based-w/ohgodjgnfedgikkgcjdkomkadbfedcjd), [ChatGPT Sidebar](https://chrome.google.com/webstore/detail/chatgpt-sidebar-support-g/difoiogjjojoaoomphldepapgpbgkhkb)，他們的總結功能都很令人驚艷。但是，我認為還是得要**自己吸收一遍**。

就像美食街的食物模型，能夠幫助你快速瞭解這些菜長什麼樣子。但若你沒吃，最後還是講不出味道啊！**善用 AI 是為了幫助你快理解重點，而不是代替你消化**。

```py
# Prompt: 消化/翻譯資料
summarize & translate #zh-TW
```

### 2. 20% 重新詮釋

依照自己的觀點重新詮釋，打出完整句子也會費時。用 AI 潤飾的部分 = 彙整我的草稿，協助補充遺漏的，或是換一個綜觀的角度再檢視我的內容，是否有傳達到重點。另外，因為我會想要保留自己的文筆風格，所以其實這部分會多了要比對自己的文字的功夫。

```py
# Prompt: 詮釋/彙整草稿
summarize #bullet-point #zh-TW
```

### 3. 10% 社群貼文

還有一塊是社群貼文時, 我覺得可以啟動 "小編模式", 讓 AI 用另一個觀點來輔助貼文的口吻:

```py
# Prompt: 社群貼文
summarize to an attractive social media post #zh-TW
```

我也嘗試利用 [Buffer - Social Media Management](https://buffer.com/) 同步將我的貼文發布到 Facebook, Twitter, LinkedIn 上

## 搭配時間管理

另外，也許刻意壓縮時間到 100 分鐘內完成，可能就會更逼著自己不要吹毛求疵，而是專注在整體完整度。

(我覺得我可能需要一個 Gordon Ramsay 在旁邊喊 15 minutes left! 😂)

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-03-26-chatgpt-knowledge-production-gordon-ramsay.png?raw=true">
<p align="center"><sub><sup>
  Gordon Ramsay: 15 minutes left!
</sup></sub></p>

實務上可以使用 Pomodoro 番茄鐘技巧，或是 Clockify 等軟體來記錄耗時。可以參考

1. [如何做好時間管理的三個方法論與工具](https://blog.androchen.tw/time-managment/)
2. [2021 Agile Life](https://blog.androchen.tw/2021-agile-life/)

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. 行為改變循環: [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)
2. 知識革命: [如何善用 AI 加速知識循環](https://blog.androchen.tw/ai-accelerate-knowledge-revolution)
3. 各種場景想像 2022-12-10, 4個月回頭看都感覺像 2 年前的舊聞了: [https://blog.androchen.tw/chatgpt-applied-ai-sci-fi-reflection/](https://blog.androchen.tw/chatgpt-applied-ai-sci-fi-reflection/)

### Murmur

* 2023-03-26: 但其實這篇沒有成功 😂 (大概也是花了 3 小時, 尤其是在做圖的部分花特別久) 習慣還是很難改... 當作目標努力!
