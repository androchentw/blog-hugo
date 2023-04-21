---
draft: true
title: "SRE Conference 2023 - 11 場議程解密企業 SRE 實踐 + 方法論"
url: sre-conference-2023
# date: 2023-04-21T09:00:00+08:00
date: 2023-04-21T11:30:00+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - tech-event
  - sre
  - devops
  - platform-engineering
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-04-21-sre-conference-2023-1-cover.jpg?raw=true
series: tech-event
---

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-04-21-sre-conference-2023-1-cover.jpg?raw=true">
<p align="center"><sub><sup>
  SRE Conference 2023 - 富邦國際會議中心
</sup></sub></p>

## Overview 概述

04-21(五) SRE Conference 2023 在富邦國際會議中心，邀請 11 位來自 **iThome、台灣微軟、國泰世華銀行、台積電**等企業專家，分享 **SRE 方法論、實踐作法**，為企業帶來更多**競爭力與生產力提升**。

今年這一場研討會的 [HackMD 共筆](https://r.itho.me/SRE23note) 非常精彩，想看議程細節的朋友，裡面有很完整的筆記。我這篇文章會提更多我自己額外的發想。

🤔 Q: 你想瞭解哪一場 SRE 議程？公司團隊碰到了什麼挑戰？

💪 A: 提問 + 分享 2 個你有興趣的題目，並思考如何應用於自己的團隊。

<!--more-->

## Agenda

[官網議程表](https://sre.ithome.com.tw/2023/agenda)有完整簡介，也可以直接參考下方我的整理，快速瀏覽有興趣的公司與題目 (🥇 是我個人推薦的)

1. 🥇 [iThome] 平臺工程為何是企業 IT 現代化新關鍵
2. 🥇 [台灣微軟] SRE. This is the way
3. 🥇 [國泰世華銀行] 國泰如何進行金融 SRE 的發展
4. [XREX] 從單體到容器化的導入之路
5. [Shopback] How to survive in the 1111
6. [卡洛地] 從 AI 到 AIOps 再到 SRE
7. [國泰金控] 金融業雲端 API 管理轉型實戰經驗
8. [聯齊科技] 做 SRE 還是要靠通靈？讓我們看見看不到的東西
9. [KKCompany] 從 SRE 與非 SRE 視角，探討大型長期專案如何面對與評估技術轉折
10. [兆勤科技] 在設備跟雲的融合之路上孵化 SRE 的旅程
11. 🥇 [台積電] SRE 經驗分享 - 從事故分析、精準監控到自動化維運

## 💡 總結反思

因為內容實在太多了，先總結 12 個重點在此。底下還有更多精彩內容。

每一個議程主題幾乎都有「主題重點」與「**💡 反思**」，邀請你也一起深思。

1. 需要 SRE 的時候，通常是因為客戶在抱怨 (內部 / 外部)。也就是 **需要救火，需要建立信任**。
2. 企業內部要推動 SRE，要從　**業務切入**，技術只是輔助。將 SRE 與 Business Value / SLA / Cost 掛勾，才會讓 stakeholders 有感。
3. 從「**回答 SRE 帶來什麼目標商業效益**」的角度出發定義 SLA。
4. **平台工程的產品思維** 至關重要。
5. 「**文化，技術，流程**」缺一不可。
6. 建立 **溝通協作** 橋樑，串聯 Data source, Data Platform, Consumption。
7. 運用 [DevOps Topologies](https://web.devopstopologies.com/): 辨識你的組織運作架構，並選擇更適合的**合作模式**。
8. 具體作法幾乎都圍繞在 「**監控 + 事故分析 + 自動化維運**」。
9. 監控指標並非一成不變，需要不斷檢視與**敏捷地持續改善**。
10. **Actionable Alert** 告警信必須搭配 後續處理 SOP (症狀 + 緩解)。
11. 沒有銀子彈。
12. 重新定義 SRE = Service Restart Engineer 🤣

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-04-21-sre-conference-2023-2-lunch.jpg?raw=true">
<p align="center"><sub><sup>
  每次最期待的議程 - 便當 (並不是 😆)
</sup></sub></p>

## 1. 🥇 [iThome] 平臺工程為何是企業 IT 現代化新關鍵

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

### [CNCF Platforms White Paper](https://appdelivery.cncf.io/whitepapers/platforms/) - 平台的屬性 Attributes of platforms

1. **平台作為產品 Platform as a product**
2. **使用者體驗 User experience**
3. 文件和引導 Documentation and onboarding
4. 自助式 Self-service
5. **減輕使用者的認知負載 Reduced cognitive load for users**
6. 可選和可組合 Optional and composable
7. 默認安全性 Secure by default

### Case Study - Zalando

<img style="width:80%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-04-21-sre-conference-2023-3-zalando-tech-radar.png?raw=true">
<p align="center"><sub><sup>
  <a href="https://opensource.zalando.com/tech-radar/" target="_blank">Zalando Tech Radar 技術雷達圖</a>
</sup></sub></p>

### PlatformCon

1. 可以關注 [PlatformCon 2023](https://platformcon.com/)
2. 過去的 [PlatformCon 2022](https://2022.platformcon.com/) 也有精彩內容
3. [PlatformCon 2022 recap, from a public PaaS PoV](https://www.artifakt.com/blog/paas/platformcon-2022-recap/)

{{< youtube "WaL3ZbLgMuI" >}}

### iThome 文章

1. [【iThome 2022 CIO大調查(中)｜新興技術熱門趨勢】大數據分析和混合雲架構成主流，更有6大新興技術爆紅](https://www.ithome.com.tw/article/152583)
2. [【2023年CIO必看10大趨勢：趨勢3】數位轉型帶動維運現代化需求，平臺工程開始崛起](https://www.ithome.com.tw/news/155033)

## 2. 🥇 [台灣微軟] SRE. This is the way

> Frank Chen / 台灣微軟 資深雲端架構師

<img style="width:60%;" src="https://i.imgur.com/nUBe3e2.png">
<p align="center"><sub><sup>
  <a href="https://blog.bytebytego.com/i/110521562/devops-vs-sre-vs-platform-engineering-what-is-the-difference" target="_blank">DevOps vs. SRE vs. Platform Engineering</a>
</sup></sub></p>

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

### SRE 關鍵概念

1. SLI/SLO: 定義服務目標
2. Error Budget: 透過錯誤預算的概念，平衡開發維運速度
3. Blameless postmortems: 對事不對人的事後報告
4. Eliminating toil: 減少瑣碎的維運操作
5. More like an evangelist: 與其說是個工作，更多會是像個傳教士

### 作法

* **調整流程 Actionable alert**: SOP (symptom and mitigation) + post-mortem followup。
* [DevOps Topologies](https://web.devopstopologies.com/): 辨識你的組織運作架構，並選擇更適合的**合作模式**。
* 給予不同角色，不同的**視覺化呈現**: Data Visbility, Permission Design, Communication tools。
* **Connect to Business**: 將 SRE 與 Business Value / SLA / Cost 掛勾，才會讓 stakeholders 有感。
* **Communication channel**: 將溝通橋樑建立起來，串聯 Data source, Data Platform, Consumption。

<img style="width:60%;" src="https://web.devopstopologies.com/images/type-7.png">
<p align="center"><sub><sup>
  <a href="https://blog.bytebytego.com/i/110521562/devops-vs-sre-vs-platform-engineering-what-is-the-difference" target="_blank">DevOps Topologies</a>: 辨識你的組織運作架構，並選擇更適合的合作模式
</sup></sub></p>

### 💡 反思

1. [x]: 如何在企業內部的 Data Platform，建立完整的 observability 與 reliability 標準流程機制，有效率地確保 business value 能夠持續地被交付?
2. [x]: 在推廣 SRE 作法時，如何與 Business Value / SLA / Cost 掛勾，讓 stakeholders 有感?
3. [x]: SRE, Dev, Ops 團隊在合作時，如何將溝通橋樑建立起來，串聯 Data source, Data Platform, Consumption?

## 3. 🥇 [國泰世華銀行] 國泰如何進行金融 SRE 的發展

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

### 其他

* 裝 agent 會影響 service performance, 務必考量。
* Mindset: 發生問題，去釐清，期望不要再次發生
* 解放 AP (application 開發) 人力是痛點，降下維運 loading。

### IT 維運自動化: 現代化監控中心的分類

1. DEM: 數位體驗監控
2. NPMD: 網路性能監控
3. ITIM: IT 基礎設施監控
4. APM: 應用性能監控

### IT 運營組織的管理成熟度: IT 導向 > 業務導向

### 執行面向

1. 人文的改變
2. 流程優化
3. 技術發展

### SRE 團隊 R&R

國泰目前 SRE 團隊總共人數: 38 人，多為兼職。

1. Ops
   1. Dev SRE (6 + N)
   2. Infra SRE (6 + N)
   3. Cloud SRE (3 + N)
   4. Bussiness SRE (3 + N)
2. DevSecOps Arch. (3 + N)

### 發展學習體系發展策略，有專業的戰鬥營課程規劃

1. 技術 Technology
2. 思維 Mindset
3. 企業文化 Culture

### 💡 反思

1. [x]: 技術 + 思維 + 企業文化 如何持續推廣，改變工作流程？
2. [x]: 中台定位與其他業務單位的合作模式，人數編制?

## 4. [XREX] 從單體到容器化的導入之路

> 李太毓 (Danny) / XREX SRE

雖然有點不好意思，這場我在跟前一場的講者對談，沒有聽到 😂 可以直接參考[共筆](https://hackmd.io/@sre-conf/2023/%2FnvQwpiNiQbe5IuaztiZCcg)。講比較多技術 know-how。

題外話，其實我自己覺得參加 conference 最好玩也最充實的，就是跟講者去互動，帶著平時工作中，團隊遇到的狀況去交流。真的是會獲得非常多，也推薦給大家，多多跟分享的人互動！ 🎉

## 5. [Shopback] How to survive in the 1111

> 陳道陞 (Tao-Sheng) / ShopBack VP of Engineering

### 主題重點

* Engineer 數量 ~= 200 人。
* **Preparation for unknown traffic**: 對於電子商務來說，最挑戰的就是如何去提前準備不預期的流量。

### Key Element 關鍵要素

* Estimation for the worst/best?
* Money talks but can't buy everything
* Alignment with Business(know the traffic behavior)
  * 業務成長是好事，但需要技術去支援。
  * 即便有 Auto-Scale 機制，仍然是落後指標。
  * 行銷活動 或是 YouTuber 帶來突如其來的流量，若造成 service slow response，對於 SRE 來說會是一件很嚴重的事情。

### 壓力測試

* 在測試環境，一來是貴，二來是無法完全模擬。
* 所以實務上還是會在 production 非主要流量時間 (比如凌晨 4 點)，進行壓力測試。

### 事前規劃

* D-Day plan: 一定會發生的事件 (1111, 聖誕節)。
  * 1111 是平日的 45 倍流量
  * worst case plan
  * on-duty schedule: process, leadership
* Technically readiness
* No silver bullet。仍然需要從業務角度去選擇適當的解決方案。
* Retrospective: review + improve

### 💡 反思

1. [x]: 我們在意 service slow response 嗎? 有對應的 SLA 嗎? 我們的技術架構是否足夠支持業務成長？

## 6. [卡洛地] 從 AI 到 AIOps 再到 SRE

> 蘇國鈞 / 卡洛地 技術總監

### 主題重點

* 用來做 Disaster recovery, Anomaly detection, Billing Data
* Deep Learning Model: Univariate / Multivariate Time-Series Data

### 小記

這場的[共筆](https://hackmd.io/@sre-conf/2023/%2FsJ3lAYokSdGOgwYtWkcjTw)很精彩，真不愧是 SRE confenrece 的與會者 ~~鄉民~~ 😆

過程中因為簡報投影中斷，超過 30 秒沒有畫面，然後就有了以下的討論:

> * 論簡報投影不出來之SLA為多少？
>   * 投影機：95%
>   * 轉接頭：90%
> * 投影機廠商不用負責嗎
> * 每一場議程允許 x 秒投影中斷?
> * 沒有HA嗎？？

### 💡 反思

1. [x]: 如何用新技術來協助既有日常工作流程？ 你會時常關注新技術如何提升生產力嗎？

## 7. [國泰金控] 金融業雲端 API 管理轉型實戰經驗

> 林家慶 (Kai) / 國泰金控 SRE Engineer

### 主題重點

1. API Application Strategies
2. API Management System
3. APIM Architecture Evolution
4. APIM Problem-Solving
5. APIM Future Enhancement

### Security and Governance

1. Threat Protection
2. Access Controls
3. Self Service and SSO
4. Security Governance (法規性上的要求，像是金融法規 or GDPR)
5. Data Security

### Cathay Finance Group APIM Structure

1. Open banking
2. Integration
3. Portal
4. Monitoring

### 其他

* 採用 Google Cloud Anthos
* 法規關係，所以 API 維持在地端，採用混合雲的架構。業務在地端，log拋雲端，方便追蹤和管控。
* 消費性金融，在法規上要避免資料流到海外，所以要有地端資料庫。
* 若有大檔上傳，中間擴充功能會先把檔案傳到雲端空間 (cloud storage or S3)，再把 URL 放進 request 來完成。
* TLS certificates 更新時需要特別注意。

### 💡 反思

1. [x]: 如何在企業內部創造 API 經濟，推廣 API-first 思維?

<img style="width:50%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-04-21-sre-conference-2023-4-afternoon-tea.jpg?raw=true">
<p align="center"><sub><sup>
  下午茶
</sup></sub></p>

## 8. [聯齊科技] 做 SRE 還是要靠通靈？讓我們看見看不到的東西

> 曾光毅 (光光) / 聯齊科技 SRE

### 主題重點

* Prometheus Exporter 介紹 + Elasticsearch
* 重新定義 SRE = Server Reboot/Restart Engineer 😂

### 💡 反思

1. [x]: 你使用過 prometheus 時會搭配什麼管理工具呢 (ELK, Grafana)?

## 9. [KKCompany] 從 SRE 與非 SRE 視角，探討大型長期專案如何面對與評估技術轉折

> 許榮倫 (Minimum) / KKCompany Technologies Senior Engineer

### 主題重點

IaC - Terraform

* KKCompany 使用 Terraform
* 模組化 & 再利用
* 線上透過介面調整系統組態，並同步更新回 Terraform
* 權限管理 與 基礎設施管理分開

### 筆記

[共筆聊天區](https://hackmd.io/@sre-conf/2023/%2FMG_WfuPPQwuiuvc4N7iUVw)剛好有人在討論，Golang 這個語言是否推薦學習，會不會很快又沒有人使用了？

有感而發，回覆了以下內容：

> 可以從幾個面向去觀察一個語言的社群大小/會存活多久，但這些都不是絕對，想學都還是可以去學，多少都會有收穫
>
> 1. GitHub repository 數量 & 星星數
> 2. Stackoverflow 年度調查
> 3. Google Trend 關鍵字
> 4. 各大公司開的職缺

<img style="width:40%;" src="https://i.imgur.com/EmTsa15.png">
<p align="center"><sub><sup>
  PHP is dead? 程式語言存活戰
</sup></sub></p>

### 💡 反思

1. [x]: 評估大型專案技術轉折時, 有哪些面向需要考慮?

## 10. [兆勤科技] 在設備跟雲的融合之路上孵化 SRE 的旅程

> 吳俊德 (Julian) / 兆勤科技 智慧雲中心 協理

### 主題重點

結論 = 文化很重要

* 敏捷 (開發): Agile Team 包含 PM、RD（FW & Cloud）、QA 跟 SRE
* 合作跟溝通
  * 降低整體（Ent-to-End）的複雜度，盡量做 Parameterization
  * 架構出合理的守備範圍（e.g. 雲/設備、測試/研發、資安 etc）
* 自動化: 程式部署, 異常事件通知
* 監控: SLO metrics, Outage, Business Insight

### 💡 反思

1. [x]: 如何在你的企業文化與日常工作流程中，導入 SRE?

## 11. 🥇 [台積電] SRE 經驗分享 - 從事故分析、精準監控到自動化維運

> 謝政廷 (Duran) / 台積電 Principal Site Reliability Engineer

### 主題重點

1. 事故分析
2. 監控指標
3. 自動化維運

### 事故三種類型與效益

1. 使用者報案: 有可能代表監控不夠
2. 監控與警告: 稍微成熟的產品，已經可以在user發現前就收到通知
3. 團隊預先察覺: 成熟的監控與警告機制才有較高的機率預先察覺事故發生

### 檢討報告 (Postmortem)

1. 日期資訊, 時間軸
2. 採取作為
3. 執行摘要
4. 問題摘要
5. 從中學習

### 後續檢討工作

1. 建立標準解決流程
2. 檢視事故回應與監控指標
3. 主動測試
4. 案例分享

### 鼓勵經營社群方式

* 讀書會
* SRE 工作群組或會議
* 建立 V-Team

### 不咎責文化: 其實有點難

1. 高層支持
2. 鼓勵面對錯誤
3. 建設性批評
4. 確保流程改善

### 監控的 4 個黃金信號

[Google SRE - The Four Golden Signals](https://sre.google/sre-book/monitoring-distributed-systems/#xref_monitoring_golden-signals)

1. 不要全部放進來，避免雜訊
2. 正確的監控指標必須經過長時間觀察與測試: 監控指標需要持續更新

### 目標明確的指標

1. 說明指標含義
2. 數值異常時可能的影響或事故
3. 保留實用的指標

### 自動化維運目的與前提

1. 維運資料標準化
2. CI/CD流程標準化
3. 使用一致的工具
4. 消除無效率的操作與管理
5. 減少人為錯誤發生
6. 有效降低成本
7. 減少聯繫與等待時間

### 自動化維運

1. 減少瑣事
2. 使用正確的工具
3. 識別高價值流程
4. 檢視團隊技能

小筆記

1. 注意到講者用的 Powerpoint template 是 [Jafar Designs](https://www.behance.net/jafardesigns) 😆
2. 這場本來更想聽 TSMC 內部作法，但今天比較多講書上的內容，雖然充實但有點可惜！

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2023-04-21-sre-conference-2023-5-reception.jpg?raw=true">
<p align="center"><sub><sup>
  SRE Conference 2023 - 富邦國際會議中心
</sup></sub></p>

### 💡 反思

1. [x]: 你在推行 SRE 時，是如何安排「事故分析、精準監控、自動化維運」的持續優化？

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [2022 TSMC IT Day - 看台積電 CIO 如何以矽谷軟體公司思維打造 IT 數位轉型之路](https://blog.androchen.tw/2022-tsmc-it-day/)
2. [DevOpsDays Taipei 2022 - 企業 IT 數位轉型投資成長 + 持續交付高品質可用產品](https://blog.androchen.tw/devopsdays-taipei-2022/)
3. [Agile Summit 2022 敏捷高峰盛會 - VUCA 時代敏捷導入 + 持續交付價值](https://blog.androchen.tw/agile-summit-2022/)
4. [來點 SRE - 從 ChatGPT 停機公告，學維運事後剖析](https://blog.androchen.tw/chatgpt-sre-postmortem/)

```text
#SRE #DevOps #PlatformEngineering #IT
```

### Murmur

* 2023-04-21: 真的是很喜歡參加 conference 多看看大家的分享 🥳 每次都很多靈感。有些人會說「出來講的都包裝得很好，公司裡面是不是這樣很難說」，但我總是想「至少這些講者願意出來分享，而且公司也支持，這就是**文化上的決定性差異**」。每個單位絕對都會有自己的議題需要處理，但重要的應該是**我們選擇如何看待這個問題，並敏捷地持續改善**。
