---
title: "Raycast 6 招啟動工作生產力"
url: /raycast-6-tips-boost-productivity
# date: 2023-04-08T21:00:00+08:00
date: 2023-04-11T18:30:00+08:00
author: androchentw
type: post
categories:
  - soft
tags: 
  - productivity
share_img: https://github.com/androchentw/blog-hugo/blob/master/content/soft/productivity/2023-04-11-raycast-6-tips-boost-productivity-cover.png?raw=true
series: productivity
---

## Overview

<img style="width:60%;" src="https://github.com/androchentw/blog-hugo/blob/master/content/soft/productivity/2023-04-11-raycast-6-tips-boost-productivity-cover.png?raw=true">
<p align="center"><sub><sup>
  Raycast 6 招啟動工作生產力
</sup></sub></p>

先前分享過我使用的軟體，今天聚焦講講 Mac 上的萬能啟動器: Raycast。一路從 Alfred 換過來，超級滿意!

🤔 Q: 你常用的工作生產力軟體是什麼? 推薦用在什麼場景?

💪 A: 舉出 2 個生產力提升的改進方向。

<!--more-->

## 1. Mac OS 操作

1. Mac 操作 (sleep, 移動視窗位置 Window Management ...)
2. App open (開 iTerm, VS Code, Notion, OneNote, Craft, Miro, ...)
3. File open (f > filename; cmd + enter 開資料夾)

## 2. Snippet 貼上範本文字

1. 可以帶有一點格式 & placeholder (主要是時間)
2. 工作
   1. Meeting minute
   2. Milestone table
3. 生活
   1. 每日 Reflection
   2. ChatGPT Prompt book

舉例來說, 我的 meeting minute snippet 如下

```md
Hi all,

感謝今天的時間, 請參考以下記錄

## Meeting Goal

1. 範圍界定
2. 確認時程

## Meeting Follow-up {date "yyyy-MM-dd"}

1. [@A] 
2. [@B] 
3. [@C] 
```

## 3. 情境組合拳: Blog 知識產出

我在寫 Blog 基本上也已經離不開 Raycast 跟快捷鍵了 😂

1. 開 App: Craft, VS Code
2. Search Emoji 🥳
3. Snippet 貼上範本文字
4. TinyPNG: 壓縮圖片
5. 找圖: Unsplash, gif, 開應用 GIPHY CAPTURE 錄製 gif

## 4. 小技巧與 Extension 推薦

1. 關閉沒有使用的 Extensions
   1. 搜尋 Extension, 把 Enabled 反勾選
2. 設定 global 快捷鍵
   1. 特別常用的，可以設定全域快捷鍵
   2. `File search`: `cmd + ctrl + shfit + F`
   3. `Search Emoji`: `cmd + ctrl + shfit + E`
   4. `Search Snippet`: `cmd + ctrl + shfit + S`
3. Extension 推薦
   1. `Store`: 找自己喜歡的 extension
   2. `Calendar`: 看接下來的待辦
   3. `Search Emoji`: 比原生的好在有英文，看久了比較會記得

## 5. 進階: 串接客製 Script

最後大決就是自己串接客製化的 script。[GitHub 上有完整的指令大全](https://github.com/raycast/script-commands/tree/master/commands#craft)，以下是我看起來覺得蠻有趣的:

1. [Run Shell Command](https://github.com/raycast/script-commands/blob/master/commands/apps/iterm/iterm-run-shell-command.applescript): [iterm-run-shell-command.applescript](https://github.com/raycast/script-commands/blob/master/commands/apps/iterm/iterm-run-shell-command.applescript)
2. [Conversions](https://github.com/raycast/script-commands/tree/master/commands#conversions) 各種有用的轉換
   1. [QR Code Generation](https://github.com/raycast/script-commands/blob/master/commands/conversions/qrcode-generate.sh)
   2. [rich-text-clipboard-to-markdown](https://github.com/raycast/script-commands/blob/master/commands/conversions/rich-text-clipboard-to-markdown.sh)
   3. [create-markdown-table](https://github.com/raycast/script-commands/blob/master/commands/conversions/create-markdown-table.js)
3. [Developer Utils](https://github.com/raycast/script-commands/tree/master/commands#developer-utils)
   1. [Create .gitignore](https://github.com/raycast/script-commands/blob/master/commands/developer-utils/generate-git-ignore.sh)
   2. [Prettify JSON](https://github.com/raycast/script-commands/blob/master/commands/developer-utils/prettify-json.sh)
   3. [Time Between Dates](https://github.com/raycast/script-commands/blob/master/commands/developer-utils/time-between-dates.js)
   4. [Lighthouse](https://github.com/raycast/script-commands/blob/master/commands/developer-utils/google/google-lighthouse.sh)
4. [Navigation](https://github.com/raycast/script-commands/tree/master/commands#navigation)
   1. [Open Current Finder Directory in iTerm](https://github.com/raycast/script-commands/blob/master/commands/navigation/open-iterm-from-finder.applescript)
   2. [Open Current iTerm Directory in Finder](https://github.com/raycast/script-commands/blob/master/commands/navigation/open-finder-from-iterm.applescript)
5. [Productivity](https://github.com/raycast/script-commands/tree/master/commands#productivity)
    1. [Clipboard to Imgur](https://github.com/raycast/script-commands/blob/master/commands/productivity/imgur/imgur-upload-clipboard-image.template.sh)
    2. [Run OCR](https://github.com/raycast/script-commands/blob/master/commands/productivity/macocr/macocr-run-ocr.sh)

## 6. Windows Alternative

Windows 的部分, 之前是用 Launchy 跟 PowerToys。藉著這次機會也來試試:

1. [WoX](https://github.com/Wox-launcher/Wox)
2. [ueli](https://github.com/oliverschwendener/ueli)

## 你怎麼看?

留下你的想法一起討論吧! 🥳

延伸閱讀

1. [自然語言 SQL Client + Chatbot - AI 時代開發者工具 2.0](https://blog.androchen.tw/sqlchat-ai-developer-tools-2)
2. [OpenAI CEO Sam Altman 生產力 4 招解密](https://blog.androchen.tw/openai-ceo-sam-altman-productivity-4-tips)

### Murmur

* 2023-04-11: 快捷鍵魔人 💪
