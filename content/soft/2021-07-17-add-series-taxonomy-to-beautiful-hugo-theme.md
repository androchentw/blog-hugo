---
title: "Add Series Taxonomy to Beautiful Hugo Theme"
url: /add-series-taxonomy-to-beautiful-hugo-theme
date: 2021-07-17T15:47:50+08:00
author: androchentw
type: post
categories:
  - tech
tags:
  - tech
  - blog
  - hugo
share_img: https://i.imgur.com/S8CwQqI.png
series: blog-hugo
---

<img style="width:80%;" src="https://i.imgur.com/S8CwQqI.png">

## Overview

原本是看到這個 Series 操作就覺得蠻生火的: [Add Series Taxonomy to Hugo Theme](https://www.kiroule.com/article/add-series-taxonomy-to-hugo-theme/), 剛好拿來當練習~


### Challenges

1. Profile: Tech Blogger
2. Jobs
   1. Post great articles with friendly reading experience
   

### Objectives

1. Achieve better reading exprience with better blog post structure

### KRs

1. 2021-07 Implement `Series` feature on Hugo blog theme

<!--more-->

## Content

* [androchentw/blog-theme](https://github.com/androchentw/blog-theme) commit: [feat: add series implementation](https://github.com/androchentw/blog-theme/commit/3dbf0ac244cec5c7a1bdca661d795e81f3516439)
* [Add Series Taxonomy to Hugo Theme](https://www.kiroule.com/article/add-series-taxonomy-to-hugo-theme/)


### Voilà

* [Series List](https://blog.androchen.tw/series/) 
  <img style="width:80%;" src="https://i.imgur.com/S8CwQqI.png">


* Embed in post
  <img style="width:80%;" src="https://i.imgur.com/1aMj8ZL.png">




### Hugo Template 語法

  * [Introduction to Hugo Templating](https://gohugo.io/templates/introduction/)
  * [Go 模板啟蒙讀本](https://bwaycer.github.io/hugo_tutorial.hugo/templates/go-templates/)
  * [Hugo模板的基本語法](https://hugo.aiaide.com/post/hugo%E6%A8%A1%E6%9D%BF%E7%9A%84%E5%9F%BA%E6%9C%AC%E8%AF%AD%E6%B3%95/)
  * [Hugo 不完美教程 - V: Templates 模板机制](https://www.jianshu.com/p/e1f9123c721a)
  * [Hugo中定制Taxonomy页面](https://note.qidong.name/2017/10/hugo-taxonomy/)
  * [Lists of Content in Hugo - By Publish Date](https://gohugo.io/templates/lists/#by-publish-date)
  * [Taxonomy Templates - WeightedPages ](https://gohugo.io/templates/taxonomy-templates/#weightedpages)


### Git Submodule

* [Git Submodule 用法筆記](https://blog.chh.tw/posts/git-submodule/)

### Additional Modification


為 Hugo blog 的 SEO og:title 加上 Site.Title 的修改方法

* [feat: add $.Site.Title to SEO og:title](https://github.com/androchentw/blog-theme/commit/efabe56ac1b2317272d7a7319e162b5043969978)

```html
# themes/beautifulhugo/layouts/partials/seo/opengraph.html

{{- with .Title | default .Site.Title }}
<meta property="og:title" content="{{ $.Title }} | {{$.Site.Title }}" />
{{- end }}
```

## Murmur

* 2021-07-17 Template 語法讚啦

