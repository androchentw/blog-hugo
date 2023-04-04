---
title: "GDG DevFest 2022 Taipei 社群志工與議程心得"
url: /gdg-devfest-2022-taipei
# date: 2022-12-03T07:28:16+08:00
date: 2022-12-04T16:34:16+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - tech-event
  - devops
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2022-12-03-gdg-devfest-2022-taipei-cover.webp?raw=true
series: tech-event
---

<img style="width:40%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/tech/tech-event/2022-12-03-gdg-devfest-2022-taipei-cover.webp?raw=true">

## Overview 概述

2022-11-19 起心動念: 一直都想參與社群, 終於在 11-16 在萬豪酒店的 ☁️ [Google Cloud Next Recap](https://cloudonair.withgoogle.com/events/next-recap-taiwan-2022) 的時候去找 GDG 攤位聊天，然後就主動報名參加志工了 😂 於是開啟了一段奇幻旅程...

🦄 [GDG DevFest 2022 Taipei] 是由一群使用 Google 技術的開發者所推動的全球盛會, 在 12/3 週六於台大舉辦實體活動。今年超過 600 位報名。(實際約 300 ~ 400 人到場)

議程共有 8 軌同時實體線上進行

1. Cloud
2. 資安
3. Machine Learning
4. Web + DevOps
5. Mobile
6. WTM (Woman Techmakers 女性技術發展)
7. GDSC
8. Workshops

[GDG DevFest 2022 Taipei]: https://gdg.community.dev/events/details/google-gdg-taipei-presents-devfest-2022-taipei/



### Objectives 目標 效益

* O: 參與社群、建立連結、實質貢獻
* Expectation: 行前目的 & 自我期許
* Build: 多學習如何建立社群, 安排活動, 促進凝聚力
* Connect: 多認識議程講者 & 工作人員, 承先啟後
* Contribute: 多思考可以如何貢獻

### KRs 成果

* [x] 認識 N > 5 DevOps / Cloud 講者 => N = 2 (Shawn, Edward)
* [x] 認識 N > 10 工作人員 => (Kevin, Meg, Hank) & GDSC Lead (3 + 5)
* 實際貢獻記錄
* 機動組: 組織調度報到台 9 軌流程動線與分流引導
* 議程攝影、引導、場佈場復
* 600+ 人報名, 實際約 300 ~ 400 人到場

## 🙋 機動組志工心得

* 行前準備
  * [行前說明會](https://docs.google.com/presentation/d/1pcHY-6Rru79ct_wOkkrb87ZuljcGrb21kYvbwkD_lh8/edit?usp=sharing) 使用 Google Meet + Google Slide 說明 & 自我介紹
  * 結果今年剛好志工幾乎都是 GDSC 的學生，我根本來拉高年齡平均的 😂
  * 但是能夠認識年輕朋友的感覺很不錯! 可以瞭解到大家在意的不同角度
* 當天活動內容 & 回想 & 下次可以多注意改進的部分
  * [GDG DevFest Taipei 2022 - Google 相簿](https://photos.app.goo.gl/v4QhBTGn9qnQYjsd8 "https://photos.app.goo.gl/v4QhBTGn9qnQYjsd8")
  * 07:20 到學校 ~~唸書的時候都沒這麼早到~~
  * 雖然報到時一度很混亂, 但最後還是大家一起協助順暢協助報到了~ 👏
    * 報到桌布置動線
    * 報到名單僅 9 份; QR Code 掃描機僅一台
    * 約有 30 位欲現場報名但網站已關
  * 議程偶有 投影畫面/接觸不良、直播沒聲音等突發狀況
  * 場佈場復時不太有人清楚什麼東西該跟誰拿 & 放哪
  * 指令系統不一致, 不容易確定當下該做些什麼
  * 18:00 ~ 21:00 晚宴在小樹屋吃 PAPAGO 外匯聊天。好久沒參加社群了, 很有感!

## 🔒 How to secure your software supply chain from dependencies to deployment

* Speaker: Edward Chuang (Googler)
* Software Delivery Shield
* 資安左移 = 風險 & 成本降低
  * CVE 快速盤點, 快速知道有沒有危害
  * 有沒有政策& CICD 快速確認 惡意程式 被部署
  * 做 app security = 軟體漏洞風險的影響高 「不能相信外面都壞人 裡面都好人」
* 符合 [SLSA](https://www.ithome.com.tw/news/145101) level 3
* Cloud workstation = fully managed development environments
* Cloud Code = Security assistance in the IDE
* Artifact Registry + Assured OSS = improving security of artifacts and dependencies. 在背景不定時做弱掃
* GKE + Cloud Run = Security insight at the runtime
* Binary authorization = Trust based policy. 確認是否包含 走過正常流程才會有的 簽章
* Ref: [近兩年更多臺廠加入成為CVE編號管理者，涵蓋網通、IC設計、資安等類型廠商](https://www.ithome.com.tw/news/154501)
  * 聯發科針對旗下各產品線均已設立專屬PSIRT團隊，加入MITRE CNA計畫的主要目的，是希望更迅速掌控安全性問題，更即時完成漏洞修補。
  * 展現積極正面看待安全事件處理的態度，並提及收到外部安全事件通報時，要落實五大步驟，包括：事件確認、修補、更新、公告與致謝。

## 🤖 WYSIWYG 容器的 Config As Data - KPT

* Speaker: Shawn 何宗憲(Googler)
* IaC: terraform, pulumi
* KPM: Helm, kustomize.io
* crossplane

## 🦄 GDG, GDE, GDSC

* [GDG Taipei](https://gdg.community.dev/gdg-taipei/) - GDG Taipei (Google Developer Group Taipei) 是以研究 Google 相關技術為主的開發者社群，於週三晚上聚會，由與會者提供數個 Lightening Talk，並不定期邀請講者分享特定主題、舉辦 Hackthon 或 Workshop 等活動。
* [為什麼你應該申請成為Google Developers Experts (GDE)](https://ericsk.medium.com/為什麼你應該申請成為-google-developers-experts-gde-58cf7c361f62) - GDE 全名 [Google Developers Experts](https://developers.google.com/experts)，它是眾多 Google 針對開發人員所設計的計劃之一，這個計劃將認可 (recognize) 開發人員在某一個專業領域所鑽研的深度，以及他願意把這項專業透過各種方式分享或推廣給其它開發人員的熱情，除了給予一個 GDE 的頭銜之外，也透過各種活動或獎勵（下面會詳述）來感謝 GDEs 們的付出，同時也鼓勵繼續鑽研技術與發揮影響力。
* [Google Cloud Innovators](https://cloud.google.com/innovators?hl=zh-tw) - Innovators 計畫是一項免費計畫，適用於 Google Cloud (包括 Workspace) 的使用者，或是任何有意在數位轉型方面提升專業與個人發展的使用者，藉此推動革新及解決一些現今最棘手的業務挑戰。身為 Innovators 計畫成員，您有機會與 Google Cloud 的創新人士網路交流並分享想法、加入即時討論、直接聽取 Google 員工的意見回饋、使用獨特的學習機會，以及獲得技能肯定，還能讓您輕鬆將數位技能徽章上傳並分享至個人資料。
* [Google Cloud Skills Boost](https://www.cloudskillsboost.google/) - Choose your path, build your skills, and validate your knowledge with Google Cloud.
* GDSC
  * [TW/HK 2022 Google 學生開發者社群（GDSC）領袖招募說明會](https://www.youtube.com/watch?v=CLjVUEl-XsM&t=537s)
  * Lead 任期一年, 目前是各個 Lead 自行決定整年在自己學校的議程與活動. 有些是像社課, 可能每週都有; 也有一些是更大型的活動
  * 一般在校園內辦的, 題目以 UI/UX, Low-Code/No-Code 的場次會吸引到更多人來聽

## Murmur

* 2022-12-03: 好久沒有這麼早到台大... 以前唸書都沒這麼認真😂
* 2022-12-11: 調整 mobile-friendly 格式 (減少列點縮排)
