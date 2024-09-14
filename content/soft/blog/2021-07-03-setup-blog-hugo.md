---
title: "Setup Blog Hugo"
url: setup-blog-hugo
date: 2021-07-03T20:51:44+08:00
author: androchentw
type: post
categories:
  - soft
tags:
  - blog
share_img: https://d33wubrfki0l68.cloudfront.net/c38c7334cc3f23585738e40334284fddcaf03d5e/2e17c/images/hugo-logo-wide.svg
series: blog
---

<img style="width:40%;" src="https://d33wubrfki0l68.cloudfront.net/c38c7334cc3f23585738e40334284fddcaf03d5e/2e17c/images/hugo-logo-wide.svg">

Step by step Setup Hugo Blog

終於從 ghost 搬來 Hugo 啦

<!--more-->

## 1. Setup github page: project

<https://androchentw.github.io/blog-hugo/>

```sh
git clone https://github.com/androchentw/blog-hugo.git
```

## 2. Install Hugo

* [Hugo - Quick Start](https://gohugo.io/getting-started/quick-start/)
* [Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

```sh
brew install hugo
hugo new site blog-hugo
cd blog-hugo
git submodule add https://github.com/androchentw/blog-theme.git themes/beautifulhugo
echo 'theme = "beautifulhugo"' >> config.toml

hugo new posts/hello_world.md

# to preview at http://localhost:1313/
hugo server -D 

# to build static page
hugo -D
```

## 3. Setup GitHub Action

* [深入但不淺出，如何用 github actions 自動發佈 gh-pages](https://milkmidi.medium.com/深入但不淺出-如何用-github-actions-自動發佈-gh-pages-8183464dfe84)
* [從零開始: 用github pages 上傳靜態網站](https://medium.com/進擊的-git-git-git/從零開始-用github-pages-上傳靜態網站-fa2ae83e6276)
[About GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#user--organization-pages)

## 4. Add Comment Block - utterances

2022-11-19 Added.

* [blog-theme: 3f81f19](https://github.com/androchentw/blog-theme/commit/3f81f194e9a688982a5ed0466f3f5da5e1d2863c)
* [blog-hugo: d47f631](https://github.com/androchentw/blog-hugo/commit/d47f631ab84d042a10f1903730f8c51ff8316750)

* [GitHub - utterances](https://github.com/utterance/utterances)
* [如何在hugo上安裝utterances?](https://bjmqfg83.github.io/blog/hugo_unnerances/)
* [Hugo 插件 Utterances 用法](https://xwi88.com/hugo-plugin-utterances-usage/)

## References

1. [將部落格從 Wordpress 轉換到 Hugo](https://blog.wu-boy.com/2021/05/migrate-wordpress-to-hugo/)
2. [ghostToHugo](https://dwmkerr.com/migrating-from-ghost-to-hugo/)
3. [Hugo - Front Matter](https://gohugo.io/content-management/front-matter/)
4. [Hugo - Archetypes](https://gohugo.io/content-management/archetypes/)
5. [Hugo - URL Management](https://gohugo.io/content-management/urls/)
6. [Hugo 加入 Google Custom Search 站內搜尋功能](https://blog.uncletony.tw/2021/03/hugo_%E5%8A%A0%E5%85%A5%E6%90%9C%E5%B0%8B%E5%8A%9F%E8%83%BD/)
7. [如在 Github Pages 建立 Hugo 靜態網站](https://kaichu.io/posts/my-first-post/)
8. [我的 Hugo 工作流程](https://www.ernestchiang.com/zh/posts/2021/my-hugo-workflow/)

## 2023-04-15 i18n 作法記錄

* url = {lang}/post. 預設中文: /blog-1, /en/blog-1, /ja/blog-1
  * ✅ 改用 url:, 而非 url:  => 正確! 有 {lang}/{post}
  * ❌ 改用 slug, 而非 url:  => 會變這樣 <http://localhost:1313/post/life/blog/blog-1>
* 每篇 post 正確要有類似 "翻訳：繁體中文・English"
  * ✅ 把 en/ 放到 post/en/ 跟 zh-tw 對齊 => 正確! 有 "翻譯"

### Ref

1. Hugo 官網
   1. [Multilingual Mode](https://gohugo.io/content-management/multilingual)
   2. [URL Management](https://gohugo.io/content-management/urls/)
      1. multilingual site
   3. [Sections](https://gohugo.io/content-management/sections/)
   4. [Archetypes](https://gohugo.io/content-management/archetypes/)
   5. 在每一篇 md 裡有指定的 `type: post`
   6. [Taxonomies](https://gohugo.io/content-management/taxonomies/)
   7. [Add Sub Menu in Hugo Website](https://codingnconcepts.com/hugo/nested-menu-hugo/)
   8. [Lists of Content in Hugo](https://gohugo.io/templates/lists/)
2. [Theme - Beautifulhugo (我使用的)](https://github.com/halogenica/beautifulhugo/blob/master/i18n/zh-TW.yaml)
   1. [blog-theme](https://github.com/androchentw/blog-theme/blob/main/i18n/zh-TW.yaml)
   2. [Locales - zh, zh_Hant, zh_Hant_TW](https://github.com/gohugoio/locales)
3. [Hugo 論壇](https://discourse.gohugo.io/search?q=zh%20chinese)
   1. [zh-tw](https://discourse.gohugo.io/t/is-it-good-idea-to-use-tw-instead-of-zh-tw-in-i18n/39088/4)
