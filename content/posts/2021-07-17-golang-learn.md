---
title: "Golang Learn"
url: /golang-learn
date: 2021-07-17T10:13:58+08:00
author: androchentw
type: post
categories:
  - tech
tags: 
  - tech
  - golang
share_img: https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Go_Logo_Blue.svg/440px-Go_Logo_Blue.svg.png
series: golang-learn
---

<img style="width:40%;" src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Go_Logo_Blue.svg/440px-Go_Logo_Blue.svg.png">

## Intro

[從 Ghost 搬來 Hugo 後](https://blog.androchen.tw/setup-blog-hugo/), 終於更積極地回歸 blog 了... 今天要來立下學 golang 的 flag 😂 

作為新手, 條列一些觀察與期許


### Challenges

1. Profile: Data Engineer
2. Jobs
   1. Deliver data to value by designing and implementing data pipeline 
   2. Maintain operations and continuously improve service levels


### Objectives

1. Master 1 programming language to better understand the mechanism and principle of Dev & Ops .
2. Manage Ops in software engineering way like [`class SRE implements DevOps`](https://blog.androchen.tw/google-sre-books/). 


### KRs

1. 2021-08 Complete [Go by Example](https://gobyexample.com/) and get familiar with VS Code extensions.
2. 2021-09 Setup lightweight web server with modern frontend and backend framework to handle form input, api and authentication.

<!--more-->

## Content

### More about Why Golang

1. Statically-typed 

先前是寫 Android 起家, Java 有許多為人所詬病之處, 在 java 8 之際有嚐到一點 lambda 的甜頭, 可惜來不及參與到 Kotlin 的盛況就跑去做 Data Engineering 了 😂. 但是也發現自己還是鍾情這種 Statically-typed  的性質. 以下這段可以說是深得我心: [A Data Engineering Perspective on Go vs. Python (Part 1)](https://chollinger.com/blog/2020/06/a-data-engineering-perspective-on-go-vs.-python-part-1/)

> When Go was designed, Java and C++ were the most commonly used languages for writing servers, at least at Google. We felt that these languages required too much bookkeeping and repetition. Some programmers reacted by moving towards more dynamic, fluid languages like Python, at the cost of efficiency and type safety. We felt it should be possible to have the efficiency, the safety, and the fluidity in a single language.


2. DevOps Friendly

加上做資料分析, 監控等也一陣子了, 都能看見 go sdk 在各種主流框架的支援快速竄起, Kubernetes, Prometheus, Grafana 等. [Why Golang is DevOps' Top Programming Language in 2021](https://www.youtube.com/watch?v=7pLqIIAqZD4) 這支影片裡的論點直接打中我: "executable binary". 光是不用解 library dependency 就絕對足夠在 DevOps 混雜的環境中生存了 🤩


### Go Training

* 🧑🏻‍💻 [Go by Example](https://gobyexample.com/): hands-on introduction to Go using annotated example programs.
* [7 GitHub projects to make you a better Go Developer](https://dev.to/ankit01oss/7-github-projects-to-make-you-a-better-go-developer-2nmh)
  1. [Awesome Go](https://github.com/avelino/awesome-go): A curated list of awesome Go frameworks, libraries and software
  2. [Standard Go Project Layout](https://github.com/golang-standards/project-layout)
  3. [Go kit](https://github.com/go-kit/kit): A standard library for microservices.
  4. [Go Design patterns](https://github.com/tmrts/go-patterns): Curated list of Go design patterns, recipes and idioms
  5. 🧑🏻‍💻 [Learn Go with test-driven development](https://github.com/quii/learn-go-with-tests)
  6. 🧑🏻‍💻 [The Ultimate Go Study Guide](https://github.com/ardanlabs/gotraining)
  7. [1000+ Hand-crafted Go examples, exercises and quizzes](https://github.com/inancgumus/learngo)
* [Go Wiki](https://github.com/golang/go/wiki/Learn)
* [go-training/training](https://github.com/go-training/training)


### VS Code Extension

* [Visual Studio Code 安裝及插件推薦](https://morosedog.gitlab.io/golang-20201028-golang-2/)
* [50 VS Code themes for 2020](https://dev.to/thegeoffstevens/50-vs-code-themes-for-2020-45cc)
* [What Are the Most Popular VS Code Themes?](https://visualstudiomagazine.com/articles/2021/07/07/vs-code-themes.aspx): [Material Icon Theme](https://github.com/PKief/vscode-material-icon-theme)
* [go-training/workshop-20201111](https://github.com/go-training/workshop-20201111/blob/main/01-setup-env/vscode/settings.json)

### Gin & Frontend

* [Gin - 好用的 web framework](https://ithelp.ithome.com.tw/articles/10234075), [Gin框架搭配模板](https://ithelp.ithome.com.tw/articles/10222711)
* [awesome-gin](https://github.com/FlowerWrong/awesome-gin)
* [Gin 起步走（Getting Started）](https://pjchender.dev/golang/gin-getting-started/)
* [golang-gin-realworld-example-app/FRONTEND_INSTRUCTIONS.md](https://github.com/gothinkster/golang-gin-realworld-example-app/blob/master/FRONTEND_INSTRUCTIONS.md)
* [GOLANG TUTORIAL : INTRODUCTION GIN HTML TEMPLATE AND HOW INTEGRATION WITH BOOTSTRAP](https://hoohoo.top/blog/20210530112304-golang-tutorial-introduction-gin-html-template-and-how-integration-with-bootstrap/)
* [Bootstrap](https://getbootstrap.com/)
* [Semantic UI](https://semantic-ui.com/)
* [material-ui store](https://material-ui.com/store/)
* [Why Are You Still Creating CRUD Apis?](https://levelup.gitconnected.com/why-are-you-still-creating-crud-apis-8790ca261bfb)

## Murmur

* 2021-07-17 總覺得最近支線任務開得有點多...


## Series

{{< series "golang-learn" >}}
