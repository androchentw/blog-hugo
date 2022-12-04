---
title: "GDG DevFest 2022 Taipei"
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
share_img: https://res.cloudinary.com/startup-grind/image/upload/c_fill,dpr_2.0,f_auto,g_center,h_1080,q_100,w_1080/v1/gcs/platform-data-goog/events/tiapei-Bevy-EventThumb%402x.png
series: tech-event
---

<img style="width:60%;" src="https://res.cloudinary.com/startup-grind/image/upload/c_fill,dpr_2.0,f_auto,g_center,h_1080,q_100,w_1080/v1/gcs/platform-data-goog/events/tiapei-Bevy-EventThumb%402x.png">

## Overview 概述

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

[GDG DevFest Taipei]: https://gdg.community.dev/events/details/google-gdg-taipei-presents-devfest-2022-taipei/

<!--more-->

### Objectives 目標 效益

* O: 參與社群、建立連結、實質貢獻
* Expectation: 行前目的 & 自我期許
  * Build: 多學習如何建立社群, 安排活動, 促進凝聚力
  * Connect: 多認識議程講者 & 工作人員, 承先啟後
  * Contribute: 多思考可以如何貢獻

### KRs 成果

* [-] 認識 N > 5 DevOps / Cloud 講者 => N = 2 (Shawn, Edward)
* [-] 認識 N > 10 工作人員 => (Kevin, Meg, Hank) & GDSC Lead (3 + 5)
* 實際貢獻記錄
  * 組織調度報到台 9 軌流程動線與分流引導
  * 議程攝影、引導、場佈場復
  * 600 人報名, 實際約 300 ~ 400 人到場

##  心得記錄

* 2022-11-19 起心動念: 一直都想參與社群, 終於在 11-16 ☁️ [Google Cloud Next Recap](https://event.e21magicmedia.com.tw/Google/CloudNextRecap/?eid=kw0icz6nYsRr)的時候去找 GDG 攤位聊天，然後就主動報名參加志工了
* 行前準備
  * [行前說明會](https://docs.google.com/presentation/d/1pcHY-6Rru79ct_wOkkrb87ZuljcGrb21kYvbwkD_lh8/edit?usp=sharing) 使用 Google Meet + Google Slide 說明 & 自我介紹
  * 結果今年剛好志工幾乎都是 GDSC 的學生，我根本來拉高年齡平均的 😂
* 當天活動內容 & 回想
  * [GDG DevFest Taipei 2022 - Google 相簿](https://photos.app.goo.gl/v4QhBTGn9qnQYjsd8 "https://photos.app.goo.gl/v4QhBTGn9qnQYjsd8")
  * 07:20 到學校 ~~唸書的時候都沒這麼早到~~
  * 雖然報到時一度很混亂, 但最後還是大家一起協助順暢協助報到了~
    * 報到桌布置動線
    * 報到名單僅 9 份; QR Code 掃描機僅一台
    * 約有 30 位欲現場報名但網站已關
  * 議程也蠻常有 投影畫面/接觸不良、直播沒聲音等突發狀況
  * 場佈場復時沒人清楚什麼東西該跟誰拿 & 放哪
  * 指令系統不一致
  * 18:00 ~ 21:00 晚宴在小樹屋吃 PAPAGO 外匯聊天。好久沒參加社群了, 很有感!

## 🔒 How to secure your software supply chain from dependencies to deployment

* Speaker: Edward Chuang (Googler)
* Software Delivery Shield
  * 資安左移 = 風險 & 成本降低
    * CVE 快速盤點, 快速知道有沒有危害
    * 有沒有政策& CICD 快速確認 惡意程式 被部署
    * 做 app security = 軟體漏洞風險的影響高 「不能相信外面都壞人 裡面都好人」
  * 符合[SLSA](https://www.ithome.com.tw/news/145101) level 3
  * Cloud workstation = fully managed development environments
  * Cloud Code = Security assistance in the IDE
  * Artifact Registry + Assured OSS = improving security of artifacts and dependencies. 在背景不定時做弱掃
  * GKE + Cloud Run = Security insight at the runtime
  * Binary authorization = Trust based policy. 確認是否包含 走過正常流程才會有的 簽章

## 🤖 WYSIWYG 容器的 Config As Data - KPT

* Speaker: Shawn 何宗憲(Googler)
* IaC: terraform, pulumi
* KPM: Helm, kustomize.io
* crossplane

## Ref

* <https://www.ithome.com.tw/news/154501>
  * 聯發科針對旗下各產品線均已設立專屬PSIRT團隊，加入MITRE CNA計畫的主要目的，是希望更迅速掌控安全性問題，更即時完成漏洞修補。
  * 展現積極正面看待安全事件處理的態度，並提及收到外部安全事件通報時，要落實五大步驟，包括：事件確認、修補、更新、公告與致謝。

* <https://cloud.google.com/innovators?hl=zh-tw>

## Murmur

* 2022-11-20:
* 2022-12-03: 好久沒有這麼早到台大... 以前唸書都沒這麼認真😂
