---
title: "Setup Blog Hugo"
url: /setup-blog-hugo
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
