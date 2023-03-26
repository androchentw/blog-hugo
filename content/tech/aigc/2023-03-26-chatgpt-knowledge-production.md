---
draft: true
title: "ChatGPT 實戰 - 3 招加速知識產出"
url: /chatgpt-knowledge-production
# date: 2023-03-26T12:30:00+08:00
date: 2023-03-26T15:30:00+08:00
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
  ChatGPT Prompt 實戰 - 3 招加速知識生產術
</sup></sub></p>

## Overview 概述

prompt = 提詞工程 (引導/指令)

🥇 淺層知識 談 ReaderGPT。就像 美食街食物模型，你看是看了但沒吃 最後還是講不出味道啊。目的是幫助你快理解重點，而不是代替你消化。

<!--more-->

## 為什麼要寫 Blog?

總結原因有三:

1. 我本來就有興趣關注。也可以說是一種小確幸的**成就感**。
2. 輸出就是最好的**消化**。透過文字重新整理自己的思緒。
3. 可以激發不到角度的**討論**，進一步刺激自己的思考。被問問題的時候就是腦子動得最快的時候 😂

其中, 我又想特別推薦 [The Sense of Style](https://www.amazon.com/-/zh_TW/Steven-Pinker-ebook/dp/B00INIYG74/ref=tmm_kin_swatch_0?_encoding=UTF8&qid=&sr=) 的這段描述

> 寫作之難，在於將**網狀的思想**，通過**樹狀的句法**，用**線性的文字**展開 -- 《寫作風格的意識：好的英語寫作怎麽寫》, 史迪芬.平克, 2014
>
> Skillful writers must be sensitive to the ways in which syntax converts a **tangled web of ideas** into a **linear string of words**. -- The Sense of Style: The Thinking Person's Guide to Writing in the 21st Century, Steven Pinker, 2014

## 知識產出的組成結構是?

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-03-26-chatgpt-knowledge-production-time.png?raw=true">
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

用 AI 摘要的部分: 彙整 + 翻譯 他人文章 (Summarize + Translate)

另外，因為我會想要保留自己的文筆風格，所以其實這部分會多了要比對自己的文字的功夫。

```py
# Prompt: 消化/翻譯資料
summarize & translate #zh-TW
```

### 2. 20% 重新詮釋

依照自己的觀點重新詮釋，打出完整句子也會費時
用 AI 潤飾的部分 = 彙整 我的草稿 Summarize

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

## 透過時間管理加速循環

另外，也許刻意壓縮時間到 100 分鐘內完成，可能就會更逼著自己不要吹毛求疵，而是專注在整體完整度。

(我覺得我可能需要一個 Gordon Ramsay 在旁邊喊 15 minutes left! 😂)

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/aigc/2023-03-26-chatgpt-knowledge-production-gordon-ramsay.png?raw=true">
<p align="center"><sub><sup>
  Gordon Ramsay: 15 minutes left!
</sup></sub></p>

實務上可以使用 Pomodoro 番茄鐘技巧，或是 Clockify 等軟體來記錄耗時。可以參考

1. [如何做好時間管理的三個方法論與工具](https://blog.androchen.tw/time-managment/)
2. [2021 Agile Life](https://blog.androchen.tw/2021-agile-life/)

## 補充: 知識產出方法論

### 1. 什麼是 knowledge production

知識生產是指通過各種過程如研究、教育、創新和交流，創建、傳播和利用知識。特別是人工智慧（AI）的發展對知識生產和未來的學習、工作和生活方式有著極大的影響。

AI可以通過分析大量的數據並產生人類可能無法辨識的見解來協助知識生產。這可以導致更高效和準確的研究和開發過程，以及創建新產品和服務。例如，AI算法可以幫助研究人員篩選大量的醫學數據，以識別模式並開發更有效的治療方法。

AI也可以通過提供個性化的學習體驗並適應個人的學習風格來協助教育。使用AI，教育工作者可以跟蹤學生進度並調整他們的教學方法以滿足每個學生的需求，從而實現更有效和高效的學習過程。

然而，AI協助的知識生產的未來也存在潛在的風險和挑戰。一個問題是AI算法可能存在偏見，這可能導致不準確或不公正的結果。此外，AI在知識生產中的使用越來越廣泛，如果某些行業和人口在自動化轉型中被落下，這可能會導致失業和不平等。

因此，有必要考慮AI的道德問題，並確保其發展和實施遵循透明、負責和包容的原則。通過慎重考慮和負責任的使用，AI有潛力革新知識生產並為所有人帶來更光明的未來。

### 2. 什麼是典範轉移 Paradigm Shift

典範轉移 (Paradigm Shift) 是科學哲學中的一個概念，指的是某個領域的基本框架和觀念發生徹底的轉變，從而引起了該領域的一系列變革。

範式轉移是一種思想上的轉變，從一種思維方式到另一種思維方式的轉變。當某些事物或理論不能解釋或預測新事實或現象時，就會出現範式轉移。這種轉變往往需要突破舊有的思想框架和觀念，並形成新的科學范式和理論體系。

範式轉移通常需要經過一個過程，包括問題的發現、新范式的出現、新范式的建立和廣泛的接受和應用。這種轉變往往需要大量的時間、資源和努力，而且可能會引起爭議和不安。

範式轉移對科學和社會的影響都是深遠的，它可以推動科學的進步和社會的變革。但是，範式轉移也可能會帶來一些風險和挑戰，例如對現有的權威和價值觀的挑戰，以及對人們對現實的看法和信仰的改變。

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. 行為改變循環: [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)
2. 知識革命: [如何善用 AI 加速知識循環](https://blog.androchen.tw/ai-accelerate-knowledge-revolution)
3. 各種場景想像 2022-12-10, 4個月回頭看都感覺像 2 年前的舊聞了: [https://blog.androchen.tw/chatgpt-applied-ai-sci-fi-reflection/](https://blog.androchen.tw/chatgpt-applied-ai-sci-fi-reflection/)

### Murmur

* 2023-03-26: 快要跟不上 GPT 發展速度了 😂
