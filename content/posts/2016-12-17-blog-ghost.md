---
title: "自架部落格 - 使用 Ghost 並設定自己的域名"
url: /blog-ghost
date: 2016-12-17T16:00:00Z
author: androchentw
type: post
categories:
  - Dev
tags: 
  - blog
---


2021-03-25

這次會重新用，可能是太久沒有升級導致超過 sunset, 過期了

改用這套來重新建 [https://github.com/SNathJr/ghost-on-heroku](https://github.com/SNathJr/ghost-on-heroku)

---

以下環境皆是 mac 。

先說清楚以下不是打廣告，只是記錄當初我找到的一些配套 & local 最佳解法，有更好者請告訴我～

* Blog platform: [Ghost](https://ghost.org/)
* Hosting: [Heroku](https://www.heroku.com/)
* Domain name: [水世界](http://host.waterworld.tw/)

以下簡單列一下選擇的原因

### Ghost

* CMS 可以寫 markdown (這對我來說是必備)
* 免費 (自架的話)
* 版面漂亮 (Casper)，也可自訂 HTML, CSS

這邊說明一下，markdown 是我個人的習慣，所以我只挑可以寫 markdown 的編輯器的 blog platform。其實前前後後用過了不少家的 blog, 也同時有 [Corner hack](http://androchen.logdown.com/) 是用 logdown。更之前還有用過 Wordpress, Google 的 Blogger, (無名算不算)。就都各有擅場囉。

### Heroku

* 免費
* 可以 run node.js code (為了配合 ghost)
* 用 git 管理 code。我懶懶的，就直接用 Heroku CLI 囉。

用 Heroku 會免費獲得一個 domain name，我是把 [https://blog-androchen.herokuapp.com/](https://blog-androchen-tw.herokuapp.com/) 再轉到自己的 [https://blog.androchen.tw/](/), 然後中間也有用 Cloudflare 額外加 ssl。

另外介紹一個 [Kaffeine](https://kaffeine.herokuapp.com/)。這東西很酷，會幫你不定時戳你的 herokuapp, 讓 heroku 覺得一直有人在訪問這個網頁，於是就不會 shut down 你的 app (若被 shut down 會花比較久時間才會醒來)

> pings your Heroku app every 30 minutes so it will never go to sleep

### 水世界

* 便宜
* 中文客服

之前最一開始就有跟他們家買過主機服務，那時候還不會用 heroku，還是只會用 ftp 的時代 (笑)。一來是好像都比 GoDaddy 便宜，二來是也有中文客服，而且他們的反應速度也都蠻快的(前前後後問了大概五個問題，都是在一天內會回答)

後來比較會用 Heroku 後，發現他們家的 domain name 也很便宜，就一次買了 10 年 3900 元的囉。只是說如果要自己設定轉址的話，一樣要登入會員，跟他們的客服留一下訊息，然後他就會給你一個網址讓你自己去設定 (設定過一次。。。有點麻煩，但就麻煩一次而已)。





