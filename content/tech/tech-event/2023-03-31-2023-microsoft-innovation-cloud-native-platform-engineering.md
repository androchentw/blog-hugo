---
draft: true
title: "台灣微軟研討會 - 應用創新起手式 - 打造化繁為簡的雲原生平台"
url: /2023-microsoft-innovation-cloud-native-platform-engineering
# date: 2023-03-31T13:00:00+08:00
date: 2023-03-31T18:30:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - tech-event
  - devops
  - sre
  - aigc
  - chatgpt
share_img: https://res.cloudinary.com/startup-grind/image/upload/c_fill,dpr_2.0,f_auto,g_center,h_1080,q_100,w_1080/v1/gcs/platform-data-goog/events/tiapei-Bevy-EventThumb%402x.png
series: tech-event
---

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-microsoft-innovation-cloud-native-platform-engineering-cover.png?raw=true">
<p align="center"><sub><sup>
  AIGC 浪潮翻騰 15 週後的 6 大行為改變
</sup></sub></p>

## Overview 概述

台灣微軟在微風信義 19F 辦公室，邀請 7 場 session 分享如何打造[企業的數位轉型與應用創新](https://showroom.ithome.com.tw/public/ms0331/index.html)的基礎: 高效率、彈性靈活且安全的雲原生平台，為企業帶來更多**競爭力與生產力提升**。

今天談得多半是 fundamental 的部分，但是也算是一個 overview 了。若你也是 Dev 軟體工程師, 或 IT Ops 相關從業人員，從來沒接觸過類似概念，蠻推薦瞭解這些關鍵字。

🤔 Q: IT 現代化與我們的開發維運團隊有何關聯?

<!--more-->

## Sessions

### 非典型 SRE 為何是企業 IT 現代化新關鍵

<img style="width:80%;" src="https://s4.itho.me/sites/default/files/files/【內文圖表-超連結大圖】封面-1P-豆子-四大技術.png">
<p align="center"><sub><sup>
  iThome - 2022 企業新興技術雷達圖
</sup></sub></p>

> iThome 王宏仁 副總編輯

如同我們先前在 [DevOpsDays Taipei 2022 - 企業 IT 數位轉型投資成長 + 持續交付高品質可用產品](https://blog.androchen.tw/devopsdays-taipei-2022/) 當中彙整的。SRE 自 2021 年起大受矚目。

1. 非典型 SRE => Platform Engineering
2. **平台工程團隊**負責這些與商業創新無關，但又是企業必要的**非功能性需求**
3. [CNCF Platforms White Paper](https://appdelivery.cncf.io/whitepapers/platforms/) - 平台的屬性 Attributes of platforms
   1. 平台作為產品 Platform as a product
   2. 使用者體驗 User experience
   3. 文件和引導 Documentation and onboarding
   4. 自助式 Self-service
   5. 減輕使用者的認知負載 Reduced cognitive load for users
   6. 可選和可組合 Optional and composable
   7. 默認安全性 Secure by default
4. 可以關注 [PlatformCon 2023](https://platformcon.com/), 過去的 [PlatformCon 2022](https://2022.platformcon.com/) 也有精彩內容
   1. [The Magic of Platforms • Gregor Hohpe • PlatformCon 2022](https://www.youtube.com/watch?v=WaL3ZbLgMuI)
   2. [PlatformCon 2022 recap, from a public PaaS PoV](https://www.artifakt.com/blog/paas/platformcon-2022-recap/)
5. iThome
   1. [【iThome 2022 CIO大調查(中)｜新興技術熱門趨勢】大數據分析和混合雲架構成主流，更有6大新興技術爆紅](https://www.ithome.com.tw/article/152583)
   2. [【2023年CIO必看10大趨勢：趨勢3】數位轉型帶動維運現代化需求，平臺工程開始崛起](https://www.ithome.com.tw/news/155033)

### 雲原生將走向何方？

> 台灣微軟客戶成功事業群 副總經理 張書源

1. DevOps/Automation is mandatory (infrastructure/code/environment)
2. [網站可靠性工程(SRE) 簡介- Training - Microsoft Learn](https://learn.microsoft.com/zh-tw/training/modules/intro-to-site-reliability-engineering/)
3. [CNCF Cloud Native Definition v1.0](https://github.com/cncf/toc/blob/main/DEFINITION.md)

> Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, microservices, immutable infrastructure, and declarative APIs exemplify this approach.
>
> These techniques enable loosely coupled systems that are resilient, manageable, and observable. Combined with robust automation, they allow engineers to make high-impact changes frequently and predictably with minimal toil.
>
> The Cloud Native Computing Foundation seeks to drive adoption of this paradigm by fostering and sustaining an ecosystem of open source, vendor-neutral projects. We democratize state-of-the-art patterns to make these innovations accessible for everyone.

### 開發安全維運一體化

> 台灣微軟資深雲端解決方案 架構師 邱英瑞

1. [GitHub Advanced Security](https://github.com/advanced-security)
2. 我個人也蠻推薦 Google 開源的 [osv-scanner](https://github.com/google/osv-scanner)
3. 如何定義 **階段性目標**? 何謂做完? Priority? 使用如 DSOMM 成熟度模型? => 使用即可
4. [Microsoft Defender for Cloud](https://learn.microsoft.com/zh-tw/azure/defender-for-cloud/defender-for-cloud-introduction) 整合 Dashboard, 拼上最後一塊拼圖。Sec team 可以直接在此看完整儀表版進行管理。

### 可觀測性 (Observability) 鏈路追蹤的實踐

> MAYO 鼎恒數位科技總監 董淳吉 Marcus Tung

1. DevOpsDay Taipei 2022 共筆: [可觀測性 (Observability) 的實踐](https://hackmd.io/6A1z7CHrTrOlHjVdti_ywQ)

### GitHub Copilot 與 Visual Studio Code 實戰解析

> 多奇數位創意有限公司 技術總監 黃保翕 (Will 保哥)

1. 追蹤[保哥的 facebook](https://www.facebook.com/will.fans) 就可以知道最新資訊啦!
2. 重點: 如果你寫的 Code 讓 GitHub Copilot 看不懂的話, 先自我檢討!

### 如何運用 ChatGPT 徹底解放 SRE

> twMVC 劉書傳 Roberson Liou

1. 場景
   1. Automation
   2. Scripting
   3. Troubleshooting
2. Incident Report: 時間軸 + 事件描述 + 影響範圍 + 改善計畫
3. 透過 Pair 快速迭代
4. Text > Mermaid Diagram > Terraform

### SRE 客戶實戰分享

> 趨勢科技 SRE 高級經理 羊輝

1. Why SRE?
   1. Global Regions, Reliability Challenges
   2. New features velocity vs. reliability
   3. Servces vs. # of Operators
   4. Full Observability: microservices vs. monolithic product
2. SLO/SLI/Error Budget: 在 Design/Architecture 上進行優化, prevent risk
3. Full Observability based on trace data
4. How to Roll Out Tracing - [The Future of Observability with OpenTelemetry](https://www.oreilly.com/library/view/the-future-of/9781098118433/)

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [Agile Summit 2022 敏捷高峰盛會 - VUCA 時代敏捷導入 + 持續交付價值](https://blog.androchen.tw/agile-summit-2022/)
2. [DevOpsDays Taipei 2022 - 企業 IT 數位轉型投資成長 + 持續交付高品質可用產品](https://blog.androchen.tw/devopsdays-taipei-2022/)
3. [2022 TSMC IT Day - 看台積電 CIO 如何以矽谷軟體公司思維打造 IT 數位轉型之路](https://blog.androchen.tw/2022-tsmc-it-day/)

```text
#應用創新 #平台工程 #雲原生 #Microsoft #ChatGPT #DevOps #DevSecOps #SRE #Observability #CloudNative #IT #GitHub #Copilot
```

### Murmur

* 2023-03-31: DevOps / SRE / Platform Engineering 一家親
