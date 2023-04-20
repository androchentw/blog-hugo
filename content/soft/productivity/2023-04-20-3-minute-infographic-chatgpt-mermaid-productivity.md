---
title: "3 分鐘打造資訊圖表 - ChatGPT + Mermaid 輕鬆提升生產力"
url: chatgpt-mermaid-3-minute-diagram-productivity
# date: 2023-04-19T22:00:00+08:00
date: 2023-04-20T10:00:00+08:00
author: androchentw
type: post
categories:
  - soft
tags: 
  - aigc
  - chatgpt
  - productivity
  - infographic
  - diagram
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/soft/productivity/2023-04-20-3-minute-infographic-chatgpt-mermaid-productivity-cover.png?raw=true
series: productivity
---

## Overview

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/soft/productivity/2023-04-20-3-minute-infographic-chatgpt-mermaid-productivity-cover.png?raw=true">
<p align="center"><sub><sup>
  3 分鐘打造資訊圖表 - ChatGPT + Mermaid 輕鬆提升生產力
</sup></sub></p>

前一回在 [ChatGPT 實戰 - 3 招加速知識產出](https://blog.androchen.tw/chatgpt-knowledge-production/) 分享了運用 ChatGPT 或其他 AI 來輔助 "**消化資料, 重新詮釋, 社群貼文**" 的 3 個部分。這次來分享我實務中使用的圖表工具與結合方式，希望能幫助到愛用視覺化呈現說明邏輯的朋友。

其實這類 diagram as code 工具出來很久了，只是剛好 ChatGPT 讓這件事情更輕鬆。

今天介紹的工具特色:

1. 🌐 線上網頁即可免費使用
2. 🚀 快速產生流程圖、心智圖、圓餅圖、甘特圖、時間軸、用戶旅程等等圖表
3. 📝 使用 markdown 語法，無工程背景亦可簡單上手，方便版本控制

<!--more-->

## 什麼是 Mermaid

> 基於 JavaScript 的圖表工具，呈現 Markdown 語法，讓使用者能動態創建和修改圖表。

官方直接提供了線上編輯器 [Mermaid Live Editor](https://mermaid.live)。

[Mermaid 官方教學文件](https://mermaid.js.org/syntax/flowchart.html) 有各種語法可以參考。大概可以繪製 15 種圖表，以下分成兩類展示:

一般

### 1. 流程圖 Flowchart

```md
flowchart LR

A[Hard] -->|Text| B(Round)
B --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

{{< mermaid >}}
flowchart LR

A[Hard] -->|Text| B(Round)
B --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
{{< /mermaid >}}

### 2. 時間軸 Timeline

```md
timeline
    title History of Social Media Platform
    2002 : LinkedIn
    2004 : Facebook
         : Google
    2005 : Youtube
    2006 : Twitter
```

{{< mermaid >}}
timeline
    title History of Social Media Platform
    2002 : LinkedIn
    2004 : Facebook
         : Google
    2005 : Youtube
    2006 : Twitter
{{< /mermaid >}}

### 3. 甘特圖 Gantt

```md
gantt
    section Section
    Completed :done,    des1, 2014-01-06,2014-01-08
    Active        :active,  des2, 2014-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
```

{{< mermaid >}}
gantt
    section Section
    Completed :done,    des1, 2014-01-06,2014-01-08
    Active        :active,  des2, 2014-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
{{< /mermaid >}}

### 4. 圓餅圖 Pie chart

```md
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
```

{{< mermaid >}}
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
{{< /mermaid >}}

### 5. 用戶旅程 User Journey

```md
journey
  title My working day
  section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
  section Go home
    Go downstairs: 5: Me
    Sit down: 3: Me
```

{{< mermaid >}}
journey
  title My working day
  section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
  section Go home
    Go downstairs: 5: Me
    Sit down: 3: Me
{{< /mermaid >}}

### 6. 心智圖 Mindmaps

因為我不習慣用網狀展開的 mindmap，所以我自己是使用 [markmap](https://markmap.js.org/repl) 產生 mindmap。

### 其他工程相關

以下就不詳述了，請直接參考[官網教學](https://mermaid.js.org/syntax/flowchart.html):

1. 循序圖 Sequence
2. 類別圖 Class
3. 狀態圖 State
4. 實體關聯性模型圖 ER Diagram
5. 🔥 Git 圖 Gitgraph
6. C4 模型 C4C diagram

## ChatGPT + Mermaid 實際應用

你可能會想說，mermaid markdown 語法看起來還是有點複雜。沒錯！所以才要讓 ChatGPT 來幫助我們產生語法範本。建議挑選 ChatGPT 擅長的任務，像是生成、總結、翻譯等等。

我這邊舉例用 Markmap 的心智圖比較方便，Mermaid 也是依樣畫葫蘆。所以我們就能在 3 分鐘內做到以下事情:

1. 🤖 [ChatGPT](https://chat.openai.com/): 使用 Prompt 產生需要的內容。
2. 📝 [Mermaid Live Editor 線上編輯器](https://mermaid.live/): 直接丟進 mermaid 產生圖表。
3. 🎉 完成！

比如說想要總結這篇文章，Prompt 可以參考這樣下:

```md
# ChatGPT prompt for markdown
provide summary in bullet point and in markdown codeblock:

# ChatGPT prompt for Mermaid
provide summary mermaid diagram in markdown codeblock:
```

拿到以下 markdown

```md
- Overview
- 什麼是 Mermaid
    1. 流程圖 Flowchart
    2. 時間軸 Timeline
    3. 甘特圖 Gantt
    4. 圓餅圖 Pie chart
    5. 用戶旅程 User Journey
    6. 心智圖 Mindmaps
    7. 其他 Others
- ChatGPT + Mermaid 實際應用
- 其他工具
- 你怎麼看?
```

貼到 [markmap](https://markmap.js.org/repl) 產生的心智圖就是本篇的封面圖片了。

Mermaid 版本用流程圖反而比較是我慣用的樣子:

```md
graph LR
    A[概述] --> B[什麼是 Mermaid];
    B --> C[流程圖 Flowchart];
    B --> D[時間軸 Timeline];
    B --> E[甘特圖 Gantt];
    B --> F[圓餅圖 Pie chart];
    B --> G[用戶旅程 User Journey];
    B --> H[心智圖 Mindmaps];
    B --> I[其他 Others];
    A --> J[ChatGPT + Mermaid 實際應用];
    A --> K[其他工具];
    A --> L[你怎麼看?];
```

{{< mermaid >}}
graph LR
    A[概述] --> B[什麼是 Mermaid];
    B --> C[流程圖 Flowchart];
    B --> D[時間軸 Timeline];
    B --> E[甘特圖 Gantt];
    B --> F[圓餅圖 Pie chart];
    B --> G[用戶旅程 User Journey];
    B --> H[心智圖 Mindmaps];
    B --> I[其他 Others];
    A --> J[ChatGPT + Mermaid 實際應用];
    A --> K[其他工具];
    A --> L[你怎麼看?];
{{< /mermaid >}}

順帶一提，不知道為什麼我用 GPT-3.5 產生的 Mermaid 效果比 GPT-4 來得好。有經驗的朋友可以留言分享一下~

## 其他工具

1. [Miro](https://miro.com/): 當我想畫客製化樣式程度再更高一點的方塊圖或其他圖表時，會優先考慮 Miro。我太喜歡大白板了，可以把很多草稿時期的想法跟完成版的擺在一起。
2. [diagrams.net (舊稱 draw.io)](https://app.diagrams.net/): 其實改名叫 diagrams.net 但大家還是習慣叫 Draw.io 的圖表工具。優勢在畫完整的架構圖時，有很多內建元件。但拖拉元件對齊真的很痛苦...。
3. [Excalidraw](https://excalidraw.com/): 手繪風格的圖表工具。用過一段時間就轉移到 Miro 去了。
4. [PlantUML](https://plantuml.com/): 很常拿來跟 mermaid 比的工具。介面比較經典。以前會用，現在很少。
5. VS Code Plugin
   1. [Markdown Preview Mermaid Support](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid)
   2. [Markmap](https://marketplace.visualstudio.com/items?itemName=gera2ld.markmap-vscode)

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [ChatGPT 實戰 - 3 招加速知識產出](https://blog.androchen.tw/chatgpt-knowledge-production/)
2. [AIGC 浪潮翻騰 15 週後的 6 大行為改變](https://blog.androchen.tw/6-behavior-change-after-AIGC-burst-15-weeks)
3. [OpenAI CEO Sam Altman 生產力 4 招解密](https://blog.androchen.tw/openai-ceo-sam-altman-productivity-4-tips)

### Murmur

* 2023-04-22: Everything as Code 信仰 🤣
