---
draft: true
title: "Discord Bot Playground"
url: /discord-bot-playground
# date: 2022-10-15T00:06:16+08:00
date: 2022-10-15T18:35:16+08:00
author: androchentw
type: post
categories:
  - tech
tags:
  - chatbot
share_img: https://images.unsplash.com/photo-1640367169401-534dec442631?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80
series: chatbot
---

<img style="width:60%;" src="https://images.unsplash.com/photo-1640367169401-534dec442631?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80">
<p align="center"><sub><sup>
  Photo by <a href="https://unsplash.com/@paman0744?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Aman Pal</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</sup></sub></p>

## Overview

### Challenges 現況 挑戰

* 一直想練習玩玩看 chatbot

### Objectives 目標 效益

* 學習並建立可快速擴充的 chatbot 框架

### KRs 成果

* [ ] 2022-10-16 MVP local discord bot

<!--more-->

## Materials

* [Top.gg - Discord Bots](https://top.gg/)
* 建立 FF14 資訊 Discord chatbot 系列
  * [[DAY 05]物品拍賣價格查詢功能(3/4)](https://ithelp.ithome.com.tw/m/articles/10268117)
  * [[DAY 10]讓BOT 24小時在線(1/3)](https://ithelp.ithome.com.tw/m/articles/10271672)
* GCP
  * [GCP + Discord](https://cloud.google.com/blog/topics/developers-practitioners/build-and-run-discord-bot-top-google-cloud)
  * [free tier hosting: GCE](https://ithelp.ithome.com.tw/articles/10276289?sc=iThomeR)
    * [VPC (一)](https://ithelp.ithome.com.tw/articles/10262895)
    * [第一次開 GCP VM 就上手！Compute Engine 開機教學](https://blog.cloud-ace.tw/infrastructure/vm/start-a-google-vm-compute-engine/)
    * [開 GCP VM 要注意什麼？Compute Engine 開機詳細教學](https://blog.cloud-ace.tw/infrastructure/vm/gcp-tutorial-first-google-vm-attention-please/)
    * [教學 如何使用 Google Cloud Storage 建立靜態網站](https://ikala.cloud/cloud-storage-application-website/)
  * [Serverless cloud function](https://www.maxlist.xyz/2022/02/01/discord-bot-with-gcp/)

## 場景

* Chatbot 指令 串 API 做事
  * 每日提醒
  * 資料寫入
  * 網頁資料蒐集
* 比較: 暫時選 discord
  * 免費版 Slack 10k msg 上限, 搜尋紀錄 30 天
    * Slack 優勢
      * Business 導向
      * 可送 voice / video recording
      * 搜尋可選 reaction
  * 社群導向, [第三方 bot](https://top.gg/) 直接裝

## Architecture Planning

<https://github.com/kslifer/wordpress-on-gcp-free-tier>
<https://github.com/androchentw/diagrams-res/blob/main/blog/2022-10-15-GCP-Dev-Portal-Plan.svg>

## Dev

* [Discord.py](https://github.com/Rapptz/discord.py)

### ngrok

* <https://5xruby.tw/posts/easy-ngrok-by-nginx-ssh-tunnel>
* <https://learn.markteaching.com/ngrok-webhook/>

## Murmur

* 2022-10-14 一直挖坑給自己跳 😂
