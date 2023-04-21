---
draft: true
title: "SRE Conference 2023 - 11 場議程解密企業實踐與方法論"
url: sre-conference-2023
# date: 2023-04-21T09:00:00+08:00
date: 2023-04-21T11:30:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - tech-event
  - devops
  - sre
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-04-21-sre-conference-2023-cover.jpg?raw=true
series: tech-event
---

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-04-21-sre-conference-2023-cover.jpg?raw=true">
<p align="center"><sub><sup>
  SRE Conference 2023 - 富邦國際會議中心
</sup></sub></p>

## Overview 概述

04-21(五) SRE Conference 2023 在富邦國際會議中心，邀請 11 位企業專家，來自台灣微軟、國泰世華銀行、台積電等，分享 **SRE 方法論、實踐作法**，為企業帶來更多**競爭力與生產力提升**。

素材

1. [議程表](https://sre.ithome.com.tw/2023/agenda)
2. [HackMD 共筆](https://r.itho.me/SRE23note) => 希望看到議程細節的朋友，共筆裡都很完整的筆記。我這篇文章會提更多我自己額外的發想。

🤔 Q: 你想瞭解哪一場 SRE 議程？公司團隊碰到了什麼挑戰？

💪 A: 提問分享 2 個你有興趣的題目

<!--more-->

## Agenda

1. [台灣微軟] SRE. This is the way
2. [國泰世華銀行] 國泰如何進行金融 SRE 的發展
3. [XREX] 從單體到容器化的導入之路
4. [Shopback] How to survive in the 1111
5. [卡洛地] 從 AI 到 AIOps 再到 SRE
6. [國泰金控] 金融業雲端 API 管理轉型實戰經驗
7. [聯齊科技] 做 SRE 還是要靠通靈？讓我們看見看不到的東西
8. [KKCompany] 從 SRE 與非 SRE 視角，探討大型長期專案如何面對與評估技術轉折
9. [兆勤科技] 在設備跟雲的融合之路上孵化 SRE 的旅程
10. [台積電] SRE 經驗分享 - 從事故分析、精準監控到自動化維運

## 💡 總結反思

因為內容實在太多了，先總結在此。

* 每一個議程主題都有「主題重點」與「💡 反思」


## 1. [iThome] 平臺工程為何是企業 IT 現代化新關鍵

<img style="width:80%;" src="https://s4.itho.me/sites/default/files/files/【內文圖表-超連結大圖】封面-1P-豆子-四大技術.png">
<p align="center"><sub><sup>
  iThome - 2022 企業新興技術雷達圖
</sup></sub></p>

> iThome 王宏仁 副總編輯
>
> 原議程: "From Zero to SRE（街口 SRE 從零做起）" 講者確診，之後會再舉辦線上 talk

如同我們先前在 [DevOpsDays Taipei 2022 - 企業 IT 數位轉型投資成長 + 持續交付高品質可用產品](https://blog.androchen.tw/devopsdays-taipei-2022/) 當中彙整的。SRE 自 2021 年起大受矚目。

1. 非典型 SRE => Platform Engineering
2. **平台工程團隊**負責這些與商業創新無關，但又是企業必要的**非功能性需求**。
3. [CNCF Platforms White Paper](https://appdelivery.cncf.io/whitepapers/platforms/) - 平台的屬性 Attributes of platforms
   1. **平台作為產品 Platform as a product**
   2. **使用者體驗 User experience**
   3. 文件和引導 Documentation and onboarding
   4. 自助式 Self-service
   5. **減輕使用者的認知負載 Reduced cognitive load for users**
   6. 可選和可組合 Optional and composable
   7. 默認安全性 Secure by default
4. Case study: [Zalando Tech Radar 技術雷達圖](https://opensource.zalando.com/tech-radar/)
5. 可以關注 [PlatformCon 2023](https://platformcon.com/), 過去的 [PlatformCon 2022](https://2022.platformcon.com/) 也有精彩內容
   1. [The Magic of Platforms • Gregor Hohpe • PlatformCon 2022](https://www.youtube.com/watch?v=WaL3ZbLgMuI)
   2. [PlatformCon 2022 recap, from a public PaaS PoV](https://www.artifakt.com/blog/paas/platformcon-2022-recap/)
6. iThome
   1. [【iThome 2022 CIO大調查(中)｜新興技術熱門趨勢】大數據分析和混合雲架構成主流，更有6大新興技術爆紅](https://www.ithome.com.tw/article/152583)
   2. [【2023年CIO必看10大趨勢：趨勢3】數位轉型帶動維運現代化需求，平臺工程開始崛起](https://www.ithome.com.tw/news/155033)

## 2. [台灣微軟] SRE. This is the way

> Frank Chen / 台灣微軟 資深雲端架構師

<img style="width:80%;" src="https://i.imgur.com/nUBe3e2.png">
<p align="center"><sub><sup>
  DevOps vs. SRE vs. Plaform Engineering
</sup></sub></p>

* [DevOps vs. SRE vs. Plaform Engineering](https://blog.bytebytego.com/i/110521562/devops-vs-sre-vs-platform-engineering-what-is-the-difference)

### SRE 關鍵概念

1. SLI/SLO: 定義服務目標
2. Error Budget: 透過錯誤預算的概念，平衡開發維運速度
3. Blameless postmortems: 對事不對人的事後報告
4. Eliminating toil: 減少瑣碎的維運操作
5. More like an evangelist: 與其說是個工作，更多會是像個傳教士

### 主題重點

* **如何開始 How to Get Started**: Start from small, make influence
* **如何持續 Plan for Continuity**: Identify orgranization type
  1. No "Best" type
  2. Identify stakeholders
  3. Shared Responsibility

> 你需要 SRE 的時候，通常是因為客戶在抱怨 (內部 / 外部)
>
> => **需要救火**
>
> => 需要建立信任 (Build trust)

### 作法

* **調整流程 Actionable alert**: SOP (symptom and mitigation) + post-mortem followup。
* [DevOps Topologies](https://web.devopstopologies.com/): 辨識你的組織運作架構，並選擇更適合的**合作模式**。
* 給予不同角色，不同的**視覺化呈現**: Data Visbility, Permission Design, Communication tools。
* **Connect to Business**: 將 SRE 與 Business Value / SLA / Cost 掛勾，才會讓 stakeholders 有感。
* **Communication channel**: 將溝通橋樑建立起來，串聯 Data source, Data Platform, Consumption。

### 反思

[ ] 💡: 如何在企業內部的 Data Platform，建立完整的 observability 與 reliability 標準流程機制，有效率地確保 business value 能夠持續地被交付?
[ ] 💡: 在推廣 SRE 作法時，如何與 Business Value / SLA / Cost 掛勾，讓 stakeholders 有感?
[ ] 💡: SRE, Dev, Ops 團隊在合作時，如何將溝通橋樑建立起來，串聯 Data source, Data Platform, Consumption?

## 3. [國泰世華銀行] 國泰如何進行金融 SRE 的發展

> 鄭正略 (Louis) / 國泰世華銀行 協理 中台發展部

### 開場

* SRE 最重要的是經驗的分享，以及如何傳承下去。
* 國泰 Day 1 就是從微服務開始，所以就有內建 SRE 與 DevSecOps 的概念。
* 銀行的技術債非常可觀，難度也會更高: 資訊處 700 多人 + 數位發展部 700 多人 = 1500 人

### 演講主題

1. Why: 金融為何要 SRE
2. How: 現代化監控中心發展路線圖
3. What: 銀行(金融) SRE 的運作方式

### 目標效益

1. 強化營運維穩，首要監控
2. 提升應變速度
3. 降低間接影響
4. 優化協作監控

### 監控體系建設的階段 (金字塔)

1. 基礎營運: 專業監控覆蓋率 -> 100%
2. 集中運營: 事件即時響應 -> 100%
3. 監控運營: 監控有效率 -> 100%
4. 根因定位: 故障定位時間 -> 0
5. 協同停損: MTTR（平均故障恢復時間）-> 0
6. 故障規避: MTBF (平均故障間隔時間) -> infinity

* 裝 agent 會影響 service performance, 務必考量。
* 國泰的 practice
  * zabbix 全方位監控
  * 目前是以一個 pod 0.5 ~ 1 core 來做水平擴展, 所以會有影響
  * Mindset: 發生問題，去釐清，期望不要再次發生
* 解放 AP (application 開發) 人力是痛點，降下維運 loading。

### IT 維運自動化: 現代化監控中心的分類

1. DEM: 數位體驗監控
2. NPMD: 網路性能監控
3. ITIM: IT 基礎設施監控
4. APM: 應用性能監控

### IT運營組織的管理成熟度: IT 導向 > 業務導向

### 執行面向

1. 人文的改變
2. 流程優化
3. 技術發展

### SRE 團隊 R&R

國泰目前 SRE 團隊總共人數: 38 人

1. Ops
   1. Dev SRE (6 + N)
   2. Infra SRE (6 + N)
   3. Cloud SRE (3 + N)
   4. Bussiness SRE (3 + N)
2. DevSecOps Arch. (3 + N)

並發展學習體系發展策略，有專業的戰鬥營課程規劃。

技術 Technology
思維 Mindset
企業文化 Culture

### 反思

[ ] 💡:

## 4. [XREX] 從單體到容器化的導入之路

> 李太毓 (Danny) / XREX SRE

### 主題重點

### 反思

[ ] 💡:

## 5. [Shopback] How to survive in the 1111

> 陳道陞 (Tao-Sheng) / ShopBack VP of Engineering

### 主題重點

### 反思

[ ] 💡:

## 6. [卡洛地] 從 AI 到 AIOps 再到 SRE

> 蘇國鈞 / 卡洛地 技術總監

### 主題重點

### 反思

[ ] 💡:

## 7. [國泰金控] 金融業雲端 API 管理轉型實戰經驗

> 林家慶 (Kai) / 國泰金控 SRE Engineer

### 主題重點

### 反思

[ ] 💡:

## 8. [聯齊科技] 做 SRE 還是要靠通靈？讓我們看見看不到的東西

> 曾光毅 (光光) / 聯齊科技 SRE

### 主題重點

### 反思

[ ] 💡:

## 9. [KKCompany] 從 SRE 與非 SRE 視角，探討大型長期專案如何面對與評估技術轉折

> 許榮倫 (Minimum) / KKCompany Technologies Senior Engineer

### 主題重點

### 反思

[ ] 💡:

## 10. [兆勤科技] 在設備跟雲的融合之路上孵化 SRE 的旅程

> 吳俊德 (Julian) / 兆勤科技 智慧雲中心 協理

### 主題重點

### 反思

[ ] 💡:

## 11. [台積電] SRE 經驗分享 - 從事故分析、精準監控到自動化維運

> 謝政廷 (Duran) / 台積電 Principal Site Reliability Engineer

### 主題重點

### 反思

[ ] 💡:

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [Agile Summit 2022 敏捷高峰盛會 - VUCA 時代敏捷導入 + 持續交付價值](https://blog.androchen.tw/agile-summit-2022/)
2. [DevOpsDays Taipei 2022 - 企業 IT 數位轉型投資成長 + 持續交付高品質可用產品](https://blog.androchen.tw/devopsdays-taipei-2022/)
3. [2022 TSMC IT Day - 看台積電 CIO 如何以矽谷軟體公司思維打造 IT 數位轉型之路](https://blog.androchen.tw/2022-tsmc-it-day/)

```text
#平台工程 #DevOps #SRE #IT
#ChatGPT #GitHub #Copilot
```

### Murmur

* 2023-04-21: 真的是很喜歡參加 conference 多看看大家的分享 🥳 每次都很多靈感。有些人會說「出來講的都包裝得很好，公司裡面是不是這樣很難說」，但我總是想「至少這些講者願意出來分享，而且公司也支持，這就是**文化上的決定性差異**」。每個單位絕對都會有自己的議題需要處理，但重要的應該是**我們選擇如何看待這個問題，並敏捷地持續改善**。