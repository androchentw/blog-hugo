---
title: "Google SRE Books"
url: /google-sre-books
date: 2021-07-11T00:58:14+08:00
author: androchentw
type: post
series: google-sre-books
categories:
  - tech
  - google-sre-books
tags: 
  - tech
  - sre
  - devops
  - bigdata
  - read
share_img: https://lh3.googleusercontent.com/A-7rSIEgq-hwTETYDdYrcDQ6sftGmy0-a0LkQyvt2lrFy2p7QejyOGxhaCKDM74KmYqhqRkw63eCVfJFssRa023x0suoEgdOMZv9
---

![share_img](https://lh3.googleusercontent.com/A-7rSIEgq-hwTETYDdYrcDQ6sftGmy0-a0LkQyvt2lrFy2p7QejyOGxhaCKDM74KmYqhqRkw63eCVfJFssRa023x0suoEgdOMZv9)

## Intro

Google 推行 SRE 也已經好一陣子, 十分認同其中的各種想法與作法. 最近終於能有機會好好整理讀書心得筆記, 持續學習.

因為內容很多, 所以打算以系列文的方式, 不定期地更新內容, 這篇會作為 Summary 使用. 一來紀錄緣由, 二來追蹤進度.

### Challenges

1. **Hybrid Cloud Environment Complexity Grows**. 身為 IT, 在 Hybrid Cloud 環境與 Micro-service 趨勢下, 帶來的是更多的 Dependency 以及更為複雜的資料流. 
2. **Hard to Prove and Maintain Reliability**. 在設計 Data Pipeline 的過程中, 除了最終要 Deliver Data to Value 以達到 Business Impact 外, 更需要確保每天的 Data & Services Quality & Reliability, 甚至可以說是服務上線後天天都會遇到的事.
3. **Often Without Clear Value Proposition**. 而這些日常維運繁瑣的事務其實有很多可以用工程手段解決/自動化的部分, 但是卻非常容易在繁忙且接踵而來的專案下, 不自覺地疏忽了. 
4. **Prioritize ITOps Tasks**: 為了及早發現及早還技術債, 應該更有意識地持續分析: 
   1. 哪些該先做, 成本效益最佳? 
   2. 鎖定目標後, 又該如何實作, 才能真的事半功倍?
   3. 實作完成後, 如何良好衡量優化效益?

### Objectives

* Learn from Google SRE books
  * then introduce and continuously implement and improve current data services design reliability at work. 

### KRs

1. 2021-12 完讀 [The Site Reliability Workbook](https://sre.google/workbook/table-of-contents/) (實作細節, 實例)
2. 2021-12 完讀 [Site Reliability Engineering](https://sre.google/sre-book/table-of-contents/) (概念, 文化)

<!--more-->

## Index

因為兩本書的內容多有重疊, 目前我打算以 workbook 實例為主, sre-book 概念為輔, 統整內容.

### I. Foundation & Principles
1. Eliminating Toil
2. SLO
3. Monitoring

### II. Practices
1. Incidents
2. Postmortem Culture: Learning from Failure
3. Data Processing Pipelines
4. Configuration Design and Best Practices

### III. Processes & Management
1. SRE Engagement Model
2. SRE Team Lifecycles, Communication and Collaboration in SRE

### IV. Conclusion


### The Site Reliability Workbook

![workbook](https://lh3.googleusercontent.com/A-7rSIEgq-hwTETYDdYrcDQ6sftGmy0-a0LkQyvt2lrFy2p7QejyOGxhaCKDM74KmYqhqRkw63eCVfJFssRa023x0suoEgdOMZv9)

[The Site Reliability Workbook](https://sre.google/workbook/table-of-contents/)

* 實作細節, 實例

1. Part I - Foundations
2. Part II - Practices
3. Part III - Processes
4. Conclusion



### Site Reliability Engineering

![sre-book](https://lh3.googleusercontent.com/JvM0JKKuZNJMWAC5iZPm4j-mdS9ORpZbpEWzg0zmJ0i2_xgIcju0OLXJ-zmnvz_GtFFGHe9qZ9Dz-6W0u5fRLFQaRlOI_hGzbetw)

[Site Reliability Engineering](https://sre.google/sre-book/table-of-contents/)

* 概念, 文化

1. Part I - Introduction
2. Part II - Principles
3. Part III - Practices
4. Part IV - Management
5. Part V - Conclusions


## Ref

* [SRE / DevOps Taiwan 讀書會](https://study-area.sre.tw/01_SRE/CH01/)


## Murmur

* 2021-07-11. 學無止盡! 科技來自於人性... 懶就是一切的原動力 😎

